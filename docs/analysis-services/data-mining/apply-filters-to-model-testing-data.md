---
title: Anwenden von Filtern zum Modellieren von Testdaten | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input row filtering [SQL Server]
- filtering input rows [Analysis Services]
- Mining Accuracy Chart [Analysis Services], filtering input rows
ms.assetid: 9ccc9a23-5597-4b35-a05f-2fc8eb885147
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bb193bb9e90d1bd2b7773c2a1bd2f237e7fa0135
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="apply-filters-to-model-testing-data"></a>Anwenden von Filtern zum Modellieren von Testdaten
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Wenn Sie beim Testen eines Modells eine externen Datenquelle angeben, können Sie optional einen Filter, um die Eingabedaten einzuschränken anwenden. Sie möchten das Modell zum Beispiel speziell für Vorhersagen zu Kunden in einem bestimmten Einkommensbereich testen.  
  
 Beispiel: Im Targeted Mailing-Szenario von Adventure Works können Sie einen Filterausdruck wie den folgenden Ausdruck für ProspectiveBuyer erstellen. Dabei handelt es sich um die Tabelle, die die Testdaten enthält und die Testfälle nach Einkommensbereich einschränkt:  
  
 `[YearlyIncome] = '50000'`  
  
 Das Verhalten von Filtern unterscheidet sich ein wenig, was davon abhängig ist, ob Sie Modelltrainingsdaten oder ein Testdataset filtern:  
  
-   Wenn Sie einen Filter für ein Testdataset definieren, erstellen Sie eine WHERE-Klausel für die eingehenden Daten. Wenn ein zum Auswerten des Modells verwendetes Eingabedataset gefiltert wird, wird der Filterausdruck in eine Transact-SQL-Anweisung übersetzt und bei der Diagrammerstellung auf die Eingabetabelle angewendet. Dadurch kann die Anzahl von Testfällen stark verringert werden.  
  
-   Wenn Sie einen Filter auf ein Miningmodell anwenden, wird der von Ihnen definierte Filterausdruck in eine DMX-Anweisung (Data Mining Extensions) übersetzt und auf das einzelne Modell angewendet. Daher wird beim Anwenden eines Filters auf ein Modell nur eine Teilmenge der ursprünglichen Daten zum Trainieren des Modells verwendet. Dies kann Probleme verursachen, wenn Sie das Trainingsmodell mit einem Kriteriensatz filtern, damit das Modell im Hinblick auf einen bestimmten Satz von Daten optimiert wird, und anschließend das Modell mit einem anderen Satz von Kriterien testen.  
  
-   Wenn beim Erstellen der Struktur ein Testdataset definiert wurde, umfassen die zum Training verwendeten Modellfälle nur die Fälle, die im Trainingssatz der Miningstruktur enthalten sind **und** den Filterbedingungen entsprechen. Wenn Sie ein Modell testen und die Option **Testfälle für Miningstruktur verwenden**auswählen, beinhalten die Testfälle daher nur die Fälle, die im Testsatz der Miningstruktur enthalten sind und den Filterbedingungen entsprechen. Wenn das Zurückhaltungsdataset nicht definiert wurde, werden alle Modellfälle, die den Filterbedingungen entsprechen, zum Training verwendet.  
  
-   Filterbedingungen, die Sie für ein Modell übernehmen, beeinflussen auch Drillthroughabfragen für die Modellfälle.  
  
 Zusammenfassung: Wenn Sie mehrere Modelle testen, auch wenn alle Modelle auf der gleichen Miningstruktur basieren, müssen Sie sich darüber im Klaren sein, dass die Modelle für Training und Tests möglicherweise andere Teilmengen von Daten verwenden. Dies kann folgende Auswirkungen auf Genauigkeitsdiagramme haben:  
  
-   Die Gesamtzahl der Fälle in den Testsätzen kann sich je nach getestetem Modell unterscheiden.  
  
-   Die Prozentsätze für jedes Modell ergeben im Diagramm möglicherweise keine Übereinstimmung, wenn die Modelle unterschiedliche Teilmengen von Trainings- oder Testdaten verwenden.  
  
 Um zu bestimmen, ob ein Modell einen vordefinierten Filter enthält, der sich auf die Ergebnisse auswirken könnte, können Sie nach der **Filter** -Eigenschaft im **Eigenschaftenbereich** suchen, oder Sie können das Modell abfragen, indem Sie die Data Mining-Schemarowsets verwenden. Zum Beispiel wird bei der folgenden Abfrage der Filtertext für das angegebene Modell zurückgegeben:  
  
 `SELECT [FILTER] FROM $system.DMSCHEMA_MINING_MODELS WHERE MODEL_NAME = 'name of model’`  
  
> [!WARNING]  
>  Wenn Sie den Filter aus einem vorhandenen Miningmodell entfernen oder die Filterbedingungen ändern möchten, müssen Sie das Miningmodell erneut verarbeiten.  
  
 Weitere Informationen zu den Filtertypen, die angewendet werden können, und zur Auswertung von Filterausdrücken finden Sie unter [Modellfiltersyntax und Beispiele &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md).  
  
### <a name="create-a-filter-on-external-testing-data"></a>Erstellen eines Filters für externe Testdaten  
  
1.  Doppelklicken Sie auf die Miningstruktur, die das Modell enthält, das Sie testen möchten, um den Data Mining-Designer zu öffnen.  
  
2.  Wählen Sie die Registerkarte **Mininggenauigkeitsdiagramm** und anschließend die Registerkarte **Eingabeauswahl** aus.  
  
3.  Wählen Sie auf der Registerkarte **Eingabeauswahl** unter **Dataset auswählen, das für das Genauigkeitsdiagramm verwendet werden soll**die Option **Anderes Dataset verwenden**.  
  
4.  Klicken Sie auf die Durchsuchen-Schaltfläche **(...)** , um ein Dialogfeld zu öffnen, und wählen Sie das externe Dataset aus.  
  
5.  Wählen Sie die Falltabelle aus, und fügen Sie ggf. eine geschachtelte Tabelle hinzu. Ordnen Sie Spalten im Modell nach Bedarf Spalten im externen Dataset zu. Schließen Sie das Dialogfeld **Spaltenzuordnung angeben** , um die Quelltabellendefinition zu speichern.  
  
6.  Klicken Sie auf **Filter-Editor öffnen** , um einen Filter für das Dataset zu definieren.  
  
     Das Dialogfeld **Datasetfilter** wird geöffnet. Wenn die Struktur eine geschachtelte Tabelle enthält, können Sie einen Filter in zwei Teilen erstellen. Legen Sie zuerst mithilfe des Dialogfelds **Datasetfilter** Bedingungen für die Falltabelle fest, und anschließend legen Sie Bedingungen für die geschachtelten Zeilen mithilfe des Dialogfelds **Filter** fest.  
  
7.  Klicken Sie im Dialogfeld **Datasetfilter** auf die oberste Zeile im Raster (unter **Miningstrukturspalte**), und wählen Sie eine Tabelle oder eine Spalte in der Liste aus.  
  
     Wenn die Datensatzsicht mehrere Tabellen oder eine geschachtelte Tabelle enthält, müssen Sie zuerst den Tabellennamen auswählen. Andernfalls können Sie Spalten direkt aus der Falltabelle auswählen.  
  
     Fügen Sie eine neue Zeile für jede Spalte hinzu, die Sie filtern möchten.  
  
8.  Verwenden Sie die Spalten **Operator**und **Wert** , um zu definieren, wie die Spalte gefiltert wird.  
  
     **Hinweis** Geben Sie die Werte ohne Anführungszeichen ein.  
  
9. Klicken Sie auf das Textfeld **Und/Oder** , und wählen Sie einen logischen Operator aus, um zu definieren, wie mehrere Bedingungen kombiniert werden.  
  
10. Optional können Sie auf die Schaltfläche zum Durchsuchen **(…)** rechts neben dem Textfeld **Wert** klicken, um das Dialogfeld **Filter** zu öffnen und Bedingungen für die geschachtelte Tabelle oder die einzelnen Spalten der Falltabelle festzulegen.  
  
11. Überprüfen Sie, dass die fertig gestellten Filterbedingungen richtig sind, indem Sie den Text im Bereich **Ausdruck** anzeigen.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Die Filterbedingung wird auf die Datenquelle angewendet, wenn Sie das Genauigkeitsdiagramm erstellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Auswählen und Zuordnen von Modelltestdaten](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [Verwenden von geschachtelten Tabellendaten als Eingabe für ein Genauigkeitsdiagramm](../../analysis-services/data-mining/using-nested-table-data-as-an-input-for-an-accuracy-chart.md)   
 [Auswählen eines Genauigkeitsdiagrammtyps und Festlegen von Diagrammoptionen](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
