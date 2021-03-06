---
title: "Konvertieren eines Typs in eine generische IEnumerable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 64774fb5-7447-4296-ad3b-8a94346f99a1
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Konvertieren eines Typs in eine generische IEnumerable
Verwenden Sie <xref:System.Linq.Enumerable.AsEnumerable%2A>, um das als generische `IEnumerable` eingegebene Argument zurückzugeben.  
  
## Beispiel  
 In diesem Beispiel würde [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] \(mit der generischen Standard\-`Query`\) versuchen, die Abfrage in SQL zu konvertieren und auf dem Server auszuführen.  Die `where`\-Klausel verweist jedoch auf eine benutzerdefinierte clientseitige Methode \(`isValidProduct`\), die nicht in SQL konvertiert werden kann.  
  
 Die Lösung erfordert das Definieren der clientseitigen generischen <xref:System.Collections.Generic.IEnumerable%601>\-Implementierung von `where`, um das generische <xref:System.Linq.IQueryable%601> zu ersetzen.  Rufen Sie hierzu den <xref:System.Linq.Enumerable.AsEnumerable%2A>\-Operator auf.  
  
 [!code-csharp[DLinqQueryExamples#46](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#46)]
 [!code-vb[DLinqQueryExamples#46](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#46)]  
  
## Siehe auch  
 [Abfragebeispiele](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)