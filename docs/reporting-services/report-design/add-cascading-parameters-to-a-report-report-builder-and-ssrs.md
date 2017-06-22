---
title: "Hinzufügen von kaskadierenden Parametern zu einem Bericht (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a22eec3-57a7-478e-b6fc-102a9dbe0591
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d8efc7a0b7120faa53a63bd07c51029a1b379f9e
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="add-cascading-parameters-to-a-report-report-builder-and-ssrs"></a>Hinzufügen von kaskadierenden Parametern zu einem Bericht (Berichts-Generator und SSRS)
  Kaskadierende Parameter ermöglichen das Verwalten großer Berichtsdatenmengen. Sie können einen Satz von abhängigen Parametern definieren, sodass die Liste der Werte für einen Parameter von dem Wert abhängt, der in einem anderen Parameter ausgewählt wurde. Der erste Parameter ist beispielsweise unabhängig und stellt eine Liste von Produktkategorien dar. Wenn der Benutzer eine Kategorie auswählt, hängt der zweite Parameter vom Wert des ersten Parameters ab. Seine Werte werden mit einer Liste von Unterkategorien innerhalb der ausgewählten Kategorie aktualisiert. Wenn der Benutzer den Bericht anzeigt, werden die Berichtsdaten mit den Parameterwerten für die Kategorie und die Unterkategorien gefiltert.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Zum Erstellen von kaskadierenden Parametern definieren Sie zunächst die Datasetabfrage und binden einen Abfrageparameter für jeden benötigten kaskadierenden Parameter ein. Außerdem müssen Sie ein separates Dataset für jeden kaskadierenden Parameter erstellen, um verfügbare Werte bereitzustellen. Weitere Informationen finden Sie unter [Hinzufügen, Ändern oder Löschen von verfügbaren Werten für einen Berichtsparameter &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md).  
  
 Die Reihenfolge ist für kaskadierende Parameter relevant, da die Datasetabfrage für einen Parameter weiter unten in der Liste einen Verweis auf jeden Parameter weiter oben in der Liste enthält. Zur Laufzeit bestimmt die Reihenfolge der Parameter im Berichtsdatenbereich die Reihenfolge, in der Parameterabfragen im Bericht aufgeführt werden, und damit die Reihenfolge, in der Benutzer die einzelnen aufeinander folgenden Parameterwerte auswählen.  
  
 Informationen zum Erstellen von kaskadierenden Parametern mit mehreren Werten und einschließlich der Funktion "Alle auswählen" finden Sie unter [Informationen zu einem mehrwertigen, kaskadierenden Parameter vom Typ &lt;legacyBold&gt;Alle auswählen&lt;/legacyBold&gt;](http://go.microsoft.com/fwlink/?LinkId=184757).  
  
## <a name="to-create-the-main-dataset-with-a-query-that-includes-multiple-related-parameters"></a>So erstellen Sie das Hauptdataset mit einer Abfrage, die mehrere abhängige Parameter enthält  
  
1.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf eine Datenquelle, und klicken Sie anschließend auf **Dataset hinzufügen**.  
  
2.  Geben Sie unter **Name**den Namen des Datasets ein.  
  
3.  Wählen Sie in **Datenquelle**den Namen der Datenquelle aus, oder klicken Sie auf **Neu** , um eine Datenquelle zu erstellen.  
  
4.  Wählen Sie in **Abfragetyp**den Abfragetyp für die ausgewählte Datenquelle aus. In diesem Thema wird angenommen, dass der Abfragetyp **Text** ausgewählt wurde.  
  
5.  Geben Sie in **Abfrage**die Abfrage ein, mit der die Daten für diesen Bericht abgerufen werden sollen. Die Abfrage muss die folgenden Teile enthalten:  
  
    1.  Eine Liste mit Datenquellenfeldern. In einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung gibt beispielsweise die SELECT-Anweisung eine Liste mit den Namen aller Datenbankspalten aus einer bestimmten Tabelle oder Sicht an.  
  
    2.  Einen Abfrageparameter für jeden kaskadierenden Parameter. Ein Abfrageparameter beschränkt die von der Datenquelle abgerufenen Daten, indem bestimmte Werte angegeben werden, die in die Abfrage eingebunden bzw. von dieser ausgeschlossen werden sollen. Typischerweise sind Abfrageparameter in einer Einschränkungsklausel in der Abfrage enthalten. In einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -SELECT-Anweisung sind Abfrageparameter beispielsweise in der WHERE-Klausel enthalten. Weitere Informationen finden Sie unter "Filtern von Zeilen mithilfe von WHERE und HAVING" in der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dokumentation in der [SQL Server-Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=120955).  
  
6.  Klicken Sie auf **Ausführen** (**!**). Nachdem Sie die Abfrageparameter eingebunden und anschließend die Abfrage ausgeführt haben, werden automatisch Berichtsparameter erstellt, die den Abfrageparametern entsprechen.  
  
    > [!NOTE]  
    >  Die Reihenfolge von Abfrageparametern beim erstmaligen Ausführen einer Abfrage bestimmt die Reihenfolge, in der sie im Bericht erstellt werden. Informationen zum Ändern der Reihenfolge finden Sie unter [Ändern der Reihenfolge von Berichtsparametern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md).  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Anschließend erstellen Sie ein Dataset, das die Werte für den unabhängigen Parameter bereitstellt.  
  
## <a name="to-create-a-dataset-to-provide-values-for-an-independent-parameter"></a>So erstellen Sie ein Dataset zum Bereitstellen von Werten für einen unabhängigen Parameter  
  
1.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf eine Datenquelle, und klicken Sie anschließend auf **Dataset hinzufügen**.  
  
2.  Geben Sie unter **Name**den Namen des Datasets ein.  
  
3.  Vergewissern Sie sich, dass der Name in **Datenquelle**dem Namen der Datenquelle entspricht, die in Schritt 1 ausgewählt wurde.  
  
4.  Wählen Sie in **Abfragetyp**den Abfragetyp für die ausgewählte Datenquelle aus. In diesem Thema wird angenommen, dass der Abfragetyp **Text** ausgewählt wurde.  
  
5.  Geben Sie in **Abfrage**die Abfrage ein, mit der Werte für diesen Parameter abgerufen werden sollen. Abfragen für unabhängige Parameter enthalten normalerweise keine Abfrageparameter. Wenn Sie z. B. eine Abfrage für einen Parameter erstellen möchten, der alle Kategoriewerte bereitstellt, können Sie eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung wie die Folgende verwenden:  
  
    ```  
    SELECT DISTINCT <column name> FROM <table>  
    ```  
  
     Der SELECT DISTINCT-Befehl entfernt doppelte Werte aus dem Resultset, sodass Sie die einzelnen eindeutigen Werte aus der angegebenen Spalte in der angegebenen Tabelle abrufen.  
  
     Klicken Sie auf **Ausführen** (**!**). Im Resultset werden die Werte angezeigt, die für diesen ersten Parameter verfügbar sind.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Anschließend legen Sie die Eigenschaften des ersten Parameters fest, um mit diesem Dataset zur Laufzeit die verfügbaren Werte aufzufüllen.  
  
## <a name="to-set-available-values-for-a-report-parameter"></a>So legen Sie verfügbare Werte für einen Berichtsparameter fest  
  
1.  Klicken Sie im Berichtsdatenbereich im Ordner „Parameter“ mit der rechten Maustaste auf den ersten Parameter, und klicken Sie anschließend auf **Parametereigenschaften**.  
  
2.  Vergewissern Sie sich, dass in **Name**der korrekte Name des Parameters angegeben ist.  
  
3.  Klicken Sie auf **Verfügbare Werte**.  
  
4.  Klicken Sie auf **Werte aus Abfrage abrufen**. Es werden drei Felder angezeigt.  
  
5.  Klicken Sie in **Dataset**in der Dropdownliste auf den Namen des Datasets, das Sie in der vorherigen Prozedur erstellt haben.  
  
6.  Klicken Sie im Feld **Wert** auf den Namen des Felds, das den Parameterwert bereitstellt.  
  
7.  Klicken Sie im Feld **Bezeichnung** auf den Namen des Felds, das die Parameterbezeichnung bereitstellt.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Nun erstellen Sie ein Dataset, das die Werte für einen abhängigen Parameter bereitstellt.  
  
## <a name="to-create-a-dataset-to-provide-values-for-a-dependent-parameter"></a>So erstellen Sie ein Dataset zum Bereitstellen von Werten für einen abhängigen Parameter  
  
1.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf eine Datenquelle, und klicken Sie anschließend auf **Dataset hinzufügen**.  
  
2.  Geben Sie unter **Name**den Namen des Datasets ein.  
  
3.  Vergewissern Sie sich, dass der Name in **Datenquelle**dem Namen der Datenquelle entspricht, die in Schritt 1 ausgewählt wurde.  
  
4.  Wählen Sie in **Abfragetyp**den Abfragetyp für die ausgewählte Datenquelle aus. In diesem Thema wird angenommen, dass der Abfragetyp **Text** ausgewählt wurde.  
  
5.  Geben Sie in **Abfrage**die Abfrage ein, mit der Werte für diesen Parameter abgerufen werden sollen. Abfragen für abhängige Parameter enthalten normalerweise Abfrageparameter für jeden Parameter, von dem der betreffende Parameter abhängig ist. Wenn Sie beispielsweise eine Abfrage für einen Parameter erstellen möchten, der alle Unterkategoriewerte (abhängiger Parameter) für eine Kategorie (unabhängiger Parameter) bereitstellt, können Sie eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung wie die Folgende verwenden:  
  
    ```  
    SELECT DISTINCT Subcategory FROM <table>   
    WHERE (Category = @Category)  
    ```  
  
     In der WHERE-Klausel Kategorie den Namen eines Felds aus ist \<Tabelle > und @Category ist ein Abfrageparameter. Diese Anweisung erstellt eine Liste von Unterkategorien für die Kategorie, die im angegebenen @Category. Zur Laufzeit wird dieser Wert mit dem Wert ausgefüllt, der vom Benutzer für den Berichtsparameter mit demselben Namen ausgewählt wurde.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Anschließend legen Sie die Eigenschaften des zweiten Parameters fest, um mit diesem Dataset zur Laufzeit die verfügbaren Werte aufzufüllen.  
  
## <a name="to-set-available-values-for-a-report-parameter"></a>So legen Sie verfügbare Werte für einen Berichtsparameter fest  
  
1.  Klicken Sie im Berichtsdatenbereich im Ordner „Parameter“ mit der rechten Maustaste auf den ersten Parameter, und klicken Sie anschließend auf **Parametereigenschaften**.  
  
2.  Vergewissern Sie sich, dass in **Name**der korrekte Name des Parameters angegeben ist.  
  
3.  Klicken Sie auf **Verfügbare Werte**.  
  
4.  Klicken Sie auf **Werte aus Abfrage abrufen**.  
  
5.  Klicken Sie in **Dataset**in der Dropdownliste auf den Namen des Datasets, das Sie in der vorherigen Prozedur erstellt haben.  
  
6.  Klicken Sie im Feld **Wert** auf den Namen des Felds, das den Parameterwert bereitstellt.  
  
7.  Klicken Sie im Feld **Bezeichnung** auf den Namen des Felds, das die Parameterbezeichnung bereitstellt.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-test-the-cascading-parameters"></a>So testen Sie die kaskadierenden Parameter  
  
1.  Klicken Sie auf **Ausführen**.  
  
2.  Wählen Sie in der Dropdownliste für den ersten unabhängigen Parameter einen Wert aus.  
  
     Der Berichtsprozessor führt die Datasetabfrage für den nächsten Parameter aus und übergibt den Wert, den Sie für den ersten Parameter ausgewählt haben. Die Dropdownliste für den zweiten Parameter wird mit den verfügbaren Werten gefüllt, die auf dem Wert des ersten Parameters beruhen.  
  
3.  Wählen Sie in der Dropdownliste für den zweiten, abhängigen Parameter einen Wert aus.  
  
     Der Bericht wird nach dem Auswählen des letzten Parameters nicht automatisch ausgeführt, sodass Sie eine andere Auswahl vornehmen können.  
  
4.  Klicken Sie auf **Bericht anzeigen**. Die Anzeige des Berichts wird mit den ausgewählten Parametern aktualisiert.  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen, Ändern oder Löschen von Berichtsparametern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Tutorial: Hinzufügen eines Parameters zum Bericht &#40;Berichts-Generator&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Lernprogramme für den Berichts-Generator](../../reporting-services/report-builder-tutorials.md)   
 [Hinzufügen von Datasetfiltern, Datenbereichsfiltern und Gruppenfiltern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
