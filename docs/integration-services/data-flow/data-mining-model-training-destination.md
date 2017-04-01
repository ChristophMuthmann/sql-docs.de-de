---
title: "Ziel des Data Mining-Modelltrainings | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dataminingmodeltrainingdest.f1"
helpviewer_keywords: 
  - "Ziele [Integration Services], Data Mining-Modelltraining"
  - "Ziel des Data Mining-Modelltrainings"
  - "Miningmodelle [Analysis Services], Trainieren"
  - "Trainieren von Miningmodellen"
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# Ziel des Data Mining-Modelltrainings
  Das Ziel des Data Mining-Modelltrainings trainiert Data Mining-Modelle, indem die Daten, die vom Ziel empfangen werden, über Data Mining-Modellalgorithmen übergeben werden. Mehrere Data Mining-Modelle können von einem Ziel trainiert werden, falls die Modelle mit der gleichen Data Mining-Struktur erstellt wurden. Weitere Informationen finden Sie unter [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md) und [Mining Model Columns](../../analysis-services/data-mining/mining-model-columns.md).  
  
## Konfiguration des Ziels des Data Mining-Modelltrainings  
 Wenn eine Spalte auf Fallebene der Zielstruktur und die Modelle, die mit der Struktur erstellt wurden, den Inhaltstyp KEY TIME oder KEY SEQUENCE aufweisen, müssen die Eingabedaten nach dieser Spalte sortiert werden. Beispielsweise verwenden Modelle, die mit dem Microsoft Time Series-Algorithmus erstellt wurden, den KEY TIME-Inhaltstyp. Falls Eingabedaten nicht sortiert sind, wird beim Verarbeiten des Modells möglicherweise ein Fehler gemeldet. Falls die Daten sortiert werden müssen, können sie mithilfe einer Transformation zum Sortieren in einer früheren Phase des Datenflusses sortiert werden. Diese Anforderung gilt nicht für Spalten mit dem KEY-Inhaltstyp. Weitere Informationen finden Sie unter [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md) und [Transformation zum Sortieren](../../integration-services/data-flow/transformations/sort-transformation.md).  
  
> [!NOTE]  
>  Die Eingabe des Zieles für das Data Mining-Modelltraining muss sortiert werden. Zum Sortieren der Daten können Sie ein Upstreamsortierungsziel aus dem Ziel des Data Mining-Modelltrainings in den Datenfluss einschließen. Weitere Informationen finden Sie unter [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md).  
  
 Dieses Ziel weist eine Eingabe und keine Ausgabe auf.  
  
 Das Ziel des Data Mining-Modelltrainings stellt mithilfe eines Verbindungs-Managers für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Verbindung mit dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt oder der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] her, die die Miningstruktur und die Miningmodelle enthält, die vom Ziel trainiert werden. Weitere Informationen finden Sie unter [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Trainings-Editor für Data Mining-Modelle** festlegen können:  
  
-   [Trainings-Editor für Data Mining-Modelle &#40;Registerkarte Verbindung&#41;](../../integration-services/data-flow/data-mining-model-training-editor-connection-tab.md)  
  
-   [Trainings-Editor für Data Mining-Modelle &#40;Registerkarte Spalten&#41;](../../integration-services/data-flow/data-mining-model-training-editor-columns-tab.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften des Ziels des Data Mining-Modelltrainings](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  