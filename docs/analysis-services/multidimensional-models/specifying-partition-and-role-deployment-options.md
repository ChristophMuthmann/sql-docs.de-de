---
title: "Angeben von Bereitstellungsoptionen f&#252;r Partitionen und Rollen | Microsoft Docs"
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
  - "Partitionen [Analysis Services], Bereitstellungsoptionen"
  - "Analysis Services-Bereitstellungen, Rollen"
  - "Analysis Services-Bereitstellungen, Partitionen"
  - "Bereitstellungs-Assistent für Analysis Services, Rollen"
  - "Bereitstellungs-Assistent für Analysis Services, Partitionen"
  - "Bereitstellen [Analysis Services], Rollen"
  - "Rollen [Analysis Services], Bereitstellungsoptionen"
  - "Bereitstellen [Analysis Services], Partitionen"
  - "Ändern von Rollenbereitstellungen"
  - "Ändern von Partitionsbereitstellungen"
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
caps.latest.revision: 37
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Angeben von Bereitstellungsoptionen f&#252;r Partitionen und Rollen
  Der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Bereitstellungs-Assistent liest die Optionen für die Partition und die Rollenbereitstellung aus der Datei „\<*Projektname*>.deploymentoptions“. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellt diese Datei, wenn Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erstellen. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] verwendet die Optionen für die Partition und die Rollenbereitstellung des aktuellen Projekts, wenn die Datei „\<*Projektname*>.deploymentoptions“ erstellt wird. Weitere Informationen zu den Konfigurationseinstellungen finden Sie unter [Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md).  
  
## Überprüfen der Bereitstellungsoptionen für Partitionen und Rollen  
 In der Datei „\<*Projektname*>.deploymentoptions“ sind folgende Bereitstellungsoptionen enthalten:  
  
 **Bereitstellungsoptionen für Partitionen**  
 In der Datei „\<*Projektname*>.deploymentoptions“ ist angegeben, ob die vorhandenen Partitionen in der Zieldatenbank beibehalten oder überschrieben (Standardeinstellung) werden. Wenn vorhandene Partitionen beibehalten werden, werden nur neue Partitionen bereitgestellt, und der Partitions- bzw. Aggregationsentwurf in allen vorhandenen Measuregruppen wird nicht geändert.  
  
> [!NOTE]  
>  Wird die Measuregruppe, in der die Partition vorhanden ist, gelöscht, wird die Partition automatisch gelöscht.  
  
 **Bereitstellungsoptionen für Rollen**  
 In der Datei „\<*Projektname*>.deploymentoptions“ ist eine der folgenden Bereitstellungsoptionen für Rollen angegeben:  
  
-   Vorhandene Rollen und Rollenelemente in der Zieldatenbank werden beibehalten, und nur neue Rollen und Rollenelemente werden bereitgestellt.  
  
-   Alle in der Zieldatenbank vorhandenen Rollen und Elemente werden durch die bereitgestellten Rollen und Elemente ersetzt.  
  
-   Vorhandene Rollen und Rollenelemente in der Zieldatenbank werden beibehalten, neue Rollen werden nicht bereitgestellt.  
  
-   **Hinweis:** Wenn vorhandene Rollen und Elemente beibehalten werden, werden die Berechtigungen, die diesen Rollen zugeordnet sind, zurückgesetzt. Sicherheitsberechtigungen sind in den Objekten enthalten, die sie sichern, und nicht in den Sicherheitsrollen, denen sie zugeordnet sind. Weitere Informationen zum Arbeiten mit diesem Verhalten mithilfe des Analysis Services-Bereitstellungs-Assistenten finden Sie im Abschnitt zum Beibehalten von Rollen und Elementen in der Microsoft Knowledge Base.  
  
## Ändern der Bereitstellungsoptionen für Partitionen und Rollen  
 Möglicherweise müssen Sie das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Projekt mit anderen Partitions- und Rollenoptionen bereitstellen, als denen, die in der Datei „\<*Projektname*>.deploymentoptions“ gespeichert sind. Dies wäre beispielsweise dann der Fall, wenn Sie vorhandene Partitionen, Rollen und Rollenelemente beibehalten möchten, statt alle vorhandenen Partitionen, Rollen und Elemente, wie in der Datei „\<*Projektname*>.deploymentoptions“ angegeben ist, zu ersetzen.  
  
 Wenn Sie die Bereitstellung von Partitionen und Rollen in einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Projekt ändern möchten, können Sie die Partitions- und Rolleneinstellungen nicht innerhalb des Projekts ändern, da im Dialogfeld *\<Projektname>*-**Eigenschaftenseiten** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] diese Optionen nicht angezeigt werden. Wenn Sie die Bereitstellungsoptionen für Rollen und Partitionen ändern möchten, müssen Sie diese Informationen in der Datei „\<*Projektname*>.deploymentoptions“ direkt ändern. In der folgenden Vorgehensweise wird beschrieben, wie Sie die Bereitstellungsoptionen für Partitionen und Rollen in der Datei „\<*Projektname*>.deploymentoptions“ ändern.  
  
#### So ändern Sie die Bereitstellung von Partitionen und Rollen, nachdem die Eingabedateien generiert wurden  
  
-   Führen Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interaktiv aus, und geben Sie auf der Seite **Bereitstellungsoptionen für Partitionen und Rollen** neue Bereitstellungsoptionen für die Partitionen und Rollen an.  
  
     – oder –  
  
-   Führen Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an der Eingabeaufforderung aus, und legen Sie fest, dass der Assistent im Antwortdateimodus ausgeführt wird. Weitere Informationen zum Antwortdateimodus finden Sie unter [Ausführen des Bereitstellungs-Assistenten für Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     – oder –  
  
-   Öffnen Sie die Datei „\<*Projektname*>.deploymentoptions“ in einem beliebigen Text-Editor, und ändern Sie die Optionen manuell.  
  
## Siehe auch  
 [Angeben des Installationszieles](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)   
 [Angeben der Konfigurationseinstellungen für die Lösungsbereitstellung](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)   
 [Angeben von Verarbeitungsoptionen](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  