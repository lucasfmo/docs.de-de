---
title: "Oracle-REF&#160;CURSORs | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c6b25b8b-0bdd-41b2-9c7c-661f070c2247
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Oracle-REF&#160;CURSORs
Der .NET Framework\-Datenanbieter für Oracle unterstützt den Oracle\-Datentyp **REF CURSOR**.  Wenn Sie beim Arbeiten mit Oracle\-REF CUSORS diesen Datenanbieter verwenden, müssen Sie das jeweilige Verhalten berücksichtigen.  
  
> [!NOTE]
>  Das jeweilige Verhalten weicht von dem des Microsoft OLE DB\-Anbieters für Oracle \(MSDAORA\) ab.  
  
-   Aus Leistungsgründen bindet der Datenanbieter für Oracle, im Gegensatz zu MSDAORA, **REF CURSOR**\-Datentypen nur dann automatisch, wenn Sie sie explizit angeben.  
  
-   Der Datenanbieter unterstützt keine ODBC\-Escapesequenzen, auch nicht das {resultset}\-Escapezeichen für die Angabe von REF CURSOR\-Parametern.  
  
-   Wenn eine gespeicherte Prozedur ausgeführt werden soll, die REF CURSORs zurückgibt, müssen Sie die Parameter in der <xref:System.Data.OracleClient.OracleParameterCollection> mit einem auf **Cursor** festgelegten <xref:System.Data.OracleClient.OracleType> und einer auf **Output** festgelegten <xref:System.Data.OracleClient.OracleParameter.Direction%2A> definieren.  Mit diesem Datenanbieter können REF CURSORs nur als Ausgabeparameter gebunden werden.  Das Binden von REF CURSORs als Eingabeparameter wird von diesem Datenanbieter nicht unterstützt.  
  
-   Das Abrufen eines <xref:System.Data.OracleClient.OracleDataReader> aus dem Parameterwert wird nicht unterstützt.  Nach dem Ausführen des Befehls weisen die Werte den Typ <xref:System.DBNull> auf.  
  
-   Der einzige **CommandBehavior**\-Enumerationswert, der mit REF CURSORs verwendet werden kann \(z. B. beim Aufrufen von <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A>\), ist **CloseConnection**. Alle anderen Werte werden ignoriert.  
  
-   Die Reihenfolge der REF CURSORs im **OracleDataReader** richtet sich nach der Reihenfolge der Parameter in der **OracleParameterCollection**.  Die <xref:System.Data.OracleClient.OracleParameter.ParameterName%2A>\-Eigenschaft wird ignoriert.  
  
-   Der PL\/SQL\-Datentyp **TABLE** wird nicht unterstützt.  REF CURSORs sind im Vergleich effizienter.  Wenn Sie dennoch einen **TABLE**\-Datentyp verwenden müssen, verwenden Sie den .NET\-Datenanbieter für OLE DB mit MSDAORA.  
  
## In diesem Abschnitt  
 [REF CURSOR\-Beispiele](../../../../docs/framework/data/adonet/ref-cursor-examples.md)  
 Enthält drei Beispiele, in denen die Verwendung von REF CURSORs veranschaulicht wird.  
  
 [REF CURSOR\-Parameter in einem 'OracleDataReader'](../../../../docs/framework/data/adonet/ref-cursor-parameters-in-an-oracledatareader.md)  
 Veranschaulicht das Ausführen einer gespeicherten PL\/SQL\-Prozedur, die einen REF CURSOR\-Parameter zurückgibt. Der Wert wird als **OracleDataReader** gelesen.  
  
 [Abrufen von Daten aus mehreren REF CURSORs mithilfe eines OracleDataReader](../../../../docs/framework/data/adonet/retrieving-data-from-multiple-ref-cursors.md)  
 Veranschaulicht das Ausführen einer gespeicherten PL\/SQL\-Prozedur, die zwei REF CURSOR\-Parameter zurückgibt. Der Wert wird mithilfe eines **OracleDataReader** gelesen.  
  
 [Auffüllen eines "DataSets" mit einem oder mehreren REF CURSORs](../../../../docs/framework/data/adonet/filling-a-dataset-using-one-or-more-ref-cursors.md)  
 Veranschaulicht das Ausführen einer gespeicherten PL\/SQL\-Prozedur, die zwei REF CURSOR\-Parameter zurückgibt. Das <xref:System.Data.DataSet> wird mit den zurückgegebenen Zeilen aufgefüllt.  
  
## Siehe auch  
 [Oracle und ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)   
 [ADO.NET Verwaltete Anbieter und DataSet\-Entwicklercenter](http://go.microsoft.com/fwlink/?LinkId=217917)