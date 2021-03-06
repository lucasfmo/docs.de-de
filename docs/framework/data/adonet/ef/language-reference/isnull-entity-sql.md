---
title: "ISNULL (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: dc7a0173-3664-4c90-a57b-5cbb0a8ed7ee
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# ISNULL (Entity SQL)
Ermittelt, ob ein Abfrageausdruck den Wert NULL hat.  
  
## Syntax  
  
```  
  
expression IS [ NOT ] NULL  
```  
  
## Argumente  
 `expression`  
 Ein gültiger Abfrageausdruck. Dieser darf keine Auflistung sein oder über Auflistungsmember oder einen Datensatztyp mit Auflistungstypeigenschaften verfügen.  
  
 NOT  
 Negiert das EDM.Boolean\-Ergebnis von IS NULL.  
  
## Rückgabewert  
 `true` wenn `expression` NULL zurückgibt, andernfalls `false`.  
  
## Hinweise  
 Verwenden Sie `IS NULL`, um zu ermitteln, ob das Element einer äußeren Verknüpfung den Wert NULL hat:  
  
```  
select c   
      from LOB.Customers as c left outer join LOB.Orders as o   
                              on c.ID = o.CustomerID    
      where o is not null and o.OrderQuantity = @x  
```  
  
 Verwenden Sie `IS NULL`, um zu ermitteln, ob ein Member über einen tatsächlichen Wert verfügt:  
  
```  
select c from LOB.Customer as c where c.DOB is not null  
```  
  
 In der folgenden Tabelle wird das Verhalten von `IS NULL` für einige Muster dargestellt. Alle Ausnahmen werden von der Clientseite ausgelöst, bevor der Anbieter aufgerufen wird:  
  
|Muster|Verhalten|  
|------------|---------------|  
|null IS NULL|Gibt `true` zurück.|  
|TREAT \(null AS EntityType\) IS NULL|Gibt `true` zurück.|  
|TREAT \(null AS ComplexType\) IS NULL|Löst einen Fehler aus.|  
|TREAT \(null AS RowType\) IS NULL|Löst einen Fehler aus.|  
|EntityType IS NULL|Gibt einen `true` oder `false` zurück.|  
|ComplexType IS NULL|Löst einen Fehler aus.|  
|RowType IS NULL|Löst einen Fehler aus.|  
  
## Beispiel  
 In der folgenden [!INCLUDE[esql](../../../../../../includes/esql-md.md)]\-Abfrage wird der IS NOT NULL\-Operator verwendet, um zu ermitteln, ob ein Abfrageausdruck nicht den Wert NULL hat. Diese Abfrage beruht auf dem "AdventureWorks Sales"\-Modell. Führen Sie folgende Schritte aus, um diese Abfrage zu kompilieren und auszuführen:  
  
1.  Verwenden Sie das Verfahren unter [Vorgehensweise: Ausführen einer Abfrage, die StructuralType\-Ergebnisse zurückgibt](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Übergeben Sie die folgende Abfrage als Argument an die `ExecuteStructuralTypeQuery`\-Methode:  
  
 [!code-csharp[DP EntityServices Concepts 2#ISNULL](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#isnull)]  
  
## Siehe auch  
 [Entity SQL\-Referenz](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)