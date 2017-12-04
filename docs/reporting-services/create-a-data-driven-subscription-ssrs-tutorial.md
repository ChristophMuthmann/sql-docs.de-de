---
title: Erstellen eines datengesteuerten Abonnements (SSRS-Tutorial) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
caps.latest.revision: "50"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 4af396aaffe116ff7000c2c787c31f775742a485
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>Erstellen eines datengesteuerten Abonnements (SSRS-Lernprogramm)
In diesem [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Tutorial lernen Sie die Konzepte von datengesteuerten Abonnements kennen, indem Sie durch ein einfaches Beispiel geführt werden, mit dem ein datengesteuertes Abonnement erstellt wird, das zum Generieren und Speichern einer gefilterten Berichtsausgabe in eine Dateifreigabe verwendet wird. 
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Mit datengesteuerten Abonnements können Sie die Verteilung eines Berichts auf der Basis dynamischer Abonnementdaten anpassen und automatisieren. Datengesteuerte Abonnements sind für folgende Arten von Szenarios gedacht:  
  
-   Verteilen von Berichten an einen großen Empfängerpool, dessen Mitglieder sich bis zur nächsten Verteilung ändern können. Beispiel: das Versenden einer E-Mail mit einem Monatsberichts an alle aktuellen Kunden.  
  
-   Verteilen von Berichten an eine spezifische Empfängergruppe, die anhand vordefinierter Kriterien ermittelt wird. Beispiel: das Versenden eines Umsatzberichts an alle führenden Verkaufsmanager einer Organisation.
+ Automatisieren Sie die Generierung von Berichten in einer Vielzahl von Formaten, z.B. .xlsx und .pdf.  
  
## <a name="what-you-will-learn"></a>Lernziele  
 Dieses Lernprogramm ist in drei Lektionen aufgeteilt:  
 Lektion | Kommentare
 ------- | --------------
 [Lektion 1: Erstellen einer Beispiel-Abonnentendatenbank](../reporting-services/lesson-1-creating-a-sample-subscriber-database.md) | In dieser Lektion erstellen Sie eine lokale [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Datenbank, die Abonnenteninformationen enthält. Die Bestellnummern, die zum Filtern und Ausgeben von Dateiformaten verwendet wird.
[Lektion 2: Ändern der Eigenschaften der Berichtsdatenquelle](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md) |In dieser Lektion konfigurieren Sie eine Berichtsdatenquelleneigenschaft, sodass der Bericht unbeaufsichtigt ausgeführt werden kann. Für die unbeaufsichtigte Verarbeitung sind gespeicherte Anmeldeinformationen erforderlich. Sie ändern auch das Berichtsdataset, um einen Parameter einzuschließen, der von den Abonnentendaten angegeben wird. Dieser Parameter wird verwendet, um die Berichtsdaten anhand der Bestellnummer zu filtern.
 [Lektion 3: Definieren eines datengesteuerten Abonnements](../reporting-services/lesson-3-defining-a-data-driven-subscription.md) | In dieser Lektion erstellen Sie ein datengesteuertes Abonnement. In dieser Lektion werden Sie durch die einzelnen Seiten im Assistenten für das datengesteuerte Abonnement geführt.

 Im folgenden Diagramm wird der im Tutorial verwendete grundlegende Workflow veranschaulicht.

Schritt  |Description 
---------|---------
(1)     |  Die Abonnementkonfiguration schreibt den Quellbericht, den Zeitplan und die Feldzuordnung in die Datenbank des Abonnenten.        
(2)     | Die OrderInfo-Tabelle enthält 4 Bestellnummern, die für das Filtern verwendet werden, – eine pro Datei. Die Tabelle enthält auch die Dateiformate für die generierten Berichte.
(3)     | Informationen aus der Adventureworks-Datenbank werden gefiltert und im Bericht zurückgegeben. 
(4)     | Die Berichte werden in den Dateiformaten erstellt, die in der OrderInfo-Tabelle angegeben sind.

 
 
   ![ssrs_tutorial_datengesteuert_flow](../reporting-services/media/ssrs-tutorial-datadriven-flow.png) 
  
## <a name="requirements"></a>Anforderungen  
Datengesteuerte Abonnements werden normalerweise von einem Berichtsserveradministrator erstellt und verwaltet. Die Schritte für das Anlegen von datengesteuerten Abonnements erfordern das Erstellen von Abfragen, Kenntnisse darüber, welche Datenquellen Abonnentendaten enthalten, und erhöhte Berechtigungen auf einem Berichtsserver.  
  
Das Tutorial verwendet den Bericht *Sales order* , der im Tutorial [Erstellen eines einfachen Tabellenberichts &#40;SSRS-Tutorial&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) erstellt wurde sowie Daten aus der Beispieldatenbank **AdventureWorks2014**.  
  
Auf Ihrem Computer müssen für die Verwendung dieses Lernprogramms folgende Anwendungen installiert sein:  
  
-   Eine Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , die datengesteuerte Abonnements unterstützt. Weitere Informationen finden Sie unter [Editionen und Komponenten von SQL Server 2016](../sql-server/editions-and-components-of-sql-server-2016.md).  
  
-   Der Berichtsserver muss im einheitlichen Modus ausgeführt werden. Die in diesem Lernprogramm beschriebene Benutzeroberfläche basiert auf einem Berichtsserver im einheitlichen Modus. Abonnements werden auf Berichtsservern im SharePoint-Modus unterstützt, aber die Benutzeroberfläche weicht von der die in diesem Lernprogramm beschriebenen ab.  
  
-   Der SQL Server-Agent-Dienst muss ausgeführt werden.  
  
-   Ein Bericht mit Parametern. Dieses Tutorial geht von dem Beispielbericht `Sales Orders` aus, den Sie mit dem Tutorial [Erstellen eines einfachen Tabellenberichts &#40;SSRS-Tutorial&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  
  
-   Die **AdventureWorks2014** -Beispieldatenbank, die Daten für den Beispielbericht bereitstellt.  
  
-   Eine [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Rollenzuordnung, welche die Aufgabe Alle Abonnements verwalten für den Beispielbericht umfasst. Diese Aufgabe ist für das Definieren eines datengesteuerten Abonnements erforderlich. Wenn Sie als Administrator am Computer angemeldet sind, gewährt die standardmäßige Rollenzuweisung für lokale Administratoren die zum Erstellen datengesteuerter Abonnements erforderlichen Berechtigungen. Weitere Informationen finden Sie unter [Granting Permissions on a Native Mode Report Server](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).  
  
-   Ein freigegebener Ordner, für den Sie Schreibberechtigungen besitzen. Auf den freigegebenen Ordner muss über eine Netzwerkverbindung zugegriffen werden können.  
  
**Ungefähre Dauer dieses Tutorials:** 30 Minuten. Zusätzliche 30 Minuten werden benötigt, wenn Sie das Lernprogramm für grundlegende Berichte nicht abgeschlossen haben.  
  
## <a name="see-also"></a>Siehe auch  
[Data-Driven Subscriptions](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[Erstellen eines einfachen Tabellenberichts &#40;SSRS-Tutorial&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)
 

