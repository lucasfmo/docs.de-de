---
title: "Sichern von ADO.NET-Anwendungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 005a1d43-6ee5-471e-ad98-1d30a44d49d5
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Sichern von ADO.NET-Anwendungen
Beim Schreiben von sicheren ADO.NET\-Anwendungen gilt es nicht nur, häufige Fallstricke bei der Codierung zu umgehen, wie die Nichtvalidierung von Benutzereingaben.  Eine Anwendung, die auf Daten zugreift, verfügt über viele mögliche Schwachstellen, über die ein Hacker vertrauliche Daten abrufen, manipulieren oder vernichten kann.  Es ist daher unerlässlich, alle Sicherheitsaspekte zu verstehen, und zwar beginnend bei der Erstellung von Gefahrenmodellen während des Anwendungsentwurfs bis hin zur eigentlichen Bereitstellung der Anwendung und ihrem laufenden Betrieb.  
  
 .NET Framework bietet eine Reihe nützlicher Klassen, Dienste und Tools zum Sichern und Verwalten von Datenbankanwendungen.  Die Common Language Runtime \(CLR\) bietet eine typsichere Umgebung für die Ausführung von Code mit Codezugriffssicherheit \(Code Access Security, CAS\), um die Berechtigungen für verwalteten Code weiter einzuschränken.  Die Beachtung von Codierungspraktiken für einen sicheren Datenzugriff hilft, den Schaden zu begrenzen, den ein potenzieller Angreifer verursachen kann.  
  
 Das Schreiben von sicherem Code schützt jedoch nicht vor selbst zu verantwortenden Sicherheitslücken beim Arbeiten mit nicht verwalteten Ressourcen, wie Datenbanken.  Die meisten Serverdatenbanken, wie SQL Server, verfügen über eigene Sicherheitssysteme, die bei korrekter Implementierung für mehr Sicherheit sorgen.  Aber auch Datenquellen mit einem robusten Sicherheitssystem können zum Angriffsopfer werden, wenn sie nicht ordnungsgemäß konfiguriert werden.  
  
## In diesem Abschnitt  
 [Übersicht über die Sicherheit](../../../../docs/framework/data/adonet/security-overview.md)  
 Enthält Empfehlungen für das Entwerfen sicherer ADO.NET\-Anwendungen.  
  
 [Sicherer Datenzugriff](../../../../docs/framework/data/adonet/secure-data-access.md)  
 Beschreibt das Arbeiten mit Daten aus einer gesicherten Datenquelle.  
  
 [Sichere Clientanwendungen](../../../../docs/framework/data/adonet/secure-client-applications.md)  
 Enthält Überlegungen zum Thema Sicherheit für Clientanwendungen.  
  
 [Codezugriffssicherheit und ADO.NET](../../../../docs/framework/data/adonet/code-access-security.md)  
 Beschreibt, wie CAS zum Schutz von ADO.NET\-Code beitragen kann.  Erläutert außerdem das Arbeiten mit teilweiser Vertrauenswürdigkeit.  
  
 [Datenschutz und Datensicherheit](../../../../docs/framework/data/adonet/privacy-and-data-security.md)  
 Beschreibt Verschlüsselungsmöglichkeiten für ADO.NET\-Anwendungen.  
  
## Verwandte Abschnitte  
 [SQL Server\-Sicherheit](../../../../docs/framework/data/adonet/sql/sql-server-security.md)  
 Beschreibt SQL Server\-Sicherheitsfunktionen aus Entwicklersicht.  
  
 [Sicherheitsüberlegungen](../../../../docs/framework/data/adonet/ef/security-considerations.md)  
 Beschreibt Sicherheitsfunktionen für Entity Framework\-Anwendungen.  
  
 [Security](../../../../docs/standard/security/index.md)  
 Enthält Links zu Themen, in denen alle Aspekte der Sicherheit in .NET Framework beschrieben werden.  
  
 [Security Tools](http://msdn.microsoft.com/de-de/2a3eb98a-2de6-4fba-b41c-01a74d354c11)  
 .NET Framework\-Tools zum Sichern und Verwalten von Sicherheitsrichtlinien.  
  
 [Resources for Creating Secure Applications](http://msdn.microsoft.com/de-de/0ebf5f69-76f2-498a-a2df-83cf3443e132)  
 Enthält Links zu Themen zum Erstellen sicherer Anwendungen.  
  
 [Sicherheitsbibliographie](../Topic/Security%20Bibliography.md)  
 Enthält Links zu externen Ressourcen, die online und in Druckversion verfügbar sind.  
  
## Siehe auch  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)   
 [ADO.NET Verwaltete Anbieter und DataSet\-Entwicklercenter](http://go.microsoft.com/fwlink/?LinkId=217917)