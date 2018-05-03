---
title: 'SSIS: Erstellen eines einfachen ETL-Pakets | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 04/17/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 83e51e583e0c83d8d0cbc8dbd213a78baa766ffb
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="ssis-how-to-create-an-etl-package"></a>SSIS-Tutorials: Erstellen eines einfachen ETL-Pakets

 > Inhalte im Zusammenhang mit früheren Versionen von SQL Server finden Sie unter [SSIS-Lernprogramm: Erstellen eines einfachen ETL-Pakets](https://msdn.microsoft.com/library/ms169917(SQL.120).aspx).

In diesem Tutorial lernen Sie, wie der [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer zum Erstellen eines einfachen [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Pakets verwendet wird. Das von Ihnen erstellte Paket übernimmt Daten aus einer Flatfile, formatiert die Daten und fügt die neu formatierten Daten in eine Faktentabelle ein. In den folgenden Lektionen wird das Paket erweitert, um Schleifen, Paketkonfigurationen, Protokollierung und Fehlerfluss zu veranschaulichen.  
  
Beim Installieren der im Tutorial verwendeten Beispieldaten werden auch die abgeschlossenen Versionen der Pakete, die Sie in der jeweiligen Lektion des Tutorials erstellen werden, installiert. Mithilfe der abgeschlossenen Pakete können Sie Lektionen überspringen und nach Belieben mit einer späteren Lektion in das Lernprogramm einsteigen. Wenn dieses Tutorial Ihre erste Erfahrung mit Paketen oder mit der neuen Entwicklungsumgebung ist, empfehlen wir Ihnen, mit Lektion 1 zu beginnen.  

> [!IMPORTANT]
> Vor Kurzem waren die Beispieldateien, die für das Ausführen dieses Tutorials erforderlich sind, online nicht mehr an ihrem bisherigen Speicherort verfügbar. Wir entschuldigen uns für die Unannehmlichkeiten. Diese Dateien wurden am neuen Speicherort zur Verfügung gestellt, und die Links in diesem Artikel wurden aktualisiert.

## <a name="what-is-sql-server-integration-services-ssis"></a>Was ist SQL Server Integration Services (SSIS)?

[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) ist eine Plattform zum Erstellen von leistungsstarken Datenintegrationslösungen, z.B. ETL-Paketen (Extrahieren, Transformieren und Laden) für das Data Warehousing. SSIS enthält grafische Tools und Assistenten zum Erstellen und Debuggen von Paketen; Tasks zum Ausführen von Workflowfunktionen wie z. B. FTP-Vorgänge, Ausführen von SQL-Anweisungen und Senden von E-Mails; Datenquellen und Ziele zum Extrahieren und Laden von Daten; Transformationen zum Bereinigen, Aggregieren, Zusammenführen und Kopieren von Daten; einen Verwaltungsdienst, den [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Dienst zum Verwalten der Paketausführung und -speicherung; und Anwendungsprogrammierschnittstellen (APIs, Application Programming Interfaces) zum Programmieren des [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Objektmodells.  

## <a name="what-you-learn"></a>Ihre Lernziele  
Die beste Möglichkeit, den Umgang mit den neuen Tools, Steuerelementen und Funktionen von [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] zu üben, besteht in ihrer Verwendung. Dieses Tutorial leitet Sie Schritt für Schritt durch den [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer, um ein einfaches ETL-Paket einschließlich Schleifen, Konfigurationen, Fehlerflusslogik und Protokollierung zu erstellen.  
  
## <a name="requirements"></a>Anforderungen  
Dieses Tutorial wendet sich an Benutzer, die mit grundlegenden Datenbankvorgängen vertraut sind, aber nur über begrenzte Kenntnisse in Bezug auf die neuen Funktionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]verfügen.  
  
Ihr System muss die folgenden installierten Komponenten aufweisen, damit dieses Lernprogramm verwendet werden kann:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mit der **AdventureWorksDW2012** -Datenbank. Laden Sie `AdventureWorksDW2012.bak` von der [AdventureWorks-Beispieldatenbank](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) herunter, und stellen Sie die Sicherung wieder her, um die Datenbank **AdventureWorksDW2012** herunterzuladen.  

-   Beispieldaten. Die Beispieldaten sind in den [!INCLUDE[ssIS](../includes/ssis-md.md)] -Lektionspaketen enthalten. [Klicken Sie hier](http://download.microsoft.com/download/3/1/4/314A4169-D540-4E9E-9776-585BFBFC2CC5/Creating a Simple ETL Package.zip), um die Beispieldaten und die Lektionspakete als ZIP-Datei herunterzuladen.  

## <a name="lessons-in-this-tutorial"></a>Lektionen in diesem Lernprogramm  
[Lesson 1: Create a Project and Basic Package with SSIS](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)  
In dieser Lektion erstellen Sie ein einfaches ETL-Paket, das Daten aus einer einzelnen Flatfile extrahiert, die Daten mithilfe von Transformationen zum Suchen transformiert und die Ergebnisse schließlich in ein Faktentabellenziel lädt.  
  
[Lesson 2: Adding Looping with SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
In dieser Lektion erweitern Sie das Paket, das Sie in Lektion 1 erstellt haben, um die Vorteile der neuen Schleifenfunktionen zum Extrahieren von mehreren Flatfiles in einen einzigen Datenflussprozess zu nutzen.  
  
[Lektion 3: Hinzufügen der Protokollierung mit SSIS](../integration-services/lesson-3-add-logging-with-ssis.md)  
In dieser Lektion erweitern Sie das von Ihnen in Lektion 2 erstellte Paket, um die Vorteile der neuen Protokollierungsfunktionen zu nutzen.  
  
[Lektion 4: Hinzufügen der Fehlerflussumleitung mit SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
In dieser Lektion erweitern Sie das von Ihnen in Lektion 3 erstellte Paket, um die Vorteile der neuen Fehlerausgabekonfigurationen zu nutzen.  
  
[Lesson 5: Add SSIS Package Configurations for the Package Deployment Model](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
In dieser Lektion erweitern Sie das von Ihnen in Lektion 4 erstellte Paket, um die Vorteile der neuen Paketkonfigurationsoptionen zu nutzen.  
  
[Lesson 6: Using Parameters with the Project Deployment Model in SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
In dieser Lektion erweitern Sie das Paket, das Sie in Lektion 5 erstellt haben, um von der Verwendung der neuen Parameter für das Projektbereitstellungsmodell zu profitieren.  
  
  
  
