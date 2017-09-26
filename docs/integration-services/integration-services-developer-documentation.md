---
title: "Integration Services-Dokumentation für Entwickler | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services, programming
- SSIS, programming
- SQL Server Integration Services, programming
- packages [Integration Services], programming
ms.assetid: 60fe148b-a7c4-4289-ae3e-2e949fc1886c
caps.latest.revision: 76
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cf7d7afba8ada3f6027db3053914b1822597792c
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-developer-documentation"></a>Integration Services-Entwicklerdokumentation
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] umfasst ein völlig neu konzipiertes Objektmodell mit vielen verbesserten Funktionen, um das Erweitern und Programmieren von Paketen einfacher, flexibler und leistungsstärker zu gestalten. Entwickler haben die Möglichkeit, fast jeden Aspekt von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Paketen zu erweitern und zu programmieren.  
  
 Als [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Entwickler gibt es zwei grundlegende Ansätze, die Sie bei der [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Programmierung verfolgen können:  
  
-   Sie können Pakete erweitern, indem Sie Komponenten, die in [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer zur Verfügung gestellt werden, zur Bereitstellung von benutzerdefinierten Funktionen in einem Paket programmieren.  
  
-   Sie können Pakete erstellen, konfigurieren und programmgesteuert aus Ihren eigenen Anwendungen ausführen.  
  
 Wenn sich die integrierten Komponenten in ggf. Folgendes herausstellen [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nicht Ihren Anforderungen entsprechen, Sie können die Effektivität von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] durch codieren eigener Erweiterungen erhöhen. Dieser Ansatz bietet Ihnen zwei unterschiedliche Optionen:  
  
-   Zur sofortigen Verwendung in einem einzelnen Paket können Sie einen benutzerdefinierten Task erstellen, indem Sie Code in den Skripttask schreiben. Sie haben auch die Möglichkeit, eine benutzerdefinierte Datenflusskomponente, die Sie als Quelle, Transformation oder Ziel konfigurieren können, zu erstellen, indem Sie Code in die Skriptkomponente schreiben. Diese leistungsstarken Wrapper schreiben den Infrastrukturcode für Sie, damit Sie sich vollständig auf die Entwicklung der benutzerdefinierten Funktionen konzentrieren können. Sie lassen sich jedoch nicht leicht an anderer Stelle wiederverwenden.  
  
-   Zur Verwendung in mehreren Paketen können Sie benutzerdefinierte [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Erweiterungen wie Verbindungs-Manager, Tasks, Enumeratoren, Protokollanbieter und Datenflusskomponenten erstellen. Das verwaltete [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Objektmodell umfasst Basisklassen, die als Startpunkt dienen und die Entwicklung benutzerdefinierter Erweiterungen bequemer als je zuvor gestalten.  
  
 Wenn Sie Pakete dynamisch erstellen oder [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Pakete außerhalb der Entwicklungsumgebung verwalten und ausführen möchten, können Sie Pakete programmgesteuert ändern. Sie können bestehende Pakete laden, ändern und ausführen oder völlig neue Pakete programmgesteuert erstellen und ausführen. Dieser Ansatz bietet Ihnen eine breite Palette von Optionen:  
  
-   Laden und Ausführen eines vorhandenen Pakets ohne Änderung  
  
-   Laden, Neukonfigurieren (z. B. Festlegen einer anderen Datenquelle) und Ausführen eines vorhandenen Pakets  
  
-   Erstellen eines neuen Pakets, Hinzufügen und Konfigurieren von Komponenten, Vornehmen von Änderungen Objekt um Objekt und Eigenschaft um Eigenschaft, Speichern und Ausführen des Pakets  
  
 Diese Ansätze zur [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Programmierung werden in diesem Abschnitt beschrieben und mit Beispielen veranschaulicht.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Übersicht über die Programmierung von 'Integration Services'](../integration-services/integration-services-programming-overview.md)  
 Beschreibt die Rollen von Ablaufsteuerung und Datenfluss bei der [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Entwicklung.  
  
 [Grundlegendes zu synchronen und asynchronen Transformationen](../integration-services/understanding-synchronous-and-asynchronous-transformations.md)  
 Beschreibt die wichtige Unterscheidung zwischen synchronen und asynchronen Ausgaben sowie die Komponenten, von denen sie im Datenfluss verwendet werden.  
  
 [Programmgesteuertes Arbeiten mit Verbindungs-Managern](../integration-services/working-with-connection-managers-programmatically.md)  
 Listet die Verbindungs-Manager die Verwendung von verwaltetem Code und die Werte, die die Verbindungs-Manager zurückgeben, wenn der Code Ruft die **AcquireConnection** Methode.  
  
 [Erweitern von Paketen mit Skripts](../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 Erläutert, wie die Ablaufsteuerung mithilfe des Skripttasks und der Datenfluss mithilfe der Skriptkomponente erweitert werden können.  
  
 [Erweitern von Paketen mit benutzerdefinierten Objekten](../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Beschreibt, wie benutzerdefinierte Tasks, Datenflusskomponenten und andere Paketobjekte für die Verwendung in mehreren Paketen erstellt und programmiert werden.  
  
 [Programmgesteuertes Erstellen von Paketen](../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 Erläutert, wie [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Pakete programmgesteuert erstellt, konfiguriert und gespeichert werden.  
  
 [Programmgesteuerte Ausführung und Verwaltung von Paketen](../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 Beschreibt, wie [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Pakete programmgesteuert aufgezählt, ausgeführt und verwaltet werden.  
  
## <a name="reference"></a>Verweis  
 [Fehler- und Meldungsreferenz von Integration Services](../integration-services/integration-services-error-and-message-reference.md)  
 Listet die vordefinierten [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Fehlercodes sowie ihre symbolischen Namen und Beschreibungen auf.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
 [Tools zur Problembehandlung für die Paketentwicklung](../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
 Beschreibt die Funktionen und Tools, die von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] zur Behandlung von Problemen mit Paketen während der Entwicklung bereitgestellt werden.  
  
## <a name="external-resources"></a>Externe Ressourcen  
  
-   CodePlex-Beispiele, [Integration Services Product Samples](http://go.microsoft.com/fwlink/?LinkID=131204), auf www.codeplex.com/MSFTISProdSamples  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
  
  
