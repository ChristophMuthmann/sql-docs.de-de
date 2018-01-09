---
title: Zum Erstellen von MDX-Abfragen, die mit OlapR | Microsoft Docs
ms.custom: 
ms.date: 11/29/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: c12b988e-be7e-41ba-a84c-299a5c45d4ab
caps.latest.revision: "3"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3ac889212aaccb25d0c738195e2e2e04c3c1a5d4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="how-to-create-mdx-queries-using-olapr"></a>Vorgehensweise: Erstellen von MDX-Abfragen mit olapR

Die [OlapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) Paket unterstützt MDX-Abfragen für Cubes in SQL Server Analysis Services gehostet. Sie können eine Abfrage für einen vorhandenen Cube zu erstellen, Durchsuchen von Dimensionen und andere Cubeobjekte und fügen Sie in vorhandenen MDX-Abfragen zum Abrufen von Daten.

Dieser Artikel beschreibt die zwei Hauptanwendungsgebiete von der **OlapR** Paket:

+ [Erstellen Sie eine MDX-Abfrage von R, mithilfe der Konstruktoren, die im Paket OlapR bereitgestellt](#buildMDX)
+ [Führen Sie eine gültige MDX-Abfrage, die mit OlapR und OLAP-Anbieter](#executeMDX)

Die folgenden Vorgänge werden nicht unterstützt:

+ DAX-Abfragen für ein tabellarisches Modell
+ Erstellen von neuen OLAP-Objekten
+ Rückschreiben von Daten in Partitionen, einschließlich Measures "oder" Summen

## <a name="buildMDX"></a>Erstellen Sie eine MDX-Abfrage von R

1. Definieren Sie eine Verbindungszeichenfolge, die die OLAP-Datenquelle (SSAS-Instanz) und den MSOLAP-Anbieter angibt.

2. Verwenden Sie die Funktion `OlapConnection(connectionString)` , um ein Handle für die MDX-Abfrage zu erstellen und die Verbindungszeichenfolge zu übergeben.

3. Verwenden Sie den `Query()` -Konstruktor zum Instanziieren eines Abfrageobjekts.

4. Verwenden Sie die folgenden Hilfsfunktionen, um weitere Details über die Dimensionen und Measures anzugeben, die in der MDX-Abfrage enthalten sein sollen:

     + `cube()` Geben Sie den Namen der SSAS-Datenbank an. Wenn eine Verbindung mit einer benannten Instanz herstellen, geben Sie den Computernamen und den Instanznamen ein. 
     + `columns()`Geben Sie die Namen von Measures zur Verwendung in der **ON Spalten** Argument.
     + `rows()`Geben Sie die Namen von Measures zur Verwendung in der **ON Zeilen** Argument.
     + `slicers()` Geben Sie ein Feld oder Elemente an, das bzw. die als Datenschnitt verwendet werden soll(en). Ein Datenschnitt funktioniert wie ein Filter, der auf alle MDX-Abfragedaten angewendet wird.
     
     + `axis()` Geben Sie den Namen einer in der Abfrage zu verwendenden zusätzlichen Achse an. 
     
         Ein OLAP-Cube kann bis zu 128 Abfrageachsen enthalten. In der Regel die ersten vier Achsen werden als bezeichnet **Spalten**, **Zeilen**, **Seiten**, und **Kapiteln**. 
         
         Wenn Ihre Abfrage relativ einfach ist, können Sie die Funktionen `columns`, `rows`usw. verwenden, um Ihre Abfrage zu erstellen. Jedoch können Sie auch die `axis()` -Funktion mit einem Indexwert ungleich null verwenden, um eine MDX-Abfrage mit vielen Qualifizierern zu erstellen oder zusätzliche Dimensionen als Qualifizierer hinzuzufügen.

5. Übergeben Sie das Handle und die abgeschlossene MDX-Abfrage in einem der folgenden Funktionen, abhängig von der Form der Ergebnisse: 

  + `executeMD` Gibt ein mehrdimensionales Array zurück
  + `execute2D` Gibt einen zweidimensionalen (tabellarischen) Datenrahmen zurück

## <a name="executeMDX"></a>Führen Sie eine gültige MDX-Abfrage von R

1. Definieren Sie eine Verbindungszeichenfolge, die die OLAP-Datenquelle (SSAS-Instanz) und den MSOLAP-Anbieter angibt.

2. Verwenden Sie die Funktion `OlapConnection(connectionString)` , um ein Handle für die MDX-Abfrage zu erstellen und die Verbindungszeichenfolge zu übergeben.

3. Definieren Sie eine R-Variable zum Speichern des Texts der MDX-Abfrage.

4. Übergeben Sie das Handle und die Variable, die die MDX-Abfrage enthält, an die Funktionen `executeMD` oder `execute2D`, je nach Form der Ergebnisse.

    + `executeMD` Gibt ein mehrdimensionales Array zurück
    + `execute2D` Gibt einen zweidimensionalen (tabellarischen) Datenrahmen zurück

## <a name="examples"></a>Beispiele

In den folgenden Beispielen basieren auf dem AdventureWorks Data Mart und den Cube-Projekt, da dieses Projekt ist weit verbreitet, in mehreren Versionen, einschließlich der Sicherungsdateien, die mit Analysis Services einfach wiederhergestellt werden können. Wenn Sie einen vorhandenen Cube besitzen, erhalten Sie einen Beispielcube mithilfe dieser Optionen aus:

+ Erstellen des Cubes, der verwendet wird, in diesen Beispielen anhand der Analysis Services-Lernprogramm bis zu Lektion 4: [erstellen einen OLAP-Cube](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)

+ Herunterladen von einem vorhandenen Cube als Sicherung, und stellen Sie es mit einer Instanz von Analysis Services wieder her. Diese Site enthält z. B. einen vollständig verarbeiteten Cubes im ZIP-Format: [Adventure Works mehrdimensionalen Modell SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334). Extrahieren Sie die Datei, und klicken Sie dann in der SSAS-Instanz wiederherstellen. Weitere Informationen finden Sie unter [Sicherung und Wiederherstellung](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md), oder [Restore-ASDatabase-Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md).

### <a name="1-basic-mdx-with-slicer"></a>1. Einfache MDX mit Datenschnitt

Diese MDX-Abfrage wählt die _Measures_ für die Anzahl und den Betrag von Internetumsätzen aus und platziert sie auf der Spaltenachse. Sie fügt ein Mitglied der Dimension „Verkaufsgebiet“ als *Datenschnitt*hinzu, um die Abfrage so zu filtern, dass nur Umsätze aus Australien in Berechnungen verwendet werden.

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, 
{[Product].[Product Line].[Product Line].MEMBERS} ON ROWS 
FROM [Analysis Services Tutorial] 
WHERE [Sales Territory].[Sales Territory Country].[Australia]
```

+ In Spalten können Sie mehrere Measures als Elemente einer durch Trennzeichen getrennten Zeichenfolge angeben.
+ Die Zeilenachse verwendet alle möglichen Werte (alle ELEMENTE) der Dimension „Produktlinie“. 
+ Diese Abfrage würde eine Tabelle mit drei Spalten, die mit Zurückgeben einer _Rollup_ Zusammenfassung der Internet Sales aus allen Ländern.
+ Die WHERE-Klausel gibt die _Slicer-Achse_. In diesem Beispiel wird der Slicer wird verwendet, ein Mitglied der **"salesterritory"** Dimension, um die Abfrage zu filtern, sodass nur die Umsätze von Handelspartnern aus Australien in Berechnungen verwendet werden.

#### <a name="to-build-this-query-using-the-functions-provided-in-olapr"></a>So erstellen Sie diese Abfrage mithilfe der in olapR bereitgestellten Funktionen

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

qry <- Query()
cube(qry) <- "[Analysis Services Tutorial]"
columns(qry) <- c("[Measures].[Internet Sales Count]", "[Measures].[Internet Sales-Sales Amount]")
rows(qry) <- c("[Product].[Product Line].[Product Line].MEMBERS") 
slicers(qry) <- c("[Sales Territory].[Sales Territory Country].[Australia]")

result1 <- executeMD(ocs, qry)

```

Müssen Sie für eine benannte Instanz alle Zeichen mit Escapezeichen, die Steuerzeichen in r berücksichtigt werden konnte  Die folgende Verbindungszeichenfolge verweist, beispielsweise eine Instanz OLAP01, auf einem Server mit dem Namen ContosoHQ:

```R
cnnstr <- "Data Source=ContosoHQ\\OLAP01; Provider=MSOLAP;"
```

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>So führen Sie diese Abfrage als vordefinierte MDX-Zeichenfolge aus

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

Wenn Sie eine Abfrage definieren, mit dem MDX-Generator in SQL Server Management Studio, und speichern Sie die MDX-Zeichenfolge, wird es die Achsen, beginnend mit 0, number, wie hier gezeigt: 

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Countr,y].[Australia]
```

Trotzdem können Sie diese Abfrage als vordefinierte MDX-Zeichenfolge ausführen. Allerdings die gleiche Abfrage mithilfe von R erstellen die `axis()` -Funktion, Sie müssen neu nummerieren die Achsen, beginnend mit 1.

### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2. Durchsuchen von Cubes und ihren Feldern in einer SSAS-Instanz

Sie können die `explore`-Funktion verwenden, um eine Liste der Cubes, Dimensionen oder Elemente zurückzugeben, die zum Erstellen Ihrer Abfrage verwendet werden sollen. Dies ist praktisch, wenn Sie keinen Zugang zu anderen Tools zum Durchsuchen von OLAP haben oder die MDX-Abfrage programmgesteuert erstellen oder ändern möchten.

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>So listen Sie die für die angegebene Verbindung verfügbaren Cubes auf

Um alle Cubes oder Perspektiven auf der Instanz anzuzeigen, für die Sie eine Ansichtsberechtigung besitzen, übergeben Sie das Handle als Argument an `explore`.

> [!IMPORTANT]
> Das Endergebnis ist **nicht** eines Cubes; "True" lediglich gibt an, dass der Metadatenvorgang erfolgreich war. Bei ungültigen Argumenten wird ein Fehler ausgelöst.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)
explore(ocs)
```

| Ergebnisse  |
| ----|
| _Analysis Services-Tutorial_|
|_Internetumsätze_|
|_Umsätze der Wiederverkäufer_|
|_Umsatzzusammenfassung_|
|_[1] WAHR_|

#### <a name="to-get-a-list-of-cube-dimensions"></a>So rufen Sie eine Liste der Cubedimensionen ab

Um alle Dimensionen im Cube oder der Perspektive anzuzeigen, geben Sie den Namen des Cubes oder der Perspektive an.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs \<- OlapConnection(cnnstr)
explore(ocs, "Sales")
```

| Ergebnisse  |
| ----|
| _Kunde_|
|_Datum_|
|_Region_|


#### <a name="to-return-all-members-of-the-specified-dimension-and-hierarchy"></a>So geben Sie alle Elemente der angegebenen Dimension und Hierarchie zurück

Geben Sie nach dem Definieren der Quelle und dem Erstellen des Handles den Cube, die Dimension und die Hierarchie an, die zurückgegeben werden sollen. In den zurückgegebenen Ergebnisse, Elemente, die mit dem Präfix  **->**  untergeordneten Elemente des vorherigen Elements darstellen.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs \<- OlapConnection(cnnstr)
explore(ocs, "Analysis Services Tutorial", "Product", "Product Categories", "Category")
```

| Ergebnisse  |
| ----|
| _Zubehör_|
|_Fahrräder_|
|_Bekleidung_|
|_Komponenten_|
|Montagekomponenten >|
|Montagekomponenten >|


## <a name="see-also"></a>Siehe auch

[Verwenden von Daten aus OLAP-Cubes in R](../../advanced-analytics/r/using-data-from-olap-cubes-in-r.md)
