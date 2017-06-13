---
title: "Lernprogramm: Einführung in Ausdrücke | Microsoft Docs"
ms.custom: 
ms.date: 09/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
caps.latest.revision: 14
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 97b19aaffd06a196d3cbd39e44b49c971a146edf
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="tutorial-introducing-expressions"></a>Lernprogramm: Einführung in Ausdrücke
In diesem [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] -Tutorial verwenden Sie Ausdrücke mit allgemeinen Funktionen und Operatoren zum Erstellen von leistungsstarken und flexiblen [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] paginierten Berichten. 

Sie werden Ausdrücke schreiben, die Namenswerte verketten, Werte in separaten Datasets suchen, auf Grundlage der Feldwerte verschiedene Farben anzeigen usw.  
  
Der Bericht ist ein gebänderter Bericht mit abwechselnd in weiß und einer Farbe gestalteten Zeilen. Der Bericht enthält einen Parameter zur Auswahl der Farbe für alle Zeilen, die nicht weiß dargestellt werden sollen.  
  
Diese Abbildung zeigt einen Bericht, der mit dem Bericht vergleichbar ist, den Sie erstellen werden.  
  
![Berichts-Generator-Ausdruck-Tutorial-in-Browser](../reporting-services/media/report-builder-expression-tutorial-in-browser.png) 
  
Geschätzte Zeit zum Bearbeiten dieses Lernprogramms: 30 Minuten  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Anforderungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Setup"></a>1. Erstellen eines Tabellenberichts und eines Datasets mit dem Tabellen- oder Matrix-Assistenten  
In diesem Abschnitt erstellen Sie einen Tabellenbericht, eine Datenquelle und ein Dataset. Für den Entwurf der Tabelle werden nur einige wenige Felder verwendet. Nach Fertigstellung des Assistenten werden Sie manuell Spalten hinzufügen. Der Assistent erleichtert das Layout der Tabelle.  
  
> [!NOTE]  
> In diesem Tutorial sind die Datenwerte in der Abfrage enthalten, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
### <a name="to-create-a-table-report"></a>So erstellen Sie einen Tabellenbericht  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
  
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist.  
  
3.  Klicken Sie im rechten Bereich auf **Tabellen- oder Matrix-Assistent**.  
  
4.  Klicken Sie auf der Seite **Dataset auswählen** auf **Dataset erstellen** > **Weiter**.  
  
6.  Wählen Sie auf der Seite **Verbindung mit einer Datenquelle auswählen** eine Datenquelle vom Typ **SQL Server**aus. Wählen Sie in der Liste eine Datenquelle aus, oder navigieren Sie zum Berichtsserver, um eine Datenquelle auszuwählen.  

    > [!NOTE]  
    > Welche Datenquelle Sie auswählen, ist unwichtig, solange Sie über ausreichende Berechtigungen verfügen. Aus der Datenquelle werden keine Daten abgerufen. Weitere Informationen finden Sie unter [Alternative Methoden zum Herstellen einer Datenverbindung &#40;Berichts-Generator&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
7.  Klicken Sie auf **Weiter**.  
  
8.  Klicken Sie auf der Seite **Abfrage entwerfen** auf **Als Text bearbeiten**.  
  
9. Fügen Sie die folgende Abfrage in den Abfragebereich ein:  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Female' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2015-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2015-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2015-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2015-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2015-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2015-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2015-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2015-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2015-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2015-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2015-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2015-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2015-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2015-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2015-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2015-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2015-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2015-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2015-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2015-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2015-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2015-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2015-11-30' AS date) AS LastPurchase  
    ```  

  
10. Klicken Sie auf der Symbolleiste des Abfrage-Designers auf **Ausführen** (**!**). Das Resultset umfasst 23 Datenzeilen in den folgenden Spalten: FirstName (Vorname), LastName (Nachname), StateProvince (Bundesstaat/Provinz), CountryRegionID (ID des Landes/der Region), Gender (Geschlecht), YTDPurchase (Käufe seit Jahresbeginn) und LastPurchase (Letzter Kauf).  

    ![Berichts-Generator-Ausdruck-Tutorial-Abfrage-als-Text](../reporting-services/media/report-builder-expression-tutorial-query-as-text.png)
  
11. Klicken Sie auf **Weiter**.  
  
12. Ziehen Sie auf der Seite **Felder anordnen** die folgenden Felder in der angegebenen Reihenfolge aus der Liste **Verfügbare Felder** in die Liste **Werte** .  
  
    -   StateProvince   
    -   CountryRegionID  
    -   LastPurchase  
    -   YTDPurchase  
  
    Da CountryRegionID und YTDPurchase numerische Daten enthalten, wird die SUM-Aggregatfunktion standardmäßig auf diese Felder angewendet. Allerdings sollen die Spalten nicht addiert werden.  
   
13. Klicken Sie in der Liste **Werte** mit der rechten Maustaste auf **CountryRegionID** , und deaktivieren Sie anschließend die das Kontrollkästchen **Sum** .  
  
    Sum wird nicht länger auf CountryRegionID angewendet.  
  
14. Klicken Sie in der Liste **Werte** mit der rechten Maustaste auf **YTDPurchase** und klicken Sie anschließend auf die Option **Sum** .  
  
    Sum wird nicht länger auf YTDPurchase angewendet.  
    
    ![Berichts-Generator-Ausdruck-nicht-Sum](../reporting-services/media/report-builder-expression-not-sum.png)
  
15. Klicken Sie auf **Weiter**.  
  
16. Behalten Sie auf der Seite **Layout auswählen** alle Standardeinstellungen bei, und klicken Sie auf **Weiter**.  

    ![Berichts-Generator-Ausdruck-Tutorial-Layout-auswählen](../reporting-services/media/report-builder-expression-tutorial-choose-layout.png)
  
17. Klicken Sie auf **Fertig stellen**.  
  
## <a name="UpdateNames"></a>2. Aktualisieren der Standardnamen der Datenquelle und des Datensets  
  
### <a name="to-update-the-default-name-of-the-data-source"></a>So aktualisieren Sie den Standardnamen der Datenquelle  
  
1.  Erweitern Sie im Bereich „Berichtsdaten“ den Ordner **Datenquellen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf **DataSource1** und anschließend auf **Datenquelleneigenschaften**.  
  
3.  Geben Sie im Feld **Name** Folgendes ein: **Datenquelle_für_Ausdrücke**  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-update-the-default-name-of-the-dataset"></a>So aktualisieren Sie den Standardnamen des Datasets  
  
1.  Erweitern Sie im Bereich „Berichtsdaten“ den Ordner **Datasets** .  
  
2.  Klicken Sie mit der rechten Maustaste auf **DataSet1** und anschließend auf **Dataseteigenschaften**.  

    ![Berichts-Generator-Ausdruck-Tutorial-Dataset-umbenennen](../reporting-services/media/report-builder-expression-tutorial-rename-dataset.png)
  
3.  Geben Sie im Feld **Name** Folgendes ein: **Ausdrücke**  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Concatenate"></a>3. Anzeigen des Anfangsbuchstabens des Vornamens und des Nachnamens  
In diesem Abschnitt verwenden Sie die **Left**-Funktion und den Operator zum **Verketten** (**&**) in einem Ausdruck, der zu einem Anfangsbuchstaben des Vornamens und dem Nachnamen ausgewertet wird. Sie können den Ausdruck Schritt für Schritt erstellen oder diesen Teil der Prozedur überspringen und den Ausdruck aus dem Tutorial in das Dialogfeld **Ausdruck** kopieren und einfügen.   
  
1.  Klicken Sie mit der rechten Maustaste auf die Spalte **StateProvince** , zeigen Sie auf **Spalte einfügen**und klicken Sie auf **Links**.  
  
    Links von der Spalte **StateProvince** wird eine neue Spalte hinzugefügt. 
    
    ![Berichts-Generator-Ausdruck-Tutorial-Spalte-einfügen](../reporting-services/media/report-builder-expression-tutorial-insert-column.png) 
  
2.  Klicken Sie auf den Titel der neuen Spalte, und geben Sie **Name**ein.  
  
3.  Klicken Sie mit der rechten Maustaste in die Datenzelle der Spalte **Name** und klicken Sie auf **Ausdruck**.  

    ![Berichts-Generator-Ausdruck-Tutorial-Ausdruck-einfügen](../reporting-services/media/report-builder-expression-tutorial-insert-expression.png)
  
4.  Erweitern Sie im Dialogfeld **Ausdruck** die Option **Allgemeine Funktionen**und klicken Sie anschließend auf **Text**.  
  
5.  Doppelklicken Sie in der Liste **Element** auf **Left**.  
  
    Die Funktion **Left** wird dem Ausdruck hinzugefügt.  
    
    ![Berichts-Generator-Ausdruck-Tutorial-left-Funktion](../reporting-services/media/report-builder-expression-tutorial-left-function.png)
  
6.  Doppelklicken Sie in der Liste **Kategorie** auf **Felder (Ausdrücke)**.  
  
7.  Doppelklicken Sie in der Liste **Werte** auf **FirstName**.  
  
8.  Geben Sie **, 1)**ein  
  
    Der Ausdruck extrahiert ein Zeichen aus dem Wert **FirstName**, beginnend von links.  
  
9. Geben Sie **&". "&** ein.  

    Dadurch wird ein Punkt und ein Leerzeichen an den Ausdruck angefügt.
  
10. Doppelklicken Sie in der Liste **Werte** auf **LastName**.  
  
    Der vollständige Ausdruck lautet wie folgt: `=Left(Fields!FirstName.Value, 1) &". "& Fields!LastName.Value`.  
    
    ![Berichts-Generator-Ausdruck-Tutorial-vollständiger-Namensausdruck](../reporting-services/media/report-builder-expression-tutorial-complete-name-expression.png)
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  

## <a name="DateFormat"></a>(optional) Formatieren der Datums- und Währungsspalten und der Kopfzeile  
In diesem Abschnitt formatieren Sie die Spalte **Last Purchase** , die Datumsangaben enthält, und die Spalte „YTDPurchase“, die Währungsangaben enthält. Sie werden auch die Kopfzeile formatieren.  
  
### <a name="to-format-the-date-column"></a>So formatieren Sie die Datumsspalte  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Wählen Sie die Datenzelle in der Spalte **Last Purchase** aus, und wählen Sie auf der Registerkarte **Stamm** im Abschnitt **Zahl** **Datum** aus.  

    ![Berichts-Generator-Ausdruck-Tutorial-Datumsformat](../reporting-services/media/report-builder-expression-tutorial-date-format.png)
  
3.  Klicken Sie im Abschnitt **Zahl** auf den Pfeil neben **Platzhalterformate** , und wählen Sie **Beispielwerte**aus. 

    ![Berichts-Generator-Ausdruck-Tutorial-Beispielwerte](../reporting-services/media/report-builder-expression-tutorial-sample-values.png)

    Jetzt sehen Sie ein Beispiel für die Formatierung, die Sie ausgewählt haben. 
  
### <a name="to-format-the-currency-column"></a>So formatieren Sie die Währungsspalte

- Wählen Sie die Datenzelle in der Spalte **YTDPurchase** aus, und wählen Sie im Abschnitt **Zahl** **Währungssymbol**aus.
 
### <a name="to-format-the-column-headers"></a>So formatieren Sie die Spaltenheader

1. Wählen Sie die Zeile mit Spaltenheadern aus.

2. Wählen Sie auf der Registerkarte **Stamm** im Abschnitt **Absatz** **Links** aus. 

    ![Berichts-Generator-Ausdruck-Tutorial-Header-formatieren](../reporting-services/media/report-builder-expression-tutorial-format-headings.png)

3. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen. 

So sieht der vorläufige Bericht mit den formatierten Datumsangaben und Spaltenheadern sowie der formatierten Währung aus.

![Berichts-Generator-Ausdruck-Tutorial-Vorschau-formatiert](../reporting-services/media/report-builder-expression-tutorial-preview-formatted.png)

  
## <a name="Gender"></a>4. Verwenden von Farben für die Differenzierung nach Geschlechtern  
In diesem Abschnitt fügen Sie Farben hinzu, um das Geschlecht einer Person anzuzeigen. Sie fügen eine neue Spalte für die Farbanzeige hinzu. Anschließend legen Sie fest, welche Farbe auf Grundlage des Werts im Feld für das Geschlecht in der Spalte angezeigt wird.  
  
Um bei der Erstellung eines gebänderten Berichts die Farbe beizubehalten, die Sie in dieser Tabellenzelle angewendet haben, müssen Sie ein Rechteck und diesem dann die Hintergrundfarbe hinzufügen.  
    
 
### <a name="to-add-an-mf-column"></a>So fügen die Spalte „M/W“ hinzu  
  
1.  Klicken Sie mit der rechten Maustaste auf die Spalte **Name** , zeigen Sie auf **Spalte einfügen**und klicken Sie anschließend auf **Links**.  
  
    Links von der Spalte **Name** wird eine neue Spalte hinzugefügt.  
  
2.  Klicken Sie auf den Titel der neuen Spalte, und geben Sie **M/W**(männlich/weiblich) ein.  
  
### <a name="to-add-a-rectangle"></a>So fügen Sie ein Rechteck hinzu  
  
1.   Klicken Sie auf der Registerkarte **Einfügen** auf **Rechteck** und anschließend in die Datenzelle der Spalte **M/W** .  
  
     Der Zelle wird ein Rechteck hinzugefügt.  
     
     ![Berichts-Generator-Ausdruck-Tutorial-Rechteck-einfügen](../reporting-services/media/report-builder-expression-tutorial-insert-rectangle.png)
  
2. Ziehen Sie den Spaltenunterteiler zwischen die Spalten **M/W** und **Name** , um die **M/W** -Spalte schmaler zu gestalten.

    ![Berichts-Generator-Ausdruck-Tutorial-Spalte-verengen](../reporting-services/media/report-builder-expression-tutorial-narrow-column.png)
  
### <a name="to-use-color-to-show-gender"></a>So verwenden Sie Farben für die Anzeige des Geschlechts  
  
1.  Klicken Sie mit der rechten Maustaste auf das Rechteck in der Datenzelle in der Spalte **M/W** und anschließend auf **Rechteckeigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Rechteckeigenschaften** auf der Registerkarte **Füllen** auf die Ausdrucksschaltfläche **fx** neben **Füllfarbe**.  
  
3.  Erweitern Sie im Dialogfeld **Ausdruck** die Option **Allgemeine Funktionen** und klicken Sie auf **Programmfluss**.  
  
4.  Doppelklicken Sie in der Liste **Element** auf **Switch**.  
  
5.  Doppelklicken Sie in der Liste **Kategorie** auf **Felder (Ausdrücke)**.  
  
6.  Doppelklicken Sie in der Liste **Werte** auf **Geschlecht**.  
  
7.  Geben Sie **="Male",** (einschließlich des Kommas) ein.

8. Klicken Sie in der Liste **Kategorie** auf **Konstanten**, und klicken Sie im Feld **Werte** auf **Kornblumenblau**.

    ![Berichts-Generator-Ausdruck-Tutorial-Farbausdruck-Kornblumenblau](../reporting-services/media/report-builder-expression-tutorial-color-expression-cornflower-blue.png)

9. Geben Sie nach dem Ausdruck ein Komma ein. 
  
5.  Klicken Sie in der Liste **Kategorie** auf **Felder (Ausdrücke)**, und doppelklicken Sie in der Liste **Werte** erneut auf **Geschlecht** .  
  
7.  Geben Sie **="Female",** (einschließlich des Kommas) ein. 

8. Klicken Sie in der Liste **Kategorie** auf **Konstanten**, und klicken Sie im Feld **Werte** auf **Tomatenrot**.

13. Geben Sie dahinter eine schließende Klammer **)** ein. 
  
    Der vollständige Ausdruck lautet wie folgt: `=Switch(Fields!Gender.Value ="Male", "CornflowerBlue",Fields!Gender.Value ="Female","Tomato")`.  
    
    ![Berichts-Generator-Ausdruck-Tutorial-Farbausdruck-vollständig](../reporting-services/media/report-builder-expression-tutorial-color-expression-complete.png)
  
12. Klicken Sie auf **OK**und dann noch einmal auf **OK** , um das Dialogfeld **Rechteckeigenschaften** zu schließen.  
  
14. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  

    ![Berichts-Generator-Ausdruck-Tutorial-Vorschau-M-W-Spalte](../reporting-services/media/report-builder-expression-tutorial-preview-m-f-column.png)

### <a name="to-format-the-color-rectangles"></a>So formatieren Sie die Farbrechtecke

1. Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  

16. Wählen Sie das Rechteck in der **M/W** -Spalte aus. Legen Sie im Eigenschaftenbereich im Abschnitt „Rahmen“ diese Eigenschaften fest:

    - BorderColor = White
    - BorderStyle = Solid
    - BorderWidth = 5pt
    
    ![Berichts-Generator-Ausdruck-Tutorial-M-W-Spalte-formatieren](../reporting-services/media/report-builder-expression-tutorial-format-m-f-column.png)

18. Klicken Sie auf **Ausführen** , um erneut eine Vorschau des Berichts anzuzeigen. Jetzt sind die Farbblöcke weiß eingerahmt.

    ![Berichts-Generator-Ausdruck-Tutorial-Vorschau-formatierte-M-W-Spalte](../reporting-services/media/report-builder-expression-tutorial-preview-formatted-m-f-column.png)  
  
## <a name="Lookup"></a>5. Suchen des CountryRegion-Namens  
In diesem Abschnitt erstellen Sie das CountryRegion-Dataset und verwenden die **Lookup**-Funktion, um den Namen des Lands/der Region anstelle des Bezeichners des Lands/der Region anzuzeigen.  
  
### <a name="to-create-the-countryregion-dataset"></a>So erstellen Sie das CountryRegion-Dataset  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie im Berichtsdatenbereich auf **Neu** und anschließend auf **Dataset**.  
  
3.  In ** Dataset-Eigenschaften, klicken Sie auf **ein in den eigenen Bericht eingebettetes Dataset verwenden**.  
  
4.  Wählen Sie in der Liste **Datenquelle** die Option „Datenquelle_für_Ausdrücke“.  
  
5.  Geben Sie im Feld **Name** Folgendes ein: **CountryRegion**  
  
6.  Überprüfen Sie, ob der Abfragetyp **Text** ausgewählt ist und klicken Sie auf **Abfrage-Designer**.  
  
7.  Klicken Sie auf **Als Text bearbeiten**.  
  
8.  Kopieren Sie die folgende Abfrage, und fügen Sie sie in den Abfragebereich ein:  
  
    ```  
    SELECT 1 AS ID, 'American Samoa' AS CountryRegion  
    UNION SELECT 2 AS CountryRegionID, 'Australia' AS CountryRegion  
    UNION SELECT 3 AS ID, 'Canada' AS CountryRegion  
    UNION SELECT 4 AS ID, 'Germany' AS CountryRegion  
    UNION SELECT 5 AS ID, 'Micronesia' AS CountryRegion  
    UNION SELECT 6 AS ID, 'France' AS CountryRegion  
    UNION SELECT 7 AS ID, 'United States' AS CountryRegion  
    UNION SELECT 8 AS ID, 'Brazil' AS CountryRegion  
    UNION SELECT 9 AS ID, 'Mexico' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Japan' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Australia' AS CountryRegion  
    UNION SELECT 12 AS ID, 'United Kingdom' AS CountryRegion  
    ```  
  
9. Klicken Sie auf **Ausführen** (**!**), um die Abfrage auszuführen.  
  
    Abfrage-Ergebnisse sind die Land/Region-Bezeichner und -Namen.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Klicken Sie auf **OK** , um das Dialogfeld **Dataseteigenschaften** zu schließen.  

     Nun verfügen Sie über ein zweites Dataset in der Spalte **Berichtsdaten** .
  
### <a name="to-look-up-values-in-the-countryregion-dataset"></a>So schlagen Sie Werte im CountryRegion-Dataset nach  
  
1.  Klicken Sie auf den Spaltenheader **Country Region ID** , und löschen Sie den Text **ID**, sodass dort nur noch **Country Region**steht.  
  
2.  Klicken Sie mit der rechten Maustaste in die Datenzelle der Spalte **Country Region** und klicken Sie auf **Ausdruck**.  
  
3.  Löschen Sie den Ausdruck bis auf das Gleichheitszeichen (=).  
  
    Der verbleibende Ausdruck lautet: `=`  
  
4.  Erweitern Sie im Dialogfeld **Ausdruck** die Option **Allgemeine Funktionen** , klicken Sie anschließend auf **Sonstiges**, und doppelklicken Sie in der Liste **Elemente** auf **Suchen**.  
  
6.  Klicken Sie in der Liste **Kategorie** auf **Felder (Ausdrücke)**, und doppelklicken Sie in der Liste **Werte** auf **CountryRegionID**.  
  
8.  Platzieren Sie den Cursor direkt hinter `CountryRegionID.Value`, und geben Sie **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")**ein.  
  
    Der vollständige Ausdruck lautet wie folgt: `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
    Die Syntax der **Lookup** -Funktion spezifiziert eine Suche zwischen CountryRegionID im Dataset „Expressions“ und der ID im Dataset „CountryRegion“, die den Wert „CountryRegion“ aus dem Dataset „CountryRegion“ zurückgibt.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
## <a name="Count"></a>6. Ermitteln der vergangenen Tage seit dem letzten Kauf  
In diesem Abschnitt fügen Sie eine Spalte hinzu und verwenden anschließend die **Now**-Funktion oder die integrierte globale `ExecutionTime`-Variable, um die Anzahl der Tage seit dem letzten Einkauf (ab heute) eines Kunden zu berechnen.  
  
### <a name="to-add-the-days-ago-column"></a>So fügen Sie die Spalte "Vor (n) Tagen)" hinzu  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Last Purchase** , zeigen Sie auf **Spalte einfügen**und klicken Sie auf **Rechts**.  
  
    Rechts von der Spalte **Letzter Kauf** wird eine neue Spalte hinzugefügt.  
  
3.  Geben Sie in der Spaltenüberschrift **Vor (n) Tagen**ein  
  
4.  Klicken Sie mit der rechten Maustaste in die Datenzelle der Spalte **Vor (n) Tagen** und klicken Sie auf **Ausdruck**.  
  
5.  Erweitern Sie im Dialogfeld **Ausdruck** die Option **Allgemeine Funktionen**, und klicken Sie anschließend auf **Datum & Uhrzeit**.  
  
6.  Doppelklicken Sie in der Liste **Elemente** auf **DateDiff**.  
  
7.  Geben Sie unmittelbar hinter `DateDiff(` **"d",** (einschließlich der Anführungszeichen "" und des Kommas) ein. 
  
9. Klicken Sie in der Liste **Kategorie** auf **Felder (Ausdrücke)**, und doppelklicken Sie in der Liste **Werte** auf **LastPurchase**.  
  
11. Geben Sie unmittelbar hinter `Fields!LastPurchase.Value` ein Komma **,** ein. 
  
13. Klicken Sie in der Liste **Kategorie** erneut auf **Datum/Uhrzeit**, und doppelklicken Sie in der Liste **Elemente** auf **Now** (Jetzt).  
  
    > [!WARNING]  
    > In Produktionsberichten dürfen Sie nicht die **Now**-Funktion in Ausdrücken verwenden, die beim Rendern des Berichts mehrmals ausgewertet werden (z.B. in den Detailzeilen eines Berichts). Der Wert von **Now** ändert sich von Zeile zu Zeile, und die verschiedenen Werte wirken sich auf die Auswertungsergebnisse der Ausdrücke aus, was zu inkonsistenten Resultaten führt. Verwenden Sie stattdessen die globale Variable `ExecutionTime` , die von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] bereitgestellt wird.  
  
15. Löschen Sie die öffnende Klammer nach `Now(`, und geben Sie dann eine schließende Klammer **)**ein.  
  
    Der vollständige Ausdruck lautet wie folgt: `=DateDiff("d", Fields!LastPurchase.Value, Now)`.  
    
    ![Berichts-Generator-Ausdruck-Tutorial-Datum-letzter-Einkauf](../reporting-services/media/report-builder-expression-tutorial-date-since-last-purchase.png)
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

11. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
## <a name="Indicator"></a>7. Verwenden eines Indikators zur Anzeige des Umsatzvergleichs  
In diesem Abschnitt fügen Sie eine neue Spalte hinzu und verwenden einen Indikator, um anzuzeigen, ob die Einkäufe im laufenden Jahr oberhalb oder unterhalb des Durchschnitts liegen. Die Funktion **Round** entfernt die Dezimalstellen aus den Werten.  
  
Das Konfigurieren des Indikators und seiner Zustände erfordert viele Schritte. Wenn Sie möchten, können Sie gleich zu der Prozedur „So konfigurieren Sie den Indikator“ wechseln und die fertigen Ausdrücke aus diesem Tutorial kopieren und in das Dialogfeld **Ausdruck** einfügen.  
  
### <a name="to-add-the--or---avg-sales-column"></a>So fügen Sie die Spalte "+/- durchschnittl. Käufe" hinzu  
  
1.  Klicken Sie mit der rechten Maustaste auf **YTD Purchase** , zeigen Sie auf **Spalte einfügen**und klicken Sie auf **Rechts**.  
  
    Rechts von der Spalte **YTD Purchase** wird eine neue Spalte hinzugefügt.  
  
2.  Klicken Sie auf den Spaltenheader, und geben Sie **+/- durchschnittl. Umsatz**ein.  
  
### <a name="to-add-an-indicator"></a>So fügen Sie einen Indikator hinzu  
  
1.  Klicken Sie auf der Registerkarte **Einfügen** auf **Indikator**und anschließend in die Datenzelle der Spalte **+/- durchschnittl. Umsatz** .  
  
    Das Dialogfeld **Indikatortyp auswählen** wird geöffnet.  
  
2.  Klicken Sie in der Gruppe **Direktional** der Symbolsätze auf den Satz mit den drei grauen Pfeilen.  

    ![Berichts-Generator-Ausdruck-Tutorial-Indikator-auswählen](../reporting-services/media/report-builder-expression-tutorial-select-indicator.png)
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-configure-the-indicator"></a>So konfigurieren Sie den Indikator  
  
1.  Klicken Sie mit der rechten Maustaste auf den Indikator, anschließend auf **Indikatoreigenschaften**und schließlich auf **Wert und Status**.  
  
2.  Klicken Sie auf die Ausdrucksschaltfläche **fx** neben dem Textfeld **Wert** .  
  
3.  Erweitern Sie im Dialogfeld **Ausdruck** die Option **Allgemeine Funktionen**, und klicken Sie anschließend auf **Mathematisch**.  
  
4.  Doppelklicken Sie in der Liste **Element** auf **Round**.  
  
5.  Klicken Sie in der Liste **Kategorie** auf **Felder (Ausdrücke)**, und doppelklicken Sie in der Liste **Werte** auf **YTDPurchase**.  
  
7.  Geben Sie unmittelbar hinter `Fields!YTDPurchase.Value`ein Minuszeichen  **-** ein. 
  
9. Erweitern Sie erneut die **Allgemeinen Funktionen** , klicken Sie auf **Aggregat**, und doppelklicken Sie in der Liste **Element** auf **Avg**.  
  
11. Klicken Sie in der Liste **Kategorie** auf **Felder (Ausdrücke)**, und doppelklicken Sie in der Liste **Werte** auf **YTDPurchase**.  
  
13. Geben Sie unmittelbar hinter `Fields!YTDPurchase.Value` **, "Expressions"))**ein.  
  
    Der vollständige Ausdruck lautet wie folgt: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`.  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. Wählen Sie als **Maßeinheit für Status** **Numerisch**aus.  
  
17. Klicken Sie in der Reihe mit dem Pfeil nach unten auf die Schaltfläche **fx** rechts neben dem Textfeld für den **Start** -Wert.  

    ![Berichts-Generator-Ausdruck-Tutorial-Indikator-starten](../reporting-services/media/report-builder-expression-tutorial-indicator-start.png)
  
18. Erweitern Sie im Dialogfeld **Ausdruck** die Option **Allgemeine Funktionen**, und klicken Sie anschließend auf **Mathematisch**.  
  
19. Doppelklicken Sie in der Liste **Element** auf **Round**.  
  
20. Klicken Sie in der Liste **Kategorie** auf **Felder (Ausdrücke)**, und doppelklicken Sie in der Liste **Werte** auf **YTDPurchase**.  
  
22. Geben Sie unmittelbar hinter `Fields!YTDPurchase.Value`ein Minuszeichen  **-** ein. 
  
24. Erweitern Sie erneut die **Allgemeinen Funktionen** , klicken Sie auf **Aggregat**, und doppelklicken Sie in der Liste **Element** auf **Avg**.  
  
26. Klicken Sie in der Liste **Kategorie** auf **Felder (Ausdrücke)**, und doppelklicken Sie in der Liste **Werte** auf **YTDPurchase**.  
  
28. Geben Sie unmittelbar hinter `Fields!YTDPurchase.Value` **, "Expressions")) < 0** ein.  
  
    Der vollständige Ausdruck lautet wie folgt: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. Geben Sie im Textfeld **Ende** den Wert **0**ein  
  
32. Klicken Sie auf die Zeile mit dem horizontalen Pfeil, und klicken Sie auf **Löschen**.  

    ![Berichts-Generator-Ausdruck-Tutorial-Indikatorstatus-löschen](../reporting-services/media/report-builder-expression-tutorial-delete-indicator-state.png)
    
    Nun gibt es nur noch zwei Pfeile, die nach oben und nach unten zeigen.
  
33. Geben Sie in der Zeile mit dem nach oben zeigenden Pfeil im Feld **Start** den Wert **0**ein  
  
34. Klicken Sie auf die Schaltfläche **fx** rechts neben dem Textfeld für den **Ende** -Wert.  
  
35. Löschen Sie im Dialogfeld **Ausdruck** **100** , und erstellen Sie den folgenden Ausdruck: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. Klicken Sie auf **OK** , um das Dialogfeld **Indikatoreigenschaften** zu schließen.  
  
38. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  

    ![Berichts-Generator-Ausdruck-Tutorial-Vorschauindikator](../reporting-services/media/report-builder-expression-tutorial-preview-indicator.png)
  
## <a name="GreenBar"></a>8. Erstellen eines gebänderten Berichts  
Erstellen Sie einen Parameter, damit die Leser des Berichts die Farbe bestimmen können, die abwechselnd auf die Zeilen im Bericht angewendet wird und diesen zu eine gebänderten Bericht machen.  
  
### <a name="to-add-a-parameter"></a>So fügen Sie einen Parameter hinzu  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie im Bereich **Berichtsdaten** mit der rechten Maustaste auf **Parameter** und anschließend auf **Parameter hinzufügen**.  

    ![Berichts-Generator-Ausdruck-Tutorial-Parameter-hinzufügen](../reporting-services/media/report-builder-expression-tutorial-add-parameter.png)
  
    Das Dialogfeld **Berichtsparametereigenschaften** wird geöffnet.  
  
3.  Geben Sie in die **Eingabeaufforderung** **Farbe auswählen**ein  
  
4.  Geben Sie in **Name** **Spaltenfarbe**ein  
  
5.  Klicken Sie auf der Registerkarte **Verfügbare Werte** auf die Option **Werte angeben**.  
  
7.  Klicken Sie auf **Hinzufügen**.  
  
8.  Geben Sie im Feld **Bezeichnung**  **Gelb**ein.  
  
9. Geben Sie im Feld **Wert** Folgendes ein: **Gelb**  
  
10. Klicken Sie auf **Hinzufügen**.  
  
11. Geben Sie im Feld **Bezeichnung** Folgendes ein: **Grün**  
  
12. Geben Sie im Feld **Wert** Folgendes ein: **Blassgrün**  
  
13. Klicken Sie auf **Hinzufügen**.  
  
14. Geben Sie im Feld **Bezeichnung** Folgendes ein: **Blau**  
  
15. Geben Sie im Feld **Wert** Folgendes ein: **Hellblau**  
  
16. Klicken Sie auf **Hinzufügen**.  
  
17. Geben Sie im Feld **Bezeichnung** Folgendes ein: **Rosa**  
  
18. Geben Sie im Feld **Wert** Folgendes ein: **Rosa**  

    ![Berichts-Generator-Ausdruck-Tutorial-verfügbare-Parameter](../reporting-services/media/report-builder-expression-tutorial-parameter-available.png)
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-apply-alternating-colors-to-detail-rows"></a>So wenden Sie abwechselnde Farben auf Detailzeilen an  
  
1.   Wählen Sie die gesamte Zelle in der Datenzeile mit Ausnahme der Zelle in der **M/W** -Spalte aus, die eine eigene Hintergrundfarbe aufweist.  

     ![Berichts-Generator-Ausdruck-Tutorial-gebändert-auswählen](../reporting-services/media/report-builder-expression-tutorial-select-banded.png)
  
4.  Klicken Sie im Bereich „Eigenschaften“ auf **BackgroundColor**. 

     Wenn der Eigenschaftenbereich nicht angezeigt wird, wählen Sie auf der Registerkarte **Ansicht** das Kästchen **Eigenschaften** aus.  
  
    Wenn die Eigenschaften im Eigenschaftenbereich nach Kategorie aufgeführt werden, finden Sie **BackgroundColor** in der Kategorie **Verschiedenes** .  
  
5.  Klicken Sie auf den Pfeil nach unten und anschließend auf **Ausdruck**.  

    ![Berichts-Generator-Ausdruck-Tutorial-Eigenschaft-gebänderte-Farben](../reporting-services/media/report-builder-expression-tutorial-banded-color-property.png)
  
6.  Erweitern Sie im Dialogfeld **Ausdruck** die Option **Allgemeine Funktionen**, und klicken Sie anschließend auf **Programmfluss**.  
  
7.  Doppelklicken Sie in der Liste **Element** auf **IIf**.  
  
8.  Klicken Sie unter **Allgemeine Funktionen**auf **Verschiedenes**, und doppelklicken Sie in der Liste **Element** auf **RowNumber**.  

9. Geben Sie unmittelbar hinter **RowNumber(**  **Nothing) MOD 2,**ein.
  
8. Klicken Sie auf **Parameter** und doppelklicken Sie in der Liste **Werte** auf **Spaltenfarbe**.  
  
22. Geben Sie unmittelbar hinter `Parameters!RowColor.Value` **, “White”)**ein.  
  
    Der vollständige Ausdruck lautet wie folgt: `=IIF(RowNumber(Nothing) MOD 2, Parameters!RowColor.Value, “White”)`.  
    
    ![Berichts-Generator-Ausdruck-Tutorial-Ausdruck-gebänderte-Farben](../reporting-services/media/report-builder-expression-tutorial-banded-color-expressn.png)
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="run-the-report"></a>Führen Sie den Bericht aus  
  
1.  Klicken Sie auf der Registerkarte **Stamm** auf **Ausführen**.  

    Wenn Sie den Bericht nun ausführen, wird er nicht angezeigt, bis Sie eine Farbe für die nicht weißen Bänder festgelegt haben.
  
3.  Wählen Sie in der Liste **Farbe** eine Farbe für die nicht weißen Bänder im Bericht aus.  
    
    ![Berichts-Generator-Ausdruck-Tutorial-Farbe-auswählen](../reporting-services/media/report-builder-expression-tutorial-select-color.png)
  
4.  Klicken Sie auf **Bericht anzeigen**.  
  
    Der Bericht wird gerendert und die abwechselnden Zeilen weisen den gewünschten Hintergrund auf. 
    
    ![Berichts-Generator-Ausdruck-Tutorial-Vorschau-gebändert](../reporting-services/media/report-builder-expression-tutorial-preview-banded.png) 
  
## <a name="Title"></a>Hinzufügen eines Berichtstitels (optional)  
Hinzufügen eines Titels zu einem Bericht  
  
### <a name="to-add-a-report-title"></a>So fügen Sie einen Berichtstitel hinzu  
  
1.  Klicken Sie auf der Entwurfsoberfläche auf **Zum Hinzufügen eines Titels klicken**.  
  
2.  Geben Sie **Sales Comparison Summary**(Übersicht über den Umsatzvergleich) ein, und wählen Sie dann den Text aus.  
  
3.  Legen Sie auf der Registerkarte **Stamm** im Feld **Schriftart** Folgendes fest:

    -  Größe = 18
    -  Farbe = Grau
    -  Fett
  
4.  Klicken Sie auf der Registerkarte **Stamm** auf **Ausführen**.  
  
3.  Wählen Sie eine Farbe für die nicht weißen Bänder im Bericht aus, und klicken Sie auf **Bericht anzeigen**.  
  
## <a name="Save"></a>Sichern des Berichts (optional)  
Sie können Berichte auf einem Berichtsserver, in einer SharePoint-Bibliothek oder auf dem Computer speichern. Weitere Informationen finden Sie unter [Speichern von Berichten &#40;Berichts-Generator&#41;](../reporting-services/report-builder/saving-reports-report-builder.md).  
  
In diesem Tutorial speichern Sie den Bericht auf einem Berichtsserver. Wenn Sie keinen Zugriff auf einen Berichtsserver besitzen, speichern Sie den Bericht auf dem Computer.  
  
### <a name="to-save-the-report-to-a-report-server"></a>So speichern Sie den Bericht auf einem Berichtsserver  
  
1.  Klicken Sie im Menü **Datei** auf **Speichern unter**.  
  
2.  Klicken Sie auf **Letzte Sites und Server**.  
  
3.  Wählen Sie den Namen des Berichtsservers aus, auf dem Sie zum Speichern von Berichten berechtigt sind, oder geben Sie ihn ein.  
  
    Die Meldung "Verbindung mit Berichtsserver wird hergestellt" wird angezeigt. Nachdem die Verbindung hergestellt wurde, sehen Sie den Inhalt des Berichtsordners, den der Berichtsserveradministrator als Standardspeicherort für Berichte angegeben hat.  
  
4.  Benennen Sie den Bericht, und klicken Sie auf **Speichern**.  
  
Der Bericht wird auf dem Berichtsserver gespeichert. Der Name des Berichtsservers, mit dem Sie verbunden sind, wird in der Statusleiste unten im Fenster angezeigt.

Die Leser Ihres Berichts können den Bericht nun im [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Webportal anzeigen.

![Berichts-Generator-Ausdruck-Tutorial-endgültige-Version-im-Browser](../reporting-services/media/report-builder-expression-tutorial-final-in-browser.png)

   
## <a name="see-also"></a>Siehe auch  
[Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
[Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
[Indikatoren &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
[Bilder, Textfelder, Rechtecke und Linien &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)  
[Tabellen &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[Berichtsdatasets &#40;SSRS&#41;](../reporting-services/report-data/report-datasets-ssrs.md)  
  
  
  


