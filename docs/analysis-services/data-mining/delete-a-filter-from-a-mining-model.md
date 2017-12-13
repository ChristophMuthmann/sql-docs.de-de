---
title: "Löschen eines Filters aus einem Miningmodell | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: filters [Analysis Services]
ms.assetid: 91220b21-adbc-49a9-b200-8bf0a724eff1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f39a61be641cf10e7cc3753e7e4c169013076f20
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="delete-a-filter-from-a-mining-model"></a>Löschen eines Filters aus einem Miningmodell
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Wenn Sie einen Filter für ein Miningmodell erstellen, können Sie Modelle für eine Teilmenge der Daten in der Datenquellensicht erstellen. Filter sind auch für das Testen der Genauigkeit des Modells auf einer Teilmenge der ursprünglichen Daten nützlich.  
  
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
 [Ausführen von Drillthroughs für Falldaten aus einem Miningmodell](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)   
 [Miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Filter für Miningmodelle &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
