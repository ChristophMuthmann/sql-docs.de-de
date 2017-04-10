---
title: "Transformation f&#252;r Zeilenstichproben | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.rowsamplingtrans.f1"
helpviewer_keywords: 
  - "Stichproben-Ausgangswerte [Integration Services]"
  - "Zufällige Ausgangswerte"
  - "Zufällige Stichproben"
  - "Beispieldatasets [Integration Services]"
  - "Transformation für Zeilenstichproben"
  - "Pakete [Integration Services], Stichproben"
  - "Datasets [Integration Services], Stichprobe"
ms.assetid: b6caafd3-30b2-4368-82af-a44611d4cd39
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Transformation f&#252;r Zeilenstichproben
  Mit der Transformation für Zeilenstichproben wird eine nach dem Zufallsprinzip ausgewählte Teilmenge eines Eingabedatasets abgerufen. Sie können die genaue Größe der Ausgabestichprobe sowie einen Ausgangswert für den Zufallszahlen-Generator angeben.  
  
 Für zufällige Stichproben gibt es viele Anwendungsmöglichkeiten. Beispielsweise könnte ein Unternehmen, das 50 Mitarbeiter nach dem Zufallsprinzip für einen Lotteriepreis auswählen möchte, die Transformation für Zeilenstichproben für die Mitarbeiterdatenbank ausführen und die genaue Anzahl von Gewinnern generieren.  
  
 Die Transformation für Zeilenstichproben ist außerdem bei der Paketentwicklung hilfreich, um ein kleines, aber repräsentatives Dataset zu erstellen. Sie können die Paketausführung und die Datentransformation mit äußerst repräsentativen Daten, aber schneller testen, weil anstelle des vollständigen Datasets eine zufällige Stichprobe verwendet wird. Das vom Testpaket verwendete Stichprobendataset besitzt immer die gleiche Größe. Deshalb können mit der Stichprobenteilmenge auch Leistungsprobleme beim Paket einfacher identifiziert werden.  
  
 Diese Transformation ist mit der Transformation für Prozentwert-Stichproben vergleichbar, die ein Stichprobendataset durch Auswählen eines Prozentwerts der Eingabezeilen erstellt. Siehe [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
## Konfigurieren der Transformation für Zeilenstichproben  
 Die Transformation für Zeilenstichproben erstellt ein Stichprobendataset durch Auswählen einer angegebene Anzahl von Transformationseingabezeilen. Da die Auswahl von Zeilen aus der Transformationseingabe nach dem Zufallsprinzip erfolgt, ist die Stichprobe für die Eingabe repräsentativ. Darüber hinaus können Sie den Ausgangswert angeben, der vom Zufallszahlen-Generator verwendet wird, um die Auswahl der Zeilen durch die Transformation zu beeinflussen.  
  
 Wenn der gleiche zufällige Ausgangswert in derselben Transformationseingabe verwendet wird, wird immer dieselbe Stichprobenausgabe generiert. Wenn kein Ausgangswert angegeben ist, erstellt die Transformation die Zufallszahl mithilfe der Taktanzahl des Betriebssystems. Deshalb können Sie beim Testen denselben Ausgangswert verwenden, um die Transformationsergebnisse beim Entwickeln und Testen des Pakets zu überprüfen. Anschließend verwenden Sie dann einen zufälligen Ausgangswert, wenn das Paket auf den Produktionsserver verschoben wird.  
  
 Die Transformation für Zeilenstichproben schließt die benutzerdefinierte Eigenschaft **SamplingValue** ein. Diese Eigenschaft kann beim Laden des Pakets mithilfe eines Eigenschaftsausdrucks aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Diese Transformation weist eine Eingabe und zwei Ausgaben auf. Es ist keine Fehlerausgabe vorhanden.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld **Transformations-Editor für Zeilenstichprobe** festlegen können, finden Sie unter [Transformations-Editor für Zeilenstichprobe &#40;Seite „Sampling“&#41;](../../../integration-services/data-flow/transformations/row-sampling-transformation-editor-sampling-page.md).  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Weitere Informationen zum Festlegen von Eigenschaften finden Sie unter.  
  
## Verwandte Aufgaben  
 [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
  