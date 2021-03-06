---
title: "Laufzeit-Profilerstellung | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Leistungsindikatoren"
  - "Common Language Runtime, Profilerstellung"
  - "Perfmon.exe"
  - "Systemmonitor"
  - "Profilerstellung"
  - "Laufzeit, Profilerstellung"
  - "Erstellen von Anwendungsprofilen"
  - "Leistung (Verwaltungskonsole)"
ms.assetid: ccd68284-f3a8-47b8-bc3f-92e5fe3a1640
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 22
---
# Laufzeit-Profilerstellung
Die Profilerstellung ist eine Methode zum Sammeln von Leistungsdaten in einer Bereitstellung oder einem Bereitstellungsszenario. Dieser Abschnitt ist für Entwickler und Systemadministratoren vorgesehen, die Informationen zur Leistung der Anwendung erfassen möchten.  
  
## Verfolgen der Leistung mithilfe des Systemmonitors \(Perfmon.exe\)  
 Der Systemmonitor ist das einfachste Tool zur Profilerstellung für Ihre [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]\-Anwendung. Der Systemmonitor stellt in den .NET Framework\-Leistungsindikatoren erfasste Daten grafisch dar, die mit der Common Language Runtime und dem [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] installiert werden. Mithilfe dieser Leistungsindikatoren können Sie von der Speicherverwaltung bis zur JIT\-Compilerleistung \(JIT\) sämtliche Informationen überwachen. Sie informieren Sie über die von der Anwendung verwendeten Ressourcen, die ein indirektes Maß für die Leistung der Anwendung sind. Verwenden Sie diese Leistungsindikatoren, um zu verstehen, wie die Anwendung intern funktioniert.  
  
#### So führen Sie „Perfmon.exe“ unter Windows Vista und höheren Versionen aus  
  
1.  Geben Sie an der Eingabeaufforderung **perfmon** ein. Die **Systemmonitor**\-Konsole wird angezeigt.  
  
2.  Klicken Sie im Ordner **Überwachungstools** auf **Systemmonitor**.  
  
3.  Klicken Sie auf der Symbolleiste des Systemmonitors auf das Symbol **Hinzufügen** \(das Pluszeichen\), sofern es vorhanden ist. Wenn es nicht vorhanden ist, klicken Sie mit der rechten Maustaste im Überwachungsfenster, und wählen Sie dann die Option **Leistungsindikatoren hinzufügen** aus.  
  
     Dadurch wird das Dialogfeld **Leistungsindikatoren hinzufügen** geöffnet. Das Listenfeld **Verfügbare Indikatoren** zeigt die verfügbaren Leistungsobjekte an. Es gibt eine Reihe von vordefinierten Objekten für .NET Framework\-Clientanwendungen, einschließlich der Objekte für die Speicherverwaltung \(**.NET CLR\-Speicher**\), Interoperabilität \(**.NET CLR\-Interop**\), Ausnahmebehandlung \(**.NET CLR\-Ausnahmen**\) und für Multithreading \(**.NET CLR\-Sperren und Threads**\). Jedes Leistungsobjekt umfasst eine Reihe von einzelnen Leistungsindikatoren. Eine Liste der im Systemmonitor verfügbaren Leistungsindikatoren finden Sie unter [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md).  
  
4.  Aktivieren Sie das Kontrollkästchen neben dem Namen eines Leistungsobjekts, um die Liste der einzelnen Leistungsindikatoren anzuzeigen, die es unterstützt.  
  
5.  Klicken Sie auf den Leistungsindikator, den Sie anzeigen möchten.  
  
6.  Klicken Sie im Listenfeld **Instanzen des ausgewählten Objekts** auf **\<Alle Instanzen\>**, um anzugeben, dass Sie den Leistungsindikator für die Common Language Runtime global \(d. h. systemweit\) überwachen möchten.  
  
     \- oder \-  
  
     Klicken Sie im Listenfeld **Instanzen des ausgewählten Objekts** auf einen Anwendungsnamen, um den Leistungsindikator für diese Anwendung zu überwachen.  
  
     Sie müssen zudem einen Registrierungsschlüssel ändern, um verschiedene Versionen der Laufzeit oder mehrere Clientanwendungen mit dem gleichen Namen zu unterscheiden. Weitere Informationen finden Sie unter [Performance Counters and In\-Process Side\-By\-Side Applications](../../../docs/framework/debug-trace-profile/performance-counters-and-in-process-side-by-side-applications.md).  
  
> [!NOTE]
>  Wenn neue Leistungsindikatoren installiert werden, während die Leistungskonsole ausgeführt wird, beenden Sie die Leistungskonsole und starten sie anschließend neu, damit die neuen Indikatoren angezeigt werden.  
  
 Wenn Sie für eine Assembly ein Profil erstellen möchten, die sich in einer Zone oder auf einer Remotefreigabe befindet, stellen Sie sicher, dass die Remoteassembly auf dem Computer über volle Vertrauenswürdigkeit verfügt, auf dem die Leistungsindikatoren ausgeführt werden. Ist die Vertrauenswürdigkeit der Assembly zu gering bemessen, funktionieren die Leistungsindikatoren nicht. Informationen zum Gewähren von Vertrauenswürdigkeit für verschiedene Zonen finden Sie unter [Caspol.exe \(Code Access Security Policy Tool\)](../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md).  
  
> [!NOTE]
>  Auf Systemen, auf denen [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] installiert ist, zeigt der Systemmonitor möglicherweise in einigen Kategorien, z. B. in **.NET CLR\-Daten** und **.NET CLR\-Netzwerk**, keine Daten für Leistungsindikatoren für Anwendungen an, die mithilfe von [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] entwickelt wurden. Wenn dies der Fall ist, können Sie den Systemmonitor entsprechend konfigurieren, um diese Daten durch Hinzufügen des [\<forcePerformanceCounterUniqueSharedMemoryReads\>](../../../docs/framework/configure-apps/file-schema/runtime/forceperformancecounteruniquesharedmemoryreads-element.md)\-Elements in der Konfigurationsdatei der Anwendung anzuzeigen.  
  
## Programmgesteuertes Lesen und Erstellen von Leistungsindikatoren  
 Der [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] stellt Klassen bereit, mit denen Sie programmgesteuert auf dieselben Leistungsdaten zugreifen können, die in der Leistungskonsole verfügbar sind. Mithilfe dieser Klassen können Sie auch benutzerdefinierte Leistungsindikatoren erstellen. In der folgenden Tabelle sind einige der Systemmonitorklassen beschrieben, die im [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] bereitgestellt werden.  
  
|Klasse|Beschreibung|  
|------------|------------------|  
|<xref:System.Diagnostics.PerformanceCounter?displayProperty=fullName>|Stellt eine Windows NT\-Leistungsindikatorkomponente dar. Verwenden Sie diese Klasse, um vordefinierte oder benutzerdefinierte Leistungsindikatoren zu lesen und Leistungsdaten für benutzerdefinierte Indikatoren zu veröffentlichen \(schreiben\).|  
|<xref:System.Diagnostics.PerformanceCounterCategory?displayProperty=fullName>|Bietet verschiedene Methoden für die Interaktion mit Indikatoren und Kategorien von Indikatoren auf dem Computer.|  
|<xref:System.Diagnostics.PerformanceCounterInstaller?displayProperty=fullName>|Gibt einen Installer für die `PerformanceCounter`\-Komponente an.|  
|<xref:System.Diagnostics.PerformanceCounterType?displayProperty=fullName>|Gibt die Formel zum Berechnen der `NextValue`\-Methode für eine `PerformanceCounter` an.|  
  
## Siehe auch  
 [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md)