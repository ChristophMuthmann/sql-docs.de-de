---
title: SELECT-Anweisung (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: SELECT
dev_langs: kbMDX
helpviewer_keywords:
- SELECT statement [MDX]
- cubes [Analysis Services], SELECT statement
ms.assetid: c0a57214-aa3f-44ce-a369-660c69746f34
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b1cf2d78fcb8b275a899be437b85b643c2f5b6af
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-manipulation---select"></a>Datenbearbeitung für MDX - SELECT
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ruft Daten aus einem angegebenen Cube ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
[ WITH <SELECT WITH clause>   
   [ , <SELECT WITH clause>...n ]   
]   
SELECT   
     [ *   
    | ( <SELECT query axis clause>   
                  [ , <SELECT query axis clause>,...n ]   
            )   
            ]  
FROM   
   <SELECT subcube clause>   
      [ <SELECT slicer axis clause> ]  
      [ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
     ( CELL CALCULATION <CREATE CELL CALCULATION body clause> )   
   | ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>)   
   | ( SET <CREATE SET body clause>)  
   | ( MEASURE = <measure body clause> )  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression  
   [ <SELECT dimension property list clause> ]   
      ON   
            Integer_Expression   
       | AXIS(Integer)   
       | COLUMNS   
       | ROWS   
       | PAGES   
       | SECTIONS   
       | CHAPTERS   
  
<SELECT subcube clause> ::=  
      Cube_Name   
   | [NON VISUAL] (SELECT   
                  [ *   
       | ( <SELECT query axis clause> [ ,   
           <SELECT query axis clause>,...n ] )   
         ]   
            FROM   
         <SELECT subcube clause>   
         <SELECT slicer axis clause> )  
  
<SELECT slicer axis clause> ::=   
      WHERE Tuple_Expression  
  
<SELECT cell property list clause> ::=   
   [ CELL ] PROPERTIES CellProperty_Name   
      [ , CellProperty_Name,...n ]  
  
<SELECT dimension property list clause> ::=  
   [DIMENSION] PROPERTIES   
      (DimensionProperty_Name   
         [,DimensionProperty_Name,...n ] )   
    | (LevelProperty_Name   
         [, LevelProperty_Name,...n ] )   
    | (MemberProperty_Name   
         [, MemberProperty_Name,...n ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Integer*  
 Eine ganze Zahl zwischen 0 und 127.  
  
 *Cube_Name*  
 Eine gültige Zeichenfolge, die einen Cubenamen bereitstellt.  
  
 *Tuple_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Tupel zurückgibt.  
  
 *CellProperty_Name*  
 Eine gültige Zeichenfolge, die eine Zelleneigenschaft darstellt.  
  
 *DimensionProperty_Name*  
 Eine gültige Zeichenfolge, die eine Dimensionseigenschaft darstellt.  
  
 *LevelProperty_Name*  
 Eine gültige Zeichenfolge, die eine Ebeneneigenschaft darstellt.  
  
 *MemberProperty_Name*  
 Eine gültige Zeichenfolge, die eine Elementeigenschaft darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Der `<SELECT slicer axis clause>`-Ausdruck muss Elemente in anderen Dimensionen und Hierarchien enthalten als denen, auf die in den angegebenen `<SELECT query axis clause>`-Ausdrücken verwiesen wird.  
  
 Wird ein Attribut im Cube in den angegebenen `<SELECT query axis clause>`-Ausdrücken und dem `<SELECT slicer axis clause>`-Wert ausgelassen, wird das Standardelement des Attributs implizit der Slicer-Achse hinzugefügt.  
  
 Mit der NON VISUAL-Option in der untergeordneten SELECT-Anweisung können Sie Member durch Filtern ausschließen und gleichzeitig die tatsächlichen Gesamtwerte anstelle der gefilterten Gesamtwerte beibehalten. So können Sie die besten zehn Verkaufswerte (Personen/Produkte/Regionen) abfragen und die tatsächliche Summe aller Verkaufswerte für alle abgefragten Member beibehalten und nicht den Gesamtwert der Verkäufe für die zurückgegebenen besten zehn. Weitere Informationen finden Sie unten in den Beispielen.  
  
 Berechnete Elemente können in eingeschlossen werden \<SELECT-abfrageachsenklausel > Wenn die Verbindung geöffnet wurde mit dem Verbindungszeichenfolgenparameter *Unterabfragen = 1*; finden Sie unter [unterstützten XMLA-Eigenschaften &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) und <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> für die Verwendung von Parametern. Es wird ein Beispiel für berechnete Elemente in untergeordneten SELECT-Anweisungen bereitgestellt.  
  
## <a name="autoexists"></a>Autoexists  
 Wenn mindestens zwei Attribute der Dimension in einer SELECT-Anweisung verwendet werden, wertet Analysis Services die Ausdrücke der Attribute aus, damit die Elemente dieser Attribute ordnungsgemäß so beschränkt werden, dass sie die Kriterien aller anderen Attribute erfüllen. Angenommen, Sie arbeiten mit Attributen der Geography-Dimension. Wenn Sie einen Ausdruck, die alle Elemente der City-Attribut und ein anderer Ausdruck die Einschränkung Elemente des Country-Attributs auf alle Länder in Europa zurückgibt verwenden, wird dies führen, dass es nur die Orte, die auf Länder in Europa gehören Europas City-Elemente. Diese Eigenschaft von Analysis Services wird als Autoexists bezeichnet und gilt nur für Attribute in der gleichen Dimension. Autoexists gilt nur für Attribute der gleichen Dimension, denn es versucht zu verhindern, dass die in einem Attributausdruck ausgeschlossenen Dimensionsdatensätze von den anderen Attributausdrücken eingeschlossen werden. Autoexists kann auch als resultierende Schnittmenge der unterschiedlichen Attributausdrücke in den Dimensionsdatensätzen bezeichnet werden. Finden Sie unter den folgenden Beispielen unten:  
  
 `//Obtain the Top 10 best reseller selling products by Name`  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 Das Resultset lautet:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**14.356.699,36 €**|**19.012,71 €**|**0,13 %**|  
|**Road-250**|**9.377.457,68 €**|**4.032,47 €**|**0,04 %**|  
|**Mountain-100**|**8.568.958,27 €**|**139.393,27 €**|**1,63 %**|  
|**Road-650**|**7.442.141,81 €**|**39.698,30 €**|**0,53 %**|  
|**Touring-1000**|**6.723.794,29 €**|**166.144,17 €**|**2,47 %**|  
|**Road-550-W**|**3.668.383,88 €**|**1.901,97 €**|**0,05 %**|  
|**Road-350-W**|**3.665.932,31 €**|**20.946,50 €**|**0,57 %**|  
|**HL Mountain Frame**|**3.365.069,27 €**|**174,11 €**|**0,01 %**|  
|**Road-150**|**2.363.805,16 €**|**0,00 €**|**0,00 %**|  
|**Touring-3000**|**2.046.508,26 €**|**79.582,15 €**|**3,89 %**|  
  
 Die erhaltene Produktgruppe ist offenbar die gleiche wie Preferred10Products. Die Gruppe Preferred10Products wird deshalb überprüft:  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 Laut den folgenden Ergebnissen sind beide Gruppen (Top10SellingProducts, Preferred10Products) identisch.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**14.356.699,36 €**|**19.012,71 €**|**0,13 %**|  
|**Road-250**|**9.377.457,68 €**|**4.032,47 €**|**0,04 %**|  
|**Mountain-100**|**8.568.958,27 €**|**139.393,27 €**|**1,63 %**|  
|**Road-650**|**7.442.141,81 €**|**39.698,30 €**|**0,53 %**|  
|**Touring-1000**|**6.723.794,29 €**|**166.144,17 €**|**2,47 %**|  
|**Road-550-W**|**3.668.383,88 €**|**1.901,97 €**|**0,05 %**|  
|**Road-350-W**|**3.665.932,31 €**|**20.946,50 €**|**0,57 %**|  
|**HL Mountain Frame**|**3.365.069,27 €**|**174,11 €**|**0,01 %**|  
|**Road-150**|**2.363.805,16 €**|**0,00 €**|**0,00 %**|  
|**Touring-3000**|**2.046.508,26 €**|**79.582,15 €**|**3,89 %**|  
  
 In den vorherigen Beispielen haben wir zwei Gruppen erstellt: eine als berechneten Ausdruck und die andere als konstanten Ausdruck. Diese Beispiele veranschaulichen die unterschiedlichen Typen von Autoexists.  
  
 Autoexists können tief oder flach auf die Ausdrücke angewendet werden. Die Standardeinstellung ist tief. Im folgenden Beispiel wird der Begriff "tiefes Autoexists" veranschaulicht. Im Beispiel filtern wir Top10SellingProducts mit dem [Product].[Product Line]-Attribut nach den in der [Mountain]-Gruppe enthaltenen Produkten. Beachten Sie, dass beide Attribute (Slicer und Achse) zur gleichen Dimension [Produkt] gehören.  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `// Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Dadurch ergibt sich folgendes Resultset:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**14.356.699,36 €**|**19.012,71 €**|**0,13 %**|  
|**Mountain-100**|**8.568.958,27 €**|**139.393,27 €**|**1,63 %**|  
|**HL Mountain Frame**|**3.365.069,27 €**|**174,11 €**|**0,01 %**|  
|**Mountain-300**|**1.907.249,38 €**|**876,95 €**|**0,05 %**|  
|**Mountain-500**|**1.067.327,31 €**|**17.266,09 €**|**1,62 %**|  
|**Mountain-400-W**|**592.450,05 €**|**303,49 €**|**0,05 %**|  
|**LL Mountain Frame**|**521.864,42 €**|**252,41 €**|**0,05 %**|  
|**ML Mountain Frame-W**|**482.953,16 €**|**206,95 €**|**0,04 %**|  
|**ML Mountain Frame**|**343.785,29 €**|**161,82 €**|**0,05 %**|  
|**Women's Mountain Shorts**|**260.304,09 €**|**6.675,56 €**|**2,56 %**|  
  
 Das vorherige Resultset enthält sieben Neueinträge für die Liste mit den Top10SellingProducts, und Mountain-200, Mountain-100 sowie HL Mountain Frame wurden an den Anfang der Liste verschoben. Im vorherigen Resultset befanden sich diese drei Werte an verschiedenen Stellen.  
  
 Dies wird als tiefes Autoexists bezeichnet, da die Gruppe Top10SellingProducts so ausgewertet wird, dass die Slicingbedingungen der Abfrage erfüllt werden. Tiefes Autoexists bedeutet, dass alle Ausdrücke so ausgewertet werden, dass nach Anwendung der Slicerausdrücke, der untergeordneten SELECT-Ausdrücke in der Achse usw. der tiefstmögliche Bereich erfüllt ist.  
  
 Eventuell soll es jedoch auch möglich sein, die Analyse der Top10SellingProducts als Entsprechung zu Preferred10Products auszuführen wie im folgenden Beispiel:  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Dadurch ergibt sich folgendes Resultset:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**14.356.699,36 €**|**19.012,71 €**|**0,13 %**|  
|**Mountain-100**|**8.568.958,27 €**|**139.393,27 €**|**1,63 %**|  
|**HL Mountain Frame**|**3.365.069,27 €**|**174,11 €**|**0,01 %**|  
  
 Nach den oben aufgeführten Ergebnissen führt das Slicing zu einem Ergebnis, das nur die Produkte von Preferred10Products enthält, die Teil der Gruppe [Mountain] in [Product].[Product Line] sind. Dies entspricht den Erwartungen, da Preferred10Products ein konstanter Ausdruck ist.  
  
 Dieses Resultset wird auch als flaches Autoexists bezeichnet. Das liegt daran, dass der Ausdruck vor der Slicingklausel ausgewertet wird. Im vorherigen Beispiel war der Ausdruck ein konstanter Ausdruck, damit das Konzept anschaulicher eingeführt werden konnte.  
  
 Das Autoexists-Verhalten kann mit der **Autoexists** -Eigenschaft der Verbindungszeichenfolge auf Sitzungsebene geändert werden. Im folgenden Beispiel wird zunächst eine neue Sitzung geöffnet und dann die *Autoexists=3* -Eigenschaft zur Verbindungszeichenfolge hinzugefügt. Sie müssen eine neue Verbindung öffnen, um das Beispiel ausführen zu können. Sobald die Verbindung mit der Autoexist-Einstellung hergestellt ist, bleibt diese Einstellung bis zum Ende der Verbindung wirksam.  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `//Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Das folgende Resultset zeigt jetzt das flache Verhalten von Autoexists.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**14.356.699,36 €**|**19.012,71 €**|**0,13 %**|  
|**Mountain-100**|**8.568.958,27 €**|**139.393,27 €**|**1,63 %**|  
|**HL Mountain Frame**|**3.365.069,27 €**|**174,11 €**|**0,01 %**|  
  
 Autoexists-Verhalten kann geändert werden, mithilfe der AUTOEXISTS = [1 | 2 | 3]-Parameter in der Verbindungszeichenfolge; finden Sie unter [unterstützten XMLA-Eigenschaften &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) und <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> für die Verwendung von Parametern.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt die Summe aus der `Measures.[Order Quantity]` Elements, aggregiert über die ersten acht Monate des Kalenderjahres 2003 in der `Date` Dimension, aus der **Adventure Works** Cube.  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 Um zu verstehen, **NON VISUAL** im folgende Beispiel wird eine Abfrage der [Adventure Works] zu [Reseller Sales Amount] Abbildungen in einer Tabelle zu erhalten, wobei die Produktkategorien die Spalten und Geschäftstypen der Wiederverkäufer die Zeilen sind. Beachten Sie, dass Gesamtbeträge für Produkte und Wiederverkäufer aufgeführt werden.  
  
 SELECT-Anweisung:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Hierdurch werden folgende Ergebnisse erzielt:  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Bikes**|**Bekleidung**|**Components**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
 Wenn Sie eine Tabelle erstellen möchten, die nur Accessories- und Clothing-Produkte, Value Added Reseller und Warehouse-Wiederverkäufer enthält, wobei die Gesamtbeträge jedoch beibehalten werden, kann dies mit NON VISUAL wie folgt notiert werden:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Hierdurch werden folgende Ergebnisse erzielt:  
  
|||||  
|-|-|-|-|  
||**All Products**|**Accessories**|**Clothing**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
 Wenn Sie eine Tabelle erstellen möchten, in der sichtbare Gesamtwerte für die Spalten, für die Zeilensummen jedoch die tatsächliche Summe aller [Category]-Werten angezeigt werden, geben Sie die folgende Abfrage aus:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 NON VISUAL wird nur auf [Category] angewendet.  
  
 Die oben dargestellte Abfrage führt zu den folgenden Ergebnissen:  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 Im Vergleich zu den vorhergehenden Ergebnissen können Sie feststellen, dass die Zeile [All Resellers] jetzt die Summe der angezeigten Werte für [Value Added Reseller] und [Warehouse] enthält, die Spalte [All Products] hingegen den Gesamtwert aller Produkte anzeigt, einschließlich der nicht sichtbaren Produkte.  
  
 Im folgenden Beispiel wird veranschaulicht, wie Sie mit berechneten Elementen in untergeordneten SELECT-Ausdrücken nach diesen filtern. Um dieses Beispiel reproduzieren können, muss die Verbindung mit dem Verbindungszeichenfolgenparameter hergestellt werden *Unterabfragen = 1*.  
  
 `select Measures.allmembers on 0`  
  
 `from (`  
  
 `Select { [Measures].[Reseller Sales Amount]`  
  
 `, [Measures].[Reseller Total Product Cost]`  
  
 `, [Measures].[Reseller Gross Profit]`  
  
 `, [Measures].[Reseller Gross Profit Margin]`  
  
 `} on 0`  
  
 `from [Adventure Works]`  
  
 `)`  
  
 Die oben dargestellte Abfrage führt zu den folgenden Ergebnissen:  
  
|||||  
|-|-|-|-|  
|Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|Reseller Gross Profit Margin|  
|$80,450,596.98|$79,980,114.38|$470,482.60|0.58%|  
  
## <a name="see-also"></a>Siehe auch  
 [Schlüsselkonzepte in MDX &#40; Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [MDX-Datenbearbeitungsanweisungen &#40; MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [Beschränken die Abfrage mit Abfrage- und Slicerachsen &#40; MDX &#41;](~/analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)  
  
  

