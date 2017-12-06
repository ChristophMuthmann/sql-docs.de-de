---
title: "Lektion 2: Ändern der Eigenschaften der Berichtsdatenquelle | Microsoft-Dokumentation"
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
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
caps.latest.revision: "43"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: ba7880d9cc6f316b7ce06b73dda896becd892797
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>Lektion 2: Ändern der Eigenschaften der Berichtsdatenquelle
In dieser Lektion des [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] Tutorials verwenden Sie das Webportal, um einen Bericht auszuwählen, der an Empfänger übermittelt werden soll. Das datengesteuerte Abonnement, das Sie definieren, verteilt den im Tutorial **Erstellen eines einfachen Tabellenberichts &#40;SSRS-Tutorial&#41;** erstellten Bericht [Erstellen eines einfachen Tabellenberichts &amp;#40;SSRS-Tutorial&amp;#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  In den folgenden Schritten wird erläutert, wie Sie die Datenquellen-Verbindungsinformationen ändern, die vom Bericht zum Abrufen von Daten verwendet werden. Nur Berichte, die **gespeicherte Anmeldeinformationen** für das Zugreifen auf eine Berichtsdatenquelle verwenden, können über ein datengesteuertes Abonnement verteilt werden. Für die unbeaufsichtigte Berichtsverarbeitung sind gespeicherte Anmeldeinformationen erforderlich.  
  
Sie ändern auch das Dataset und den Bericht, um einen Parameter zu verwenden, mit dem der Bericht nach `[Order]` gefiltert wird, damit das Abonnement verschiedene Instanzen des Berichts für bestimmte Aufträge und Renderingformate ausgeben kann.  
  
## <a name="bkmk_modify_datasource"></a>So ändern Sie eine Datenquelle zur Verwendung von gespeicherten Anmeldeinformationen  
  
1.  Navigieren Sie zum [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] Webportal mit Administratorrechten, indem Sie z.B. mit der rechten Maustaste auf das Symbol für Internet Explorer und anschließend auf **Als Administrator ausführen**klicken.  
 
2.    Navigieren Sie zur Webportal-URL.  Beispiel:   
    `http://<server name>/reports`.  
    `http://localhost/reports`
 **Hinweis:** Sie *Webportal* -URL lautet „Reports“, nicht die URL des *Berichtsservers* „Berichtsserver“.  
3.  Navigieren Sie zu dem Ordner, der den Bericht **Sales Orders** enthält, und klicken Sie im Kontextmenü des Berichts auf **Verwalten**.  
 
 ![ssrs_Tutorial_datadriven_Bericht_verwalten](../reporting-services/media/ssrs-tutorial-datadriven-manage-report.png)
  
3.  Klicken Sie auf **Datenquellen** im linken Bereich.  
  
4.  Achten Sie darauf, dass beim **Verbindungstyp** der **Microsoft SQL Server**eingestellt ist.  
  
5.  Die benutzerdefinierte Datenquellenverbindungszeichenfolge muss wie folgt lauten (es wird vorausgesetzt, dass sich die Beispieldatenbank auf einem lokalen Datenbankserver befindet):  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
6.  Klicken Sie auf **Die folgenden Anmeldeinformationen verwenden**.  
  
7. In **Typ der Anmeldeinformationen**wählen Sie **Windows-Benutzername und Kennwort**
8. Geben Sie Ihren Benutzernamen (verwenden Sie das Format *domain\user*) und Ihr Kennwort ein. Wenn Sie über keine Zugriffsberechtigung für die AdventureWorks2014-Datenbank verfügen, geben Sie eine gültige Anmeldung an.  
    
9. Klicken Sie auf **Verbindung testen** , um sicherzustellen, dass die Verbindung mit der Datenquelle hergestellt werden kann.  
  
10. Klicken Sie auf **Speichern**.
11. Klicken Sie auf **Abbrechen**  
  
11. Zeigen Sie den Bericht an, um zu überprüfen, ob er mit den von Ihnen angegebenen Anmeldeinformationen ausgeführt wird. .  
  
## <a name="bkmk_modify_dataset"></a>So ändern Sie den AdventureWorksDataset  
 In den folgenden Schritten ändern Sie das Dataset, um einen Parameter zu verwenden, damit sich das Dataset nach einer Bestellnummer filtern lässt.
1.  Öffnen Sie den Bericht **Sales Orders** in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]  
  
2.  Klicken Sie mit der rechten Maustaste auf das Dataset `AdventureWorksDataset` und anschließend auf **Dataseteigenschaften**.  
    ![ssrs_Tutorial_datadriven_Dataseteigenschaften](../reporting-services/media/ssrs-tutorial-datadriven-datasetproperties.png)  
3.  Fügen Sie die Anweisung `WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)` vor der Anweisung `Group By` hinzu. Die vollständige Abfragesyntax lautet wie folgt:  
  
    ```  
    SELECT soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal)  AS LineTotal  
    FROM Sales.SalesPerson AS sp INNER JOIN  
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN  
       Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID INNER JOIN  
       Production.Product AS pp ON sd.ProductID = pp.ProductID  
    INNER JOIN  
       Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID   
    INNER JOIN  
        Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID  
  
    WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)  
  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID  
    HAVING (ppc.Name = 'Clothing')  
    ```  
  
4.  Klicken Sie auf **OK**.  
 In den folgenden Schritten fügen Sie einen Parameter zum Bericht hinzu.  Der Berichtsparameter dient als Feed des Datasetparameters. 
## <a name="bkmk_add_reportparameter"></a>So fügen Sie einen Berichtsparameter hinzu und veröffentlichen den Bericht erneut  
  
1.  Im Bereich **Berichtsdaten** erweitern Sie den Parameter-Ordner und doppelklicken Sie auf den Parameter **Ordernumber** .  Er wurde als Teil der vorherigen Schritte automatisch erstellt, als Sie den Parameter zum Dataset hinzugefügt haben. Klicken Sie auf **Neu** und anschließend auf **Parameter...**  
 ![ssrs_Tutorial_datadriven_Parameter](../reporting-services/media/ssrs-tutorial-datadriven-parameter.png) 
2.  **Name** muss `OrderNumber`sein.  
  
3.  **Prompt** muss `OrderNumber`sein.  
  
4.  Wählen Sie **Leeren Wert zulassen ("")**aus.  
  
5.  Wählen Sie **NULL-Wert zulassen**aus.  
  
6.  Klicken Sie auf **OK**.  
  
7.  Klicken Sie auf die Registerkarte **Vorschau** zum Ausführen des Berichts. Beachten Sie den Parametereingabebereich am oberen Rand des Berichts. Sie haben folgende Möglichkeiten:  
  
    -   Klicken Sie auf "Bericht anzeigen", um den vollständigen Bericht zu sehen, ohne einen Parameter zu verwenden.  
  
    -   Deaktivieren Sie die Option **Null** und geben Sie eine Bestellnummer ein, z.B. *so71949*. Klicken Sie anschließend auf **Bericht anzeigen** , um nur die eine Bestellung im Bericht anzuzeigen.  
    ![ssrs_tutorial_datadriven_reportviewer_parameter](../reporting-services/media/ssrs-tutorial-datadriven-reportviewer-parameter.png) 
 
  
## <a name="bkmk_redeploy"></a>Bericht erneut bereitstellen  
  
1.  Stellen Sie den Bericht erneut bereit, damit bei der Abonnementkonfiguration in der nächsten Lektion die in dieser Lektion vorgenommenen Änderungen verwendet werden können. Weitere Informationen zu den Projekteigenschaften, die im Tabellentutorial verwendet werden, finden Sie im Abschnitt „So veröffentlichen Sie den Bericht auf dem Berichtsserver (Optional)“ in [Lektion 6: Hinzufügen von Gruppierungen und Gesamtwerten (Reporting Services)](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).  
  
2.  Klicken Sie auf der Symbolleiste auf **Erstellen** , und klicken Sie dann auf **Tutorial bereitstellen**.  
  
## <a name="next-steps"></a>Nächste Schritte  
+ Sie haben damit erfolgreich den Bericht so konfiguriert, dass er beim Abrufen von Daten gespeicherte Anmeldeinformationen verwendet und die Daten mit einem Parameter gefiltert werden können. 
+ In der nächsten Lektion Konfigurieren Sie das Abonnement mithilfe der datengesteuerten Abonnements des Webportals. Siehe [Lektion 3: Definieren eines datengesteuerten Abonnements](../reporting-services/lesson-3-defining-a-data-driven-subscription.md).  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Berichtsdatenquellen](../reporting-services/report-data/manage-report-data-sources.md)  
[Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
[Erstellen eines datengesteuerten Abonnements &#40;SSRS-Tutorial&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[Erstellen eines einfachen Tabellenberichts &#40;SSRS-Tutorial&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
  

