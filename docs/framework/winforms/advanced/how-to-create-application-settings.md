---
title: "Gewusst wie: Erstellen von Anwendungseinstellungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Anwendungseinstellungen, Erstellen"
  - "Anwendungseinstellungen, Windows Forms"
ms.assetid: 1e7aa347-af75-41e5-89ca-f53cab704f72
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Gewusst wie: Erstellen von Anwendungseinstellungen
Mithilfe von verwaltetem Code können Sie neue Anwendungseinstellungen erstellen und diese an Eigenschaften für Ihr Formular oder die Steuerelemente Ihres Formulars binden, damit diese Einstellungen zur Laufzeit automatisch geladen und gespeichert werden.  
  
 Im folgenden Verfahren erstellen Sie manuell eine Wrapperklasse, die von <xref:System.Configuration.ApplicationSettingsBase> abgeleitet ist.  Dieser Klasse fügen Sie für jede Anwendungseinstellung, die Sie verfügbar machen möchten, eine Eigenschaft hinzu, auf die öffentlich zugegriffen werden kann.  
  
 Sie können dieses Verfahren auch mit minimalem Programmieraufwand in Visual Studio\-Designer ausführen.  Siehe auch [Gewusst wie: Erstellen von Anwendungseinstellungen mithilfe des Designers](http://msdn.microsoft.com/library/wabtadw6%20\(v=vs.110\)).  
  
### So erstellen Sie programmgesteuert neue Anwendungseinstellungen  
  
1.  Fügen Sie dem Projekt eine neue Klasse hinzu, und benennen Sie diese um.  Für dieses Verfahren wird diese Klasse `MyUserSettings` aufgerufen.  Ändern Sie die Klassendefinition so, dass die Klasse von <xref:System.Configuration.ApplicationSettingsBase> abgeleitet wird.  
  
2.  Definieren Sie eine Eigenschaft für diese Wrapperklasse für jede benötigte Anwendungseinstellung, und wenden Sie diese Eigenschaft mit <xref:System.Configuration.ApplicationScopedSettingAttribute> oder mit <xref:System.Configuration.UserScopedSettingAttribute>, abhängig vom Bereich der Einstellung an.  Weitere Informationen zum Einstellungsbereich finden Sie unter [Übersicht über Anwendungseinstellungen](../../../../docs/framework/winforms/advanced/application-settings-overview.md).  Ihr Code sollte jetzt wie folgt aussehen.  
  
     [!code-csharp[ApplicationSettings.Create#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Create/CS/MyAppSettings.cs#1)]
     [!code-vb[ApplicationSettings.Create#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Create/VB/MyAppSettings.vb#1)]  
  
3.  Erstellen Sie eine Instanz dieser Wrapperklasse in Ihrer Anwendung.  Sie wird in der Regel ein privates Element des Hauptformulars sein.  Nachdem Sie nun Ihre Klasse definiert haben, müssen Sie sie an eine Eigenschaft binden. In diesem Fall ist dies die Eigenschaft <xref:System.Windows.Forms.Form.BackColor%2A> des Formulars.  Sie können dies im `Load` \-Ereignishandler des Formulars ausführen.  
  
     [!code-csharp[ApplicationSettings.Create#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Create/CS/Form1.cs#2)]
     [!code-vb[ApplicationSettings.Create#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Create/VB/Form1.vb#2)]  
  
4.  Wenn Sie eine Möglichkeit zum Ändern von Einstellungen zur Laufzeit bereitstellen, müssen Sie die aktuellen Einstellungen des Benutzers auf dem Datenträger speichern, wenn das Formular geschlossen wird. Andernfalls gehen diese Änderungen verloren.  
  
     [!code-csharp[ApplicationSettings.Create#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Create/CS/Form1.cs#3)]
     [!code-vb[ApplicationSettings.Create#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Create/VB/Form1.vb#3)]  
  
     Sie haben nun erfolgreich eine neue Anwendungseinstellung erstellt und diese an die angegebene Eigenschaft gebunden.  
  
## .NET Framework-Sicherheit  
 Der Standardeinstellungsanbieter \(<xref:System.Configuration.LocalFileSettingsProvider>\) speichert Informationen in Konfigurationsdateien als Nur\-Text persistent.  Auf diese Weise wird die Sicherheit für die Dateizugriffssicherheit eingeschränkt, die vom Betriebssystem für den aktuellen Benutzer bereitgestellt wird.  Aus diesem Grund müssen die Informationen, die in Konfigurationsdateien gespeichert werden, sorgfältig ausgewählt werden.  Häufig werden z. B. Anwendungseinstellungen zum Speichern von Verbindungszeichenfolgen verwendet, die auf den Datenspeicher der Anwendung zeigen.  Allerdings sollten diese Zeichenfolgen aus Sicherheitsgründen keine Kennwörter enthalten.  Weitere Informationen zu Verbindungszeichenfolgen finden Sie unter <xref:System.Configuration.SpecialSetting>.  
  
## Siehe auch  
 <xref:System.Configuration.SpecialSettingAttribute>   
 <xref:System.Configuration.LocalFileSettingsProvider>   
 [Übersicht über Anwendungseinstellungen](../../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [Gewusst wie: Überprüfen von Anwendungseinstellungen](../../../../docs/framework/winforms/advanced/how-to-validate-application-settings.md)