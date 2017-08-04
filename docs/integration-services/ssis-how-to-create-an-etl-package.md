---
title: 'SSIS Gewusst wie: Erstellen eines ETL-Pakets | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: d4dc2ff665ff191fb75dd99103a222542262d4c4
ms.openlocfilehash: 2005755d073f7bb4950268e0fba827860491d1c4
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="ssis-how-to-create-an-etl-package"></a>SSIS-Tutorials: Erstellen eines einfachen ETL-Pakets

 > Inhalt im Zusammenhang mit früheren Versionen von SQL Server, finden Sie unter [SSIS-Lernprogramm: Erstellen eines einfachen ETL-Pakets](https://msdn.microsoft.com/en-US/library/ms169917(SQL.120).aspx).

[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) ist eine Plattform zum Erstellen leistungsfähiger Datenintegrationslösungen, z.B. von ETL-Paketen (Extraction, Transformation und Load) für das Data Warehousing. SSIS enthält grafische Tools und Assistenten zum Erstellen und Debuggen von Paketen; Tasks zum Ausführen von Workflowfunktionen wie z. B. FTP-Vorgänge, Ausführen von SQL-Anweisungen und Senden von E-Mails; Datenquellen und Ziele zum Extrahieren und Laden von Daten; Transformationen zum Bereinigen, Aggregieren, Zusammenführen und Kopieren von Daten; einen Verwaltungsdienst, den [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Dienst zum Verwalten der Paketausführung und -speicherung; und Anwendungsprogrammierschnittstellen (APIs, Application Programming Interfaces) zum Programmieren des [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Objektmodells.  
  
In diesem Tutorial lernen Sie die Verwendung des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers zum Erstellen eines einfachen Pakets in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Das von Ihnen erstellte Paket übernimmt Daten aus einer Flatfile, formatiert die Daten und fügt die neu formatierten Daten in eine Faktentabelle ein. In den folgenden Lektionen wird das Paket erweitert, um Schleifen, Paketkonfigurationen, Protokollierung und Fehlerfluss zu demonstrieren.  
  
Beim Installieren der im Lernprogramm verwendeten Beispieldaten werden auch die abgeschlossenen Versionen der Pakete, die Sie in der jeweiligen Lektion des Lernprogramms erstellen werden, installiert. Mithilfe der abgeschlossenen Pakete können Sie Lektionen überspringen und nach Belieben mit einer späteren Lektion in das Lernprogramm einsteigen. Wenn dies Ihre erste Erfahrung mit Paketen oder mit der neuen Entwicklungsumgebung ist, empfehlen wir Ihnen, mit Lektion 1 zu beginnen.  
  
## <a name="what-you-will-learn"></a>Lernziele  
Die beste Möglichkeit, den Umgang mit den neuen Tools, Steuerelementen und Funktionen von [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] zu üben, besteht in ihrer Verwendung. Dieses Lernprogramm leitet Sie Schritt für Schritt durch den [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer, um ein einfaches ETL-Paket einschließlich Schleifen, Konfigurationen, Fehlerflusslogik und Protokollierung zu erstellen.  
  
## <a name="requirements"></a>Anforderungen  
Dieses Tutorial wendet sich an Benutzer, die mit grundlegenden Datenbankvorgängen vertraut sind, aber nur über begrenzte Kenntnisse in Bezug auf die neuen Funktionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]verfügen.  
  
Ihr System muss die folgenden installierten Komponenten aufweisen, damit dieses Lernprogramm verwendet werden kann:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]mit der **AdventureWorksDW2012** Datenbank. Aus Sicherheitsgründen werden die Beispieldatenbanken standardmäßig nicht installiert. Wie die **AdventureWorksDW2012** -Datenbank heruntergeladen wird, informieren Sie sich unter [Adventure Works für SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=275026).  
  
    > [!IMPORTANT]  
    > Wenn Sie die Datenbank (\*.mdf-Datei) anfügen, sucht [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] standardmäßig nach einer LDF-Datei. Sie müssen die LDF-Datei manuell entfernen, bevor Sie im Dialogfeld **Datenbanken anfügen** auf OK klicken.  
    >   
    > Weitere Informationen zum Anfügen von Datenbanken finden Sie unter [Anfügen einer Datenbank](../relational-databases/databases/attach-a-database.md).  
  
-   Beispieldaten. Die Beispieldaten sind in den [!INCLUDE[ssIS](../includes/ssis-md.md)] -Lektionspaketen enthalten. Um die Beispieldaten und die Lektionspakete herunterzuladen, gehen Sie wie folgt vor.  
  
    1.  Klicken Sie [hier](http://go.microsoft.com/fwlink/?LinkId=275027), um zur Seite Integration Services Product Samples zu gelangen  
  
    2.  Klicken Sie auf die Registerkarte **DOWNLOADS** .  
  
    3.  Klicken Sie auf die Datei SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
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
  
  
  

