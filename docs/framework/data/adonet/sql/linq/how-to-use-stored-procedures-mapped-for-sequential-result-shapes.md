---
title: "Vorgehensweise: Verwenden von gespeicherten Prozeduren, die sequenziellen Ergebnisformen zugeordnet sind | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a73530de-5a4e-4d9c-8d66-abb19c225b11
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Vorgehensweise: Verwenden von gespeicherten Prozeduren, die sequenziellen Ergebnisformen zugeordnet sind
Diese Art von gespeicherten Prozeduren kann mehr als eine Ergebnisform erstellen. Sie wissen jedoch, in welcher Reihenfolge die Ergebnisse zurückgegeben werden.  Stellen Sie dieses Szenario dem Szenario gegenüber, bei dem Sie die Rückgabereihenfolge nicht kennen.  Weitere Informationen finden Sie unter [Vorgehensweise: Verwenden gespeicherter Prozeduren für mehrere Ergebnisformen](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-stored-procedures-mapped-for-multiple-result-shapes.md).  
  
## Beispiel  
 Es folgt das T\-SQL einer gespeicherten Prozedur, die mehrere Ergebnisformen sequenziell zurückgibt:  
  
```  
CREATE PROCEDURE MultipleResultTypesSequentially  
AS  
select * from products  
select * from customers  
```  
  
 [!code-csharp[DLinqSprox#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#6)]
 [!code-vb[DLinqSprox#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#6)]  
  
## Beispiel  
 Um die gespeicherte Prozedur auszuführen, wird in etwa der folgende Code verwendet.  
  
 [!code-csharp[DLinqSprox#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/Program.cs#7)]
 [!code-vb[DLinqSprox#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/Module1.vb#7)]  
  
## Siehe auch  
 [Gespeicherte Prozeduren](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)