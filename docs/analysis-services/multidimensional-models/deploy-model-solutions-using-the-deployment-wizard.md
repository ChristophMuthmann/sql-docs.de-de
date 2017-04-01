---
title: "Bereitstellen von Modelll&#246;sungen mithilfe des Bereitstellungs-Assistenten | Microsoft Docs"
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
  - "Bereitstellungs-Assistent für Analysis Services"
  - "Bereitstellen [Analysis Services], Bereitstellungs-Assistent für Analysis Services"
  - "Analysis Services-Bereitstellungen, Bereitstellungs-Assistent für Analysis Services"
  - "Bereitstellungs-Assistent für Analysis Services, Informationen zum Bereitstellungs-Assistenten für Analysis Services"
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
caps.latest.revision: 39
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 37
---
# Bereitstellen von Modelll&#246;sungen mithilfe des Bereitstellungs-Assistenten
  Der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet die von einem Projekt in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] generierten XML-Ausgabedateien als Eingabedateien. Diese Eingabedateien können problemlos geändert werden, um die Bereitstellung eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts anzupassen. Anschließend kann das generierte Bereitstellungsskript entweder sofort ausgeführt oder für eine spätere Bereitstellung gespeichert werden.  
  
 Sie können die Bereitstellung mithilfe des Assistenten wie hier beschrieben durchführen. Sie können die Bereitstellung auch automatisieren oder die Synchronisierungsfunktion verwenden. Wenn die bereitgestellte Datenbank groß ist, sollten Sie die Verwendung von Partitionen auf den Zielsystemen in Erwägung ziehen. Mithilfe von Analysis Management Objects \(AMO\) können Sie auch die Partitionserstellung und -auffüllung automatisieren.  
  
> [!IMPORTANT]  
>  Weder die XML-Ausgabedateien noch das Bereitstellungsskript enthalten die Benutzer-ID oder das Kennwort, wenn diese in der Verbindungszeichenfolge für eine Datenquelle oder für Identitätswechsel angegeben sind. Da diese Informationen zum Verarbeiten in diesem Szenario erforderlich sind, müssen Sie sie manuell hinzufügen. Wenn die Bereitstellung keine Verarbeitung umfasst, können Sie die Verbindungs- und Identitätswechselinformationen bei Bedarf nach der Bereitstellung hinzufügen. Wenn die Bereitstellung die Verarbeitung umfasst, können Sie diese Informationen nach dem Speichern entweder innerhalb des Assistenten oder im Bereitstellungsskript hinzufügen.  
  
## In diesem Abschnitt  
 In den folgenden Themen wird beschrieben, wie Sie mit dem Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , den Eingabedateien und dem Bereitstellungsskript arbeiten:  
  
|Thema|Description|  
|-----------|-----------------|  
|[Ausführen des Bereitstellungs-Assistenten für Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)|Beschreibt die verschiedenen Möglichkeiten zum Ausführen des Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)|Beschreibt, welche Dateien der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] als Eingabewerte verwendet und was jede dieser Dateien enthält. Stellt außerdem Links zu Themen bereit, in denen beschrieben wird, wie Sie die Werte in den einzelnen Eingabedateien ändern können.|  
|[Grundlegendes zum Analysis Services-Bereitstellungsskript](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)|Beschreibt den Inhalt des Bereitstellungsskripts und wie das Skript ausgeführt wird.|  
  
## Siehe auch  
 [Bereitstellen von Modelllösungen mit XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [Synchronisieren von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)   
 [Bereitstellen von Modelllösungen mit dem Bereitstellungshilfsprogramm](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  