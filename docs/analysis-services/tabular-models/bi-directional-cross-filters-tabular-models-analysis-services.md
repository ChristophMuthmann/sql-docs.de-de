---
title: Bidirektionale kreuzfilter-Analysis-Services - Tabellenmodelle - | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5e810707-f58d-4581-8f99-7371fa75b6ac
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 98a16bacbaf839d65555b1495e7010d98a88e857
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="bi-directional-cross-filters---tabular-models---analysis-services"></a>Bidirektionale kreuzfilter-- tabellenmodellen - Analysis Services
  Neu in SQL Server 2016 ist eine integrierte Methode zum Aktivieren *bidirektionaler Kreuzfilter* in tabellarischen Modellen, durch die keine Notwendigkeit für manuell erstellte DAX-Umgehungen für die Tabellenbeziehungen übergreifende Weitergabe des Filterkontexts mehr besteht.  
  
 Das Konzept lässt sich wie folgt in seine Komponenten unterteilen: Die *Kreuzfilterung* ist die Möglichkeit, einen Filterkontext für eine Tabelle basierend auf Werten in einer verknüpften Tabelle festzulegen, und *bidirektional* ist die Übertragung eines Filterkontexts an eine zweite verknüpfte Tabelle auf der anderen Seite einer Tabellenbeziehung. Wie der Name schon sagt, ist eine Segmentierung in beide Richtungen der Beziehung und nicht bloß in eine möglich.  Intern wird bei der bidirektionalen Filterung der Filterkontext so erweitert, dass eine Obermenge Ihrer Daten abgefragt wird.  
  
 ![SSAS-BIDI-1-Filteroption](../../analysis-services/tabular-models/media/ssas-bidi-1-filteroption.PNG "SSAS-BIDI-1-Filteroption")  
  
 Es gibt zwei Arten von Kreuzfilterung: uni- und bidirektional. Unidirektional ist die herkömmliche n:1-Filterrichtung zwischen Fakten- und Dimensionstabellen in der jeweiligen Beziehung. Bidirektional heißt ein Kreuzfilter, der ermöglicht, dass der Filterkontext einer Beziehung als Filterkontext einer anderen Tabellenbeziehung verwendet wird, wobei beide Beziehungen eine Tabelle gemeinsam haben.  
  
 Wenn **DimDate** und **DimProduct** mit Fremdschlüsselbeziehungen zu **FactOnlineSales**gegeben sind, entspricht ein bidirektionaler Kreuzfilter der gleichzeitigen Verwendung von **FactOnlineSales-to-DimDate** plus **FactOnlineSales-to-DimProduct** .  
  
 Bidirektionale Kreuzfilter können eine einfache Lösung für das Entwurfsproblem von m:n-Abfragen sein, vor dem Tabellen- und Power Pivot-Entwickler bislang standen. Wenn Sie die DAX-Umgehung für m:n-Beziehungen in Tabellen- oder PowerPivot-Modellen verwendet haben, können Sie versuchen, einen bidirektionalen Filter anzuwenden, um festzustellen, ob er die erwarteten Ergebnisse liefert.  
  
 Wenn Sie einen bidirektionalen Kreuzfilter erstellen, bedenken Sie die folgenden Punkte:  
  
-   Prüfen Sie sorgfältig, ob bidirektionale Filter aktiviert werden sollten.  
  
     Wenn Sie überall bidirektionale Filter aktivieren, könnten Ihre Daten zu stark in einer Weise gefiltert werden, die Sie ggf. nicht erwarten.  Sie können auch versehentlich für Mehrdeutigkeit sorgen, indem Sie mehr als einen potenziellen Abfragepfad erstellen. Um beide Probleme zu vermeiden, planen Sie eine Kombination aus unidirektionalen und bidirektionalen Filtern.  
  
-   Führen Sie Tests stufenweise durch, um die Auswirkung der einzelnen Filteränderungen auf das Modell zu überprüfen. [In Excel analysieren](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md) eignet sich gut für das stufenweise Testen. Als bewährte Methode sollten Sie in regelmäßigen Abständen Tests mit anderen Clients für die Berichterstellung durchführen, damit es später nicht zu Überraschungen kommt.  
  
> [!NOTE]  
>  Ab Version CTP 3.2 enthält SSDT einen Standardwert, der bestimmt, ob eine bidirektionale Kreuzfilterung automatisch versucht wird. Wenn Sie bidirektionale Filter standardmäßig aktivieren, aktiviert SSDT die bidirektionale Filterung nur dann, wenn im Modell ein Abfragepfad durch eine Kette von Beziehungen klar definiert wird.  
  
## <a name="set-the-default"></a>Festlegen des Standards  
 Unidirektionale Filter sind Standard. Sie können den Standard für alle neuen im Designer erstellten Projekte oder für das Modell selbst ändern, sollte das Projekt bereits vorhanden sein.  
  
 Auf Projektebene wird die Einstellung ausgewertet, wenn Sie das Projekt so erstellen. Wenn Sie also die Standardeinstellung in „Bidirektional“ ändern, werden die Auswirkungen Ihrer Auswahl beim Erstellen des nächsten Projekts wirksam.  
  
1.  Wählen Sie in SSDT **Tools** > **Optionen** > **Analysis Services-Tabellen-Designer** > **Neue Projekteinstellungen**.  
  
2.  Legen Sie **Standardfilterrichtung** entweder auf **Unidirektional** oder **Bidirektional**fest.  
  
 Alternativ können Sie den Standard für das Modell ändern.  
  
1.  Wählen Sie im Projektmappen-Explorer **Model.bim** > **Eigenschaften** aus.  
  
2.  Legen Sie **Standardfilterrichtung** entweder auf **Unidirektional** oder **Bidirektional**fest.  
  
## <a name="walkthrough-an-example"></a>Exemplarische Vorgehensweise anhand eines Beispiels  
 Die beste Möglichkeit, den Nutzen der bidirektionalen Kreuzfilterung zu erkennen, ist ein Beispiel. Betrachten Sie das folgende Dataset aus [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279), und sehen Sie sich die Kardinalität und Kreuzfilter an, die standardmäßig erstellt werden.  
  
 ![SSAS-BIDI-2-Modell](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "SSAS-BIDI-2-Modell")  
  
> [!NOTE]  
>  Tabellenbeziehungen werden standardmäßig während des Datenimports für Sie in n:1-Konfigurationen erstellt, die von den Beziehungen zwischen Fremdschlüsseln und Primärschlüsseln zwischen der Faktentabelle und verknüpften Dimensionstabellen abgeleitet werden.  
  
 Beachten Sie, dass die Filterrichtung von Dimensionstabellen zur Faktentabelle ist. Werbeaktionen, Produkte, Datumsangaben, Kunde und Kundenregion sind allesamt gültige Filter, die erfolgreich eine bestimmte Aggregation eines Measures liefern. Dabei variiert der Istwert basierend auf den verwendeten Dimensionen.  
  
 ![SSAS-Bidi-3-Defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "Ssas-Bidi-3-Defaultrelationships")  
  
 Für dieses einfache Sternschema ergibt ein Test in Excel, dass Daten wie gewünscht segmentiert werden, wenn die Filterung von Dimensionstabellen für Zeilen und Spalten zu aggregierten Daten erfolgt, die vom Measure **Sum of Sales** erfolgt, dass sich in der zentralen Tabelle **FactOnlineSales** befindet.  
  
 ![SSAS-Bidi-4-ExcelSumSales](../../analysis-services/tabular-models/media/ssas-bidi-4-excelsumsales.PNG "Ssas-Bidi-4-ExcelSumSales")  
  
 Solange Measures aus der Faktentabelle abgerufen werden und der Filterkontext bei der Faktentabelle endet, werden die Aggregationen für dieses Modell ordnungsgemäß gefiltert. Doch was geschieht, wenn Sie Measures woanders erstellen möchten, z. B. eine diskrete Anzahl in der Produkt- oder Kundentabelle oder einen Durchschnittsrabatt in der Tabelle mit den Werbeaktionen, und dafür sorgen, dass ein vorhandener Filterkontext auf dieses Measure erweitert wird.  
  
 Versuchen Sie es, indem Sie eine diskrete Anzahl aus **DimProducts** der PivotTable hinzufügen. Beachten Sie die sich wiederholenden Werte für **Count Products**. Auf den ersten Blick sieht es so aus, als fehle eine Tabellenbeziehung. Doch in unserem Modell können wir erkennen, dass alle Beziehungen vollständig definiert und aktiv sind. In diesem Fall treten die sich wiederholenden Werte auf, da es für die Zeilen in der Produkttabelle keinen Datumsfilter gibt.  
  
 ![SSAS-Bidi-5-Prodcount-Nofilter](../../analysis-services/tabular-models/media/ssas-bidi-5-prodcount-nofilter.png "Ssas-Bidi-5-Prodcount-Nofilter")  
  
 Nach Hinzufügen eines bidirektionalen Kreuzfilters zwischen **FactOnlineSales** und **DimProduct**werden die Zeilen in der Produkttabelle nun ordnungsgemäß nach Hersteller und Datum gefiltert.  
  
 ![SSAS-Bidi-6-Prodcount-Withfilter](../../analysis-services/tabular-models/media/ssas-bidi-6-prodcount-withfilter.png "Ssas-Bidi-6-Prodcount-Withfilter")  
  
## <a name="learn-step-by-step"></a>Schrittweises Lernen  
 Sie können bidirektionale Kreuzfilter durch schrittweises Durchlaufen dieser exemplarischen Vorgehensweise ausprobieren. Um folgen zu können, benötigen Sie Folgendes:  
  
-   SQL Server 2016 Analysis Services-Instanz im tabellarischen Modus mit aktueller CTP-Version  
  
-   [SQL Server Data Tools für Visual Studio 2015 (SSDT)](http://go.microsoft.com/fwlink/p/?LinkID=627574)(im Funktionsumfang der aktuellen CTP-Version)  
  
-   [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279)  
  
-   Leseberechtigungen für diese Daten  
  
-   Excel (zur Verwendung von „In Excel analysieren“)  
  
### <a name="create-a-project"></a>Erstellen eines Projekts  
  
1.  Starten Sie SQL Server Data Tools für Visual Studio 2015.  
  
2.  Klicken Sie auf **Datei** > **Neu** > **Projekt** > **Analysis Services-Tabellenmodell**.  
  
3.  Legen Sie im Tabellenmodell-Designer die Arbeitsbereichs-Datenbank auf eine SQL Server 2016 Preview Analysis Services-Instanz im tabellarischen Servermodus fest.  
  
4.  Überprüfen Sie die Modell-Kompatibilitätsgrad auf festgelegt ist **SQL Server 2016 RTM (1200)** oder höher.  
  
     Klicken Sie auf **OK** , um das Projekt zu erstellen.  
  
### <a name="add-data"></a>Hinzufügen von Daten  
  
1.  Klicken Sie auf **Modell** > **Aus Datenquelle importieren** > **Microsoft SQL Server**.  
  
2.  Geben Sie den Server, die Datenbank und Authentifizierungsmethode an.  
  
3.  Wählen Sie die Datenbank „ContosoRetailDW“ aus.  
  
4.  Klicken Sie auf **Weiter**.  
  
5.  Klicken Sie zur Tabellenauswahl bei gedrückter STRG-TASTE auf die folgenden Tabellen:  
  
    -   FactOnlineSales  
  
    -   DimCustomer  
  
    -   DimDate  
  
    -   DimGeography  
  
    -   DimPromotion  
  
     Sie können an dieser Stelle die Namen bearbeiten, wenn Sie im Modell einfacher lesbar sein sollen.  
  
     ![SSAS-Bidi-7-Importdaten](../../analysis-services/tabular-models/media/ssas-bidi-7-importdata.PNG "Ssas-Bidi-7-Importdaten")  
  
6.  Importieren Sie die Daten.  
  
 Wenn Sie Fehlermeldungen erhalten, vergewissern Sie sich, dass das Konto zum Verbinden mit der Datenbank über eine SQL Server-Anmeldung mit Leseberechtigung für das Data Warehouse „Contoso“ verfügt. Bei einer Remoteverbindung sollten Sie auch die Konfiguration von Ports in der Firewall für SQL Server prüfen.  
  
### <a name="review-default-table-relationships"></a>Überprüfen der Standardtabellenbeziehungen  
 Wechseln Sie zur Diagrammansicht: **Modell** > **Modellansicht** > **Diagrammansicht**. Kardinalität und aktive Beziehungen werden visuell angezeigt. Alle Beziehungen sind 1:n zwischen zwei beliebigen verknüpften Tabellen.  
  
 ![SSAS-BIDI-2-Modell](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "SSAS-BIDI-2-Modell")  
  
 Klicken Sie alternativ auf **Tabelle** > **Beziehungen verwalten** , um die gleichen Informationen in einem Tabellenlayout anzeigen.  
  
 ![SSAS-Bidi-3-Defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "Ssas-Bidi-3-Defaultrelationships")  
  
### <a name="create-measures"></a>Erstellen von Measures  
 Sie benötigen eine Aggregation zum Summieren von Umsatzbeträgen anhand verschiedener Facets von Dimensionsdaten. In **DimProduct** können Sie ein Measure erstellen, das Produkte zählt. Dieses können Sie anschließend in einer Analyse der Produktvermarktung nutzen, die zeigt, wie viele Produkte für ein bestimmtes Jahr, eine bestimmte Region oder einen Kundentyp am Umsatz beteiligt waren.  
  
1.  Klicken Sie auf **Modell** > **Modellansicht** > **Diagrammansicht**.  
  
2.  Klicken Sie auf **FactOnlineSales**.  
  
3.  Wählen Sie die Spalte **SalesAmount** aus.  
  
4.  Klicken Sie auf **Spalte** > **AutoSumme** > **Summe** , um ein Measure für den Umsatz zu erstellen.  
  
5.  Klicken Sie auf **DimProduct**.  
  
6.  Wählen Sie die Spalte **ProductKeycolumn**aus.  
  
7.  Klicken Sie auf **Spalte** > **AutoSumme** > **DistinctCount** , um ein Measure für eindeutige Produkte zu erstellen.  
  
### <a name="analyze-in-excel"></a>In Excel analysieren  
  
1.  Klicken Sie auf **Modell** > **In Excel analysieren** , um alle Daten in einer PivotTable zusammenzuführen.  
  
2.  Wählen Sie in der Feldliste die beiden Measures aus, die Sie gerade erstellt haben.  
  
3.  Wählen Sie **Produkte** > **Hersteller**.  
  
4.  Wählen Sie **Datum** > **Kalenderjahr**aus.  
  
 Beachten Sie, dass die Umsätze wie erwartet nach Jahr und Hersteller unterteilt werden. Der Grund hierfür ist, dass der Standardfilterkontext zwischen **FactOnlineSales**, **DimProduct**und **DimDate** für Measures auf der n-Seite der Beziehung ordnungsgemäß funktioniert.  
  
 Gleichzeitig können Sie erkennen, dass für die Produktanzahl nicht derselbe Filterkontext wie für den Umsatz verwendet wird. Während die Produktanzahlen ordnungsgemäß anhand des Herstellers gefiltert werden (sowohl die Hersteller- als auch die Produktanzahlen befinden sich in derselben Tabelle), wird der Datumsfilter nicht an die Produktanzahl weitergegeben.  
  
### <a name="change-the-cross-filter"></a>Ändern des Kreuzfilters  
  
1.  Zurück im Modell wählen Sie **Tabelle** > **Beziehungen verwalten**aus.  
  
2.  Bearbeiten Sie die Beziehung zwischen **FactOnlineSales** und **DimProduct**.  
  
     Ändern Sie die Filterrichtung für beide Tabellen.  
  
3.  Speichern Sie die Einstellungen.  
  
4.  Klicken Sie in der Arbeitsmappe auf **Aktualisieren** , um das Modell erneut einzulesen.  
  
 Nun sollte erkennbar sein, dass sowohl Produktzahlen als auch Umsätze anhand des gleichen Filterkontexts gefiltert werden, der nicht nur Hersteller aus **DimProducts** , sondern auch das Kalenderjahr aus **DimDate**enthält.  
  
## <a name="conclusion-and-next-steps"></a>Zusammenfassung und nächste Schritte  
 Ob und wie ein Kreuzfilter sinnvoll ist, kann ein ausgiebiges Ausprobieren erfordern, um festzustellen, ob ein solcher Filter in Ihrem Szenario funktioniert. Mitunter werden Sie feststellen, dass die integrierten Verhalten nicht ausreichend sind, sodass Sie auf DAX-Berechnungen zurückgreifen müssen, um die Aufgabe zu erledigen. Im Abschnitt **Siehe auch** finden Sie einige Links zu weiteren Ressourcen zu diesem Thema.  
  
 Aus praktischer Sicht kann die Kreuzfilterung Formen der Datenuntersuchung ermöglichen, die normalerweise nur mit einer m:n-Konstruktion möglich ist. Vor diesem Hintergrund ist anzumerken, dass die bidirektionale Kreuzfilterung kein m:n-Konstrukt ist.  Eine tatsächliche m:n-Tabellenkonfiguration wird im Designer für tabellarische Modelle in dieser Version weiterhin nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Verwalten von Beziehungen in Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/464155-create-and-manage-relationships-in-power-bi-desktop)   
 [Ein praktisches Beispiel zur Behandlung einfacher m-Pivot-Beziehungen in Power Pivot und SSAS-Tabellenmodelle](http://social.technet.microsoft.com/wiki/contents/articles/22202.a-practical-example-of-how-to-handle-simple-many-to-many-relationships-in-power-pivotssas-tabular-models.aspx)   
 [Auflösen von m: n-Beziehungen, die mithilfe der DAX-kreuztabellenfilterung](http://blog.gbrueckl.at/2012/05/resolving-many-to-many-relationships-leveraging-dax-cross-table-filtering/)   
 [M: n-Revolution (SQLBI-Blog)](http://www.sqlbi.com/articles/many2many/)  
  
  

