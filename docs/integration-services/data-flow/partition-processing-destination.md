---
title: "Ziel f&#252;r Partitionsverarbeitung | Microsoft Docs"
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
  - "sql13.dts.designer.partitionprocessingdest.f1"
helpviewer_keywords: 
  - "Partitionen [Analysis Services], verarbeiten"
  - "Ziel für Partitionsverarbeitung [Integration Services]"
  - "Ziel [Integration Services], Partitionsverarbeitung"
ms.assetid: 36c592ff-3f78-4a58-b496-31c1c8eee131
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Ziel f&#252;r Partitionsverarbeitung
  Das Ziel für Partitionsverarbeitung lädt und verarbeitet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Partition. Weitere Informationen zu Partitionen finden Sie unter [Partitionen &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md).  
  
 Das Ziel für Partitionsverarbeitung schließt die folgenden Funktionen ein:  
  
-   Optionen für die inkrementelle Verarbeitung, vollständige Verarbeitung oder Updateverarbeitung.  
  
-   Fehlerkonfiguration, um anzugeben, ob die Verarbeitung Fehler ignoriert oder nach einer bestimmten Anzahl von Fehlern beendet wird.  
  
-   Zuordnung von Eingabespalten zu Partitionsspalten.  
  
 Weitere Informationen zum Verarbeiten von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Objekten finden Sie unter [Verarbeitungsoptionen und -einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
> [!NOTE]  
>  Hier beschriebene Tasks gelten nicht für tabellarische Analysis Services-Modelle.  Sie können Partitionsspalten für tabellarische Modelle keine Eingabespalten zuordnen. Sie können stattdessen den Analysis Services-Task "DDL ausführen" [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) verwenden, um die Partition zu verarbeiten.  
  
## Konfiguration des Ziels für die Partitionsverarbeitung  
 Das Ziel für Partitionsverarbeitung stellt mithilfe eines Verbindungs-Managers für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Verbindung mit dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt oder der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] her, die die vom Ziel verarbeiteten Cubes und Partitionen enthält. Weitere Informationen finden Sie unter [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Das Ziel weist eine Eingabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Ziel-Editor für Partitionsverarbeitung** festlegen können:  
  
-   [Ziel-Editor für Partitionsverarbeitung &#40;Seite Verbindungs-Manager&#41;](../../integration-services/data-flow/partition-processing-destination-editor-connection-manager-page.md)  
  
-   [Ziel-Editor für Partitionsverarbeitung &#40;Seite Zuordnungen&#41;](../../integration-services/data-flow/partition-processing-destination-editor-mappings-page.md)  
  
-   [Ziel-Editor für Partitionsverarbeitung &#40;Seite Erweitert&#41;](../../integration-services/data-flow/partition-processing-destination-editor-advanced-page.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften des Ziels für Partitionsverarbeitung](../../integration-services/data-flow/partition-processing-destination-custom-properties.md)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  