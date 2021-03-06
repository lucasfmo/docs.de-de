---
title: "&lt;ws2007FederationHttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9af4ec79-cdef-457e-9dca-09d5eb821594
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;ws2007FederationHttpBinding&gt;
Eine sichere und vollständig kompatible Bindung, die von [\<wsFederationHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md) abgeleitet ist und Verbundsicherheit unterstützt.  
  
## Syntax  
  
```  
  
<ws2007FederationHttpBinding>  
    <binding   
        bypassProxyOnLocal="Boolean"  
        closeTimeout="TimeSpan"   
        hostNameComparisonMode="StrongWildcard/Exact/WeakWildcard"  
        maxBufferPoolSize="integer"  
        maxReceivedMessageSize="integer"  
        messageEncoding="Text/Mtom"   
                name="string"  
        openTimeout="TimeSpan"   
        privacyNoticeAt="Uri"  
        privacyNoticeVersion="Integer"  
        proxyAddress="Uri"   
        receiveTimeout="TimeSpan"  
        sendTimeout="TimeSpan"  
        textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding"  
        transactionFlow="Boolean"  
        useDefaultWebProxy="Boolean">  
        <security mode="None/Message/TransportWithMessageCredential">  
           <message negotiateServiceCredential="Boolean"  
                algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
                issuedTokenType="string"  
                issuedKeyType="SymmetricKey/PublicKey"  
           </message>  
        </security>  
        <reliableSession ordered="Boolean"  
           inactivityTimeout="TimeSpan"  
           enabled="Boolean" />  
       <readerQuotas   
            maxArrayLength="Integer"  
            maxBytesPerRead="Integer"  
            maxDepth="Integer"   
            maxNameTableCharCount="Integer"           
            maxStringContentLength="Integer" />  
    </binding>  
</ws2007FederationHttpBinding>  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|`bypassProxyOnLocal`|Ein Wert, der angibt, ob der Proxyserver bei lokalen Adressen umgangen werden soll.  Die Standardeinstellung ist `false`.|  
|`closeTimeout`|Ein <xref:System.TimeSpan>\-Wert, der das Zeitintervall für den Abschluss eines Schließvorgangs angibt.  Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein.  Der Standardwert ist 00:01:00.|  
|`hostnameComparisonMode`|Gibt den HTTP\-Hostnamen\-Vergleichsmodus an, der verwendet wird, um URIs zu analysieren.  Dieses Attribut ist vom Typ <xref:System.ServiceModel.HostnameComparisonMode> und gibt an, ob beim Abgleich des URI der Hostname zum Erreichen des Dienstes verwendet wird.  Der Standardwert lautet <xref:System.ServiceModel.HostnameComparisonMode.StrongWildcard>, wodurch der Hostname beim Abgleich ignoriert wird.|  
|`maxBufferPoolSize`|Die maximale Pufferpoolgröße dieser Bindung.  Der Standardwert ist 524.288 Byte \(512 \* 1024\).  Viele Teile von [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] verwenden Puffer.  Das Erstellen und Zerstören von Puffern bei jeder Verwendung ist kostspielig. Dasselbe gilt für die Garbage Collection für Puffer.  Bei Pufferpools können Sie einen zu verwendenden Puffer aus dem Pool nehmen und ihn nach der Verwendung wieder dem Pool zuführen.  So wird der Aufwand beim Erstellen und Zerstören von Puffern vermieden.|  
|`maxReceivedMessageSize`|Die maximale Nachrichtengröße in Byte einschließlich Header, die in einem für diese Bindung konfigurierten Kanal beim Nachrichtenempfang zulässig ist.  Der Absender einer Nachricht, die diesen Grenzwert überschreitet, erhält einen SOAP\-Fehler.  Der Empfänger verwirft die Nachricht und erstellt einen Eintrag des Ereignisses im Ablaufverfolgungsprotokoll.  Der Standard ist 65536.|  
|`messageEncoding`|Definiert den Encoder, der verwendet wird, um die SOAP\-Nachricht zu codieren.  Folgende Werte sind gültig:<br /><br /> -   Text: Verwenden Sie einen Textnachrichtenencoder.<br />-   Mtom: Verwendung eines MTOM\-Encoders \(Message Transmission Organisation Mechanism 1.0\).<br /><br /> Der Standardwert ist Text.<br /><br /> Dieses Attribut ist vom Typ <xref:System.ServiceModel.WSMessageEncoding>.|  
|`name`|Der Konfigurationsname der Bindung.  Dieser Wert sollte eindeutig sein, da er von der Bindung zur Identifizierung verwendet wird.  Ab [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)] müssen Bindungen und Verhalten keinen Namen aufweisen.  Weitere Informationen zu Standardkonfiguration und zu namenlosen Bindungen und Verhalten finden Sie unter [Vereinfachte Konfiguration](../../../../../docs/framework/wcf/simplified-configuration.md) und [Vereinfachte Konfiguration für WCF\-Dienste](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|`openTimeout`|Ein <xref:System.TimeSpan>\-Wert, der das Zeitintervall für den Abschluss eines Öffnungsvorgangs angibt.  Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein.  Der Standardwert ist 00:01:00.|  
|`privactyNoticeAt`|Ein URI, an dem sich der Datenschutzhinweis befindet.|  
|`privactyNoticeVersion`|Die Version des aktuellen Datenschutzhinweises.|  
|`proxyAddress`|Ein URI, der die Adresse des HTTP\-Proxys angibt.  Wenn `useDefaultWebProxy` `true` ist, muss diese Einstellung `null` lauten.  Die Standardeinstellung ist `null`.|  
|`receiveTimeout`|Ein <xref:System.TimeSpan>\-Wert, der das Zeitintervall für den Abschluss eines Empfangsvorgangs angibt.  Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein.  Der Standardwert ist 00:10:00.|  
|`sendTimeout`|Ein <xref:System.TimeSpan>\-Wert, der das Zeitintervall für den Abschluss eines Sendevorgangs angibt.  Dieser Wert muss größer oder gleich <xref:System.TimeSpan.Zero> sein.  Der Standardwert ist 00:01:00.|  
|`textEncoding`|Legt die Zeichensatzkodierung fest, die zum Ausgeben von Nachrichten über die Bindung verwendet werden soll.  Folgende Werte sind gültig:<br /><br /> -   BigEndianUnicode: Unicode BigEndian\-Codierung.<br />-   Unicode: 16\-Bit\-Codierung.<br />-   UTF8: 8\-Bit\-Codierung.<br /><br /> Der Standard ist UTF8.  Dieses Attribut ist vom Typ <xref:System.Text.Encoding>.|  
|`transactionFlow`|Ein Wert, der angibt, ob die Bindung geleitete WS\-Transaktionen unterstützt.  Die Standardeinstellung ist `false`.|  
|`useDefaultWebProxy`|Ein Wert, der angibt, ob der automatisch konfigurierte HTTP\-Proxy des Systems verwendet wird.  Die Proxyadresse muss `null` sein \(das heißt, sie ist nicht festgelegt\), wenn dieses Attribut den Wert `true` hat.  Die Standardeinstellung ist `true`.|  
  
### Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<Sicherheit\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wsfederationhttpbinding.md)|Definiert die Sicherheitseinstellungen für die Nachricht.  Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.WSFederationHttpSecurityElement>.|  
|[\<readerQuotas\>](../Topic/%3CreaderQuotas%3E.md)|Definiert die Beschränkungen der Komplexität von SOAP\-Nachrichten, die von Endpunkten verarbeitet werden können, die mit dieser Bindung konfiguriert wurden.  Dieses Element ist vom Typ <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.|  
|[reliableSession](http://msdn.microsoft.com/de-de/9c93818a-7dfa-43d5-b3a1-1aafccf3a00b)|Gibt an, ob zuverlässige Sitzungen zwischen Kanalendpunkten aufgebaut werden.|  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<Bindungen\>](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|Dieses Element enthält eine Auflistung von standardmäßigen und benutzerdefinierten Bindungen.|  
  
## Hinweise  
 Ein Verbund zeichnet sich durch die Möglichkeit aus, Identitäten in mehreren Unternehmen oder vertrauenswürdigen Domänen für Authentifizierung und Autorisierung freizugeben.  Er verwendet das WS\-Trust\-Protokoll, um die Identitätsdarstellung von einer vertrauenswürdigen Domäne zu einer anderen zuzuordnen.  Eine verbundene HTTP\-Bindung unterstützt sowohl SOAP\-Sicherheit als auch Sicherheit im gemischten Modus, jedoch keine Transportsicherheit.  Mit dieser Bindung konfigurierte Dienste müssen den HTTP\-Transport verwenden.  [!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [\<wsFederationHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md).  
  
## Beispiel  
  
```  
<configuration>  
<system.ServiceModel>  
<bindings>  
<ws2007FederationHttpBinding>  
    <binding   
        bypassProxyOnLocal="false"  
        transactionFlow="false"  
        hostNameComparisonMode="WeakWildcard"  
        maxReceivedMessageSize="1000"  
        messageEncoding="Mtom"   
        proxyAddress="http://www.contoso.com"   
        textEncoding="Utf16TextEncoding"  
        useDefaultWebProxy="false">  
        <reliableSession ordered="false"  
            inactivityTimeout="00:02:00" enabled="true" />  
        <security mode="None">  
           <message negotiateServiceCredential="false"  
                algorithmSuite="Aes128"  
                issuedTokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1"   
                issuedKeyType="PublicKey">  
               <issuer address="http://localhost/Sts" />  
           </message>  
        </security>  
    </binding>  
</ws2007FederationBinding>  
</bindings>  
</system.ServiceModel>  
</configuration>  
```  
  
## Siehe auch  
 <xref:System.ServiceModel.WS2007FederationHttpBinding>   
 <xref:System.ServiceModel.Configuration.WS2007FederationHttpBindingElement>   
 [\<wsFederationHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)   
 [Bindungen](../../../../../docs/framework/wcf/bindings.md)   
 [Konfigurieren der vom System bereitgestellten Bindungen](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/de-de/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<Bindung\>](../../../../../docs/framework/misc/binding.md)