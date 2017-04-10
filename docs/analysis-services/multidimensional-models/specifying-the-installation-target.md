---
title: "Angeben des Installationszieles | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Eingabedateien [Analysis Services]"
  - "Installationsziele [Analysis Services]"
  - "Analysis Services-Bereitstellungen, Installationsziele"
  - "Bereitstellungs-Assistent für Analysis Services, Installationsziele"
  - "Bereitstellen [Analysis Services], Installationsziele"
  - "Ändern von Installationszielen"
ms.assetid: cb706817-6f63-4771-92c3-b70030bbce3d
caps.latest.revision: 35
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Angeben des Installationszieles
  Der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] liest die Informationen zum Installationsziel aus der Datei „\<*Projektname*>.deploymenttargets“. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellt diese Datei, wenn Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erstellen. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellt die Datei „\<*Projektname*>.targets“ anhand der Datenbank und des Servers, die bzw. der auf der Seite **Bereitstellung** im Dialogfeld **Eigenschaftenseiten** von *\<Projektname>* angegeben sind.  
  
## Ändern des Installationszieles für die Bereitstellung  
 In einigen Situationen müssen Sie möglicherweise ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt für eine andere Datenbank oder eine andere Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitstellen, als auf der Seite **Bereitstellung** angegeben ist. Vielleicht möchten Sie das Projekt, bevor Sie es bereitstellen, erst auf einem Server zum Testen bereitstellen und es nach Abschluss der Testes auf einem Produktionsserver bereitstellen. Sie können aber auch ein abgeschlossenes und getestetes Projekt auf mehreren Produktionsservern in einem Netzwerklastenausgleich-Cluster oder auf einem Stagingserver und einem Produktionsserver bereitstellen.  
  
 Sie können mit einer der im Folgenden beschriebenen Methoden das Installationsziel in der Eingabedatei ändern, um ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt auf einer anderen Datenbank oder einer anderen Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitzustellen.  
  
#### So ändern Sie das Installationsziel, nachdem die Eingabedateien erstellt wurden  
  
-   Führen Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interaktiv aus. Geben Sie auf der Seite **Installationsziel** ein neues Ziel für die Instanz und die Datenbank von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an.  
  
     – oder –  
  
-   Führen Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an der Eingabeaufforderung aus, und legen Sie fest, dass der Assistent im Antwortdateimodus ausgeführt wird. Weitere Informationen zum Antwortdateimodus finden Sie unter [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     – oder –  
  
-   Ändern Sie die Datei „\<*Projektname*>.deploymenttargets“ mit einem beliebigen Text-Editor.  
  
## Siehe auch  
 [Angeben von Bereitstellungsoptionen für Partitionen und Rollen](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)   
 [Angeben der Konfigurationseinstellungen für die Lösungsbereitstellung](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)   
 [Angeben von Verarbeitungsoptionen](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  