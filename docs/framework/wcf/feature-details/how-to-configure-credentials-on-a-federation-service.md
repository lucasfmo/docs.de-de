---
title: "Vorgehensweise: Konfigurieren von Anmeldeinformationen auf einem Verbunddienst | Microsoft Docs"
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
  - "Verbund"
  - "WCF, Verbund"
ms.assetid: 149ab165-0ef3-490a-83a9-4322a07bd98a
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Vorgehensweise: Konfigurieren von Anmeldeinformationen auf einem Verbunddienst
In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] wird ein Verbunddienst mit folgenden Hauptschritten erstellt:  
  
1.  <xref:System.ServiceModel.WSFederationHttpBinding> oder einer ähnlichen benutzerdefinierten Bindung konfigurieren.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] zum Erstellen einer entsprechenden Bindung finden Sie unter [Vorgehensweise: Erstellen einer WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md).  
  
2.  Konfigurieren von <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>, die kontrollieren, wie dem Dienst präsentierte ausgestellte Token authentifiziert werden.  
  
 Dieses Thema enthält Details über den zweiten Schritt.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] darüber, wie ein Verbunddienst funktioniert, finden Sie unter [Verbund](../../../../docs/framework/wcf/feature-details/federation.md).  
  
### So legen Sie die Eigenschaften von IssuedTokenServiceCredential in Code fest  
  
1.  Verwenden Sie die <xref:System.ServiceModel.Description.ServiceCredentials.IssuedTokenAuthentication%2A>\-Eigenschaft der <xref:System.ServiceModel.Description.ServiceCredentials>\-Klasse, um einen Verweis an eine <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>\-Instanz zurückzugeben.Der Zugriff auf die Eigenschaft erfolgt über die <xref:System.ServiceModel.ServiceHostBase.Credentials%2A>\-Eigenschaft der <xref:System.ServiceModel.ServiceHostBase>\-Klasse.  
  
2.  Legen Sie die <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.AllowUntrustedRsaIssuers%2A>\-Eigenschaft auf `true` fest, wenn selbst ausgestellte Token wie [!INCLUDE[infocard](../../../../includes/infocard-md.md)]\-Karten authentifiziert werden sollen.Der Standardwert ist `false`.  
  
3.  Füllen Sie die von der <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A>\-Eigenschaft zurückgegebene Sammlung mit Instanzen der <xref:System.Security.Cryptography.X509Certificates.X509Certificate2>\-Klasse auf.Jede Instanz stellt einen Aussteller dar, von dem der Dienst Token authentifiziert.  
  
    > [!NOTE]
    >  Im Gegensatz zur clientseitigen Sammlung, die von der <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A>\-Eigenschaft zurückgegeben wird, handelt es sich bei der Sammlung bekannter Zertifikate nicht um eine schlüsselgebundene Sammlung.Der Dienst akzeptiert die Token, die die angegebenen Zertifikate unabhängig von der Adresse des Clients, der die Nachricht mit dem ausgestellten Token gesendet hat, ausstellen \(mit gewissen Einschränkungen, die später in diesem Thema beschrieben werden\).  
  
4.  Legen Sie die <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A>\-Eigenschaft auf einen der <xref:System.ServiceModel.Security.X509CertificateValidationMode>\-Enumerationswerte fest.Dies kann nur in Code erfolgen.Die Standardeinstellung ist <xref:System.IdentityModel.Selectors.X509CertificateValidator.ChainTrust%2A>.  
  
5.  Wenn die <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A>\-Eigenschaft auf <xref:System.ServiceModel.Security.X509CertificateValidationMode> gesetzt ist, weisen Sie eine Instanz der benutzerdefinierten <xref:System.IdentityModel.Selectors.X509CertificateValidator>\-Klasse zur <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CustomCertificateValidator%2A>\-Eigenschaft zu.  
  
6.  Wenn <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> auf `ChainTrust` oder `PeerOrChainTrust` eingestellt ist, legen Sie die <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.RevocationMode%2A>\-Eigenschaft auf einen entsprechenden Wert aus der <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>\-Enumeration fest.Beachten Sie, dass der Sperrmodus nicht im `PeerTrust`\-Validierungsmodus oder im `Custom`\-Validierungsmodus verwendet wird.  
  
7.  Weisen Sie, sofern erforderlich, eine Instanz einer benutzerdefinierten <xref:System.IdentityModel.Tokens.SamlSerializer>\-Klasse zur <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.SamlSerializer%2A>\-Eigenschaft zu.Ein benutzerdefiniertes SAML\-Serialisierungsprogramm \(Security Assertions Markup Language\) wird benötigt, z. B. zum Analysieren von benutzerdefinierten SAML\-Assertionen.  
  
### So legen Sie die Eigenschaften von IssuedTokenServiceCredential in der Konfiguration fest  
  
1.  Erstellen Sie ein `<issuedTokenAuthentication>`\<`-Element als untergeordnetes Element eines serviceCredentials`\>\-Elements.  
  
2.  Legen Sie das `allowUntrustedRsaIssuers`\-Attribut des `<issuedTokenAuthentication>`\-Elements auf `true` fest, wenn die Authentifizierung ein selbst ausgestelltes Token ist, wie z. B. eine [!INCLUDE[infocard](../../../../includes/infocard-md.md)]\-Karte.  
  
3.  Erstellen Sie ein `<knownCertificates>``<issuedTokenAuthentication>-Element als untergeordnetes Element des` \-Elements.  
  
4.  Erstellen Sie null oder mehr `<add>``<knownCertificates>-Elemente als untergeordnete Elemente des` `storeLocation``-Elements, und geben Sie mithilfe der storeName``, dem x509FindType``-Attribut, dem findValue`\-Attribut und dem \-Attribut an, wie das Zertifikat zu finden ist.  
  
5.  Legen Sie ggf. das `samlSerializer`\-Attribut des \<`issuedTokenAuthentication`\>\-Elements auf den Typnamen der benutzerdefinierten <xref:System.IdentityModel.Tokens.SamlSerializer>\-Klasse fest.  
  
## Beispiel  
 Im folgenden Beispiel werden die Eigenschaften von <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> in Code festgelegt.  
  
 [!code-csharp[C_FederatedService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_federatedservice/cs/source.cs#2)]
 [!code-vb[C_FederatedService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_federatedservice/vb/source.vb#2)]  
  
 Damit ein Verbunddienst einen Client authentifizieren kann, muss Folgendes für das ausgestellte Token zutreffen:  
  
-   Wenn die digitale Signatur des ausgestellten Tokens einen RSA\-Sicherheitsschlüsselbezeichner verwendet, muss die <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.AllowUntrustedRsaIssuers%2A>\-Eigenschaft `true` lauten.  
  
-   Wenn die Signatur des ausgestellten Tokens eine Seriennummer eines X.509\-Ausstellers, einen Subjektschlüsselbezeichner des X.509\-Zertifikats oder einen Fingerabdruck\-Sicherheitsbezeichner des X.509\-Zertifikats verwendet, muss das ausgestellte Token von einem Zertifikat in der Sammlung signiert sein, die von der <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A>\-Eigenschaft der <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>\-Klasse zurückgegeben wurde.  
  
-   Wenn das ausgestellte Token mit einem X.509\-Zertifikat signiert ist, muss das Zertifikat anhand der semantischen Informationen validiert werden, die vom Wert der <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A>\-Eigenschaft angegeben werden, unabhängig davon, ob das Zertifikat als <xref:System.IdentityModel.Tokens.X509RawDataKeyIdentifierClause> an die vertrauende Seite gesendet wurde oder von der <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A>\-Eigenschaft stammt.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] zur Validierung des X.509\-Zertifikats finden Sie unter [Verwenden von Zertifikaten](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
 Durch Festlegen von <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> auf <xref:System.ServiceModel.Security.X509CertificateValidationMode> würde beispielsweise jedes ausgestellte Token, dessen Signaturzertifikat im `TrustedPeople`\-Zertifikatspeicher abgelegt ist, authentifiziert werden.Legen Sie in diesem Fall die <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.TrustedStoreLocation%2A>\-Eigenschaft entweder auf <xref:System.Security.Cryptography.X509Certificates.StoreLocation> oder auf <xref:System.Security.Cryptography.X509Certificates.StoreLocation> fest.Sie können andere Modi auswählen, einschließlich <xref:System.ServiceModel.Security.X509CertificateValidationMode>.Bei Auswahl von `Custom` müssen Sie eine Instanz der <xref:System.IdentityModel.Selectors.X509CertificateValidator>\-Klasse zur <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CustomCertificateValidator%2A>\-Eigenschaft zuweisen.Das benutzerdefinierte Validierungssteuerelement kann Zertifikate mit allen beliebigen Kriterien überprüfen.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Vorgehensweise: Erstellen eines Dienstes, der ein benutzerdefiniertes Zertifikats\-Validierungssteuerelement verwendet](../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md).  
  
## Siehe auch  
 [Verbund](../../../../docs/framework/wcf/feature-details/federation.md)   
 [Verbund und Vertrauenswürdigkeit](../../../../docs/framework/wcf/feature-details/federation-and-trust.md)   
 [Verbundbeispiel](../../../../docs/framework/wcf/samples/federation-sample.md)   
 [Vorgehensweise: Deaktivieren sicherer Sitzungen auf einer WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)   
 [Vorgehensweise: Erstellen einer WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)   
 [Vorgehensweise: Erstellen eines Verbundclients](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [Verwenden von Zertifikaten](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [SecurityBindingElement\-Authentifizierungsmodi](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md)