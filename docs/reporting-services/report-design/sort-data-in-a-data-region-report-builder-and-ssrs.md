---
title: Sortieren von Daten in einem Datenbereich (Berichts-Generator und SSRS) | Microsoft Docs
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
ms.assetid: 2fcb9be2-1daa-4c92-ad00-5f63cdf39f70
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 01fdabcd4005e5b3b15e6c2656daed1cff499211
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="sort-data-in-a-data-region-report-builder-and-ssrs"></a>Sortieren von Daten in einem Datenbereich (Berichts-Generator und SSRS)
  Wenn Sie bei der erstmaligen Ausführung eines Berichts die Sortierreihenfolge für Daten in einem Datenbereich ändern möchten, müssen Sie den Sortierungsausdruck für den Datenbereich oder die Datengruppe festlegen. Die Sortierungsausdruck für eine Gruppe wird automatisch auf den gleichen Wert wie der Gruppierungsausdruck festgelegt.  
  
-   Legen Sie in einem Tablix-Datenbereich den Sortierungsausdruck für den Datenbereich oder für die einzelnen Gruppen, einschließlich der Detailgruppe, fest. Enthält ein Tablix-Datenbereich nur eine Detailgruppe, können Sie mit gleichem Ergebnis einen Sortierungsausdruck in der Abfrage, für den Datenbereich oder aber für die Detailgruppe definieren.  
  
-   Legen Sie in einem Diagrammdatenbereich den Sortierungsausdruck für die Kategorie- und Reihengruppen fest, um die Sortierreihenfolgen für die einzelnen Gruppen zu steuern. Die Reihenfolge der Farben in einer Diagrammlegende wird durch den Sortierungsausdruck für die Datenpunkte in der Kategoriegruppe bestimmt.  
  
-   Daten in einen Messgerätdatenbereich müssen meist nicht sortiert werden, da auf dem Messgerät ein einzelner Wert in Bezug auf einen Bereich angezeigt wird. Wenn Sie die Daten eines Messgeräts dennoch sortieren müssen, definieren Sie zunächst eine Gruppe, und legen Sie dann den Sortierungsausdruck für die Gruppe fest.  
  
 Weitere Informationen finden Sie unter [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 Bei einem Tablix-Datenbereich können Sie auch am oberen Rand eines Spaltenheaders eine interaktive Sortierschaltfläche hinzufügen, um Benutzern die Möglichkeit zu geben, die Sortierreihenfolge von Gruppen oder Detailzeilen zu ändern. Weitere Informationen finden Sie unter [Interaktive Sortierung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-sort-data-in-a-tablix-data-region"></a>So sortieren Sie Daten in einem Tablix-Datenbereich  
  
1.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf ein Zeilenhandle, und klicken Sie anschließend auf **Tablix-Eigenschaften**.  
  
2.  Klicken Sie auf **Sortierung**.  
  
3.  Führen Sie für jeden Sortierungsausdruck die folgenden Schritte aus:  
  
    1.  Klicken Sie auf **Hinzufügen**.  
  
    2.  Geben Sie einen Ausdruck ein, nach dem die Daten sortiert werden sollen, oder wählen Sie diesen aus.  
  
    3.  Wählen Sie in der Dropdownliste der Spalte **Reihenfolge** die Sortierreihenfolge für die einzelnen Ausdrücke aus. Bei Auswahl von**A-Z** sortiert der Ausdruck in aufsteigender Reihenfolge. Bei Auswahl von**Z-A** sortiert der Ausdruck in absteigender Reihenfolge.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-values-in-a-group-including-the-details-group-for-a-tablix"></a>So sortieren Sie Werte in einer Gruppe (einschließlich der Detailgruppe) für eine Tablix  
  
1.  Klicken Sie auf der Entwurfsoberfläche auf den Tablix-Datenbereich, um ihn auszuwählen. Im Bereich "Gruppierung" werden die Zeilengruppen und Spaltengruppen für den Tablix-Datenbereich angezeigt.  
  
2.  Klicken Sie im Bereich „Zeilengruppen“ mit der rechten Maustaste auf den Gruppennamen, und klicken Sie anschließend auf **Gruppe bearbeiten**.  
  
3.  Klicken Sie im Dialogfeld **Tablix-Gruppe** auf **Sortieren**.  
  
4.  Führen Sie für jeden Sortierungsausdruck die folgenden Schritte aus:  
  
    1.  Klicken Sie auf **Hinzufügen**.  
  
    2.  Geben Sie einen Ausdruck ein, nach dem die Daten sortiert werden sollen, oder wählen Sie diesen aus.  
  
    3.  Wählen Sie in der Dropdownliste der Spalte **Reihenfolge** die Sortierreihenfolge für die einzelnen Ausdrücke aus. Bei Auswahl von**A-Z** sortiert der Ausdruck in aufsteigender Reihenfolge. Bei Auswahl von**Z-A** sortiert der Ausdruck in absteigender Reihenfolge.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-x-axis-labels-in-alphabetical-order-on-a-chart"></a>So sortieren Sie x-Achsenbezeichnungen in alphabetischer Reihenfolge in einem Diagramm  
  
1.  Klicken Sie mit der rechten Maustaste auf ein Feld in der Kategoriefeldablagezone, und klicken Sie auf **Kategoriegruppeneigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Kategoriegruppeneigenschaften** auf **Sortierung**.  
  
3.  Führen Sie für jeden Sortierungsausdruck die folgenden Schritte aus:  
  
    1.  Klicken Sie auf **Hinzufügen**.  
  
    2.  Wählen Sie den Ausdruck aus, der mit dem Gruppierungsfeld übereinstimmt. Sie können den Ausdruck für das Gruppierungsfeld überprüfen, indem Sie auf **Gruppierung**klicken.  
  
    3.  Wählen Sie in der Dropdownliste der Spalte **Reihenfolge** die Sortierreihenfolge für die einzelnen Ausdrücke aus. Bei Auswahl von**A-Z** sortiert der Ausdruck in aufsteigender alphabetischer Reihenfolge. Bei Auswahl von**Z-A** sortiert der Ausdruck in absteigender alphabetischer Reihenfolge.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-the-data-points-in-ascending-or-descending-order-on-a-chart"></a>So sortieren Sie die Datenpunkte in aufsteigender oder absteigender Reihenfolge in einem Diagramm  
  
1.  Klicken Sie mit der rechten Maustaste auf ein Feld in der Kategoriefeldablagezone, und klicken Sie auf **Kategoriegruppeneigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Kategoriegruppeneigenschaften** auf **Sortierung**.  
  
3.  Führen Sie für jeden Sortierungsausdruck die folgenden Schritte aus:  
  
    1.  Klicken Sie auf **Hinzufügen**.  
  
    2.  Wählen Sie den Ausdruck aus, der mit dem Datenfeld übereinstimmt. In den meisten Fällen ist dies ein aggregierter Wert, z. B. `=Sum(Fields!Quantity.Value)`.  
  
    3.  Wählen Sie in der Dropdownliste der Spalte **Reihenfolge** die Sortierreihenfolge für die einzelnen Ausdrücke aus. Bei Auswahl von**A-Z** sortiert der Ausdruck in aufsteigender Reihenfolge. Bei Auswahl von**Z-A** sortiert der Ausdruck in absteigender Reihenfolge.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-data-in-ascending-or-descending-order-for-display-on-a-gauge"></a>So sortieren Sie die Daten in aufsteigender oder absteigender Reihenfolge zur Anzeige auf einem Messgerät  
  
1.  Klicken Sie mit der rechten Maustaste auf das Messgerät, und klicken Sie auf **Datengruppe hinzufügen**.  
  
2.  Klicken Sie im Dialogfeld **Messgerätbereichsgruppen-Eigenschaften** bei Bedarf auf **Allgemein** .  
  
3.  Klicken Sie unter **Gruppierungsausdrücke**auf **Hinzufügen**.  
  
4.  Geben Sie unter **Gruppieren nach**einen Ausdruck ein, nach dem die Daten gruppiert werden sollen, oder wählen Sie diesen aus.  
  
5.  Wiederholen Sie die Schritte 3 und 4, bis Sie alle zu verwendenden Gruppierungsausdrücke hinzugefügt haben.  
  
6.  Klicken Sie auf **Sortierung**.  
  
7.  Führen Sie für jeden Sortierungsausdruck die folgenden Schritte aus:  
  
    1.  Klicken Sie auf **Hinzufügen**.  
  
    2.  Wählen Sie den Ausdruck aus, der mit dem Gruppierungsfeld übereinstimmt. Sie können den Ausdruck für das Gruppierungsfeld überprüfen, indem Sie auf **Gruppierung**klicken.  
  
    3.  Wählen Sie in der Dropdownliste der Spalte **Reihenfolge** die Sortierreihenfolge für die einzelnen Ausdrücke aus. Bei Auswahl von**A-Z** sortiert der Ausdruck in aufsteigender Reihenfolge. Bei Auswahl von **Z-A** sortiert der Ausdruck in absteigender Reihenfolge.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Weitere Informationen zur Gruppierung von Daten auf einem Messgerät finden Sie unter [Messgeräte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Hilfe zu Dialogfeldern, Bereichen und Assistenten in Berichts-Generator](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [Diagramme &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formatieren von Achsenbezeichnungen in einem Diagramm &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Geben Sie konsistente Farben für mehrere Formdiagramme &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
  

