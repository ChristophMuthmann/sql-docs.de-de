---
title: 'Lernprogramm: Formatieren von Text (Berichts-Generator) | Microsoft Docs'
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
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
caps.latest.revision: 16
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: cfbe1001a049466af839363db29156df6b972556
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---

# <a name="tutorial-format-text-report-builder"></a>Lernprogramm: Formatieren von Text (Berichts-Generator)

In diesem Tutorial formatieren Sie in einem paginierten [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Bericht Text auf verschiedene Weise. Sie können mit unterschiedlichen Formaten experimentieren. 

Nach dem Einrichten des leeren Berichts mit der Datenquelle und dem Dataset können Sie die Formate auswählen, mit denen Sie sich vertraut machen möchten. Die folgende Abbildung zeigt einen Bericht, der mit dem Bericht vergleichbar ist, den Sie erstellen werden.  
  
![Bericht-Erstellen-Format-Bericht](../reporting-services/media/report-build-format-report.png) 
  
In einem Schritt machen Sie absichtlich einen Fehler, um dadurch erkennen zu können, warum es sich um einen Fehler handelt. Anschließend beheben Sie den Fehler, um den gewünschten Effekt zu erreichen.  
    
Ungefähre Dauer dieses Lernprogramms: 20 Minuten.  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Anforderungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="CreateReport"></a>Erstellen eines leeren Berichts mit einer Datenquelle und einem Dataset  
  
### <a name="to-create-a-blank-report"></a>So erstellen Sie einen leeren Bericht  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
 
2.  Vergewissern Sie sich links im Dialogfeld **Erste Schritte** , dass die Option **Neuer Bericht** ausgewählt ist.  
  
3.  Klicken Sie im rechten Bereich auf **Leerer Bericht**.  
  
### <a name="to-create-a-data-source"></a>So erstellen Sie eine Datenquelle  
  
1.  Klicken Sie im Bereich „Berichtsdaten“ auf **Neu**  >  **Datenquelle**.  

    Wenn der Bereich **Berichtsdaten** nicht auf der Registerkarte **Ansicht** angezeigt, überprüfen Sie **Berichtsdaten**.
  
2.  Geben Sie im Feld **Name** Folgendes ein: **TextDataSource**  
  
3.  Klicken Sie auf **In Bericht eingebettete Verbindung verwenden**.  
  
4.  Überprüfen Sie, ob der Verbindungstyp Microsoft SQL Server ist, und geben Sie anschließend im Feld **Verbindungszeichenfolge** Folgendes ein: `Data Source = <servername>`  
  
    > [!NOTE]  
    > Der Ausdruck `<servername>`, z.B. „Report001“, bezeichnet einen Computer, auf dem eine Instanz des SQL Server-Datenbankmoduls installiert ist. Dieses Lernprogramm ist es bestimmte Daten nicht erforderlich; Es benötigt lediglich eine Verbindung mit einer SQL Server-Datenbank. Wenn unter **Datenquellenverbindungen**bereits eine Datenquellenverbindung aufgeführt ist, können Sie sie auswählen und zum nächsten Schritt übergehen, nämlich „So erstellen Sie ein Dataset“. Weitere Informationen finden Sie unter [Alternative Methoden zum Herstellen einer Datenverbindung &#40;Berichts-Generator&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-dataset"></a>So erstellen Sie ein Dataset  
  
1.  Klicken Sie im Bereich „Berichtsdaten“ auf **Neu**  >  **Dataset**.  
  
2.  Vergewissern Sie sich, dass die Datenquelle **TextDataSource** ist.  
  
3.  Geben Sie im Feld **Name** Folgendes ein: **TextDataset**.  
  
4.  Überprüfen Sie, ob der Abfragetyp **Text** ausgewählt ist, und klicken Sie anschließend auf **Abfrage-Designer**.  
  
5.  Klicken Sie auf **Als Text bearbeiten**.  
  
6.  Fügen Sie die folgende Abfrage in den Abfragebereich ein:  

    > [!NOTE]  
    > In diesem Lernprogramm enthält die Abfrage bereits die Datenwerte, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  Klicken Sie auf „Ausführen“ (**!**), um die Abfrage auszuführen.  
  
    Bei den Abfrageergebnissen handelt es sich um die Daten, die im Bericht angezeigt werden können.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

9.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="AddField"></a>Hinzufügen eines Felds zur Berichtsentwurfsoberfläche  
Wenn Sie möchten, dass ein Feld aus dem Dataset in einem Bericht erscheint, werden Sie möglicherweise zunächst versuchen, das Feld direkt auf die Entwurfsoberfläche zu ziehen. Diese Übung zeigt auf, warum dies nicht funktioniert und wie stattdessen vorzugehen ist.  
  
### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>So fügen Sie dem Bericht ein Feld hinzu (und erhalten das falsche Ergebnis)  
  
1.  Ziehen Sie das Feld **FullName** aus dem Berichtsdatenbereich auf die Entwurfsoberfläche.  
  
    Der Berichts-Generator erstellt ein Textfeld mit einem darin enthaltenen Ausdruck, der als `<Expr>`dargestellt wird.  
  
2.  Klicken Sie auf **Ausführen**.  
  
    Es wird nur ein Datensatz angezeigt ( **Fernando Ross**), der nach alphabetischer Sortierung der erste Datensatz in der Abfrage ist. Die anderen Datensätze in diesem Feld werden nicht erneut angezeigt.  
  
3.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
4.  Wählen Sie den Ausdruck `<Expr>` im Textfeld aus.  
  
5.  Im Eigenschaftenbereich für die **Value** -Eigenschaft wird Folgendes angezeigt (wenn der Bereich nicht angezeigt wird, wählen Sie auf der Registerkarte **Ansicht** die Option **Eigenschaften**aus):  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
    Die `First` -Funktion dient dazu, dass nur der erste Wert in einem Feld abgerufen wird, und genau dies war auch der Fall.  
  
    Durch das direkte Ziehen des Felds auf die Entwurfsoberfläche wurde ein Textfeld erstellt. Textfelder an sich sind keine Datenbereiche, weshalb darin keine Daten aus einem Berichtsdataset angezeigt werden. In Textfeldern in Datenbereichen, z. B. Tabellen, Matrizen und Listen werden hingegen Daten angezeigt.  
  
6.  Wählen Sie das Textfeld aus (wenn der Ausdruck ausgewählt wurde, drücken Sie ESC, um das Textfeld auszuwählen), und drücken Sie die ENTF-TASTE.  
  
### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>So fügen Sie dem Bericht ein Feld hinzu (und erhalten das richtige Ergebnis)  
  
1.  Klicken Sie auf der Registerkarte **Einfügen** des Menübands im Bereich **Datenbereiche** auf **Liste**. Klicken Sie auf die Entwurfsoberfläche, und ziehen Sie anschließend den Mauszeiger, um ein Feld mit einer Breite von ungefähr fünf Zentimetern und einer Höhe von ca. 2,5 Zentimetern zu erstellen.  
  
2.  Ziehen Sie das Feld **FullName** aus dem Berichtsdatenbereich in das Listenfeld.  
  
    Dieses Mal erstellt der Berichts-Generator ein Textfeld mit dem Ausdruck `[FullName]` darin.  
  
3.  Klicken Sie auf **Ausführen**.  
  
    Dieses Mal werden im Feld alle Datensätze in der Abfrage erneut angezeigt.  
  
4.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
5.  Wählen Sie den Ausdruck im Textfeld aus.  
  
6.  Im Eigenschaftenbereich für die **Value** -Eigenschaft wird Folgendes angezeigt:  
  
    ```  
    =Fields!FullName.Value  
    ```  
  
    Durch Ziehen des Textfelds in den Listendatenbereich werden die Daten, die sich in diesem Feld befinden, im Dataset angezeigt.  
  
7.  Wählen Sie das Listenfeld aus, und drücken Sie die ENTF-TASTE.  
  
## <a name="AddTable"></a>Hinzufügen einer Tabelle zur Berichtsentwurfsoberfläche  
Erstellen Sie diese Tabelle, damit Sie Hyperlinks und den gedrehten Text an einer bestimmten Stelle ablegen können.   
  
1.  Klicken Sie auf der Registerkarte **Einfügen** auf **Tabelle** > **Tabellen-Assistent**.  
  
2.  Klicken Sie auf der Seite **Dataset auswählen** des Assistenten für neue Tabellen oder Matrizen auf **Vorhandenes Dataset in diesem Bericht oder einem freigegebenen Dataset auswählen** > **TextDataset (in diesem Bericht)** > **Weiter**.  
  
3.  Ziehen Sie auf der Seite **Felder anordnen** die Felder **Territory**, **LinkText**und **Product** nach **Zeilengruppen**, ziehen Sie das Feld **Sales** nach **Werte**, und klicken Sie anschließend auf **Weiter**.  

    ![Berichts-Generator-Text-Felder-anordnen](../reporting-services/media/report-builder-text-arrange-fields.png)
  
4.  Deaktivieren Sie auf der Seite **Layout auswählen** das Kontrollkästchen **Gruppen erweitern/reduzieren** , damit die vollständige Tabelle angezeigt wird, und klicken Sie anschließend auf **Weiter**. 
  
5.  Klicken Sie auf **Fertig stellen**.  
  
6.  Klicken Sie auf **Ausführen**.  
  
    Die Tabelle sieht einwandfrei aus, enthält jedoch zwei Ergebniszeilen. Die **LinkText** -Spalte benötigt keine Ergebniszeilen.  
    
    ![Berichts-Generator-Format-2-Gesamtwerte](../reporting-services/media/report-builder-format-2-totals.png)
  
8.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
9. Wählen Sie Zelle **Gesamt** in der Spalte **LinkText** aus, halten Sie die UMSCHALTTASTE gedrückt, und wählen Sie die zwei Zellen rechts daneben aus: die leere Zelle in der Spalte **Product** und die `[Sum(Sales)]` -Zelle in der Spalte **Sales** .  
  
11. Wenn diese drei Zellen ausgewählt sind, klicken Sie mit der rechten Maustaste auf eine der Zellen, und klicken Sie anschließend auf **Zeile löschen**.  

    ![Berichts-Generator-Format-löschen-Zeilen](../reporting-services/media/report-builder-format-delete-rows.png)
  
12. Klicken Sie auf **Ausführen**.  

    Jetzt ist es nur eine „Gesamt“-Zeile vorhanden.
    
    ![Berichts-Generator-Format-eine-Gesamt](../reporting-services/media/report-builder-format-one-total.png)
  
## <a name="AddHyperlink"></a>Hinzufügen eines Links zum Bericht  
In diesem Abschnitt fügen Sie dem Text in der Tabelle aus dem vorherigen Abschnitt einen Link hinzu.  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Zelle, die `[LinkText]`enthält, und klicken Sie auf **Textfeldeigenschaften**.  
  
3.  Auf der **Aktion** auf **Gehe zu URL**.  
  
5.  Klicken Sie im Feld **URL auswählen** auf **[URL]**und anschließend auf **OK**.  
  
6.  Das Aussehen des Texts unterscheidet sich nicht. Es muss jedoch dem des Linktexts entsprechen.  
  
7.  Wählen Sie `[LinkText]` aus.  
  
8.  Wählen Sie unter **Stamm** > **Schriftart**die Einstellung **Unterstreichen** aus, und ändern Sie die **Farbe** zu **Blau**.  
  
9. Klicken Sie auf **Ausführen**.  
  
    Der Text sieht nun wie ein Link aus.  
    
    ![Berichts-Generator-Format-Hyperlink](../reporting-services/media/report-builder-format-hyperlink.png)
  
10. Klicken Sie auf einen Link. Wenn der Computer mit dem Internet verbunden ist, wird vom Browser ein Hilfethema zu Berichts-Generator geöffnet.  
  
## <a name="RotateText"></a>Drehen von Text im Bericht  
In diesem Abschnitt drehen Sie Text in der Tabelle aus den vorherigen Abschnitten.  
 
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zurückzukehren.  
  
2.  Klicken Sie in die Zelle, die enthält. `[Territory].`  
  
3.  Klicken Sie auf der Registerkarte **Stamm** im Abschnitt **Schriftart** auf die Schaltfläche **Fett** .  
  
4.  Wenn der Eigenschaftenbereich nicht geöffnet ist, aktivieren Sie auf der Registerkarte **Ansicht** das Kontrollkästchen **Eigenschaften** .  
  
5.  Im Bereich Eigenschaften suchen Sie die WritingMode-Eigenschaft und ändern Sie den Schreibmodus von **Standard** auf **Rotate270**.  
 
    > [!NOTE]  
    > Wenn die Eigenschaften im Eigenschaftenbereich in Kategorien angeordnet sind, befindet sich WritingMode in der Kategorie **Lokalisierung** . Stellen Sie sicher, dass Sie die Zelle und nicht den Text ausgewählt haben. WritingMode ist eine Eigenschaft des Textfeldes, nicht des Texts.  

    ![Berichts-Generator-Auswählen-der-Zelle-Territory](../reporting-services/media/report-builder-select-territory-cell.png)
   
6.  Klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Absatz** auf die Schaltflächen **Mitte** und **Zentriert**, um den Text sowohl vertikal als auch horizontal im Mittelpunkt der Zelle zu platzieren.  
  
8.  Klicken Sie auf (**!**).  
  
Nun verläuft der Text in der `[Territory]` -Zelle in den Zellen vertikal von unten nach oben.  

![Berichts-Generator-Format-270 Grad-drehen](../reporting-services/media/report-builder-format-rotate-270.png)

## <a name="FormatCurrency"></a>Formatieren von Währung  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zu wechseln.  
  
2.  Klicken Sie auf die oberste Tabellenzelle, die `[Sum(Sales)]` enthält, halten Sie die UMSCHALTTASTE gedrückt, und klicken Sie auf die unterste Tabellenzelle, die `[Sum(Sales)]` enthält.  
  
3.  Klicken Sie auf der Registerkarte **Stamm** unter **Zahl** auf die Schaltfläche **Währung**.  
  
4.  (Optional) Wenn Sie das Gebietsschema „Deutsch (Deutschland)“ verwenden, lautet der Standardbeispieltext [**12.345,00€**]. Falls kein Beispielwährungswert angezeigt wird, klicken Sie in der Gruppe **Zahlen** auf **Platzhalterformate**  >  **Beispielwerte**.  

    ![Berichts-Generator-Schaltfläche-Platzhalterwert](../reporting-services/media/report-builder-placeholder-value-button.png)
  
5.  (Optional) Klicken Sie auf der Registerkarte **Stamm** in der Gruppe **Zahl** zweimal auf die Schaltfläche **Dezimalstellen verringern** , um volle Dollarbeträge ohne Centangaben anzuzeigen.  
  
6.  Klicken Sie auf „Ausführen“ (**!**), um eine Vorschau des Berichts anzuzeigen.  
  
Im Bericht werden nun formatierte Daten angezeigt, und die Lesbarkeit wurde verbessert.  

![Bericht-Erstellen-Format-Bericht](../reporting-services/media/report-build-format-report.png)
    
## <a name="FormatHTML"></a>Anzeigen von Text mit HTML-Formatierung  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zu wechseln.  
  
2.  Klicken Sie auf der Registerkarte **Einfügen** auf **Textfeld**. Klicken Sie anschließend auf die Entwurfsoberfläche, und ziehen Sie den Mauszeiger, um unter der Tabelle ein Textfeld mit einer Breite von etwa zehn Zentimetern und einer Höhe von etwa 7,5 Zentimetern zu ziehen.  
  
3.  Kopieren Sie diesen Text, und fügen Sie ihn in das Textfeld ein:  
  
    ```  
    <h4>Limitations of cascading style sheet attributes</h4>  
          <p>Only a basic set of <b>cascading style sheet (CSS)</b> attributes are defined:</p>  
          <ul><li>  
              text-align, text-indent  
            </li><li>  
              font-family, font-size  
            </li><li>  
              color  
            </li><li>  
              padding, padding-bottom, padding-top, padding-right, padding-left  
            </li><li>  
              font-weight  
            </li></ul>  
    ```  
  
4.  Ziehen Sie am unteren Rand des Textfelds, damit der gesamte Text hineinpasst. Sie sehen, dass die Entwurfsoberfläche größer wird, je weiter Sie ziehen.

5. Wählen Sie den gesamten Text im Textfeld aus.  
  
5.  Klicken Sie mit der rechten Maustaste auf den gesamten ausgewählten Text und anschließend auf **Texteigenschaften**.  
  
    Dies ist eine Eigenschaft des Texts (nicht des Textfelds). Daher kann in einem Textfeld eine Mischung aus Nur-Text und Text, die HTML-Tags als Formatvorlagen verwenden.  
  
6.  Klicken Sie auf der Seite **Allgemein** unter **Markuptyp**auf **HTML - HTML-Tags als Formate interpretieren**.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Klicken Sie auf „Ausführen“ (**!**), um eine Vorschau des Berichts anzuzeigen.  
  
Der Text im Textfeld wird als Überschrift, Absatz und Aufzählung angezeigt.  
  
![Berichts-Generator-Format-HTML](../reporting-services/media/report-builder-format-html.png)

## <a name="Save"></a>Speichern des Berichts  
Sie können Berichte auf einem Berichtsserver, in einer SharePoint-Bibliothek oder auf dem Computer speichern.  
  
Speichern Sie in diesem Lernprogramm den Bericht auf einem Berichtsserver. Wenn Sie keinen Zugriff auf einen Berichtsserver besitzen, speichern Sie den Bericht auf dem Computer.  
  
### <a name="to-save-the-report-on-a-report-server"></a>So speichern Sie den Bericht auf einem Berichtsserver  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Letzte Sites und Server**.  
  
3.  Wählen Sie den Namen des Berichtsservers aus, auf dem Sie zum Speichern von Berichten berechtigt sind, oder geben Sie ihn ein.  
  
    Die Meldung "Verbindung mit Berichtsserver wird hergestellt" wird angezeigt. Nachdem die Verbindung hergestellt wurde, sehen Sie den Inhalt des Berichtsordners, den der Berichtsserveradministrator als Standardspeicherort für Berichte angegeben hat.  
  
4.  Ersetzen Sie in **Name**den Standardnamen durch einen Namen Ihrer Wahl.

5.  Klicken Sie auf **Speichern**.  
  
Der Bericht wird auf dem Berichtsserver gespeichert. Der Name des Berichtsservers, mit dem Sie verbunden sind, wird in der Statusleiste unten im Fenster angezeigt.  
  
### <a name="to-save-the-report-on-your-computer"></a>So speichern Sie den Bericht auf dem Computer  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Desktop**, **Meine Dokumente**oder **Arbeitsplatz**, und navigieren Sie anschließend zu dem Ordner, in dem Sie den Bericht speichern möchten.  
  
3.  Ersetzen Sie in **Name**den Standardnamen durch einen Namen Ihrer Wahl. 
  
4.  Klicken Sie auf **Speichern**.  

## <a name="next-steps"></a>Nächste Schritte

Es gibt in Berichts-Generator viele Möglichkeiten, um Text zu formatieren. [Lernprogramm: Erstellen eines Freiformberichts](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md) enthält weitere Beispiele.  

[Berichts-Generator-Lernprogramme ](../reporting-services/report-builder-tutorials.md)  
 [Formatieren von Berichtselementen](../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)  
[Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)

