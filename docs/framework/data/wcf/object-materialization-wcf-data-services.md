---
title: "Objektmaterialisierung (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, Clientbibliothek"
  - "WCF Data Services, Abfragen"
ms.assetid: f0dbf7b0-0292-4e31-9ae4-b98288336dc1
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Objektmaterialisierung (WCF Data Services)
Wenn Sie das Dialogfeld **Dienstverweis hinzufügen** verwenden, um einen [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]\-Feed in einer .NET Framework\-basierten Clientanwendung zu nutzen, werden für jeden Entitätstyp in dem vom Feed verfügbar gemachten Datenmodell entsprechende Datenklassen generiert.  Weitere Informationen finden Sie unter [Generieren der Datendienst\-Clientbibliothek](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md).  Entitätsdaten, die von einer Abfrage zurückgegeben werden, werden in eine Instanz einer dieser generierten Client\-Datendienstklassen materialisiert.  Weitere Informationen zu Zusammenführungsoptionen und zur Identitätsauflösung für nachverfolgte Objekte finden Sie unter [Verwalten des Datendienstkontextes](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md).  
  
 Mit [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] können Sie auch eigene Client\-Datendienstklassen definieren, anstatt die von Tools generierten Datenklassen zu verwenden.  Dies ermöglicht es Ihnen, eigene Datenklassen zu verwenden, die auch als POCO \(plain\-old CLR object\)\-Datenklassen bezeichnet werden.  Wenn Sie diese Arten von benutzerdefinierten Datenklassen verwenden, sollten Sie die Datenklasse mit <xref:System.Data.Services.Common.DataServiceKeyAttribute> oder <xref:System.Data.Services.Common.DataServiceEntityAttribute> auszeichnen und sicherstellen, dass Typnamen auf dem Client mit Typnamen im Datenmodell des Datendiensts übereinstimmen.  
  
 Nachdem die Bibliothek die Abfrageantwortnachricht empfangen hat, materialisiert sie die zurückgegebenen Daten aus dem [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]\-Feed in Instanzen von Client\-Datendienstklassen, die dem Typ der Abfrage entsprechen.  Zur Materialisierung dieser Objekte werden die folgenden allgemeinen Schritte ausgeführt:  
  
1.  Die Clientbibliothek liest den serialisierten Typ aus dem `entry`\-Element im Antwortnachrichtenfeed und versucht, mit einer der folgenden Methoden eine neue Instanz des richtigen Typs zu erstellen:  
  
    -   Wenn der im Feed deklarierte Typ den gleichen Namen wie den Typ der <xref:System.Data.Services.Client.DataServiceQuery%601>\-Abfrage hat, wird mit dem leeren Konstruktor eine neue Instanz dieses Typs erstellt.  
  
    -   Wenn der im Feed deklarierte Typ den gleichen Namen wie ein Typ hat, der vom Typ vom <xref:System.Data.Services.Client.DataServiceQuery%601> abgeleitet ist, wird mit dem leeren Konstruktor eine neue Instanz dieses abgeleiteten Typs erstellt.  
  
    -   Wenn der im Feed deklarierte Typ nicht dem Typ der <xref:System.Data.Services.Client.DataServiceQuery%601>\-Abfrage oder einem abgeleiteten Typen entspricht, wird mit dem leeren Konstruktor eine neue Instanz des abgefragten Typs erstellt.  
  
    -   Wenn die <xref:System.Data.Services.Client.DataServiceContext.ResolveType%2A>\-Eigenschaft festgelegt wird, wird der angegebene Delegat aufgerufen, um die namensbasierte Standardtypzuordnung zu überschreiben, und stattdessen wird eine neue Instanz des Typs erstellt, die von <xref:System.Func%602> zurückgegeben wurde.  Wenn dieser Delegat einen NULL\-Wert zurückgibt, wird stattdessen eine neue Instanz des abgefragten Typs erstellt.  Es ist möglicherweise erforderlich, die namensbasierte Standardtypnamenzuordnung zu überschreiben, um Vererbungsszenarien zu unterstützen.  
  
2.  Die Clientbibliothek liest den URI\-Wert aus dem `id`\-Element des `entry`Elements, das der Identitätswert der Entität darstellt.  Sofern nicht der <xref:System.Data.Services.Client.DataServiceContext.MergeOption%2A>\-Wert <xref:System.Data.Services.Client.MergeOption> verwendet wird, wird der Identitätswert verwendet, um das Objekt im <xref:System.Data.Services.Client.DataServiceContext>\-Kontext zu verfolgen.  Der Identitätswert wird auch verwendet, um zu garantieren, dass selbst dann nur eine einzelne Entitätsinstanz erstellt wird, wenn eine Entität mehrmals in der Abfrageantwort zurückgegeben wird.  
  
3.  Die Clientbibliothek liest Eigenschaften vom Feedeintrag und legt die entsprechenden Eigenschaften auf dem neu erstellten Objekt fest.  Wenn ein Objekt über den gleichen Identitätswert verfügt wie ein bereits im <xref:System.Data.Services.Client.DataServiceContext>\-Kontext vorhandenes Objekt, dann werden die Eigenschaften  auf der Grundlage der <xref:System.Data.Services.Client.MergeOption>\-Einstellung des <xref:System.Data.Services.Client.DataServiceContext>\-Kontexts festgelegt.  Die Antwort kann Eigenschaftswerte enthalten, für die keine entsprechende Eigenschaft im Clienttyp vorhanden ist.  Wenn dieser Fall eintritt, hängt die Aktion vom Wert der <xref:System.Data.Services.Client.DataServiceContext.IgnoreMissingProperties%2A>\-Eigenschaft des <xref:System.Data.Services.Client.DataServiceContext>\-Kontexts ab.  Wenn diese Eigenschaft auf `true` festgelegt wurde, wird die fehlende Eigenschaft ignoriert.  Andernfalls wird ein Fehler ausgelöst.  Eigenschaften werden wie folgt festgelegt:  
  
    -   Skalare Eigenschaften werden auf den entsprechenden Wert im Eintrag in der Antwortnachricht festgelegt.  
  
    -   Komplexe Eigenschaften werden auf eine neue komplexe Typinstanz festgelegt, die mit den Eigenschaften des komplexen Typs von der Antwort festgelegt wird.  
  
    -   Navigationseigenschaften, die eine Sammlung von verknüpften Entitäten zurückgeben, werden auf eine neue oder vorhandene Instanz von <xref:System.Collections.Generic.ICollection%601> festgelegt, wobei `T` der Typ der verknüpften Entität ist.  Diese Sammlung ist leer, sofern die verknüpften Objekte nicht in den <xref:System.Data.Services.Client.DataServiceContext>\-Kontext geladen wurden.  Weitere Informationen finden Sie unter [Laden von verzögertem Inhalt](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md).  
  
        > [!NOTE]
        >  Wenn die generierten Clientdatenklassen die Datenbindung unterstützen, geben Navigationseigenschaften stattdessen Instanzen der <xref:System.Data.Services.Client.DataServiceCollection%601>\-Klasse zurück.  Weitere Informationen finden Sie unter [Binden von Daten an Steuerelemente](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md).  
  
4.  Das <xref:System.Data.Services.Client.DataServiceContext.ReadingEntity>\-Ereignis wird ausgelöst.  
  
5.  Die Clientbibliothek fügt das Objekt an den <xref:System.Data.Services.Client.DataServiceContext>\-Kontext an.  Das Objekt wird nicht angefügt, wenn <xref:System.Data.Services.Client.MergeOption> auf <xref:System.Data.Services.Client.MergeOption> festgelegt wurde.  
  
## Siehe auch  
 [Abfragen des Datendiensts](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)   
 [Abfrageprojektionen](../../../../docs/framework/data/wcf/query-projections-wcf-data-services.md)