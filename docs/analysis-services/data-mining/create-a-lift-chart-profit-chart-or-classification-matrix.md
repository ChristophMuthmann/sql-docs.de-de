---
title: Erstellen Sie ein Prognosegütediagramm, Gewinndiagramm oder Klassifikationsmatrix | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services], mining structures
ms.assetid: aa3d052f-58a9-4417-8e7a-5e6feb562af0
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b16770ad1bf8ca0052f7b8b6af22df02d4e4392f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-lift-chart-profit-chart-or-classification-matrix"></a>Erstellen von Prognosegütediagrammen, Gewinndiagrammen oder Klassifikationsmatrizen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sie können für ein Genauigkeitsdiagramm erstellen eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datamining-Modell in fünf grundlegenden Schritten:  
  
-   Wählen Sie die Miningstruktur aus, die die zu vergleichenden Miningmodelle enthält.  
  
-   Wählen Sie die Miningmodelle aus, die dem Diagramm hinzugefügt werden sollen.  
  
-   Geben Sie eine Testdatenquelle an, die beim Generieren des Diagramms verwendet werden soll.  
  
-   Wählen Sie den Diagrammtyp.  
  
-   Konfigurieren Sie die Diagrammoptionen.  
  
 Diese grundlegenden Schritte sind für das Prognosegütediagramm, das Gewinndiagramm und die Klassifizierungsmatrix identisch. Die folgenden Prozeduren gliedern die Schritte zur Konfiguration der grundlegenden Diagrammoptionen für diese Diagrammtypen. Informationen zum Erstellen eines übergreifenden Überprüfungsberichts finden Sie unter [Measures im Kreuzvalidierungsbericht](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
### <a name="open-the-mining-structure-in-the-accuracy-chart-designer"></a>Öffnen der Miningstruktur im Genauigkeitsdiagramm-Designer  
  
1.  Öffnen Sie den Data Mining-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Doppelklicken Sie in Projektmappen-Explorer auf die Struktur, die das bzw. die Miningmodelle enthält.  
  
3.  Klicken Sie auf die Registerkarte **Mininggenauigkeitsdiagramm** .  
  
### <a name="select-mining-models-for-inclusion-in-the-chart"></a>Auswählen von Miningmodellen für die Einbeziehung in das Diagramm  
  
1.  Klicken Sie in **auf der Registerkarte** Mininggenauigkeitsdiagramm [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]im Data Mining-Designer auf die Registerkarte **Eingabeauswahl** .  
  
     Die Liste zeigt alle Modelle in der aktuellen Struktur an, die über das gleiche vorhersagbare Attribut verfügen.  
  
2.  Wählen Sie das Feld **Anzeigen** für jedes Modell aus, das Sie ins Diagramm aufnehmen möchten.  
  
3.  Klicken Sie auf das Textfeld **Name der vorhersagbaren Spalte** , und wählen Sie den Namen einer vorhersagbaren Spalte in der Liste aus. Alle Modelle, die Sie in das Diagramm aufnehmen, müssen die gleiche vorhersagbare Spalte verwenden.  
  
4.  Wenn Sie zwei Modelle vergleichen und die vorhersagbaren Spalten unterschiedliche Werte oder Datentypen besitzen, deaktivieren Sie das Kontrollkästchen **Vorhersagespalten und -werte synchronisieren** , um einen Vergleich zu erzwingen.  
  
    > [!NOTE]  
    >  Ist das Kontrollkästchen **Vorhersagespalten und -werte synchronisieren** aktiviert, analysiert Analysis Services die Daten in den vorhersagbaren Spalten des Modells sowie die Testdaten und versucht, die größte Übereinstimmung zu finden. Deaktivieren Sie das Kontrollkästchen daher nur, wenn es absolut erforderlich ist, um einen Vergleich der Spalten zu erzwingen.  
  
5.  Klicken Sie auf das Textfeld **Wert vorhersagen** , und wählen Sie einen Wert aus der Liste aus. Wenn die vorhersagbare Spalte einen kontinuierlichen Datentyp enthält, müssen Sie einen Wert in das Textfeld eingeben.  
  
     Weitere Informationen finden Sie unter [Auswählen der zum Testen eines Miningmodells zu verwendenden Spalte](../../analysis-services/data-mining/choose-the-column-to-use-for-testing-a-mining-model.md).  
  
### <a name="select-testing-data"></a>Auswählen von Testdaten  
  
1.  Geben Sie auf der Registerkarte **Eingabeauswahl** der Registerkarte **Mininggenauigkeitsdiagramm** die Datenquelle an, mit der Sie das Diagramm generieren. Wählen Sie dazu eine der Optionen in der Gruppe **Dataset auswählen, das für das Genauigkeitsdiagramm verwendet werden soll**aus.  
  
    -   Wählen Sie die Option **Miningmodelltestfälle verwenden**, wenn Sie die Teilmenge der Fälle verwenden möchten, die von der Schnittmenge der Miningstrukturtestfälle und aller Filter definiert werden, die möglicherweise während der Modellerstellung angewendet wurden.  
  
    -   Wählen Sie die Option **Miningstrukturtestfälle verwenden**aus, um den vollständigen Satz der Testfälle zu verwenden, die als Teil des zurückgehaltenen Datasets der Miningstrukturen definiert wurden.  
  
    -   Aktivieren Sie die Option **Anderes Dataset verwenden**, wenn Sie externe Daten verwenden möchten.  Das Dataset muss als Datenquellensicht verfügbar sein.   Klicken Sie auf die Schaltfläche zum Durchsuchen (**…**), um die Datentabellen auszuwählen, die Sie für das Genauigkeitsdiagramm verwenden möchten. Weitere Informationen finden Sie unter [Choose and Map Model Testing Data](../../analysis-services/data-mining/choose-and-map-model-testing-data.md).  
  
         Wenn Sie ein externes Dataset verwenden, können Sie das Eingabedataset optional filtern. Weitere Informationen finden Sie unter [Anwenden von Filtern zum Modellieren von Testdaten](../../analysis-services/data-mining/apply-filters-to-model-testing-data.md).  
  
> [!NOTE]  
>  Mithilfe der Registerkarte **Eingabeauswahl** können Sie keinen Filter für die Testfälle für das Miningmodell oder die Miningstruktur erstellen. Um einen Filter für das Miningmodell zu erstellen, ändern Sie die Filtereigenschaft des Modells. Weitere Informationen finden Sie unter [Anwenden eines Filters auf ein Miningmodell](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
### <a name="configure-chart-settings-and-generate-the-chart"></a>Konfigurieren von Diagrammeinstellungen und Generieren des Diagramms  
  
1.  Klicken Sie in der Registerkarte **Mininggenauigkeitsdiagramm** auf die Registerkarte für das Diagramm, das Sie erstellen möchten.  
  
2.  Klicken Sie für ein **Prognosegütediagramm**auf die Registerkarte **Prognosegütediagramm** . Das Diagramm wird automatisch auf Grundlage des Modells, der vorhersagbaren Attribute und der Eingabedaten generiert, die Sie soeben ausgewählt haben.  
  
3.  Klicken Sie für eine **Klassifikationsmatrix**auf die Registerkarte **Klassifikationsmatrix** . Es werden keine weiteren Einstellungen benötigt. Das Diagramm wird automatisch auf Grundlage der Eingabedaten und des Modells generiert, das Sie ausgewählt haben.  
  
4.  Klicken Sie für ein **Gewinndiagramm**auf die Registerkarte **Prognosegütediagramm** . Wählen Sie anschließend in der Dropdownliste **Diagrammtyp** die Option **Gewinndiagramm**aus.  
  
     Geben Sie die folgenden Einstellungen im Dialogfeld **Gewinndiagrammeinstellungen** ein.  
  
     **Auffüllung**  
     Die Anzahl von Fällen im Dataset, die Sie beim Erstellen des Prognosegütediagramms verwenden möchten.  
  
     Das Modell wählt die Fälle immer nach sinkender Wahrscheinlichkeit aus. Wenn Sie also potenzielle Kunden bewerten und eine Anzahl auswählen, die der Hälfte der in der Kundendatenbank vorhandenen Kunden entspricht, misst das Modell die Genauigkeit für die Teilmenge der Fälle, die am besten für Ihr Modell geeignet sind.  
  
     Die Ursache hierfür liegt darin, dass Sie beim Erstellen eines Mailings oder einer Kampagne mit dem Modell die Vorhersagewahrscheinlich für jeden Fall nutzen, um nur die Kunden anzusprechen, die mit höchster Wahrscheinlichkeit einen Kauf tätigen werden.  
  
     **Feste Kosten**  
     Die festen Kosten, die mit dem Geschäftsproblem verbunden sind.  
  
     Bei einer Targeted Mailing-Lösung könnten die festen Kosten beispielsweise die Kosten zum Einrichten eines Druckers umfassen, die die anfänglichen Kosten für die Vorbereitung des Mailings abdecken.  
  
     Diese Kosten gelten einmal für die gesamte Zielpopulation.  
  
     **Einzelkosten**  
     Kosten, die zusätzlich zu den festen Kosten entstehen und den einzelnen Kundenkontakten zugeordnet werden können. Sie könnten beispielsweise die Versandkosten für ein Mailing oder die Kosten für Telefonanrufe eingeben.  
  
     Diese Kosten müssen für die gesamte Zielpopulation die gleichen sein. Jeder Wert wird mit der Anzahl der angesprochenen Fälle multipliziert.  
  
     **Einzelumsatz**  
     Die Höhe des mit einem erfolgreichen Verkauf verbundenen Umsatzes.  
  
## <a name="see-also"></a>Siehe auch  
 [Prognosegütediagramm &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [Klassifikationsmatrix &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)  
  
  
