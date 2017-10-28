---
title: "Lernprogramm: Hinzufügen eines Kreisdiagramms zu einem Bericht (Berichts-Generator) | Microsoft Docs"
ms.custom: 
ms.date: 06/15/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
caps.latest.revision: 14
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e28719a7ee1f1610e8e673711958592837198046
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>Tutorial: Hinzufügen eines Kreisdiagramms zu einem Bericht (Berichts-Generator)
In diesem Tutorial erstellen Sie ein Kreisdiagramm in einem paginierten Reporting Services-Bericht. Sie fügen Prozentsätze hinzu und kombinieren kleine Slices zu einem einzelnen Slice.

Kreis- und Ringdiagramme zeigen Daten als Teile des Ganzen an. Sie haben keine Achsen. Wenn Sie ein numerisches Feld zu einem Kreisdiagramm hinzufügen, berechnet das Diagramm den prozentualen Anteil jedes einzelnen Werts der Gesamtsumme.  

Diese Abbildung zeigt das Kreisdiagramm, das Sie erstellen. 
 
![Berichts-Generator-Kreisdiagramm-fertig](../reporting-services/media/report-builder-pie-chart-final.png)
  
Wenn in einem Kreisdiagramm zu viele Datenpunkte vorhanden sind, können die Datenpunktbezeichnungen zu überfüllt sein, um sie zu lesen. Erwägen Sie in diesem Fall eine Anzahl von kleinen Slices zu einem größeren Slice zu kombinieren. Kreisdiagramme sind besser lesbar, wenn Sie die Daten bereits zu einer kleineren Anzahl von Datenpunkten aggregiert haben.  
 
> [!NOTE]  
> In diesem Lernprogramm werden die Schritte für den Assistenten in zwei Verfahren zusammengefasst. Im ersten Tutorial dieser Reihe erhalten Sie detaillierte Anweisungen zum Navigieren zu einem Berichtsserver, Hinzufügen einer Datenquelle und Hinzufügen eines Datasets: [Tutorial: Erstellen eines einfachen Tabellenberichts &#40;Berichts-Generator&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Ungefähre Dauer dieses Lernprogramms: 10 Minuten  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Anforderungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Chart"></a>1. Erstellen eines Kreisdiagramms im Diagramm-Assistenten  
In diesem Abschnitt verwenden Sie den Diagramm-Assistenten, um ein eingebettetes Dataset zu erstellen, eine freigegebene Datenquelle auszuwählen, und ein Kreisdiagramm zu erstellen.  

  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
  
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist.  
  
3.  Klicken Sie im rechten Bereich auf **Diagramm-Assistent**.  
  
4.  Klicken Sie auf der Seite **Dataset auswählen** auf **Dataset erstellen**und anschließend auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Verbindung mit einer Datenquelle auswählen** eine vorhandene Datenquelle aus, oder navigieren Sie zum Berichtsserver, und wählen Sie eine Datenquelle aus. Klicken Sie anschließend auf **Weiter**. Möglicherweise müssen Benutzername und Kennwort eingegeben werden.  
  
    > [!NOTE]  
    > Welche Datenquelle Sie auswählen, ist unwichtig, solange Sie über ausreichende Berechtigungen verfügen. Aus der Datenquelle werden keine Daten abgerufen. Weitere Informationen finden Sie unter [Alternative Methoden zum Herstellen einer Datenverbindung &#40;Berichts-Generator&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Klicken Sie auf der Seite **Abfrage entwerfen** auf **Als Text bearbeiten**.  
  
7.  Fügen Sie die folgende Abfrage in den Abfragebereich ein:  

    > [!NOTE]  
    > In diesem Tutorial sind die Datenwerte in der Abfrage enthalten, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
    ```  
    SELECT 'Advanced Digital Camera' AS Product, CAST(254995.21 AS money) AS Sales  
    UNION SELECT 'Slim Digital Camera' AS Product, CAST(164499.04 AS money) AS Sales  
    UNION SELECT 'SLR Digital Camera' AS Product, CAST(782176.79 AS money) AS Sales  
    UNION SELECT 'Lens Adapter' AS Product, CAST(36333.08 AS money) AS Sales  
    UNION SELECT 'Macro Zoom Lens' AS Product, CAST(40199.3 AS money) AS Sales  
    UNION SELECT 'USB Cable' AS Product, CAST(53245.5 AS money) AS Sales  
    UNION SELECT 'Independent Filmmaker Camcorder' AS Product, CAST(452288.0 AS money) AS Sales  
    UNION SELECT 'Full Frame Digital Camera' AS Product, CAST(247250.85 AS money) AS Sales  
    ```  
  
8.  (Optional) Klicken Sie auf die Schaltfläche „Ausführen“ (**!**), um die Daten anzuzeigen, auf denen das Diagramm basiert.  
  
9. Klicken Sie auf **Weiter**.  
  
## <a name="ChartType"></a>2. Auswählen des Diagrammtyps  
Sie können aus einer Vielzahl vordefinierter Diagrammtypen auswählen.  

  
1.  Klicken Sie auf der Seite **Diagrammtyp auswählen** auf **Kreis**und anschließend auf **Weiter**. Die Seite **Diagrammfelder anordnen** wird geöffnet.  
  
    Ziehen Sie auf der Seite **Diagrammfelder anordnen** das Feld „Product“ in den Bereich **Kategorien** . Kategorien definieren die Anzahl von Slices im Kreisdiagramm. In diesem Beispiel werden acht Slices verwendet, eines für jedes Produkt.  
  
2.  Ziehen Sie das Feld „Sales“ in den Bereich **Werte** . Das Feld "Sales" stellt den Umsatz für die Unterkategorie dar. Im Bereich **Werte** wird `[Sum(Sales)]` angezeigt, da im Diagramm der aggregierte Wert für die einzelnen Produkte angezeigt wird.  
  
3.  Klicken Sie auf **Weiter** , um eine Vorschau anzuzeigen.  
  
5.  Klicken Sie auf **Fertig stellen**.  
  
    Das Diagramm wird der Entwurfsoberfläche hinzugefügt. Die tatsächlichen Werte des Diagramms werden nicht angezeigt – es wird Product 1, Product 2 usw. angezeigt, um einen Überblick zu übermitteln, wie das Diagramm aussehen wird.  
    
    ![Berichts-Generator-Kreisdiagramm-erster-Entwurf](../reporting-services/media/report-builder-pie-chart-first-design.png)
  
6.  Klicken Sie auf das Diagramm, um die Diagrammziehpunkte anzuzeigen. Ziehen Sie an der unteren rechten Ecke des Diagramms, um es zu vergrößern. Die Berichtsentwurfsoberfläche wird ebenso vergrößert, um genügend Platz für das Diagramm zu bieten.  
  
7.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Im Bericht wird das Kreisdiagramm mit acht Slices angezeigt, eines für jedes Produkt. Nun können Sie die tatsächlichen Produkte sehen, und die Größe der Slices stellt den Umsatz für das jeweilige Produkt dar. Drei der Slices sind relativ dünn.  

![Berichts-Generator-Kreisdiagramm-erste-Vorschau](../reporting-services/media/report-builder-pie-chart-first-preview.png)
  
## <a name="Percentages"></a>3. Anzeigen von Prozentsätzen in jedem Slice  
Sie können für jeden Slice des Kreisdiagramms den Prozentsatz des Slices im Vergleich zum gesamten Kreis anzeigen.  

  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Kreisdiagramm, und klicken Sie anschließend auf **Datenbezeichnungen anzeigen**. Die Datenbezeichnungen werden im Diagramm angezeigt.  
  
3.  Klicken Sie mit der rechten Maustaste auf eine Bezeichnung, und klicken Sie anschließend auf **Reihenbezeichnungseigenschaften**.  
  
4.  Geben Sie **#PERCENT** für die Option **Bezeichnungsdaten**ein.  
    
5.  (Optional) Um anzugeben, wie viele Dezimalstellen die Bezeichnung zeigt, in der **bezeichnen können** nach Feld **#PERCENT**, Typ **{Pn}** , in denen  *n*  ist die Anzahl der anzuzeigenden Dezimalstellen. Geben Sie z.B. **#PERCENT{P0}**ein, um keine Dezimalstellen anzuzeigen.  

6.  Die UseValueAsLabel-Eigenschaft muss zum Anzeigen von Werten als Prozentsätze auf "False" festgelegt werden. Klicken Sie auf **Ja** , wenn Sie im Dialogfeld **Aktion bestätigen**zum Festlegen dieses Werts aufgefordert werden.  
  
    > [!NOTE]  
    > Die Option**Zahlenformat** im Dialogfeld **Reihenbezeichnungseigenschaften** hat beim Formatieren von Prozentwerten keinen Einfluss auf das Format. Hierdurch werden die Bezeichnungen als Prozentwerte formatiert, die eigentlichen Prozentwerte der einzelnen Slices eines Kreisdiagramms werden jedoch nicht berechnet.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Im Bericht wird der Prozentsatz am gesamten Kreis für jeden Kreisslice angezeigt.  

![Berichts-Generator-Kreisdiagramm-Vorschau-Prozente](../reporting-services/media/report-builder-pie-chart-preview-percents.png)
  
## <a name="CombineSlices"></a>4. Kombinieren von kleinen Slices zu einem Slice  
Drei der Slices im Kreis sind relativ klein. Sie können mehrere kleine Slices zu einem größeren „Other“-Slice kombinieren, durch das alle drei Slices dargestellt werden.  

1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Sollte das Fenster „Eigenschaften“ nicht angezeigt werden, können Sie es über die Registerkarte **Ansicht** > Gruppe **Ein-/Ausblenden** > **Eigenschaften** öffnen.  
  
3.  Klicken Sie auf der Entwurfsoberfläche auf ein Segment des Kreisdiagramms. Die Eigenschaften für die Reihe werden im Bereich "Eigenschaften" angezeigt.  
  
4.  Erweitern Sie im Abschnitt **Allgemein** den Knoten **CustomAttributes** .  
  
5.  Legen Sie die Eigenschaft **CollectedStyle** auf **SingleSlice**fest.  

    ![Berichts-Generator-Kreisdiagramm-einzelne-Slice-Eigenschaft](../reporting-services/media/report-builder-pie-chart-single-slice-property.png)
 
6.  Vergewissern Sie sich, dass die **CollectedThreshold** -Eigenschaft auf 5 festgelegt ist.  
  
7.  Vergewissern Sie sich, dass die **CollectedThresholdUsePercent** -Eigenschaft auf **TRUE**festgelegt ist.  
  
8.  Klicken Sie auf der Registerkarte **Stamm** auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
In der Legende wird die Kategorie „Other“ jetzt angezeigt. Im neuen Kreisslice werden alle Slices, die kleiner als 5 % waren, zu einem Slice kombiniert, das 6 % des gesamten Kreises darstellt.  

![Berichts-Generator-Kreisdiagramm-beginnt-bei-90](../reporting-services/media/report-builder-pie-chart-start-at-90.png)
 
## <a name="DrawingEffect"></a>5. Beginnen der Kreisdiagrammwerte bei 0° 

Standardmäßig beginnt bei Kreisdiagrammen der erste Wert im Dataset bei 90 Grad zur Oberseite des Kreises versetzt. Dies wird im Kreisdiagramm in den vorherigen Abschnitten angezeigt.

In diesem Abschnitt reduzieren wir diesen Versatz auf 0°.

1.  Wechseln Sie zur Berichtsentwurfsansicht.  

2. Wählen Sie den Kreis selbst aus.

3. Ändern Sie im Bereich „Eigenschaften“ unter **Benutzerdefinierte Attribute**den Eintrag PieStartAngle von **0** in **270**.

4. Klicken Sie auf **Ausführen** , um den Bericht in der Vorschau anzuzeigen.

Jetzt sind die Segmente des Kreisdiagramms in alphabetischer Reihenfolge, beginnend am oberen Ende und endend mit dem Segment „Other“.

![Berichts-Generator-Kreisdiagramm-Beginn-oben](../reporting-services/media/report-builder-pie-chart-start-at-top.png)
  
## <a name="Title"></a>6. Hinzufügen eines Berichtstitels  
  
Da das Kreisdiagramm die einzige Visualisierung im Bericht ist, muss für das Diagramm kein eigener Titel vergeben werden. Der Berichtstitel reicht völlig aus.
  
1.  Wählen Sie im Diagramm das Feld „Diagrammtitel“ aus, und drücken Sie die Taste ENTF.

2. Klicken Sie auf der Entwurfsoberfläche auf **Zum Hinzufügen eines Titels klicken**.  
  
2.  Geben Sie wie folgt **Kamera- und Camcorderumsatz**ein, drücken Sie die EINGABETASTE, und geben Sie anschließend **Als Prozentsatz des Gesamtumsatzes**ein:  
  
    **Kamera- und Camcorderumsatz**  
  
    **Als Prozentsatz des Gesamtumsatzes**  
  
3.  Wählen Sie **Kamera- und Camcorderumsatz**, und klicken Sie auf der Registerkarte **Stamm** im Abschnitt **Schriftart** auf **Fett**.  
  
4.  Markieren Sie **Als Prozentsatz des Gesamtumsatzes**, und legen Sie auf der Registerkarte **Stamm** im Abschnitt **Schriftart** den Schriftgrad auf **10** fest.  
  
5.  (Optional) Das Textfeld "Titel" muss ggf. vergrößert werden, damit die beiden Textzeilen hineinpassen.  
  
    Dieser Titel wird am Anfang des Berichts angezeigt. Ist keine Kopfzeile definiert, erfüllen die Elemente über dem Berichtshauptteil die Funktion einer Berichtskopfzeile.  
  
6.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
## <a name="Save"></a>7. Speichern des Berichts  
  
### <a name="to-save-the-report"></a>So speichern Sie den Bericht  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie im Menü **Datei** auf **Speichern**.  
  
3.  Geben Sie im Feld **Name**den Namen **Umsatz-Kreisdiagramm**ein.  
  
4.  Klicken Sie auf **Speichern**.  
  
Der Bericht wird auf dem Berichtsserver gespeichert.  
  
## <a name="next-steps"></a>Nächste Schritte  
Sie haben das Lernprogramm "Hinzufügen eines Kreisdiagramms zu einem Bericht" erfolgreich abgeschlossen. Weitere Informationen zu Diagrammen finden Sie unter [Diagramme &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/charts-report-builder-and-ssrs.md) und [Sparklines und Datenbalken &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
[Lernprogramme für den Berichts-Generator](../reporting-services/report-builder-tutorials.md)  
[Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  


