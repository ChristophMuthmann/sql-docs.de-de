---
title: "Tutorial: Hinzufügen eines Säulendiagramms zu einem Bericht (Berichts-Generator) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
caps.latest.revision: "17"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b1768cbe53155ec37c5f6dd690542b90e22a59cd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>Lernprogramm: Hinzufügen eines Säulendiagramms zu einem Bericht (Berichts-Generator)
In diesem Tutorial erstellen Sie einen paginierten [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Bericht mit einem Säulendiagramm, das eine Datenreihe in Form mehrerer nach Kategorie gruppierter Säulen erstellt. 

Säulendiagramme sind für Folgendes nützlich:  
  
-   Anzeigen von Datenänderungen über einen bestimmten Zeitraum  
-   Vergleichen des relativen Werts mehrerer Reihen  
-   Anzeigen eines gleitenden Durchschnitts, um Trends darzustellen  
  
In der folgenden Abbildung sehen Sie das zu erstellende Säulendiagramm mit einem gleitenden Durchschnitt:  
  
![report-builder-column-chart-tutorial](../reporting-services/media/report-builder-column-chart-tutorial.png)    
> [!NOTE]  
> In diesem Lernprogramm werden die Schritte für den Assistenten in einem Verfahren zusammengefasst. Im ersten Tutorial dieser Reihe erhalten Sie detaillierte Anweisungen zum Navigieren zu einem Berichtsserver, zum Auswählen einer Datenquelle sowie zum Erstellen eines Datasets: [Tutorial: Erstellen eines einfachen Tabellenberichts (Berichts-Generator)](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Geschätzte Zeit zum Bearbeiten dieses Tutorials: 15 Minuten.  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Anforderungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Chart"></a>1. Erstellen eines Diagrammberichts mithilfe des Diagramm-Assistenten  
In diesem Abschnitt verwenden Sie den Diagramm-Assistenten, um ein eingebettetes Dataset zu erstellen, eine freigegebene Datenquelle auszuwählen, und ein Säulendiagramm zu erstellen.  
  
> [!NOTE]  
> Die Abfrage in diesem Tutorial enthält die Datenwerte, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
### <a name="to-create-a-chart-report"></a>So erstellen Sie einen Diagrammbericht  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
  
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist.  
  
3.  Klicken Sie im rechten Bereich auf **Diagramm-Assistent**.  
  
4.  Klicken Sie auf der Seite **Dataset auswählen**auf **Dataset erstellen**und anschließend auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Verbindung mit einer Datenquelle auswählen** eine vorhandene Datenquelle aus, oder navigieren Sie zum Berichtsserver, und wählen Sie eine Datenquelle aus. Klicken Sie anschließend auf **Weiter**. Möglicherweise müssen Benutzername und Kennwort eingegeben werden.  
  
    > [!NOTE]  
    > Welche Datenquelle Sie auswählen, ist unwichtig, solange Sie über ausreichende Berechtigungen verfügen. Aus der Datenquelle werden keine Daten abgerufen. Weitere Informationen finden Sie unter [Alternative Methoden zum Herstellen einer Datenverbindung (Berichts-Generator)](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Klicken Sie auf der Seite **Abfrage entwerfen** auf **Als Text bearbeiten**.  
  
7.  Fügen Sie die folgende Abfrage in den Abfragebereich ein:  
  
    ```  
    SELECT CAST('2015-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2015-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2015-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2015-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2015-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2015-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2015-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2015-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2015-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2015-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2015-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2015-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2015-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2015-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2015-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2015-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (Optional) Klicken Sie auf die Schaltfläche „Ausführen“ (**!**), um die Daten anzuzeigen, auf denen das Diagramm basiert.  
  
9. Klicken Sie auf **Weiter**.  
  
## <a name="ChartType"></a>2. Auswählen des Diagrammtyps  
Sie können aus mehreren vordefinierten Diagrammtypen auswählen und anschließend das Diagramm ändern, nachdem Sie den Assistenten abgeschlossen haben.  
  
### <a name="to-add-a-column-chart"></a>So fügen Sie einem Bericht ein Säulendiagramm hinzu  
  
1.  Das Säulendiagramm ist der Standarddiagrammtyp der Seite **Diagrammtyp auswählen** . Klicken Sie auf **Weiter**.  
  
2.  Ziehen Sie auf der Seite **Diagrammfelder anordnen** das Feld „SalesDate“ in **Kategorien**. Kategorien werden auf der horizontalen Achse angezeigt.  
  
3.  Ziehen Sie das Feld „Sales“ in **Werte**. Im Feld **Werte** wird „Sum(Sales)“ angezeigt, da die Summe des Gesamtumsatzwerts für jedes Datum aggregiert wird. Werte werden auf der vertikalen Achse angezeigt.  
  
4.  Klicken Sie auf **Weiter**.  
 
6.  Klicken Sie auf **Fertig stellen**.  
  
    Das Diagramm wird der Entwurfsoberfläche hinzugefügt. Beachten Sie, dass das neue Säulendiagramm nur aussagekräftige Daten zeigt. Die Legende enthält Sales Date A, Sales Date B usw., um Ihnen einen Überblick zu übermitteln, wie Ihr Bericht aussehen wird. 
    
    ![Berichts-Generator-Säulendiagramm-1-Entwurfsansicht](../reporting-services/media/report-builder-column-chart-1-design-view.png)
  
7.  Klicken Sie auf das Diagramm, um die Diagrammziehpunkte anzuzeigen. Ziehen Sie die rechte untere Ecke des Diagramms, um das Diagramm zu vergrößern. Die Berichtsentwurfsoberfläche wird vergrößert, um genügend Platz für das Diagramm zu bieten.  
  
8.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  

    ![Berichts-Generator-Säulendiagramm-1-Vorschau](../reporting-services/media/report-builder-column-chart-1-preview.png)

Beachten Sie, dass im Diagramm nicht jede Kategorie auf der horizontalen Achse beschriftet ist. Standardmäßig werden nur Bezeichnungen aufgenommen, die neben die Achse passen. 
  
## <a name="Horizontal"></a>3. Formatieren eines Datums auf der horizontalen Achse  
Standardmäßig werden die Werte auf der horizontalen Achse in einem allgemeinen Format angezeigt, dessen Größe automatisch an die Diagrammgröße angepasst wird.  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie mit der rechten Maustaste auf die horizontale Achse und anschließend auf **Eigenschaften für horizontale Achsen**.  
  
3.  Klicken Sie auf **Nummer** , und wählen Sie unter **Kategorie**die Option **Datum**aus.  
  
5.  Wählen Sie im Feld **Typ** die Option **31. Jan. 2000**aus.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Klicken Sie auf der Registerkarte „Stamm“ auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Das Datum wird im ausgewählten Datumsformat angezeigt. Im Diagramm wird immer noch nicht jede Kategorie auf der horizontalen Achse beschriftet. 

![Berichts-Generator-Säulendiagramm-2-Vorschau](../reporting-services/media/report-builder-column-chart-2-preview.png)
  
Sie können die Bezeichnungsanzeige anpassen, indem Sie die Bezeichnungen drehen und das Intervall angeben.  
  
## <a name="4-rotate-the-axis-labels-on-the-horizontal-axis"></a>4. Rotieren der Achsenbezeichnungen auf der horizontalen Achse  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Titel der horizontalen Achse und anschließend auf **Achsentitel anzeigen** , um den Titel zu entfernen. Da auf der horizontalen Achse Datumsangaben angezeigt werden, wird der Titel nicht benötigt.  
  
3.  Klicken Sie mit der rechten Maustaste auf die horizontale Achse und anschließend auf **Eigenschaften für horizontale Achsen**.  
  
5.  Wählen Sie auf der Registerkarte **Bezeichnungen** unter **Optionen für automatische Anpassung von Achsenbezeichnungen ändern** **Automatische Anpassung deaktivieren**aus.  
  
7.  Wählen Sie in **Drehwinkel für Bezeichnungen**den Wert **-90**aus.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Der Beispieltext für die horizontale Achse wird um 90 Grad gedreht.  
    
    ![Berichts-Generator-Säulendiagramm-Rotieren-der-X-Achse](../reporting-services/media/report-builder-column-chart-rotate-x-axis.png)
  
9. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Im Diagramm werden die Bezeichnungen gedreht.  

![Berichts-Generator-Säulendiagramm-1-Rotieren-der-X-Achse-Vorschau](../reporting-services/media/report-builder-column-chart-rotate-x-axis-preview.png)
  
## <a name="Legend"></a>5. Verschieben der Legende  
Die Legende wird automatisch auf Basis der Kategorie- und Reihendaten erstellt. Sie können die Legende unter den Diagrammbereich eines Säulendiagramms verschieben.  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Legende des Diagramms und anschließend auf **Legendeneigenschaften**.  
  
3.  Wählen Sie unter **Layout und Position**eine andere Position aus. Wählen Sie z.B. die Option unten in der Mitte aus.  
  
    Wenn Sie die Legende über oder unter einem Diagramm platzieren, ändert sich das Layout der Legende von vertikal zu horizontal. Im Feld **Layout** können Sie ein anderes Layout auswählen.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (Optional) Da es nur eine Kategorie in diesem Tutorial gibt, benötigt das Diagramm keine Legende. Klicken Sie mit der rechten Maustaste auf die Legende und anschließend auf **Legende löschen**, um sie zu entfernen.  
  
6.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
## <a name="ChartTitle"></a>6. Benennen des Diagramms  
    
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Markieren Sie am oberen Diagrammrand den Text **Diagrammtitel** , und geben Sie anschließend den Text **Store Sales Order Totals**ein.  
  
3.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
## <a name="Vertical"></a>7. Formatieren und Beschriften der vertikalen Achse  
Standardmäßig werden die Werte auf der vertikalen Achse in einem allgemeinen Format angezeigt, dessen Größe automatisch an die Diagrammgröße angepasst wird.   
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2. Klicken Sie neben dem Diagramm auf die Bezeichnungen der vertikalen Achse, um sie auszuwählen.  
  
3.  Klicken Sie auf der Registerkarte **Stamm** unter **Zahl** auf die Schaltfläche **Währung**. Die Achsenbezeichnungen werden nun im Währungsformat dargestellt.  
  
4.  Klicken Sie zweimal auf die Schaltfläche **Dezimalstellen verringern** , damit die Zahl auf einen vollständigen Dollarbetrag gerundet wird.  
  
5.  Klicken Sie mit der rechten Maustaste auf die vertikale Achse und anschließend auf **Eigenschaften für vertikale Achsen**.  
  
6.  Beachten Sie, dass auf der Registerkarte **Zahl** im Feld **Kategorie** bereits die Option **Währung** ausgewählt und **Dezimalstellen** bereits auf **0** (Null) festgelegt ist.  
  
7.  Überprüfen Sie **Werte anzeigen in**. **Tausende** ist bereits ausgewählt.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Klicken Sie mit der rechten Maustaste auf die vertikale Achse und anschließend auf **Achsentitel anzeigen**. 

10. Klicken Sie mit der rechten Maustaste auf die vertikale Achse und anschließend auf **Achsentiteleigenschaften**.  
  
10. Ersetzen Sie den Text im Feld **Titeltext** durch **Sales Total (in Thousands)**. Darüber hinaus können Sie das gewünschte Format für den Titel festlegen.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  

    ![Berichts-Generator-Säulendiagramm-Format-Y-Achse](../reporting-services/media/report-builder-column-chart-format-y-axis.png)
    
## <a name="8-show-all-the-labels-on-the-horizontal-x-axis"></a>8. Anzeigen aller Bezeichnungen auf der horizontalen Achse (x-Achse)

Sie sehen, dass nur einige der Bezeichnungen auf der X-Achse angezeigt werden. In diesem Abschnitt legen Sie eine Eigenschaft im Bereich „Eigenschaften“ fest, damit alle Bezeichnungen angezeigt werden.

1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie auf das Diagramm, und wählen Sie anschließend die horizontalen Achsenbezeichnungen aus.

3. Legen Sie im Eigenschaftenbereich LabelInterval auf 1 fest.

    ![Berichts-Generator-Säulendiagramm-festlegen-von-Bezeichnungsintervall](../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    Das Diagramm sieht genauso aus wie in der Entwurfsansicht. 
    
5.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.

    ![report-builder-column-chart-label-interval-one-preview](../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    Jetzt zeigt das Diagramm alle seine Bezeichnungen an.
  
## <a name="Average"></a>9. Hinzufügen eines gleitenden Durchschnitts mit einer berechneten Reihe  

Ein gleitender Durchschnitt ist ein Mittelwert der Daten in der Reihe, die über einen Zeitraum berechnet wird. Der gleitende Durchschnitt kann Trends erkennen.
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Doppelklicken Sie auf das Diagramm, um den Bereich **Diagrammdaten** anzuzeigen.  
  
3.  Klicken Sie mit der rechten Maustaste auf das Feld **[Sum(Sales)]** im Bereich **Werte** und anschließend auf **Berechnete Reihe hinzufügen**.  

     ![Berichts-Generator-Säulendiagramm-Hinzufügen-von-berechneter-Reihe](../reporting-services/media/report-builder-column-chart-add-calculated-series.png)
  
4.  Überprüfen Sie in **Formel**, ob **Gleitender Durchschnitt** ausgewählt ist.  
  
5.  Wählen Sie in **Formelparameter festlegen**für **Zeitraum**den Wert **4**aus.  
  
6.  Wählen Sie auf der Registerkarte **Rahmen** unter **Linienstärke** **3 pt**aus.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Im Diagramm wird eine Linie angezeigt, die den gleitenden Durchschnitt für den Gesamtumsatz nach Datum darstellt – gemittelt über jeweils vier Datumsangaben. Erfahren Sie mehr über das [Hinzufügen eines gleitenden Durchschnitts zu einem Diagramm (Berichts-Generator und SSRS)](../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md). 

![Berichts-Generator-Säulendiagramm-gleitender-Durchschnitt](../reporting-services/media/report-builder-column-chart-moving-average.png)
  
## <a name="Title"></a>10. Hinzufügen eines Berichtstitels  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie auf der Entwurfsoberfläche auf **Zum Hinzufügen eines Titels klicken**.  
  
3.  Geben Sie **Umsatzdiagramm**ein, drücken Sie die EINGABETASTE, und geben Sie anschließend **Januar bis Dezember 2015**ein:  
  
    **Umsatzdiagramm**  
  
    **Januar bis Dezember 2015**  
  
4.  Wählen Sie **Umsatzdiagramm** aus, und wählen Sie auf der Registerkarte **Stamm** im Abschnitt **Schriftart** die Einstellung **Fett** aus.  
  
5.  Klicken Sie auf **January to December 2015** (Januar bis Dezember 2015), und wählen Sie auf der Registerkarte **Stamm** im Abschnitt **Schriftart** den Schriftgrad **10** aus.  
  
6.  (Optional) Das Textfeld **Titel** muss ggf. vergrößert werden, damit die beiden Textzeilen hineinpassen. Ziehen Sie den Pfeil mit den zwei Spitzen nach unten, wenn Sie in die Mitte des unteren Rands klicken. Sie müssen möglicherweise auch den oberen Rand der Tabelle verschieben, sodass der Titel nicht überlappt wird.  
  
    Dieser Titel wird oben im Bericht angezeigt. Ist keine Kopfzeile definiert, erfüllen die Elemente über dem Berichtshauptteil die Funktion einer Berichtskopfzeile.  
  
7.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
## <a name="Save"></a>11. Speichern des Berichts  
  
### <a name="to-save-the-report"></a>So speichern Sie den Bericht  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie auf die Schaltfläche "Berichts-Generator" und anschließend auf **Speichern unter**.  

    Sie können ihn entweder auf Ihrem Computer oder auf dem Berichtsserver speichern.
  
3.  Geben Sie im Feld **Name**den Text **Sales Order Column Chart**ein.  
  
4.  Klicken Sie auf **Speichern**.  
  
## <a name="next-steps"></a>Nächste Schritte  
Sie haben das Lernprogramm "Hinzufügen eines Säulendiagramms zu einem Bericht" erfolgreich abgeschlossen. Weitere Informationen zu Diagrammen finden Sie unter [Diagramme (Berichts-Generator und SSRS)](../reporting-services/report-design/charts-report-builder-and-ssrs.md) und [Sparklines und Datenbalken (Berichts-Generator und SSRS)](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
-    [Tutorials (Berichts-Generator)](../reporting-services/report-builder-tutorials.md) 
-    [Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

