---
title: "XML literals and XML properties are not supported in embedded code within ASP.NET | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31200"
  - "bc31200"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31200"
ms.assetid: 053e8cba-8584-45cc-9fa0-43d122779772
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# XML literals and XML properties are not supported in embedded code within ASP.NET
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

XML\-Literale und XML\-Eigenschaften werden in eingebettetem Code in ASP.NET nicht unterstützt.Verschieben Sie den Code in eine Code\-Behind\-Datei, um XML\-Features verwenden zu können.  
  
 Ein XML\-Literal oder eine XML\-Achseneigenschaft wurde innerhalb des eingebetteten Codes \(`<%= =>`\) in einer ASP.NET\-Datei definiert.  
  
 **Fehler\-ID:** BC31200  
  
### So beheben Sie diesen Fehler  
  
-   Verschieben Sie den Code, in dem das XML\-Literal oder die XML\-Achseneigenschaft enthalten ist, in eine ASP.NET\-Code\-Behind\-Datei.  
  
## Siehe auch  
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)