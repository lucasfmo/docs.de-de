---
title: "XmlSerializer-Fehler | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c6b80f14-64f4-4162-ae76-71664cf42fd3
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# XmlSerializer-Fehler
Im <xref:System.Xml.Serialization.XmlSerializer>\-Fehlervertragsbeispiel wird veranschaulicht, wie Fehlerinformationen von einem Dienst zu einem Client mit <xref:System.Xml.Serialization.XmlSerializer> übermittelt werden.  Das Beispiel basiert auf [Erste Schritte](../../../../docs/framework/wcf/samples/getting-started-sample.md). Dem Dienst wurde dabei zusätzlicher Code hinzugefügt, um eine interne Ausnahme in einen Fehler zu konvertieren.  Der Client versucht, eine Division durch 0 \(null\) auszuführen, um einen Fehlerzustand beim Dienst zu erzwingen.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
 Der Rechnervertrag wurde geändert, um ein <xref:System.ServiceModel.FaultContractAttribute> einzuschließen, wie im folgenden Beispielcode gezeigt.  Darüber hinaus wird das <xref:System.ServiceModel.XmlSerializerFormatAttribute> verwendet, um die Serialisierung mit <xref:System.Xml.Serialization.XmlSerializer> zu aktivieren.  Die <xref:System.ServiceModel.XmlSerializerFormatAttribute.SupportFaults%2A>\-Eigenschaft wird für dieses Attribut auf `true` festgelegt, wodurch das Serialisierungsprogramm angewiesen wird, <xref:System.Xml.Serialization.XmlSerializer> zum Schreiben und Lesen von Fehlern zu verwenden.  
  
```  
[XmlSerializerFormat(SupportFaults=true)]  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract]  
    int Add(int n1, int n2);  
  
    [OperationContract]  
    int Subtract(int n1, int n2);  
  
    [OperationContract]  
    int Multiply(int n1, int n2);  
  
    [OperationContract]  
    [FaultContract(typeof(MathFault))]  
    int Divide(int n1, int n2);  
}  
```  
  
 Beim Generieren von Code für den Clientproxy müssen Sie das **\/UseSerializerForFaults**\-Flag auf [ServiceModel Metadata Utility\-Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) anwenden.  
  
### So können Sie das Beispiel einrichten, erstellen und ausführen  
  
1.  Stellen Sie sicher, dass Sie die [Einmaliges Setupverfahren für Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) ausgeführt haben.  
  
2.  Zum Erstellen der C\#\- oder Visual Basic .NET\-Edition der Projektmappe befolgen Sie die unter [Erstellen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md) aufgeführten Anweisungen.  
  
3.  Um das Beispiel in einer Konfiguration mit einem Computer oder computerübergreifend auszuführen, befolgen Sie die Anweisungen unter [Durchführen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.  Suchen Sie nach dem folgenden Verzeichnis \(Standardverzeichnis\), bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.  Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples\WCF\Basic\Contract\Service\XmlSerializerFaults`  
  
## Siehe auch  
 <xref:System.ServiceModel.XmlSerializerFormatAttribute>   
 <xref:System.ServiceModel.XmlSerializerFormatAttribute.SupportFaults%2A>