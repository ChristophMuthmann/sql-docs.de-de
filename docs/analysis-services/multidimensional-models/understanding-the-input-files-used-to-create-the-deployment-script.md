---
title: "Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien | Microsoft Docs"
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
  - "Eingabedateien [Analysis Services]"
  - "Bereitstellungs-Assistent für Analysis Services, Skripts"
  - "Bereitstellen [Analysis Services], Eingabedateien"
  - "Bereitstellungs-Assistent für Analysis Services, Eingabedateien"
  - "Skripts [Analysis Services], Bereitstellung"
  - "Analysis Services-Bereitstellungen, Eingabedateien"
  - "Ändern von Eingabedateien"
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien
  Wenn Sie ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erstellen, generiert [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] XML-Dateien für das Projekt. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] legt diese XML-Dateien im Ausgabeordner des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts ab. Standardmäßig erfolgt die Ausgabe in den Ordner „\\Bin“. In der folgenden Tabelle werden die von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellten Dateien aufgeführt.  
  
|XMLA-Datei|Description|  
|---------------|-----------------|  
|\<*Projektname*\>.asdatabase|Enthält die deklarativen Definitionen für alle [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte im Projekt.|  
|\<*Projektname*\>.deploymenttargets|Enthält den Namen der Instanz und der Datenbank von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , in der die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte erstellt werden.|  
|\<*Projektname*\>.configsettings|Enthält umgebungsspezifische Einstellungen wie Verbindungsinformationen für die Datenquelle und Speicherorte für die Objektspeicherung. Die Einstellungen in dieser Datei überschreiben die Einstellungen in der Datei „\<*Projektname*\>.asdatabase“.|  
|\<*Projektname*\>.deploymentoptions|Enthält Bereitstellungsoptionen, z. B. ob es sich um eine Transaktionsbereitstellung handelt und ob die bereitgestellten Objekte nach der Bereitstellung verarbeitet werden sollen.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] speichert Kennwörter nie in den Projektdateien.  
  
## Ändern der Eingabedateien  
 Durch Ändern der Werte in den Eingabedateien bzw. der aus den Eingabedateien abgerufenen Werte können ein anderes Bereitstellungsziel sowie andere Konfigurationseinstellungen und Bereitstellungsoptionen verwendet werden, ohne dass die gesamte Datei „\<*Projektname*\>.asdatabase“ \(oder eine gesamte XMLA-Skriptdatei, wenn Sie aus einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbank ein Skript generieren\) bearbeitet werden muss. Durch die Möglichkeit, einzelne Dateien zu ändern, können Sie auf einfache Weise verschiedene Bereitstellungsskripts für unterschiedliche Zwecke erstellen.  
  
 In den folgenden Themen wird erläutert, wie Sie Werte in den verschiedenen Eingabedateien ändern:  
  
-   [Angeben des Installationszieles](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)  
  
-   [Angeben von Bereitstellungsoptionen für Partitionen und Rollen](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)  
  
-   [Angeben der Konfigurationseinstellungen für die Lösungsbereitstellung](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)  
  
-   [Angeben von Verarbeitungsoptionen](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
## Siehe auch  
 [Ausführen des Bereitstellungs-Assistenten für Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Grundlegendes zum Analysis Services-Bereitstellungsskript](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  