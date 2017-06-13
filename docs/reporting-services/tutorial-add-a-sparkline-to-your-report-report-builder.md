---
title: "Lernprogramm: Hinzufügen einer Sparkline zum Bericht (Berichts-Generator) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 18c90a36-48bf-4805-a960-2d1e8f00c2dc
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c4cc42eaf9862f2154f598d6f91dafffa906c799
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---

# <a name="tutorial-add-a-sparkline-to-your-report-report-builder"></a>Lernprogramm: Hinzufügen einer Sparkline zum Bericht (Berichts-Generator)

In diesem [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)]-Tutorial erstellen Sie eine einfache Tabelle mit einem Sparkline-Diagramm in einem paginierten [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Bericht.   
  
Sparklines und Datenbalken sind einfache, kleine Diagramme, die zahlreiche Informationen auf wenig Raum vermitteln, häufig in Form von Tabellen und Matrizen in paginierten [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Berichten. Die folgende Abbildung zeigt einen Bericht, der mit dem Bericht vergleichbar ist, den Sie erstellen werden.  
  
![Berichts-Generator-Sparkline-fertig](../reporting-services/media/report-builder-sparkline-final.png)  
     
Geschätzte Zeit zum Bearbeiten dieses Lernprogramms: 30 Minuten  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Anforderungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="CreateTable"></a>1. Erstellen eines Berichts mit einer Tabelle  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)]-Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
  
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist.  
  
3.  Klicken Sie im rechten Bereich auf **Tabellen- oder Matrix-Assistent**.  
  
4.  Klicken Sie auf der Seite **Dataset auswählen** auf **Dataset erstellen**  >  **Weiter**. Die Seite **Verbindung mit einer Datenquelle auswählen** wird geöffnet.  
  
    > [!NOTE]  
    > In diesem Lernprogramm sind keine bestimmte Daten erforderlich; Es benötigt lediglich eine Verbindung mit einer SQL Server-Datenbank. Wenn unter **Datenquellenverbindungen**bereits eine Datenquellenverbindung aufgeführt ist, können Sie sie auswählen und zu Schritt 10 wechseln. Weitere Informationen finden Sie unter [Alternative Methoden zum Herstellen einer Datenverbindung &#40;Berichts-Generator&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
5.  Klicken Sie auf **Neu**. Das Dialogfeld **Datenquelleneigenschaften** wird angezeigt.  
  
6.  Geben Sie im Feld **Name**den Namen **Product Sales**für die Datenquelle ein.  
  
7.  Vergewissern Sie sich, dass unter **Verbindungstyp auswählen**die Option **Microsoft SQL Server** ausgewählt ist.  
  
8.  Geben Sie für **Verbindungszeichenfolge**den folgenden Text ein:  
  
    `Data Source\=<servername>`  
  
    Der Ausdruck `<servername>`, z.B. „Report001“, bezeichnet einen Computer, auf dem eine Instanz des SQL Server-Datenbankmoduls installiert ist. Da die Berichtsdaten nicht aus einer SQL Server-Datenbank extrahiert werden, muss der Name einer Datenbank nicht eingeschlossen werden. Die Standarddatenbank auf dem angegebenen Server wird verwendet, um die Abfrage zu analysieren.  
  
9. Klicken Sie auf **Anmeldeinformationen**. Geben Sie die für den Zugriff auf die externe Datenquelle benötigten Anmeldeinformationen ein.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Nun wird wieder die Seite **Verbindung mit einer Datenquelle auswählen** angezeigt.  
  
11. Klicken Sie auf **Verbindung testen**, um sicherzustellen, dass die Verbindung mit der Datenquelle hergestellt werden kann.  
  
    Die Meldung "Die Verbindung wurde erfolgreich hergestellt" wird angezeigt.  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. Klicken Sie auf **Weiter**.  
  
## <a name="Query"></a>2. Erstellen eines Abfrage- und Tabellenlayouts im Tabellen-Assistenten  
In einem Bericht können Sie ein freigegebenes Dataset mit einer vordefinierten Abfrage verwenden oder ein eingebettetes Dataset erstellen, das nur in Ihrem Bericht verwendet wird. In diesem Lernprogramm erstellen Sie ein eingebettetes Dataset.  
  
> [!NOTE]  
> In diesem Lernprogramm sind die Datenwerte in der Abfrage enthalten, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
### <a name="to-create-a-query-and-table-layout-in-the-table-wizard"></a>So erstellen Sie ein Abfrage- und Tabellenlayout im Tabellen-Assistenten 
  
1.  Auf der Seite **Abfrage entwerfen** ist der relationale Abfrage-Designer geöffnet. Für dieses Lernprogramm verwenden Sie den textbasierten Abfrage-Designer.  
  
2.  Klicken Sie auf **Als Text bearbeiten**. Der textbasierte Abfrage-Designer umfasst zwei Bereiche: den Abfragebereich und den Ergebnisbereich.  
  
3.  Fügen Sie die folgende [!INCLUDE[tsql](../includes/tsql-md.md)] -Abfrage in das Feld **Abfrage** ein.  
  
    ```  
    SELECT CAST('2015-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Budget Movie-Maker' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Slim Digital' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,'Accessories' as Subcategory,    
       'Budget Movie-Maker' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Carrying Case' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-04' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
4.  Klicken Sie auf der Symbolleiste des Abfrage-Designers auf „Ausführen“ (**!**).  
  
    Die Abfrage wird ausgeführt, und das Resultset für die Felder **SalesDate**, **Subcategory**, **Product**, **Sales**und **Quantity**wird angezeigt.  
  
5.  Klicken Sie auf **Weiter**.  
  
6.  Ziehen Sie auf der Seite **Felder anordnen** das Feld **Sales** in **Werte**.  
  
    **Sales** wird von der Sum-Funktion aggregiert. Der Wert ist "[Sum(Sales)]".  
  
7.  Ziehen Sie **Product** in **Zeilengruppen**.  
  
8.  Ziehen Sie **SalesDate** in **Spaltengruppen**.  

    ![Berichts-Generator-Sparkline-Felder-anordnen](../reporting-services/media/report-builder-sparkline-arrange-fields.png)
  
9. Klicken Sie auf **Weiter**.  
  
10. Vergewissern Sie sich auf der Seite **Layout auswählen** , dass unter **Optionen**die Option **Teil- und Gesamtergebnisse anzeigen** ausgewählt ist.  
  
    Im Vorschaubereich des Assistenten wird eine Tabelle mit drei Zeilen angezeigt. Bei der Ausführung des Berichts wird jede Zeile wie folgt angezeigt:  
  
    *  Die erste Zeile erscheint einmal, damit Spaltenüberschriften in der Tabelle angezeigt werden.  
  
    *  Die zweite Zeile wird einmal für jedes Produkt wiederholt. In dieser Zeile werden Produktname, Summe pro Tag und die Zeilensumme angezeigt.  
  
    *  Die dritte Zeile erscheint einmal, damit Gesamtsummen in der Tabelle angezeigt werden.  
    
    ![Berichts-Generator-Sparkline-Layout-auswählen](../reporting-services/media/report-builder-sparkline-choose-layout.png)
  
11. Klicken Sie auf **Weiter**.  
  
12. Klicken Sie auf **Fertig stellen**.  
  
14. Die Tabelle wird der Entwurfsoberfläche hinzugefügt. Die Tabelle enthält drei Spalten und drei Zeilen.  
  
    Betrachten Sie den Gruppierungsbereich. Wenn der Gruppierungsbereich nicht angezeigt wird, klicken Sie im Menü **Ansicht** auf **Gruppierung**. Im Zeilengruppenbereich wird eine Zeilengruppe angezeigt: **Product**. Im Spaltengruppenbereich wird eine Spaltengruppe angezeigt: **SalesDate**. Detaildaten sind alle Daten, die von der Datasetabfrage abgerufen werden.  
    
    ![Berichts-Generator-Sparkline-Gruppierungsbereich](../reporting-services/media/report-builder-sparkline-grouping-pane.png)
  
15. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  

### <a name="FormatCurrency"></a>2a. Formatieren von Daten als Währung  
Die Zusammenfassungsdaten für das Feld **Sales** werden standardmäßig als eine Zahl im Standardzahlenformat angezeigt. Formatieren Sie das Feld, um die Zahl als Währung anzuzeigen. Ändern Sie die Einstellung der Option **Platzhalterformate** , um formatierte Textfelder und Platzhaltertext als Beispielwerte anzuzeigen.  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zu wechseln.  
  
2.  Klicken Sie auf die Zelle in der zweiten Zeile (unter der Zeile mit den Spaltenüberschriften) in der Spalte **SalesDate** . Halten Sie die STRG-Taste gedrückt, und wählen Sie alle Zellen mit `[Sum(Sales)]`aus. 

    ![Berichts-Generator-Sum-Sales-markieren](../reporting-services/media/report-builder-select-sum-sales.png) 
  
3.  Klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Zahl** auf **Währung**. Die Zellen ändern sich, um die formatierte Währung anzuzeigen.  

    ![Berichts-Generator-Platzhalter-Währung](../reporting-services/media/report-builder-placeholder-currency.png)
  
    Wenn Sie das Gebietsschema „Deutsch (Deutschland)“ verwenden, lautet der Standardbeispieltext [**12,345.00€**]. Falls kein Beispielwährungswert angezeigt wird, klicken Sie in der Gruppe **Zahlen** auf **Platzhalterformate**  >  **Beispielwerte**.  
    
    ![Berichts-Generator-Schaltfläche-Platzhalterwert](../reporting-services/media/report-builder-placeholder-value-button.png)
   
### <a name="FormatDates"></a>2b. Formatieren von Daten als Datumsangaben (optional)  
Im Feld **SalesDate** werden standardmäßig sowohl Datums- als auch Zeitangaben angezeigt. Durch entsprechende Formatierung kann auch nur das Datum angezeigt werden.  
  
1.  Klicken Sie auf die Zelle, die `[SalesDate]` enthält.  
  
3.  Klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Zahl** auf **Datum**.  
  
    In der Zelle wird das Beispieldatum **[31.01.2000]** angezeigt.
     
4.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Die Werte für **SalesDate** werden im Standarddatumsformat angezeigt und die zusammenfassenden Werte für **Sales** als Währung.   
  
## <a name="Sparkline"></a>3. Hinzufügen einer Sparkline    
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Wählen Sie die Summenspalte in der Tabelle aus.  
  
3.  Führen Sie einen Rechtsklick aus, zeigen Sie auf **Spalte einfügen**, und klicken Sie anschließend auf **Links**.  

    ![Berichts-Generator-Spalte-links-hinzufügen](../reporting-services/media/report-builder-add-column-left.png)
  
4.  Klicken Sie in der neuen Spalte mit der Maustaste in die Zelle in der `[Product]`-Zeile und anschließend auf **Einfügen**  >  **Sparkline**.  

    ![Berichts-Generator-Sparkline-einfügen](../reporting-services/media/report-builder-insert-sparkline.png)
  
5.  Stellen Sie sicher, dass die erste Sparkline in der Zeile **Spalte** im Dialogfeld **Sparklinetyp auswählen** ausgewählt wurde, und klicken Sie anschließend auf **OK**.  
  
6.  Klicken Sie zum Anzeigen des Diagrammdatenbereichs auf die Sparkline.  
  
7.  Klicken Sie im Wertefeld auf das Pluszeichen (+) und anschließend auf **Sales**. 

    ![Berichts-Generator-Sparkline-Werte](../reporting-services/media/report-builder-sparkline-values.png) 
  
    Die Werte im Feld **Sales** sind nun die Werte für die Sparkline.  
  
8.  Klicken Sie im Feld „Kategoriegruppe“ auf das Pluszeichen (+) und anschließend auf **SalesDate**.  
  
9. Klicken Sie auf **Ausführen** , um den Bericht in der Vorschau anzuzeigen.  
  
    Beachten Sie, dass die Balken in den Diagrammen nicht einheitlich dargestellt werden. In der zweiten Datenzeile befinden sich nur vier Balken, weshalb die Balken breiter als in der ersten Zeile sind, die sechs Balken enthält. Werte für die einzelnen Produkte können nicht pro Tag verglichen werden. Daher müssen die Balken einheitlich ausgerichtet werden.  
  
    Außerdem entspricht die maximale Balkenlänge der jeweiligen Höhe der Zeile. Dies ist ebenfalls irreführend, da die größten Werte der jeweiligen Zeilen nicht identisch sind: Der größte Wert für Budget Movie-Maker beträgt USD 10.400, für Slim Digital jedoch USD 26.576 – mehr als das Doppelte. Dennoch sind die größten Balken in diesen zwei Zeilen etwa gleich hoch. Alle Sparklines müssen dieselbe Skala verwenden.  
  
     ![Berichts-Generator-Sparkline-falsch-ausgerichtet](../reporting-services/media/report-builder-sparkline-misaligned.png)
  
## <a name="AlignSparklines"></a>4. Vertikales und horizontales Ausrichten der Sparklines  
Sparklines sind schwierig zu lesen, wenn nicht durchgängig der gleiche Maßstab verwendet wird. Sowohl die horizontale als auch die vertikale Achse muss mit dem Rest übereinstimmen.  
   
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Sparkline, und klicken Sie auf **Eigenschaften für vertikale Achsen**.  
  
3.  Aktivieren Sie das Kontrollkästchen **Achsen ausrichten in** . Die einzige Option in der Liste lautet „Tablix1“.  
  
     Dadurch wird die Höhe der Balken in jeder Sparkline relativ zu den anderen Balken festgelegt. 
  
4.  Klicken Sie auf **OK**.  
  
5.  Klicken Sie mit der rechten Maustaste auf die Sparkline, und klicken Sie auf **Eigenschaften für horizontale Achsen**.  
  
6.  Aktivieren Sie das Kontrollkästchen **Achsen ausrichten in** . Die einzige Option in der Liste lautet „Tablix1“. 
  
    Dadurch wird die Breite der Balken in jeder Sparkline relativ zu den anderen Balken festgelegt. Wenn in einigen Sparklines weniger Balken enthalten sind, enthalten diese Sparklines Leerräume für die fehlenden Daten.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Klicken Sie auf **Ausführen** , um den Bericht erneut in der Vorschau anzuzeigen.  
  
Nun sind alle Balken in jeder Sparkline und an den Balken der anderen Sparklines ausgerichtet, und die Höhen stehen in einem Verhältnis zueinander.  
  
![Berichts-Generator-Sparkline-ausgerichtet](../reporting-services/media/report-builder-sparkline-aligned.png)
  
## <a name="Width"></a>7. Ändern der Spaltenbreite (optional)  
Standardmäßig enthält jede Zelle in einer Tabelle ein Textfeld. Textfelder werden beim Rendern der Seite entsprechend dem anzuzeigenden Text vertikal erweitert. Im gerenderten Bericht werden alle Zeilen auf die Höhe des größten gerenderten Textfelds in der Zeile vergrößert. Die Höhe der Zeile auf der Entwurfsoberfläche hat keinen Einfluss auf die Höhe der Zeile im gerenderten Bericht.  
  
Um die Höhe der Zeilen zu reduzieren, vergrößern Sie die Spaltenbreite, sodass der erwartete Inhalt der Textfelder in der Spalte in einer Zeile untergebracht werden kann.  
  
### <a name="to-change-the-width-of-columns"></a>So ändern Sie die Breite von Spalten  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie auf die Tabelle, damit graue Leisten über und neben der Tabelle angezeigt werden. Dabei handelt es sich um die Spalten- und Zeilenziehpunkte
  
3.  Zeigen Sie auf die Zeile zwischen Spaltenhandles, sodass sich der Cursor in einen Doppelpfeil ändert. Vergrößern Sie z.B. die **Product** -Spalte, damit der Produktname auf einer Zeile angezeigt wird.  
  
4.  Klicken Sie auf **Ausführen** , um den Bericht als Vorschau anzuzeigen und zu ermitteln, ob er breit genug ist.  
  
## <a name="Title"></a>8. Hinzufügen eines Berichtstitels (optional)  
Ein Berichtstitel wird oben im Bericht angezeigt. Sie können den Berichtstitel in eine Berichtskopfzeile einfügen oder, wenn der Bericht keine Kopfzeile enthält, in einem Textfeld am oberen Rand des Berichtshauptteils. In diesem Lernprogramm verwenden Sie das Textfeld, das automatisch am oberen Rand des Berichtshauptteils platziert wird.  
  
Die Darstellung des Texts kann weiter verbessert werden, indem andere Schriftschnitte, Größen und Farben für Ausdrücke und einzelne Zeichen des Texts angewendet werden. Weitere Informationen finden Sie unter [Formatieren von Text in einem Textfeld &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-report-title"></a>So fügen Sie einen Berichtstitel hinzu  
  
1.  Klicken Sie auf der Entwurfsoberfläche auf **Zum Hinzufügen eines Titels klicken**.  
  
2.  Geben Sie **Sales by Date**ein, und klicken Sie in den Bereich außerhalb des Textfelds.  
  
3.  Wählen Sie das Textfeld aus, das **Product Sales** enthält.  
  
4.  Wählen Sie auf der Registerkarte „Stamm“ in der Gruppe **Schriftart** für **Farbe** die Option **Blaugrün** aus.  
  
7.  Wählen Sie **Fett**aus.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Save"></a>9. Speichern des Berichts  
Speichern Sie den Bericht auf einem Berichtsserver oder auf Ihrem Computer. Wenn Sie den Bericht nicht auf dem Berichtsserver speichern, ist eine Reihe von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Funktionen nicht verfügbar, z. B. Berichtsteile und Unterberichte.  
  
### <a name="to-save-the-report-on-a-report-server"></a>So speichern Sie den Bericht auf einem Berichtsserver  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Letzte Sites und Server**.  
  
3.  Wählen Sie den Namen des Berichtsservers aus, auf dem Sie zum Speichern von Berichten berechtigt sind, oder geben Sie ihn ein.  
  
    Die Meldung "Verbindung mit Berichtsserver wird hergestellt" wird angezeigt. Nachdem die Verbindung hergestellt wurde, sehen Sie den Inhalt des Berichtsordners, den der Berichtsserveradministrator als Standardspeicherort für Berichte angegeben hat.  
  
4.  Ersetzen Sie im Feld **Name**den Standardnamen durch **Product Sales**.  
  
5.  Klicken Sie auf **Speichern**.  
  
Der Bericht wird auf dem Berichtsserver gespeichert. Der Name des Berichtsservers, mit dem Sie verbunden sind, wird in der Statusleiste unten im Fenster angezeigt.  
  
### <a name="to-save-the-report-on-your-computer"></a>So speichern Sie den Bericht auf dem Computer  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Desktop**, **Eigene Dokumente**oder **Computer**, und navigieren Sie zu dem Ordner, in dem Sie den Bericht speichern möchten.  
  
3.  Ersetzen Sie im Feld **Name**den Standardnamen durch **Product Sales**.  
  
4.  Klicken Sie auf **Speichern**.  
  
## <a name="next-steps"></a>Nächste Schritte  

Hiermit ist das Lernprogramm zum Erstellen eines Tabellenberichts mit Sparklinediagrammen abgeschlossen. Weitere Informationen zu Sparklines finden Sie unter [Sparklines und Datenbalken](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
[Tutorials (Berichts-Generator)](../reporting-services/report-builder-tutorials.md) 
[Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
