---
title: Erstellen von MDX-Abfragen mit olapR | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: c12b988e-be7e-41ba-a84c-299a5c45d4ab
caps.latest.revision: 3
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: adcc1c80fdd04cfa3f49b550e5ea5fd8cc34003a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="how-to-create-mdx-queries-using-olapr"></a>Erstellen von MDX-Abfragen mit olapR
## <a name="how-to-build-an-mdx-query-from-r"></a>Erstellen einer MDX-Abfrage aus R

1. Definieren Sie eine Verbindungszeichenfolge, die die OLAP-Datenquelle (SSAS-Instanz) und den MSOLAP-Anbieter angibt.

2. Verwenden Sie die Funktion `OlapConnection(connectionString)` , um ein Handle für die MDX-Abfrage zu erstellen und die Verbindungszeichenfolge zu übergeben.

3. Verwenden Sie den `Query()` -Konstruktor zum Instanziieren eines Abfrageobjekts.

4. Verwenden Sie die folgenden Hilfsfunktionen, um weitere Details über die Dimensionen und Measures anzugeben, die in der MDX-Abfrage enthalten sein sollen:
     + `cube()` Geben Sie den Namen der SSAS-Datenbank an.
     + `columns()` Geben Sie die Namen der zu verwendenden Measures im ON COLUMNS-Argument an.  
     + `rows()` Geben Sie die Namen der zu verwendenden Measures im ON ROWS-Argument an.
     + `slicers()` Geben Sie ein Feld oder Elemente an, das bzw. die als Datenschnitt verwendet werden soll(en). Ein Datenschnitt funktioniert wie ein Filter, der auf alle MDX-Abfragedaten angewendet wird.
     
     + `axis()` Geben Sie den Namen einer in der Abfrage zu verwendenden zusätzlichen Achse an. Ein OLAP-Cube kann bis zu 128 Abfrageachsen enthalten. Im Allgemeinen werden die ersten vier Achsen als Spalten, Zeilen, Seiten und Kapitel bezeichnet. Wenn Ihre Abfrage relativ einfach ist, können Sie die Funktionen `columns`, `rows`usw. verwenden, um Ihre Abfrage zu erstellen.     
     Jedoch können Sie auch die `axis()` -Funktion mit einem Indexwert ungleich null verwenden, um eine MDX-Abfrage mit vielen Qualifizierern zu erstellen oder zusätzliche Dimensionen als Qualifizierer hinzuzufügen.

5. Übergeben Sie das Handle und die fertiggestellte MDX-Abfrage an die Funktionen `executeMD` oder `execute2D`, je nach Form der Ergebnisse.

  + `executeMD` Gibt ein mehrdimensionales Array zurück
  + `execute2D` Gibt einen zweidimensionalen (tabellarischen) Datenrahmen zurück


## <a name="how-to-run-an-existing-mdx-query-from-r"></a>Ausführen einer vorhandenen MDX-Abfrage aus R

1. Definieren Sie eine Verbindungszeichenfolge, die die OLAP-Datenquelle (SSAS-Instanz) und den MSOLAP-Anbieter angibt.

2. Verwenden Sie die Funktion `OlapConnection(connectionString)` , um ein Handle für die MDX-Abfrage zu erstellen und die Verbindungszeichenfolge zu übergeben.

3. Definieren Sie eine R-Variable zum Speichern des Texts der MDX-Abfrage.

4. Übergeben Sie das Handle und die Variable, die die MDX-Abfrage enthält, an die Funktionen `executeMD` oder `execute2D`, je nach Form der Ergebnisse.

    + `executeMD` Gibt ein mehrdimensionales Array zurück
    + `execute2D` Gibt einen zweidimensionalen (tabellarischen) Datenrahmen zurück



## <a name="examples"></a>Beispiele

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
+ Diese Abfrage würde eine Tabelle mit drei Spalten zurückgeben, die eine _Rollup_ -Zusammenfassung der Internetumsätze aus allen Ländern enthält. 
+ Die WHERE-Klausel bildet die _Datenschnittachse_. Der Datenschnitt verwendet ein Element der Verkaufsgebiet-Dimension zum Filtern der Abfrage, sodass nur Umsätze aus Australien in Berechnungen verwendet werden.

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

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>So führen Sie diese Abfrage als vordefinierte MDX-Zeichenfolge aus

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

Beachten Sie, dass beim Definieren von Abfragen mithilfe des MDX-Generators in SQL Server Management Studio und dem anschließenden Speichern der MDX-Zeichenfolge die Nummerierung der Achsen bei 0 beginnt, wie hier dargestellt: 

~~~~
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Country].[Australia]
~~~~

Trotzdem können Sie diese Abfrage als vordefinierte MDX-Zeichenfolge ausführen. Um jedoch die gleiche Abfrage mithilfe von R und der `axis()`-Funktion zu erstellen, achten Sie darauf, die Nummerierung der Achsen mit 1 zu beginnen.


### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2. Durchsuchen von Cubes und ihren Feldern in einer SSAS-Instanz

Sie können die `explore`-Funktion verwenden, um eine Liste der Cubes, Dimensionen oder Elemente zurückzugeben, die zum Erstellen Ihrer Abfrage verwendet werden sollen. Dies ist praktisch, wenn Sie keinen Zugang zu anderen Tools zum Durchsuchen von OLAP haben oder die MDX-Abfrage programmgesteuert erstellen oder ändern möchten.

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>So listen Sie die für die angegebene Verbindung verfügbaren Cubes auf

Um alle Cubes oder Perspektiven auf der Instanz anzuzeigen, für die Sie eine Ansichtsberechtigung besitzen, übergeben Sie das Handle als Argument an `explore`.
Beachten Sie, dass das Endergebnis kein Cube ist; WAHR zeigt einfach an, dass die Metadatenoperation erfolgreich war. Bei ungültigen Argumenten wird ein Fehler ausgelöst.

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

Geben Sie nach dem Definieren der Quelle und dem Erstellen des Handles den Cube, die Dimension und die Hierarchie an, die zurückgegeben werden sollen.
Beachten Sie, dass Elemente in den Rückgabeergebnissen, denen **->** vorangestellt ist, untergeordnete Elemente des zuvor aufgelisteten Elements darstellen.

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

[Verwenden von Daten aus OLAP-Cubes in R](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md)

