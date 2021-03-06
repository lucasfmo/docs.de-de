---
title: "Lokale Transaktionen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ae3712f-ef5e-41a1-9ea9-b3d0399439f1
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Lokale Transaktionen
Transaktionen werden in [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] verwendet, wenn mehrere Aufgaben miteinander verbunden werden sollen, damit sie als eine einzelne Verarbeitungseinheit ausgeführt werden können.  Stellen Sie sich z.&\#160;B. vor, dass eine Anwendung zwei Aufgaben ausführt.  Zum einen aktualisiert sie eine Tabelle mit Bestellinformationen.  Zum anderen aktualisiert sie eine Tabelle mit Bestandsinformationen und bucht die bestellten Artikel ab.  Wenn eine der Aufgaben nicht ausgeführt werden kann, wird für beide Aktualisierungen ein Rollback durchgeführt.  
  
## Bestimmen des Transaktionstyps  
 Eine Transaktion wird als lokale Transaktion bezeichnet, wenn sie nur eine Phase hat und direkt von der Datenbank behandelt wird.  Transaktionen werden als verteilte Transaktionen bezeichnet, wenn sie von einem Transaktionsmonitor koordiniert werden und für die Transaktionsauflösung ausfallsichere Mechanismen verwenden \(z. B. Übergabe in zwei Phasen\).  
  
 Alle [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]\-Datenanbieter verfügen jeweils über ein eigenes `Transaction`\-Objekt für das Ausführen lokaler Transaktionen.  Wählen Sie eine <xref:System.Data.SqlClient>\-Transaktion, wenn eine Transaktion in einer SQL Server\-Datenbank ausgeführt werden muss.  Verwenden Sie für eine Oracle\-Transaktion den <xref:System.Data.OracleClient>\-Anbieter.  Zusätzlich gibt es eine neue <xref:System.Data.Common.DbTransaction>\-Klasse zum Schreiben von anbieterunabhängigem Code, der Transaktionen erfordert.  
  
> [!NOTE]
>  Transaktionen sind am effizientesten, wenn sie auf dem Server ausgeführt werden.  Wenn Sie mit einer SQL Server\-Datenbank arbeiten, die häufig explizite Transaktionen verwendet, empfiehlt es sich, die Transaktionen unter Verwendung der BEGIN TRANSACTION\-Anweisung von Transact\-SQL als gespeicherte Prozeduren zu schreiben.  Weitere Informationen zum Ausführen serverseitiger Transaktionen finden Sie in der Onlinedokumentation zu SQL Server.  
  
## Ausführen einer Transaktion unter Verwendung einer einzelnen Verbindung  
 In [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] können Sie Transaktionen mit dem `Connection`\-Objekt steuern.  Zum Initiieren einer lokalen Transaktion steht Ihnen die `BeginTransaction`\-Methode zur Verfügung.  Nachdem Sie eine Transaktion gestartet haben, können Sie mit der `Transaction`\-Eigenschaft eines `Command`\-Objekts einen Befehl in dieser Transaktion eintragen.  Dann können Sie für Änderungen an der Datenquelle auf Grundlage des Erfolgs oder Fehlschlags der Komponenten der Transaktion einen Commit oder Rollback ausführen.  
  
> [!NOTE]
>  Die `EnlistDistributedTransaction`\-Methode darf nicht für eine lokale Transaktion verwendet werden.  
  
 Der Gültigkeitsbereich der Transaktion ist auf die Verbindung beschränkt.  Im folgenden Beispiel wird eine explizite Transaktion ausgeführt, die aus zwei separaten Befehlen im `try`\-Block besteht.  Die Befehle führen INSERT\-Anweisungen für die Production.ScrapReason\-Tabelle in der AdventureWorks\-Beispieldatenbank von [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] aus. Für die Anweisungen wird ein Commit ausgeführt, wenn keine Ausnahmen ausgelöst werden.  Wenn eine Ausnahme ausgelöst wird, führt der Code im `catch`\-Block einen Rollback für die Transaktion aus.  Wenn die Transaktion abgebrochen oder die Verbindung geschlossen wird, bevor die Transaktion beendet wurde, wird automatisch ein Rollback für die Transaktion ausgeführt.  
  
## Beispiel  
 Führen Sie diese Schritte aus, um eine Transaktion auszuführen:  
  
1.  Rufen Sie die <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A>\-Methode des <xref:System.Data.SqlClient.SqlConnection>\-Objekts auf, um den Start der Transaktion festzulegen.  Die <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A>\-Methode gibt einen Verweis auf die Transaktion zurück.  Dieser Verweis wird den <xref:System.Data.SqlClient.SqlCommand>\-Objekten zugeordnet, die in der Transaktion eingetragen sind.  
  
2.  Weisen Sie das `Transaction`\-Objekt der <xref:System.Data.SqlClient.SqlCommand.Transaction%2A>\-Eigenschaft des auszuführenden <xref:System.Data.SqlClient.SqlCommand> zu.  Wenn ein Befehl für eine Verbindung mit einer aktiven Transaktion ausgeführt wird und das `Transaction`\-Objekt nicht der `Transaction`\-Eigenschaft des `Command`\-Objekts zugewiesen wurde, wird eine Ausnahme ausgelöst.  
  
3.  Führen Sie die erforderlichen Befehle aus.  
  
4.  Rufen Sie die <xref:System.Data.SqlClient.SqlTransaction.Commit%2A>\-Methode des <xref:System.Data.SqlClient.SqlTransaction>\-Objekts auf, um die Transaktion abzuschließen, oder rufen Sie die <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A>\-Methode auf, um die Transaktion zu beenden.  Wenn die Verbindung vor dem Ausführen der <xref:System.Data.SqlClient.SqlTransaction.Commit%2A>\-Methode oder der <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A>\-Methode geschlossen oder verworfen wurde, wird für die Transaktion ein Rollback ausgeführt.  
  
 Im folgenden Codebeispiel wird die Transaktionslogik unter Verwendung von [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] mit Microsoft SQL Server veranschaulicht.  
  
 [!code-csharp[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/VB/source.vb#1)]  
  
## Siehe auch  
 [Transaktionen und Parallelität](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)   
 [Verteilte Transaktionen](../../../../docs/framework/data/adonet/distributed-transactions.md)   
 [System.Transactions\-Integration in SQL Server](../../../../docs/framework/data/adonet/system-transactions-integration-with-sql-server.md)   
 [ADO.NET Verwaltete Anbieter und DataSet\-Entwicklercenter](http://go.microsoft.com/fwlink/?LinkId=217917)