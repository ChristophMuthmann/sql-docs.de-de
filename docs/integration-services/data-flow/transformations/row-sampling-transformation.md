---
title: "Transformation für Zeilenstichproben | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.rowsamplingtrans.f1
- sql13.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql13.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- sampling seeds [Integration Services]
- random seeds
- random sampling
- sample data sets [Integration Services]
- Row Sampling transformation
- packages [Integration Services], samples
- datasets [Integration Services], sample
ms.assetid: b6caafd3-30b2-4368-82af-a44611d4cd39
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 74bc28f5ce476bf86ad91258877fe3c45e44c8df
ms.contentlocale: de-de
ms.lasthandoff: 08/19/2017

---
# <a name="row-sampling-transformation"></a>Transformation für Zeilenstichproben
  Mit der Transformation für Zeilenstichproben wird eine nach dem Zufallsprinzip ausgewählte Teilmenge eines Eingabedatasets abgerufen. Sie können die genaue Größe der Ausgabestichprobe sowie einen Ausgangswert für den Zufallszahlen-Generator angeben.  
  
 Für zufällige Stichproben gibt es viele Anwendungsmöglichkeiten. Beispielsweise könnte ein Unternehmen, das 50 Mitarbeiter nach dem Zufallsprinzip für einen Lotteriepreis auswählen möchte, die Transformation für Zeilenstichproben für die Mitarbeiterdatenbank ausführen und die genaue Anzahl von Gewinnern generieren.  
  
 Die Transformation für Zeilenstichproben ist außerdem bei der Paketentwicklung hilfreich, um ein kleines, aber repräsentatives Dataset zu erstellen. Sie können die Paketausführung und die Datentransformation mit äußerst repräsentativen Daten, aber schneller testen, weil anstelle des vollständigen Datasets eine zufällige Stichprobe verwendet wird. Das vom Testpaket verwendete Stichprobendataset besitzt immer die gleiche Größe. Deshalb können mit der Stichprobenteilmenge auch Leistungsprobleme beim Paket einfacher identifiziert werden.  
  
 Diese Transformation ist mit der Transformation für Prozentwert-Stichproben vergleichbar, die ein Stichprobendataset durch Auswählen eines Prozentwerts der Eingabezeilen erstellt. Siehe [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
## <a name="configuring-the-row-sampling-transformation"></a>Konfigurieren der Transformation für Zeilenstichproben  
 Die Transformation für Zeilenstichproben erstellt ein Stichprobendataset durch Auswählen einer angegebene Anzahl von Transformationseingabezeilen. Da die Auswahl von Zeilen aus der Transformationseingabe nach dem Zufallsprinzip erfolgt, ist die Stichprobe für die Eingabe repräsentativ. Darüber hinaus können Sie den Ausgangswert angeben, der vom Zufallszahlen-Generator verwendet wird, um die Auswahl der Zeilen durch die Transformation zu beeinflussen.  
  
 Wenn der gleiche zufällige Ausgangswert in derselben Transformationseingabe verwendet wird, wird immer dieselbe Stichprobenausgabe generiert. Wenn kein Ausgangswert angegeben ist, erstellt die Transformation die Zufallszahl mithilfe der Taktanzahl des Betriebssystems. Deshalb können Sie beim Testen denselben Ausgangswert verwenden, um die Transformationsergebnisse beim Entwickeln und Testen des Pakets zu überprüfen. Anschließend verwenden Sie dann einen zufälligen Ausgangswert, wenn das Paket auf den Produktionsserver verschoben wird.  
  
 Die Transformation für Zeilenstichproben schließt die benutzerdefinierte Eigenschaft **SamplingValue** ein. Diese Eigenschaft kann beim Laden des Pakets mithilfe eines Eigenschaftsausdrucks aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Diese Transformation weist eine Eingabe und zwei Ausgaben auf. Es ist keine Fehlerausgabe vorhanden.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Weitere Informationen zum Festlegen von Eigenschaften finden Sie unter.  
  
## <a name="row-sampling-transformation-editor-sampling-page"></a>Transformations-Editor für Zeilenstichprobe (Seite Stichprobenentnahme)
  Im Dialogfeld **Transformations-Editor für Zeilenstichprobe** können Sie einen Teil der Eingabe mithilfe der angegebenen Anzahl von Zeilen als Stichprobe entnehmen. Durch diese Transformation wird die Eingabe in zwei getrennte Ausgaben geteilt.  
  
### <a name="options"></a>enthalten  
 **Anzahl von Zeilen**  
 Geben Sie die Anzahl der Zeilen in der Eingabe an, die als Stichprobe verwendet werden sollen.  
  
 Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.  
  
 **Ausgabename für Stichprobendaten**  
 Geben Sie einen eindeutigen Namen für die Ausgabe an, die die als Stichprobe entnommenen Zeilen enthalten wird. Der angegebene Name wird im SSIS-Designer angezeigt.  
  
 **Ausgabename für nicht ausgewählte Daten**  
 Geben Sie einen eindeutigen Namen für die Ausgabe an, die die Zeilen enthalten wird, die nicht zur Stichprobe gehören. Der angegebene Name wird im SSIS-Designer angezeigt.  
  
 **Folgenden zufälligen Ausgangswert verwenden**  
 Geben Sie den Ausgangswert für den Zufallszahlen-Generator an, der von der Transformation zum Erstellen der Stichprobe verwendet wird. Dies wird ausschließlich für Entwicklung und Tests empfohlen. Wenn kein zufälliger Ausgangswert angegeben wird, wird von der Transformation die Taktanzahl aus Microsoft Windows als Ausgangswert verwendet.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
  

