---
title: "Rendering von Steuerelementen mit visuellen Stilen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "professionelle Darstellung, Rendern von Windows Forms-Steuerelementen"
  - "Designs, Visuelle XP-Stile in Windows Forms"
  - "Benutzerdefinierte Steuerelemente [Windows Forms], Rendering"
  - "Benutzerdefinierte Steuerelemente [Windows Forms], Zeichnen"
  - "Visuelle Designs, Rendering von Windows Forms-Steuerelementen"
  - "Benutzersteuerelemente [Windows Forms], Malen"
  - "Visuelle Stile, Rendering von Windows Forms-Steuerelementen"
ms.assetid: a5b178ba-610e-46c4-a6c0-509c0886a744
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Rendering von Steuerelementen mit visuellen Stilen
Mithilfe visueller Stile in Betriebssystemen, die diese unterstützen, bietet das [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] Unterstützung für das Rendern von Steuerelementen und anderen Elementen der Windows\-Benutzeroberfläche \(UI\). In diesem Thema werden die verschiedenen Unterstützungsebenen im [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] für das Rendern von Steuerelementen und anderen UI\-Elementen mit dem aktuellen visuellen Stil des Betriebssystems diskutiert.  
  
## Rendern von Klassen für allgemeine Steuerelemente  
 Unter dem Rendern eine Steuerelements versteht man das Zeichnen der Benutzeroberfläche eines Steuerelements. Der <xref:System.Windows.Forms?displayProperty=fullName>\-Namespace stellt die <xref:System.Windows.Forms.ControlPaint>\-Klasse zum Rendern einiger allgemeiner Windows Forms\-Steuerelemente bereit. Allerdings zeichnet diese Klasse die Steuerelemente im klassischen Windows\-Stil. Dies kann eine einheitliche Gestaltung der Benutzeroberfläche erschweren, wenn das Zeichnen benutzerdefinierter Steuerelemente in Anwendungen mit visuellen Stilen aktiviert ist.  
  
 Das [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)] beinhaltet Klassen im <xref:System.Windows.Forms?displayProperty=fullName>\-Namespace, die Teile und Zustände von allgemeinen Steuerelementen mit visuellen Stilen rendern. Jede dieser Klassen enthält `static`\-Methoden für das Zeichnen des Steuerelements oder Teile des Steuerelements in einem bestimmten Zustand mit dem aktuellen visuellen Stil des Betriebssystems.  
  
 Einige dieser Klassen dienen dem Zeichnen des zugehörigen Steuerelements, unabhängig davon, ob visuelle Stile verfügbar sind. Wenn visuelle Stile aktiviert sind, werden die Klassenelemente das zugehörige Steuerelement mit visuellen Stilen gezeichnet. Wenn visuelle Stile deaktiviert sind, zeichnen die Klassenelemente das Steuerelement im klassischen Windows\-Stil. Diese Klassen umfassen:  
  
-   <xref:System.Windows.Forms.ButtonRenderer>  
  
-   <xref:System.Windows.Forms.CheckBoxRenderer>  
  
-   <xref:System.Windows.Forms.GroupBoxRenderer>  
  
-   <xref:System.Windows.Forms.RadioButtonRenderer>  
  
 Andere Klassen können das zugehörige Steuerelement nur zeichnen, wenn visuelle Stile verfügbar sind, und ihre Member löst eine Ausnahme aus, wenn visuelle Stile deaktiviert sind. Diese Klassen umfassen:  
  
-   <xref:System.Windows.Forms.ComboBoxRenderer>  
  
-   <xref:System.Windows.Forms.ProgressBarRenderer>  
  
-   <xref:System.Windows.Forms.ScrollBarRenderer>  
  
-   <xref:System.Windows.Forms.TabRenderer>  
  
-   <xref:System.Windows.Forms.TextBoxRenderer>  
  
-   <xref:System.Windows.Forms.TrackBarRenderer>  
  
 Weitere Informationen zum Verwenden dieser Klassen zum Zeichnen eines Steuerelements finden Sie unter [Gewusst wie: Verwenden einer Steuerelementwiedergabeklasse](../../../../docs/framework/winforms/controls/how-to-use-a-control-rendering-class.md).  
  
## Visuelles Stilelement und Renderingklassen  
 Der <xref:System.Windows.Forms.VisualStyles?displayProperty=fullName>\-Namespace enthält Klassen, die zum Zeichnen und Abrufen von Informationen über jedes Steuerelement oder UI\-Element verwendet werden können, das von visuellen Stilen unterstützt wird. Unterstützte Steuerelemente enthalten allgemeine Steuerelemente, die über eine Rendering\-Klasse im <xref:System.Windows.Forms?displayProperty=fullName>\-Namespace verfügen \(s. Abschnitt oben\), sowie andere Steuerelemente, z.B. Registersteuerelemente und Grundleistensteuerelemente. Weitere unterstützte UI\-Elemente sind z.B. Teile des **Startmenüs**, der Taskleiste und des Nicht\-Clientbereichs von Windows.  
  
 Die wichtigsten Klassen des <xref:System.Windows.Forms.VisualStyles?displayProperty=fullName>\-Namespaces sind <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> und <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer>.<xref:System.Windows.Forms.VisualStyles.VisualStyleElement> ist eine Foundation Class zur Ermittlung aller von visuellen Stilen unterstützten Steuerelemente oder Benutzeroberflächenelemente. Zusätzlich zu <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> selbst enthält der <xref:System.Windows.Forms.VisualStyles?displayProperty=fullName>\-Namespace viele geschachtelte Klassen von <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> mit `static`\-Eigenschaften, die <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> für jeden Zustand eines Steuerelements, Teil eines Steuerelements oder jedes UI\-Element zurückgeben, der bzw. das von visuellen Stilen unterstützt wird.  
  
 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> stellt Methoden zum Zeichnen und Abrufen von Informationen zu jedem einzelnen <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> bereit, das durch den aktuellen visuellen Stil des Betriebssystems definiert wird. Die Informationen, die über ein Element abgerufen werden können, beinhalten die Standardgröße, den Hintergrundtyp und die Farbdefinitionen.<xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> umschließt die Funktionalität der API für visuelle Stile \(UxTheme\) aus dem Windows Shell\-Bereich der Windows Platform SDK. Weitere Informationen finden Sie unter „Using Windows XP Visual Styles“ \(Verwenden von visuelle Windows XP\-Stilen\) im Teil zum Platform SDK der MSDN Library unter [http:\/\/msdn.microsoft.com\/library](http://msdn.microsoft.com/library/).  
  
 Weitere Informationen über die Verwendung von <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> und <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> finden Sie unter [Gewusst wie: Rendern eines visuellen Stilelements](../../../../docs/framework/winforms/controls/how-to-render-a-visual-style-element.md).  
  
## Aktivieren von visuellen Stilen  
 Programmierer müssen ein Anwendungsmanifest beifügen, das angibt, dass Version 6 von „ComCtl32.dll“ oder höher zum Zeichnen von Steuerelementen verwendet werden wird, damit visuelle Stile für Anwendungen aktiviert werden, die für [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] Version 1.0 geschrieben wurden. Anwendungen, die mit [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] Version 1.1 oder höher erstellt wurden, können die <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName>\-Methode der <xref:System.Windows.Forms.Application>\-Klasse verwenden.  
  
## Überprüfen der Unterstützung für visuelle Stile  
 Die <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A>\-Eigenschaft der <xref:System.Windows.Forms.Application>\-Klasse gibt an, ob die aktuelle Anwendung Steuerelemente mit visuellen Stilen zeichnet. Wenn Sie ein benutzerdefiniertes Steuerelement zeichnen, können Sie den Wert von <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A> anzeigen, um zu festzulegen, ob das Steuerelement mit oder ohne visuelle Stile gerendert werden soll. In der folgenden Tabelle werden die vier Faktoren aufgelistet, die gegeben sein müssen, damit <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A>`true` zurückgibt.  
  
|Bedingung|Notizen|  
|---------------|-------------|  
|Das Betriebssystem unterstützt visuelle Stile.|Verwenden Sie die <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation.IsSupportedByOS%2A>\-Eigenschaft der <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation>\-Klasse, um diese Bedingung separat zu überprüfen.|  
|Der Benutzer hat visuelle Stile auf seinem Betriebssystem aktiviert.|Verwenden Sie die <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation.IsEnabledByUser%2A>\-Eigenschaft der <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation>\-Klasse, um diese Bedingung separat zu überprüfen.|  
|Visuelle Stile sind in der Anwendung aktiviert.|Visuelle Stile können in einer Anwendung durch Aufrufen der <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName>\-Methode oder mithilfe des Anwendungsmanifests aktiviert werden. Das Manifest gibt an, dass Version 6 von „ComCtl32.dll“ oder höher zum Zeichnen von Steuerelementen verwendet werden wird.|  
|Visuelle Stile werden dazu verwendet, den Clientbereich von Anwendungsfenstern zu zeichnen.|Verwenden Sie die <xref:System.Windows.Forms.Application.VisualStyleState%2A>\-Eigenschaft der <xref:System.Windows.Forms.Application>\-Klasse und überprüfen Sie, ob sie den Wert <xref:System.Windows.Forms.VisualStyles.VisualStyleState?displayProperty=fullName> oder <xref:System.Windows.Forms.VisualStyles.VisualStyleState?displayProperty=fullName> aufweist, um diese Bedingung separat zu überprüfen.|  
  
 Überprüfen Sie den <xref:Microsoft.Win32.UserPreferenceCategory?displayProperty=fullName>\-Wert in den Handlern auf <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging?displayProperty=fullName>\- oder <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged?displayProperty=fullName>\-Ereignisse, um zu ermitteln, ob Benutzer visuelle Stile aktiviert oder deaktiviert haben oder ob sie von einem visuellen Stil zu einem anderen gewechselt haben.  
  
> [!IMPORTANT]
>  Wenn Sie <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> verwenden möchten, um ein Steuerelement oder ein UI\-Element zu rendern, müssen Sie, wenn der Benutzer visuelle Stile aktiviert oder zwischen ihnen wechselt, sicherstellen, dass Sie dies während der Verarbeitung des <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged>\-Ereignisses und nicht während der Verarbeitung des <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging>\-Ereignisses tun. Eine Ausnahme wird ausgelöst, wenn Sie mithilfe der <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer>\-Klasse bei der Verarbeitung von <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging> verwenden.  
  
## Siehe auch  
 [Zeichnen und Ausgeben von benutzerdefinierten Steuerelementen](../../../../docs/framework/winforms/controls/custom-control-painting-and-rendering.md)