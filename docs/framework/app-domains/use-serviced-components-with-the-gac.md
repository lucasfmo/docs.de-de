---
title: Verwenden von Serviced Components mit dem globalen Assemblycache
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- GAC (global assembly cache), serviced components
- serviced components, global assembly cache
- global assembly cache, serviced components
ms.assetid: 3423e5d9-234c-4571-8161-e35f6d130128
caps.latest.revision: 8
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 493ca9a2da4a06528eab9b87db78a5b7a49a2f1d
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="using-serviced-components-with-the-global-assembly-cache"></a>Verwenden von Serviced Components mit dem globalen Assemblycache
Die Serviced Components (COM+-Komponenten mit verwaltetem Code) sollten im globalen Assemblycache abgelegt werden. Nur in bestimmten Szenarien können die Common Language Runtime und die COM+-Dienste mit Serviced Components umgehen, die sich nicht im globalen Assemblycache befinden. Folgende Beispielszenarien verdeutlichen dies:  
  
-   Für Serviced Components in einer COM+-Serveranwendung muss sich die Assembly, die die Komponenten enthält, im globalen Assemblycache befinden. Der Grund dafür ist, dass „Dllhost.exe“ nicht im Verzeichnis ausgeführt werden kann, das die Serviced Components enthält.  
  
-   Bei Serviced Components in einer COM+-Bibliotheksanwendung können die Common Language Runtime und die COM+-Dienste durch Durchsuchen des aktuellen Verzeichnisses den Verweis auf die Assembly auflösen. Demzufolge muss sich in diesem Fall die Assembly nicht unbedingt im globalen Assemblycache befinden.  
  
-   Bei Serviced Components in einer ASP.NET-Anwendung stellt sich die Situation anders dar. Wenn Sie die Assembly, die Serviced Components enthält, im Verzeichnis „bin“ des Anwendungsstamms ablegen und bedarfsabhängige Registrierung verwenden, wird die Assembly mittels Spiegelung in den Downloadcache kopiert, da ASP.NET die Spiegelungsfunktionen der Common Language Runtime verwendet.  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit Assemblys und dem globalen Assemblychache](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Gacutil.exe (Global Assembly Cache-Tool)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)

