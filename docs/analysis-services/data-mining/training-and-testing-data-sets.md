---
title: Trainings- und Testdatasets | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- testing mining models
- holdout [data mining]
- testing data mining models
- accuracy testing [data mining]
ms.assetid: 5798fa48-ef3c-4e97-a17c-38274970fccd
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9465d0eda4b15827cf20c4b9579a5eff672ce1d1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="training-and-testing-data-sets"></a>Trainings- und Testdatasets
  Das Aufteilen von Daten in Trainings- und Testsätze ist ein wichtiger Bestandteil der Auswertung von Data Mining-Modellen. Wenn Sie ein Dataset in einen Trainings- und einen Testsatz unterteilen, wird der Großteil der Daten in der Regel für das Training und die restlichen Daten zum Testen verwendet. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] prüft die Daten nach dem Zufallsprinzip, um sicherzustellen, dass sich die Test- und Trainingssets ähneln. Durch die Verwendung der gleichen Daten für das Training und das Testen können Sie mögliche Datendiskrepanzen weitgehend ausschließen und die Eigenschaften des Modells leichter verstehen.  
  
 Nachdem ein Modell durch die Verwendung des Trainingssatzes bearbeitet wurde, können Sie das Modell testen, indem Sie Vorhersagen für den Testsatz erstellen. Da die Daten im Testsatz bereits bekannte Werte für das Attribut enthalten, das Sie vorhersagen möchten, ist es einfach, die Vorhersagegenauigkeit des Modells zu bestimmen.  
  
## <a name="creating-test-and-training-sets-for-data-mining-structures"></a>Erstellen von Test- und Trainingsets für Data Mining-Strukturen  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]wird das ursprüngliche Dataset auf der Ebene der Miningstruktur unterteilt. Die Informationen zur Größe des Trainings- und Testdatasets bzw. welche Zeile zu welchem Satz gehört, wird mit der Struktur gespeichert. Alle auf dieser Struktur basierenden Modelle können die Sätze für Trainings- und Testzwecke verwenden.  
  
 Testdatasets für eine Miningstruktur können auf folgende Weisen definiert werden:  
  
-   Verwenden Sie den Data Mining-Assistenten, um die Miningstruktur bei der Erstellung zu unterteilen.  
  
-   Ändern Sie die Struktureigenschaften auf der Registerkarte **Miningstruktur** des Data Mining-Designers.  
  
-   Erstellen und ändern Sie die Strukturen programmgesteuert mithilfe von Analysis Management Objects (AMO) oder der XML-Datendefinitionssprache (DDL).  
  
### <a name="using-the-data-mining-wizard-to-divide-a-mining-structure"></a>Verwenden des Data Mining-Assistenten zur Unterteilung einer Miningstruktur  
 Nachdem Sie die Datenquellen für eine Miningstruktur definiert haben, unterteilt der Data Mining-Assistent die Daten standardmäßig in zwei Sätze: einen mit 70 Prozent der Quelldaten zum Trainieren des Modells und einen zweiten mit 30 Prozent der Quelldaten zum Testen des Modells. Dieses Standardverhältnis wurde ausgewählt, weil das 70:30-Verhältnis beim Data Mining häufig verwendet wird. Mithilfe von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] können Sie dieses Verhältnis jedoch entsprechend Ihren Anforderungen ändern.  
  
 Sie können den Assistenten auch so konfigurieren, dass eine maximale Anzahl von Trainingsfällen festgelegt wird, oder Sie können die Grenzwerte kombinieren, um einen maximalen Prozentsatz von Fällen bis zu einer festgelegten maximalen Anzahl von Fällen zuzulassen. Wenn Sie sowohl einen maximalen Prozentsatz von Fällen als auch eine maximale Anzahl von Fällen festlegen, verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] den kleineren der beiden Grenzwerte für die Größe des Testsatzes. Wenn Sie beispielsweise für die Testfälle 30 Prozent zurückgehaltene Daten festlegen und für die maximale Anzahl der Testfälle 1000, wird die Größe des Testsatzes niemals 1000 Fälle überschreiten. Dies kann hilfreich sein, wenn Sie sicherstellen möchten, dass die Größe Ihres Testsatzes konsistent bleibt, selbst wenn dem Modell weitere Trainingsdaten hinzugefügt werden.  
  
 Wenn Sie dieselbe Datenquellensicht für unterschiedliche Miningstrukturen verwenden und sicherstellen möchten, dass die Daten für alle Miningstrukturen und ihre Modelle weitestgehend auf die gleiche Weise unterteilt werden, sollten Sie den Ausgangswert festlegen, der für die Initialisierung der zufälligen Stichprobe verwendet wird. Wenn Sie einen Wert für **HoldoutSeed**angeben, verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diesen Wert für den Beginn der Stichprobe. Andernfalls verwendet die Stichprobe einen Hashalgorithmus auf den Namen der Miningstruktur, um den Ausgangswert zu erstellen.  
  
> [!NOTE]  
>  Wenn Sie mithilfe der **EXPORT** -Anweisung und der **IMPORT** -Anweisung eine Kopie der Miningstruktur erstellen, besitzt die neue Miningstruktur die gleichen Trainings- und Testdatasets, weil durch den Exportvorgang eine neue ID erstellt wird, die den gleichen Namen verwendet. Wenn jedoch zwei Miningstrukturen dieselbe zugrunde liegende Datenquelle verwenden, aber unterschiedliche Namen besitzen, sind die Sätze, die für jede Miningstruktur erstellt werden, unterschiedlich.  
  
### <a name="modifying-structure-properties-to-create-a-test-data-set"></a>Ändern von Struktureigenschaften zum Erstellen eines Testdatasets  
 Wenn Sie eine Miningstruktur erstellen und verarbeiten und zu einem späteren Zeitpunkt ein Testdataset separieren möchten, können Sie die Eigenschaften der Miningstruktur ändern. Um die Methode zu ändern, mit der die Daten partitioniert werden, bearbeiten Sie die folgenden Eigenschaften:  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**HoldoutMaxCases**|Gibt die maximale Anzahl der Fälle an, die in dem Testsatz enthalten sein soll.|  
|**HoldoutMaxPercent**|Gibt die Anzahl der Fälle, die in dem Testsatz enthalten sein soll, als Prozentsatz des gesamten Datasets an. Um kein Dataset zu verwenden, geben Sie 0 an.|  
|**HoldoutSeed**|Gibt einen ganzzahligen Wert an, der als Ausgangswert für die stichprobenartige Auswahl der Daten für die Partition verwendet werden soll. Dieser Wert hat keinen Einfluss auf die Anzahl der Fälle in dem Trainingssatz, er stellt lediglich sicher, dass die Partition wiederholt werden kann.|  
  
 Wenn Sie einer vorhandenen Struktur ein Testdataset hinzufügen bzw. ein vorhandenes Testdataset ändern, müssen Sie die Struktur und alle zugeordneten Modelle neu verarbeiten. Da das Unterteilen der Quelldaten dazu führt, dass das Modell mit einer anderen Teilmenge der Daten trainiert wird, liefert das Modell möglicherweise unterschiedliche Ergebnisse.  
  
### <a name="specifying-holdout-programmatically"></a>Programmgesteuertes Festlegen zurückgehaltener Daten  
 Test- und Trainingsdatasets für eine Miningstruktur können mithilfe von DMX-Anweisungen, AMO oder XML DDL definiert werden. Die ALTER MINING STRUCTURE-Anweisung unterstützt nicht die Verwendung von Zurückhaltungsparametern.  
  
-   **DMX** In der Sprache Data Mining-Erweiterungen (Data Mining Extensions, DMX) wurde die CREATE MINING STRUCTURE-Anweisung um eine WITH HOLDOUT-Klausel erweitert.  
  
-   **ASSL** Sie können entweder eine neue Miningstruktur erstellen oder einer vorhandenen Miningstruktur mithilfe von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ASSL (Analysis Services Scripting Language) ein Testdataset hinzufügen.  
  
-   **AMO** Sie können mithilfe von AMO auch zurückgehaltene Datasets anzeigen und ändern.  
  
 Sie können Informationen über zurückgehaltene Datasets in einer bestehenden Miningstruktur anzeigen. Dazu wird das Data Mining-Schemarowset abgefragt. Führen Sie hierzu einen DISCOVER ROWSET-Aufruf aus, oder verwenden Sie eine DMX-Abfrage.  
  
## <a name="retrieving-information-about-holdout-data"></a>Abrufen von Informationen über zurückgehaltene Daten  
 Alle Informationen über die Trainings- und Testdatasets werden standardmäßig zwischengespeichert, damit Sie zum Trainieren und anschließenden Testen neuer Modelle vorhandener Daten verwenden können. Sie können auch Filter festlegen, die auf die zwischengespeicherten zurückgehaltenen Daten angewendet werden, um so das Modell anhand von Datenteilmengen auszuwerten.  
  
 Die Art und Weise, wie Fälle in Trainings- und Testdatasets unterteilt werden, hängt davon ab, wie Sie die Zurückhaltung von Daten konfigurieren und welche Daten Sie angeben. Wenn Sie die Anzahl der Fälle festlegen möchten, die zum Trainieren oder Testen verwendet werden, oder wenn Sie zusätzliche Details zu den Fällen in den Trainings- und Testsätzen erhalten möchten, können Sie die Modellstruktur abfragen, indem Sie eine DMX-Abfrage erstellen. Die folgende Abfrage gibt beispielsweise die Fälle zurück, die im Trainingssatz des Modells verwendet wurden.  
  
```  
SELECT * from <structure>.CASES WHERE IsTrainingCase()  
```  
  
 Verwenden Sie die folgende Syntax, um nur die Testfälle abzurufen und um die Testfälle außerdem nach einer der Spalten in der Miningstruktur zu filtern:  
  
```  
SELECT * from <structure>.CASES WHERE IsTestCase() AND <structure column name> = '<value>'  
```  
  
## <a name="limitations-on-the-use-of-holdout-data"></a>Einschränkungen bei der Verwendung zurückgehaltener Daten  
  
-   Um zurückgehaltene Daten verwenden zu können, muss für die <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> -Eigenschaft der Miningstruktur der Standardwert **KeepTrainingCases**festgelegt werden. Wenn Sie die **CacheMode** -Eigenschaft zu **ClearAfterProcessing**ändern und die Miningstruktur anschließend neu verarbeiten, geht die Partition verloren.  
  
-   Aus einem Zeitreihenmodell können keine Daten entfernt werden; deshalb ist es nicht möglich, Quelldaten in Trainings- und Testsätze zu unterteilen. Wenn Sie mit der Erstellung einer Miningstruktur und eines Modells beginnen und den [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Time Series-Algorithmus auswählen, wird die Option zum Erstellen eines zurückgehaltenen Datasets deaktiviert. Die Verwendung zurückgehaltener Daten ist ebenfalls deaktiviert, wenn die Miningstruktur auf der Fallebene oder auf der Ebene geschachtelter Tabellen eine KEY TIME-Spalte enthält.  
  
-   Manchmal wird das zurückgehaltene Dataset auch versehentlich erstellt. In diesem Fall wird das gesamte Dataset für Tests verwendet, und es bleiben keine Daten für Trainingszwecke übrig. Sollte dies passieren, gibt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] jedoch eine Fehlermeldung aus, und Sie können das Problem beheben. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] außerdem eine Warnung aus, wenn mehr als 50 Prozent der Daten für Testzwecke zurückgehalten wurden.  
  
-   In den meisten Fällen stellt der Wert von 30 Prozent für zurückgehaltene Daten ein gutes Gleichgewicht zwischen Trainings- und Testdaten dar. Es lässt sich schwer sagen, wie groß das Dataset sein soll, um ein ausreichendes Training zu gewährleisten, oder wie gering die Dichte des Trainingssatzes sein und trotzdem eine Überanpassung vermieden werden kann. Nach der Erstellung eines Modells können Sie jedoch eine Kreuzvalidierung durchführen, um das Dataset im Hinblick auf ein bestimmtes Modell zu testen.  
  
-   Zusätzlich zu den in der vorstehenden Tabelle aufgeführten Eigenschaften enthalten AMO und XML DDL die schreibgeschützte **HoldoutActualSize**-Eigenschaft. Da die tatsächliche Größe einer Partition jedoch nicht präzise ermittelt werden kann, bevor die Struktur nicht verarbeitet wurde, sollten Sie überprüfen, ob das Modell verarbeitet wurde, bevor Sie den Wert der **HoldoutActualSize** -Eigenschaft abrufen.  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
|Thema|Links|  
|------------|-----------|  
|Beschreibt die Interaktion der Modellfilter mit Trainings- und Testdatasets.|[Filter für Miningmodelle &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)|  
|Beschreibt, wie sich die Verwendung der Trainings- und Testdaten auf die Kreuzvalidierung auswirkt.|[Kreuzvalidierung &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|Enthält Informationen über die programmgesteuerten Schnittstellen, die beim Arbeiten mit Trainings- und Testsätzen in einer Miningstruktur verwendet werden.|[AMO-Konzepte und -Objektmodell](../../analysis-services/multidimensional-models/analysis-management-objects/amo-concepts-and-object-model.md)<br /><br /> [MiningStructure-Element &#40;ASSL&#41;](../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|Stellt DMX-Syntax zum Erstellen zurückgehaltener Datasets bereit.|[CREATE MINING STRUCTURE &#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md)|  
|Hier erhalten Sie Informationen zu Fällen in Trainings- und Testsätzen.|[Data Mining-Schemarowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)<br /><br /> [Data Mining-Schemarowsets &#40;SSAs&#41;](../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Tools](../../analysis-services/data-mining/data-mining-tools.md)   
 [Datamining-Konzepte](../../analysis-services/data-mining/data-mining-concepts.md)   
 [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Tests und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  

