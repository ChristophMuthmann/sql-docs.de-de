---
title: SQL Server Integration Services (SSIS)-Server und Katalog | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 939f31adf1ab0a975bd4339dabab310ef9025049
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-server-and-catalog"></a>SQL Server Integration Services (SSIS)-Server und -Katalog
  Nachdem Sie Pakete und Konfigurationen in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]entworfen und getestet haben, können Sie die Projekte, die die Pakete enthalten, auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen.  
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server stellt eine Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] dar, die als Host für die **SSISDB** -Datenbank fungiert. Die Datenbank speichert die folgenden Objekte: Pakete, Projekte, Parameter, Berechtigungen, Servereigenschaften und Verwendungsverlauf.  
  
 Die **SSISDB** -Datenbank macht die Objektinformationen in öffentlichen Sichten verfügbar, die Sie abfragen können. Die Datenbank stellt auch gespeicherte Prozeduren bereit, die Sie aufrufen können, um die Objekte zu verwalten.  
  
 Bevor Sie die Projekte auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen können, müssen Sie den **SSISDB** -Katalog erstellen.  
  
 Einen Überblick über die Funktionen des SSISDB-Katalogs finden Sie unter [SSIS-Katalog](../../integration-services/service/ssis-catalog.md).  
  
## <a name="high-availability"></a>Hohe Verfügbarkeit  
 Wie andere Benutzerdatenbanken unterstützt die Datenbank **SSISDB** die Datenbankspiegelung und Replikation. Weitere Informationen zur Spiegelung und Replikation finden Sie unter [Datenbankspiegelung &#40; SQLServer &#41; ](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 Sie können auch hohe Verfügbarkeit von SSISDB und dessen Inhalt angeben, indem Sie die Verfügbarkeit von SSIS und AlwaysOn-Verfügbarkeitsgruppen verwenden. Weitere Informationen finden Sie im folgenden Blogbeitrag von Matt Masson, [SSIS mit Always On-](http://go.microsoft.com/fwlink/?LinkId=255873), auf blogs.msdn.com.  
  
##  <a name="ssms"></a> Integration Services-Server in SQL Server Management Studio  
 Wenn Sie eine Verbindung mit einer Instanz des [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] dar, die als Host für die **SSISDB** -Datenbank fungiert, werden die folgenden Objekte im Objekt-Explorer angezeigt:  
  
-   **SSISDB-Datenbank**  
  
     Die **SSISDB** -Datenbank wird unter dem Knoten **Datenbanken** im Objekt-Explorer angezeigt. Sie können die Sichten abfragen und die gespeicherten Prozeduren aufrufen, die zur Verwaltung des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Servers sowie der darauf gespeicherten Objekte verwendet werden.  
  
-   **Integration Services-Kataloge**  
  
     Unter dem Knoten **Integration Services-Kataloge** befinden sich Ordner für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekte und -Umgebungen.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Zeigen Sie die Liste der Pakete auf dem Integration Services-Server an.](../../integration-services/service/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Bereitstellen von Integrationsservices (SSIS)-Projekten und Paketen](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
-   [Ausführen von Integration Services-Paketen (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Blogeintrag, [SSIS mit Always On-](http://go.microsoft.com/fwlink/?LinkId=255873), auf blogs.msdn.com.  
  
  
