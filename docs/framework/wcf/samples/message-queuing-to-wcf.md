---
title: "Message Queuing zu Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6d718eb0-9f61-4653-8a75-d2dac8fb3520
caps.latest.revision: 34
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 34
---
# Message Queuing zu Windows Communication Foundation
In diesem Beispiel wird veranschaulicht, wie eine Message Queuing \(MSMQ\)\-Anwendung eine MSMQ\-Nachricht an einen [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\-Dienst senden kann.Der Dienst ist eine selbst gehostete Konsolenanwendung, die es Ihnen ermöglicht, den Dienst beim Empfang von Nachrichten in der Warteschlange zu beobachten.  
  
 Der Dienstvertrag ist `IOrderProcessor` und definiert einen unidirektionalen Dienst, der für die Verwendung mit Warteschlangen geeignet ist.Eine MSMQ\-Nachricht verfügt über keinen Aktionsheader, d h. es ist nicht möglich, verschiedene MSMQ\-Nachrichten Vorgangsverträgen automatisch zuzuordnen.Deshalb kann es nur einen Vorgangsvertrag geben.Wenn Sie mehr als einen Vorgangsvertrag für den Dienst definieren möchten, muss die Anwendung Informationen darüber bereitstellen, welcher Header in der MSMQ\-Nachricht \(z. B. die Bezeichnung oder CorrelationID\) für die Entscheidung, welcher Vorgangsvertrag erteilt werden soll, verwendet werden kann.Dies wird im [Benutzerdefinierter Demux](../../../../docs/framework/wcf/samples/custom-demux.md) veranschaulicht.  
  
 Die MSMQ\-Nachricht enthält keine Informationen darüber, welche Header den verschiedenen Parametern des Vorgangsvertrags zugeordnet sind.Der Parameter ist vom Typ <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>\(`MsmqMessage<T>`\), der die zugrunde liegende MSMQ\-Nachricht enthält.Der Typ "T" in der Klasse <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>\(`MsmqMessage<T>`\) steht für die Daten, die zum MSMQ\-Nachrichtentext serialisiert werden.In diesem Beispiel wird der `PurchaseOrder`\-Typ zum MSMQ\-Nachrichtentext serialisiert.  
  
 Im folgenden Beispielcode wird der Dienstvertrag des Diensts für die Auftragsverarbeitung gezeigt.  
  
```  
// Define a service contract.  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
[ServiceKnownType(typeof(PurchaseOrder))]  
public interface IOrderProcessor  
{  
    [OperationContract(IsOneWay = true, Action = "*")]  
    void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg);  
}  
  
```  
  
 Der Dienst ist selbst gehostet.Bei Verwendung von MSMQ muss die Warteschlange im Voraus erstellt werden.Dies kann manuell erfolgen oder mithilfe eines Codes.In diesem Beispiel prüft der Dienst, ob die Warteschlange vorhanden ist, und erstellt sie gegebenenfalls.Der Warteschlangenname wird aus der Konfigurationsdatei gelesen.  
  
```  
public static void Main()  
{  
    // Get the MSMQ queue name from the application settings in   
    // configuration.  
    string queueName = ConfigurationManager.AppSettings["queueName"];  
    // Create the MSMQ queue if necessary.  
    if (!MessageQueue.Exists(queueName))  
        MessageQueue.Create(queueName, true);  
    …  
}  
  
```  
  
 Der Dienst erstellt und öffnet einen <xref:System.ServiceModel.ServiceHost> für den `OrderProcessorService`, wie im folgenden Beispielcode gezeigt.  
  
```  
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))  
{  
    serviceHost.Open();  
    Console.WriteLine("The service is ready.");  
    Console.WriteLine("Press <ENTER> to terminate service.");  
    Console.ReadLine();  
    serviceHost.Close();  
}  
  
```  
  
 Der Name der MSMQ\-Warteschlange wird im appSettings\-Abschnitt der Konfigurationsdatei angegeben, wie in der folgenden Beispielkonfiguration gezeigt.  
  
> [!NOTE]
>  Im Warteschlangennamen wird ein Punkt \(.\) für den lokalen Computer verwendet, und in der Pfadangabe werden umgekehrte Schrägstriche als Trennzeichen verwendet.Die [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Endpunktadresse gibt ein msmq.formatname\-Schema an, und für den lokalen Computer wird localhost verwendet.Die Adresse der Warteschlange für jeden MSMQ\-Formatnamen, der sich auf Richtlinien bezieht, folgt dem msmq.formatname\-Schema.  
  
```  
<appSettings>  
    <add key="orderQueueName" value=".\private$\Orders" />  
</appSettings>  
  
```  
  
 Die Clientanwendung ist eine MSMQ\-Anwendung, die sich der <xref:System.Messaging.MessageQueue.Send%2A>\-Methode bedient, um eine permanente Transaktionsnachricht an die Warteschlange zu senden, wie im folgenden Beispielcode gezeigt.  
  
```  
//Connect to the queue.  
MessageQueue orderQueue = new MessageQueue(ConfigurationManager.AppSettings["orderQueueName"]);  
  
// Create the purchase order.  
PurchaseOrder po = new PurchaseOrder();  
po.CustomerId = "somecustomer.com";  
po.PONumber = Guid.NewGuid().ToString();  
  
PurchaseOrderLineItem lineItem1 = new PurchaseOrderLineItem();  
lineItem1.ProductId = "Blue Widget";  
lineItem1.Quantity = 54;  
lineItem1.UnitCost = 29.99F;  
  
PurchaseOrderLineItem lineItem2 = new PurchaseOrderLineItem();  
lineItem2.ProductId = "Red Widget";  
lineItem2.Quantity = 890;  
lineItem2.UnitCost = 45.89F;  
  
po.orderLineItems = new PurchaseOrderLineItem[2];  
po.orderLineItems[0] = lineItem1;  
po.orderLineItems[1] = lineItem2;  
  
// Submit the purchase order.  
Message msg = new Message();  
msg.Body = po;  
//Create a transaction scope.  
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))  
{  
  
    orderQueue.Send(msg, MessageQueueTransactionType.Automatic);  
    // Complete the transaction.  
    scope.Complete();  
  
}  
Console.WriteLine("Placed the order:{0}", po);  
Console.WriteLine("Press <ENTER> to terminate client.");  
Console.ReadLine();  
  
```  
  
 Wenn Sie das Beispiel ausführen, werden die Client\- und Dienstaktivitäten sowohl im Dienst\- als auch Clientkonsolenfenster angezeigt.Sie können sehen, wie der Dienst Nachrichten vom Client empfängt.Drücken Sie die EINGABETASTE in den einzelnen Konsolenfenstern, um den Dienst und den Client zu schließen.Beachten Sie, dass aufgrund der Verwendung einer Warteschlange der Client und der Dienst nicht gleichzeitig ausgeführt werden müssen.Sie können beispielsweise den Client ausführen, ihn schließen und anschließend den Dienst starten, der dann trotzdem noch die Nachrichten des Clients empfängt.  
  
### So richten Sie das Beispiel ein, erstellen es und führen es aus  
  
1.  Stellen Sie sicher, dass Sie die [Einmaliges Setupverfahren für Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) ausgeführt haben.  
  
2.  Wenn der Dienst zuerst ausgeführt wird, wird überprüft, ob die Warteschlange vorhanden ist.Ist die Warteschlange nicht vorhanden, wird sie vom Dienst erstellt.Sie können zuerst den Dienst ausführen, um die Warteschlange zu erstellen, oder Sie können sie über den MSMQ\-Warteschlangen\-Manager erstellen.Führen Sie zum Erstellen einer Warteschlange in Windows 2008 die folgenden Schritte aus:  
  
    1.  Öffnen Sie Server\-Manager in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
    2.  Erweitern Sie die Registerkarte **Funktionen**.  
  
    3.  Klicken Sie mit der rechten Maustaste auf **Private Meldungswarteschlangen**, und klicken Sie anschließend auf **Neu** und **Private Warteschlange**.  
  
    4.  Aktivieren Sie das Kontrollkästchen **Transaktional**.  
  
    5.  Geben Sie `ServiceModelSamplesTransacted` als Namen der neuen Warteschlange ein.  
  
3.  Folgen Sie zum Erstellen der C\#\- bzw. Visual Basic .NET\-Version der Projektmappe den Anweisungen unter [Erstellen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Um das Beispiel in einer Konfiguration mit einem einzigen Computer auszuführen, befolgen Sie die Anweisungen unter [Durchführen der Windows Communication Foundation\-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
### So führen Sie das Beispiel computerübergreifend aus  
  
1.  Kopieren Sie die Dienstprogrammdateien aus dem Ordner \\service\\bin\\ \(unterhalb des sprachspezifischen Ordners\) auf den Dienstcomputer.  
  
2.  Kopieren Sie die Clientprogrammdateien aus dem Ordner \\client\\bin\\ \(unterhalb des sprachspezifischen Ordners\) auf den Clientcomputer.  
  
3.  Ändern Sie in der Datei Client.exe.config den Wert von orderQueueName, und geben Sie anstelle von "." den Namen des Dienstcomputers an.  
  
4.  Starten Sie auf dem Dienstcomputer Service.exe an einer Eingabeaufforderung.  
  
5.  Starten Sie auf dem Clientcomputer Client.exe an einer Eingabeaufforderung.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Suchen Sie nach dem folgenden Verzeichnis \(Standardverzeichnis\), bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\MsmqToWcf`  
  
## Siehe auch  
 [Warteschlangen in WCF](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [Vorgehensweise: Nachrichtenaustausch mit WCF\-Endpunkten und Message Queuing\-Anwendungen](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)   
 [Message Queuing](http://go.microsoft.com/fwlink/?LinkId=94968)