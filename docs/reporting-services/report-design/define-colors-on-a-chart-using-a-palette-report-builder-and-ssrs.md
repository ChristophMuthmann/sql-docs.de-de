---
title: Definieren von Farben in einem Diagramm mit einer Palette (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d95efc22-5a32-43d4-9bd2-12753e7fd395
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c244f75603ae96dad15c98411bffe223b2857b56
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs"></a>Definieren von Farben in einem Diagramm mit einer Palette (Berichts-Generator und SSRS)
  Sie können die Farbpalette für ein Diagramm durch Auswählen einer vordefinierten Palette oder durch Definieren einer benutzerdefinierten Palette ändern. Benutzerdefinierte Paletten sind berichtsspezifisch.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-colors-on-the-chart-using-a-built-in-color-palette"></a>So ändern Sie die Farben im Diagramm mit einer integrierten Farbpalette  
  
1.  Öffnen Sie den Bereich Eigenschaften.  
  
2.  Klicken Sie auf der Entwurfsoberfläche auf das Diagramm. Die Eigenschaften für das Diagrammobjekt werden im Bereich Eigenschaften angezeigt.  
  
     Der Objektname (standardmäßig**Chart1** ) wird in der Dropdownliste oben im Bereich „Eigenschaften“ aufgeführt.  
  
3.  Wählen Sie im Abschnitt **Diagramm** für die „Palette“-Eigenschaft eine neue Palette aus der Dropdownliste aus.  
  
    > [!NOTE]  
    >  Sie können die Farben oder die Reihenfolge in einer vordefinierten Palette nicht ändern.  
  
### <a name="to-define-your-own-colors-on-the-chart-using-a-custom-color-palette"></a>So definieren Sie eigene Farben im Diagramm mit einer benutzerdefinierten Farbpalette  
  
1.  Öffnen Sie den Bereich Eigenschaften.  
  
2.  Klicken Sie auf der Entwurfsoberfläche auf das Diagramm. Die Eigenschaften für das Diagrammobjekt werden im Bereich Eigenschaften angezeigt.  
  
3.  Wählen Sie im Abschnitt **Diagramm** für die Eigenschaft **Palette** die Option **Benutzerdefiniert**aus.  
  
4.  Klicken Sie in der „CustomPaletteColors“-Eigenschaft auf die Schaltfläche zum Bearbeiten der Auflistung (**…**). Das Dialogfeld **ReportColorExpression-Auflistungs-Editor** wird geöffnet.  
  
5.  Klicken Sie auf **Hinzufügen** , um eine Farbe hinzuzufügen. Wählen Sie in der Dropdownliste eine Farbe aus, oder wählen Sie Ausdruck, und geben Sie einen hexadezimalen Wert für eine bestimmte Farbe an, z. B. ff6600 für "Orange".  
  
     Weitere Informationen zu Hexadezimalwerten finden Sie unter [Color Table](http://go.microsoft.com/fwlink/?linkid=9258) auf MSDN.  
  
6.  Klicken Sie auf **Hinzufügen** , um der Palette weitere Farben hinzuzufügen.  
  
7.  Abschließend klicken Sie auf **OK**.  
  
 Wenn Sie eine benutzerdefinierte Palette verwenden, können Sie die Reihenfolge der Farben ändern, um die Farbe verschiedener Reihen im Diagramm zu ändern.  
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren von Reihenfarben in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Angeben von Farben, die für mehrere Formdiagramme konsistent sind &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
  
