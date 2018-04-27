---
title: Dateien zum Verwalten von Projektmappen und Projekten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-solutions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5af04c43ed4b8adaa9a5a86dba1320fd59865744
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="files-that-manage-solutions-and-projects"></a>Dateien zum Verwalten von Projektmappen und Projekten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 In diesem Thema werden die Dateitypen von [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]beschrieben. Standardmäßig werden alle Projektmappen und Projekte im Verzeichnis \Meine Dokumente\SQL Server Management Studio Projects erstellt.  


## <a name="management-studio-solution-files"></a>Management Studio-Projektmappendateien  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] verwendet andere Dateitypen als [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] oder [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Studio. Dies bedeutet, dass Sie eine [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] -Projektmappe nicht in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] oder in Visual Studio öffnen können. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] Projektmappendateien ermöglichen dem Projektmappen-Explorer, eine grafische Benutzeroberfläche zum Verwalten Ihrer Dateien anzuzeigen.  
   
|Erweiterung|Dateityp|Description|Erstellt von|  
|-------------|-------------|---------------|--------------|  
|SSMSSLN|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] Projektmappenobjekt|Stellt der Umgebung Verweise auf den Speicherort auf dem Datenträger von [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Projekten, -Projektelementen und -Projektmappen bereit|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]|  
  
## <a name="management-studio-project-files"></a>Management Studio-Projektdateien  
In derselben Weise, wie Projektmappen Projektmappendateien zum Verwalten von Objekten in einer Projektmappe enthalten, enthalten Projekte Projektdateien. Der Projektdateityp, der von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] für ein Projekt erstellt wird, hängt von der Vorlage ab, mit der das Projekt erstellt wurde. In der folgenden Tabelle werden die Dateitypen beschrieben, die für die einzelnen Projekte erstellt werden.  
   
|Erweiterung|Projektvorlage|  
|-------------|--------------------|  
|SSMSSQLPROJ|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Skriptprojekt|  
|SSMSASPROJ|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Skriptprojekt|  
   
## <a name="location-of-solution-level-files"></a>Speicherort für Dateien auf Projektmappenebene  
Standardmäßig werden Dateien auf Projektmappenebene im physischen Verzeichnis des ersten Projekts erstellt, das mit der Projektmappe erstellt wird. Sie können ein Verzeichnis für die Projektmappe angeben, indem Sie eine Projektmappe erstellen. Sie können das Verzeichnis auch angeben, wenn Sie ein neues Projekt erstellen.  
 
Wenn eine Verzeichnisstruktur vorhanden ist, die der logischen Struktur im Projektmappen-Explorer ähnelt, lassen sich Projekt- und Projektmappendateien einfacher suchen und mit anderen Entwicklern im Team gemeinsam nutzen.  
   
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Verwalten von Dateien mit Codierung](../../ssms/solution/manage-files-with-encoding.md)  
[Sonstige Dateien](../../ssms/solution/miscellaneous-files.md)  
[Projektmappen-Explorer](../../ssms/solution/solution-explorer.md)  
[Projektmappen &#40;SQL Server Management Studio&#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[Projekte &#40;SQL Server Management Studio&#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
[Quellcodeverwaltung des Projektmappen-Explorers](https://msdn.microsoft.com/en-us/library/ms173879.aspx)  
  
