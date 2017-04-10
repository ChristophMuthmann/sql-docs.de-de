---
title: "Angeben der Konfigurationseinstellungen f&#252;r die L&#246;sungsbereitstellung | Microsoft Docs"
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
  - "Bereitstellungs-Assistent für Analysis Services, Konfigurationseinstellungen"
  - "Eingabedateien [Analysis Services]"
  - "Konfigurationsoptionen [Analysis Services]"
  - "Analysis Services-Bereitstellungen, Konfigurationseinstellungen"
  - "Bereitstellen [Analysis Services], Konfigurationseinstellungen"
ms.assetid: 953814a3-85ef-40cc-b46a-d532aa7a6569
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Angeben der Konfigurationseinstellungen f&#252;r die L&#246;sungsbereitstellung
  Der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Bereitstellungs-Assistent liest die Bereitstellungsoptionen für Partitionen und Rollen, die Sie im Bereitstellungsskript verwenden, aus der Datei \<*project name*>.configsettings. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellt diese Datei, wenn Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erstellen. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellt die Datei \<*project name*>.configsettings mit den Konfigurationseinstellungen des aktuellen Projekts.  
  
## Überprüfen der Konfigurationseinstellungen für die Bereitstellung  
 Die folgenden Konfigurationseinstellungen sind in der Datei \<*project name*>.configsettings gespeichert:  
  
-   **Datenquellen-Verbindungszeichenfolgen** Hierbei handelt es sich um die Verbindungszeichenfolgen für die jeweiligen Datenquellen basierend auf den im [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt angegebenen Werten. Die Benutzer-ID und das Kennwort werden stets aus der Verbindungszeichenfolge entfernt, bevor die restliche Zeichenfolge in dieser Datei gespeichert wird. Wenn jedoch die Bereitstellung durch den Bereitstellungs-Assistenten direkt auf einer Analysis Services-Instanz erfolgt, können Sie die entsprechenden Informationen zur Benutzer-ID und zum Kennwort im Assistenten hinzufügen, um eine erfolgreiche Verarbeitung der Bereitstellungsdatenbank zu ermöglichen. Diese Verbindungsinformationen werden nicht direkt im Bereitstellungsskript gespeichert, wenn ein solches vom Bereitstellungs-Assistenten gespeichert wird.  
  
-   **Identitätswechselkonten** Diese Einstellung gibt den Benutzernamen an, unter dem in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Anweisungen in den einzelnen Datenquellen ausgeführt werden. Wird kein Identitätswechselkonto angegeben, verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zum Ausführen von Anweisungen das Anmeldekonto. Wenn das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Anmeldekonto über Berechtigungen direkt in der Datenquelle verfügt, haben alle Datenbankadministratoren in allen Datenbanken in der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] über das Anmeldekonto Zugriff auf die Datenquelle. Wenn ein Benutzerkonto und ein Kennwort angegeben sind, werden diese Informationen stets entfernt, bevor die Identitätswechselinformationen in dieser Datei gespeichert werden. Wenn jedoch die Bereitstellung durch den Bereitstellungs-Assistenten direkt auf einer Analysis Services-Instanz erfolgt, können Sie die entsprechenden Informationen zur Benutzer-ID und zum Kennwort im Assistenten hinzufügen, um eine erfolgreiche Verarbeitung der Bereitstellungsdatenbank zu ermöglichen. Diese Identitätswechselinformationen werden nicht direkt im Bereitstellungsskript gespeichert, wenn ein solches vom Bereitstellungs-Assistenten gespeichert wird.  
  
-   **Schlüsselfehler-Protokolldateien** Diese Einstellung gibt den Dateinamen und Pfad der Schlüsselfehler-Protokolldatei für jeden Cube und für jede Measuregruppe, Partition und Dimension in der Datenbank an.  
  
-   **Speicherorte** Diese Einstellung gibt den Speicherort für jeden Cube, jede Measuregruppe und Partition in der Datenbank an. Wird für ein Objekt kein Wert angegeben, verwendet der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] den Standardspeicherort für das Objekt. Partitionen verwenden beispielsweise den Speicherort für die Measuregruppe, Measuregruppen verwenden den Speicherort für den Cube, und Cubes verwenden den Standardspeicherort für Objekte in der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Als Speicherort kann ein lokaler Pfad oder ein UNC-Pfad (Universal Naming Convention) angegeben werden.  
  
-   **Berichtsserver** Diese Einstellung gibt den Berichtsserver und Ordnerspeicherort für jede in den einzelnen Cubes in der Datenbank definierte Berichtsaktion an.  
  
## Ändern der Konfigurationseinstellungen für die Bereitstellung  
 In manchen Fällen müssen Sie möglicherweise das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Projekt mit anderen Konfigurationseinstellungen bereitstellen, als mit denen, die in der Datei \<*project name*>.configsettings gespeichert sind. Vielleicht möchten Sie die Verbindungszeichenfolge für eine oder mehrere Datenquellen ändern oder Speicherorte für bestimmte Partitionen oder Measuregruppen angeben.  
  
 Um die Bereitstellung von Partitionen und Rollen in einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Projekt zu ändern, müssen Sie diese Informationen wie im Folgenden beschrieben in der Datei \<*project name*>.configsettings ändern. Die Partitions- und Rolleneinstellungen können nicht innerhalb des Projekts geändert werden, da im Dialogfeld *\<project name>* **Eigenschaftenseiten** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] diese Optionen nicht angezeigt werden.  
  
> [!NOTE]  
>  Konfigurationseinstellungen können für alle Objekte oder nur für neu erstellte Objekte gelten. Wenden Sie Konfigurationseinstellungen nur dann auf neu erstellte Objekte an, wenn Sie für eine bereits früher bereitgestellte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank zusätzliche Objekte bereitstellen und vorhandene Objekte nicht überschreiben möchten. Legen Sie diese Option in der Datei \<*project name*>.deploymentoptions fest, um anzugeben, ob Konfigurationseinstellungen für alle Objekte oder nur für die neu erstellten gelten. Weitere Informationen finden Sie unter [Angeben von Bereitstellungsoptionen für Partitionen und Rollen](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md).  
  
#### So ändern Sie Konfigurationseinstellungen, nachdem die Eingabedateien generiert wurden  
  
-   Führen Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interaktiv aus, und geben Sie auf der Seite **Konfigurationseinstellungen** die Konfigurationseinstellungen für die Objekte an, die bereitgestellt werden.  
  
     – oder –  
  
-   Führen Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an der Eingabeaufforderung aus, und legen Sie fest, dass der Assistent im Antwortdateimodus ausgeführt wird. Weitere Informationen zum Antwortdateimodus finden Sie unter [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     – oder –  
  
-   Ändern Sie die Datei \<*Projektname*>.configsettings mit einem beliebigen Text-Editor.  
  
## Siehe auch  
 [Angeben des Installationszieles](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)   
 [Angeben von Bereitstellungsoptionen für Partitionen und Rollen](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)   
 [Angeben von Verarbeitungsoptionen](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  