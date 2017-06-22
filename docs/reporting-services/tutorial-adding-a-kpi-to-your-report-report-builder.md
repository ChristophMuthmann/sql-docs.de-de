---
title: "Lernprogramm: Hinzufügen eines KPIS zu einem Bericht (Berichts-Generator) | Microsoft Docs"
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
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
caps.latest.revision: 13
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6ff993552c5c5b8a3e48c672a29f6567107f2331
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>Lernprogramm: Hinzufügen eines KPIs zu einem Bericht (Berichts-Generator)
In diesem [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] -Tutorial fügen Sie eine Leistungskennzahl (key performance indicator; KPI) zu einem paginierten [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Bericht hinzu.  

KPIs sind für Unternehmen bedeutende, messbare Werte. In diesem Szenario ist die Verkaufszusammenfassung nach Produktunterkategorien der KPI. Der aktuelle Status der KPI wird mithilfe von Farben, Messgeräten und Indikatoren angezeigt.
  
Die folgende Abbildung ähnelt dem Bericht, den Sie erstellen werden.  
  
![Berichts-Generator-KPI-Bericht](../reporting-services/media/report-builder-kpi-report.png)
    
> [!NOTE]  
> In diesem Lernprogramm werden die Schritte für den Assistenten in zwei Verfahren zusammengefasst: ein Verfahren zum Erstellen des Datasets und ein Verfahren zum Erstellen einer Tabelle. Im ersten Tutorial dieser Reihe erhalten Sie Schritt-für-Schritt-Anweisungen zum Navigieren zu einem Berichtsserver, Auswählen einer Datenquelle, Erstellen eines Datasets und Ausführen des Assistenten: [Tutorial: Erstellen eines einfachen Tabellenberichts &#40;Berichts-Generator&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Geschätzte Zeit zum Bearbeiten dieses Tutorials: 15 Minuten.  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Anforderungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Table"></a>1. Erstellen eines Tabellenberichts und eines Datasets mit dem Tabellen- oder Matrix-Assistenten  
In diesem Abschnitt wählen Sie eine freigegebene Datenquelle aus, erstellen ein eingebettetes Dataset und zeigen die Daten in einer Tabelle an.  
 
### <a name="to-create-a-table-with-an-embedded-dataset"></a>So erstellen Sie eine Tabelle mit einem eingebetteten Dataset  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
  
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist.  
  
3.  Klicken Sie im rechten Bereich auf **Tabellen- oder Matrix-Assistent**.  
  
4.  Klicken Sie auf der Seite **Dataset auswählen** auf **Dataset erstellen**.  
  
5.  Klicken Sie auf **Weiter**.  
  
6.  Wählen Sie auf der Seite **Verbindung mit einer Datenquelle auswählen** eine vorhandene Datenquelle aus, oder navigieren Sie zum Berichtsserver, und wählen Sie eine Datenquelle aus. Falls dort keine Datenquelle verfügbar ist oder Sie keinen Zugriff auf einen Berichtsserver haben, können Sie stattdessen eine eingebettete Datenquelle verwenden. Weitere Informationen finden Sie unter [Tutorial: Erstellen eines einfachen Tabellenberichts &#40;Berichts-Generator&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Klicken Sie auf **Weiter**.  
  
8.  Klicken Sie auf der Seite **Abfrage entwerfen** auf **Als Text bearbeiten**.  
  
9. Kopieren Sie die folgende Abfrage, und fügen Sie sie in den Abfragebereich ein:  

    > [!NOTE]  
    > In diesem Lernprogramm sind die Datenwerte in der Abfrage enthalten, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. Klicken Sie auf der Symbolleiste des Abfrage-Designers auf „Ausführen“ (**!**).

11. Klicken Sie auf **Weiter**.  
  
## <a name="CompleteWizard"></a>2. Organisieren von Daten und Auswählen des Layouts im Assistenten  
Der Tabellen- oder Matrix-Assistent stellt ein erstes Design für die Darstellung von Daten bereit. Im Vorschaufenster des Assistenten können Sie das Ergebnis der Datengruppierung visualisieren, bevor Sie den Tabellen- oder Matrixentwurf abschließen.  
  
### <a name="to-organize-data-into-groups-and-choose-a-layout"></a>So organisieren Sie Daten in Gruppen und wählen ein Layout aus 
  
1.  Ziehen Sie auf der Seite „Felder anordnen“ das Feld „Product“ in **Werte**.  
  
2.  Ziehen Sie „Quantity“ in **Werte** , und platzieren Sie es unter „Product“.  
  
    Die Menge wird mit der Sum-Funktion zusammengefasst, der Standardfunktion zum Summieren numerischer Felder.  
  
3.  Ziehen Sie „Sales“ in **Werte** , und fügen Sie dieses Feld unter „Quantity“ ein.  
  
    In Schritt 1, 2 und 3 werden die Daten angegeben, die in der Tabelle angezeigt werden sollen.  
  
4.  Ziehen Sie „SalesDate“ in **Zeilengruppen**.  
  
5.  Ziehen Sie „Subcategory“ in **Zeilengruppen** , und fügen Sie dieses Feld unter „SalesDate“ ein.  
  
    Durch die Schritte 4 und 5 werden die Werte für die Felder zuerst nach Datum und dann nach allen Umsätzen für dieses Datum angeordnet.  
  
6.  Klicken Sie auf **Weiter**.  
  
    Bei der Ausführung des Berichts werden in der Tabelle jedes Datum, alle Aufträge für jedes Datum sowie alle Produkte, Mengen und Umsatzsummen für jeden Auftrag angezeigt.  
  
7.  Vergewissern Sie sich auf der Seite „Layout auswählen“, dass unter **Optionen**die Option **Teil- und Gesamtergebnisse anzeigen** ausgewählt ist.  
  
8.  Überprüfen Sie, ob **Als Block, Teilergebnis unterhalb** ausgewählt ist.  
  
9. Deaktivieren Sie die Option **Gruppen erweitern/reduzieren**.  
  
    In diesem Lernprogramm enthält der erstellte Bericht keine Drilldownfunktion, mit der ein Benutzer eine übergeordnete Gruppenhierarchie einblenden kann, um untergeordnete Gruppenzeilen und Detailzeilen anzuzeigen.  
  
10. Klicken Sie auf **Weiter**.  
  
11. Klicken Sie auf **Fertig stellen**.  
  
      Die Tabelle wird der Entwurfsoberfläche hinzugefügt. Die Tabelle enthält fünf Spalten und fünf Zeilen. Im Bereich "Zeilengruppen" werden drei Zeilengruppen angezeigt: "SalesDate", "Subcategory" und "Details". Detaildaten sind alle Daten, die von der Datasetabfrage abgerufen werden. Der Bereich „Spaltengruppen“ ist leer.  
      
      ![Berichts-Generator-KPI-Zeilengruppen](../reporting-services/media/report-builder-kpi-row-groups.png)
  
12. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Für jedes an einem bestimmten Datum verkaufte Produkt werden in der Tabelle der Produktname, die verkaufte Menge und der Gesamtumsatz angezeigt. Die Daten sind zuerst nach Verkaufsdatum und dann nach Unterkategorie organisiert. 

![Berichts-Generator-KPI-einfache-Tabelle](../reporting-services/media/report-builder-kpi-basic-table.png)
    
### <a name="format-dates-and-currency"></a>Formatieren von Datumsangaben und Währung
Erweitern Sie die Spalten, und legen Sie das Format für die Datums- und Währungsangaben fest.

1. Klicken Sie auf **Entwurf** , um wieder zur Entwurfsansicht zurückzuwechseln.

2. Die Produktnamen könnten mehr Platz benötigen. Um die Spalte „Product“ breiter zu gestalten, wählen Sie die gesamte Tabelle aus, und ziehen Sie den rechten Rand des Spaltenziehpunkts am oberen Rand der Product-Spalte.

3. Drücken Sie die STRG-TASTE, und wählen Sie anschließend die vier Zellen aus, die [Sum(Sales)] enthalten.

4. On the **Home** tab > **Number** > **Currency**. Die Zellen ändern sich, um die formatierte Währung anzuzeigen.

   Wenn Sie das Gebietsschema „Deutsch (Deutschland)“ verwenden, lautet der Standardbeispieltext [12.345,00€]. Falls kein Beispielwährungswert angezeigt wird, klicken Sie in der Gruppe **Zahlen** auf **Platzhalterformate**  >  **Beispielwerte**.
    
    ![Berichts-Generator-Schaltfläche-Platzhalterwert](../reporting-services/media/report-builder-placeholder-value-button.png)

5. (Optional) Klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Zahl** zweimal auf die Schaltfläche **Dezimalstellen verringern** , um volle Dollarbeträge ohne Centangaben anzuzeigen.

6. Klicken Sie auf die Zelle, die [SalesDate] enthält.

6. Wählen Sie in der Gruppe **Zahl** im Einblendmenü die Einstellung **Datum**.

   In der Zelle wird das Beispieldatum [1/31/2000] angezeigt. 

12. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
 
![Berichts-Generator-KPI-Zahlen-formatieren](../reporting-services/media/report-builder-kpi-format-numbers.png)

## <a name="BackgroundColors"></a>3. Anzeigen eines KPI mithilfe von Hintergrundfarben  
Hintergrundfarben können für einen Ausdruck festgelegt werden, der beim Ausführen des Berichts ausgewertet wird.  
  
### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>So zeigen Sie den aktuellen Status eines KPI mit Hintergrundfarben an  
  
1.  Klicken Sie in der Tabelle mit der rechten Maustaste die `[Sum(Sales)]` -Zelle (die Teilergebniszeile mit dem Umsatz für eine Unterkategorie), und klicken Sie anschließend auf **Textfeldeigenschaften**. 

    Stellen Sie sicher, dass Sie die Zelle (und nicht den darin enthaltenen Text) ausgewählt haben, um die **Textfeldeigenschaften**anzuzeigen. 
    
    ![Berichts-Generator-Textfeldeigenschaften](../reporting-services/media/report-builder-text-box-properties.png)
  
2.  Klicken Sie auf der Registerkarte **Ausfüllen** auf die Schaltfläche **fx** neben der Option **Füllfarbe** , und geben Sie den folgenden Ausdruck in das Feld **Ausdruck festlegen für: BackgroundColor** ein:  
  
    `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
     Dadurch wird die Hintergrundfarbe für jede Zelle in Limonengrün geändert, die eine aggregierte Summe von `[Sum(Sales)]` enthält, die größer gleich 5.000 ist. Werte von `[Sum(Sales)]` zwischen 2.500 und 5.000 werden gelb eingefärbt. Werte kleiner als 2.500 werden rot eingefärbt.  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
In der Teilergebniszeile, die den Umsatz für eine Unterkategorie anzeigt, ist die Hintergrundfarbe der Zelle abhängig vom Wert der Umsatzsumme rot, gelb oder grün.  

![Berichts-Generator-KPI-Farben](../reporting-services/media/report-builder-kpi-colors.png)
  
## <a name="Gauge"></a>4. Anzeigen eines KPI mit einem Messgerät  
Ein Messgerät stellt einen einzelnen Wert in einem Dataset dar. In diesem Tutorial wird ein horizontales lineares Messgerät verwendet, da es aufgrund seiner Form und Einfachheit auch dann leicht zu lesen ist, wenn es klein ist und innerhalb einer Tabellenzelle verwendet wird. Weitere Informationen finden Sie unter [Messgeräte &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>So zeigen Sie den aktuellen Status eines KPI mit einem Messgerät an  
  
1.  Wechseln Sie zurück in die Entwurfsansicht.  
  
2.  Klicken Sie in der Tabelle mit der rechten Maustaste auf den Spaltenziehpunkt für die Spalte „Sales“, und klicken Sie auf **Spalte einfügen**  >  **Rechts**. Eine neue Spalte wird der Tabelle hinzugefügt.  

    ![Berichts-Generator-KPI-Spalte-einfügen](../reporting-services/media/report-builder-kpi-insert-column.png)
  
3.  Geben Sie in der Spaltenüberschrift **Lineare KPI** ein.  
  
4.  Klicken Sie auf der Registerkarte **Einfügen** auf **Datenvisualisierungen**  >  **Messgerät**, und klicken Sie anschließend außerhalb der Tabelle auf die Entwurfsoberfläche.   
  
5.  Wählen Sie im Dialogfeld **Messgerättyp auswählen** den ersten linearen Messgerättyp (**Horizontal**) aus.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Der Entwurfsoberfläche wird ein Messgerät hinzugefügt.  
  
7.  Ziehen Sie im Bereich „Berichtsdaten“ das `Sales` -Feld in das Messgerät. Der Bereich **Messgerätdaten** wird geöffnet.  
  
    Wenn Sie das `Sales` -Feld auf dem Messgerät ablegen, wird es in der Liste **Werte** hinzugefügt und anhand der integrierten Sum-Funktion aggregiert.  
   
    ![Berichts-Generator-KPI-Sales-Feld-ziehen](../reporting-services/media/report-builder-kpi-drag-sales-field.png)
   
9. Klicken Sie im Bereich **Messgerätdaten** auf den Pfeil neben **LinearPointer1**  >  **Zeigereigenschaften**.  
  
10. Stellen Sie im Dialogfeld **Lineare Zeigereigenschaften** in der Registerkarte **Zeigeroptionen** unter **Zeigertyp** sicher, dass **Leiste** ausgewählt ist. 
 
11. Klicken Sie auf **OK**.  
  
12. Klicken Sie mit der rechten Maustaste auf die Skala im Messgerät, und klicken Sie auf **Skalierungseigenschaften**.  
  
13. Legen Sie im Dialogfeld **Lineare Skalierungseigenschaften** auf der Registerkarte **Allgemein** **Maximum** auf 25.000 fest.  

    > [!NOTE]  
    > Anstelle einer Konstante wie 25.000 können Sie den Wert der Option **Maximum** auch mithilfe eines Ausdrucks dynamisch berechnen. Der Ausdruck würde das Aggregat der Aggregatfunktion verwenden und dem Ausdruck `=Max(Sum(Fields!Sales.value), "Tablix1")`ähneln.  

14. Aktivieren Sie auf der Registerkarte **Bezeichnungen** das Kontrollkästchen **Skalabezeichnungen ausblenden**.

15. Klicken Sie auf **OK**.
  
14. Ziehen Sie das Messgerät innerhalb der Tabelle in die zweite leere Zelle der Spalte „Lineare KPI“, und zwar in die Zeile, die das Teilergebnis „Vertrieb“ für das `Subcategory` -Feld anzeigt, und neben das Feld, in dem Sie die Formel für die Hintergrundfarbe hinzugefügt haben.  
  
    > [!NOTE]  
    > Möglicherweise müssen Sie die Größe der Spalte ändern, damit das horizontale lineare Messgerät in die Zelle passt. Um die Größe einer Spalte anzupassen, wählen Sie die Tabelle aus und ziehen den Spaltenziehpunkt. Daraufhin passt die Berichtsentwurf-Oberfläche die Größe an die Tabelle an.  
  
15. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
    Die horizontale Länge der grünen Leiste im Messgerät ändert sich je nach Wert der KPI.  
  
![Berichts-Generator-KPI-linear](../reporting-services/media/report-builder-linear-kpi.png) 
  
## <a name="Indicator"></a>5. Anzeigen eines KPI mit einem Indikator  
Indikatoren sind kleine einfache Messgeräte, die Datenwerte auf einen Blick darstellen. Aufgrund ihrer Größe und Einfachheit werden Indikatoren oft in Tabellen und Matrizen verwendet. Weitere Informationen finden Sie unter [Indikatoren &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md).  
  
### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>So zeigen Sie den aktuellen Status eines KPI mit einem Indikator an  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Klicken Sie in der Tabelle mit der Maustaste den Spaltenziehpunkt für die Spalte „Lineare KPI“, die Sie in der vorherigen Prozedur hinzugefügt haben, und klicken Sie anschließend auf **Spalte einfügen**  >  **Rechts**. Eine neue Spalte wird der Tabelle hinzugefügt.  
  
3.  Geben Sie in der Spaltenüberschrift **Ampel-KPI** ein.  
  
4.  Klicken Sie auf die Zelle für die Unterkategorie „Teilergebnis“, die sich neben dem linearen Messgerät befindet, das Sie in der vorherigen Prozedur hinzugefügt haben.  
  
5.  Doppelklicken Sie auf der Registerkarte **Einfügen** unter **Datenvisualisierungen** auf **Indikator**.  
  
6.  Wählen Sie im Dialogfeld **Indikatortyp auswählen** unter **Formen** den ersten Formtyp **3 Ampeln (ohne Rand)** aus.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Der Indikator wird der Zelle in der neuen Spalte „Stoplight KPI“ hinzugefügt.  
  
8.  Klicken Sie mit der rechten Maustaste auf den Indikator, und klicken Sie auf **Indikatoreigenschaften**.  
  
9. Wählen Sie auf der Registerkarte **Werte und Status** im Feld **Wert** **[Sum(Sales)]**aus. Ändern Sie keine weiteren Optionen.  
  
    Standardmäßig findet eine Datensynchronisierung im Datenbereich statt, und der Wert **Tablix1**, der Name des Tabellendatenbereichs im Bericht, wird im Feld **Synchronisierungsbereich** angezeigt.  
  
    In diesem Bericht können Sie auch den Bereich eines Indikators ändern, der in der Zelle für das Teilergebnis der Unterkategorie eingefügt wurde, um das Feld "SalesDate" zu synchronisieren.  
  
11. Klicken Sie auf **OK**.

11. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  

![Berichts-Generator-KPI-Ampel](../reporting-services/media/report-builder-kpi-stoplight.png)
  
## <a name="Title"></a>6. Hinzufügen eines Berichtstitels  
Ein Berichtstitel wird oben im Bericht angezeigt. Sie können den Berichtstitel in eine Berichtskopfzeile einfügen oder, wenn der Bericht keine Kopfzeile enthält, in einem Textfeld am oberen Rand des Berichtshauptteils. In diesem Abschnitt verwenden Sie das Textfeld, das automatisch am oberen Rand des Berichtshauptteils platziert wird.  
  
Sie können die Textdarstellung weiter verbessern, indem Sie verschiedene Schriftschnitte, Größen und Farben für Ausdrücke und einzelne Zeichen des Texts anwenden. Weitere Informationen finden Sie unter [Formatieren von Text in einem Textfeld &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-report-title"></a>So fügen Sie einen Berichtstitel hinzu  
  
1.  Klicken Sie auf der Entwurfsoberfläche auf **Zum Hinzufügen eines Titels klicken**.  
  
2.  Geben Sie **Produktvertriebs-KPI**ein, und klicken Sie in den Bereich außerhalb des Textfelds.  
  
3.  Klicken Sie optional mit der rechten Maustaste auf das Textfeld mit dem Eintrag **Product Sales KPI**, klicken Sie auf **Textfeldeigenschaften**, und wählen Sie auf der Registerkarte „Schriftart“ andere Schriftschnitte, Größen und Farben aus.  
  
4.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
## <a name="Save"></a>7. Speichern des Berichts  
Speichern Sie den Bericht auf einem Berichtsserver oder auf Ihrem Computer. Wenn Sie den Bericht nicht auf dem Berichtsserver speichern, ist eine Reihe von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Funktionen nicht verfügbar, z. B. Berichtsteile und Unterberichte.  
  
### <a name="to-save-the-report-on-a-report-server"></a>So speichern Sie den Bericht auf einem Berichtsserver  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Letzte Sites und Server**.  
  
3.  Wählen Sie den Namen des Berichtsservers aus, auf dem Sie zum Speichern von Berichten berechtigt sind, oder geben Sie ihn ein.  
  
    Die Meldung "Verbindung mit Berichtsserver wird hergestellt" wird angezeigt. Nachdem die Verbindung hergestellt wurde, sehen Sie den Inhalt des Berichtsordners, den der Berichtsserveradministrator als Standardspeicherort für Berichte angegeben hat.  
  
4.  Ersetzen Sie im Feld **Name**den Standardnamen durch **Produktumsatz-KPI**.  
  
5.  Klicken Sie auf **Speichern**.  
  
Der Bericht wird auf dem Berichtsserver gespeichert. Der Name des Berichtsservers, mit dem Sie verbunden sind, wird in der Statusleiste unten im Fenster angezeigt.  
  
### <a name="to-save-the-report-on-your-computer"></a>So speichern Sie den Bericht auf dem Computer  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Desktop**, **Eigene Dokumente**oder **Computer**, und navigieren Sie zu dem Ordner, in dem Sie den Bericht speichern möchten.  
  
> [!NOTE]  
> Wenn Sie keinen Zugriff auf einen Berichtsserver haben, klicken Sie auf **Desktop**&gt; **Eigene Dokumente**oder **Arbeitsplatz** , und speichern Sie den Bericht auf dem Computer.  
  
1.  Ersetzen Sie im Feld **Name**den Standardnamen durch **Produktumsatz-KPI**.  
  
2.  Klicken Sie auf **Speichern**.  
  
## <a name="next-steps"></a>Nächste Schritte  
Sie haben das Lernprogramm "Hinzufügen eines KPI zu einem Bericht" erfolgreich abgeschlossen. Weitere Informationen finden Sie in den folgenden Themen:
*  [Messgeräte](../reporting-services/report-design/gauges-report-builder-and-ssrs.md)
* [Indikatoren](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Siehe auch  
* [Lernprogramme für den Berichts-Generator](../reporting-services/report-builder-tutorials.md)
* [Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  


