---
title: Sicherungsoptionen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7c2d6f719e6b37560e515558175cc3389072bc69
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="backup-options"></a>Sicherungsoptionen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Es gibt viele Möglichkeiten, um Ihre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken zu sichern, und für all diese Sicherungsmöglichkeiten benötigen Sie Administratorberechtigungen für den Server und für die Datenbank. Sie können das **Sichern** -Dialogfeld in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]öffnen, die geeignete Optionskonfiguration auswählen und dann die Sicherung aus dem Dialogfeld starten. Sie können aber auch ein Skript erstellen, wobei die bereits in der Datei angegebenen Einstellungen verwendet werden. Dieses Skript kann dann gespeichert und beliebig häufig ausgeführt werden.  
  
## <a name="backup-and-synchronize"></a>Sichern und Synchronisieren  
 Wenn sich die Datenbank auf einer Remoteinstanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]befindet, können Sie die Datenbank mit der Synchronisierungsfunktion auf der lokalen Instanz sichern. Auf diese Weise können Entwicklungsbuilds einer Datenbank in die Produktionsumgebung verschoben werden. Sie können zwar auch das herkömmliche, auf Dateien basierende Sichern und Wiederherstellen verwenden, um das Entwicklungsbuild in die Produktionsumgebung zu verschieben, die Synchronisierung bietet aber zusätzliche Features. Wenn z. B. auf dem Entwicklungscomputer andere Sicherheitseinstellungen vorliegen als auf dem Produktionscomputer, haben Sie bei der Synchronisierung die Option, diese Einstellungen beizubehalten und alle Objekte außer Rollen zu synchronisieren. Außerdem erfolgt bei der Synchronisierung typischerweise ein inkrementelles Update der Objekte, die sich auf dem Quell- und auf dem Zielcomputer unterscheiden. Diese Art der inkrementellen Sicherung steht beim Verwenden der Sichern/Wiederherstellen-Funktion nicht zur Verfügung. Weitere Informationen finden Sie unter [Synchronize Analysis Services Databases](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md).  
  
> [!IMPORTANT]  
>  Das Analysis Services-Dienstkonto muss über die Berechtigung zum Schreiben von Daten in den für jede Datei angegebenen Sicherungsspeicherort verfügen. Dem Benutzer muss zudem eine der folgenden Rollen zugewiesen worden sein: Administratorrolle für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz oder Mitglied einer Datenbankrolle mit der Berechtigung Vollzugriff (Administrator) für die wiederherzustellende Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherungsdatenbank (Dialogfeld) & #40; Analysis Services – mehrdimensionale Daten & #41;](http://msdn.microsoft.com/library/7811ce7d-6c37-4189-bfa6-ef36fb4932db)   
 [Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [Backup-Element & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [Sichern, wiederherstellen und Synchronisieren von Datenbanken & #40; XMLA & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
