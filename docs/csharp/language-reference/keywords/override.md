---
title: override (C#-Referenz)
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- override
- override_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- override keyword [C#]
ms.assetid: dd1907a8-acf8-46d3-80b9-c2ca4febada8
caps.latest.revision: 26
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0f5a87eaa5894b61187c379c92ad785336aa79b2
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="override-c-reference"></a>override (C#-Referenz)
Der `override`-Modifizierer wird benötigt, um die abstrakte oder virtuelle Implementierung einer geerbten Methode, Eigenschaft, eines Indexers oder Ereignisses zu erweitern oder ändern.  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel muss die `Square`-Klasse eine überschriebene Implementierung von `Area` bereitstellen, da `Area` von der abstrakten `ShapesClass` geerbt wurde:  
  
 [!code-cs[csrefKeywordsModifiers#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/override_1.cs)]  
  
 Eine `override`-Methode stellt eine neue Implementierung eines Members bereit, der von einer Basisklasse geerbt wurde. Die Methode, die durch eine `override`-Deklaration überschrieben wird, wird als die überschriebene Basismethode bezeichnet. Die überschriebene Basismethode muss die gleiche Signatur wie die `override`-Methode haben. Weitere Informationen zur Vererbung in C# finden Sie unter [Vererbung](../../../csharp/programming-guide/classes-and-structs/inheritance.md).  
  
 Sie können keine nicht virtuelle oder statische Methode überschreiben. Die überschriebene Basismethode muss `virtual`, `abstract` oder `override` sein.  
  
 Ein `override`-Deklaration kann nicht die Erreichbarkeit auf die `virtual` Methode ändern. Sowohl die Methode `override` als auch `virtual` müssen den gleichen [Zugriffsebenenmodifizierer](../../../csharp/language-reference/keywords/access-modifiers.md) besitzen.  
  
 Sie können die Modifizierer `new`, `static` oder `virtual` nicht verwenden, um eine `override`-Methode zu ändern.  
  
 Eine überschreibende Eigenschaftsdeklaration muss genau den selben Zugriffsmodifizierertyp und -namen wie die geerbte Eigenschaft angeben, und die überschriebene Eigenschaft muss `virtual`, `abstract` oder `override` sein.  
  
 Weitere Informationen zur Verwendung des `override`-Schlüsselworts finden Sie unter [Versionsverwaltung mit den Schlüsselwörtern „override“ und „new“](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md) und [Wann müssen die Schlüsselwörter „override“ und „new“ verwendet werden?](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md).  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird eine Basisklasse namens `Employee` und eine abgeleitete Klasse namens `SalesEmployee` definiert. Die `SalesEmployee`-Klasse enthält eine zusätzliche Eigenschaft, `salesbonus`, und überschreibt die `CalculatePay`-Methode, um dies zu berücksichtigen.  
  
 [!code-cs[csrefKeywordsModifiers#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/override_2.cs)]  
  
## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Referenz](../../../csharp/language-reference/index.md)   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [Vererbung](../../../csharp/programming-guide/classes-and-structs/inheritance.md)   
 [C#-Schlüsselwörter](../../../csharp/language-reference/keywords/index.md)   
 [Modifizierer](../../../csharp/language-reference/keywords/modifiers.md)   
 [abstract](../../../csharp/language-reference/keywords/abstract.md)   
 [virtual](../../../csharp/language-reference/keywords/virtual.md)   
 [new](../../../csharp/language-reference/keywords/new.md)   
 [Polymorphismus](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)

