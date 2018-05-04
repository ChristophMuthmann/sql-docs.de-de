---
title: Miningmodelle (Analysis Services – Datamining) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- mining models [Analysis Services]
- logical architecture [Analysis Services Multidimensional Data]
- properties [Analysis Services]
- mining models [Analysis Services], about data mining models
- architecture [Analysis Services]
ms.assetid: cd4df273-0c6a-4b3e-9572-8a7e313111e8
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 74ce9756752ca98057c0a4a1c75544063c1d392b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mining-models-analysis-services---data-mining"></a>Miningmodelle (Analysis Services – Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ein *Miningmodell* wird erstellt, indem ein Algorithmus auf Daten angewendet wird. Dabei handelt es sich jedoch um mehr als einen Algorithmus oder einen Metadatencontainer, vielmehr um einen Satz von Daten, Statistiken und Muster, die auf neue Daten angewendet werden können, um Vorhersagen zu generieren und Rückschlüsse auf Beziehungen zu ziehen.  
  
 In diesem Abschnitt werden der Aufbau und die Verwendungsweise eines Data Mining-Modells erläutert: die grundlegende Architektur von Modellen und Strukturen, die Eigenschaften von Miningmodellen sowie Verfahren zum Erstellen und Verwenden von Miningmodellen.  
  
 [Architektur des Miningmodells](#bkmk_mdlArch)  
  
 [Definition von Data Mining-Modellen](#bkmk_mdlDefine)  
  
 [Miningmodelleigenschaften](#bkmk_mdlProps)  
  
 [Miningmodellspalten](#bkmk_mdlCols)  
  
 [Verarbeiten von Miningmodellen](#bkmk_mdlProcess)  
  
 [Anzeigen und Abfragen von Miningmodellen](#bkmk_mdlView)  
  
##  <a name="bkmk_mdlArch"></a> Architektur des Miningmodells  
 Ein Data Mining-Modell erhält Daten aus einer Miningstruktur und analysiert diese Daten durch die Verwendung eines Data Mining-Algorithmus. Die Miningstruktur und das Miningmodell sind separate Objekte. Die Miningstruktur speichert Informationen, die die Datenquelle definieren. Ein Miningmodell speichert Informationen, die aus der statistischen Verarbeitung der Daten herrühren, beispielsweise die als Ergebnis der Analyse gefundenen Muster.  
  
 Ein Miningmodell ist leer, bis die Daten, die von der Miningstruktur bereitgestellt werden, verarbeitet und analysiert wurden. Nachdem ein Miningmodell verarbeitet wurde, enthält es Metadaten, Ergebnisse und Bindungen zur Miningstruktur.  
  
 ![Modell enthält Metadaten, Muster und Bindungen](../../analysis-services/data-mining/media/dmcon-modelarch2.gif "Modell enthält Metadaten, Muster und Bindungen")  
  
 Die Metadaten legen den Namen des Modells und des Servers, auf dem es gespeichert ist, und eine Definition des Modells fest, einschließlich der Spalten aus der Miningstruktur, die bei der Erstellung des Modells herangezogen wurden, der Definitionen der Filter, die bei der Verarbeitung des Modells angewandt wurden, und eines Algorithmus, der für die Analyse der Daten verwendet wurde. All diese Faktoren – von den Datenspalten und deren Datentypen über Filter bis hin zum Algorithmus – haben einen erheblichen Einfluss auf die Analyseergebnisse.  
  
 Sie können mehrere Modelle mithilfe der gleichen Daten erstellen und dabei Algorithmen wie den Clustering-Algorithmus, Decision Tree-Algorithmus und Naïve Bayes-Algorithmus verwenden. Durch jeden Modelltyp wird ein anderer Satz von Mustern, Itemsets, Regeln oder Formeln erstellt, den Sie zum Generieren von Vorhersagen verwenden können. Im Allgemeinen werden die Daten von jedem Algorithmus auf unterschiedliche Weise analysiert, sodass der *Inhalt* des resultierenden Modells ebenfalls in unterschiedlichen Strukturen angeordnet ist. In einem Modelltyp könnten die Daten und Muster in *Clustern*gruppiert werden, während sie in einem anderen Modelltyp in Strukturen, Verzweigungen und Regeln angeordnet sein könnten, durch die die Daten und Muster unterteilt und definiert werden.  
  
 Außerdem wird das Modell durch die Daten beeinflusst, für die es trainiert wird: Selbst Modelle, die in der gleichen Miningstruktur trainiert wurden, können unterschiedliche Ergebnisse liefern, wenn Sie die Daten unterschiedlich filtern oder während der Analyse verschiedene Ausgangswerte verwenden. Die tatsächlichen Daten werden jedoch nicht im Modell gespeichert, sondern befinden sich in der Miningstruktur. Im Modell werden lediglich Zusammenfassungsstatistiken gespeichert. Wenn Sie beim Trainieren des Modells Filter für die Daten erstellt haben, werden die Filterdefinitionen auch mit dem Modellobjekt gespeichert.  
  
 Das Modell enthält einen Satz von Bindungen, die auf die in der Miningstruktur zwischengespeicherten Daten zurückverweisen. Wenn die Daten in der Struktur zwischengespeichert und nach der Verarbeitung nicht bereinigt wurden, können Sie über diese Bindungen einen Drillthrough von den Ergebnissen zu den Fällen durchführen, die die Ergebnisse unterstützen. Die tatsächlichen Daten werden jedoch im Strukturcache, nicht im Modell, gespeichert.  
  
 [Architektur des Miningmodells](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlDefine"></a> Definition von Data Mining-Modellen  
 Ein Data Mining-Modell wird mithilfe der folgenden allgemeinen Schritte erstellt:  
  
-   Erstellen Sie die zugrunde liegende Miningstruktur, und schließen Sie die Datenspalten ein, die u. U. benötigt werden.  
  
-   Wählen Sie den Algorithmus aus, der am besten für den analytischen Task geeignet ist.  
  
-   Wählen Sie die im Modell zu verwendenden Spalten aus der Struktur aus, und geben Sie deren Verwendungsweise an, z. B. welche Spalte das vorherzusagende Ergebnis enthält, welche Spalten nur für Eingaben vorgesehen sind usw.  
  
-   Legen Sie optional Parameter fest, die die Verarbeitung durch den Algorithmus optimieren.  
  
-   Füllen Sie das Modell mit Daten auf, indem Sie die Struktur und das Modell *verarbeiten* .  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt die folgenden Tools bereit, um die Verwaltung Ihrer Miningmodelle zu unterstützen:  
  
-   Der Data Mining-Assistent unterstützt Sie bei der Erstellung einer Struktur und des zugehörigen Miningmodells. Dies ist die leichteste Vorgehensweise. Der Assistent erstellt automatisch die erforderliche Miningstruktur und unterstützt Sie bei der Konfiguration der wichtigen Einstellungen.  
  
-   Eine DMX CREATE MODEL-Anweisung kann verwendet werden, um ein Modell zu definieren. Die erforderliche Struktur wird automatisch als Teil des Prozesses erstellt. Daher können Sie eine bestehende Struktur mit dieser Methode nicht erneut verwenden. Verwenden Sie diese Methode, wenn Sie bereits wissen, welches Modell Sie erstellen möchten, oder wenn Sie Skripts für Modelle schreiben möchten.  
  
-   Eine DMX ALTER STRUCTURE ADD MODEL-Anweisung kann verwendet werden, um ein neues Miningmodell zu einer bestehenden Struktur hinzuzufügen. Verwenden Sie diese Methode, wenn Sie mit unterschiedlichen Modellen experimentieren möchten, die auf dem gleichen Dataset basieren.  
  
 Darüber hinaus können Sie Miningmodelle programmgesteuert über AMO oder XML/A oder über den Einsatz anderer Clients, wie dem Data Mining-Client für Excel, erstellen. Weitere Informationen finden Sie in folgenden Themen:  
  
 [Architektur des Miningmodells](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlProps"></a> Miningmodelleigenschaften  
 Jedes Miningmodell verfügt über Eigenschaften, die das Modell und seine Metadaten definieren. Hierzu gehören Name, Beschreibung, Datum der letzten Verarbeitung des Modells, Berechtigungen für das Modell und Filter für die zum Trainieren verwendeten Daten.  
  
 Jedes Miningmodell verfügt darüber hinaus über Eigenschaften, die sich aus der Miningstruktur ableiten und die vom Modell verwendeten Datenspalten beschreiben. Wenn eine vom Modell verwendete Spalte eine geschachtelte Tabelle ist, kann auf die Spalte auch ein separater Filter angewendet werden.  
  
 Zusätzlich enthält jedes Miningmodell zwei besondere Eigenschaften: <xref:Microsoft.AnalysisServices.MiningModel.Algorithm%2A> und <xref:Microsoft.AnalysisServices.MiningModelColumn.Usage%2A>.  
  
-   **Algorithmus-Eigenschaft** Legt den Algorithmus fest, der zur Erstellung des Modells verwendet wird. Die verfügbaren Algorithmen hängen von Ihrem Anbieter ab. Eine Liste der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]enthaltenen Algorithmen finden Sie unter [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md). Die **Algorithm** -Eigenschaft gilt für das Miningmodell und kann für jedes Modell nur einmal festgelegt werden. Sie können den Algorithmus zu einem späteren Zeitpunkt ändern, aber einige Spalten im Miningmodell werden möglicherweise ungültig, wenn sie vom ausgewählten Algorithmus nicht unterstützt werden. Nachdem diese Eigenschaft geändert wurde, muss das Modell immer erneut verarbeitet werden.  
  
-   **Usage-Eigenschaft** Definiert die Verwendung der einzelnen Spalten durch das Modell. Sie können die Spaltenverwendung als **Input**, **Predict**, **Predict Only**oder **Key**. Die **Usage** -Eigenschaft gilt für einzelne Spalten des Miningmodells und muss für jede in einem Modell enthaltene Spalte separat festgelegt werden. Wenn die Struktur eine Spalte enthält, die Sie im Modell nicht verwenden möchten, wird die Verwendung auf **Ignore**festgelegt. Beispiele für Daten, die Sie zwar in die Miningstruktur einschließen können, in der Analyse u. U. jedoch nicht verwenden, sind Kundennamen oder E-Mail-Adressen. Auf diese Weise können sie später abgefragt werden, ohne sie in der Analysephase zu berücksichtigen.  
  
 Sie können die Werte der Eigenschaften des Miningmodells nach der Erstellung eines Miningmodells ändern. Allerdings erfordert jede Änderung, auch die des Namens des Miningmodells, eine erneute Verarbeitung des Modells. Nachdem Sie das Modell erneut verarbeitet haben, sehen Sie möglicherweise andere Ergebnisse.  
  
 [Architektur des Miningmodells](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlCols"></a> Miningmodellspalten  
 Das Miningmodell enthält Datenspalten, die aus den in der Miningstruktur definierten Spalten abgerufen werden. Sie können auswählen, welche Spalten aus der Miningstruktur im Modell verwendet werden sollen, und Kopien der Miningstrukturspalten erstellen und diese dann umbenennen oder ihre Verwendungsart ändern. Zusätzlich müssen Sie bei der Modellerstellung festlegen, auf welche Weise die Spalte vom Modell verwendet wird. Dazu gehören beispielsweise folgende Informationen: ob die Spalte ein Schlüssel ist, ob sie für Vorhersagen verwendet wird oder ob sie vom Algorithmus ignoriert werden kann.  
  
 Es wird empfohlen, während der Modellerstellung nicht jede verfügbare Datenspalte automatisch hinzuzufügen, sondern die Daten in der Struktur sorgfältig daraufhin zu überprüfen, ob sie für die Analyse geeignet sind, und nur diese Spalten in das Modell einzuschließen. Beispielsweise sollten Sie nicht mehrere Spalten mit den gleichen Daten einschließen und keine Spalten verwenden, die größtenteils eindeutige Werte enthalten. Wenn Sie der Meinung sind, dass eine Spalte nicht verwendet werden sollte, müssen Sie diese nicht aus der Miningstruktur oder dem Miningmodell löschen, sondern können stattdessen die Spalte mit einem Flag versehen, das festlegt, dass diese Spalte bei der Erstellung des Modells ignoriert werden soll. Dies bedeutet, dass die Spalte in der Miningstruktur verbleibt, im Miningmodell jedoch nicht verwendet wird. Wenn Sie Drillthroughs vom Modell zur Miningstruktur aktiviert haben, können Sie die Informationen später aus der Spalte abrufen.  
  
 Abhängig vom ausgewählten Algorithmus können einige Spalten in der Miningstruktur inkompatibel mit bestimmten Modelltypen sein oder keine zufrieden stellenden Ergebnisse liefern. Wenn die Daten z. B. kontinuierliche numerische Daten, wie eine Spalte Income, enthalten und das Modell diskrete Werte erfordert, müssen Sie die Daten u. U. in diskrete Bereiche konvertieren oder aus dem Modell entfernen. In einigen Fällen werden die Daten vom Algorithmus automatisch konvertiert oder ausgeschlossen, die Ergebnisse dürften jedoch nicht immer Ihren Erwartungen entsprechen. Sie haben die Möglichkeit, zusätzliche Kopien der Spalte zu erstellen und unterschiedliche Modelle auszuprobieren. Sie können auch Flags für die einzelnen Spalten festlegen, um anzugeben, bei welcher Spalte eine spezielle Verarbeitung erforderlich ist. Wenn die Daten z. B. NULL-Werte enthalten, können Sie die Behandlung mithilfe eines Modellierungsflags steuern. Wenn eine bestimmte Spalte in einem Modell als Regressor betrachtet werden soll, können Sie dazu ein Modellierungsflag verwenden.  
  
 Nach der Erstellung des Modells können Sie Änderungen vornehmen. Hierzu gehören zum Beispiel das Hinzufügen oder Löschen von Spalten oder das Ändern des Modellnamens. Allerdings erfordern alle Änderungen, auch solche, die ausschließlich an den Modellmetadaten vorgenommen werden, eine erneute Verarbeitung des Modells.  
  
 [Architektur des Miningmodells](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlProcess"></a> Verarbeiten von Miningmodellen  
 Beim Data Mining-Modell handelt es sich bis zu seiner Verarbeitung um ein leeres Objekt. Bei der Verarbeitung eines Modells werden die Daten, die von der Struktur zwischengespeichert werden, durch einen Filter geschickt, falls einer im Modell definiert wurde, und durch den Algorithmus analysiert. Der Algorithmus berechnet Zusammenfassungsstatistiken zur Beschreibung der Daten, identifiziert die Regeln und Muster innerhalb der Daten und verwendet diese dann zum Auffüllen des Modells.  
  
 Nach der Verarbeitung enthält das Miningmodell zahlreiche Informationen zu den in der Analyse gefundenen Daten und Mustern, einschließlich Statistiken, Regeln und Regressionsformeln. Sie können diese Informationen mithilfe der benutzerdefinierten Viewer durchsuchen oder Data Mining-Abfragen erstellen, um die Informationen abzurufen und zu Analyse- und Präsentationszwecken zu verwenden.  
  
 [Architektur des Miningmodells](#bkmk_mdlArch)  
  
##  <a name="bkmk_mdlView"></a> Anzeigen und Abfragen von Miningmodellen  
 Nach der Verarbeitung eines Modells können Sie es mithilfe der in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verfügbaren benutzerdefinierten Viewer durchsuchen. Für  
  
 Darüber hinaus können Sie Abfragen des Miningmodells erstellen, um entweder Vorhersagen zu treffen oder Modellmetadaten oder vom Modell erstellte Muster abzufragen. Abfragen werden über Data Mining-Erweiterungen (DMX; Data Mining Extensions) erstellt.  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
|Thema|Links|  
|------------|-----------|  
|Hier erfahren Sie, wie Miningstrukturen erstellt werden, die mehrere Miningmodelle unterstützen. Informationen zur Verwendung von Spalten in Modellen.|[Miningstrukturspalten](../../analysis-services/data-mining/mining-structure-columns.md)<br /><br /> [Miningmodellspalten](../../analysis-services/data-mining/mining-model-columns.md)<br /><br /> [Content-Arten & #40; Datamining & #41;](../../analysis-services/data-mining/content-types-data-mining.md)|  
|Hier erhalten Sie Informationen zu den verschiedenen Algorithmen und erfahren, wie sich die Auswahl des Algorithmus auf den Modellinhalt auswirkt.|[Miningmodellinhalt &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)<br /><br /> [Datamining-Algorithmen & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)|  
|Hier erfahren Sie, wie Eigenschaften für das Modell festgelegt werden, die dessen Zusammensetzung und Verhalten beeinflussen.|[Miningmodelleigenschaften](../../analysis-services/data-mining/mining-model-properties.md)<br /><br /> [Modellieren von Ablaufverfolgungsflags & #40; Datamining & #41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)|  
|Informationen zu programmierbaren Schnittstellen für das Data Mining.|[Entwickeln mit Analysis Management Objects & #40; AMO & #41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)<br /><br /> [Data Mining-Erweiterungen &#40;DMX&#41; – Referenz](../../dmx/data-mining-extensions-dmx-reference.md)|  
|Informationen zur Verwendung der benutzerdefinierten Data Mining-Viewer in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|[Datamining-Modell-Viewer](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|Beispiele für verschiedene Abfragetypen, die für Data Mining-Modelle verwendet werden können.|[Datamining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md)|  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Über die folgenden Links erhalten Sie spezifischere Informationen zur Verwendung von Data Mining-Modellen.  
  
|Task|Link|  
|----------|----------|  
|Hinzufügen und Löschen von Miningmodellen|[Hinzufügen eines Miningmodells zu einer vorhandenen Miningstruktur](../../analysis-services/data-mining/add-a-mining-model-to-an-existing-mining-structure.md)<br /><br /> [Löschen eines Miningmodells aus einer Miningstruktur](../../analysis-services/data-mining/delete-a-mining-model-from-a-mining-structure.md)|  
|Arbeiten mit Miningmodellspalten|[Ausschließen einer Spalte aus einem Miningmodell](../../analysis-services/data-mining/exclude-a-column-from-a-mining-model.md)<br /><br /> [Erstellen eines Alias für eine Modellspalte](../../analysis-services/data-mining/create-an-alias-for-a-model-column.md)<br /><br /> [Ändern der Diskretisierung von Spalten in einem Miningmodell](../../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)<br /><br /> [Bestimmen einer in einem Modell als Regressor zu verwendenden Spalte](../../analysis-services/data-mining/specify-a-column-to-use-as-regressor-in-a-model.md)|  
|Ändern von Modelleigenschaften|[Ändern der Eigenschaften eines Miningmodells](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)<br /><br /> [Anwenden eines Filters auf ein Miningmodell](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)<br /><br /> [Löschen eines Filters aus einem Miningmodell](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)<br /><br /> [Aktivieren von Drillthrough für ein Miningmodell](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)<br /><br /> [Anzeigen oder Ändern von Algorithmusparametern](../../analysis-services/data-mining/view-or-change-algorithm-parameters.md)|  
|Kopieren, Verschieben oder Verwalten von Modellen|[Erstellen Sie eine Kopie eines Miningmodells](../../analysis-services/data-mining/make-a-copy-of-a-mining-model.md)<br /><br /> [Kopieren einer Sicht eines Miningmodells](../../analysis-services/data-mining/copy-a-view-of-a-mining-model.md)<br /><br /> [EXPORT & #40; DMX & #41;](../../dmx/export-dmx.md)<br /><br /> [IMPORT &#40;DMX&#41;](../../dmx/import-dmx.md)|  
|Auffüllen von Modellen mit Daten oder Aktualisieren von Daten in einem Modell|[Verarbeiten eines Miningmodells](../../analysis-services/data-mining/process-a-mining-model.md)|  
|Arbeiten mit OLAP-Modellen|[Erstellen von Datamining-Dimension](../../analysis-services/data-mining/create-a-data-mining-dimension.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankobjekte &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
