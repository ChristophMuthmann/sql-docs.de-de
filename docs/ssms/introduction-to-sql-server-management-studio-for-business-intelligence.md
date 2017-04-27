---
title: "Einführung in SQL Server Management Studio für BI | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a94d889f59d03adf7ece002e02e54f56704d437c
ms.lasthandoff: 04/11/2017

---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>Einführung in SQL Server Management Studio für Business Intelligence
Verwenden Sie [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] für den Zugriff auf und die Verwaltung von [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)] und [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]. Obwohl alle drei Business Intelligence-Technologien auf [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]basieren, weichen die mit den jeweiligen Technologien verbundenen Verwaltungsaufgaben leicht voneinander ab.  
  
> [!NOTE]  
> Verwenden Sie zum Erstellen und Ändern von Projektmappen in [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)]und [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)]und nicht [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)] ist eine Entwicklungsumgebung, die auf [!INCLUDE[msCoName](../includes/msconame_md.md)][!INCLUDE[vsprvs](../includes/vsprvs_md.md)]basiert.  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>Verwalten von Analysis Services-Lösungen mit SQL Server Management Studio  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] ermöglicht es Ihnen, [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] -Objekte zu verwalten, beispielsweise Ausführen von Sicherungen und Verarbeiten von Objekten.  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] bietet ein [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] -Skriptprojekt, in dem Sie in Multidimensional Expressions (MDX), Data Mining Extensions (DMX) und XML for Analysis (XMLA) geschriebene Skripts entwickeln und speichern können. Sie verwenden [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] -Skriptprojekte, um Verwaltungsaufgaben auszuführen oder Objekte wie Datenbanken oder Cubes in [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] -Instanzen neu zu erstellen. Sie können beispielsweise ein XMLA-Skript in einem [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] -Skriptprojekt entwickeln, das neue Objekte direkt auf einer vorhandenen [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] -Instanz erstellt. Die [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] -Skriptprojekte können als Teil einer Lösung gespeichert werden und mit dem Quellcodeverwaltungssystem integriert werden.  
  
Weitere Informationen zur Verwendung von [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)], finden Sie unter [Entwickeln und Implementieren mithilfe von SQL Server Management Studio](http://msdn.microsoft.com/en-us/c4f5a06b-e2e4-4660-a3a8-6fd356742c02).  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>Verwalten von Integration Services-Lösungen mit SQL Server Management Studio  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] ermöglicht Ihnen die Verwendung des [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] -Diensts, mit dem Sie Pakete verwalten und ausgeführte Pakete überwachen können. Zudem können Sie [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] zur Organisation von Paketen in Ordnern, zum Ausführen von Paketen, zum Im- und Exportieren von Paketen, zum Migrieren von DTS-Paketen (Data Transformation Services) sowie zum Aktualisieren von [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] -Paketen verwenden.  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>Verwalten von Reporting Services-Projekten mit SQL Server Management Studio  
Verwenden Sie SQL Server Management Studio zum Aktivieren von Reporting Services-Funktionen und zum Verwalten von Server und Datenbanken sowie von Rollen und Aufträgen.  
  
Verwalten Sie freigegebene Zeitpläne mit dem Ordner Freigegebene Zeitpläne, und verwalten Sie Berichtsserver-Datenbanken (ReportServer, ReportServerTempdb). Sie können darüber hinaus eine RSExecRole-Rolle in der master-Systemdatenbank erstellen, wenn Sie eine Berichtsserver-Datenbank in ein neues oder anderes SQL Server-Datenbankmodul ([!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] [!INCLUDE[ssDE](../includes/ssde_md.md)]) verschieben. Weitere Informationen zu diesen Aufgaben finden Sie unter den folgenden Themen:  
  
-   [Management Studio (Themen zur Vorgehensweisen)](http://msdn.microsoft.com/en-us/60685458-9108-47bf-820a-5e7db454d408)  
  
-   [Verwalten einer Berichtsserver-Datenbank](http://msdn.microsoft.com/en-us/97b2e1b5-3869-4766-97b9-9bf206b52262)  
  
-   [Vorgehensweise: Erstellen der Rolle 'RSExecRole'](http://msdn.microsoft.com/en-us/7ac17341-df7e-4401-870e-652caa2859c0)  
  
Zudem verwalten Sie den Server, indem Sie verschiedene Funktionen aktivieren und konfigurieren, Serverstandardwerte festlegen und Rollen und Aufträge verwalten. Weitere Informationen zu diesen Aufgaben finden Sie unter den folgenden Themen:  
  
-   [Vorgehensweise: Festlegen von Berichtsservereigenschaften (Management Studio)](http://msdn.microsoft.com/en-us/1ed0f84b-b12a-4e49-b65c-a11a99f9093f)  
  
-   [Vorgehensweise: Erstellen, Löschen oder Ändern einer Rolle (Management Studio)](http://msdn.microsoft.com/en-us/3d1d56e6-a283-44a7-8417-36cb4d2c74d1)  
  
-   [Aktivieren und Deaktivieren von clientseitigem Druck für Reporting Services](http://msdn.microsoft.com/en-us/0e709c96-7517-4547-8ef6-5632f8118524)  
  
## <a name="see-also"></a>Siehe auch  
[Entwickeln und Implementieren mithilfe von SQL Server Data Tools](http://msdn.microsoft.com/en-us/132ed779-3ec8-4734-9698-802116d1b017)  
[Reporting Services in SQL Server-Datentools](http://msdn.microsoft.com/en-us/0903c7b2-ac59-45f1-b7d0-922ecd9d76f8)  
  

