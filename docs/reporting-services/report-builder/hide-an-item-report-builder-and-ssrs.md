---
title: Ausblenden eines Elements (Berichts-Generator und SSRS) | Microsoft-Dokumentation
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
f1_keywords:
- sql13.rtp.rptdesigner.shared.visibility.f1
- "10503"
ms.assetid: 9d78f8de-959b-456f-8947-687fa6e2ba91
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 285d84aaa0f73cb8e366b6c96fcf279883591667
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="hide-an-item-report-builder-and-ssrs"></a>Ausblenden eines Elements (Berichts-Generator und SSRS)
  Legen Sie die Sichtbarkeit eines Berichtselements fest, wenn Sie ein Element basierend auf einem Berichtsparameter oder einem anderen von Ihnen angegebenen Ausdruck bedingt ausblenden möchten.  
  
 Sie können auch einen Bericht entwerfen, der dem Benutzer ermöglicht, die Sichtbarkeit von Berichtselementen durch Klicken auf Textfelder im Bericht ein- und auszublenden. Beispielsweise kann dies bei einem Drilldownbericht hilfreich sein. Weitere Informationen finden Sie unter [Hinzufügen einer Erweiterungs- oder Reduzieraktion zu einem Element &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md).  
  
 In den folgenden Verfahren wird beschrieben, wie ein Berichtselement in einem gerenderten Bericht basierend auf einer Konstante oder einem Ausdruck ein- oder ausgeblendet wird.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-a-report-item"></a>So blenden Sie ein Berichtselement aus  
  
1.  Klicken Sie in der Berichtsentwurfsansicht mit der rechten Maustaste auf das Berichtselement, und öffnen Sie die Seite **Eigenschaften** des Elements.  
  
    > [!NOTE]  
    >  Klicken Sie im Datenbereich, um eine ganze Tabelle oder Matrix auszuwählen. Klicken Sie mit der rechten Maustaste auf einen Zeilen-, Spalten- oder Eckziehpunkt, und klicken Sie anschließend auf **Tablix-Eigenschaften**.  
  
2.  Klicken Sie auf **Sichtbarkeit**.  
  
3.  Geben Sie unter **Bei erstmaliger Ausführung des Berichts**an, ob das Element ausgeblendet werden soll, wenn der Bericht erstmals angezeigt wird:  
  
    -   Um das Element anzuzeigen, klicken Sie auf **Anzeigen**.  
  
    -   Um das Element auszublenden, klicken Sie auf **Ausblenden**.  
  
    -   Klicken Sie auf **Je nach Ausdruck einblenden/ausblenden**, um einen Ausdruck anzugeben, der zur Laufzeit ausgewertet wird. Geben Sie den Ausdruck ein, oder klicken Sie auf die Ausdrucksschaltfläche (**fx**), um den Ausdruck im Dialogfeld **Ausdruck** zu erstellen.  
  
        > [!NOTE]  
        >  Wenn Sie einen Ausdruck für die Sichtbarkeit angeben, legen Sie die Hidden-Eigenschaft des Berichtselements wie im folgenden Bild dargestellt fest. Der ausgewertete Ausdruck zeigt das Berichtselement an, wenn der Wert False lautet, und blendet das Berichtselement aus, wenn der Wert True lautet.   
        > ![Properties_Visibility Dialogfeld und ausgeblendete Eigenschaft](../../reporting-services/report-builder/media/hiddenproperty-propertiesvisibility.png "Properties_Visibility dialog and Hidden property")  
  
4.  Klicken Sie zweimal auf **OK** .  
  
### <a name="to-hide-static-rows-in-a-table-matrix-or-list"></a>So blenden Sie statische Zeilen in einer Tabelle, Matrix oder Liste aus  
  
1.  Klicken Sie in der Berichtsentwurfsansicht auf die Tabelle, Matrix oder Liste, um die Zeilen- und Spaltenziehpunkte anzuzeigen.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Zeilenziehpunkt, und klicken Sie anschließend auf **Sichtbarkeit anzeigen**. Das Dialogfeld **Sichtbarkeit anzeigen** wird geöffnet.  
  
3.  Um die Sichtbarkeit festzulegen, führen Sie die Schritte 3 und 4 der ersten Prozedur aus.  
  
### <a name="to-hide-static-columns-in-a-table-matrix-or-list"></a>So blenden Sie statische Spalten in einer Tabelle, Matrix oder Liste aus  
  
1.  Wählen Sie in der Entwurfsansicht die Tabelle, Matrix oder Liste, um die Zeilen- und Spaltenziehpunkte anzuzeigen.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Spaltenziehpunkt, und klicken Sie anschließend auf **Spaltensichtbarkeit**.  
  
3.  Führen Sie im Dialogfeld **Spaltensichtbarkeit** die Schritte 3 und 4 der ersten Prozedur aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Drilldownaktion &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [Hinzufügen einer Erweiterungs- oder Reduzieraktion zu einem Element (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
