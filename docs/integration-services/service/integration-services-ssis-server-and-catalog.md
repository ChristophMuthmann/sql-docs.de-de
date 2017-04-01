---
title: "SQL Server Integration Services (SSIS)-Server und Katalog | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Pakete [Integration Services], verwalten"
  - "Verwalten von Paketen [Integration Services]"
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# SQL Server Integration Services (SSIS)-Server und Katalog
  Nachdem Sie Pakete und Konfigurationen in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]entworfen und getestet haben, können Sie die Projekte, die die Pakete enthalten, auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen.  
  
 Die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Server ist eine Instanz der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] der als Host der **SSISDB** Datenbank. Die Datenbank speichert die folgenden Objekte: Pakete, Projekte, Parameter, Berechtigungen, Servereigenschaften und Verwendungsverlauf.  
  
 Die **SSISDB** -Datenbank macht die Objektinformationen in öffentlichen Sichten verfügbar, die Sie abfragen können. Die Datenbank stellt auch gespeicherte Prozeduren bereit, die Sie aufrufen können, um die Objekte zu verwalten.  
  
 Vor der Bereitstellung der Projekte, die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Server, müssen Sie zum Erstellen der **SSISDB** Katalog.  
  
 Einen Überblick über die Funktionen des SSISDB-Katalogs finden Sie unter [SSIS-Katalog](../../integration-services/service/ssis-catalog.md).  
  
## Hohe Verfügbarkeit  
 Wie andere Benutzerdatenbanken unterstützt die Datenbank **SSISDB** die Datenbankspiegelung und Replikation. Weitere Informationen zur Spiegelung und Replikation finden Sie unter [Datenbankspiegelung & #40; SQL Server & #41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 Sie können auch hohe Verfügbarkeit von SSISDB und die Inhalte bereitstellen, und Verwenden von SSIS und AlwaysOn-Verfügbarkeitsgruppen. Weitere Informationen finden Sie im Blogbeitrag von Matt Masson [SSIS mit AlwaysOn](http://go.microsoft.com/fwlink/?LinkId=255873), auf blogs.msdn.com.  
  
##  <a name="ssms"></a> Integration Services-Server in SQL Server Management Studio  
 Die Verbindung mit einer Instanz von der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] der als Host der **SSISDB** Datenbank Sie die folgenden Objekte im Objekt-Explorer finden Sie unter:  
  
-   **SSISDB-Datenbank**  
  
     Die **SSISDB** -Datenbank wird unter dem Knoten **Datenbanken** im Objekt-Explorer angezeigt. Sie können die Sichten abfragen und die gespeicherten Prozeduren aufrufen, die zur Verwaltung des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Servers sowie der darauf gespeicherten Objekte verwendet werden.  
  
-   **Integration Services-Kataloge**  
  
     Unter dem Knoten **Integration Services-Kataloge** befinden sich Ordner für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekte und -Umgebungen.  
  
## Verwandte Aufgaben  
  
-   [Erstellen des SSIS-Katalogs](../../integration-services/service/create-the-ssis-catalog.md)  
  
-   [Anzeigen der Liste der auf dem Integration Services-Server gespeicherten Pakete](../../integration-services/service/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Bereitstellen von Projekten auf dem Integration Services-Server](../../integration-services/packages/deploy-projects-to-integration-services-server.md)  
  
-   [Ausführen eines Pakets auf dem SSIS-Server mit SQL Server Management Studio](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## Verwandte Inhalte  
 Blogeintrag [SSIS mit AlwaysOn](http://go.microsoft.com/fwlink/?LinkId=255873), auf blogs.msdn.com.  
  
  