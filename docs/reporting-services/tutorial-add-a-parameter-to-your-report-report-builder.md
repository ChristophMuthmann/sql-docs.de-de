---
title: "Lernprogramm: Hinzufügen eines Parameters zum Bericht (Berichts-Generator) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: eab34ec4-b3ad-4a76-95cc-07b2f75ee6d7
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a3e5da225eb8008f74d6fc5aade3e55543d93d91
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="tutorial-add-a-parameter-to-your-report-report-builder"></a>Lernprogramm: Hinzufügen eines Parameters zum Bericht (Berichts-Generator)
In diesem Tutorial fügen Sie einen Parameter zu einem paginierten [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Bericht hinzu, sodass Leser des Berichts Berichtsdaten für einen Wert oder mehrere Werte filtern können. 
  
![Berichts-Generator-Parameter-Tutorial](../reporting-services/media/report-builder-parameter-tutorial.png)

Berichtsparameter werden automatisch für jeden Abfrageparameter erstellt, den Sie in eine Datasetabfrage einschließen. Der Parameterdatentyp bestimmt, wie der Parameter auf der Symbolleiste der Berichtsansicht angezeigt wird. 
   
> [!NOTE]  
> In diesem Lernprogramm werden die Schritte für den Assistenten in einem Verfahren zusammengefasst. Im ersten Tutorial dieser Reihe erhalten Sie detaillierte Anweisungen zum Navigieren zu einem Berichtsserver, zum Auswählen einer Datenquelle sowie zum Erstellen eines Datasets: [Tutorial: Erstellen eines einfachen Tabellenberichts &#40;Berichts-Generator&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Ungefähre Dauer dieses Lernprogramms: 25 Minuten.  
  
## <a name="requirements"></a>Anforderungen  
Weitere Informationen zu den Anforderungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Setup"></a>1. Erstellen eines Matrixberichts und eines Datasets mit dem Tabellen- oder Matrix-Assistenten  
Erstellen Sie einen Matrixbericht, eine Datenquelle und ein Dataset.  
  
> [!NOTE]  
> In diesem Lernprogramm sind die Datenwerte in der Abfrage enthalten, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
### <a name="to-create-a-new-matrix-report"></a>So erstellen Sie einen neuen Matrixbericht  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] -Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
  
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist.  
  
3.  Klicken Sie im rechten Bereich auf **Tabellen- oder Matrix-Assistent**.  
  
4.  Klicken Sie auf der Seite **Dataset auswählen** auf **Dataset erstellen** > **Weiter**.  
  
7.  Wählen Sie auf der Seite **Verbindung mit einer Datenquelle auswählen** eine Datenquelle aus der Liste aus, oder navigieren Sie zum Berichtsserver, um eine auszuwählen. Wählen Sie eine beliebige Datenquelle des Typs **SQL Server**aus.  
      
8.  Klicken Sie auf **Weiter**.  

    Sie müssen möglicherweise Ihre Anmeldeinformationen eingeben.    
     
9. Klicken Sie auf der Seite **Abfrage entwerfen** auf **Als Text bearbeiten**.  
  
10. Fügen Sie die folgende Abfrage in den leeren Bereich am oberen Ende ein:  
  
    ```  
    ;WITH CTE (StoreID, Subcategory, Quantity)   
    AS (  
    SELECT 200 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 2002 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Camcorders' AS Subcategory, 1954 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Accessories' AS Subcategory, 1895 AS Quantity  
    UNION SELECT  199 AS StoreID, 'Digital Cameras' AS Subcategory, 1849 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1579 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Camcorders' AS Subcategory, 1561 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital Cameras' AS Subcategory, 1553 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Accessories' AS Subcategory, 1534 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Accessories' AS Subcategory, 1755 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Camcorders' AS Subcategory, 1631 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1772 AS Quantity)  
    SELECT StoreID, Subcategory, Quantity  
    FROM CTE  
    ```  
  
    Durch diese Abfrage werden die Ergebnisse mehrerer [!INCLUDE[tsql_md](../includes/tsql-md.md)] -SELECT-Anweisungen in einem allgemeinen Tabellenausdruck kombiniert, um Werte anzugeben, die auf vereinfachten Umsatzdaten für Kameras aus der Contoso-Beispieldatenbank basieren. Die Unterkategorien sind Digitalkameras, digitale Spiegelreflexkameras (DSLR), Camcorder und Zubehör.  
  
11. Klicken Sie auf der Symbolleiste des Abfrage-Designers auf **Ausführen** (**!**), um die Daten anzuzeigen.   
  
    Das Resultset enthält 11 Datenzeilen, in denen die Menge verkaufter Artikel in jeder Unterkategorie für vier Geschäfte angezeigt in folgenden Spalten angezeigt wird: „StoreID“, „Subcategory“ und „Quantity“. Der Geschäftsname ist nicht Teil des Resultsets. An späterer Stelle dieses Lernprogramms suchen Sie in einem separaten Dataset nach dem Namen des Geschäfts, das der Geschäfts-ID entspricht.  
  
    Diese Abfrage enthält keine Abfrageparameter. Abfrageparameter werden später in diesem Lernprogramm hinzugefügt.   
  
12. Klicken Sie auf **Weiter**.  
  
## <a name="CompleteWizard"></a>2. Organisieren von Daten und Auswählen des Layouts im Assistenten  
Der Assistent stellt einen Startentwurf für die Anzeige von Daten bereit. Im Vorschaufenster des Assistenten können Sie das Ergebnis der Datengruppierung visualisieren, bevor Sie den Tabellen- oder Matrixentwurf abschließen.  
  
### <a name="to-organize-data-into-groups"></a>So gruppieren Sie Daten  
  
1.  Ziehen Sie „Subcategory“ auf der Seite **Felder anordnen** in **Zeilengruppen**.  
  
2.  Ziehen Sie „StoreID“ in **Spaltengruppen**.  
  
3.  Ziehen Sie „Quantity“ in **Werte**.  
  
    Sie haben die Werte für die verkaufte Menge in Zeilen organisiert und nach Unterkategorie gruppiert.  
  
4.  Klicken Sie auf **Weiter**.  
  
5.  Vergewissern Sie sich auf der Seite **Layout auswählen** , dass unter **Optionen**die Option **Teil- und Gesamtergebnisse anzeigen** ausgewählt ist.  
  
    Wenn Sie den Bericht ausführen, werden in der letzten Spalte die Gesamtmenge jeder Unterkategorie für alle Geschäfte und in der letzten Zeile die Gesamtmenge für alle Unterkategorien für jedes Geschäft angezeigt.  
  
6.  Klicken Sie auf **Weiter**.  
  
8.  Klicken Sie auf **Fertig stellen**.  
  
    Die Matrix wird der Entwurfsoberfläche hinzugefügt. Die Matrix enthält drei Spalten und drei Zeilen. Die Zellen in der ersten Zeile enthalten "Subcategory", "[StoreID]" und "Total". Die Zellen in der zweiten Zeile enthalten Ausdrücke, die die Unterkategorie, die Menge verkaufter Artikel für jedes Geschäft und die Gesamtmenge in jeder Unterkategorie für alle Geschäfte darstellen. Die Zellen in der letzten Zeile enthalten das Gesamtergebnis für jedes Geschäft.  
      
    ![ssRB_ParamTut_Design](../reporting-services/media/ssrb-paramtut-design.png)  
  
9. Klicken Sie in die Matrix, zeigen Sie auf den Rand der ersten Spalte, und vergrößern Sie die Spaltenbreite mithilfe des Ziehpunkts.  
  
   ![ssRB_ParamTut_Drag](../reporting-services/media/ssrb-paramtut-drag.png)  
  
10. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  
  
Der Bericht wird auf dem Berichtsserver ausgeführt. Titel und Zeitpunkt der Verarbeitung des Berichts werden angezeigt.  

![ssRB_ParamTut__Preview1](../reporting-services/media/ssrb-paramtut-preview1.png)
  
Bisher wird in den Spaltenüberschriften die Geschäfts-ID, aber nicht der Geschäftsnamen angezeigt. Später fügen Sie einen Ausdruck hinzu, um in einem Dataset, das Geschäfts-ID/Geschäftsname-Paare enthält, nach dem Geschäftsnamen suchen.  
  
## <a name="Query"></a>3. Hinzufügen eines Abfrageparameters zum Erstellen eines Berichtsparameters  
Wenn Sie einer Abfrage einen Abfrageparameter hinzufügen, erstellt der Berichts-Generator automatisch einen eindeutigen Berichtsparameter mit Standardeigenschaften für Name, Eingabe und Datentyp.  
  
### <a name="to-add-a-query-parameter"></a>So fügen Sie einen Abfrageparameter hinzu  
  
1.  Klicken Sie auf **Entwurf** , um wieder zur Entwurfsansicht zurückzuwechseln.  
  
2.  Erweitern Sie im Berichtsdatenbereich den Ordner **Datasets** , klicken Sie mit der rechten Maustaste auf **DataSet1**, und klicken Sie anschließend auf **Abfrage**.  
  
3.  Fügen Sie die folgende [!INCLUDE[tsql](../includes/tsql-md.md)] **WHERE** -Klausel als letzte Zeile in der Abfrage hinzu:  
  
    ```  
    WHERE StoreID = (@StoreID)  
    ```  
  
    Das Dialogfeld **WHERE** -Klausel beschränkt die abgerufenen Daten auf die Geschäfts-ID, die vom Abfrageparameter *@StoreID*.  
  
4.  Klicken Sie auf der Symbolleiste des Abfrage-Designers auf **Ausführen** (**!**). Das Dialogfeld **Abfrageparameter definieren** wird geöffnet, und Sie werden aufgefordert, einen Wert für den Abfrageparameter *@StoreID*.  
  
5.  Geben Sie im Feld **Parameterwert**die Zahl **200**ein.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Im Resultset werden die verkauften Mengen für Zubehör, Camcorder und digitale SLR-Kameras für die Geschäfts-ID **200**angezeigt.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Erweitern Sie im Berichtsdatenbereich den Ordner **Parameter** .  
  
Beachten Sie, dass nun ein Berichtsparameter namens *@StoreID*existiert sowie ein Bereich „Parameter“, in dem Sie die Berichtsparameter erstellen können.   
  
![ssRB_ParamPane](../reporting-services/media/ssrb-parampane.png)  
  
Wird kein Bereich „Parameter“ angezeigt? Wählen Sie im Menü **Ansicht** den Befehl **Parameter**aus.  
  
## <a name="ChangeDefaultProperties"></a>4. Ändern des Standarddatentyps und anderer Eigenschaften für einen Berichtsparameter  
Nachdem Sie einen Berichtsparameter erstellt haben, können Sie die Standardwerte für Eigenschaften anpassen.  
  
### <a name="to-change-the-default-data-type-for-a-report-parameter"></a>So ändern Sie den Standarddatentyp für einen Berichtsparameter  
  
Standardmäßig weist der Parameter, den Sie erstellt haben, den Datentyp **Text**auf. Da es sich bei der Geschäfts-ID um eine ganze Zahl handelt, können Sie den Datentyp in „Integer“ ändern.  
  
1.  Klicken Sie im Berichtsdatenbereich unter dem Knoten **Parameter** mit der rechten Maustaste auf *@StoreID*, und klicken Sie anschließend auf **Parametereigenschaften**.  
  
2.  Geben Sie im Feld **Eingabeaufforderung** **Geschäfts-ID?**ein. Dieser Text wird auf der Berichts-Viewer-Symbolleiste angezeigt, wenn Sie den Bericht ausführen.  
  
3.  Wählen Sie in der Dropdownliste **Datentyp**die Option **Ganze Zahl**aus.  
  
4.  Nehmen Sie die verbleibenden Standardwerte im Dialogfeld an.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen. Der Berichts-Viewer zeigt die Eingabeaufforderung **Store Identifier?** für *@StoreID*.  
  
7.  Geben Sie auf der Berichts-Viewer-Symbolleiste neben Geschäfts-ID die Zahl **200**ein, und klicken anschließend auf **Bericht anzeigen**.  
  
![SSRB_ParamTutStoreID](../reporting-services/media/ssrb-paramtutstoreid.png)  
  
## <a name="AddDataset"></a>4a. Hinzufügen eines Datasets, um verfügbare Werte und Anzeigenamen anzuzeigen  
Um sicherzustellen dass die Leser des Berichts nur gültige Werte für einen Parameter eingeben kann, können Sie eine Dropdownliste von Werten erstellen. Die Werte können aus einem Dataset oder einer von Ihnen angegebenen Liste stammen. Verfügbare Werte müssen aus einem Dataset stammen, dessen Abfrage keinen Verweis auf den Parameter enthält.  
  
### <a name="to-create-a-dataset-for-valid-values-for-a-parameter"></a>So erstellen Sie ein Dataset für gültige Werte für einen Parameter  
  
1.  Klicken Sie auf **Entwurf** , um zur Entwurfsansicht zu wechseln.  
  
2.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf den Ordner **Datasets** , und klicken Sie anschließend auf **Dataset hinzufügen**.  
  
3.  Geben Sie im Feld **Name**den Namen **Geschäfte**ein.  
  
4.  Wählen Sie **Ein in den eigenen Bericht eingebettetes Dataset verwenden**aus.  
  
5.  Wählen Sie unter **Datenquelle**in der Dropdownliste die Datenquelle aus, die Sie im ersten Verfahren verwendet haben.  
  
6.  Vergewissern Sie sich, dass unter **Abfragetyp**die Option **Text** ausgewählt ist.  
  
7.  Fügen Sie unter **Abfrage**folgende Abfrage ein:  
  
    ```  
    SELECT 200 AS StoreID, 'Contoso Catalog Store' as StoreName  
    UNION SELECT 199 AS StoreID, 'Contoso North America Online Store' as StoreName  
    UNION SELECT 307 AS StoreID, 'Contoso Asia Online Store' as StoreName  
    UNION SELECT 306 AS StoreID, 'Contoso Europe Online Store' as StoreName  
    ```  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Im Berichtsdatenbereich werden die Felder „StoreID“ und „StoreName“ unter dem Datasetknoten **Geschäfte** angezeigt.  
  
## <a name="AvailableValues"></a>4b. Angeben der verfügbaren Werte, die in einer Liste angezeigt werden sollen 
Nachdem Sie ein Dataset erstellt haben, um verfügbare Werte bereitzustellen, ändern Sie die Berichtseigenschaften, um das Dataset und das Feld anzugeben, aus denen die Dropdownliste gültiger Werte auf der Berichts-Viewer-Symbolleiste aufgefüllt wird.  
  
### <a name="to-provide-available-values-for-a-parameter-from-a-dataset"></a>So stellen Sie verfügbare Werte für einen Parameter aus einem Dataset bereit  
  
1.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf den Parameter *@StoreID*, und klicken Sie anschließend auf **Parametereigenschaften**.  
  
2.  Klicken Sie auf **Verfügbare Werte**und anschließend auf **Werte aus Abfrage abrufen**.  
  
3.  Klicken Sie unter **Dataset**in der Dropdownliste auf den Eintrag **Stores**.  
  
4.  Wählen Sie unter **Wertfeld**den Eintrag „StoreID“ aus der Dropdownliste aus.  
  
5.  Wählen Sie unter **Bezeichnungsfeld**den Eintrag „StoreName“ aus der Dropdownliste aus. Das Bezeichnungsfeld gibt den Anzeigenamen für den Wert an.  
  
6.  Klicken Sie auf **Allgemein**.  
  
7.  Ändern Sie in der **Eingabeaufforderung** **Geschäfts-ID?** zu **Szure name?**.  
  
    Berichtsleser wählen jetzt anstelle einer Liste von Geschäfts-IDs eine Liste von Geschäftsnamen aus. Beachten Sie, dass der Parameterdatentyp weiterhin **Integer** lautet, da der Parameter nicht auf dem Geschäftsnamen, sondern auf der Geschäfts-ID basiert.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Zeigen Sie eine Vorschau des Berichts an.  
  
    Auf der Berichts-Viewer-Symbolleiste ist das Parametertextfeld jetzt eine Dropdownliste, die **Einen Wert auswählen**anzeigt.  
  
10. Wählen Sie in der Dropdownliste „Contoso Catalog Store“ aus, und klicken Sie anschließend auf **Bericht anzeigen**.  
  
Im Bericht werden die verkauften Mengen für Zubehör, Camcorder und digitale SLR-Kameras für die Geschäfts-ID **200**angezeigt.  
  
## <a name="DefaultValues"></a>4c. Angeben eines Standardwerts 
Sie können einen Standardwert für jeden Berichtsparameter angeben, damit der Bericht automatisch ausgeführt wird.  
  
### <a name="to-specify-a-default-value-from-a-dataset"></a>So geben Sie einen Standardwert aus einem Dataset an  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf *@StoreID*, und klicken Sie anschließend auf **Parametereigenschaften**.  
  
3.  Klicken Sie auf **Standardwerte**und anschließend auf **Werte aus Abfrage abrufen**.  
  
4.  Klicken Sie unter **Dataset**in der Dropdownliste auf den Eintrag **Stores**.  
  
5.  Wählen Sie unter **Wertfeld**den Eintrag „StoreID“ aus der Dropdownliste aus.  
  
6.  [!INCLUDE[clickOK_md](../includes/clickok-md.md)]  
  
7.  Zeigen Sie eine Vorschau des Berichts an.  
  
For *@StoreID*zeigt der Berichts-Viewer den Wert „Contoso North America Online Store“ an, da es sich um den ersten Wert aus dem Resultset für das Dataset **Geschäfte**. Im Bericht wird die verkaufte Menge von Digitalkameras für die Geschäfts-ID **199**angezeigt.  
  
### <a name="to-specify-a-custom-default-value"></a>So geben Sie einen benutzerdefinierten Standardwert an  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf *@StoreID*, und klicken Sie anschließend auf **Parametereigenschaften**.  
  
3.  Klicken Sie auf **Standardwerte** > **Werte angeben** > **Hinzufügen**. Eine neue Wertzeile wird hinzugefügt.  
  
4.  Geben Sie im Feld **Wert**die Zeichenfolge **200**ein.  
  
5.  [!INCLUDE[clickOK_md](../includes/clickok-md.md)] 
  
6.  Zeigen Sie eine Vorschau des Berichts an.  
  
For *@StoreID*zeigt der Report Viewer „Contoso Catalog Store“ an, da dies der Anzeigename für die Geschäfts-ID **200**. Im Bericht werden die verkauften Mengen für Zubehör, Camcorder und digitale SLR-Kameras für die Geschäfts-ID **200**angezeigt.  
  
## <a name="NameValue"></a>4d. Suchen eines Name-Wert-Paares  
Ein Dataset kann sowohl den Bezeichner als auch das entsprechende Namensfeld enthalten. Wenn Sie nur einen Bezeichner haben, können Sie in einem von Ihnen erstellten Dataset, das Name-Wert-Paare enthält, nach dem entsprechenden Namen suchen.  
  
### <a name="to-look-up-a-value-from-a-dataset"></a>So suchen Sie nach einem Wert in einem Dataset  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Klicken Sie auf der Entwurfsoberfläche in der Matrix im ersten Zeilenspaltenheader mit der rechten Maustaste auf `[StoreID]` , und klicken Sie anschließend auf **Ausdruck**.  
  
3.  Löschen Sie im Ausdrucksbereich den gesamten Text mit Ausnahme des Anfangs **Gleichheitszeichen** (=).  
  
4.  Erweitern Sie unter **Kategorie**den Knoten **Allgemeine Funktionen**, und klicken Sie auf **Sonstiges**. Im Bereich "Element" wird ein Satz von Funktionen angezeigt.  
  
5.  Doppelklicken Sie in „Element“ auf **Suche**. Im Ausdrucksbereich wird `=Lookup(`angezeigt. Der Bereich "Beispiel" enthält ein Beispiel für die Suchsyntax.  
  
6.  Geben Sie den folgenden Ausdruck ein: 

    ```  
    =Lookup(Fields!StoreID.Value,Fields!StoreID.Value,Fields!StoreName.Value,"Stores")      
    ```  
  
    Die Suchfunktion empfängt den Wert für "StoreID", sucht im Dataset "Geschäfte" danach und gibt den "StoreName"-Wert zurück.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Der Spaltenheader für das Geschäft enthält den Anzeigetext für einen komplexen Ausdruck: **Expr**.  
  
8.  Zeigen Sie eine Vorschau des Berichts an.  
  
Die Spaltenkopfzeile oben auf jeder Seite zeigt anstelle den Geschäftsnamen anstatt der Geschäfts-ID an.  
  
## <a name="Expression"></a>5. Anzeigen des ausgewählten Parameterwerts im Bericht  
Wenn die Leser des Berichts Fragen zu einem Bericht hat, ist es hilfreich, die ausgewählten Parameterwerte zu kennen. Die vom Benutzer ausgewählten Werte können für jeden Parameter im Bericht beibehalten werden. Sie können die Parameter z. B. in einem Textfeld im Seitenfuß anzeigen.  
  
### <a name="to-display-the-selected-parameter-value-and-label-on-a-page-footer"></a>So zeigen Sie den ausgewählten Parameterwert und die Bezeichnung in einem Seitenfuß an  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Fußzeile > **Einfügen** > **Textfeld**. Ziehen Sie das Textfeld neben das Textfeld mit dem Zeitstempel. Vergrößern Sie die Breite des Textfelds mit dem seitlichen Ziehpunkt.  
  
3.  Ziehen Sie im Berichtsdatenbereich den Parameter *@StoreID* in das Textfeld. Im Textfeld wird `[@StoreID]`angezeigt.  
  
4.  Um die Parameterbezeichnung anzuzeigen, klicken Sie auf das Textfeld, bis der Einfügecursor nach dem vorhandenen Ausdruck angezeigt wird, geben Sie ein Leerzeichen ein, und ziehen Sie dann eine andere Kopie des Parameters im Berichtsdatenbereich in das Textfeld. Im Textfeld wird `[@StoreID] [@StoreID]`angezeigt.  
  
5.  Klicken Sie mit der rechten Maustaste auf die erste `[@StoreID]` , und klicken Sie auf **Ausdruck**. Das Dialogfeld **Ausdruck** wird geöffnet. Ersetzen Sie den Text `Value` durch `Label`.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Der folgende Text wird angezeigt: `[@StoreID.Label] [@StoreID]`.  
  
7.  Zeigen Sie eine Vorschau des Berichts an.  
  
## <a name="Filter"></a>6. Verwenden des Berichtsparameters in einem Filter  
Mithilfe von Filtern können die in einem Bericht zu verwendenden Daten gesteuert werden, nachdem sie aus einer externen Datenquelle abgerufen wurden. Schließen Sie den Berichtsparameter in einen Filter für die Matrix ein, um Lesern des Berichts das Steuern der angezeigten Daten zu ermöglichen.  
  
### <a name="to-specify-a-parameter-in-a-matrix-filter"></a>So geben Sie einen Parameter in einem Matrixfilter an  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Klicken Sie mit der rechten Maustaste auf einen Zeilen- oder Spaltenheaderziehpunkt in der Matrix und anschließend auf **Tablix-Eigenschaften**.  
  
3.  Klicken Sie auf **Filter**und anschließend auf **Hinzufügen**. Es wird ein neuer Zeilenfilter angezeigt.  
  
4.  Wählen Sie im Feld **Ausdruck**aus der Dropdownliste das Datasetfeld StoreID aus. Der Datentyp zeigt **Ganze Zahl**an. Wenn der Ausdruckswert ein Datasetfeld ist, wird der Datentyp automatisch festgelegt.  
  
5.  Vergewissern Sie sich, dass unter **Operator**die Option **Gleichheitszeichen** (=) ausgewählt ist.  
  
6.  Geben Sie im Feld **Wert**die Zeichenfolge `[@StoreID]`ein. 

    `[@StoreID]` ist die einfache Ausdruckssyntax, die `=Parameters!StoreID.Value`darstellt.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Zeigen Sie eine Vorschau des Berichts an.  
  
    In der Matrix werden nur Daten für "Contoso Catalog Store" angezeigt.  
  
9. Wählen Sie auf der Berichts-Viewer-Symbolleiste für **Geschäftsname?**die Option **Contoso Asia Online Store**aus, und klicken Sie anschließend auf **Bericht anzeigen**.  
  
In der Matrix werden Daten für das ausgewählte Geschäft angezeigt.  
  
## <a name="Multivalued"></a>7. Ändern des Berichtsparameters in einen mehrwertigen Parameter  
Wenn Sie einen einwertigen Parameter in einen mehrwertigen Parameter ändern möchten, müssen Sie die Abfrage und alle Ausdrücke, die einen Verweis auf den Parameter enthalten (einschließlich Filter) ändern. Ein mehrwertiger Parameter ist ein Wertarray. In einer Datasetabfrage muss die Abfragesyntax überprüfen, ob ein Wert in einem Satz von Werten enthalten ist. In einem Berichtsausdruck greift die Ausdruckssyntax nicht auf einzelnen Wert, sondern auf ein Wertarray zu.  
  
### <a name="to-change-a-parameter-from-single-to-multivalued"></a>So ändern Sie einen einwertigen Parameter in einen mehrwertigen Parameter  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf *@StoreID*, und klicken Sie anschließend auf **Parametereigenschaften**.  
  
3.  Aktivieren Sie **Mehrere Werte zulassen**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Erweitern Sie im Berichtsdatenbereich den Ordner **Datasets** , klicken Sie mit der rechten Maustaste auf **DataSet1**, und klicken Sie anschließend auf **Abfrage**.  
  
6.  Ändern Sie die **Gleichheitszeichen** (=) in der **** WHERE [!INCLUDE[tsql](../includes/tsql-md.md)] **WHERE** clause WHERE last line WHERE query:  
  
    ```  
    WHERE StoreID IN (@StoreID)  
    ```  
  
    Der **IN** -Operator testet, ob ein Wert in einem Satz von Werten enthalten ist.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Klicken Sie mit der rechten Maustaste auf einen Zeilen- oder Spaltenheaderziehpunkt in der Matrix und anschließend auf **Tablix-Eigenschaften**.  
  
9. Klicken Sie auf **Filter**.  
  
10. Wählen Sie unter **Operator**die Option **IN**aus.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Löschen Sie im Textfeld, in dem der Parameter im Seitenfuß angezeigt wird, den gesamten Text.  
  
13. Klicken Sie mit der rechten Maustaste auf das Textfeld, und klicken Sie anschließend auf **Ausdruck**. Geben Sie den folgenden Ausdruck ein: `=Join(Parameters!StoreID.Label, ", ")`  
  
    Dieser Ausdruck verkettet alle Geschäftsnamen, die der Benutzer ausgewählt hat, und die durch ein Komma und ein Leerzeichen getrennt sind.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. Klicken Sie vor dem soeben erstellten Ausdruck in das Textfeld, und geben Sie dann Folgendes ein: 

    **Ausgewählte Parameterwerte:** 
  
16. Zeigen Sie eine Vorschau des Berichts an.  
  
17. Klicken Sie auf die Dropdownliste neben "Geschäftsname?"  
  
    Alle gültigen Werte werden neben einem Kontrollkästchen angezeigt.  
  
18. Klicken Sie auf **Alles auswählen**und anschließend auf **Bericht anzeigen**.  
  
    Im Bericht wird die verkaufte Menge in allen Unterkategorien für alle Geschäfte angezeigt.  
  
19. Klicken Sie in der Dropdownliste auf **Alles auswählen** , um die Liste zu löschen, klicken Sie auf „Contoso Catalog Store“ und „Contoso Asia Online Store“ und anschließend auf **Bericht anzeigen**.  

    ![Berichts-Generator-Parameter-multiselect](../reporting-services/media/report-builder-parameter-multiselect.png)
  
 
## <a name="Boolean"></a>8. Hinzufügen eines booleschen Parameters für bedingte Sichtbarkeit  
  
### <a name="to-add-a-boolean-parameter"></a>So fügen Sie einen booleschen Parameter hinzu  
  
1.  Klicken Sie auf der Entwurfsoberfläche im Berichtsdatenbereich mit der rechten Maustaste auf **Parameter**, und klicken Sie anschließend auf **Parameter hinzufügen**.  
  
2.  Geben Sie im Feld **Name**„ShowSelections“ ein.  
  
3.  Geben Sie im Feld **Eingabeaufforderung**„Auswahl anzeigen?“ ein.  
  
4.  Klicken Sie in **Datentyp**auf **Boolean**.  
  
5.  Klicken Sie auf **Standardwerte**.  
  
6.  Klicken Sie auf **Wert angeben**und anschließend auf **Hinzufügen**.  
  
7.  Geben Sie im Feld **Wert**den Wert **FALSE**ein.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-set-visibility-based-on-a-boolean-parameter"></a>So legen Sie die Sichtbarkeit basierend auf einem booleschen Parameter fest  
  
1.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf das Textfeld im Seitenfuß, in dem die Parameterwerte angezeigt werden, und klicken Sie anschließend auf **Textfeldeigenschaften**.  
  
2.  Klicken Sie auf **Sichtbarkeit**.  
  
3.  Aktivieren Sie die Option **Je nach Ausdruck einblenden/ausblenden**, und klicken Sie anschließend auf die Ausdrucksschaltfläche **Fx**.  
  
4.  Geben Sie den folgenden Ausdruck ein: `=Not Parameters!ShowSelections.Value`  
  
    Die Textfeldoption "Sichtbarkeit" wird durch die Hidden-Eigenschaft gesteuert. Wenden Sie den **Not** -Operator an, sodass die Hidden-Eigenschaft bei Auswahl des Parameters den Wert „FALSE“ hat und das Textfeld angezeigt wird.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Zeigen Sie eine Vorschau des Berichts an.  
  
    Das Textfeld mit der Parameterauswahl in der Fußzeile wird nicht angezeigt.  
  
8.  Klicken Sie auf der Berichts-Viewer-Symbolleiste neben **Auswahl anzeigen**auf **TRUE** > **Bericht anzeigen**.  
  
    Im Textfeld, das im Seitenfuß erscheint, werden alle Geschäftsnamen angezeigt, die Sie ausgewählt haben.  
  
## <a name="Title"></a>9. Hinzufügen eines Berichtstitels  
  
### <a name="to-add-a-report-title"></a>So fügen Sie einen Berichtstitel hinzu  

1.  Wechseln Sie in die Entwurfsansicht.  
   
1.  Klicken Sie auf der Entwurfsoberfläche auf **Zum Hinzufügen eines Titels klicken**.  
  
2.  Geben Sie "Parametrisierte Produktumsätze" ein, und klicken Sie dann außerhalb des Textfelds.  
  
## <a name="Save"></a>10. Speichern des Berichts  
  
### <a name="to-save-the-report-on-a-report-server"></a>So speichern Sie den Bericht auf einem Berichtsserver  
  
1.  Klicken Sie auf die Schaltfläche **Berichts-Generator** und anschließend auf **Speichern unter**.  
  
2.  Klicken Sie auf **Letzte Sites und Server**.  
  
3.  Wählen Sie den Namen des Berichtsservers aus, auf dem Sie zum Speichern von Berichten berechtigt sind, oder geben Sie ihn ein.  
  
    Die Meldung **Verbindung mit Berichtsserver wird hergestellt**wird angezeigt. Nachdem die Verbindung hergestellt wurde, sehen Sie den Inhalt des Berichtsordners, den der Berichtsserveradministrator als Standardspeicherort für Berichte angegeben hat.  
  
4.  Ersetzen Sie im Feld **Name**den Standardnamen durch „Parametrisierter Umsatzbericht“.  
  
5.  Klicken Sie auf **Speichern**.  
  
Der Bericht wird auf dem Berichtsserver gespeichert. Der Berichtsserver, mit dem Sie verbunden sind, wird in der Statusleiste unten im Fenster angezeigt.  
  
## <a name="next-steps"></a>Nächste Schritte  
Damit ist die exemplarische Vorgehensweise zum Hinzufügen eines Parameters zum Bericht abgeschlossen. Weitere Informationen zu Parametern finden Sie unter [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Siehe auch  
* [Lernprogramme für den Berichts-Generator](../reporting-services/report-builder-tutorials.md)
* [Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
*  [Lookup-Funktion](../reporting-services/report-design/report-builder-functions-lookup-function.md)   

