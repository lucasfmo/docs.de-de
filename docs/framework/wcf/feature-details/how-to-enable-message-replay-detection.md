---
title: "Vorgehensweise: Aktivieren der Nachrichtenreplay-Erkennung | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Replay-Erkennung [WCF]"
  - "WCF-Sicherheit"
  - "WCF, Benutzerdefinierte Bindungen"
  - "WCF, Sicherheit"
ms.assetid: 8b847e91-69a3-49e1-9e5f-0c455e50d804
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Vorgehensweise: Aktivieren der Nachrichtenreplay-Erkennung
Ein Replay\-Angriff tritt auf, wenn ein Angreifer einen Nachrichtenstrom zwischen zwei Parteien kopiert und den Strom für eine oder mehrere Parteien wiedergibt.Wenn der Angriff nicht abgeschwächt wird, verarbeiten die angegriffenen Computer den Strom als zulässige Meldungen, was zu einer Reihe negativer Konsequenzen führt, wie z. B. redundanten Bestellungen eines Artikels.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] zur Nachrichtenreplay\-Erkennung finden Sie unter [Message Replay Detection](http://go.microsoft.com/fwlink/?LinkId=88536).  
  
 Die folgende Prozedur veranschaulicht verschiedene Eigenschaften, die Sie verwenden können, um die Replay\-Erkennung mit [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] zu steuern.  
  
### So steuern Sie die Replay\-Erkennung für den Client mithilfe von Code  
  
1.  Erstellen Sie ein <xref:System.ServiceModel.Channels.SecurityBindingElement> zur Verwendung in einem <xref:System.ServiceModel.Channels.CustomBinding>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Vorgehensweise: Erstellen einer benutzerdefinierten Bindung mit dem SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).Im folgenden Beispiel wird eine <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> verwendet, die mithilfe der <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A> der <xref:System.ServiceModel.Channels.SecurityBindingElement>\-Klasse erstellt worden ist.  
  
2.  Verwenden Sie die <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalClientSettings%2A>\-Eigenschaft, um einen Verweis auf die <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>\-Klasse zurückzugeben und die folgenden Eigenschaften nach Bedarf festzulegen:  
  
    1.  `DetectReplay`.Ein boolescher Wert.Dieser bestimmt, ob der Client Replays vom Server erkennen sollte.Die Standardeinstellung ist `true`.  
  
    2.  `MaxClockSkew`.Ein <xref:System.TimeSpan>\-Wert.Bestimmt die Zeitverschiebung, die der Replay\-Mechanismus zwischen dem Client und dem Server tolerieren kann.Das Sicherheitsverfahren untersucht den gesendeten Zeitstempel und bestimmt, ob er zu weit in der Vergangenheit zurückliegend gesendet wurde.Der Standardwert beträgt fünf Minuten.  
  
    3.  `ReplayWindow`.Ein `TimeSpan`\-Wert.Dieser bestimmt, wie lange eine Nachricht im Netzwerk bleiben kann, nachdem sie vom Server \(durch Vermittler\) gesendet worden ist, bevor sie den Client erreicht.Der Client verfolgt die Signaturen der Nachrichten, die innerhalb des letzten `ReplayWindow` gesendet wurden, zur Replay\-Erkennung.  
  
    4.  `ReplayCacheSize`.Ein Ganzzahlwert.Der Client speichert die Signaturen der Nachricht in einem Cache.Diese Einstellung gibt an, wie viele Signaturen der Cache speichern kann.Wenn die Zahl der Nachrichten, die innerhalb des letzten Replay\-Fensters gesendet wurden, das Cachelimit erreicht, werden neue Nachrichten zurückgewiesen, bis die ältesten zwischengespeicherten Signaturen das Zeitlimit überschreiten.Die Standardeinstellung ist 500.000.  
  
### So steuern Sie die Replay\-Erkennung für den Dienst mithilfe von Code  
  
1.  Erstellen Sie ein <xref:System.ServiceModel.Channels.SecurityBindingElement> zur Verwendung in einer <xref:System.ServiceModel.Channels.CustomBinding>.  
  
2.  Verwenden Sie die <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSettings%2A>\-Eigenschaft, um einen Verweis auf die <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>\-Klasse zurückzugeben, und legen Sie die Eigenschaften fest, wie zuvor beschrieben.  
  
### So steuern Sie die Replay\-Erkennung in der Konfiguration für den Client oder den Dienst  
  
1.  Erstellen Sie eine [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md).  
  
2.  Erstellen Sie ein `<security>`\-Element.  
  
3.  Erstellen Sie ein [\<localClientSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localclientsettings-element.md) oder ein[\<localServiceSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localservicesettings-element.md).  
  
4.  Legen Sie die folgenden Attributwerte nach Bedarf fest: `detectReplays`, `maxClockSkew`, `replayWindow` und `replayCacheSize`.Im folgenden Beispiel werden sowohl die Attribute eines `<localServiceSettings>``<localClientSettings>- als auch eines` \-Elements festgelegt:  
  
    ```  
    <customBinding>  
      <binding name="NewBinding0">  
       <textMessageEncoding />  
        <security>  
         <localClientSettings   
          replayCacheSize="800000"   
          maxClockSkew="00:03:00"  
          replayWindow="00:03:00" />  
         <localServiceSettings   
          replayCacheSize="800000"   
          maxClockSkew="00:03:00"  
          replayWindow="00:03:00" />  
        <secureConversationBootstrap />  
       </security>  
      <httpTransport />  
     </binding>  
    </customBinding>  
    ```  
  
## Beispiel  
 Im folgenden Beispiel wird ein <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> mithilfe der <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A>\-Methode erstellt, und die Replay\-Eigenschaften der Bindung werden festgelegt.  
  
 [!code-csharp[c_ReplayDetection#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_replaydetection/cs/source.cs#1)]
 [!code-vb[c_ReplayDetection#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_replaydetection/vb/source.vb#1)]  
  
## Replay\-Bereich: Nur Nachrichtensicherheit  
 Beachten Sie, dass die folgenden Prozeduren nur für den Nachrichtensicherheitsmodus gelten.Für den Transportmodus und den Transportmodus mit Nachrichtenanmeldeinformationen erkennen die Transportmechanismen Replays.  
  
## Hinweise für die sichere Konversation  
 Bei Bindungen, die sichere Konversationen ermöglichen, können Sie diese Einstellungen sowohl für den Anwendungskanal als auch für die sichere Konversationsbootstrap\-Bindung anpassen.Sie können z. B. Replays für den Anwendungskanal deaktivieren, sie jedoch für den Bootstrapkanal aktivieren, der die sichere Konversation aufbaut.  
  
 Wenn Sie keine Sitzungen für sichere Konversation verwenden, kann die Replay\-Erkennung nicht garantieren, dass Replays in Serverfarmszenarien und bei der Wiederverwendung des Prozesses erkannt werden.Dies gilt für die folgenden vom System bereitgestellten Bindungen:  
  
-   <xref:System.ServiceModel.BasicHttpBinding>.  
  
-   <xref:System.ServiceModel.WSHttpBinding> mit der <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A>\-Eigenschaft, die auf `false` festgelegt ist.  
  
## Kompilieren des Codes  
  
-   Die folgenden Namespaces sind zum Kompilieren des Codes erforderlich:  
  
-   <xref:System>  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.ServiceModel.Channels>  
  
## Siehe auch  
 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>   
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>   
 [Sichere Unterhaltungen und sichere Sitzungen.](../../../../docs/framework/wcf/feature-details/secure-conversations-and-secure-sessions.md)   
 [\<localClientSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localclientsettings-element.md)   
 [Vorgehensweise: Erstellen einer benutzerdefinierten Bindung mit dem SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)