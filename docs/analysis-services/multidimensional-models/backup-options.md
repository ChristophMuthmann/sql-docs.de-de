---
title: "Sicherungsoptionen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sichern von Datenbanken [Analysis Services]"
  - "Datenbanken [Analysis Services], Sichern"
ms.assetid: 02d33fc9-f3f4-4b85-8b90-449b68625cf7
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 26
---
# Sicherungsoptionen
  Es gibt viele Möglichkeiten, um Ihre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken zu sichern, und für all diese Sicherungsmöglichkeiten benötigen Sie Administratorberechtigungen für den Server und für die Datenbank. Sie können das **Sichern** -Dialogfeld in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]öffnen, die geeignete Optionskonfiguration auswählen und dann die Sicherung aus dem Dialogfeld starten. Sie können aber auch ein Skript erstellen, wobei die bereits in der Datei angegebenen Einstellungen verwendet werden. Dieses Skript kann dann gespeichert und beliebig häufig ausgeführt werden.  
  
## Sichern und Synchronisieren  
 Wenn sich die Datenbank auf einer Remoteinstanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]befindet, können Sie die Datenbank mit der Synchronisierungsfunktion auf der lokalen Instanz sichern. Auf diese Weise können Entwicklungsbuilds einer Datenbank in die Produktionsumgebung verschoben werden. Sie können zwar auch das herkömmliche, auf Dateien basierende Sichern und Wiederherstellen verwenden, um das Entwicklungsbuild in die Produktionsumgebung zu verschieben, die Synchronisierung bietet aber zusätzliche Features. Wenn z. B. auf dem Entwicklungscomputer andere Sicherheitseinstellungen vorliegen als auf dem Produktionscomputer, haben Sie bei der Synchronisierung die Option, diese Einstellungen beizubehalten und alle Objekte außer Rollen zu synchronisieren. Außerdem erfolgt bei der Synchronisierung typischerweise ein inkrementelles Update der Objekte, die sich auf dem Quell- und auf dem Zielcomputer unterscheiden. Diese Art der inkrementellen Sicherung steht beim Verwenden der Sichern/Wiederherstellen-Funktion nicht zur Verfügung. Weitere Informationen finden Sie unter [Synchronize Analysis Services Databases](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md).  
  
> [!IMPORTANT]  
>  Das Analysis Services-Dienstkonto muss über die Berechtigung zum Schreiben von Daten in den für jede Datei angegebenen Sicherungsspeicherort verfügen. Dem Benutzer muss zudem eine der folgenden Rollen zugewiesen worden sein: Administratorrolle für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz oder Mitglied einer Datenbankrolle mit der Berechtigung Vollzugriff (Administrator) für die wiederherzustellende Datenbank.  
  
## Siehe auch  
 [Dialogfeld Sicherungsdatenbank &#40;Analysis Services – Mehrdimensionale Daten%#41;](../Topic/Backup%20Database%20Dialog%20Box%20\(Analysis%20Services%20-%20Multidimensional%20Data\).md)   
 [Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [Backup-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [Sichern, Wiederherstellen und Synchronisieren von Datenbanken &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  