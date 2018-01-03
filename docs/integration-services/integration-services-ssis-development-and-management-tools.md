---
title: "SQL Server Integration Services (SSIS) – Entwicklungs- und Verwaltungstools | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- studio environments [Integration Services]
- tools [Integration Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, Integration Services in
- SQL Server Management Studio [Integration Services]
- SSIS, studio environments
- SQL Server Integration Services, studio environments
- tools [Integration Services], SQL Server Management Studio
ms.assetid: 4eb73e65-d9f3-4ac6-a408-abfa85afc537
caps.latest.revision: "52"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b78023eab9f0a737276e02c76a0ef27ce16c3002
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="integration-services-ssis-development-and-management-tools"></a>SQL Server Integration Services (SSIS) – Entwicklungs- und Verwaltungstools
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] enthält zwei Studio-Umgebungen für das Arbeiten mit Paketen:  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] zum Entwickeln der für eine Unternehmenslösung erforderlichen [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakete. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] stellt das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt bereit, in dem Sie Pakete erstellen.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] zum Verwalten von Paketen in einer Produktionsumgebung.  
  
## <a name="sql-server-data-tools"></a>SQL Server Datatools  
 In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]können Sie die folgenden Aufgaben ausführen:  
  
-   Ausführen des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Import/Export-Assistenten, um Basispakete zu erstellen, mit denen Daten von einer Quelle in ein Ziel kopiert werden.  
  
-   Erstellen von Paketen, die eine komplexe Ablaufsteuerung, ereignisgesteuerte Logik und Protokollierung sowie einen komplexen Datenfluss enthalten.  
  
-   Testen und Debuggen von Paketen mithilfe der Problembehandlungs- und Überwachungsfunktionen im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer und der Debuggingfunktionen in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   Erstellen von Konfigurationen, mit denen die Eigenschaften von Paketen und Paketobjekten zur Laufzeit aktualisiert werden.  
  
-   Erstellen eines Bereitstellungshilfsprogramms, das Pakete und deren Abhängigkeiten auf anderen Computern installieren kann.  
  
-   Speichern von Kopien von Paketen in der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-msdb-Datenbank, im [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paketspeicher und im Dateisystem.  
  
 Weitere Informationen zu [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]finden Sie unter [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686.aspx).  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] stellt den [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Dienst bereit, mit dem Sie Pakete verwalten, ausgeführte Pakete überwachen sowie Auswirkungen und die Datenherkunft für [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Objekte und [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Objekte bestimmen können.  
  
 In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]können Sie die folgenden Aufgaben ausführen:  
  
-   Erstellen von Ordnern, um Pakete auf eine für Ihre Organisation sinnvolle Weise zu organisieren.  
  
-   Ausführen von Paketen, die auf dem lokalen Computer gespeichert sind, mithilfe des Paketausführungshilfsprogramms.  
  
-   Führen Sie das Paketausführungs-Hilfsprogramm zum Generieren einer Befehlszeile aus, wenn das Eingabeaufforderungs-Hilfsprogramm **dtexec** (dtexec.exe) ausgeführt wird.  
  
-   Importieren und Exportieren Sie Pakete aus der und zur [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-MSDB-Datenbank, dem  [!INCLUDE[ssIS](../includes/ssis-md.md)] -Paketspeicher und dem Dateiensystem.  
