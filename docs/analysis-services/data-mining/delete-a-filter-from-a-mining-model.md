---
title: Löschen eines Filters aus einem Miningmodell | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6bce8cf010b253f8a45b75fdda8e5252d357f4d7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="delete-a-filter-from-a-mining-model"></a>Löschen eines Filters aus einem Miningmodell
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Wenn Sie auf einem Miningmodell einen Filter erstellen, können Sie Modelle auf einer Teilmenge der Daten in der Datenquellensicht erstellen. Filter sind auch für das Testen der Genauigkeit des Modells auf einer Teilmenge der ursprünglichen Daten nützlich.  
  
 Sie müssen den Filter jedoch löschen, wenn Sie wieder den vollständigen Satz von Fällen anzeigen möchten. Dieses Verfahren beschreibt, wie Sie Bedingungen in einem Filter entfernen oder den Filter vollständig löschen.  
  
### <a name="to-delete-a-condition-from-a-filter-on-a-mining-model"></a>So löschen Sie eine Bedingung aus einem Filter in einem Miningmodell  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]im Projektmappen-Explorer auf die Miningstruktur, die das Miningmodell enthält, auf das Sie einen Filter anwenden möchten.  
  
2.  Klicken Sie auf die Registerkarte **Miningmodelle** .  
  
3.  Wählen Sie das Modell aus, und klicken Sie mit der rechten Maustaste, um das Kontextmenü zu öffnen.  
  
     – Oder –  
  
     Wählen Sie das Modell aus. Wählen Sie im Menü **Miningmodell** die Option **Modellfilter festlegen**aus.  
  
4.  Klicken Sie im Dialogfeld **Modellfilter** mit der rechten Maustaste auf die Zeile im Raster, die die Bedingung enthält, die Sie löschen möchten.  
  
5.  Wählen Sie **Löschen**aus.  
  
### <a name="to-clear-the-filter-on-a-mining-model-in-the-filter-editor-dialog-box"></a>So löschen Sie den Filter in einem Miningmodell im Dialogfeld 'Filter-Editor'  
  
-   Klicken Sie im Dialogfeld **Filter-Editor** mit der rechten Maustaste auf eine beliebige Zeile im Raster, und wählen Sie **Alle löschen**aus.  
  
## <a name="working-with-model-filters-using-the-properties-window"></a>Arbeiten mit Modellfiltern mit dem Eigenschaftenfenster  
 Wenn Sie den gesamten Filter löschen möchten, müssen Sie die Dialogfelder des Filter-Editors nicht öffnen. Die Filterbedingungen, die Sie erstellt haben, sind in der **Filter** -Eigenschaft des Miningmodells verfügbar.  
  
> [!NOTE]  
>  Sie können die Eigenschaften eines Miningmodells in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]anzeigen, aber nicht in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-clear-the-filter-on-a-mining-model-in-solution-explorer"></a>So löschen Sie den Filter in einem Miningmodell im Projektmappen-Explorer  
  
1.  Klicken Sie im Projektmappen-Explorer auf das Miningmodell, das den Filter enthält.  
  
2.  Klicken Sie im **Eigenschaftenfenster** mit der rechten Maustaste auf den Filtertext in der **Filter** -Eigenschaft, und wählen Sie **Alles markieren**aus.  
  
3.  Drücken Sie die Rücktaste oder die Taste ENTF.  
  
## <a name="see-also"></a>Siehe auch  
 [Drillthrough zu Falldaten aus einem Miningmodell](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)   
 [Miningmodelltasks und Anweisungen Mining](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Filter für Miningmodelle & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
