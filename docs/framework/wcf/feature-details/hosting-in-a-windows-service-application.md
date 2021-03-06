---
title: "Hosten in einer Windows-Dienstanwendung | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4199998-27f3-4dd9-aee4-0a4addfa9f24
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Hosten in einer Windows-Dienstanwendung
Windows\-Dienste \(früher Windows NT\-Dienste\) bieten ein Prozessmodell, das besonders für Anwendungen geeignet ist, die sich in ausführbaren Dateien mit langer Laufzeit befinden müssen und keinerlei Benutzeroberfläche anzeigen.  Die Prozesslebensdauer einer Windows\-Dienstanwendung wird vom Dienststeuerungs\-Manager \(Service Control Manager, SCM\) verwaltet, mit dem Sie Windows\-Dienstanwendungen starten, beenden und anhalten können.  Sie können einen Windows\-Dienstprozess so konfigurieren, dass er beim Hochfahren des Computers automatisch gestartet wird. So wäre der Prozess eine angemessene Hostingumgebung für Anwendungen, die “immer aktiviert” sind.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] zu Windows\-Dienstanwendungen finden Sie unter [Windows\-Dienstanwendungen](http://go.microsoft.com/fwlink/?LinkId=89450).  
  
 Anwendungen, die [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Dienste mit langer Laufzeit hosten, haben viele Gemeinsamkeiten mit Windows\-Diensten.  Dies gilt insbesondere für [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienste, die ausführbare Serverdateien mit langer Laufzeit sind, nicht direkt mit dem Benutzer interagieren und deswegen keinerlei Benutzeroberfläche implementieren.  Damit ist das Hosten von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Diensten innerhalb einer Windows\-Dienstanwendung eine gute Möglichkeit für die Erstellung robuster [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Anwendungen mit langer Laufzeit.  
  
 Oft müssen sich [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Entwickler entscheiden, ob sie ihre [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Anwendung in einer Windows\-Dienstanwendung oder in der Hostingumgebung von Internetinformationsdiensten \(IIS\) oder Windows Process Activation Service \(WAS\) hosten sollen.  Unter folgenden Bedingungen sollen Sie die Verwendung von Windows\-Dienstanwendungen in Erwägung ziehen:  
  
-   Die Anwendung erfordert explizite Aktivierung.  Beispielsweise sollten Sie Windows\-Dienste verwenden, wenn die Anwendung automatisch beim Serverstart gestartet werden soll, statt dynamisch als Antwort auf die erste eingehende Nachricht.  
  
-   Der Prozess, der die Anwendung hostet, muss nach dem Start weiterhin ausgeführt werden.  Nach dem Start wird ein Windows\-Dienstprozess solange ausgeführt, bis er explizit von einem Serveradministrator über den Dienststeuerungs\-Manager beendet wird.  In IIS oder WAS gehostete Anwendungen können dynamisch gestartet und beendet werden, um die Systemressourcen optimal zu nutzen.  Anwendungen, die explizite Steuerung während der gesamten Lebensdauer ihres Hostingprozesses erfordern, sollten Windows\-Dienste anstelle von IIS oder WAS verwenden.  
  
-   Der [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienst muss auf Windows&\#160;Server&\#160;2003 ausgeführt werden und andere Transportoptionen als HTTP verwenden.  Auf Windows&\#160;Server&\#160;2003 ist die [!INCLUDE[iis601](../../../../includes/iis601-md.md)]\-Hostumgebung auf HTTP\-Kommunikation beschränkt.  Windows\-Dienstanwendungen fallen nicht unter diese Beschränkung und können jede von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] unterstützte Transportart verwenden, darunter net.tcp, net.pipe und net.msmq.  
  
### So hosten Sie WCF innerhalb einer Windows\-Dienstanwendung  
  
1.  Erstellen Sie eine Windows\-Dienstanwendung.  Mit den Klassen im <xref:System.ServiceProcess>\-Namespace können Sie Windows\-Dienstanwendungen in verwaltetem Code schreiben.  Diese Anwendung muss eine Klasse einschließen, die von <xref:System.ServiceProcess.ServiceBase> erbt.  
  
2.  Verknüpfen Sie die Lebensdauer des [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Diensts mit der Lebensdauer der Windows\-Dienstanwendung.  In der Regel möchten Sie, dass in einer Windows\-Dienstanwendung gehostete [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienste beim Starten des Hostingdienst aktiviert werden, beim Beenden des Hostingdiensts mit dem Warten auf Nachrichten aufhören und den Hostingprozess beenden, wenn der [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienst einen Fehler erkennt.  Dies kann folgendermaßen erfüllt werden:  
  
    -   Überschreiben Sie [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29>, um eine oder mehrere Instanzen von <xref:System.ServiceModel.ServiceHost> zu öffnen.  Eine einzelne Windows\-Dienstanwendung kann mehrere [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienste hosten, die als Gruppe gestartet und beendet werden.  
  
    -   Überschreiben Sie <xref:System.ServiceProcess.ServiceBase.OnStop%2A> um <xref:System.ServiceModel.Channels.CommunicationObject.Closed> auf dem <xref:System.ServiceModel.ServiceHost> aller ausgeführten [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienste aufzurufen, die während [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> gestartet wurden.  
  
    -   Abonnieren Sie das <xref:System.ServiceModel.Channels.CommunicationObject.Faulted>\-Ereignis von <xref:System.ServiceModel.ServiceHost>, und verwenden Sie die <xref:System.ServiceProcess.ServiceController>\-Klasse, um die Windows\-Dienstanwendung im Fehlerfall zu beenden.  
  
     Windows\-Dienstanwendungen, die [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Dienste hosten, werden auf die gleiche Weise bereitgestellt und verwaltet wie Windows\-Dienstanwendungen, die [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nicht verwenden.  
  
## Siehe auch  
 <xref:System.ServiceProcess>   
 [Exemplarische Vorgehensweise: Erstellen einer Windows\-Dienstanwendung im Komponenten\-Designer](http://go.microsoft.com/fwlink/?LinkId=94875)   
 [Vorgehensweise: Hosten eines WCF\-Diensts in einem verwalteten Windows\-Dienst](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)   
 [Windows\-Diensthost](../../../../docs/framework/wcf/samples/windows-service-host.md)   
 [Programmierarchitektur für Dienstanwendungen](http://go.microsoft.com/fwlink/?LinkId=94876)   
 [Windows Server AppFabric\-Hostingfunktionen](http://go.microsoft.com/fwlink/?LinkId=201276)