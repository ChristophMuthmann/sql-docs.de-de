---
title: 'Lernprogramm: Erstellen eines einfachen Tabellenberichts (Berichts-Generator) | Microsoft Docs'
ms.custom: 
ms.date: 06/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: d9e30521-f8ae-4c45-89c3-d40727f622f7
caps.latest.revision: 16
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 021a980dee9f6cd72f663475ba084962fa543cd4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="tutorial-creating-a-basic-table-report-report-builder"></a>Lernprogramm: Erstellen eines einfachen Tabellenberichts (Berichts-Generator)
In diesem Lernprogramm erfahren Sie, wie Sie auf Grundlage von Beispielumsatzdaten einen einfachen Tabellenbericht erstellen. Die folgende Abbildung zeigt den Bericht, den Sie erstellen.  
  
![SSRS_Tutorial_einfacher_Tabellenbericht](../reporting-services/media/ssrs-tutorial-basic-table-report.png)  
  

Ungefähre Dauer dieses Lernprogramms: 20 Minuten.  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Anforderungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="CreateTable"></a>1. Erstellen eines Berichts mithilfe eines Assistenten  
Erstellen eines Tabellenberichts mithilfe des Tabellen- oder Matrixassistenten. Zwei Modi stehen zur Auswahl: Berichtsentwurf und Entwurf von freigegebenen Datasets. Im Berichtsentwurfsmodus legen Sie im Berichtsdatenbereich Daten und auf der Entwurfsoberfläche das Berichtslayout fest. Im Entwurfsmodus für freigegebene Datasets erstellen Sie Datasetabfragen, die für andere Benutzer freigegeben werden. In diesem Lernprogramm verwenden Sie den Berichtsentwurfsmodus.  
  
### <a name="to-create-a-report"></a>So erstellen Sie einen Bericht  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
  
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist.  
  
3.  Wählen Sie im rechten Bereich **Tabellen- oder Matrix-Assistent**.  
  
## <a name="DataConnection"></a>1a. Angeben einer Datenverbindung im Tabellen-Assistenten  
Eine Datenverbindung enthält die Informationen zum Herstellen einer Verbindung mit einer externen Datenquelle, z. B. einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Datenbank. Normalerweise erhalten Sie die Verbindungsinformationen und den zu verwendenden Anmeldeinformationstyp vom Datenquellenbesitzer. Sie können zum Angeben einer Datenverbindung eine freigegebene Datenquelle vom Berichtsserver verwenden oder eine eingebettete Datenquelle erstellen, die nur in diesem Bericht verwendet wird.  
  
In diesem Lernprogramm verwenden Sie eine eingebettete Datenquelle. Weitere Informationen zur Verwendung von freigegebenen Datenquellen finden Sie unter [Alternative Verfahren zum Herstellen einer Datenverbindung &#40;Berichts-Generator&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
### <a name="to-create-an-embedded-data-source"></a>So erstellen Sie eine eingebettete Datenquelle  
  
1.  Klicken Sie auf der Seite **Dataset auswählen** auf **Dataset erstellen**und anschließend auf **Weiter**. Die Seite **Verbindung mit einer Datenquelle auswählen** wird geöffnet.  
  
2.  Klicken Sie auf **Neu**. Das Dialogfeld **Datenquelleneigenschaften** wird angezeigt.  
  
3.  Geben Sie im Feld **Name**den Namen **Product_Sales** für die Datenquelle ein.  
  
4.  Vergewissern Sie sich, dass unter **Verbindungstyp auswählen** die Option **Microsoft SQL Server** ausgewählt ist.  
  
5.  Geben Sie im Feld **Verbindungszeichenfolge** den folgenden Text ein, wobei \<Servername> der Name einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz ist:  
  
    ```  
    Data Source=<servername>  
    ```  
  
    Da Sie eine Abfrage verwenden, die die Daten enthält, anstatt die Daten aus einer Datenbank abzurufen, enthält die Verbindungszeichenfolge den Datenbanknamen nicht. Weitere Informationen finden Sie unter [Voraussetzungen für Lernprogramme &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
6.  Klicken Sie auf die Registerkarte **Anmeldeinformationen**. Geben Sie die für den Zugriff auf die externe Datenquelle benötigten Anmeldeinformationen ein.  
  
7. Klicken Sie erneut auf die Registerkarte Allgemein. Klicken Sie auf **Verbindung testen**, um sicherzustellen, dass die Verbindung mit der Datenquelle hergestellt werden kann.  
  
    Die Meldung "Die Verbindung wurde erfolgreich hergestellt" wird angezeigt.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Nun wird wieder die Seite **Verbindung mit einer Datenquelle auswählen** angezeigt, wobei Ihre neue Datenquelle ausgewählt ist.  
  
9. Klicken Sie auf **Weiter**.  
  
## <a name="Query"></a>1b. Erstellen einer Abfrage im Tabellen-Assistenten  
In einem Bericht können Sie ein freigegebenes Dataset mit einer vordefinierten Abfrage verwenden oder ein eingebettetes Dataset erstellen, das nur in diesem Bericht verwendet wird. In diesem Lernprogramm erstellen Sie ein eingebettetes Dataset.  
  
> [!NOTE]  
> In diesem Lernprogramm sind die Datenwerte in der Abfrage enthalten, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
### <a name="to-create-a-query"></a>So erstellen Sie eine Abfrage  
  
1.  Auf der Seite **Abfrage entwerfen** ist der relationale Abfrage-Designer geöffnet. Für dieses Lernprogramm verwenden Sie den textbasierten Abfrage-Designer.  
  
    Klicken Sie auf **Als Text bearbeiten**. Der textbasierte Abfrage-Designer umfasst zwei Bereiche: den Abfragebereich und den Ergebnisbereich.  
  
2.  Fügen Sie die folgende [!INCLUDE[tsql](../includes/tsql-md.md)] -Abfrage in das leere obere Feld ein.  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(9924.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
  
    ```  
  
3.  Klicken Sie auf der Symbolleiste des Abfrage-Designers auf **Ausführen** (**!**).  
  
    Die Abfrage wird ausgeführt, und das Resultset für die Felder "SalesDate", "Subcategory", "Product", "Sales" und "Quantity" wird angezeigt.  
  
    Die Spaltenüberschriften im Resultset basieren auf den Namen in der Abfrage. Im Dataset werden die Spaltennamen zu Feldnamen und werden im Bericht gespeichert. Nachdem Sie den Assistenten abgeschlossen haben, können Sie die Auflistung der Datasetfelder im Berichtsdatenbereich anzeigen.  
  
4.  Klicken Sie auf **Weiter**.  
  
## <a name="Groups"></a>1c. Gruppieren von Daten im Tabellen-Assistenten  
Durch das Auswählen von Feldern für die Gruppierung entwerfen Sie eine Tabelle mit Zeilen und Spalten, in denen Detaildaten und aggregierte Daten angezeigt werden.  
  
### <a name="to-organize-data-into-groups"></a>So gruppieren Sie Daten  
  
1.  Ziehen Sie auf der Seite **Felder anordnen** das Feld Product in **Werte**.  
  
2.  Ziehen Sie „Quantity“ in **Werte** , und platzieren Sie es unter „Product“.  
  
    "Quantity" wird automatisch von der Sum-Funktion aggregiert, dem Standardaggregat für numerische Felder. Der Wert ist "[Sum(Quantity)]".  
  
    Wählen Sie den Pfeil neben „[Sum(Quantity)]“, um die anderen verfügbaren Aggregatfunktionen anzuzeigen. Ändern Sie die Aggregatfunktion nicht.  
  
3.  Ziehen Sie „Sales“ in **Werte** , und fügen Sie dieses Feld unter „[Sum(Quantity)]“ ein.  
  
    "Sales" wird von der Sum-Funktion aggregiert. Der Wert ist "[Sum(Sales)]".  
  
    In Schritt 1, 2 und 3 werden die Daten angegeben, die in der Tabelle angezeigt werden sollen.  
  
4.  Ziehen Sie „SalesDate“ in **Zeilengruppen**.  
  
5.  Ziehen Sie „Subcategory“ in **Zeilengruppen** , und fügen Sie dieses Feld unter „SalesDate“ ein.  
  
    Durch die Schritte 4 und 5 werden die Werte für die Felder zuerst nach Datum und dann nach Produktunterkategorie für dieses Datum geordnet.  
  
6.  Klicken Sie auf **Weiter**.  
  
## <a name="Subtotals"></a>1d. Hinzufügen von Teilergebnis- und Ergebniszeilen im Tabellen-Assistenten  
Nachdem Sie Gruppen erstellt haben, können Sie Zeilen hinzufügen und formatieren, in denen Aggregatwerte für die Felder angezeigt werden. Sie können auswählen, ob alle Daten angezeigt werden oder der Benutzer gruppierte Daten interaktiv erweitern und reduzieren kann.  
  
### <a name="to-add-subtotals-and-totals"></a>So fügen Sie Teilergebnisse und Summen hinzu  
  
1.  Vergewissern Sie sich auf der Seite **Layout auswählen** , dass unter **Optionen**die Option **Teil- und Gesamtergebnisse anzeigen** ausgewählt ist.  
  
2.  Überprüfen Sie, ob **Als Block, Teilergebnis unterhalb** ausgewählt ist.  
  
    Im Vorschaubereich des Assistenten wird eine Tabelle mit fünf Zeilen angezeigt. Bei der Ausführung des Berichts wird jede Zeile wie folgt angezeigt:  
  
    1.  Die erste Zeile wird einmal wiederholt, damit Spaltenüberschriften in der Tabelle angezeigt werden.  
  
    2.  Die zweite Zeile wird einmal für jedes Zeilenelement im Verkaufsauftrag wiederholt. In dieser Zeile werden Produktname, Bestellmenge und Zeilensumme angezeigt.  
  
    3.  Die dritte Zeile wird einmal für jeden Verkaufsauftrag wiederholt. In dieser Zeile werden die Teilergebnisse für jeden Auftrag angezeigt.  
  
    4.  Die vierte Zeile wird einmal für jedes Bestelldatum wiederholt. In ihr werden Zwischensummen pro Tag angezeigt.  
  
    5.  Die fünfte Zeile wird einmal wiederholt, damit Gesamtsummen in der Tabelle angezeigt werden.  
  
3.  Deaktivieren Sie die Option **Gruppen erweitern/reduzieren**. In diesem Lernprogramm enthält der erstellte Bericht keine Drilldownfunktion, mit der ein Benutzer eine übergeordnete Gruppenhierarchie einblenden kann, um untergeordnete Gruppenzeilen und Detailzeilen anzuzeigen.  
  
4.  Klicken Sie auf **Weiter** , um eine Vorschau der Tabelle anzuzeigen, und anschließend auf **Fertig stellen**.  
  
Die Tabelle wird der Entwurfsoberfläche hinzugefügt. Die Tabelle enthält 5 Spalten und 5 Zeilen. Im Bereich "Zeilengruppen" werden drei Zeilengruppen angezeigt: "SalesDate", "Subcategory" und "Details". Detaildaten sind alle Daten, die von der Datasetabfrage abgerufen werden.  
  
## <a name="FormatCurrency"></a>2. Formatieren von Daten als Währung  
Die Zusammenfassungsdaten für das Feld "Sales" werden standardmäßig als eine Zahl im Standardzahlenformat angezeigt. Formatieren Sie das Feld, um die Zahl als Währung anzuzeigen.   
  
### <a name="to-format-a-currency-field"></a>So formatieren Sie ein Währungsfeld  
  
1.  Damit formatierte Textfelder und Platzhaltertext als Beispielwerte in der Entwurfsansicht angezeigt werden, klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Zahl** auf den Pfeil neben dem Symbol **Platzhalterformate** > **Beispielwerte**.  
  
2.   Klicken Sie auf die Zelle in der zweiten Zeile (unter der Zeile mit den Spaltenüberschriften) in der Spalte "Sales", und ziehen Sie den Mauszeiger nach unten, um alle Zellen auszuwählen, die `[Sum(Sales)]` enthalten.  
  
3.  Klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Zahl** auf die Schaltfläche **Währung** . Die Zellen ändern sich, um die formatierte Währung anzuzeigen.  
  
    Wenn Sie das Gebietsschema „Deutsch (Deutschland)“ verwenden, lautet der Standardbeispieltext [**12,345.00€**]. Wenn Sie keinen Beispielwährungswert sehen, klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Zahl** auf den Pfeil neben dem Symbol **Platzhalterformate** > **Beispielwerte**.  
  
4.  Klicken Sie auf **Ausführen** , um den Bericht in der Vorschau anzuzeigen.  
  
Die Zusammenfassungswerte für "Sales" werden als Währung angezeigt.  
  
## <a name="FormatDate"></a>3. Formatieren von Daten als Datum  
Im Feld „SalesDate“ werden standardmäßig sowohl Datum als auch Uhrzeit angezeigt. Durch entsprechende Formatierung kann auch nur das Datum angezeigt werden.  
  
### <a name="to-format-a-date-field-as-the-default-format"></a>So formatieren Sie ein Datumsfeld als Standardformat  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie auf die Zelle, die `[SalesDate]`enthält.  
  
3.  Klicken Sie auf dem Menüband auf der Registerkarte **Stamm** in der Gruppe **Zahl** auf den Pfeil und wählen Sie **Datum**aus.  
  
    In der Zelle wird das Beispieldatum **[31.01.2000]** angezeigt. Wenn Sie kein Beispieldatum sehen, klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Zahl** auf den Pfeil neben dem Symbol **Platzhalterformate** und wählen Sie **Beispielwerte** aus.  
  
4.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Die "SalesDate"-Werte werden im Standarddatumsformat angezeigt.  
  
### <a name="to-change-the-date-format-to-a-custom-format"></a>So ändern Sie das Datumsformat in ein benutzerdefiniertes Format  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Wählen Sie die Zelle, die `[SalesDate]`enthält.  
  
3.  Klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Zahl** auf den Pfeil in der Ecke unten rechts, um das Dialogfeld zu öffnen.  
  
    Das Dialogfeld **Textfeldeigenschaften** wird geöffnet.  
  
4.  Prüfen Sie im Bereich Kategorie, ob **Datum** gewählt ist.  
  
5.  Wählen Sie im Bereich **Typ** die Option **31. Januar 2000**aus.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Die Zelle zeigt das Beispieldatum an: **[31. Januar 2000]**.  
  
7.  Klicken Sie auf **Ausführen** , um den Bericht in der Vorschau anzuzeigen.  
  
Der Wert von „SalesDate“ wird mit dem Namen des Monats anstelle der Zahl für den Monat angezeigt.  
  
## <a name="Width"></a>4. Ändern der Spaltenbreite  
Standardmäßig enthält jede Zelle in einer Tabelle ein Textfeld. Textfelder werden beim Rendern der Seite entsprechend dem anzuzeigenden Text vertikal erweitert. Im gerenderten Bericht werden alle Zeilen auf die Höhe des größten gerenderten Textfelds in der Zeile vergrößert. Die Höhe der Zeile auf der Entwurfsoberfläche hat keinen Einfluss auf die Höhe der Zeile im gerenderten Bericht.  
  
Um die Höhe der Zeilen zu reduzieren, vergrößern Sie die Spaltenbreite, sodass der erwartete Inhalt der Textfelder in der Spalte in einer Zeile untergebracht werden kann.  
  
### <a name="to-change-the-width-of-table-columns"></a>So ändern Sie die Breite von Tabellenspalten  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie auf die Tabelle, damit die Spalten- und Zeilenhandles über und neben der Tabelle angezeigt werden.  
  
    Die grauen Balken oberhalb und neben der Tabelle stellen die Spalten- und Zeilenhandles dar.  
  
3.  Zeigen Sie auf die Zeile zwischen Spaltenhandles, sodass sich der Cursor in einen Doppelpfeil ändert. Ziehen Sie die Spalten auf die gewünschte Breite. Beispiel: Erweitern Sie die Spalte für Produkt, damit der Produktname auf einer Zeile angezeigt wird.  
  
4.  Klicken Sie auf **Ausführen** , um den Bericht in der Vorschau anzuzeigen.  
  
## <a name="Title"></a>5. Hinzufügen eines Berichtstitels  
Ein Berichtstitel wird oben im Bericht angezeigt. Sie können den Berichtstitel in eine Berichtskopfzeile einfügen oder, wenn der Bericht keine Kopfzeile enthält, in einem Textfeld am oberen Rand des Berichtshauptteils. In diesem Lernprogramm verwenden Sie das Textfeld, das automatisch am oberen Rand des Berichtshauptteils platziert wird.  
  
Die Darstellung des Texts kann weiter verbessert werden, indem andere Schriftschnitte, Größen und Farben für Ausdrücke und einzelne Zeichen des Texts angewendet werden. Weitere Informationen finden Sie unter [Formatieren von Text in einem Textfeld &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-report-title"></a>So fügen Sie einen Berichtstitel hinzu  
  
1.  Klicken Sie auf der Entwurfsoberfläche auf **Zum Hinzufügen eines Titels klicken**.  
  
2.  Geben Sie **Product Sales**ein, und klicken Sie anschließend außerhalb des Textfelds.  
  
3.  Klicken Sie mit der rechten Maustaste auf das Textfeld, das **Product Sales** enthält, und klicken Sie auf **Textfeldeigenschaften**.  
  
4.  Klicken Sie im Dialogfeld **Textfeldeigenschaften** auf **Schriftart**.  
  
5.  Wählen Sie in der Liste **Schriftgrad** den Eintrag **18pt**aus.  
  
6.  Wählen Sie in der Liste **Farbe** die Option **Kornblumenblau**aus.  
  
7.  Wählen Sie **Fett**aus.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Save"></a>6. Speichern des Berichts  
Speichern Sie den Bericht auf einem Berichtsserver oder auf Ihrem Computer. Wenn Sie den Bericht nicht auf dem Berichtsserver speichern, ist eine Reihe von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Funktionen nicht verfügbar, z. B. Berichtsteile und Unterberichte.  
  
### <a name="to-save-the-report-on-a-report-server"></a>So speichern Sie den Bericht auf einem Berichtsserver  
  
1.  Klicken Sie auf **Datei** > **Speichern als**.  
  
2.  Klicken Sie auf **Letzte Sites und Server**.  
  
3.  Wählen Sie den Namen des Berichtsservers aus, auf dem Sie zum Speichern von Berichten berechtigt sind, oder geben Sie ihn ein.  
  
    Die Meldung "Verbindung mit Berichtsserver wird hergestellt" wird angezeigt. Nachdem die Verbindung hergestellt wurde, sehen Sie den Inhalt des Berichtsordners, den der Berichtsserveradministrator als Standardspeicherort für Berichte angegeben hat.  
  
4.  In **Name**, ersetzen Sie **Unbenannt** mit **Product_Sales**.  
  
5.  Klicken Sie auf **Speichern**.  
  
Der Bericht wird auf dem Berichtsserver gespeichert. Der Name des Berichtsservers, mit dem Sie verbunden sind, wird in der Statusleiste unten im Fenster angezeigt.  
  
### <a name="to-save-the-report-on-your-computer"></a>So speichern Sie den Bericht auf dem Computer  
  
1.  Klicken Sie auf **Datei** > **Speichern als**.  
  
2.  Klicken Sie auf **Desktop**, **Eigene Dokumente**oder **Computer**, und navigieren Sie zu dem Ordner, in dem Sie den Bericht speichern möchten.  
  
3.  In **Name**, ersetzen Sie **Unbenannt** durch **Product Sales**.  
  
4.  Klicken Sie auf **Speichern**.  
  
## <a name="Export"></a>7. Exportieren des Berichts  
Berichte können in verschiedene Formate exportiert werden, z.B. Microsoft Excel- und CSV-Dateien. Weitere Informationen finden Sie unter [Exportieren von Berichten &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
In diesem Lernprogramm exportieren Sie den Bericht nach Excel, und Sie legen eine Eigenschaft für den Bericht fest, um einen benutzerdefinierten Namen für das Arbeitsmappenregister anzugeben.  
  
### <a name="to-specify-the-workbook-tab-name"></a>So geben Sie den Namen des Arbeitsmappenregisters an  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie auf die Entwurfsoberfläche außerhalb des Berichts.  
  
3.  Suchen Sie im Bereich Eigenschaften nach der InitialPageName-Eigenschaft und geben Sie **Product Sales Excel**ein.  
  
    > [!NOTE]  
    > Klicken Sie auf der Registerkarte **Ansicht** auf **Eigenschaften**, falls der Bereich "Eigenschaften" nicht angezeigt wird.  
    > Wenn eine Eigenschaft im Bereich Eigenschaften nicht angezeigt wird, versuchen Sie, die **Alphabetisch** Schaltfläche oben am Bereich auszuwählen, um alle Eigenschaften alphabetisch zu sortieren.   
  
### <a name="to-export-a-report-to-excel"></a>So exportieren Sie einen Bericht nach Excel  
  
1.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
2.  Klicken Sie im Menüband auf **Exportieren**  >  **Excel**.  
  
    Der Bericht öffnet sich.  
  
3.  Navigieren Sie im Dialogfeld **Speichern unter** zu dem Verzeichnis, in dem die Datei gespeichert werden soll.  
  
4.  Geben Sie im Textfeld **Dateiname** den Namen **Product_Sales_Excel** ein.  
  
5.  Vergewissern Sie sich, dass der Dateityp **Excel (\*.xlsx)** ist.  
  
6.  Klicken Sie auf **Speichern**.  
  
### <a name="to-view-the-report-in-excel"></a>So zeigen Sie den Bericht in Excel an  
  
1.  Öffnen Sie den Ordner, in dem Sie die Arbeitsmappe speichern, und doppelklicken Sie auf **Product_Sales_Excel.xlsx**.  
  
2.  Überprüfen Sie, ob der Name des Arbeitsmappenregisters **Product Sales Excel**lautet.  
  
## <a name="next-steps"></a>Nächste Schritte  
Damit ist die exemplarische Vorgehensweise für das Erstellen eines einfachen Tabellenberichts abgeschlossen. Weitere Informationen zu Tabellen finden Sie unter [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
[Lernprogramme für den Berichts-Generator](../reporting-services/report-builder-tutorials.md)  
[Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  


