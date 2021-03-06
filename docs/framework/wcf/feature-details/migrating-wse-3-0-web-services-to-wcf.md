---
title: "Migrieren von WSE 3.0-Webdiensten zu WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7bc5fff7-a2b2-4dbc-86cc-ecf73653dcdc
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Migrieren von WSE 3.0-Webdiensten zu WCF
Die Vorteile des Migrierens von WSE 3.0-Webdiensten zu [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] umfassen verbesserte Leistung und die Unterstützung zusätzlicher Transporte, zusätzlicher Sicherheitsszenarien und WS-*Spezifikationen. Bei einem Webdienst, der von WSE 3.0 zu [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] migriert wird, kann eine Leistungsverbesserung von bis zu 200 % bis 400 % auftreten. Weitere Informationen über die Transporte, die von unterstützten [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], finden Sie unter [Wählen eines Transports](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md). Eine Liste von unterstützten Szenarien [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], finden Sie unter [häufige Sicherheitsszenarios](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md). Eine Liste der Spezifikationen, die von unterstützten [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], finden Sie unter [Handbuch für die Interoperabilität von Web Services Protokolle](../../../../docs/framework/wcf/feature-details/web-services-protocols-interoperability-guide.md).  
  
 Die folgenden Abschnitte bieten eine Anleitung für das Migrieren einer bestimmten Funktion eines WSE 3.0-Webdiensts zu [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## <a name="general"></a>Allgemein  
 WSE 3.0 und [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Anwendungen umfassen Interoperabilität auf niedriger Ebene und eine Standardmenge an Terminologie. WSE 3.0 und [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Anwendungen sind auf niedriger Ebene interoperabel auf der Grundlage eines Satzes von WS-*Spezifikationen, den beide unterstützen. Wenn eine WSE 3.0- oder [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Anwendung entwickelt wird, gibt es einen Standardsatz an Terminologie, wie die Namen von sofort verwendbaren Sicherheitsassertionen in WSE und die Authentifizierungsmodi.  
  
 Obwohl es viele ähnliche Aspekte zwischen den Programmiermodellen von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] und ASP.NET oder WSE 3.0 gibt, sind sie unterschiedlich. Weitere Informationen zu den [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Programmiermodell, finden Sie unter [grundlegende Programmierung Lebenszyklus](../../../../docs/framework/wcf/basic-programming-lifecycle.md).  
  
> [!NOTE]
>  So migrieren einen WSE-Webdienst zu WCF die [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) Tool zum Generieren eines Clients verwendet werden kann. Der Client enthält jedoch Schnittstellen und Klassen, die auch als Startpunkt für einen WCF-Dienst verwendet werden können. Die Schnittstellen, die generiert werden, haben die <xref:System.ServiceModel.OperationContractAttribute> -Attribut angewendet wird, die Member des Vertrags mit der <xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A> Eigenschaft festgelegt, um `*`. Wenn ein WSE-Client einen Webdienst mit dieser Einstellung aufruft, wird die folgende Ausnahme ausgelöst: **Web.Services3.ResponseProcessingException: WSE910: während der Verarbeitung einer Antwortnachricht ist ein Fehler aufgetreten, und Sie können die Fehler in der inneren Ausnahme suchen**. Um dies zu vermeiden, legen Sie die <xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A> Eigenschaft der <xref:System.ServiceModel.OperationContractAttribute> -Attributs einen nicht-`null` Wert, z. B. `http://Microsoft.WCF.Documentation/ResponseToOCAMethod`.  
  
## <a name="security"></a>Sicherheit  
  
### <a name="wse-30-web-services-that-are-secured-using-a-policy-file"></a>WSE 3.0-Webdienste, die mit einer Richtliniendatei gesichert werden  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Dienste können mithilfe einer Konfigurationsdatei einen Dienst sichern. Dieser Mechanismus funktioniert ähnlich wie eine WSE 3.0-Richtliniendatei. Wenn Sie in WSE 3.0 einen Webdienst mit einer Richtliniendatei sichern, verwenden Sie entweder eine sofort verwendbare Sicherheitsassertion oder eine benutzerdefinierte Richtlinienassertion. Dem Authentifizierungsmodus eines [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Sicherheitsbindungselements werden die sofort verwendbaren Sicherheitsassertionen eng zugeordnet. Es werden nicht nur die [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Authentifizierungsmodi und die sofort verwendbaren WSE 3.0-Sicherheitsassertionen gleich oder ähnlich benannt, sondern sie sichern die Nachrichten unter Verwendung derselben Anmeldeinformationstypen. So wird z. B. wird die sofort verwendbare `usernameForCertificate`-Sicherheitsassertion in WSE 3.0 dem `UsernameForCertificate`-Authentifizierungsmodus in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] zugeordnet. Die folgenden Codebeispiele zeigen, wie eine minimale Richtlinie, die die sofort verwendbare `usernameForCertificate`-Sicherheitsassertion in WSE 3.0 verwendet, einem `UsernameForCertificate`-Authentifizierungsmodus in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in einer benutzerdefinierten Bindung zugeordnet wird.  
  
 **WSE 3.0**  
  
```  
<policies>  
  <policy name="MyPolicy">  
    <usernameForCertificate messageProtectionOrder="SignBeforeEncrypt"  
                            requireDeriveKeys="true"/>  
  </policy>  
</policies>  
```  
  
 **WCF**  
  
```  
<customBinding>  
  <binding name="MyBinding">  
    <security authenticationMode="UserNameForCertificate"   
              messageProtectionOrder="SignBeforeEncrypt"  
              requireDerivedKeys="true"/>  
  </binding>  
</customBinding>  
```  
  
 Um die Sicherheitseinstellungen eines WSE 3.0-Webdiensts, die in einer Richtliniendatei festgelegt sind, zu [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] zu migrieren, muss eine benutzerdefinierte Bindung in einer Konfigurationsdatei erstellt und die sofort anwendbare Sicherheitsassertion auf den entsprechenden Authentifizierungsmodus festgelegt werden. Darüber hinaus muss die benutzerdefinierte Bindung für die Verwendung der WS-Adressing-Spezifikation vom August 2004 konfiguriert werden, wenn WSE 3.0-Clients mit dem Dienst kommunizieren. Wenn der migrierte [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Dienst keine Kommunikation mit WSE 3.0-Clients erfordert und nur die Sicherheitsparität verwalten muss, sollten Sie die systemdefinierten [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Bindungen mit entsprechenden Sicherheitseinstellungen verwenden, statt eine benutzerdefinierte Bindung zu erstellen.  
  
 In der folgenden Tabelle ist die Zuordnung zwischen einer WSE 3.0-Richtliniendatei und der entsprechenden benutzerdefinierten Bindung in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] aufgelistet.  
  
|Sofort verwendbare WSE 3.0 Sicherheitsassertion|Konfiguration einer benutzerdefinierten WCF-Bindung|  
|----------------------------------------|--------------------------------------|  
|<usernameOverTransportSecurity></usernameOverTransportSecurity>\>|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="UserNameOverTransport" />     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|<mutualCertificate10Security></mutualCertificate10Security>\>|`<customBinding>   <binding name="MyBinding">     <security messageSecurityVersion="WSSecurity10WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10" authenticationMode="MutualCertificate" />     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|<usernameForCertificateSecurity></usernameForCertificateSecurity>\>|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="UsernameForCertificate"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|<anonymousForCertificateSecurity></anonymousForCertificateSecurity>\>|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="AnonymousForCertificate"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|<kerberosSecurity></kerberosSecurity>\>|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="Kerberos"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
|<mutualCertificate11Security></mutualCertificate11Security>\>|`<customBinding>   <binding name="MyBinding">     <security authenticationMode="MutualCertificate"/>     <textMessageEncoding messageVersion="Soap12WSAddressingAugust2004" />   </binding> </customBinding>`|  
  
 Weitere Informationen zum Erstellen benutzerdefinierter Bindungen in WCF finden Sie unter [benutzerdefinierte Bindungen](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
### <a name="wse-30-web-services-that-are-secured-using-application-code"></a>WSE 3.0-Webdienste, die mit einem Anwendungscode gesichert werden  
 Unabhängig davon, ob WSE 3.0 oder [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verwendet wird, können die Sicherheitsanforderungen im Anwendungscode statt in der Konfiguration festgelegt werden. Bei WSE 3.0 wird dies durch Erstellen einer Klasse, die sich von der `Policy`-Klasse ableitet, und dann durch Hinzufügen der Anforderungen durch Aufrufen der `Add`-Methode erreicht. Weitere Informationen zu die sicherheitsanforderungen im Code angeben, finden Sie unter [Gewusst wie: Sichern einer Webdiensts ohne Verwendung einer Richtliniendatei](http://go.microsoft.com/fwlink/?LinkId=73747). In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]sicherheitsanforderungen im Code festzulegen, erstellen Sie eine Instanz von der <xref:System.ServiceModel.Channels.BindingElementCollection> -Klasse und das Hinzufügen einer Instanz von einer <xref:System.ServiceModel.Channels.SecurityBindingElement> an der <xref:System.ServiceModel.Channels.BindingElementCollection>. Anforderungen an die Sicherheitsassertionen festgelegt werden, werden Hilfsmethoden der statischen Authentifizierungsmodus für die <xref:System.ServiceModel.Channels.SecurityBindingElement> Klasse. Ausführliche Informationen zum Festlegen von sicherheitsanforderungen im Code mithilfe [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], finden Sie unter [Gewusst wie: Erstellen einer benutzerdefinierten Bindung mit dem SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md) und [Gewusst wie: Erstellen eines SecurityBindingElement für einen angegebenen Authentifizierungsmodus](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md).  
  
### <a name="wse-30-custom-policy-assertion"></a>Benutzerdefinierte WSE 3.0-Richtlinienassertion  
 Bei WSE 3.0 gibt es zwei Typen von benutzerdefinierten Richtlinienassertionen: solche, die eine SOAP-Nachricht sichern, und solche, die keine SOAP-Nachricht sichern. Leiten Sie Policy-Assertionen, die SOAP-Nachrichten Sichern von WSE 3.0 `SecurityPolicyAssertion` -Klasse und das konzeptuelle Äquivalent in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ist die <xref:System.ServiceModel.Channels.SecurityBindingElement> Klasse.  
  
 Beachten Sie unbedingt, dass die sofort anwendbaren WSE 3.0-Sicherheitsassertionen eine Teilmenge der [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Authentifizierungsmodi sind. Wenn Sie in WSE 3.0 eine benutzerdefinierte Richtlinienassertion erstellt haben, kann es einen entsprechenden [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Authentifizierungsmodus geben. WSE 3.0 stellt z. B. keine CertificateOverTransport-Sicherheitsassertion bereit, die der sofort anwendbaren `UsernameOverTransport`-Sicherheitsassertion entspricht, verwendet aber ein X.509-Zertifikat für Clientauthentifizierungszwecke. Wenn Sie eine eigene benutzerdefinierte Richtlinienassertion für dieses Szenario festgelegt haben, ist die Migration mit [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ganz einfach. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]definiert einen Authentifizierungsmodus für dieses Szenario, damit Sie den Authentifizierungsmodus für die statischen Hilfsmethoden konfigurieren nutzen können eine [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] <xref:System.ServiceModel.Channels.SecurityBindingElement>.  
  
 Wenn keine [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] -Authentifizierungsmodus, der eine benutzerdefinierte Richtlinienassertion entspricht, die SOAP-Nachrichten sichert, leiten eine Klasse von <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>, <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> oder <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Klassen, und geben Sie das entsprechende Bindungselement. Weitere Informationen finden Sie unter [Gewusst wie: Erstellen einer benutzerdefinierten Bindung mit dem SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).  
  
 Um eine benutzerdefinierte Richtlinienassertion zu konvertieren, die nicht über eine SOAP-Nachricht sichert, finden Sie unter [filtern](../../../../docs/framework/wcf/feature-details/filtering.md) und im Beispiel [benutzerdefinierte Nachrichteninterceptor](../../../../docs/framework/wcf/samples/custom-message-interceptor.md).  
  
### <a name="wse-30-custom-security-token"></a>Benutzerdefiniertes WSE 3.0 Sicherheitstoken  
 Das [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Programmiermodell zum Erstellen eines benutzerdefinierten Tokens unterscheidet sich von dem in WSE 3.0. Ausführliche Informationen zum Erstellen eines benutzerdefinierten Tokens in WSE finden Sie unter [Erstellen benutzerdefinierter Sicherheitstoken](http://go.microsoft.com/fwlink/?LinkID=73750). Ausführliche Informationen zum Erstellen eines benutzerdefinierten Tokens in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], finden Sie unter [Gewusst wie: Erstellen eines benutzerdefinierten Tokens](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md).  
  
### <a name="wse-30-custom-token-manager"></a>Benutzerdefinierter WSE 3.0 Token-Manager  
 Das Programmiermodell zum Erstellen eines benutzerdefinierten Token-Managers in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterscheidet sich von dem in WSE 3.0. Ausführliche Informationen zum Erstellen einer benutzerdefinierten Sicherheitstoken-Manager und andere Komponenten, die für ein benutzerdefiniertes Sicherheitstoken erforderlich sind, finden Sie unter [Gewusst wie: Erstellen eines benutzerdefinierten Tokens](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md).  
  
> [!NOTE]
>  Wenn Sie einen benutzerdefinierten `UsernameToken`-Sicherheitstoken-Manager erstellt haben, stellt [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] einen einfacheren Mechanismus zur Verfügung, um die Authentifizierungslogik festzulegen, als das Erstellen eines benutzerdefinierten Sicherheitstoken-Managers. Weitere Informationen finden Sie unter [Gewusst wie: Verwenden Sie einen benutzerdefinierten Namen und Kennwort-Validierungssteuerelement](../../../../docs/framework/wcf/feature-details/how-to-use-a-custom-user-name-and-password-validator.md).  
  
### <a name="wse-30-web-services-that-use-mtom-encoded-soap-messages"></a>WSE 3.0-Webdienste, die MTOM-codierte SOAP-Nachrichten verwenden  
 Wie eine WSE 3-Anwendung kann eine [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Anwendung die MTOM-Nachrichtencodierung in der Konfiguration festlegen. Um diese Einstellung zu migrieren, fügen die [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/mtommessageencoding.md) der Bindung für den Dienst. Im folgenden Codebeispiel wird veranschaulicht, wie eine MTOM-Codierung in WSE 3.0 für einen Dienst festgelegt wird, der [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] entspricht.  
  
 **WSE 3.0**  
  
```  
<messaging>  
    <mtom clientMode="On"/>  
</messaging>  
```  
  
 **WCF**  
  
```  
<customBinding>  
  <binding name="MyBinding">  
    <mtomMessageEncoding/>  
  </binding>  
</customBinding>  
```  
  
## <a name="messaging"></a>Messaging  
  
### <a name="wse-30-applications-that-use-the-wse-messaging-api"></a>WSE 3.0-Anwendungen, die die WSE-Messaging-API verwenden  
 Wenn die WSE-Messaging-API verwendet wird, um direkten Zugriff auf die XML zu erhalten, die zwischen dem Client und dem Webdienst kommuniziert wird, kann die Anwendung so umgewandelt werden, dass sie "Plain Old XML" (POX) verwendet. Weitere Einzelheiten über POX finden Sie unter [Interoperabilität mit POX-Anwendungen](../../../../docs/framework/wcf/feature-details/interoperability-with-pox-applications.md). Weitere Informationen über die WSE-Messaging-API finden Sie unter [senden und Empfangen von SOAP-Nachrichten mithilfe von WSE-Messaging-API](http://go.microsoft.com/fwlink/?LinkID=73755).  
  
## <a name="transports"></a>Transportprotokolle  
  
### <a name="tcp"></a>TCP  
 Standardmäßig interoperieren WSE 3.0-Clients und -Webdienste, die SOAP-Nachrichten mittels TCP-Transport senden, nicht mit [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Clients und -Webdiensten. Diese Inkompatibilität beruht auf Unterschieden in dem im TCP-Protokoll verwendeten Rahmen und auf Leistungsgründen. Ein [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Beispiel veranschaulicht, wie eine benutzerdefinierte TCP-Sitzung implementiert wird, die mit WSE 3.0 zusammenwirkt. Weitere Informationen zu diesem Beispiel finden Sie unter [Transport: WSE 3.0-TCP-Interoperabilität](../../../../docs/framework/wcf/samples/transport-wse-3-0-tcp-interoperability.md).  
  
 Um anzugeben, dass ein [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Anwendung verwendet den TCP-Transport, mit der [ <> \</> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md).  
  
### <a name="custom-transport"></a>Benutzerdefinierter Transport  
 Die Entsprechung eines benutzerdefinierten WSE 3.0-Transports in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ist eine Kanalerweiterung. Weitere Informationen zum Erstellen einer kanalerweiterung finden Sie unter [Erweitern der Kanalschicht](../../../../docs/framework/wcf/extending/extending-the-channel-layer.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegender Programmierlebenszyklus](../../../../docs/framework/wcf/basic-programming-lifecycle.md)   
 [Benutzerdefinierte Bindungen](../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [Gewusst wie: Erstellen einer benutzerdefinierten Bindung mit dem SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [Gewusst wie: Erstellen eines SecurityBindingElement für einen angegebenen Authentifizierungsmodus](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)