---
title: "Festlegen von Eigenschaften f&#252;r mehrdimensionale Datenbanken (Analysis Services) | Microsoft Docs"
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
  - "Eigenschaften [Analysis Services], Datenbanken"
ms.assetid: a8be5b3f-3148-448a-976c-7222705155d9
caps.latest.revision: 24
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 24
---
# Festlegen von Eigenschaften f&#252;r mehrdimensionale Datenbanken (Analysis Services)
  Es gibt eine Reihe von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankeigenschaften, die Sie im Datenbank-Designer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] konfigurieren können.  
  
 In diesem Designer können Sie die folgenden Aufgaben ausführen:  
  
-   Wenn Sie im Onlinemodus mit der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank verbunden sind, können Sie den Namen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank ändern. Wenn Sie im Projektmodus arbeiten, können Sie den Datenbanknamen für die nächste Bereitstellung des Projekts ändern. Weitere Informationen finden Sie unter [Umbenennen einer mehrdimensionalen Datenbank &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md) und [Konfigurieren von Analysis Services-Projekteigenschaften &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
-   Sie können eine Beschreibung der Datenbank bereitstellen, die den Benutzern angezeigt werden kann. Sie können auch den Namen der Datenbank anzeigen; es ist jedoch nicht möglich, den Namen zu ändern. Zum Ändern des Datenbanknamens müssen Sie die Eigenschaften des Projekts bearbeiten.  
  
-   Sie können Übersetzungen für den Datenbanknamen und eine Beschreibung für eine oder mehrere Sprachen bereitstellen. Weitere Informationen finden Sie unter [Cubeübersetzungen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md), [Dimensionsübersetzungen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md) und [Unterstützung für Übersetzungen in Analysis Services](../../analysis-services/translation-support-in-analysis-services.md).  
  
-   Sie können die standardmäßigen Kontotypzuordnungen anzeigen und bearbeiten. Kontotypzuordnungen werden verwendet, wenn ein oder mehrere Measures die *ByAccount* -Aggregationsfunktion verwenden. Für jeden Kontotyp können Sie einen Alias angeben und die Standardaggregationsfunktion ändern, die dem Kontotyp zugeordnet ist. Weitere Informationen zum Ändern der Standardaggregation finden Sie unter [Semiadditives Verhalten definieren](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md).  
  
## Datenbankeigenschaften  
 Zusätzlich zu den oben genannten gibt es eine Reihe von Datenbankeigenschaften, die Sie im Eigenschaftenfenster konfigurieren können.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|Aggregationspräfix|Das allgemeine Präfix, das für Aggregationsnamen für alle Partitionen in einer Datenbank verwendet werden kann. Weitere Informationen finden Sie unter [AggregationPrefix-Element &#40;ASSL&#41;](../../analysis-services/scripting/properties/aggregationprefix-element-assl.md).|  
|Sortierung|Wenn das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt in einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitgestellt wird, erbt die Datenbank den Wert der Collation-Servereigenschaft, es sei denn, Sie stellen hier einen anderen Wert bereit.|  
|DataSourceImpersonationInfo|Gibt den standardmäßigen Identitätswechselmodus für alle Datenquellenobjekte in der Datenbank an. Es handelt sich hierbei um den Modus, den der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst beim Verarbeiten von Objekten, Synchronisieren von Servern und Ausführen der Data Mining-Anweisungen OpenQuery und SystemOpenSchema verwendet.|  
|Geschätzte Größe|Gibt eine geschätzte Größe der Datenbankdateien auf dem Datenträger an. Wenn Daten an mehreren Orten gespeichert sind, beschränkt sich diese Schätzung auf die Datendateien, die unter dem Datenbankordner gespeichert wurden.<br /><br /> **EstimatedSize** kann auch als Grundlage zum Schätzen des Arbeitsspeichers verwendet werden. Im Vergleich zu der auf dem Datenträger benötigten Datenkapazität liegen die Arbeitsspeicheranforderungen normalerweise höher. Dies liegt an den zusätzlichen Datenstrukturen, die beim Laden der Datenbank in den Arbeitsspeicher erstellt werden.<br /><br /> Um die Arbeitsspeicheranforderungen genauer einzuschätzen, können Sie auch den Task-Manager verwenden. So lässt sich der Analysis Services-Prozessarbeitsspeicher vor und nach der Verarbeitung der Datenbank überprüfen, um die Arbeitsspeichernutzung zu ermitteln und daraus die Arbeitsspeicheranforderungen der Datenbank abzuleiten.|  
|Sprache|Wenn das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt in einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitgestellt wird, erbt die Datenbank den Wert der Language-Servereigenschaft, es sei denn, Sie stellen hier einen anderen Wert bereit.|  
|MasterDataSourceID|Wird zusammen mit Remotepartitionen verwendet. Weitere Informationen finden Sie unter [Remote Partitions](../Topic/Remote%20Partitions.md).|  
  
## Siehe auch  
 [Datenbankeigenschaften &#40;Dialogfeld, SSAS – mehrdimensional&#41;](../Topic/Database%20Properties%20Dialog%20Box%20\(SSAS%20-%20Multidimensional\).md)   
 [Konfigurieren von Analysis Services-Projekteigenschaften &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
  