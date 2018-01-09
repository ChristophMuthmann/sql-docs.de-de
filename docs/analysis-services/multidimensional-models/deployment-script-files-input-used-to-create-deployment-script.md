---
title: Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: affa6ce1f6ac586ea59607da196b6a4d2dc0f666
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>Bereitstellung von Skriptdateien - Eingabe verwendet, um die Bereitstellungsskripts erstellen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Bei der Erstellung einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Dateien für das Projekt generiert. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]legt diese Dateien im Ausgabeordner des der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt. Standardmäßig erfolgt die Ausgabe in den Ordner \Bin. In der folgenden Tabelle werden die von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellten Dateien aufgeführt.  
  
|File|Description|  
|---------------|-----------------|  
|\<*Projektname*> .asdatabase|Ein XMLA-Datei für die mehrdimensionalen oder tabellarischen Modellprojekten 1100/1103 oder einer JSON-Datei für tabellarische 1200 und höher Modellprojekten. Enthält die deklarativen Definitionen für alle [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte im Projekt.|  
|\<*Projektname*> .deploymenttargets|Enthält den Namen der Instanz und der Datenbank von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , in der die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte erstellt werden.|  
|\<*Projektname*> .configsettings|Enthält umgebungsspezifische Einstellungen wie Verbindungsinformationen für die Datenquelle und Speicherorte für die Objektspeicherung. Einstellungen in dieser Datei überschreiben die Einstellungen in der \< *Projektname*> .asdatabase-Datei.|  
|\<*Projektname*> .deploymentoptions|Enthält Bereitstellungsoptionen, z. B. ob es sich um eine Transaktionsbereitstellung handelt und ob die bereitgestellten Objekte nach der Bereitstellung verarbeitet werden sollen.|  
  
> [!NOTE]  
>  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] werden Kennwörter nie in den Projektdateien gespeichert.  
  
## <a name="modifying-the-input-files"></a>Ändern der Eingabedateien  
 Durch Ändern der Werte in den Eingabedateien bzw. der aus den Eingabedateien abgerufenen Werte kann so ändern Sie das Bereitstellungsziel sowie die Konfigurationseinstellungen und Bereitstellungsoptionen, ohne die gesamte bearbeiten \< *Projekt Namen*> .asdatabase-Datei (oder eine gesamte Skriptdatei, wenn Sie ein Skript aus einer vorhandenen generieren [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank). Durch die Möglichkeit, einzelne Dateien zu ändern, können Sie auf einfache Weise verschiedene Bereitstellungsskripts für unterschiedliche Zwecke erstellen.  
  
 In den folgenden Themen wird erläutert, wie Sie Werte in den verschiedenen Eingabedateien ändern:  
  
-   [Angeben des Installationszieles](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)  
  
-   [Angeben von Bereitstellungsoptionen für Partitionen und Rollen](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [Angeben der Konfigurationseinstellungen für die Lösungsbereitstellung](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
-   [Angeben von Verarbeitungsoptionen](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen des Bereitstellungs-Assistenten für Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Grundlegendes zum Analysis Services-Bereitstellungsskript](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  
