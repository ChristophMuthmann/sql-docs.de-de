---
title: "Angeben von Verarbeitungsoptionen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services-Bereitstellungen, Verarbeitungsoptionen"
  - "Eingabedateien [Analysis Services]"
  - "Bereitstellen [Analysis Services], Verarbeitungsoptionen"
  - "Ändern von Verarbeitungsoptionen"
  - "Bereitstellungsassistenten für Analysis Services, Verarbeitungsoptionen"
ms.assetid: e9e50817-908e-4210-bc3d-8e2957568241
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Angeben von Verarbeitungsoptionen
  Der Assistent für die Bereitstellung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] liest die Verarbeitungsoptionen aus der Datei „\<*Projektname*>.deploymentoptions“. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellt diese Datei, wenn Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erstellen. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellt die Datei „\<*Projektname*>.deploymentoptions“ mit den Verarbeitungsoptionen, die im Dialogfeld **Eigenschaftenseiten** von *\<Projektname>* auf der Seite **Bereitstellung** angegeben sind.  
  
## Überprüfen der Verarbeitungsoptionen für die Bereitstellung  
 Die folgenden Konfigurationseinstellungen sind in der Datei „\<*Projektname*>.deploymentoptions“ gespeichert:  
  
-   **Verarbeitungsmethode** Diese Einstellung steuert, ob die bereitgestellten Objekte nach der Bereitstellung verarbeitet werden und welche Art von Verarbeitung ausgeführt wird. Es stehen drei Verarbeitungsoptionen zur Verfügung:  
  
    -   Standardverarbeitung (Standardeinstellung)  
  
    -   Vollständige Verarbeitung  
  
    -   InclusionThresholdSetting  
  
-   **Optionen für die Rückschreibetabelle** Wenn im [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt Rückschreiben aktiviert ist, wird mit dieser Einstellung die Ausführung dieses Vorgangs definiert. Es sind drei Rückschreibetabellenoptionen verfügbar:  
  
    -   Wenn eine Rückschreibetabelle vorhanden ist, wird diese standardmäßig verwendet. Ist keine Rückschreibetabelle vorhanden, wird eine neue Rückschreibetabelle erstellt.  
  
    -   Wenn bereits eine Rückschreibetabelle vorhanden ist, kann die Bereitstellung nicht durchgeführt werden. Ist keine Rückschreibetabelle vorhanden, wird eine neue Rückschreibetabelle erstellt.  
  
    -   Unabhängig davon, ob bereits eine Rückschreibetabelle vorhanden ist, wird eine neue Rückschreibetabelle erstellt. In diesem Fall löscht der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die vorhandene Tabelle und ersetzt sie durch eine neue Rückschreibetabelle.  
  
-   **Transaktionsbereitstellung** Diese Einstellung steuert, ob die Bereitstellung von Metadatenänderungen und Verarbeitungsbefehlen in einer einzelnen Transaktion oder in getrennten Transaktionen erfolgt.  
  
    -   Wenn diese Option auf **TRUE** (Standard) festgelegt ist, stellt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alle Metadatenänderungen und alle Verarbeitungsbefehle in einer einzelnen Transaktion bereit.  
  
    -   Ist diese Option **FALSE**, stellt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Metadatenänderungen in einer einzelnen Transaktion und jeden Verarbeitungsbefehl jeweils in einer eigenen Transaktion bereit.  
  
## Ändern der Verarbeitungsoptionen für die Bereitstellung  
 Möglicherweise müssen Sie jedoch das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Projekt mit anderen Verarbeitungsoptionen bereitstellen, als denen, die in der Datei „\<*Projektname*>.deploymentoptions“ gespeichert sind. Vielleicht sollen alle Objekte vollständig oder mithilfe der Standardverarbeitungsoption oder überhaupt nicht verarbeitet werden. Wenn die Cubes oder Dimensionen für den Schreibzugriff aktiviert sind, können Sie angeben, ob eine neue oder eine vorhandene Rückschreibetabelle verwendet werden soll.  
  
 Wenn Sie die bei der Bereitstellung zu verwendenden Verarbeitungsoptionen ändern möchten, können Sie entweder das Projekt bearbeiten und neu erstellen, oder Sie ändern mithilfe einer der im Folgenden beschriebenen Prozedur die Verarbeitungsoptionen in der Eingabedatei.  
  
#### So ändern Sie Verarbeitungsoptionen, nachdem die Eingabedateien generiert wurden  
  
-   Führen Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interaktiv aus. Geben Sie auf der Seite **Verarbeitungsoptionen** die Verarbeitungsoptionen für das bereitzustellende Projekt an.  
  
     – oder –  
  
-   Führen Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an der Eingabeaufforderung aus, und legen Sie fest, dass der Assistent im Antwortdateimodus ausgeführt wird. Weitere Informationen zum Antwortdateimodus finden Sie unter [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     – oder –  
  
-   Ändern Sie die Datei „\<*Projektname*>.deploymentoptions“ mit einem beliebigen Text-Editor.  
  
## Siehe auch  
 [Angeben des Installationszieles](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)   
 [Angeben von Bereitstellungsoptionen für Partitionen und Rollen](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)   
 [Angeben der Konfigurationseinstellungen für die Lösungsbereitstellung](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)  
  
  