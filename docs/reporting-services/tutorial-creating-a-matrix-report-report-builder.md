---
title: 'Lernprogramm: Erstellen eines Matrixberichts (Berichts-Generator) | Microsoft Docs'
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
ms.assetid: 9ee19c2e-2a8c-4bb0-9274-04a5812c2e96
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ee55d7f9499b638828a6312761dd1b7480a7816c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="tutorial-creating-a-matrix-report-report-builder"></a>Lernprogramm: Erstellen eines Matrixberichts (Berichts-Generator)
Dieses Tutorial zeigt Ihnen die Erstellung eines [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] paginierten Berichts mit einer Matrix von Beispielumsatzdaten in geschachtelten Zeilen- und Spaltengruppen. 

Sie erstellen außerdem eine angrenzende Spaltengruppe, formatieren Spalten und drehen Text. Die folgende Abbildung zeigt einen Bericht, der mit dem Bericht vergleichbar ist, den Sie erstellen werden.  
  
![Berichts-Generator-Matrix-Tutorial](../reporting-services/media/report-builder-matrix-tutorial.png)
   
Ungefähre Dauer dieses Lernprogramms: 20 Minuten.  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Voraussetzungen finden Sie unter [Voraussetzungen für Tutorials](../reporting-services/prerequisites-for-tutorials-report-builder.md). 
  
## <a name="CreateMatrix"></a>1. Erstellen eines Matrixberichts und eines Datasets mit dem Assistenten für neue Tabellen oder Matrix  
In diesem Abschnitt wählen Sie eine freigegebene Datenquelle aus, erstellen ein eingebettetes Dataset und zeigen die Daten in einer Matrix an.  
  
> [!NOTE]  
> In diesem Lernprogramm enthält die Abfrage bereits die Datenwerte, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
### <a name="to-create-a-matrix"></a>So erstellen Sie eine Matrix  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
  
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist.  
  
3.  Klicken Sie im rechten Bereich auf **Tabellen- oder Matrix-Assistent**.  
  
4.  Klicken Sie auf der Seite **Dataset auswählen** auf **Dataset erstellen**.  
  
5.  Klicken Sie auf **Weiter**.  
  
6.  Wählen Sie auf der Seite **Verbindung mit einer Datenquelle auswählen** eine vorhandene Datenquelle aus oder navigieren Sie zum Berichtsserver und wählen Sie eine Datenquelle aus. Falls keine Datenquelle verfügbar ist oder Sie über keinen Zugriff auf einen Berichtsserver verfügen, können Sie stattdessen eine eingebettete Datenquelle verwenden. Weitere Informationen zum Erstellen einer eingebetteten Datenquelle finden Sie unter [Tutorial: Erstellen eines einfachen Tabellenberichts &#40;Berichts-Generator&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Klicken Sie auf **Weiter**.  
  
8.  Klicken Sie auf der Seite **Abfrage entwerfen** auf **Als Text bearbeiten**.  
  
9. Kopieren Sie die folgende Abfrage, und fügen Sie sie in den Abfragebereich ein:  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
10. (optional) Klicken Sie auf das Symbol „Ausführen“ (!), um die Abfrage auszuführen und die Daten anzuzeigen.

11. Klicken Sie auf **Weiter**.  
  
## <a name="Groups"></a>2. Organisieren von Daten und Auswählen des Layouts mit dem Tabellen- oder Matrix-Assistenten  
Stellen Sie mithilfe des Assistenten einen Startentwurf für die Anzeige von Daten bereit. Im Vorschaufenster des Assistenten können Sie das Ergebnis der Datengruppierung visualisieren, bevor Sie den Matrixentwurf abschließen.  
  
1.  Ziehen Sie auf der Seite **Felder anordnen** „Territory“ von **Verfügbare Felder** nach **Zeilengruppen**.  
  
2.  Ziehen Sie „SalesDate“ in **Zeilengruppen** und platzieren Sie das Feld unter „Territory“.  
  
    Die Gruppenhierarchie wird durch die Reihenfolge, in der Felder in **Zeilengruppen** aufgeführt sind, definiert. Durch die Schritte 1 und 2 werden die Werte der Felder zuerst nach Gebiet und dann nach Verkaufsdatum angeordnet.  
  
3.  Ziehen Sie die „Subcategory“ in **Spaltengruppen**.  
  
4.  Ziehen Sie „Product“ in **Spaltengruppen** und ordnen Sie das Feld anschließend unter „Subcategory“ an.  
  
    Die Gruppenhierarchie wird durch die Reihenfolge, in der Felder in **Spaltengruppen** aufgeführt sind, definiert. Durch die Schritte 3 und 4 werden die Werte für die Felder zuerst nach Unterkategorie und anschließend nach Produkt geordnet.  
  
5.  Ziehen Sie „Sales“ in **Werte**.  
  
    Sales wird mit der Sum-Funktion zusammengefasst, der Standardfunktion zum Summieren numerischer Felder.  
  
6.  Ziehen Sie „Quantity“ in **Werte**.  
  
    Quantity wird mit der Sum-Funktion zusammengefasst.  
  
    In Schritt 5 und 6 werden die Daten angegeben, die in den Matrixdatenzellen angezeigt werden sollen.
    
    ![Berichts-Generator-Anordnen von Feldern-Berichts-Assistent](../reporting-services/media/report-builder-arrange-fields-report-wizard.png)  
  
7.  Klicken Sie auf **Weiter**.  
  
8.  Vergewissern Sie sich auf der Seite „Layout auswählen“, dass unter **Optionen**die Option **Teil- und Gesamtergebnisse anzeigen** ausgewählt ist.  
  
9. Überprüfen Sie, ob **Als Block, Teilergebnis unterhalb** ausgewählt ist.  
  
10. Überprüfen Sie, ob die Option **Gruppen erweitern/reduzieren** ausgewählt ist.  
  
11. Klicken Sie auf **Weiter**.  
  
13. Klicken Sie auf **Fertig stellen**.  
  
    Die Matrix wird der Entwurfsoberfläche hinzugefügt. Im Bereich Zeilengruppen werden zwei Zeilengruppen angezeigt: Territory und SalesDate. Im Bereich Spaltengruppen werden zwei Spaltengruppen angezeigt: Subcategory und Product. Detaildaten sind alle Daten, die von der Datasetabfrage abgerufen werden.  
    
    ![Berichts-Generator-Zeilengruppen-und-Spaltengruppen](../reporting-services/media/report-builder-row-and-column-groups.png)
  
14. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
    Für jedes Produkt, das an einem bestimmten Datum verkauft wird, werden in der Matrix die Unterkategorie, zu der das Produkt gehört, und das Verkaufsgebiet angezeigt.  

14. Erweitern Sie eine Unterkategorie. Sie können sehen, dass der Bericht schnell sehr breit wird.

![Berichts-Generator-Matrix-erweitern](../reporting-services/media/report-builder-expand-matrix.png)
  
## <a name="FormatData"></a>3. Formatieren von Daten  
Standardmäßig wird in den Zusammenfassungsdaten für das Feld Sales eine allgemeine Zahl angezeigt, wohingegen im Feld SalesDate sowohl Datums- als auch Uhrzeitangaben angezeigt werden. In diesem Abschnitt formatieren Sie das Feld „Sales“, um die Zahl als Währung anzuzeigen und das Feld „SalesDate“, um nur das Datum anzuzeigen. Ändern Sie die Einstellung der Option **Platzhalterformate** , um formatierte Textfelder und Platzhaltertext als Beispielwerte anzuzeigen.  
  
### <a name="to-format-fields"></a>So formatieren Sie Felder  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zu wechseln.  
  
2.  Drücken Sie die STRG-TASTE, und wählen Sie dann die neun Zellen aus, die `[Sum(Sales)]` enthalten.  
  
3.  On the **Home** tab > **Number** > **Currency**. Die Zellen ändern sich, um die formatierte Währung anzuzeigen.  
  
    Wenn Sie das Gebietsschema „Deutsch (Deutschland)“ verwenden, lautet der Standardbeispieltext [**12,345.00€**]. Falls kein Beispielwährungswert angezeigt wird, klicken Sie in der Gruppe **Zahlen** auf **Platzhalterformate**  >  **Beispielwerte**.  
    
    ![Berichts-Generator-Platzhalter-Werte](../reporting-services/media/report-builder-placeholder-value.png)
  
4.  Klicken Sie auf die Zelle, die `[SalesDate]` enthält.  
  
5.  Wählen Sie in der Gruppe **Zahl** im Einblendmenü die Einstellung **Datum**.  
  
    In der Zelle wird das Beispieldatum **[31.01.2000]** angezeigt. Falls kein Beispieldatum angezeigt wird, klicken Sie in der Gruppe **Zahlen** auf **Platzhalterformate** und anschließend auf **Beispielwerte**.  
  
6.  Klicken Sie auf **Ausführen** , um den Bericht in der Vorschau anzuzeigen.  
  
In den Datumswerten werden nur Datumsangaben angezeigt, und die Umsatzwerte werden als Währung angezeigt.  
  
## <a name="AdjacentGroup"></a>4. Hinzufügen einer angrenzenden Spaltengruppe  
Sie können Zeilen- und Spaltengruppen in Beziehungen über- und untergeordneter Objekte oder angrenzend in Beziehungen gleichgeordneter Objekte schachteln.  
  
In diesem Abschnitt fügen Sie eine Spaltengruppe hinzu, die an die Spaltengruppe „Subcategory“ grenzt, kopieren Zellen, um die neue Spaltengruppe aufzufüllen, und verwenden anschließend einen Ausdruck, um den Wert der Spaltengruppenkopfzeile zu erstellen.  
  
### <a name="to-add-an-adjacent-column-group"></a>So fügen Sie eine angrenzende Spaltengruppe hinzu  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Zelle, die `[Subcategory]`enthält, zeigen Sie auf **Gruppe hinzufügen**und klicken Sie anschließend auf **Angrenzend rechts**.  
  
    Das Dialogfeld **Tablix-Gruppe** wird geöffnet.  
  
3.  Wählen Sie in der Liste **Gruppieren nach** die Option SalesDate aus und klicken Sie anschließend auf **OK**.  
  
    Rechts neben der Spaltengruppe „Subcategory“ wird eine neue Spaltengruppe hinzugefügt.  
  
4.  Klicken Sie mit der rechten Maustaste auf die Zelle in der neuen Spaltengruppe, die `[SalesDate],` enthält, und klicken Sie anschließend auf **Ausdruck**.  
  
5.  Kopieren Sie den folgenden Ausdruck in das Feld „Ausdruck festlegen für:“.  
  
    ```  
    =WeekdayName(DatePart("w",Fields!SalesDate.Value))  
    ```  
  
    Mit diesem Ausdruck wird der Name des Wochentags aus dem Verkaufsdatum extrahiert. Weitere Informationen finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
6.  Klicken Sie mit der rechten Maustaste auf die Zelle „Gesamt“ in der Spaltengruppe „Subcategory“, und klicken Sie anschließend auf **Kopieren**.  
  
7.  Klicken Sie mit der rechten Maustaste auf die Zelle, die sich unmittelbar unter der Zelle mit dem Ausdruck befindet, den Sie in Schritt 5 erstellt haben, und klicken Sie anschließend auf **Einfügen**.  
  
8.  Drücken Sie die STRG-TASTE.  
  
9. Markieren Sie in der Gruppe „Subcategory“ die Spaltenüberschrift „Sales“ und die darunter liegenden drei Zellen und klicken Sie mit der rechten Maustaste darauf. Klicken Sie anschließend auf **Kopieren**.  
  
10. Fügen Sie die vier Zellen in die vier leeren Zellen in der neuen Spaltengruppe ein.  
  
11. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Der Bericht enthält Spalten mit der Bezeichnung "Montag" und "Dienstag". Das Dataset enthält nur Daten für diese zwei Tage.  

![Berichts-Generator-Matrix-Wochentage](../reporting-services/media/report-builder-matrix-weekdays.png)
  
> [!NOTE]  
> Wenn die Daten andere Tage einschließen würden, würde der Bericht auch Spalten für diese Tage enthalten. Jede Spalte besitzt die Spaltenüberschrift **Sales**und den Gesamtumsatz nach Gebiet.  
  
## <a name="Width"></a>5. Ändern der Spaltenbreite  
Ein Bericht, der eine Matrix enthält, wird bei der Ausführung normalerweise horizontal und vertikal erweitert. Die Steuerung der horizontalen Erweiterung ist besonders wichtig, wenn Sie beabsichtigen, den Bericht in Formate wie z. B. Microsoft Word oder Adobe PDF zu exportieren, die für gedruckte Berichte verwendet werden. Wenn sich der Bericht horizontal über mehrere Seiten erstreckt, ist der gedruckte Bericht schwer verständlich. Um die horizontale Erweiterung zu minimieren, können Sie die Breite der Spalten so anpassen, dass die Daten darin ohne Zeilenumbruch angezeigt werden. Sie können auch Spalten umbenennen, damit ihre Titel der Breite entsprechen, die zum Anzeigen der Daten erforderlich ist.  
  
### <a name="to-rename-and-resize-the-columns"></a>So benennen Sie Spalten um und ändern deren Größe  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Wählen Sie den Text in der Spalte „Quantity“ ganz links aus, und geben Sie anschließend **QTY**ein.  
  
    Der Spaltentitel lautet nun QTY.  
  
3.  Wiederholen Sie Schritt 2 für die beiden anderen Spalten mit dem Namen Quantity.
  
4.  Klicken Sie auf die Matrix, damit die Spalten- und Zeilenhandles oberhalb und neben der Matrix angezeigt werden.  
  
    Die grauen Balken oberhalb und neben der Tabelle stellen die Spalten- und Zeilenhandles dar.  
    
    ![Berichts-Generator-Spaltenhandles](../reporting-services/media/report-builder-column-handles.png)
  
5.  Wenn Sie die Größe der QTY-Spalte ganz links ändern möchten, zeigen Sie auf die Linien zwischen den Spaltenhandles, damit stammt dem Cursor ein Doppelpfeil angezeigt wird. Ziehen Sie die Spalte nach links bis zu einer Breite von ca. 1,3 cm.  
  
    Eine Spaltenbreite von ca. 1,3 cm ist für das Anzeigen der Menge ausreichend.  
  
6.  Wiederholen Sie Schritt 5 für die anderen Spalten mit dem Namen QTY.  
  
7.  Klicken Sie auf **Ausführen** , um den Bericht in der Vorschau anzuzeigen.  
  
Die Spalten mit Mengen sind nun schmaler und mit „QTY“ benannt.  
  
## <a name="MergeCells"></a>6. Verbinden von Matrixzellen  
Der Eckenbereich befindet sich oben links in der Matrix. Abhängig von der Anzahl der Zeilen- und Spaltengruppen in der Matrix unterscheidet sich die Anzahl der Zellen im Eckenbereich. Die in diesem Lernprogramm erstellte Matrix enthält vier Zellen in ihrem Eckenbereich. Die Zellen werden in zwei Zeilen und zwei Spalten angeordnet und spiegeln die Tiefe der Zeilen- und Spaltengruppenhierarchien wider. Die vier Zellen werden nicht in diesem Bericht verwendet und zu einer Zelle verbunden.  
  
### <a name="to-merge-matrix-cells"></a>So verbinden Sie Matrixzellen  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie auf die Matrix, damit die Spalten- und Zeilenhandles oberhalb und neben der Matrix angezeigt werden.  
  
3.  Drücken Sie die STRG-TASTE und wählen Sie anschließend die vier Zellen des Eckenbereichs aus.  
  
4.  Klicken Sie mit der rechten Maustaste auf die Zellen und anschließend auf **Zellen zusammenführen**.  
  
5.  Klicken Sie mit der rechten Maustaste auf die zusammengeführte Zelle und anschließend auf **Textfeldeigenschaften**.  
  
6.  On the **Border** tab > **Presets** > **None**.
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Klicken Sie auf **Ausführen** , um den Bericht in der Vorschau anzuzeigen.  
  
Die Zelle in der oberen Ecke der Matrix wird nicht mehr angezeigt. 
  
## <a name="HeaderTitle"></a>7. Hinzufügen eines Berichtskopfs und -titels  
Ein Berichtstitel wird oben im Bericht angezeigt. Sie können den Berichtstitel in eine Berichtskopfzeile einfügen oder, wenn der Bericht keine Kopfzeile enthält, in einem Textfeld am oberen Rand des Berichtshauptteils. In diesem Lernprogramm entfernen Sie das Textfeld am Anfang des Berichts und fügen der Kopfzeile einen Titel hinzu.  
  
### <a name="to-add-a-report-header-and-report-title"></a>So fügen Sie eine Berichtskopfzeile und einen Berichtstitel hinzu  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Wählen Sie das Textfeld am Anfang des Berichtstexts, das **Zum Hinzufügen eines Titels klicken** enthält, und drücken Sie anschließend die ENTF-TASTE.  
  
3.  Klicken sie auf der Registerkarte **Einfügen** auf **Kopfzeile**  >  **Kopfzeile hinzufügen**.  
  
    Am Anfang des Berichtstexts wird eine Kopfzeile hinzugefügt.  
  
4.  Klicken Sie auf der Registerkarte **Einfügen** auf **Textfeld**und ziehen Sie anschließend ein Textfeld in den Berichtskopf. Erweitern Sie das Textfeld auf eine Länge von etwa 15 cm und eine Höhe von etwa 2 cm, und platzieren Sie es links neben der Berichtskopfzeile.  
  
5.  Geben Sie im Textfeld **Umsatz nach Territory, Subcategory und Tag** ein.  
  
6.  Markieren Sie den Text, den Sie eingegeben haben, und nehmen Sie anschließend unter **Stamm** > **Schriftart** folgende Einstellungen vor:
    * **Größe 24 pt**
    * **Farbe Kastanienbraun**
 
10. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Der Bericht enthält einen Berichtstitel in der Kopfzeile des Berichts.  
  
## <a name="Save"></a>8. Speichern des Berichts  
Sie können Berichte auf einem Berichtsserver, in einer SharePoint-Bibliothek oder auf dem Computer speichern.  
  
Speichern Sie in diesem Lernprogramm den Bericht auf einem Berichtsserver. Wenn Sie keinen Zugriff auf einen Berichtsserver besitzen, speichern Sie den Bericht auf dem Computer.  
  
### <a name="to-save-the-report-on-a-report-server"></a>So speichern Sie den Bericht auf einem Berichtsserver  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Letzte Sites und Server**.  
  
3.  Wählen Sie den Namen des Berichtsservers aus, auf dem Sie zum Speichern von Berichten berechtigt sind, oder geben Sie ihn ein.  
  
    Die Meldung "Verbindung mit Berichtsserver wird hergestellt" wird angezeigt. Nachdem die Verbindung hergestellt wurde, sehen Sie den Inhalt des Berichtsordners, den der Berichtsserveradministrator als Standardspeicherort für Berichte angegeben hat.  
  
4.  Ersetzen Sie im Feld **Name**den Standardnamen durch **SalesByTerritorySubcategory**.  
  
5.  Klicken Sie auf **Speichern**.  
  
Der Bericht wird auf dem Berichtsserver gespeichert. Der Name des Berichtsservers, mit dem Sie verbunden sind, wird in der Statusleiste unten im Fenster angezeigt.  
  
#### <a name="to-save-the-report-on-your-computer"></a>So speichern Sie den Bericht auf dem Computer  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Desktop**, **Meine Dokumente**oder **Arbeitsplatz**, und navigieren Sie anschließend zu dem Ordner, in dem Sie den Bericht speichern möchten.  
  
3.  Ersetzen Sie im Feld **Name**den Standardnamen durch **SalesByTerritorySubcategory**.  
  
4.  Klicken Sie auf **Speichern**.  
  
## <a name="RotateTextBox"></a>9. (Optional) Drehen des Textfelds um 270 Grad  
Ein Bericht mit Matrizen kann bei der Ausführung horizontal und vertikal erweitert werden. Durch vertikales Drehen der Textfelder oder um 270 Grad können Sie in horizontaler Richtung Platz sparen. Der gerenderte Bericht ist in diesem Fall schmäler und passt beim Exportieren in ein Format wie Microsoft Word mit einer höheren Wahrscheinlichkeit auf eine gedruckte Seite.  
  
In einem Textfeld kann Text auch horizontal und vertikal (von oben nach unten) angezeigt werden. Weitere Informationen finden Sie unter [Textfelder &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md).  
  
### <a name="to-rotate-text-box-270-degrees"></a>So drehen Sie das Textfeld um 270 Grad  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie auf die Zelle, die „[Territory]“ enthält. `[Territory].` 

    >**Hinweis**: Wählen Sie die Zelle aus, nicht den Text. Die Eigenschaft „WritingMode“t ist nur für die Zelle verfügbar.
    
     ![Berichts-Generator-Auswählen-der-Zelle-Territory](../reporting-services/media/report-builder-select-territory-cell.png)
  
3.  Suchen Sie im Fensterbereich die Eigenschaft „WritingMode“ und ändern Sie den Schreibmodus von **Default** auf **Rotate270**.  
  
    Wenn der Eigenschaftenbereich nicht geöffnet ist, klicken Sie auf die Registerkarte **Ansicht** des Menübands und aktivieren Sie das Kontrollkästchen **Eigenschaften**.  
  
4.  Vergewissern Sie sich, dass die „CanGrow“-Eigenschaft auf **True** festgelegt wurde.  
  
5.  Klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Absatz** auf die Schaltflächen **Mitte** und **Zentriert**, um den Text sowohl vertikal als auch horizontal im Mittelpunkt der Zelle zu platzieren.  
 
6. Ändern Sie die Breite der Spalte "Territory" auf ca. 1,3 cm, und löschen Sie den Spaltentitel.  
6.  Klicken Sie auf **Ausführen** , um den Bericht in der Vorschau anzuzeigen.  
  
Der Gebietsname wird vertikal geschrieben (von unten nach oben). Die Höhe der Zeilengruppe "Territory" ändert sich abhängig von der Länge des Gebietsnamens.  
  
## <a name="next-steps"></a>Nächste Schritte  
Hiermit ist das Lernprogramm für die Erstellung eines Matrixberichts abgeschlossen. Weitere Informationen zu Matrizen finden Sie unter: 
-    [Tabellen, Matrizen und Listen](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)
-    [Erstellen einer Matrix (Berichts-Generator und SSRS)](../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)
-    [Zonen des Tablix-Datenbereichs](../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md) 
-    [Zellen, Zeilen und Spalten des Tablix-Datenbereichs](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Siehe auch  
[Lernprogramme für den Berichts-Generator](../reporting-services/report-builder-tutorials.md)  
[Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  


