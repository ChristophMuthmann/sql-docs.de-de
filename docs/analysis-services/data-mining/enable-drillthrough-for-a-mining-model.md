---
title: "Aktivieren von Drillthrough f&#252;r ein Miningmodell | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Data Mining [Analysis Services], Themen zur Vorgehensweise"
  - "Drillthrough [Analysis Services]"
ms.assetid: 4fa44f60-ef9a-4b59-98c0-c0baf1195c8e
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 28
---
# Aktivieren von Drillthrough f&#252;r ein Miningmodell
  Wenn Sie Drillthrough für ein Miningmodell aktiviert haben, können Sie beim Durchsuchen des Modells detaillierte Informationen über die Fälle abrufen, die für die Erstellung des Modells verwendet wurden. Zum Anzeigen dieser Informationen benötigen Sie die erforderlichen Berechtigungen. Außerdem muss die Struktur bereits verarbeitet worden sein.  
  
 **Berechtigungen:** Damit ein Benutzer einen Drillthrough in Modell- oder Strukturdaten ausführen kann, muss er Mitglied einer Rolle sein, die über [AllowDrillThrough](../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) -Berechtigungen für das Miningmodell oder die Miningstruktur verfügt. Drillthroughberechtigungen werden getrennt für die Struktur und das Modell festgelegt.  
  
-   Mit Drillthrough-Berechtigungen für das Modell können Sie einen Drillthrough des Modells durchführen, auch wenn Sie keine Berechtigungen für die Struktur besitzen.  
  
-   Mit Drillthroughberechtigungen für die Struktur können Sie außerdem mit der Funktion [StructureColumn &#40;DMX&#41;](../../dmx/structurecolumn-dmx.md) Strukturspalten in Drillthroughabfragen für das Modell einbeziehen. Außerdem können Sie mit der SELECT… FROM <structure>.CASES-Syntax die Trainings- und Testfälle in der Struktur abfragen.  
  
 **Zwischenspeichern von Trainingsfällen:** Beim Drillthrough werden Informationen über die Trainingsfälle in der Miningstruktur abgerufen. Diese Informationen werden zwischengespeichert, wenn die Struktur verarbeitet wird. Wenn Sie alle zwischengespeicherten Daten durch Ändern der <xref:Microsoft.AnalysisServices.MiningStructureCacheMode>-Eigenschaft in **ClearAfterProcessing** löschen, funktioniert der Drillthrough nicht.  
  
> [!NOTE]  
>  Wenn die Trainingsfälle nicht zwischengespeichert wurden, müssen Sie die <xref:Microsoft.AnalysisServices.MiningStructureCacheMode>-Eigenschaft in **KeepTrainingCases** ändern und das Modell anschließend erneut verarbeiten, bevor Sie die Falldaten anzeigen können.  
  
 Weitere Informationen finden Sie unter [Drillthroughabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
### So aktivieren Sie Drillthrough für ein Miningmodell  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Data Mining-Designer auf der Registerkarte **Miningmodelle** mit der rechten Maustaste auf den Namen des Miningmodells, für das Sie Drillthrough aktivieren möchten, und wählen Sie anschließend **Eigenschaften** aus.  
  
2.  Klicken Sie im Fenster **Eigenschaften** auf **AllowDrillthrough**, und wählen Sie **True**aus.  
  
3.  Klicken Sie auf der Registerkarte **Miningmodelle** mit der rechten Maustaste auf das Modell, und wählen Sie **Modell verarbeiten** aus.  
  
### So aktivieren Sie das Zwischenspeichern für eine Miningstruktur  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Data Mining-Designer auf der Registerkarte **Miningstruktur** mit der rechten Maustaste auf den Namen der Miningstruktur.  
  
2.  Öffnen Sie das Fenster **Eigenschaften** .  
  
3.  Suchen Sie im Fenster **Eigenschaften** die **CacheMode** -Eigenschaft, und wählen Sie dann **KeepTrainingCases** in der Liste aus.  
  
4.  Aktivieren Sie im Menü **Datenbank** die Option **Verarbeiten**.  
  
## Siehe auch  
 [Drillthroughabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
  