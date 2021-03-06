---
title: "Das BasePath-Argument muss ein Pfad zu einem Ordner sein. | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
ms.assetid: b180ce60-ad57-41a6-a313-491d86d84cc7
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Das BasePath-Argument muss ein Pfad zu einem Ordner sein.
Das `BasePath`\-Argument muss aus einen Pfad zu einem Ordner bestehen. Möglicherweise analysieren Sie eine Zeichenfolge nicht ordnungsgemäß und stellen einen Wert bereit, der nicht als gültiger Pfad erkannt wird.  
  
### So beheben Sie diesen Fehler  
  
-   Überprüfen Sie den für `BasePath` bereitgestellten Wert, um sicherzustellen, dass es sich um einen gültigen Pfad zu einem Ordner handelt.  
  
## Siehe auch  
 <xref:System.CodeDom.Compiler.TempFileCollection.BasePath%2A>   
 <xref:System.Resources.ResXResourceWriter.BasePath%2A>   
 <xref:System.Resources.ResXResourceReader.BasePath%2A>   
 [Gewusst wie: Analysieren von Dateipfaden](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)