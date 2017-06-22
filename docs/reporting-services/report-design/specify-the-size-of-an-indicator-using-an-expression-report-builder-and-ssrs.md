---
title: "Geben Sie die Größe eines Indikators mithilfe eines Ausdrucks (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab0b86f1-4882-4258-a2b6-c612faecfa4b
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 50bf03c9ad36de5e98451705aaae5c0afa79c70b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs"></a>Angeben der Größe eines Indikators mithilfe eines Ausdrucks (Berichts-Generator und SSRS)
  Zusätzlich zu Farbe, Richtung und Form können Sie die Größe anpassen und damit die visuelle Wirkung von Indikatoren maximieren.  
  
 Ein Indikator verfügt über eine Auflistung von Indikatorstatus mit der Bezeichnung IndicatorStates. Die IndicatorStates-Auflistung verfügt in der Regel über mehrere Status. Jeder Status ist ein Element der Auflistung und wird durch ein Symbol dargestellt. Zusammen bilden die Status die IndicatorsStates-Auflistung.  
  
 Um die Größen von Symbolen dynamisch zu konfigurieren, legen Sie die Eigenschaften der Elemente der IndicatorsStates-Auflistung im Eigenschaftenbereich des Berichts-Generators fest. Zum Anzeigen des Bereichs **Eigenschaften** klicken Sie auf der Registerkarte **Ansicht** auf **Eigenschaften**.  
  
> [!NOTE]  
>  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]verwenden Sie das **Eigenschaftenfenster** , um die Elementeigenschaften festzulegen. Wenn das **Eigenschaftenfenster** nicht geöffnet ist, drücken Sie die F4-TASTE.  
  
 Der Bereich **Eigenschaften** bietet Zugriff auf die Eigenschaften der IndicatorStates-Auflistung eines Indikators. Sie konfigurieren die Größe der Symbole, indem Sie die ScaleFactor-Eigenschaft der IndicatorStates-Auflistungselemente mit einem Ausdruck festlegen. Weitere Informationen finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
 Der in dieser Prozedur verwendete Ausdruck wurde ebenfalls verwendet, um den Bericht mit Indikatoren verschiedener Größe zu erstellen, wie in [Indikatoren &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md) dargestellt.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-the-indicator-icon-size-using-an-expression"></a>So geben Sie die Symbolgröße für Indikatoren mit einem Ausdruck an  
  
1.  Klicken Sie auf den Indikator, den Sie ändern möchten.  
  
2.  Suchen Sie im Eigenschaftenbereich die IndicatorStates-Eigenschaft.  
  
     Wenn der Eigenschaftenbereich nach Kategorie organisiert ist, finden Sie IndicatorStates unter der Kategorie **Status** .  
  
3.  Klicken Sie neben IndicatorStates auf die Schaltfläche mit den Auslassungszeichen **(...)** . Das Dialogfeld **IndicatorState-Auflistungs-Editor** wird geöffnet.  
  
     Wählen Sie alle Elemente der Auflistung aus.  
  
4.  Klicken Sie in der Liste mit den **Mehrfachauswahleigenschaften** auf den Abwärtspfeil neben ScaleFactor, und klicken Sie dann auf **Ausdruck**.  
  
5.  Schreiben Sie im Dialogfeld **Ausdruck** den Ausdruck.  
  
     Der folgende Beispielausdruck ändert die Größe des Symbols basierend auf dem Wert des **SalesYTD** -Felds.  
  
     `=IIF(Fields!SalesYTD.value = 0,0,Fields!SalesYTD.value/Max(Fields!SalesYTD.value,"Indicator"))`  
  
     Weitere Informationen finden Sie unter [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Indikatoren &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
