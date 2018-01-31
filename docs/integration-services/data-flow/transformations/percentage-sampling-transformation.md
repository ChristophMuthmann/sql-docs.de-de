---
title: "Transformation für Prozentwert-Stichproben | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.percentagesamplingtrans.f1
- sql13.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- testing mining models
- sampling seeds [Integration Services]
- data mining [Analysis Services], sample data sets
- Percentage Sampling transformation
- sample data sets [Integration Services]
- datasets [Integration Services], sample
- training mining models
ms.assetid: 59767e52-f732-4b3f-8602-be50d0a64ef2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be38451e2fc359949ad71d143c5eaea6a1eaf41b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="percentage-sampling-transformation"></a>Transformation für Prozentwert-Stichproben
  Die Transformation für Prozentwert-Stichproben erstellt ein Stichprobendataset, indem ein Prozentwert der Transformationseingabezeilen ausgewählt wird. Das Stichprobendataset ist eine zufällige Auswahl von Zeilen aus der Transformationseingabe, damit die Stichprobe für die Eingabe repräsentativ ist.  
  
> [!NOTE]  
>  Neben dem angegeben Prozentwert verwendet die Transformation für Prozentwert-Stichproben einen Algorithmus, um zu ermitteln, ob eine Zeile in die Stichprobenausgabe eingeschlossen werden soll. Dies bedeutet, dass die Anzahl von Zeilen in der Stichprobenausgabe möglicherweise nicht genau den angegebenen Prozentwert widerspiegelt. Wenn Sie z. B. 10 % für ein Eingabedataset mit 25.000 Zeilen angeben, kann es sein, dass keine Stichprobe mit 2.500 Zeilen generiert wird. Die Stichprobe hat möglicherweise ein paar mehr oder weniger Zeilen.  
  
 Die Transformation für Prozentwert-Stichproben ist besonders für das Data Mining hilfreich. Mit dieser Transformation können Sie ein Dataset nach dem Zufallsprinzip in zwei Datasets aufteilen: eines zum Trainieren des Data Mining-Modells und ein anderes zum Testen des Modells.  
  
 Die Transformation für Prozentwert-Stichproben ist außerdem zum Erstellen von Stichprobendatasets für die Paketentwicklung hilfreich. Wenn Sie die Transformation für Prozentwert-Stichproben auf einen Datenfluss anwenden, können Sie die Größe des Datasets gleichmäßig reduzieren und zugleich die Datenmerkmale beibehalten. Das Testpaket kann dann schneller ausgeführt werden, weil ein kleines, aber repräsentatives Dataset verwendet wird.  
  
## <a name="configuration-the-percentage-sampling-transformation"></a>Konfiguration der Transformation für Prozentwert-Stichproben  
 Sie können einen Stichproben-Ausgangswert angeben, um das Verhalten des Zufallszahlen-Generators zu ändern, mit dem die Transformation Zeilen auswählt. Wenn der gleiche Stichproben-Ausgangswert verwendet wird, erstellt die Transformation immer die gleiche Stichprobenausgabe. Wenn kein Ausgangswert angegeben ist, erstellt die Transformation die Zufallszahl mithilfe der Taktanzahl des Betriebssystems. Deshalb sollten Sie einen Standardausgangswert wählen, wenn Sie die Transformationsergebnisse beim Entwickeln und Testen eines Pakets überprüfen möchten. Anschließend verwenden Sie dann einen zufälligen Ausgangswert, wenn das Paket auf den Produktionsserver verschoben wird.  
  
 Diese Transformation ist mit der Transformation für Zeilenstichproben vergleichbar, die ein Stichprobendataset erstellt, indem eine angegebene Anzahl von Eingabezeilen ausgewählt wird. Weitere Informationen finden Sie unter [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md).  
  
 Die Transformation für Prozentwert-Stichproben schließt die benutzerdefinierte Eigenschaft **SamplingValue** ein. Diese Eigenschaft kann beim Laden des Pakets mithilfe eines Eigenschaftsausdrucks aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Diese Transformation weist eine Eingabe und zwei Ausgaben auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="percentage-sampling-transformation-editor"></a>Transformations-Editor für Prozentwertstichprobe
  Im Dialogfeld **Transformations-Editor für Prozentwertstichprobe** können Sie einen Teil der Eingabe mithilfe des angegebenen Prozentsatzes von Zeilen als Stichprobe entnehmen. Durch diese Transformation wird die Eingabe in zwei getrennte Ausgaben geteilt.  
  
### <a name="options"></a>Tastatur  
 **Prozentsatz der Zeilen**  
 Geben Sie den Prozentsatz der Zeilen in der Eingabe an, die als Stichprobe verwendet werden sollen.  
  
 Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.  
  
 **Ausgabename für Stichprobendaten**  
 Geben Sie einen eindeutigen Namen für die Ausgabe an, die die als Stichprobe entnommenen Zeilen enthalten wird. Der bereitgestellte Name wird im [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Ausgabename für nicht ausgewählte Daten**  
 Geben Sie einen eindeutigen Namen für die Ausgabe an, die die Zeilen enthalten wird, die nicht zur Stichprobe gehören. Der bereitgestellte Name wird im [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Folgenden zufälligen Ausgangswert verwenden**  
 Geben Sie den Ausgangswert für den Zufallszahlen-Generator an, der von der Transformation zum Erstellen der Stichprobe verwendet wird. Dies wird ausschließlich für Entwicklung und Tests empfohlen. Wenn kein zufälliger Ausgangswert angegeben wird, wird von der Transformation die Taktanzahl aus Microsoft Windows verwendet.  
  
  
