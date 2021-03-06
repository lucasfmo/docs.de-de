---
title: "UI Automation Support for the ToolTip Control Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UI Automation, ToolTip control type"
  - "ToolTip control type"
  - "control types, ToolTip"
ms.assetid: c3779d78-3164-43ae-8dae-bfaeafffdd65
caps.latest.revision: 22
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 22
---
# UI Automation Support for the ToolTip Control Type
> [!NOTE]
>  Diese Dokumentation ist für .NET Framework\-Entwickler vorgesehen, die die verwalteten [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Klassen verwenden möchten, die im <xref:System.Windows.Automation>\-Namespace definiert sind. Aktuelle Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] finden Sie auf der Seite zur [Windows\-Automatisierungs\-API: UI\-Automatisierung](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Dieses Thema enthält Informationen über [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Unterstützung für den Steuerelementtyp „ToolTip“. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] umfasst ein Steuerelementtyp eine Reihe von Bedingungen, die ein Steuerelement erfüllen muss, damit die <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>\-Eigenschaft verwendet werden kann. Die Bedingungen schließen bestimmte Richtlinien für [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaftswerte und Steuerelementmuster ein.  
  
 QuickInfo\-Steuerelemente sind Popupfenster, die Text enthalten.  
  
 In den folgenden Abschnitten werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur, \-Eigenschaften, \-Steuerelementmuster und \-Ereignisse definiert, die für den Steuerelementtyp „ToolTip“ erforderlich sind. Die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Anforderungen gelten für alle QuickInfo\-Steuerelemente, egal ob [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] oder [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Struktur  
 In der folgenden Tabelle werden die Steuerelementansicht und die Inhaltsansicht der [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur für QuickInfo\-Steuerelemente sowie die möglichen Inhalte der Ansichten beschrieben. Weitere Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur finden Sie unter [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Steuerelementansicht|Inhaltsansicht|  
|--------------------------|--------------------|  
|QuickInfo<br /><br /> -   Text \(beliebige Anzahl\)<br />-   Bild \(beliebige Anzahl\)|QuickInfo|  
  
 QuickInfo\-Steuerelemente werden nur dann in der Inhaltsansicht der [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur angezeigt, wenn sie den Tastaturfokus erhalten können. Andernfalls sind alle Informationen zur QuickInfo über die `HelpTextProperty` für das [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Element verfügbar, auf das die QuickInfo verweist.  
  
 QuickInfos sollten unter dem Steuerelement angezeigt werden, auf das sich ihre Informationen beziehen. Clients müssen dem `ToolTipOpenedEvent` lauschen, um sicherzustellen, dass sie fortlaufend die in QuickInfos enthaltenen Informationen erhalten.  
  
<a name="Required_UI_Automation_Properties"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Eigenschaften  
 In der folgenden Tabelle werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaften aufgelistet, deren Wert oder Definition für QuickInfo\-Steuerelemente besonders relevant ist. Weitere Informationen über [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaften finden Sie unter [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaft|Wert|Notizen|  
|----------------------------------------------------------------------------------------|----------|-------------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Siehe Hinweise.|Der Wert dieser Eigenschaft muss für alle Steuerelemente in einer Anwendung eindeutig sein.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Siehe Hinweise.|Das äußere Rechteck, das das gesamte Steuerelement enthält.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Siehe Hinweise.|Der klickbare Punkt muss Teil der QuickInfo sein, die das Steuerelement schließt. Einige QuickInfos haben diese Fähigkeit nicht und haben keinen klickbaren Punkt.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Siehe Hinweise.|Wenn das Steuerelement den Tastaturfokus erhalten kann, muss es diese Eigenschaft unterstützen.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Siehe Hinweise.|Der Name des QuickInfo\-Steuerelements ist der Text, der innerhalb der QuickInfo angezeigt wird.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|QuickInfo\-Steuerelemente werden immer durch ihren Inhalt selbstbeschriftet.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|QuickInfo|Dieser Wert ist für alle Benutzeroberflächen\-Frameworks gleich.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|„QuickInfo“|Lokalisierte Zeichenfolge für den Steuerelementtyp „ToolTip“.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|Variabel|Wenn das QuickInfo\-Steuerelement den Tastaturfokus erhalten kann, muss es in der Inhaltsansicht der Struktur enthalten sein. Ist es nur ein Textelement, steht es als HelpTextProperty des Steuerelements zur Verfügung, von dem es ausgelöst wurde.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Das QuickInfo\-Steuerelement muss immer ein Steuerelement sein.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Steuerelementmuster  
 In der folgenden Tabelle werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Steuerelementmuster aufgelistet, die von allen QuickInfo\-Steuerelementen unterstützt werden müssen. Weitere Informationen zu Steuerelementmustern finden Sie unter [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Steuerelementmuster|Unterstützung|Notizen|  
|-------------------------|-------------------|-------------|  
|<xref:System.Windows.Automation.Provider.IWindowProvider>|Variabel|QuickInfos, die durch Klicken auf ein Benutzeroberflächenelement geschlossen werden können, müssen WindowPattern unterstützen, damit sie automatisch geschlossen werden können.|  
|<xref:System.Windows.Automation.Provider.ITextProvider>|Variabel|Für eine verbesserte Barrierefreiheit kann ein QuickInfo\-Steuerelement das Text\-Steuerelementmuster unterstützen, dies ist jedoch nicht erforderlich. Das Text\-Steuerelementmuster ist nützlich, wenn der Text viele Formate und Attribute hat \(z. B., Farbe, Fettdruck und Kursivdruck\).|  
  
<a name="Required_UI_Automation_Events"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Ereignisse  
 QuickInfo\-Steuerelemente müssen `ToolTipOpenedEvent` auslösen, wenn sie auf dem Bildschirm angezeigt werden. Das Ereignis enthält einen Verweis auf das [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Element der QuickInfo selbst.  
  
 Die folgende Tabelle enthält die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Ereignisse, die von allen QuickInfo\-Steuerelementen unterstützt werden müssen. Weitere Informationen zu Ereignissen finden Sie unter [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Ereignis|Unterstützung|Notizen|  
|-------------------------------------------------------------------------------------|-------------------|-------------|  
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextSelectionChangedEvent>|Variabel|Keine|  
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextChangedEvent>|Variabel|Keine|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowClosedEvent>|Variabel|Keine|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowOpenedEvent>|Variabel|Keine|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipOpenedEvent>|Erforderlich|Keine|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipClosedEvent>|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.WindowPatternIdentifiers.WindowVisualStateProperty>\-Eigenschaft ausgelöstes Ereignis.|Variabel|Keine|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Erforderlich|Keine|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Erforderlich|Keine|  
  
## Siehe auch  
 <xref:System.Windows.Automation.ControlType.ToolTip>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)