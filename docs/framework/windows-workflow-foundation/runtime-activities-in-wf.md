---
title: "Laufzeitaktivit&#228;ten in WF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5ae8c31-19bc-4655-88b3-6b75cd6a1bd5
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Laufzeitaktivit&#228;ten in WF
[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] enthält mehrere vom System bereitgestellte Aktivitäten für den Zugriff auf die Funktionen der Workflowlaufzeit, z. B. Persistenz und Beendigung.  
  
|Aktivität|Beschreibung|  
|---------------|------------------|  
|<xref:System.Activities.Statements.Persist>|Fordert explizit an, dass der Workflow seinen Zustand beibehält.|  
|<xref:System.Activities.Statements.TerminateWorkflow>|Beendet die ausgeführte Workflowinstanz.|  
|<xref:System.Activities.Statements.NoPersistScope>|Eine Containeraktivität, die untergeordnete Aktivitäten an der Beibehaltung hindert.|