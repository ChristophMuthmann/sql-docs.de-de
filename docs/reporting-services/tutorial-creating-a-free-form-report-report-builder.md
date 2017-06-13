---
title: 'Lernprogramm: Erstellen eines Freiformberichts (Berichts-Generator) | Microsoft Docs'
ms.custom: 
ms.date: 09/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 356d795aec5249ecf4f990d549c8eacb70e25f03
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>Lernprogramm: Erstellen eines Freiformberichts (Berichts-Generator)
In diesem Tutorial erfahren Sie, wie Sie einen paginierten Bericht erstellen, der wie ein Newslettern funktioniert. Jede Seite zeigt statischen Text, zusammenfassende Visualisierungen und detaillierte Beispielumsatzdaten an.

![Berichts-Generator-Freiformbericht-vollständig](../reporting-services/media/report-builder-free-form-report-complete.png)

Im Bericht werden Informationen nach Gebiet gruppiert und der Name des Vertriebsmanagers für das Gebiet sowie ausführliche und zusammenfassende Umsatzdaten angezeigt. Der Listendatenbereich wird als Grundlage für den formfreien Bericht verwendet. Anschließend werden folgende Objekte hinzugefügt: ein dekoratives Panel mit einem Bild, statischer Text mit eingefügten Daten, eine Tabelle zum Anzeigen ausführlicher Informationen und optional Kreis- und Säulendiagramme zum Anzeigen zusammenfassender Informationen.  
  
Ungefähre Dauer dieses Lernprogramms: 20 Minuten.  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Anforderungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="BlankReport"></a>1. Erstellen eines leeren Berichts, einer leeren Datenquelle und eines leeren Datasets  
  
> [!NOTE]  
> In diesem Tutorial sind die Datenwerte in der Abfrage enthalten, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
### <a name="to-create-a-blank-report"></a>So erstellen Sie einen leeren Bericht  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
  
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist. 
 
3.  Klicken Sie im rechten Bereich auf **Leerer Bericht**.  
  
### <a name="to-create-a-new-data-source"></a>So erstellen Sie eine neue Datenquelle  
  
1.  Klicken Sie im Bereich „Berichtsdaten“ auf **Neu**  >  **Datenquelle**.  
  
2.  Geben Sie im Feld **Name** Folgendes ein: **ListDataSource**  
  
3.  Klicken Sie auf **In Bericht eingebettete Verbindung verwenden**.  
  
4.  Überprüfen Sie, ob der Verbindungstyp „Microsoft SQL Server“ ist, und geben Sie anschließend im Feld **Verbindungszeichenfolge** Folgendes ein:  **Data Source = \<Servername**.  
  
    Der **\<Servername>**, z.B. Report001, bezeichnet einen Computer, auf dem eine Instanz des SQL Server-Datenbankmoduls installiert ist. Da die Daten für diesen Bericht nicht aus einer SQL Server-Datenbank extrahiert werden, muss der Name einer Datenbank nicht eingeschlossen werden. Die Standarddatenbank auf dem angegebenen Server wird nur verwendet, um die Abfrage zu analysieren.  
  
5.  Klicken Sie auf **Anmeldeinformationen**und geben Sie die zur Verbindung mit der Instanz des SQL Server-Datenbankmoduls benötigten Anmeldeinformationen ein.  
  
6.  Klicken Sie auf **OK**.  
  
### <a name="to-create-a-new-dataset"></a>So erstellen Sie ein neues Dataset  
  
1.  Klicken Sie im Bereich „Berichtsdaten“ auf **Neu**  >  **Dataset**.  
  
2.  Geben Sie im Feld **Name** **ListDataset** ein.  
  
3.  Klicken Sie auf **Ein in den eigenen Bericht eingebettetes Dataset verwenden**und überprüfen Sie, ob **ListDataSource**die Datenquelle ist.  
  
4.  Überprüfen Sie, ob der Abfragetyp **Text** ausgewählt ist, und klicken Sie anschließend auf **Abfrage-Designer**.  
  
5.  Klicken Sie auf **Als Text bearbeiten**.  
  
6.  Kopieren Sie die folgende Abfrage, und fügen Sie sie in den Abfragebereich ein:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
7.  Klicken Sie auf das Symbol für **Ausführen** (!), um die Abfrage auszuführen.  
  
    Bei den Abfrageergebnissen handelt es sich um die Daten, die im Bericht angezeigt werden können.  
  
    ![Berichts-Generator-Freiform-Tutorial-Daten](../reporting-services/media/report-builder-free-form-tutorial-data.png) 
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="List"></a>2. Hinzufügen und Konfigurieren einer Liste  
In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] eignet sich die Datenregion „Liste“ für die Erstellung formfreier Berichte. Er basiert auf dem *Tablix* -Datenbereich, ebenso wie Tabellen und Matrizen. Weitere Informationen finden Sie unter [Erstellen von Rechnungen und Formulare mit Listen (Berichts-Generator und SSRS)](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
In diesem Abschnitt verwenden Sie eine Liste, um die Umsatzdaten für Vertriebsgebiete in einem Bericht anzuzeigen, der wie ein Newsletter formatiert wurde. Die Informationen werden nach Gebiet gruppiert. Sie fügen eine neue Zeilengruppe hinzu, in der Daten nach Gebiet gruppiert werden, und löschen dann die integrierte Zeilengruppe "Details".  
  
### <a name="to-add-a-list"></a>So fügen Sie eine Liste hinzu  
  
1.  Gehen Sie auf der Registerkarte **Einfügen** zu **Datenbereiche**  >  **Liste**. 

2. Klicken Sie auf den Berichtstext (zwischen dem Titel- und dem Fußzeilenbereich), und ziehen Sie ihn in das Listenfeld. Passen Sie die Größe des Listenfeldes auf eine Höhe von 17,8 cm und eine Breite von 15,9 cm an. Geben Sie im Bereich **Eigenschaften** unter **Position**die Werte für **Width** und **Height** ein, um die exakte Größe zu erzielen.
  
    > [!NOTE]  
    > Für diesen Bericht werden als Papierformat Letter (21,6 x 28) und Ränder mit einer Breite von ca. 2,5 cm verwendet. Ein Listenfeld, das höher als 22,9 cm oder breiter als 16,5 cm ist, kann zu leeren Seiten führen.  
  
2.  Klicken Sie in das Listenfeld, klicken Sie mit der rechten Maustaste auf den oberen Rand der Liste und anschließend auf **Tablix-Eigenschaften**.  
  
    ![Berichts-Generator-Freiform-Tablix-Eigenschaften](../reporting-services/media/report-builder-free-form-tablix-properties.png) 
  
3.  Wählen Sie in der Dropdownliste **Datasetname** die Option **ListDataset**aus.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Klicken Sie mit der rechten Maustaste in die Liste und anschließend auf **Rechteckeigenschaften**.  
  
6.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Seitenumbruch hinzufügen nach** .  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>So fügen Sie eine neue Zeilengruppe hinzu und löschen die Detailgruppe  
  
1.  Klicken Sie im Bereich „Zeilengruppen“ mit der rechten Maustaste auf die Gruppe „Details“, zeigen Sie auf **Gruppe hinzufügen**, und klicken Sie anschließend auf **Übergeordnete Gruppe**.  
  
    ![Berichts-Generator-Freiform-Übergeordnete Gruppe-hinzufügen](../reporting-services/media/report-builder-free-form-add-parent-group.png)  
  
2.  Wählen Sie in der Liste **Gruppieren nach**`[Territory].`  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Eine Spalte, die die Zelle `[Territory]` enthält, wird der Liste hinzugefügt.
  
4.  Klicken Sie mit der rechten Maustaste in der Liste auf die Spalte „Territory“, und klicken Sie anschließend auf **Spalten löschen**.  
  
    ![Berichts-Generator-Freiform-Spalten-löschen](../reporting-services/media/report-builder-free-form-delete-columns.png)
  
5.  Klicken Sie auf **Nur Spalten löschen**.  
  
6.  Klicken Sie im Bereich „Zeilengruppen“ mit der rechten Maustaste auf die Gruppe **Details**, und klicken Sie anschließend auf **Gruppe löschen**.  
   
7.  Wählen Sie **Nur Gruppe löschen**aus.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Graphics"></a>3. Hinzufügen grafischer Elemente  
Ein Vorteil von Listendatenbereichen besteht darin, dass Berichtselemente wie z.B. Rechtecke und Textfelder überall statt nur in einem tabellarischen Layout hinzugefügt werden können. Sie verbessern die Darstellung des Berichts durch Hinzufügen einer Grafik (ein mit einer Farbe ausgefülltes Rechteck).  
  
### <a name="to-add-graphic-elements-to-the-report"></a>So fügen Sie dem Bericht grafische Elemente hinzu  
  
1.  Wählen Sie auf der Registerkarte **Einfügen** die Option **Rechteck**aus. 

2. Klicken Sie in die obere linke Ecke der Liste, und ziehen Sie das Rechteck, um die Höhe auf 17,8 cm und die Breite auf 8,9 cm festzulegen. Auch hier können Sie die Werte **Width** und **Height** im Bereich **Eigenschaften** unter **Position** eingeben, um die exakte Größe zu erzielen.
  
2.  Klicken Sie mit der rechten Maustaste auf das Rechteck, und klicken Sie anschließend auf **Rechteckeigenschaften**.  
  
3.  Klicken Sie auf die Registerkarte **Ausfüllen** .  
  
4.  Wählen Sie unter **Füllfarbe**die Option **Hellgrau**aus.  
   
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Die linke Seite des Berichts enthält nun eine vertikale Grafik, die aus einem dunkelgrauen Rechteck besteht, wie in der folgenden Abbildung dargestellt.  
  
![Berichts-Generator-Freiform-Grau-Rechteck](../reporting-services/media/report-builder-free-form-gray-rectangle.png)
 
## <a name="Text"></a>4. Hinzufügen von Freitext  
Sie können Textfelder hinzufügen, um statischen Text anzuzeigen, der auf jeder Berichtsseite sowie in allen Datenfeldern wiederholt wird.  
  
### <a name="to-add-text-to-the-report"></a>So fügen Sie dem Bericht Text hinzu  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie auf der Registerkarte **Einfügen** auf **Textfeld**. Klicken Sie in die obere linke Ecke der Liste innerhalb des Rechtecks, das Sie zuvor hinzugefügt haben, und ziehen Sie das Textfeld, um die Breite auf etwa 8,8 cm und die Höhe auf etwa 12,7 cm festzulegen.  
  
3.  Setzen Sie den Cursor in das Textfeld, und geben Sie anschließend Folgendes ein: **Newsletter für** . Setzen Sie ein Leerzeichen nach dem Wort „für“, um den Text von dem Feld zu trennen, das Sie im nächsten Schritt hinzufügen werden.   
  
    ![Fügen Sie Text für newsletterüberschriften](../reporting-services/media/tutorial-newsletterfor.png "fügen Sie Text für newsletterüberschriften")  
  
4.  Ziehen Sie das `[Territory]` -Feld aus ListDataSet in den Bereich „Berichtsdaten“ in das Textfeld, und platzieren Sie es hinter „Newsletter for “.  
  
    ![Berichts-Generator-Freiform-Territory-Feld](../reporting-services/media/report-builder-free-form-territory-field.png)
  
5.  Wählen Sie den Text und das `[Territory]`-Feld aus.  
  
6.  Klicken Sie auf die Registerkarte **Stamm**, und wählen Sie unter **Schriftart** Folgendes aus: 
  
    *  **Segoe Semibold**
    *  **20 pt**
    *  **Tomate**  
  
9. Platzieren Sie den Cursor unterhalb des Texts, den Sie in Schritt 3 eingegeben haben, und geben Sie **Hallo** mit einem anschließenden Leerzeichen ein, um den Text von dem Feld zu trennen, das Sie im nächsten Schritt hinzufügen.  
 
10. Ziehen Sie das `[FullName]` -Feld aus ListDataSet im Bereich „Berichtsdaten“ in das Textfeld, platzieren Sie es hinter „Hallo “, und geben Sie anschließend ein Komma (,) ein.  
   
11. Wählen Sie den Text aus, den Sie in den vorherigen Schritten hinzugefügt haben.
  
12. Klicken Sie auf die Registerkarte **Stamm**, und wählen Sie unter **Schriftart** Folgendes aus: 
  
    *  **Segoe Semibold**
    *  **16 pt**
    *  **Schwarz**  
   
15. Setzen Sie den Cursor unter den Text, den Sie in den Schritten 9 bis 13 hinzugefügt haben, und kopieren Sie anschließend den folgenden, sinnlosen Text, und fügen Sie ihn ein:  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. 
    Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. 
    Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
 
    ```  
  
16. Wählen Sie den gerade eingegebenen Text aus.  
  
17.  Klicken Sie auf die Registerkarte **Stamm**, und wählen Sie unter **Schriftart** Folgendes aus: 
  
      *  **Segoe UI**
      *  **10 pt**
      *  **Schwarz**  
 
20. Platzieren Sie den Cursor im Textfeld unter dem bedeutungslosen Text, und geben Sie **Glückwünsche zum Gesamtumsatz von**mit einem anschließenden Leerzeichen ein, um den Text von dem Feld zu trennen, das Sie im nächsten Schritt hinzufügen. 
  
21. Ziehen Sie das Feld „Sales“ in das Textfeld, platzieren Sie es hinter dem im vorherigen Schritt eingegebenen Text, und geben Sie anschließend ein Ausrufezeichen (!) ein.  

25. Wählen Sie den Text und das Feld aus, den bzw. das Sie gerade hinzugefügt haben.  
  
17.  Klicken Sie auf die Registerkarte **Stamm**, und wählen Sie unter **Schriftart** Folgendes aus: 
  
      *  **Segoe Semibold**
      *  **16 pt**
      *  **Schwarz**  
  
22. Wählen Sie nur das `[Sales]`-Feld aus, klicken Sie mit der rechten Maustaste darauf, und wählen Sie **Ausdruck** aus.  
  
23. Ändern Sie im Feld **Ausdruck** den Ausdruck so, dass er die Sum-Funktion einschließt:  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    ![Berichts-Generator-Freiform-Textfeld](../reporting-services/media/report-builder-free-form-text-box.png)
 
29. Wählen Sie auf der Registerkarte **Stamm**, während `[Sum(Sales)]` noch ausgewählt ist, die Gruppe **Zahl** > **Währung** aus.  
  
30. Klicken Sie mit der rechten Maustaste auf das Textfeld mit dem Text „Zum Hinzufügen eines Titels klicken“, und klicken Sie anschließend auf **Löschen**.  
  
31. Wählen Sie das Listenfeld aus. Wählen Sie die zwei Pfeile mit zwei Spitzen aus, und verschieben Sie das Listenfeld an den Anfang der Seite.  

    ![Berichts-Generator-Listenfeld-verschieben](../reporting-services/media/report-builder-drag-list.png)
  
32. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Im Bericht wird statischer Text angezeigt, und jede Berichtsseite enthält Daten, die sich auf ein Gebiet beziehen. Umsatz wird als Währung formatiert.  
  
![Berichts-Generator-Newsletterseite-Vorschau](../reporting-services/media/report-builder-newsletter-page-preview.png)
  
## <a name="Table"></a>5. Hinzufügen einer Tabelle, die Umsatzdetails anzeigt  
Fügen Sie dem formfreien Bericht mithilfe des Assistenten für neue Tabellen und Matrizen eine Tabelle hinzu. Nach Fertigstellung des Assistenten wird manuell eine Zeile für Summen hinzugefügt.  
  
### <a name="to-add-a-table"></a>So fügen Sie eine Tabelle hinzu  
  
1.  Klicken Sie auf der Registerkarte **Einfügen** im Bereich **Datenbereiche** auf **Tabelle**  >  **Tabellen-Assistent**.  
  
2.  Aktivieren Sie auf der Registerkarte **Dataset auswählen** auf **ListDataset** > **Weiter**.  
  
4.  Ziehen Sie auf der Seite **Felder anordnen** das Feld „Product“ von **Verfügbare Felder** zu **Werte**.  
  
5.  Wiederholen Sie Schritt 3 für „SalesDate“, „Quantity“ und „Sales“. Orden Sie "SalesDate" unter Produkt, "Quantity" unter "SalesDate" und "Sales" unter "SalesDate" an.  
  
6.  Klicken Sie auf **Weiter**.  
  
7.  Zeigen Sie auf der Seite **Layout auswählen** das Layout der Tabelle an.  
  
    Die Tabelle ist schlicht: Sie enthält fünf Spalten mit keinen Zeilen- oder Spaltengruppen. Da die Tabelle keine Gruppen enthält, sind die gruppenbezogenen Layoutoptionen nicht verfügbar. Im späteren Verlauf des Lernprogramms wird Tabelle manuell aktualisiert, damit sie eine Summe enthält.  
  
8.  Klicken Sie auf **Weiter**.  
  
9. Klicken Sie auf **Fertig stellen**.  
  
11. Ziehen Sie die Tabelle unter das Textfeld, das Sie in Lektion 4 hinzugefügt haben.  
  
    > [!NOTE]  
    > Stellen Sie sicher, dass sich die Tabelle innerhalb des Listenfeldes und innerhalb des grauen Rechtecks befindet.  
  
12. Klicken Sie bei ausgewählter Tabelle im Bereich **Zeilengruppe** mit der rechten Maustaste auf **Details**  >  **Gesamtergebnis hinzufügen**  >  **Nach**.  
  
    ![Berichts-Generator-Freiform-Tabelle-Gesamtergebnis](../reporting-services/media/report-builder-free-form-table-totals.png)
  
13. Wählen Sie die Zelle in der Product-Spalte aus, und geben Sie **Gesamtergebnis**ein.

    ![Berichts-Generator-Freiform-Eingeben-Gesamteergebnis](../reporting-services/media/report-builder-free-form-type-total.png)

12. Wählen Sie das Feld [SalesDate] aus. Ändern Sie auf der Registerkarte **Stamm** unter **Zahl** die Option **Standard** zu **Datum**.

13. Wählen Sie die Felder für [Sum(Sales)] aus. Ändern Sie auf der Registerkarte **Stamm** unter **Zahl** die Option **Standard** zu **Währung**.

Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Im Bericht wird eine Tabelle mit Umsatzdetails und Gesamtbeträgen angezeigt.  
  
![Berichts-Generator-Freiform-mit-Tabelle](../reporting-services/media/report-builder-free-form-with-table.png)
   
## <a name="Save"></a>6. Speichern des Berichts  
Sie können Berichte auf einem Berichtsserver, in einer SharePoint-Bibliothek oder auf dem Computer speichern.  
  
Speichern Sie in diesem Lernprogramm den Bericht auf einem Berichtsserver. Wenn Sie keinen Zugriff auf einen Berichtsserver besitzen, speichern Sie den Bericht auf dem Computer.  
  
### <a name="to-save-the-report-on-a-report-server"></a>So speichern Sie den Bericht auf einem Berichtsserver  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Letzte Sites und Server**.  
  
3.  Wählen Sie den Namen des Berichtsservers aus, auf dem Sie zum Speichern von Berichten berechtigt sind, oder geben Sie ihn ein.  
  
    Die Meldung "Verbindung mit Berichtsserver wird hergestellt" wird angezeigt. Nachdem die Verbindung hergestellt wurde, sehen Sie den Inhalt des Berichtsordners, den der Berichtsserveradministrator als Standardspeicherort für Berichte angegeben hat.  
  
4.  Ersetzen Sie in **Name**den Standardnamen durch **SalesInformationByTerritory**.  
  
5.  Klicken Sie auf **Speichern**.  
  
Der Bericht wird auf dem Berichtsserver gespeichert. Der Name des Berichtsservers, mit dem Sie verbunden sind, wird in der Statusleiste unten im Fenster angezeigt.  
  
### <a name="to-save-the-report-on-your-computer"></a>So speichern Sie den Bericht auf dem Computer  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Desktop**, **Meine Dokumente**oder **Arbeitsplatz**, und navigieren Sie anschließend zu dem Ordner, in dem Sie den Bericht speichern möchten.  
  
3.  Ersetzen Sie in **Name**den Standardnamen durch **SalesInformationByTerritory**.  
  
4.  Klicken Sie auf **Speichern**.  
  
## <a name="Line"></a>7. Hinzufügen einer Zeile, um Bereiche des Berichts zu trennen (optional)  
Fügen Sie eine Zeile hinzu, um den Leitartikel und die Details des Berichts zu trennen.  
  
### <a name="to-add-a-line"></a>So fügen Sie eine Linie hinzu  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Auf der **einfügen** Registerkarte "> **Berichtselemente** > **Zeile.**  
  
3.  Zeichnen Sie eine Linie unter dem Textfeld, das Sie in Lektion 4 hinzugefügt haben.  
  
4.  Klicken Sie auf die Linie, und wählen Sie anschließend auf der Registerkarte **Stamm** im Bereich **Rahmen** Folgendes aus:
     * Wählen Sie als **Stärke** **3** pt aus.
     * Wählen Sie für**Farbe**  **Tomate**aus.  
  
## <a name="Visualization"></a>8. Hinzufügen von Zusammenfassungsdatenvisualisierungen (optional)  
Mit Rechtecken kann das Rendern des Berichts beeinflusst werden. Platzieren Sie in einem Rechteck ein Kreis- und ein Säulendiagramm, um sicherzustellen, dass der Bericht wunschgemäß gerendert wird.  
  
### <a name="to-add-a-rectangle"></a>So fügen Sie ein Rechteck hinzu  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Auf der **einfügen** Registerkarte "> **Berichtselemente** >  **Rechteck**. Ziehen Sie das Rechteck in das Listenfeld rechts neben der Tabelle, um die Breite auf etwa 5,7 cm und die Höhe auf etwa 20 cm anzupassen.  
  
3.  Wählen Sie das neue Rechteck aus und geben Sie für **BorderColor**„LightGrey“, für **BorderStyle**„Solid“ und für **BorderWidth**„2pt“ ein. 

4. Richten Sie den oberen Bereich des Rechtecks und der Tabelle aus.  
  
## <a name="to-add-a-pie-chart"></a>So fügen Sie ein Kreisdiagramm hinzu  
  
1.  Klicken Sie auf der Registerkarte **Einfügen** auf **Datenvisualisierungen**  >  **Diagramm**  >  **Diagramm-Assistent**.  
  
2.  Aktivieren Sie auf der Registerkarte **Dataset auswählen** auf **ListDataset** > **Weiter**.  
  
3.  Klicken Sie auf **Kreis**  >  **Weiter**.  
  
4.  Ziehen Sie auf der Seite „Diagrammfelder anordnen“ das Feld „Product“ in **Kategorien**.  
  
5.  Ziehen Sie „Quantity“ in das Feld **Werte**, und klicken Sie anschließend auf **Weiter**.  
  
6.  Klicken Sie auf **Fertig stellen**.  
  
8.  Ändern Sie die Größe des Diagramms, das oben links im Bericht angezeigt wird, auf eine Höhe von etwa. 9,1 cm und eine Breite von etwa. 5,8 cm.  
  
9. Ziehen Sie das Diagramm in das Rechteck.  
   
10. Wählen Sie den Diagrammtitel und Typ **Verkaufte Produktmengen** aus.  
  
12. Legen Sie für den Titel auf der Registerkarte **Stamm** im Bereich **Schriftart** Folgendes fest:
    * **Schriftart** **Segoe UI Semibold**.
    * **Size** **12 pt**.
    * **Farbe** **Schwarz**.  

13. Klicken Sie mit der rechten Maustaste auf die Legende und anschließend auf **Legendeneigenschaften**.

14. Wählen Sie auf der Registerkarte **Allgemein** unter **Legendenposition** den mittleren Punkt am unteren Rand aus. 
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

16. Ziehen Sie bei Bedarf den Diagrammbereich, um ihn zu vergrößern.

     ![Berichts-Generator-Freiform-Kreisdiagramm](../reporting-services/media/report-builder-free-form-pie.png)
  
## <a name="to-add-a-column-chart"></a>So fügen Sie einem Bericht ein Säulendiagramm hinzu  
  
1.  Klicken Sie auf der Registerkarte **Einfügen** auf **Datenvisualisierungen**  >  **Diagramm**  >  **Diagramm-Assistent**.  
  
2.  Klicken Sie auf der Seite **Dataset auswählen** auf **ListDataset** und anschließend auf **Weiter**.  
  
3.  Klicken Sie auf **Spalte**und anschließend auf **Weiter**.  
  
4.  Ziehen Sie auf der Seite **Diagrammfelder anordnen** das Feld „Product“ in **Kategorien**.  
  
5.  Ziehen Sie „Sales“ in das Feld **Werte** , und klicken Sie anschließend auf **Weiter**.  
  
    Werte werden auf der vertikalen Achse angezeigt.  
  
6.  Klicken Sie auf **Fertig stellen**.  
  
    Ein Säulendiagramm wird oben links im Bericht hinzugefügt.  
  
8.  Ändern Sie die Diagrammgröße auf eine Höhe von etwa 10,1 cm und eine Breite von etwa 5,7 cm.  
  
9. Ziehen Sie das Diagramm in das Rechteck unter dem Kreisdiagramm.  
   
10. Wählen Sie den Diagrammtitel aus und geben Sie **Produktumsatz** ein.  
  
12. Legen Sie für den Titel auf der Registerkarte **Stamm** im Bereich **Schriftart** Folgendes fest:
    * **Schriftart** **Segoe UI Semibold**.
    * **Size** **12 pt**.
    * **Color** **Black**.  
  
15. Klicken Sie mit der rechten Maustaste auf die Legende, und klicken Sie dann auf **Legende löschen**.  
  
    > [!NOTE]  
    > Das Entfernen der Legende trägt zur Lesbarkeit des Diagramms bei, wenn es sich um ein kleines Diagramm handelt.  
  
    ![Berichts-Generator-Freiform-Spalte](../reporting-services/media/report-builder-free-form-column.png)

12. Wählen Sie die Diagrammachse, und klicken Sie auf die *Home** Registerkarte "> **Anzahl** > **Währung**.

13. Klicken Sie zweimal auf **Dezimalstellen verringern** , sodass die nur der Dollarwert ohne Cents angezeigt wird.      
### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>So überprüfen Sie, ob die Diagramme im Rechteck enthalten sind  

Sie können Rechtecke als Container für andere Elemente auf einer Berichtsseite verwenden. Erfahren Sie mehr über [Rechtecke als Container](../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md).
  
1.  Wählen Sie das Rechteck aus, das Sie zuvor in dieser Lektion erstellt und dem Sie Diagramme hinzugefügt haben.  
  
    Im Eigenschaftenbereich zeigt die **Name** -Eigenschaft den Namen des Rechtecks an.  
  
    ![Berichts-Generator-Freiform-Rechteck-Name](../reporting-services/media/report-builder-free-form-rectangle-name.png) 
  
2.  Klicken Sie auf das Kreisdiagramm.  
  
3.  Überprüfen Sie im Bereich **Eigenschaften** , ob die **Parent** -Eigenschaft den Namen des Rechtecks enthält.  
  
     ![Berichts-Generator-Freiform-Kreisdiagramm-Parent](../reporting-services/media/report-builder-free-form-pie-parent.png) 
  
4.  Klicken Sie auf das Säulendiagramm, und wiederholen Sie Schritt 3.  
  
    > [!NOTE]  
    > Wenn die Diagramme nicht im Rechteck enthalten sind, werden die Diagramme im gerenderten Bericht nicht zusammen angezeigt.  
  
### <a name="to-make-the-charts-the-same-size"></a>So legen Sie für die Diagramme die gleiche Größe fest  
  
1.  Wählen Sie das Kreisdiagramm aus, drücken Sie die STRG-TASTE, und wählen Sie anschließend das Säulendiagramm aus.  
  
2.  Klicken Sie,wenn beide Diagramme ausgewählt sind, mit der rechten Maustaste auf **Layout**  >  **Breite angleichen**.  
  
    > [!NOTE]  
    > Das Element, auf das Sie zuerst klicken, bestimmt die Breite aller ausgewählten Elemente.  
  
3.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Im Bericht werden nun Zusammenfassungsumsatzdaten in Kreis- und Säulendiagrammen angezeigt.  
  

  
## <a name="next-steps"></a>Nächste Schritte  
Hiermit ist das Tutorial für die Erstellung von formfreien Berichten abgeschlossen.  
  
Weitere Informationen zu Listen finden Sie unter: 
* [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md) 
* [Erstellen von Rechnungen und Formulare mit Listen (Berichts-Generator und SSRS)](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)
* [Zellen, Zeilen und Spalten des Tablix-Datenbereichs &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
Weitere Informationen zu Abfrage-Designern finden Sie unter [Abfrage-Designer &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9) und [Benutzeroberfläche des textbasierten Abfrage-Designers &#40;Berichts-Generator&#41;](../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
## <a name="see-also"></a>Siehe auch  
[Lernprogramme für den Berichts-Generator](../reporting-services/report-builder-tutorials.md) 
  


