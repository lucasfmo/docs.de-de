---
title: "&lt;discoveryEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fae2f48b-a635-4e4b-859d-a1432ac37e1c
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;discoveryEndpoint&gt;
Dieses Konfigurationselement definiert einen Standardendpunkt mit einem festen Ermittlungsvertrag.  Wenn es der Dienstkonfiguration hinzugefügt wird, gibt es an, wo die Überwachung auf Ermittlungsnachrichten erfolgen soll.  Wenn es der Clientkonfiguration hinzugefügt wird, gibt es an, wohin die Ermittlungsabfragen gesendet werden sollen.  
  
## Syntax  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <discoveryEndpoint>   
          <standardEndpoint  
                  discoveryMode=”Adhoc/Managed”  
                  discoveryVersion=”WSDiscovery11/WSDiscoveryApril2005”  
                  maxResponseDelay=”Timespan”   
                  name="String" />  
       </discoveryEndpoint>          
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|discoveryMode|Eine Zeichenfolge, die den Modus des Suchprotokolls angibt.  Gültige Werte sind "Adhoc" und "Managed".  Im verwalteten Modus benötigt das Protokoll einen Suchproxy, der als Repository sichtbarer Dienste fungiert.  Der Ad\-hoc\-Modus erfordert, dass das Protokoll den UDP\-Multicastmechanismus verwendet, um verfügbare Dienste zu suchen.  Dieser Wert ist vom Typ <xref:System.Servicemodel.Discovery.DiscoveryMode>.|  
|discoveryVersion|Eine Zeichenfolge, die eine der zwei Versionen des WS\-Suchprotokolls angibt.  Gültige Werte sind WSDiscovery11 und WSDiscoveryApril2005.  Dieser Wert ist vom Typ <xref:System.Servicemodel.Discovery.DiscoveryVersion>.|  
|maxResponseDelay|Ein Timespan\-Wert, der den maximalen Wert für die Verzögerung angibt, den das Suchprotokoll wartet, bis bestimmte Meldungen gesendet werden, z. B. "Probe Match" oder "Resolve Match".<br /><br /> Wenn alle ProbeMatches zur gleichen Zeit gesendet werden, kann es zu einer Netzwerküberlastung kommen.  Um zu verhindern, dass dieser Fall eintritt, werden ProbeMatches mit einer zufälligen Verzögerung zwischen den ProbeMatches gesendet.  Die zufällige Verzögerung liegt im Bereich zwischen 0 und dem Wert, der von diesem Attribut festgelegt wurde.  Wenn dieses Attribut auf 0 festgelegt wird, werden die ProbeMatches\-Meldungen in einer engen Schleife ohne Verzögerung gesendet.  Andernfalls werden die ProbeMatches\-Meldungen mit einer zufällig festgelegten Verzögerung gesendet, sodass die Gesamtzeit zum Senden aller ProbeMatches\-Meldungen den maxResponseDelay\-Wert nicht überschreitet.  Dieser Wert ist nur für Dienste relevant, er wird nicht von Clients verwendet.|  
|`name`|Eine Zeichenfolge, die den Namen der Konfiguration des Standardendpunkts angibt.  Der Name wird im `endpointConfiguration`\-Attribut des Dienstendpunkts zum Verknüpfen eines Standardendpunkts mit der Konfiguration verwendet.|  
  
### Untergeordnete Elemente  
 Keine  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|Eine Auflistung von Standardendpunkten, bei denen es sich um vordefinierte Endpunkte handelt, für die eine oder mehrere Eigenschaften \(Adresse, Bindung, Vertrag\) fest vorgegeben sind.|  
  
## Beispiel  
 Das folgende Beispiel zeigt einen Dienst, der einen Multicasttransport in einem Peernetzwerk auf Ermittlungsnachrichten überwacht.  Im Beispiel wird explizit die Version WS\-Discovery April 2005 angegeben.  
  
 Die Standardendpunktkonfiguration wird pro Dienst definiert und kann nicht dienstübergreifend freigegeben werden.  Wenn ein anderer Dienst den gleichen Ermittlungsendpunkt haben soll, muss dem Abschnitt dieses Diensts die gleiche Konfiguration hinzugefügt werden.  
  
```  
  
<services>  
    <service name="CalculatorService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
             <endpoint binding="basicHttpBinding"   
                address="calculator" contract="ICalculatorService" />  
             <endpoint name="peerNetDiscovery"  
                binding="peerTcpBinding"  
                address="net.p2p://discoveryMesh/multicast"  
                kind="discoveryEndpoint"  
                endpointConfiguration="peerTcpDiscoveryEndpointConfiguration"  
                bindingConfiguration="discoveryPeerTcpBindingConfig" />      
   </service>  
</services>  
<standardEndpoints>  
  <discoveryEndpoint>  
     <standardEndpoint name="peerTcpDiscoveryEndpointConfiguration "                         
                       version="WSDiscoveryApril2005" />  
   </discoveryEndpoint>  
</standardEndpoints>  
  
```  
  
## Siehe auch  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>