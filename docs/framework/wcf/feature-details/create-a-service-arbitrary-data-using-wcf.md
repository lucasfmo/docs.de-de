---
title: "Vorgehensweise: Erstellen eines Diensts, der beliebige Daten mithilfe des WCF REST-Programmiermodells akzeptiert | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e566c15a-b600-4e4a-be3a-4af43e767dae
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Vorgehensweise: Erstellen eines Diensts, der beliebige Daten mithilfe des WCF REST-Programmiermodells akzeptiert
Unter bestimmten Voraussetzungen benötigen Entwickler umfassende Steuerungsmöglichkeiten für die Rückgabe der Daten durch einen Dienstvorgang. Dies ist der Fall, wenn ein Dienstvorgang Daten in einem Format zurückgeben muss, das von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nicht unterstützt wird. In diesem Thema wird die Verwendung des REST-Programmiermodells von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] zum Erstellen eines Diensts erläutert, von dem beliebige Daten empfangen werden.  
  
### <a name="to-implement-the-service-contract"></a>So implementieren Sie den Dienstvertrag  
  
1.  Definieren Sie den Dienstvertrag. Der Vorgang, der die beliebigen Daten empfängt, müssen einen Parameter vom Typ <xref:System.IO.Stream>. Außerdem muss es sich bei diesem Parameter um den einzigen Parameter handeln, der im Text der Anforderung übergeben wird. Der in diesem Beispiel beschriebene Vorgang nimmt auch einen Dateinamenparameter an. Dieser Parameter wird innerhalb der URL der Anforderung übergeben. Sie können angeben, dass ein Parameter in der URL, durch angeben übergeben wird einer <xref:System.UriTemplate> in der <xref:System.ServiceModel.Web.WebInvokeAttribute>. In diesem Fall endet der URI, der zum Aufrufen dieser Methode verwendet wird, auf "UploadFile/Beliebiger_Dateiname". Mit dem "{filename}"-Teil der URI-Vorlage wird angegeben, dass der Dateinameparameter für den Vorgang innerhalb des URI übergeben wird, mit dem der Vorgang aufgerufen wird.  
  
    ```  
     [ServiceContract]  
    public interface IReceiveData  
    {  
        [WebInvoke(UriTemplate = "UploadFile/{fileName}")]  
        void UploadFile(string fileName, Stream fileContents);  
    }  
    ```  
  
2.  Implementieren Sie den Dienstvertrag. Der Vertrag verfügt über nur eine Methode (`UploadFile`), die in einem Stream eine Datei mit beliebigen Daten empfängt. Der Vorgang liest den Stream, erfasst die Menge der gelesenen Bytes und zeigt anschließend den Dateinamen und die Menge der gelesenen Bytes an.  
  
    ```  
    public class RawDataService : IReceiveData  
    {  
        public void UploadFile(string fileName, Stream fileContents)  
        {  
            byte[] buffer = new byte[10000];  
            int bytesRead, totalBytesRead = 0;  
            do  
            {  
                bytesRead = fileContents.Read(buffer, 0, buffer.Length);  
                totalBytesRead += bytesRead;  
            } while (bytesRead > 0);  
            Console.WriteLine("Service: Received file {0} with {1} bytes", fileName, totalBytesRead);  
        }  
    }  
    ```  
  
### <a name="to-host-the-service"></a>So hosten Sie den Dienst  
  
1.  Erstellen Sie eine Konsolenanwendung, um den Dienst zu hosten.  
  
    ```  
    class Program  
    {  
       static void Main(string[] args)  
       {  
       }  
    }  
  
    ```  
  
2.  Erstellen Sie eine Variable, um die Basisadresse für den Dienst innerhalb der `Main`-Methode zu speichern.  
  
    ```  
    string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
    ```  
  
3.  Erstellen einer <xref:System.ServiceModel.ServiceHost> Instanz für den Dienst, der die Dienstklasse und die Basisadresse angibt.  
  
    ```  
    ServiceHost host = new ServiceHost(typeof(RawDataService), new Uri(baseAddress));  
    ```  
  
4.  Fügen Sie einen Endpunkt, der der Vertrag gibt <xref:System.ServiceModel.WebHttpBinding>, und <xref:System.ServiceModel.Description.WebHttpBehavior>.  
  
    ```  
    host.AddServiceEndpoint(typeof(IReceiveData), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
    ```  
  
5.  Öffnen des Diensthosts Der Dienst ist nun zum Empfangen von Anforderungen bereit.  
  
    ```  
    host.Open();  
    Console.WriteLine("Host opened");  
    ```  
  
### <a name="to-call-the-service-programmatically"></a>So rufen Sie den Dienst programmgesteuert auf  
  
1.  Erstellen einer <xref:System.Net.HttpWebRequest> mit dem URI zum Aufrufen des Diensts verwendet. In diesem Code wird die Basisadresse mit `“/UploadFile/Text”` kombiniert. Der `“UploadFile”`-Teil des URI gibt den aufzurufenden Vorgang an. Der `“Test.txt”`-Teil des URI gibt den Dateinamenparameter an, der an den `UploadFile`-Vorgang übergeben werden soll. Diese beiden Elemente zum Zuordnen der <xref:System.UriTemplate> auf den Vorgangsvertrag angewendet.  
  
    ```  
    HttpWebRequest req = (HttpWebRequest)HttpWebRequest.Create(baseAddress + "/UploadFile/Test.txt");  
  
    ```  
  
2.  Festlegen der <xref:System.Net.HttpWebRequest.Method%2A> Eigenschaft der <xref:System.Net.HttpWebRequest> auf `POST` und die <xref:System.Net.HttpWebRequest.ContentType%2A> -Eigenschaft auf `“text/plain”`. Dadurch wird dem Dienst mitgeteilt, dass der Code Daten sendet und diese Daten im Nur-Text-Format vorliegen.  
  
    ```  
    req.Method = "POST";  
    req.ContentType = "text/plain";  
    ```  
  
3.  Rufen Sie <xref:System.Net.HttpWebRequest.GetRequestStream%2A> um den Anforderungsstream abzurufen, erstellen Sie die Daten zum Senden, Schreiben Sie die Daten in den Anforderungsstream, und schließt den Stream.  
  
    ```  
    Stream reqStream = req.GetRequestStream();  
    byte[] fileToSend = new byte[12345];  
    for (int i = 0; i < fileToSend.Length; i++)  
       {  
           fileToSend[i] = (byte)('a' + (i % 26));  
       }  
    reqStream.Write(fileToSend, 0, fileToSend.Length);  
    reqStream.Close();  
    ```  
  
4.  Rufen Sie die Antwort vom Dienst durch Aufrufen von <xref:System.Net.HttpWebRequest.GetResponse%2A> und die Antwortdaten an der Konsole angezeigt.  
  
    ```  
    HttpWebResponse resp = (HttpWebResponse)req.GetResponse();  
    Console.WriteLine("Client: Receive Response HTTP/{0} {1} {2}", resp.ProtocolVersion, (int)resp.StatusCode, resp.StatusDescription);  
  
    ```  
  
5.  Schließen Sie den Diensthost.  
  
    ```  
    host.Close();  
    ```  
  
## <a name="example"></a>Beispiel  
 Im Folgenden finden Sie eine vollständige Liste des Codes für dieses Beispiel:  
  
```  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.ServiceModel;  
using System.ServiceModel.Web;  
using System.ServiceModel.Description;  
using System.IO;  
using System.Net;  
  
namespace ReceiveRawData  
{  
    [ServiceContract]  
    public interface IReceiveData  
    {  
        [WebInvoke(UriTemplate = "UploadFile/{fileName}")]  
        void UploadFile(string fileName, Stream fileContents);  
    }  
    public class RawDataService : IReceiveData  
    {  
        public void UploadFile(string fileName, Stream fileContents)  
        {  
            byte[] buffer = new byte[10000];  
            int bytesRead, totalBytesRead = 0;  
            do  
            {  
                bytesRead = fileContents.Read(buffer, 0, buffer.Length);  
                totalBytesRead += bytesRead;  
            } while (bytesRead > 0);  
            Console.WriteLine("Service: Received file {0} with {1} bytes", fileName, totalBytesRead);  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
            ServiceHost host = new ServiceHost(typeof(RawDataService), new Uri(baseAddress));  
            host.AddServiceEndpoint(typeof(IReceiveData), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            host.Open();  
            Console.WriteLine("Host opened");  
  
            HttpWebRequest req = (HttpWebRequest)HttpWebRequest.Create(baseAddress + "/UploadFile/Test.txt");  
            req.Method = "POST";  
            req.ContentType = "text/plain";  
            Stream reqStream = req.GetRequestStream();  
            byte[] fileToSend = new byte[12345];  
            for (int i = 0; i < fileToSend.Length; i++)  
            {  
                fileToSend[i] = (byte)('a' + (i % 26));  
            }  
            reqStream.Write(fileToSend, 0, fileToSend.Length);  
            reqStream.Close();  
            HttpWebResponse resp = (HttpWebResponse)req.GetResponse();  
            Console.WriteLine("Client: Receive Response HTTP/{0} {1} {2}", resp.ProtocolVersion, (int)resp.StatusCode, resp.StatusDescription);  
            host.Close();  
  
        }  
    }  
}  
  
```  
  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->  
  
## <a name="compiling-the-code"></a>Kompilieren des Codes  
  
-   Verweisen Sie beim Kompilieren des Codes auf "System.ServiceModel.dll" und "System.ServiceModel.Web.dll".  
  
## <a name="see-also"></a>Siehe auch  
 [UriTemplate und UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md)   
 [WCF-Web HTTP-Programmiermodell](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [WCF-Webprogrammiermodell Modell (Übersicht)](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)