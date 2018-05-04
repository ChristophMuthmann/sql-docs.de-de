---
title: Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5bad31d802f1ea9678c5accc2ce24bb1e7a25821
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>Bereitstellung von Skriptdateien - Eingabe verwendet, um die Bereitstellungsskripts erstellen
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Bei der Erstellung einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Dateien für das Projekt generiert. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] legt diese Dateien im Ausgabeordner des der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt. Standardmäßig erfolgt die Ausgabe in den Ordner \Bin. In der folgenden Tabelle werden die von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellten Dateien aufgeführt.  
  
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
  
  
