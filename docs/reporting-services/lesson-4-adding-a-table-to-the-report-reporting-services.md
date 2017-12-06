---
title: "Lektion 4: Hinzufügen einer Tabelle zum Bericht (Reporting Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/23/2016
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
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
caps.latest.revision: "64"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.openlocfilehash: a049602171321afc5ed20aaea072c73a48a68aae
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>Lektion 4: Hinzufügen einer Tabelle zum Bericht (Reporting Services)
Nach dem Definieren des Datasets können Sie mit dem Entwerfen des Berichts beginnen. Zum Erstellen eines Berichtslayouts verschieben Sie mit Drag und Drop Datenbereiche, Textfelder, Bilder und andere Elemente auf die Entwurfsoberfläche, die in den Bericht eingebunden werden sollen.  
  
Elemente, die wiederholte Zeilen von Daten aus zugrunde liegenden Datasets enthalten, werden als *Datenbereiche*bezeichnet. Ein grundlegender Bericht enthält typischerweise nur einen Datenbereich. Sie können jedoch weitere Datenbereiche hinzufügen, z. B. wenn dem Tabellenbericht ein Diagramm hinzugefügt werden soll. Nachdem Sie einen Datenbereich hinzugefügt haben, können Sie diesem Felder hinzufügen.  
  
### <a name="to-add-a-table-data-region-and-fields-to-a-report-layout"></a>So fügen Sie einem Berichtslayout einen Tabellendatenbereich und Felder hinzu  
  
1.  Klicken Sie in **Toolbox**auf **Tabelle**, und klicken Sie anschließend auf die Entwurfsoberfläche und ziehen Sie die Maus. Vom Berichts-Designer wird ein Tabellendatenbereich mit drei Spalten in der Mitte der Entwurfsoberfläche gezeichnet. Die **Toolbox** kann auf der linken Seite des **Berichtsdatenbereichs** als Registerkarte angezeigt werden. Zum Öffnen der **Toolbox**bewegen Sie den Mauszeiger über die Registerkarte **Toolbox** . Falls die **Toolbox** noch nicht angezeigt wird, klicken Sie im Menü **Ansicht** auf **Toolbox**.
  
     ![ssrs_ssdt_Tabelle_hinzufügen](../reporting-services/media/ssrs-ssdt-addtable.png) 
  
  Sie können auch dem Bericht eine Tabelle aus der Entwurfsoberfläche hinzufügen.  Klicken Sie mit der rechten Maustaste auf die Entwurfsoberfläche, anschließend auf **Einfügen** und danach auf **Tabelle**.
2.  Erweitern Sie im **Berichtsdatenbereich** das **AdventureWorksDataset** -Dataset, um die Felder anzuzeigen.  
  
3.  Ziehen Sie das Feld *Date* aus dem **Berichtsdatenbereich** in die erste Spalte in der Tabelle.  
  
    Wenn Sie das Feld in der ersten Spalte ablegen, werden zwei Vorgänge ausgeführt. Zunächst wird in der Datenzelle der als *Feldausdruck*bezeichnete Feldname in Klammern: `[Date]`angezeigt. Dann wird automatisch der Kopfzeile ein Wert für den Spaltenkopf hinzugefügt, und zwar direkt über dem Feldausdruck. Standardmäßig ist die Spalte der Name des Felds. Sie können den Kopfzeilentext auswählen und einen neuen Namen eingeben.  
  
4.  Ziehen Sie das Feld *Order* aus dem **Berichtsdatenbereich** in die zweite Spalte in der Tabelle.  
  
5.  Ziehen Sie das Feld *Product* aus dem **Berichtsdatenbereich** in die dritte Spalte in der Tabelle.  
  
6.  Ziehen Sie das Feld Qty an den rechten Rand der dritten Spalte, bis Sie einen vertikalen Cursor erhalten und der Mauszeiger ein Pluszeichen [+] aufweist. Wenn Sie die Maustaste loslassen, wird eine vierte Spalte für `[Qty]`erstellt.  
![ssrs_tutorial_Spalte_hinzufügen](../reporting-services/media/ssrs-tutorial-addcolumn.png)  
  
7.  Fügen Sie das Feld LineTotal auf dieselbe Weise hinzu, wodurch eine fünfte Spalte erstellt wird. Der Spaltenheader lautet "Line Total". Der Berichts-Designer erstellt für die Spalte automatisch einen besser lesbaren Namen, indem er "LineTotal" in zwei Wörter unterteilt.  
  
  
Die folgende Abbildung zeigt einen Datenbereich einer Tabelle, der mit folgenden Feldern aufgefüllt wurde: Date, Order, Product, Qty und Line Total.  
![rs_GrundlegendeTabellendetailsEntwurf](../reporting-services/media/rs-basictabledetailsdesign.png)  
  
## <a name="preview-your-report"></a>Zeigen Sie den Bericht in der Vorschau an.  
Wenn Sie einen Bericht in der Vorschau anzeigen, können Sie den gerenderten Bericht überprüfen, ohne ihn zuvor auf einem Berichtsserver zu veröffentlichen. Es empfiehlt sich beispielsweise, den Bericht zur Entwurfszeit häufig in der Vorschau anzuzeigen. Wenn Sie den Bericht in der Vorschau anzuzeigen, wird auch eine Überprüfung des Entwurfs und der Datenverbindungen ausgeführt, damit Sie Fehler und Probleme korrigieren können, bevor Sie den Bericht auf einem Berichtsserver veröffentlichen.  
  
#### <a name="to-preview-a-report"></a>So zeigen Sie die Vorschau eines Berichts an  
  
-   Klicken Sie auf die Registerkarte **Vorschau** . Der Berichts-Designer führt den Bericht aus und zeigt ihn in der Vorschau an.
![ssrs_ssdt_preview](../reporting-services/media/ssrs-ssdt-preview.png)  
  
    In der folgenden Abbildung wird ein Teil des Berichts in der Ansicht Vorschau angezeigt.  
  
    ![Vorschau, Detailzeilen der Tabelle mit 5 Spalten](../reporting-services/media/rs-basictabledetailspreview.png "Preview, Detail rows of table with 5 columns")  
  
    Beachten Sie, dass die Währungsangabe (in der Spalte Line Total) sechs Stellen nach dem Dezimaltrennzeichen aufweist und dass das Datum einen Zeitstempel enthält. Diese Formatierung wird in der nächsten Lektion korrigiert.  
  
> [!NOTE]  
> Klicken Sie im Menü **Datei** auf **Alle Speichern** , um den Bericht zu speichern.  
  
## <a name="next-steps"></a>Nächste Schritte  
Sie haben Ihrem Bericht erfolgreich einen Tabellendatenbereich hinzugefügt, dem Datenbereich Felder hinzugefügt und den Bericht in der Vorschau angezeigt. Anschließend formatieren Sie Spaltenheader sowie Datums- und Währungswerte. Weitere Informationen finden Sie unter [Lektion 5: Formatieren eines Berichts (Reporting Services)](../reporting-services/lesson-5-formatting-a-report-reporting-services.md).  
  
## <a name="see-also"></a>Siehe auch  
[Tabellen &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[Datasetfeld-Auflistung &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
