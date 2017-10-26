---
title: Data Mining Model Training Destination | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataminingmodeltrainingdest.f1
- sql13.dts.designer.dmmtrainingtransformation.connection.f1
- sql13.dts.designer.dmmtrainingtransformation.columns.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 570a7e8c6b20ea528f5980fb3ae53a60037d0243
ms.contentlocale: de-de
ms.lasthandoff: 08/17/2017

---
# <a name="data-mining-model-training-destination"></a>Ziel des Data Mining-Modelltrainings
  Das Ziel des Data Mining-Modelltrainings trainiert Data Mining-Modelle, indem die Daten, die vom Ziel empfangen werden, über Data Mining-Modellalgorithmen übergeben werden. Mehrere Data Mining-Modelle können von einem Ziel trainiert werden, falls die Modelle mit der gleichen Data Mining-Struktur erstellt wurden. Weitere Informationen finden Sie unter [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md) und [Mining Model Columns](../../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>Konfiguration des Ziels des Data Mining-Modelltrainings  
 Wenn eine Spalte auf Fallebene der Zielstruktur und die Modelle, die mit der Struktur erstellt wurden, den Inhaltstyp KEY TIME oder KEY SEQUENCE aufweisen, müssen die Eingabedaten nach dieser Spalte sortiert werden. Beispielsweise verwenden Modelle, die mit dem Microsoft Time Series-Algorithmus erstellt wurden, den KEY TIME-Inhaltstyp. Falls Eingabedaten nicht sortiert sind, wird beim Verarbeiten des Modells möglicherweise ein Fehler gemeldet. Falls die Daten sortiert werden müssen, können sie mithilfe einer Transformation zum Sortieren in einer früheren Phase des Datenflusses sortiert werden. Diese Anforderung gilt nicht für Spalten mit dem KEY-Inhaltstyp. Weitere Informationen finden Sie unter [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md) und [Transformation zum Sortieren](../../integration-services/data-flow/transformations/sort-transformation.md).  
  
> [!NOTE]  
>  Die Eingabe des Zieles für das Data Mining-Modelltraining muss sortiert werden. Zum Sortieren der Daten können Sie ein Upstreamsortierungsziel aus dem Ziel des Data Mining-Modelltrainings in den Datenfluss einschließen. Weitere Informationen finden Sie unter [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md).  
  
 Dieses Ziel weist eine Eingabe und keine Ausgabe auf.  
  
 Das Ziel des Data Mining-Modelltrainings stellt mithilfe eines Verbindungs-Managers für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Verbindung mit dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt oder der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] her, die die Miningstruktur und die Miningmodelle enthält, die vom Ziel trainiert werden. Weitere Informationen finden Sie unter [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften des Ziels des Data Mining-Modelltrainings](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="data-mining-model-training-editor-connection-tab"></a>Trainings-Editor für Data Mining-Modelle (Registerkarte Verbindung)
  Wählen Sie auf der Seite **Verbindung** des Dialogfelds **Trainings-Editor für Data Mining-Modelle** ein Mining-Modell zum Trainieren aus.  
  
### <a name="options"></a>enthalten  
 **Verbindungs-Manager**  
 Wählen Sie eine Verbindung aus der Liste der vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verbindungen aus, oder erstellen Sie wie im Folgenden beschrieben über die Schaltfläche [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Neu **eine neue** -Verbindung.  
  
 **eine neue**  
 Erstellen Sie mithilfe des Dialogfelds **Analysis Services-Verbindungs-Manager hinzufügen** eine neue Verbindung.  
  
 **Miningstruktur**  
 Wählen Sie eine Struktur aus der Liste der verfügbaren Miningstrukturen, oder erstellen Sie durch Klicken auf **Neu**eine neue Struktur.  
  
 **eine neue**  
 Erstellen Sie mithilfe von **Data Mining-Assistent**eine neue Miningstruktur und ein Miningmodell.  
  
 **Miningmodelle**  
 Zeigt die Liste der mit der ausgewählten Miningstruktur verknüpften Miningmodelle an.  
  
## <a name="data-mining-model-training-editor-columns-tab"></a>Trainings-Editor für Data Mining-Modelle (Registerkarte Spalten)
  Mithilfe der Seite **Spalten** des Dialogfelds **Trainings-Editor für Data Mining-Modelle** können Sie Eingabespalten Spalten in der Miningstruktur zuordnen.  
  
## <a name="options"></a>enthalten  
 **Verfügbare Eingabespalten**  
 Zeigt die Liste der verfügbaren Eingabespalten an. Ziehen Sie Eingabespalten, um sie Miningstrukturspalten zuzuordnen.  
  
 **Miningstrukturspalten**  
 Zeigt die Liste der Miningstrukturspalten an. Ziehen Sie Miningstrukturspalten, um sie verfügbaren Eingabespalten zuzuordnen.  
  
 **Eingabespalte**  
 Zeigen Sie die in obiger Tabelle ausgewählten Eingabespalten an. Verwenden Sie zum Ändern oder Entfernen einer Zuordnungsauswahl die Liste **Verfügbare Eingabespalten**.  
  
 **Miningstrukturspalten**  
 Zeigt alle verfügbaren Zielspalten an, und ob sie zugeordnet sind.  
  

