---
title: "Modellfiltersyntax und Beispiele (Analysis Services – Datamining) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- model filter [data mining]
- filter syntax [data mining]
- filters [data mining]
- filters [Analysis Services]
ms.assetid: c729d9b3-8fda-405e-9497-52b2d7493eae
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c24c6ad5bbfba2f93039bd53609ddd86010e10ee
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="model-filter-syntax-and-examples-analysis-services---data-mining"></a>Modellfiltersyntax und Beispiele (Analysis Services - Data Mining)
  Dieser Abschnitt enthält ausführliche Informationen zur Syntax von Modellfiltern sowie Beispielausdrücke.  
  
 [Filtersyntax](#bkmk_Syntax)  
  
 [Filter für Fallattribute](#bkmk_Ex1)  
  
 [Filter für geschachtelte Tabellenattribute](#bkmk_Ex2)  
  
 [Filter für mehrere geschachtelte Tabellenattribute](#bkmk_Ex3)  
  
 [Filter für in der geschachtelten Tabelle fehlende Attribute](#bkmk_Ex4)  
  
 [Filter für mehrere geschachtelte Tabellenwerte](#bkmk_Ex5)  
  
 [Filter für geschachtelte Tabellenattribute und EXISTS](#bkmk_Ex6)  
  
 [Filterkombinationen](#bkmk_Ex7)  
  
 [Filter für Datumsangaben](#bkmk_Ex8)  
  
##  <a name="bkmk_Syntax"></a> Filter Syntax  
 Filterausdrücke entsprechen im Allgemeinen dem Inhalt einer WHERE-Klausel. Sie können mehrere Bedingungen mithilfe der logischen Operatoren **AND**, **OR**und **NOT**verbinden.  
  
 In geschachtelten Tabellen können Sie auch die Operatoren **EXISTS** und **NOT EXISTS** verwenden. Eine **EXISTS** -Bedingung ergibt **true** , wenn die Unterabfrage mindestens eine Zeile zurückgibt. Dies ist hilfreich, wenn Sie das Modell auf Fälle beschränken möchten, die in der geschachtelten Tabelle einen bestimmten Wert enthalten: beispielsweise Kunden, die einen Artikel mindestens ein Mal gekauft haben.  
  
 Eine **NOT EXISTS** -Bedingung ergibt **true** , wenn die in der Unterabfrage angegebene Bedingung nicht vorhanden ist. Ein Beispiel dafür ist, wenn Sie das Modell auf Kunden beschränken möchten, die einen bestimmten Artikel noch nie gekauft haben.  
  
 Die allgemeine Syntax lautet wie folgt:  
  
```  
<filter>::=<predicate list>  | ( <predicate list> )  
<predicate list>::= <predicate> | [<logical_operator> <predicate list>]   
<logical_operator::= AND| OR  
<predicate>::= NOT <predicate>|( <predicate> ) <avPredicate> | <nestedTablePredicate> | ( <predicate> )   
<avPredicate>::= <columnName> <operator> <scalar> | <columnName> IS [NOT] NULL  
<operator>::= = | != | <> | > | >= | < | <=  
<nestedTablePredicate>::= EXISTS (<subquery>)  
<subquery>::=SELECT * FROM <columnName>[ WHERE  <predicate list> ]  
```  
  
 *filter*  
 Enthält ein oder mehrere Prädikate, die durch logische Operatoren verbunden werden.  
  
 *predicate list*  
 Ein oder mehrere gültige Filterausdrücke, die durch logische Operatoren getrennt werden.  
  
 *columnName*  
 Der Name einer Miningstrukturspalte.  
  
 logical operator  
 **AND**, **OR**, **NOT**  
  
 *avPredicate*  
 Filterausdruck, der nur auf skalare Miningstrukturspalten angewendet werden kann. Ein *avPredicate* -Ausdruck kann sowohl in Modellfiltern als auch in geschachtelten Tabellenfiltern verwendet werden.  
  
 Ein Ausdruck, der einen der folgenden Operatoren verwendet, kann nur auf eine kontinuierliche Spalte angewendet werden. :  
  
-   **\<** (kleiner als)  
  
-   **>** (größer als)  
  
-   **>=** (größer oder gleich)  
  
-   **\<=** (kleiner oder gleich)  
  
> [!NOTE]  
>  Unabhängig vom Datentyp können diese Operatoren nicht auf eine Spalte vom Typ **Discrete**, **Discretized**oder **Key**angewendet werden.  
  
 Ein Ausdruck, der einen der folgenden Operatoren verwendet, kann nur auf eine Spalte vom Typ Continuous, Discrete, Discretized oder Key angewendet werden.  
  
-   **=** (gleich)  
  
-   **!=** (ungleich)  
  
-   **IS NULL**  
  
 Wenn das Argument *avPredicate*für eine diskretisierte Spalte gilt, kann der im Filter verwendete Wert ein beliebiger Wert in einem bestimmten Bucket sein.  
  
 Mit anderen Worten, Sie definieren die Bedingung nicht als `AgeDisc = ’25-35’`, sondern Sie berechnen und verwenden einen Wert aus diesem Intervall.  
  
 Beispiel:  `AgeDisc = 27`  bedeutet jeden Wert im gleichen Intervall wie 27, in diesem Fall also 25–35.  
  
 *nestedTablePredicate*  
 Filterausdruck, der für eine geschachtelte Tabelle gilt. Kann nur in Modellfiltern verwendet werden.  
  
 Das Unterabfrageargument *nestedTablePredicate*kann nur auf eine Spalten in einer Tabellenminingstruktur angewendet werden.  
  
 Unterabfrage  
 Eine SELECT-Anweisung, gefolgt von einem gültigen Prädikat oder einer Liste von Prädikaten.  
  
 Alle Prädikate müssen dem in *avPredicates*beschriebenen Typ entsprechen. Außerdem können die Prädikate nur auf Spalten verweisen, die in der aktuellen geschachtelten Tabelle enthalten sind, die durch das Argument *columnName*angegeben wird.  
  
### <a name="limitations-on-filter-syntax"></a>Einschränkungen der Filtersyntax  
 Für Filter gelten die folgenden Einschränkungen:  
  
-   Ein Filter kann nur einfache Prädikate enthalten. Dazu gehören mathematische Operatoren, Skalare und Spaltennamen.  
  
-   Benutzerdefinierte Funktionen werden in der Filtersyntax nicht unterstützt.  
  
-   Nichtboolesche Operatoren, z. B. das Plus oder das Minuszeichen, werden in der Filtersyntax nicht unterstützt.  
  
## <a name="examples-of-filters"></a>Beispiele für Filter  
 In den folgenden Beispielen wird die Anwendung von Filtern auf ein Miningmodell veranschaulicht. Wenn Sie den Filterausdruck unter Verwendung von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]erstellen, sehen Sie im Fenster **Eigenschaft** und im Bereich **Ausdruck** des Dialogfelds Filter nur die Zeichenfolge, die nach den WITH FILTER-Schlüsselwörtern angezeigt wird. Hier wird die Definition der Miningstruktur eingefügt, um den Spaltentyp und die Spaltenverwendung verständlicher zu machen.  
  
###  <a name="bkmk_Ex1"></a> Beispiel 1: Typische Filterung auf Fallebene  
 Dieses Beispiel zeigt einen einfachen Filter, der die im Modell verwendeten Fälle auf Kunden mit dem Beruf Architekt und einem Alter von über 30 Jahren einschränkt.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_1  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH FILTER (Age > 30 AND Occupation=’Architect’)  
```  
  
  
###  <a name="bkmk_Ex2"></a> Beispiel 2: Filterung auf Fallebene unter Verwendung von Attributen in geschachtelten Tabellen  
 Wenn Ihre Miningstruktur geschachtelte Tabellen enthält, können Sie entweder auf das Vorhandensein eines Werts in einer geschachtelten Tabelle filtern oder auf Zeilen in der geschachtelten Tabelle, die einen bestimmten Wert enthalten. Dieses Beispiel schränkt die für das Modell verwendeten Fälle auf Kunden ein, die über 30 Jahre alt sind und mindestens einen Einkauf getätigt haben, der Milch enthielt.  
  
 Dieses Beispiel zeigt, dass der Filter nicht nur Spalten zu verwenden braucht, die im Modell enthalten sind. Die geschachtelte Tabelle **Products** ist Bestandteil der Miningstruktur, ist jedoch nicht im Miningmodell enthalten. Sie können jedoch auf Werte und Attribute in der geschachtelten Tabelle filtern. Um die Details dieser Fälle anzuzeigen, muss Drillthrough aktiviert werden.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_2  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH DRILLTHROUGH,   
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’)  
)  
```  
  
  
###  <a name="bkmk_Ex3"></a> Beispiel 3: Filterung auf Fallebene unter Verwendung von mehreren Attributen in geschachtelten Tabellen  
 Dieses Beispiel zeigt einen dreiteiligen Filter: Eine Bedingung gilt für die Falltabelle, eine andere Bedingung für ein Attribut in der geschachtelten Tabelle und eine weitere Bedingung für einen bestimmten Wert in einer der geschachtelten Tabellenspalten.  
  
 Die erste Bedingung im Filter, `Age > 30`, gilt für eine Spalte in der Falltabelle. Die übrigen Bedingungen gelten für die geschachtelte Tabelle.  
  
 Die zweite Bedingung, `EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’`, überprüft, ob in der geschachtelten Tabelle mindestens ein Einkauf vorhanden ist, der Milch enthält. Die dritte Bedingung, `Quantity>=2`, bedeutet, dass der Kunde in einer Transaktion mindestens zwei Einheiten Milch gekauft haben muss.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_3  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
)  
)  
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’  AND Quantity >= 2)   
)  
```  
  
  
###  <a name="bkmk_Ex4"></a> Beispiel 4: Filterung auf Fallebene unter Verwendung der Abwesenheit von Attributen in der geschachtelten Tabelle  
 Dieses Beispiel zeigt, wie Fälle auf Kunden beschränkt werden, die einen bestimmten Artikel nicht gekauft haben, indem auf das Nichtvorhandensein eines Attributs in der geschachtelten Tabelle gefiltert wird. In diesem Beispiel wird das Modell so eingerichtet, dass damit Kunden ermittelt werden können, die älter als 30 Jahre sind und noch nie Milch gekauft haben.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_4  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName  
)  
)  
FILTER (Age > 30 AND NOT EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’) )  
```  
  
  
###  <a name="bkmk_Ex5"></a> Beispiel 5: Filterung unter Verwendung von mehreren Werten in geschachtelten Tabellen  
 Dieses Beispiel soll das Filtern von geschachtelten Tabellen veranschaulichen. Der Filter für geschachtelte Tabellen wird nach dem Fallfilter angewendet und schränkt nur Zeilen in geschachtelten Tabellen ein.  
  
 Dieses Modell kann mehrere Fälle mit leeren geschachtelten Tabellen enthalten, da EXISTS nicht angegeben ist.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_5  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName=’Milk’ OR ProductName=’bottled water’)  
)  
WITH DRILLTHROUGH  
```  
  
  
###  <a name="bkmk_Ex6"></a> Beispiel 6: Filterung unter Verwendung von Attributen in geschachtelten Tabellen und EXISTS  
 In diesem Beispiel beschränkt der Filter für die geschachtelte Tabelle die Zeilen auf solche, die entweder Milch oder Wasser in Flaschen enthalten. Anschließend werden die Fälle im Modell mithilfe einer **EXISTS** -Anweisung eingeschränkt. Dies stellt sicher, dass die geschachtelte Tabelle nicht leer ist.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_6  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName=’Milk’ OR ProductName=’bottled water’)  
)  
FILTER (EXISTS (Products))  
```  
  
  
###  <a name="bkmk_Ex7"></a> Beispiel 7: Komplexe Filterkombinationen  
 Das Szenario für dieses Modell ähnelt dem von Beispiel 4, ist jedoch wesentlich komplexer. Die geschachtelte Tabelle **ProductsOnSale**besitzt die Filterbedingung `(OnSale)` . Dies bedeutet, dass der Wert von **OnSale** für das in **ProductName** aufgelistete Produkt **TRUE**sein muss. Hier ist **OnSale** eine Strukturspalte.  
  
 Der zweite Teil des Filters für **ProductsNotOnSale**wiederholt diese Syntax, filtert jedoch nach Produkten, bei denen der Wert für **OnSale** gilt: **not true**`(!OnSale)`.  
  
 Schließlich werden die Bedingungen kombiniert und der Falltabelle wird eine weitere Einschränkung hinzugefügt. Das Ergebnis ist die Vorhersage von Käufen der Produkte in der Liste **ProductsNotOnSale** auf der Grundlage der Fälle in der Liste **ProductsOnSale** für alle Kunden mit einem Alter von über 25.  
  
 `ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_7`  
  
 `(`  
  
 `CustomerId,`  
  
 `Age,`  
  
 `Occupation,`  
  
 `MaritalStatus,`  
  
 `ProductsOnSale`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(OnSale),`  
  
 `ProductsNotOnSale PREDICT ONLY`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(!OnSale)`  
  
 `)`  
  
 `WITH DRILLTHROUGH,`  
  
 `FILTER (EXISTS (ProductsOnSale) AND EXISTS(ProductsNotOnSale) AND Age > 25)`  
  
  
###  <a name="bkmk_Ex8"></a> Beispiel 8: Filtern unter Verwendung von Datumsangaben  
 Sie können Eingabespalten genau wie alle anderen Daten nach Datumsangaben filtern. In einer Spalte des Typs Datum/Uhrzeit enthaltene Datumsangaben sind kontinuierliche Werte. Sie können daher mit Operatoren wie Größer als (>) oder Kleiner als (<) einen Datumsbereich festlegen. Wenn die Datenquelle Datumsangaben nicht durch einen kontinuierlichen Datentyp, sondern als Einzel- oder Textwerte darstellt, können Sie nicht nach einem Datumsbereich filtern, sondern müssen einzelne Werte angeben.  
  
 Sie können jedoch keinen Filter für die Datumsspalte in einem Zeitreihenmodell erstellen, wenn die für den Filter verwendete Datumsspalte gleichzeitig die Schlüsselspalte für das Modell ist. Dies liegt daran, dass die Datumsspalte in Zeitreihenmodellen und Sequenzclustermodellen als eine Spalte vom Typ **KeyTime** oder **KeySequence**verarbeitet werden kann.  
  
 Wenn Sie in einem Zeitreihenmodell nach kontinuierlichen Datumsangaben filtern müssen, können Sie in der Miningstruktur eine Kopie der Spalte erstellen und das Modell unter Verwendung der neuen Spalte filtern.  
  
 Der folgende Ausdruck stellt beispielsweise einen Filter für eine Datumsspalte von Typ **Continuous** dar, die dem Modell für die Planung hinzugefügt wurde.  
  
 `=[DateCopy] > '12:31:2003:00:00:00'`  
  
> [!NOTE]  
>  Beachten Sie, dass sich alle zusätzlichen Spalten, die Sie dem Modell hinzufügen, auf die Ergebnisse auswirken können. Wenn Sie nicht möchten, dass die Spalte zur Berechnung der Reihe verwendet wird, sollten Sie die Spalte daher nur der Miningstruktur und nicht dem Modell hinzufügen. Sie können auch das Modellflag für die Spalte auf **PredictOnly** oder **Ignore**festlegen. Weitere Informationen finden Sie unter [Modellierungsflags &#40;Data Mining&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md).  
  
 Für andere Modelltypen können Sie Datumsangaben ebenso wie jede andere Spalte als Eingabekriterien oder Filterkriterien verwenden. Wenn Sie jedoch einen bestimmten Grad an Granularität benötigen, die von einem **Continuous** -Datentyp nicht unterstützt wird, können Sie einen abgeleiteten Wert in der Datenquelle erstellen, indem Sie mithilfe von Ausdrücken die Einheit extrahieren, die zur Filterung und Analyse verwendet werden soll.  
  
> [!WARNING]  
>  Wenn Sie Datumsangaben als Filterkriterien angeben, müssen Sie unabhängig vom Datumsformat für das aktuelle Betriebssystem das folgende Format verwenden: `mm/dd/yyyy`. Jedes andere Format führt zu einem Fehler.  
  
 Wenn Sie beispielsweise die Callcenterergebnisse filtern möchten, um nur Wochenenden anzuzeigen, können Sie in der Datenquellensicht einen Ausdruck erstellen, der den Namen des Wochentags für jedes Datum extrahiert, und dann diesen Wert als Eingabe oder als diskreten Wert für die Filterung verwenden. Bedenken Sie jedoch, dass sich wiederholende Werte auf das Modell auswirken können. Sie sollten deshalb nicht die Datumsspalte und den abgeleiteten Wert, sondern nur eine der Spalten verwenden.  
  
  
## <a name="see-also"></a>Siehe auch  
 [Filter für Miningmodelle &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [Tests und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  

