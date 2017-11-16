---
title: Drillthroughabfragen (Datamining) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AllowDrillThrough property
- drillthrough [Analysis Services]
- drillthrough [DMX]
ms.assetid: 246c784b-1b0c-4f0b-96f7-3af265e67051
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1cb15acfcc31572a34c6bf2fe6c3ec75101a9fd0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drillthrough-queries-data-mining"></a>Drillthroughabfragen (Data Mining)
  Mithilfe einer *Drillthroughabfrage* können Sie Details aus zugrunde liegenden Fällen oder Strukturdaten abrufen, indem Sie eine Anfrage an das Miningmodell senden. Ein Drillthrough ist hilfreich, wenn Sie die Fälle anzeigen möchten, die zum Trainieren des Modells verwendet wurden, und nicht die Fälle, die zum Testen des Modells verwendet wurden, oder wenn Sie zusätzliche Details aus den Falldaten einsehen möchten.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Data Mining stellt zwei verschiedene Drillthroughoptionen bereit:  
  
-   Drillthrough zu den **Fällen im Modell**  
  
     Drillthroughs zu Modellfällen werden ausgeführt, wenn Sie bei einem bestimmten Muster im Modell beginnen – z. B. bei einem Cluster oder einer Verzweigung einer Entscheidungsstruktur – und Details zu den einzelnen Fällen anzeigen möchten.  
  
-   Drillthrough zu den **Fällen in der Struktur**  
  
     Ein Drillthrough zu Strukturfällen wird verwendet, wenn die Struktur Informationen enthält, die im Modell möglicherweise nicht verfügbar sind. Sie würden beispielsweise keine Kundenkontaktdaten in einem Clustermodell verwenden, selbst wenn die Daten in der Struktur enthalten wären. Nachdem Sie das Modell erstellt haben, können Sie jedoch Kontaktinformationen für Kunden abrufen, die in einem bestimmten Cluster gruppiert sind.  
  
 Dieser Abschnitt enthält Beispiele dafür, wie Sie diese Abfragen erstellen können.  
  
 [Verwenden von Drillthrough in Data Mining-Designer](#bkmk_Designer)  
  
 [Erstellen von Drillthroughabfragen mit DMX](#bkmk_DMX)  
  
 [Überlegungen zur Verwendung von Drillthrough](#bkmk_Considerations)  
  
-   [Sicherheitsprobleme](#bkmk_Security)  
  
-   [Einschränkungen](#bkmk_Limits)  
  
##  <a name="bkmk_Designer"></a> Verwenden von Drillthrough in Data Mining-Designer  
 Wenn ein Miningmodell für die Verwendung von Drillthrough konfiguriert wurde, und wenn Sie über die erforderlichen Berechtigungen verfügen, können Sie beim Durchsuchen eines Modells im entsprechenden Viewer auf einen Knoten klicken, und detaillierte Informationen über die Fälle in diesem bestimmten Knoten abrufen.  
  
 [Ausführen von Drillthroughs für Falldaten aus einem Miningmodell](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md).  
  
 Wenn die Trainingsfälle bei der Verarbeitung der Miningstruktur zwischengespeichert wurden und Sie über die erforderlichen Berechtigungen verfügen, können Sie Informationen von den Modellfällen und der Miningstruktur zurückgeben, einschließlich Spalten, die nicht im Miningmodell enthalten sind.  
  
##  <a name="bkmk_DMX"></a> Erstellen von Drillthroughabfragen mit DMX  
 Sie können durch Erstellen einer DMX-Abfrage einen Drillthrough zu Falldaten ausführen, wenn Sie über Berechtigungen für das Modell oder die Struktur verfügen. Beispiele der Syntax zum Erstellen von Drillthroughabfragen in DMX finden Sie im folgenden Thema:  
  
 [Erstellen von Drillthroughabfragen mit DMX](../../analysis-services/data-mining/create-drillthrough-queries-using-dmx.md)  
  
##  <a name="bkmk_Considerations"></a> Überlegungen zur Verwendung von Drillthrough  
  
-   Wenn Sie den Data Mining-Assistenten verwenden, befindet sich die Option zur Aktivierung von Drillthrough für die Modellfälle auf der letzten Seite des Assistenten. Drillthrough ist standardmäßig deaktiviert. Weitere Informationen finden Sie unter [Abschließen des Assistenten &#40;Data Mining-Assistent&#41;](http://msdn.microsoft.com/library/6aef1548-35eb-42fd-ae87-63650a79eda1).  
  
-   Sie können die Drillthroughfähigkeit einem vorhandenen Miningmodell hinzufügen, in diesem Fall muss das Modell jedoch neu verarbeitet werden, bevor Sie einen Drillthrough mit den Daten ausführen.  
  
-   Drillthrough funktioniert, indem Informationen über die Trainingsfälle abgerufen werden, die bei der Verarbeitung der Miningstruktur zwischengespeichert wurden. Wenn Sie alle zwischengespeicherten Daten nach der Verarbeitung der Struktur durch Ändern der <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> -Eigenschaft in **ClearAfterProcessing**gelöscht haben, funktioniert der Drillthrough nicht. Um Drillthrough für Strukturspalten zu aktivieren, müssen Sie die <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> -Eigenschaft in **KeepTrainingCases** ändern und die Struktur erneut verarbeiten.  
  
-   Wenn die Miningstruktur keinen Drillthrough gestattet, jedoch das Miningmodell, können Sie nur Informationen der Modellfälle anzeigen, nicht jedoch der Miningstruktur.  
  
###  <a name="bkmk_Security"></a> Sicherheitsprobleme mit Drillthrough  
 Wenn Sie vom Modell einen Drillthrough zu Strukturfällen ausführen möchten, müssen Sie sicherstellen, dass sowohl für die Miningstruktur als auch für das Miningmodell die [AllowDrillThrough](../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) -Eigenschaft auf **True**festgelegt wurde. Außerdem müssen Sie Mitglied einer Rolle sein, die sowohl für die Struktur als auch für das Modell über Drillthroughberechtigungen verfügt. Informationen zum Erstellen von Rollen finden Sie unter [Rollen-Designer &#40;Analysis Services – Mehrdimensionale Daten&#41;](http://msdn.microsoft.com/library/e8ba42db-0565-4d68-b3ab-0c63d8d07192). Thema  
  
 Drillthroughberechtigungen werden getrennt für die Struktur und das Modell festgelegt. Mit den Modellberechtigungen können Sie einen Drillthrough des Modells durchführen, auch wenn Sie keine Berechtigungen für die Struktur besitzen. Mit Drillthroughberechtigungen für die Struktur können Sie außerdem mit der Funktion [StructureColumn &#40;DMX&#41;](../../dmx/structurecolumn-dmx.md) Strukturspalten in Drillthroughabfragen für das Modell einbeziehen.  
  
> [!NOTE]  
>  Wenn Sie Drillthrough sowohl für die Miningstruktur als auch für das Miningmodell aktivieren, kann jeder Benutzer, der Mitglied einer Rolle mit Drillthroughberechtigungen für das Miningmodell ist, auch Spalten in der Miningstruktur einsehen, selbst wenn diese Spalten nicht Teil des Miningmodells sind. Daher sollten Sie zum Schutz sensibler Daten die Datenquellensicht so einrichten, dass persönliche Informationen verborgen sind, und Drillthroughzugriff auf die Miningstruktur nur zulassen, wenn es wirklich erforderlich ist.  
  
###  <a name="bkmk_Limits"></a> Einschränkungen für Drillthrough  
  
-   Die folgenden Einschränkungen gelten für Drillthroughvorgänge auf einem Modell in Abhängigkeit von dem für die Erstellung des Modells verwendeten Algorithmus:  
  
|Algorithmusname|Problem|  
|--------------------|-----------|  
|Microsoft Naive Bayes-Algorithmus|Nicht unterstützt. Diese Algorithmen weisen bestimmten Knoten im Inhalt keine Fälle zu.|  
|Microsoft Neural Network-Algorithmus|Nicht unterstützt. Diese Algorithmen weisen bestimmten Knoten im Inhalt keine Fälle zu.|  
|Microsoft Logistic Regression-Algorithmus|Nicht unterstützt. Diese Algorithmen weisen bestimmten Knoten im Inhalt keine Fälle zu.|  
|Microsoft Linear Regression-Algorithmus|Unterstützt. Da das Modell jedoch als einzigen Knoten **All**erstellt, gibt Drillthrough alle Trainingsfälle des Modells zurück. Bei einem großen Trainingssatz kann es sehr lange dauern, bis die Ergebnisse geladen werden.|  
|Microsoft Time Series-Algorithmus|Unterstützt. Sie können jedoch keinen Drillthrough mit Struktur- oder Falldaten unter Verwendung des **Miningmodell-Viewers** im Data Mining-Designer ausführen. Sie müssen stattdessen eine DMX-Abfrage erstellen.<br /><br /> Sie können außerdem keinen Drillthrough auf bestimmten Knoten ausführen oder DMX-Abfragen schreiben, um Fälle von bestimmten Knoten eines Zeitreihenmodells abzurufen. Sie können Falldaten entweder aus dem Modell oder aus der Struktur abrufen, indem Sie andere Kriterien verwenden, beispielsweise Datums- oder Attributwerte.<br /><br /> Sie können auch die Datumsangaben der Modellfälle zurückgeben, indem Sie die [Lag &#40;DMX&#41;](../../dmx/lag-dmx.md)-Funktion verwenden.<br /><br /> Wenn Sie Details der vom Microsoft Time Series-Algorithmus erstellten ARTXP- und ARIMA-Knoten anzeigen möchten, können Sie den [Microsoft Generic Content Tree Viewer &#40;Data Mining&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c) verwenden.|  
  
##  <a name="bkmk_Tasks"></a> Verwandte Aufgaben  
 Verwenden Sie die folgenden Links, um in bestimmten Szenarien mit Drillthroughs zu arbeiten.  
  
|Task|Link|  
|----------|----------|  
|Schritte zur Verwendung von Drillthroughs im Data Mining-Designer|[Ausführen von Drillthroughs für Falldaten aus einem Miningmodell](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)|  
|So ändern Sie ein vorhandenes Miningmodell, um Drillthroughs zu ermöglichen|[Aktivieren von Drillthrough für ein Miningmodell](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)|  
|Aktivieren von Drillthroughs für eine Miningstruktur mit der DMX WITH DRILLTHROUGH-Klausel|[CREATE MINING STRUCTURE &#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md)|  
|Weitere Informationen über das Zuweisen von Berechtigungen, die für Drillthroughs in Miningstrukturen und Miningmodellen gelten|[Erteilen von Berechtigungen für Data Mining-Strukturen und -Modellen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Modell-Viewer](../../analysis-services/data-mining/data-mining-model-viewers.md)   
 [Data Mining-Abfrage](../../analysis-services/data-mining/data-mining-queries.md)  
  
  

