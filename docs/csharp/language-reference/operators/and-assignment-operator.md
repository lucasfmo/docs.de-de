---
title: "Operator&#160;&amp;= (C#-Referenz) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "&=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "&= (Operator) [C#]"
  - "AND-Zuweisungsoperator (&=) [C#]"
ms.assetid: e8d58f3f-72dd-4b5a-b995-452fcce7e6bb
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Operator&#160;&amp;= (C#-Referenz)
Der AND\-Zuweisungsoperator.  
  
## Hinweise  
 Ein Ausdruck, in dem der Zuweisungsoperator `&=` verwendet wird, z. B.  
  
```  
x &= y  
```  
  
 der folgenden Syntax:  
  
```  
x = x & y  
```  
  
 mit der Ausnahme, dass `x` nur einmal ausgewertet wird.  Der [Operator &](../../../csharp/language-reference/operators/and-operator.md) führt eine bitweise AND\-Operation für ganzzahlige Operanden aus sowie logisches AND für `bool`\-Operanden.  
  
 Der Operator `&=` kann nicht direkt überladen werden. Benutzerdefinierte Typen können jedoch den binären [Operator &](../../../csharp/language-reference/operators/and-operator.md) überladen \(siehe [Operator](../../../csharp/language-reference/keywords/operator.md)\).  
  
## Beispiel  
 [!code-cs[csRefOperators#34](../../../csharp/language-reference/operators/codesnippet/CSharp/and-assignment-operator_1.cs)]  
  
## Siehe auch  
 [C\#\-Referenz](../../../csharp/language-reference/index.md)   
 [C\#\-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [C\#\-Operatoren](../../../csharp/language-reference/operators/index.md)