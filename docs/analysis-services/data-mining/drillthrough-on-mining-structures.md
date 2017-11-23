---
title: Drillthrough in Miningstrukturen | Microsoft Docs
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
ms.assetid: a0b00a3b-f9db-4289-a8cb-ddf600cd64ac
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cfbedd4235f4409df31912df360cf192725f36e5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="drillthrough-on-mining-structures"></a>Drillthrough in Miningstrukturen
  *Drillthrough* beschreibt die Fähigkeit, entweder ein Miningmodell oder eine Miningstruktur abzufragen und ausführliche Daten zu erhalten, die im Modell nicht verfügbar sind.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] bietet zwei verschiedene Optionen für Drillthroughs in Falldaten. Sie können einen Drillthrough zu den Daten ausführen, die für die Erstellung des Miningmodells verwendet wurden, oder Sie führen einen Drillthrough zu den Quelldaten in der Miningstruktur aus.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>Drillthrough zu Modellfällen im Vergleich zu Drillthrough zu Strukturen  
 Ein Drillthrough zu **Modellfällen** ist hilfreich für die Suche nach weiteren Details zu Regeln, Mustern oder Clustern in einem Modell.  
  
 Demgegenüber soll ein **Drillthrough in Bezug auf Strukturdaten** einen Zugriff auf Informationen ermöglichen, die im Modell nicht verfügbar waren. Wenn Sie zum Beispiel über die entsprechenden Berechtigungen verfügen, möchten Sie unter Umständen feststellen, welche Datenzeilen für das Training des Modells und welche für Tests verwendet wurden.  
  
 Sie können auch Attribute der Daten anzeigen, die in der Analyse nicht verwendet wurden, vorausgesetzt, sie wurden in die Strukturdefinition eingeschlossen. Beispiel: Oftmals unterstützen Miningstrukturen zahlreiche andere Arten von Modellen, und einige Strukturspalten wurden möglicherweise aus einem Modell ausgeschlossen, da der Datentyp nicht kompatibel war oder da die Daten nicht für Analysen geeignet waren. Zum Beispiel würden Sie keine Kundenkontaktinformationen in einem Clusteringmodell verwenden, auch wenn die Daten in die Struktur eingeschlossen wurden. Durch das Aktivieren des Drillthroughs erhalten Sie jedoch Zugang zu diesen Informationen, ohne gesonderte Abfragen der Datenquelle ausführen zu müssen.  
  
## <a name="enabling-drillthrough-to-structure-data"></a>Aktivieren von Drillthroughs zu Strukturdaten  
 Um Drillthroughvorgänge in der Miningstruktur verwenden zu können, müssen die folgenden Bedingungen erfüllt werden:  
  
-   Drillthrough für das Modell muss ebenfalls aktiviert werden. Standardmäßig werden beide Formen des Drillthroughs deaktiviert. Um Drillthrough im Data Mining-Assistenten zu aktivieren, wählen Sie die Option aus, um Drillthrough zu Modellfällen auf der letzten Seite des Assistenten zu aktivieren. Sie können die Option für Drillthroughvorgänge für ein Modell auch später durch Ändern der **AllowDrillthrough** -Eigenschaft hinzufügen.  
  
-   Wenn Sie die Miningstruktur mit DMX erstellen, verwenden Sie die WITH DRILLTHROUGH-Klausel. Weitere Informationen finden Sie unter [CREATE MINING STRUCTURE &#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md).  
  
-   Drillthrough funktioniert, indem Informationen über die Trainingsfälle abgerufen werden, die bei der Verarbeitung der Miningstruktur zwischengespeichert wurden. Wenn Sie alle zwischengespeicherten Daten nach der Verarbeitung der Struktur durch Ändern der <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> -Eigenschaft in **ClearAfterProcessing**gelöscht haben, funktioniert der Drillthrough nicht. Um Drillthrough für Strukturspalten zu aktivieren, müssen Sie die <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> -Eigenschaft in **KeepTrainingCases** ändern und die Struktur erneut verarbeiten.  
  
-   Überprüfen Sie, ob sowohl für die Miningstruktur als auch für das Miningmodell der [AllowDrillThrough](../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) -Eigenschaftensatz auf **True**festgelegt wurde. Außerdem müssen Sie Mitglied einer Rolle sein, die sowohl für die Struktur als auch für das Modell über Drillthroughberechtigungen verfügt.  
  
## <a name="security-issues-for-drillthrough"></a>Sicherheitsprobleme mit Drillthrough  
 Drillthroughberechtigungen werden getrennt für die Struktur und das Modell festgelegt. Mit den Modellberechtigungen können Sie einen Drillthrough des Modells durchführen, auch wenn Sie keine Berechtigungen für die Struktur besitzen. Mit Drillthroughberechtigungen für die Struktur können Sie außerdem mit der Funktion [StructureColumn &#40;DMX&#41;](../../dmx/structurecolumn-dmx.md) Strukturspalten in Drillthroughabfragen für das Modell einbeziehen.  
  
 Informationen zum Erstellen von Rollen und zum Zuweisen von Berechtigungen in Analysis Services finden Sie unter [Rollen-Designer &#40;Analysis Services – Mehrdimensionale Daten&#41;](http://msdn.microsoft.com/library/e8ba42db-0565-4d68-b3ab-0c63d8d07192).  
  
> [!NOTE]  
>  Wenn Sie Drillthrough sowohl für die Miningstruktur als auch für das Miningmodell aktivieren, kann jeder Benutzer, der Mitglied einer Rolle mit Drillthroughberechtigungen für das Miningmodell ist, auch Spalten in der Miningstruktur einsehen, selbst wenn diese Spalten nicht Teil des Miningmodells sind. Daher sollten Sie zum Schutz sensibler Daten die Datenquellensicht so einrichten, dass persönliche Informationen verborgen sind, und Drillthroughzugriff auf die Miningstruktur nur zulassen, wenn es wirklich erforderlich ist.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 In den folgenden Themen finden Sie weitere Informationen zur Verwendung von Drillthroughs mit Miningmodellen.  
  
|||  
|-|-|  
|Verwenden von Drillthrough zu Struktur von den Miningmodell-Viewern|[Verwenden von Drillthrough mit den Modell-Viewern](../../analysis-services/data-mining/use-drillthrough-from-the-model-viewers.md)|  
|In Beispielen von Drillthroughabfragen finden Sie Informationen zu bestimmten Modelltypen.|[Data Mining-Abfrage](../../analysis-services/data-mining/data-mining-queries.md)|  
|Informationen über Berechtigungen, die für bestimmte Miningstrukturen und Miningmodelle gelten.|[Erteilen von Berechtigungen für Data Mining-Strukturen und -Modellen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodell-Drillthrough](../../analysis-services/data-mining/drillthrough-on-mining-models.md)  
  
  
