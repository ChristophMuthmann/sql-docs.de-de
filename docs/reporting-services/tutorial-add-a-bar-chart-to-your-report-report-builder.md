---
title: "Tutorial: Hinzufügen eines Balkendiagramms zu einem Bericht (Berichts-Generator) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
caps.latest.revision: "14"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 6039892e8cdd711102c2c3f647b0a201723b0eef
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>Tutorial: Hinzufügen eines Balkendiagramms zu einem Bericht (Berichts-Generator)
In diesem Tutorial verwenden Sie einen Assistenten in [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] , um ein Kreisdiagramm in einem paginierten [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Bericht zu erstellen. Anschließend fügen Sie einen Filter hinzu und erweitern das Diagramm. 

In einem Balkendiagramm werden Kategoriedaten horizontal angezeigt. Diese Darstellung bietet folgende Vorteile:  
  
-   Bessere Lesbarkeit langer Kategorienamen  
-   Bessere Verständlichkeit von Zeiten, die als Werte ausgegeben werden   
-   Vergleichen des relativen Werts mehrerer Reihen  
  
Die folgende Abbildung zeigt das zu erstellende Balkendiagramm mit den Umsätzen der fünf besten Vertriebsmitarbeiter für die Jahre 2014 und 2015 vom niedrigsten bis zum höchsten Umsatz im Jahr 2015.  
  
![Berichts-Generator-Balkendiagramm](../reporting-services/media/report-builder-bar-chart.png) 
  
 
> [!NOTE]  
> In diesem Lernprogramm werden die Schritte für den Assistenten in einem Verfahren zusammengefasst. Detaillierte Anweisungen zum Navigieren zu einem Berichtsserver, zum Erstellen eines Datasets und zum Auswählen einer Datenquelle finden Sie im ersten Tutorial dieser Reihe unter [Tutorial: Erstellen eines einfachen Tabellenberichts (Berichts-Generator)](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Geschätzte Zeit zum Bearbeiten dieses Tutorials: 15 Minuten.  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Anforderungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Chart"></a>1. Erstellen eines Diagrammberichts mithilfe des Diagramm-Assistenten  
Darin erstellen Sie ein eingebettetes Dataset, wählen eine freigegebene Datenquelle aus, und erstellen mithilfe des Diagramm-Assistenten ein Balkendiagramm.  
  
> [!NOTE]  
> In diesem Tutorial sind die Datenwerte in der Abfrage enthalten, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) aus dem [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Webportal, vom Berichtsserver im integrierten SharePoint-Modus oder von Ihrem Computer.  
  
     Das Dialogfeld **Erste Schritte** wird angezeigt.  
  
     ![Erste Schritte mit dem Berichts-Generator](../reporting-services/media/rb-getstarted.png "Report Builder Get Started")  
  
     Wenn das Dialogfeld **Erste Schritte** nicht angezeigt wird, klicken Sie auf **Datei** >**Neu**. Das Dialogfeld **Neuer Bericht oder neues Dataset** verfügt größtenteils über den gleichen Inhalt wie das Dialogfeld **Erste Schritte** . 
      
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist.  
  
3.  Klicken Sie im rechten Bereich auf **Diagramm-Assistent**.  
  
4.  Klicken Sie auf der Seite **Dataset auswählen** auf **Dataset erstellen**und anschließend auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Verbindung mit einer Datenquelle auswählen** eine vorhandene Datenquelle aus, oder navigieren Sie zum Berichtsserver, und wählen Sie eine Datenquelle aus. Klicken Sie anschließend auf **Weiter**. Möglicherweise müssen Benutzername und Kennwort eingegeben werden.  
  
    > [!NOTE]  
    > Welche Datenquelle Sie auswählen, ist unwichtig, solange Sie über ausreichende Berechtigungen verfügen. Aus der Datenquelle werden keine Daten abgerufen. Weitere Informationen finden Sie unter [Alternative Methoden zum Herstellen einer Datenverbindung (Berichts-Generator)](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Klicken Sie auf der Seite **Abfrage entwerfen** auf **Als Text bearbeiten**.  
  
7.  Fügen Sie die folgende Abfrage in den Abfragebereich ein:  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2015, CAST(150000. AS money) AS SalesYear2014  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(190000. AS money) AS SalesYear2014  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2015, CAST(195000. AS money) AS SalesYear2014  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(160000. AS money) AS SalesYear2014  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(220000. AS money) AS SalesYear2014  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(215000. AS money) AS SalesYear2014  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2015, CAST(207000. AS money) AS SalesYear2014  
    ```  
  
8.  (Optional) Klicken Sie auf die Schaltfläche „Ausführen“ (**!**), um die Daten anzuzeigen, auf denen das Diagramm basiert.  
  
9. Klicken Sie auf **Weiter**.  
  
## <a name="ChartType"></a>2. Erstellen eines Balkendiagramms  
 
1.  Das Säulendiagramm ist der Standarddiagrammtyp der Seite **Diagrammtyp auswählen** .  
  
2.  Klicken Sie auf **Balken**und anschließend auf **Weiter**.  
  
    Auf der Seite **Diagrammfelder anordnen** stehen im Bereich **Verfügbare Felder** vier Felder zur Verfügung: „FirstName“, „LastName“, „SalesYear2015“ und „SalesYear2014“.  
  
3.  Ziehen Sie "LastName" in den Bereich "Kategorien".  
  
4.  Ziehen Sie „SalesYear2015“ in den Bereich „Werte“. „SalesYear2015“ steht für den Umsatz der einzelnen Vertriebsmitarbeiter im Jahr 2015. Im Bereich Werte wird `[Sum(SalesYear2015)]` angezeigt, da im Diagramm der aggregierte Wert für die einzelnen Produkte angezeigt wird.  
  
5.  Ziehen Sie „SalesYear2014“ im Bereich „Werte“ unter „SalesYear2015“. „SalesYear2014“ steht für den Umsatz der einzelnen Vertriebsmitarbeiter im Jahr 2014.  
  
6.  Klicken Sie auf **Weiter**.  
  
7.  Klicken Sie auf **Fertig stellen**.  
  
    Das Diagramm wird der Entwurfsoberfläche hinzugefügt. Beachten Sie, dass das neue Balkendiagramm nur aussagekräftige Daten zeigt. Statt der Namen der Personen enthält die Legende Last Name A, Last Name B usw., um Ihnen einen Überblick zu übermitteln, wie Ihr Bericht aussehen wird. 
  
9. Klicken Sie auf das Diagramm, um die Diagrammziehpunkte anzuzeigen. Ziehen Sie die rechte untere Ecke des Diagramms, um das Diagramm zu vergrößern. Beachten Sie, dass sich die Entwurfsoberfläche beim Ziehen vergrößert. 
  
10. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Das Balkendiagramm zeigt die Umsätze der einzelnen Vertriebsmitarbeiter in den Jahren 2014 und 2015 an. Die Balkenlänge entspricht dem jeweiligen Gesamtumsatz.  
  
## <a name="AllValues"></a>3. Anzeigen aller Namen auf der vertikalen Achse  
Standardmäßig werden auf der vertikalen Achse nur einige der Werte angezeigt. Sie können das Diagramm so ändern, dass alle Kategorien angezeigt werden.  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie mit der rechten Maustaste auf die vertikale Achse, und klicken Sie anschließend auf **Eigenschaften für vertikale Achsen**.  
  
3.  Geben Sie unter **Achsenbereich und -intervall**im Feld **Intervall** den Wert **1**ein.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
> [!NOTE]  
> Wenn Sie die Namen der Vertriebsmitarbeiter auf der vertikalen Achse nicht lesen können, können Sie das Diagramm vergrößern oder die Formatierungsoptionen für die Achsenbezeichnungen ändern.  
  
### <a name="CategoryExpression"></a>Anzeigen der Nachnamen und Vornamen auf der vertikalen Achse  
Sie können den Kategorieausdruck so ändern, dass die Nach- und Vornamen der einzelnen Vertriebsmitarbeiter angezeigt werden.  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Doppelklicken Sie auf das Diagramm, um den Bereich **Diagrammdaten** anzuzeigen.  
  
3.  Klicken Sie mit der rechten Maustaste im Bereich **Kategoriegruppen** auf „[LastName]“, und klicken Sie anschließend auf **Kategoriegruppeneigenschaften**.  
  
4.  Klicken Sie unter "Bezeichnung" auf die Ausdrucksschaltfläche ("Fx").  
  
5.  Geben Sie den folgenden Ausdruck ein: `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
    Durch diesen Ausdruck wird eine Verkettung aus dem Nachnamen, einem Komma und dem Vornamen erstellt.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Sollten beim Ausführen des Berichts keine Vornamen angezeigt werden, können Sie die Daten manuell aktualisieren. Klicken Sie im Vorschaumodus auf der Registerkarte **Ausführen** in der Gruppe **Navigation** auf **Aktualisieren**.  
  
> [!NOTE]  
> Wenn Sie die Namen der Vertriebsmitarbeiter auf der vertikalen Achse nicht lesen können, können Sie das Diagramm vergrößern oder die Formatierungsoptionen für die Achsenbezeichnungen ändern.  
  
## <a name="Sort"></a>4. Ändern der Sortierreihenfolge der vertikalen Achse  
Beim Sortieren der Daten eines Diagramms wird die Reihenfolge der Werte auf der Kategorieachse geändert.  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Doppelklicken Sie auf das Diagramm, um den Bereich **Diagrammdaten** anzuzeigen.  
  
3.  Klicken Sie mit der rechten Maustaste im Bereich **Kategoriegruppen** auf „[LastName]“, und klicken Sie anschließend auf **Kategoriegruppeneigenschaften**.  
  
4.  Klicken Sie auf **Sortierung**. Auf der Seite **Ändern Sie die Sortieroptionen** wird eine Liste mit Sortierausdrücken angezeigt. Standardmäßig enthält diese Liste einen einzelnen Sortierungsausdruck, der dem ursprünglichen Kategoriegruppenausdruck entspricht.  
  
5.  Klicken Sie unter **Sortieren nach**auf **[SalesYear2015]**.  
  
6.  Wählen Sie in der Liste **Reihenfolge** **A bis Z** aus, sodass die Namen in der Reihenfolge vom höchsten bis zum niedrigsten Umsatz im Jahr 2015 angezeigt werden.
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Die Namen auf der horizontalen Achse werden von den höchsten bis zu den niedrigsten Umsätzen im Jahr 2015 sortiert, **Zeng** steht also ganz oben.  
  
## <a name="Legend"></a>5. Verschieben der Legende  
Um die Lesbarkeit der Diagrammwerte zu verbessern, können Sie gegebenenfalls die Diagrammlegende verschieben. So können Sie zum Beispiel in einem Balkendiagramm mit einer horizontalen Anordnung der Balken die Legende oberhalb oder unterhalb des Diagrammbereichs platzieren. Dann bleibt horizontal mehr Platz für die Balken.  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>So zeigen Sie die Legende unterhalb des Diagrammbereichs eines Balkendiagramms an  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Legende des Diagramms.  
  
3.  Wählen Sie **Legendeneigenschaften**aus.  
  
4.  Wählen Sie unter **Legendenposition**eine andere Position aus. Legen Sie z. B. eine Position unten in der Mitte fest.  
  
    Wenn Sie die Legende über oder unter einem Diagramm platzieren, ändert sich das Layout der Legende von vertikal zu horizontal. In der Dropdownliste **Layout** können Sie ein anderes Layout auswählen.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
## <a name="ChartTitle"></a>6. Benennen des Diagramms  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Markieren Sie am oberen Diagrammrand den Text **Diagrammtitel** , und geben Sie anschließend den Text **Umsätze für 2014 und 2015**ein.  
  
3.  Legen Sie bei ausgewähltem Titel im Bereich „Eigenschaften“ folgende Werte fest: **Farbe** auf **Schwarz** und **Schriftgrad** auf **12 pt**. 
  
4.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
## <a name="Horizontal"></a>7. Formatieren und Beschriften der horizontalen Achse  
Standardmäßig werden die Werte auf der horizontalen Achse in einem allgemeinen Format angezeigt, dessen Größe automatisch an die Diagrammgröße angepasst wird. Sie können es in das Währungsformat ändern.  
   
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie unten im Diagramm auf die horizontale Achse, um sie auszuwählen.  
  
3.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Number** (Zahl) auf **Currency** (Währung). Die horizontalen Achsenbezeichnungen werden zu Währungsbezeichnungen geändert.  
  
3.  (Optional) Entfernen Sie die Dezimalstellen. Klicken Sie in der Nähe der Schaltfläche **Währung** zweimal auf die Schaltfläche **Dezimalstelle löschen** .  
  
4.  Klicken Sie mit der rechten Maustaste auf die horizontale Achse, und klicken Sie anschließend auf **Eigenschaften für horizontale Achsen**.  
  
5.  Wählen Sie auf der Registerkarte **Zahl** die Option aus, mit der **Werte als Tausender-Werte angezeigt werden**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

8.  Klicken Sie mit der rechten Maustaste auf die horizontale Achse, und wählen Sie **Achsentitel anzeigen**aus.
  
7.  Geben Sie im Feld **Achsentitel** den Text **Sales in thousands** ein, und drücken Sie die EINGABETASTE.  

    >**Hinweis:** Während Sie tippen, erscheint es so, als würde sich das Feld „Achsentitel“ auf der vertikalen Achse befinden. Wenn Sie jedoch die EINGABETASTE drücken, wird es zur horizontalen Achse verschoben.
  
9. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Auf der horizontalen Achse des Berichts werden die Umsätze als Währung in Tausendern ohne Dezimalstellen angezeigt.  
  
## <a name="Filter"></a>8. Hinzufügen eines Filters zum Anzeigen der fünf besten Werte  
Sie können dem Diagramm einen Filter hinzufügen, um anzugeben, welche Daten des Datasets ein- oder ausgeschlossen werden sollen.   
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Doppelklicken Sie auf das Diagramm, um den Bereich **Diagrammdaten** anzuzeigen.  
  
3.  Klicken Sie im Bereich **Kategoriegruppen** mit der rechten Maustaste auf das Feld [LastName]. Klicken Sie danach auf **Kategoriegruppeneigenschaften**.  
  
4.  Klicken Sie auf **Filter**. Die Seite **Filter ändern** zeigt eine Liste von Filterausdrücken an. Standardmäßig ist diese Liste leer.  
  
5.  Klicken Sie auf **Hinzufügen**. Ein neuer leerer Filter wird angezeigt.  
  
6.  Geben Sie unter **Ausdruck** **[Sum(SalesYear2015)]**ein. Dadurch wird der zugrunde liegende Ausdruck `=Sum(Fields!SalesYear2015.Value)`erstellt, der durch Klicken auf die Schaltfläche **fx** angezeigt wird.  
  
7.  Überprüfen Sie, ob der Datentyp gleich **Text**ist.  
  
8.  Wählen Sie in **Operator**in der Dropdownliste den Eintrag **Erste N** aus.  
  
9. Geben Sie unter **Wert**den folgenden Ausdruck ein: **=5**  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Sollten die Ergebnisse nicht gefiltert werden, wenn Sie den Bericht ausführen, können Sie die Daten manuell aktualisieren. Klicken Sie auf der Registerkarte **Ausführen** in der Gruppe **Navigation** auf **Aktualisieren**.  
  
Im Diagramm werden die Namen der fünf besten Vertriebsmitarbeiter gemäß den Umsatzdaten des Jahres 2015 angezeigt.  
  
## <a name="Title"></a>9. Hinzufügen eines Berichtstitels  
  
1.  Klicken Sie auf der Entwurfsoberfläche auf **Zum Hinzufügen eines Titels klicken**.  
  
2.  Geben Sie **Umsatz-Balkendiagramm**ein, drücken Sie die EINGABETASTE, und geben Sie anschließend **Top Five-Verkaufsschlager 2015**ein, was anschließend in etwa wie folgt aussehen sollte:  
  
    **Umsatz-Balkendiagramm**  
  
    **Top Five-Verkaufsschlager 2015**  
  
3.  Markieren Sie **Umsatz-Balkendiagramm**, und klicken Sie auf die Schaltfläche **Fett** .  
  
4.  Markieren Sie **Top Five-Verkaufsschlager 2015**, und legen Sie auf der Registerkarte **Stamm** im Abschnitt **Schriftart** den Schriftgrad auf **10**fest.  
  
5.  (Optional) Das Textfeld „Titel“ muss ggf. vergrößert werden, damit die beiden Textzeilen hineinpassen, und der obere Rand des Balkendiagramms muss heruntergezogen werden, um die beiden Textzeilen aufzunehmen.  
  
    Dieser Titel wird am Anfang des Berichts angezeigt. Ist keine Kopfzeile definiert, erfüllen die Elemente über dem Berichtshauptteil die Funktion einer Berichtskopfzeile.  
  
6.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
## <a name="Save"></a>10. Speichern des Berichts  
  
1.  Wechseln Sie zur Berichtsentwurfsansicht.  
  
2.  Klicken Sie auf **Datei** > **Speichern als**.  
  
3.  Geben Sie im Feld **Name**die Zeichenfolge **Umsatz-Balkendiagramm**ein.  

    Sie können ihn entweder auf Ihrem Computer oder auf dem Berichtsserver speichern.
  
4.  Klicken Sie auf **Speichern**.   
  
## <a name="next-steps"></a>Nächste Schritte  
Sie haben das Lernprogramm "Hinzufügen eines Balkendiagramms zu einem Bericht" erfolgreich abgeschlossen. Weitere Informationen zu Diagrammen finden Sie unter [Diagramme](../reporting-services/report-design/charts-report-builder-and-ssrs.md) und [Balkendiagramme](../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
[Lernprogramme für den Berichts-Generator](../reporting-services/report-builder-tutorials.md)  
[Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

