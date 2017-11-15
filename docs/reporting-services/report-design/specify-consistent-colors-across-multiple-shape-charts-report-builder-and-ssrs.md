---
title: "Angeben von Farben, die in mehreren Formdiagramme konsistent sind – Berichts-Generator und SSRS | Microsoft-Dokumentation"
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
ms.assetid: d52f68e9-2ba7-4bff-9053-4089e5164ab4
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 661d22ed1d594af2c282b61ec28eaaa37bd6821d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs"></a>Angeben von Farben, die für mehrere Formdiagramme konsistent sind (Berichts-Generator und SSRS)
  Bei anderen Diagrammen als Formdiagrammen in paginierten Berichten wählt [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] eine neue Farbe anhand des Indexes von Reihen im Diagramm aus. Beispielsweise wird die erste Reihe im Diagramm der ersten Farbe in der Palette zugeordnet. Formdiagramme weisen jedoch ein anderes Verhalten auf. Bei Formdiagrammen wird jede Farbe in der Palette einem Datenpunkt im Dataset zugeordnet. Beispielsweise wird Datenpunkt 1 der ersten Farbe in der Palette zugeordnet, Datenpunkt 2 wird der zweiten Farbe in der Palette zugeordnet usw.  
  
 Wenn ein Datenpunkt keinen Wert aufweist, wird er nicht im Formdiagramm angezeigt. Dies bedeutet, dass dem Datenpunkt keine Farbe zugewiesen wird. Wenn beispielsweise Punkt 2 den Wert 0 (null) aufweist, wird Punkt 1 der ersten Farbe in der Palette und Punkt 3 der zweiten Farbe in der Palette zugeordnet. Dieses Prinzip weist den Vorteil auf, dass für leere Punkte im Dataset eines Kreisdiagramms nicht unnötigerweise eine Palettenfarbe verwendet wird, wenn die leeren Punkte nicht gezeichnet werden müssen.  
  
 Als Nebeneffekt werden möglicherweise in einem Bericht, in dem mehrere Kreisdiagramme angezeigt werden, in den Kreisdiagrammen unterschiedliche Farben für Datenpunkte angezeigt, die derselben Kategoriegruppe angehören. Um dieses Problem zu lösen, müssen Sie einzelne Farben definieren, die nicht einzelnen Datenwerten, sondern einer Kategoriegruppe zugeordnet sind. Die Vorgehensweise hängt hierbei davon ab, ob die Formdiagramme Sparklines in einer Tabelle oder Matrix sind, oder ob sie Formdiagramme im Bericht selbst sind.  
  
 Die Legende ist mit der Reihe verknüpft. Daher wird jede Farbe, die Sie für die Reihe angeben, automatisch in der Legende angezeigt.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-consistent-colors-across-multiple-sparkline-shape-charts-in-a-table-or-matrix"></a>So legen Sie konsistente Farben für mehrere Sparkline-Formdiagramme in einer Tabelle oder einer Matrix fest  
  
1.  Klicken Sie zum Anzeigen des Bereichs Diagrammdaten auf das Diagramm.  
  
2.  Klicken Sie im Bereich **Kategoriegruppen** mit der rechten Maustaste auf eine Kategorie, und klicken Sie dann auf **Kategoriegruppeneigenschaften**.  
  
3.  Klicken Sie auf der Registerkarte Allgemein im Feld **Gruppen synchronisieren in** auf den Namen der Kategorie, für die die Farben synchronisiert werden sollen, und klicken Sie dann auf **OK**.  
  
## <a name="to-specify-consistent-colors-across-multiple-shape-charts"></a>So geben Sie konsistente Farben für mehrere Formdiagramme an  
  
1.  Klicken Sie mit der rechten Maustaste außerhalb des Hauptteils des Berichts, und wählen Sie **Berichtseigenschaften**aus.  
  
2.  Geben Sie in **Code**den folgenden Code in das Textfeld ein.  
  
    ```  
    Private colorPalette As String() = {"Color1", "Color2", "Color3"}  
    Private count As Integer = 0  
    Private mapping As New System.Collections.Hashtable()  
    Public Function GetColor(ByVal groupingValue As String) As String  
        If mapping.ContainsKey(groupingValue) Then  
            Return mapping(groupingValue)  
        End If  
        Dim c As String = colorPalette(count Mod colorPalette.Length)  
        count = count + 1  
        mapping.Add(groupingValue, c)  
        Return c  
    End Function  
    ```  
  
    > [!NOTE]  
    >  Sie müssen die Zeichenfolgen "Color1", "Color2" usw. durch eigene Farben ersetzen. Sie können benannte Farben, z. B. "Red", verwenden, oder Sie können einen sechsstelligen Hexadezimalwert verwenden, der die Farbe darstellt, z. B. "#FFFFFF" für Schwarz. Wenn mehr als drei Farben definiert sind, müssen Sie das Array der Farben so erweitern, dass die Anzahl der Farben im Array mit der Anzahl von Punkten im Formdiagramm übereinstimmt. Sie können dem Array neue Farben hinzufügen, indem Sie eine durch Trennzeichen getrennte Liste von Zeichenfolgenwerten angeben, die benannte Farben oder hexadezimale Darstellungen von Farben enthalten.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Klicken Sie mit der rechten Maustaste auf das Formdiagramm, und wählen Sie **Reiheneigenschaften**aus.  
  
5.  Klicken Sie unter **Ausfüllen**auf die **Ausdrucksschaltfläche** (*fx*), um den Ausdruck für die Eigenschaft **Farbe** zu bearbeiten.  
  
6.  Geben Sie den folgenden Ausdruck ein, wobei "MyCategoryField" das Feld ist, das im Bereich **Kategoriegruppen** angezeigt wird:  
  
    ```  
    =Code.GetColor(Fields!MyCategoryField)  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren von Reihenfarben in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Hinzufügen einer Abschrägung, Prägung und Struktur zu einem Diagramm (Berichts-Generator und SSRS)](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [Definieren von Farben in einem Diagramm mit einer Palette (Berichts-Generator und SSRS)](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Hinzufügen von leeren Punkten zum Diagramm (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)   
 [Formdiagramme (Berichts-Generator und SSRS)](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [Verknüpfen mehrerer Datenbereiche mit einem Dataset &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Geschachtelte Datenbereiche &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [Sparklines und Datenbalken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
