---
title: "Verwenden von Bindungen, um Dienste und Clients zu konfigurieren | Microsoft Docs"
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
helpviewer_keywords: 
  - "Bindungen [WCF], Verwenden"
ms.assetid: c39479c3-0766-4a17-ba4c-97a74607f392
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# Verwenden von Bindungen, um Dienste und Clients zu konfigurieren
Bindungen sind Objekte, die die zum Herstellen einer Verbindung zu einem Endpunkt erforderlichen Kommunikationsdetails angeben.  Genauer gesagt enthalten Bindungen Konfigurationsinformationen, die zum Erstellen der Client\- oder Dienstlaufzeit durch Festlegen der Merkmale von Transporten, Übertragungsformaten \(Nachrichtencodierung\) und Protokollen für den entsprechenden Endpunkt oder Clientkanal verwendet werden.  Um einen funktionierenden [!INCLUDE[indigo1](../../../includes/indigo1-md.md)]\-Dienst zu erstellen, ist für jeden Endpunkt im Dienst eine Bindung erforderlich.  In diesem Thema wird erläutert, was Bindungen sind, wie sie definiert werden und wie eine bestimmte Bindung für einen Endpunkt angegeben wird.  
  
## Was eine Bindung definiert  
 Die Informationen in einer Bindung können sehr einfach oder sehr komplex sein.  Die einfachste Bindung gibt nur das Transportprotokoll \(wie HTTP\) an, das für die Verbindung zum Endpunkt verwendet werden muss.  Allgemeiner gesagt fallen die Informationen in einer Bindung zur Verbindung mit einem Endpunkt in eine der Kategorien in der folgenden Tabelle.  
  
 Protokolle  
 Bestimmt den verwendeten Sicherheitsmechanismus, entweder zuverlässige Messagingfähigkeit oder Transaktionskontextablauf\-Einstellungen.  
  
 Transport  
 Bestimmt das zu verwendende zugrunde liegende Transportprotokoll \(z. B. TCP oder HTTP\).  
  
 Codierung  
 Bestimmt die Nachrichtencodierung, z. B. Text\/XML, binär oder MTOM \(Message Transmission Optimization Mechanism\), die festlegt, wie Nachrichten bei Übertragungen als Bytestreams dargestellt werden.  
  
## Vom System bereitgestellte Bindungen  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] schließt mehrere vom System bereitgestellte Bindungen ein, die die meisten Anwendungsanforderungen und Szenarien abdecken sollen.  Die folgenden Klassen stellen einige Beispiele für vom System bereitgestellte Bindungen dar:  
  
-   <xref:System.ServiceModel.BasicHttpBinding>: Eine für Verbindungen zu Webdiensten geeignete HTTP\-Protokollbindung, die der WS\-I Basic Profile 1.1\-Spezifikation entspricht \(z. B. ASP.NET\-Webdienste \[ASMX\]\-basierte Dienste\).  
  
-   <xref:System.ServiceModel.WsHttpBinding>: Eine für Verbindungen zu Endpunkten geeignete HTTP\-Protokollbindung, die den Webdienstespezifikations\-Protokollen entspricht.  
  
-   <xref:System.ServiceModel.NetNamedPipeBinding>: Verwendet die binäre .NET\-Codierung und Rahmentechnologien zusammen mit dem Transport mittels benannter Pipes von Windows zur Verbindung mit anderen [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Endpunkten auf dem gleichen Computer.  
  
-   <xref:System.ServiceModel.NetMsmqBinding>: Verwendet die binäre .NET\-Codierung und Rahmentechnologien zusammen mit Message Queuing \(MSMQ\) zum Erstellen von Verbindung für Nachrichten in der Warteschlange mit anderen [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Endpunkten.  
  
 Eine vollständige Liste vom System bereitgestellter Bindungen mit Beschreibungen finden Sie unter [Vom System bereitgestellte Bindungen](../../../docs/framework/wcf/system-provided-bindings.md).  
  
## Benutzerdefinierte Bindungen  
 Wenn die Auflistung vom System bereitgestellter Bindungen nicht die richtige Kombination von Funktionen aufweist, die für eine Dienstanwendung erforderlich ist, können Sie eine <xref:System.ServiceModel.Channels.CustomBinding>\-Bindung erstellen.  [!INCLUDE[crabout](../../../includes/crabout-md.md)] die Elemente einer <xref:System.ServiceModel.Channels.CustomBinding>\-Bindung finden Sie unter [\<customBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) und [Benutzerdefinierte Bindungen](../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## Verwenden von Bindungen  
 Das Verwenden von Bindungen umfasst zwei grundlegende Schritte:  
  
1.  Auswählen oder Definieren einer Bindung.  Die einfachste Methode ist, eine vom System bereitgestellte Bindung auszuwählen und ihre Standardeinstellungen zu verwenden.  Sie können auch eine vom System bereitgestellte Bindung auswählen und ihre Eigenschaftswerte zurücksetzen, um sie Ihren Anforderungen anzupassen.  Alternativ können Sie eine benutzerdefinierte Bindung erstellen und jede Eigenschaft nach Bedarf festlegen.  
  
2.  Erstellen eines Endpunkts, der diese Bindung verwendet.  
  
## Code und Konfiguration  
 Sie können Bindungen durch Code bzw. Konfiguration definieren oder konfigurieren.  Diese beiden Ansätze sind unabhängig vom verwendeten Bindungstyp, z. B. ob Sie eine vom System bereitgestellte Bindung oder eine <xref:System.ServiceModel.Channels.CustomBinding>\-Bindung verwenden.  Im Allgemeinen gibt Ihnen die Verwendung von Code die vollständige Kontrolle über die Definition einer Bindung beim Kompilieren.  Bei der Konfiguration kann ein Systemadministrator oder der Benutzer eines [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Dienstes oder \-Clients wiederum die Parameter von Bindungen ändern.  Diese Flexibilität ist häufig wünschenswert, da die spezifischen Computeranforderungen und Netzwerkbedingungen, in die eine [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\-Anwendung bereitgestellt werden soll, nicht vorhersehbar sind.  Durch die Trennung der Bindungsinformationen \(und Addressierungsinformationen\) vom Code können Administratoren die Bindungsdetails ändern, ohne dass die Anwendung neu kompiliert oder bereitgestellt werden muss.  Falls die Bindung im Code definiert ist, überschreibt sie alle in der Konfigurationsdatei vorgenommenen konfigurationsbasierten Definitionen.  Beispiele für diese Ansätze finden Sie in den folgenden Themen:  
  
-   [Gewusst wie: Hosten eines WCF\-Diensts in einer verwalteten Anwendung](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md) enthält ein Beispiel für das Erstellen einer Bindung im Code.  
  
-   [Gewusst wie: Konfigurieren eines Clients](../../../docs/framework/wcf/how-to-configure-a-basic-wcf-client.md) enthält ein Beispiel für das Erstellen eines Clients mit der Konfiguration.  
  
## Siehe auch  
 [Übersicht über die Endpunkterstellung](../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [Vorgehensweise: Angeben einer Dienstbindung in einer Konfiguration](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)   
 [Vorgehensweise: Angeben einer Dienstbindung im Code](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-code.md)   
 [Vorgehensweise: Angeben einer Clientbindung in einer Konfiguration](../../../docs/framework/wcf/how-to-specify-a-client-binding-in-configuration.md)   
 [Vorgehensweise: Angeben einer Clientbindung im Code](../../../docs/framework/wcf/how-to-specify-a-client-binding-in-code.md)