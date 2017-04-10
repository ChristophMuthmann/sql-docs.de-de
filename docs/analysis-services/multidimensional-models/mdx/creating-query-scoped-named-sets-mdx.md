---
title: "Erstellen benannter Mengen im Bereich einer Abfrage (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Benannte Mengen im Bereich einer Abfrage [MDX]"
  - "WITH-Schlüsselwort"
ms.assetid: 78bc1e9a-1bc4-4a5a-ab0b-cf430c8fbfe1
caps.latest.revision: 36
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Erstellen benannter Mengen im Bereich einer Abfrage (MDX)
  Wenn eine benannte Menge nur für eine einzelne MDX-Abfrage (Multidimensional Expressions) benötigt wird, können Sie die benannte Menge mit dem WITH-Schlüsselwort definieren. Eine benannte Menge, die mit dem WITH-Schlüsselwort erstellt wird, ist nach der Ausführung der Abfrage nicht länger vorhanden.  
  
 Wie in diesem Thema erläutert wird, ist die Syntax des WITH-Schlüsselworts sehr flexibel und ermöglicht sogar die Verwendung von Funktionen, um die benannte Menge zu definieren.  
  
> [!NOTE]  
>  Weitere Informationen zu benannten Mengen finden Sie unter [Erstellen von benannten Mengen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-named-sets-in-mdx-mdx.md).  
  
## WITH-Schlüsselwort (Syntax)  
 Verwenden Sie die folgende Syntax, um einer SELECT-Anweisung von MDX das WITH-Schlüsselwort hinzuzufügen:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
   ( SET Set_Identifier AS 'Set_Expression')  
  
```  
  
 In der Syntax des WITH-Schlüsselworts enthält der `Set_Identifier` -Parameter den Alias für die benannte Menge. Der `Set_Expression` -Parameter enthält den Mengenausdruck, auf den der Alias der benannten Menge verweist.  
  
## Beispiel für das WITH-Schlüsselwort  
 Mit der folgenden MDX-Abfrage werden die umgesetzten Stückzahlen (Unit Sales) der verschiedenen Chardonnay- und Chablis-Weine in **FoodMart 2000**(der Beispieldatenbank für Microsoft SQL Server 2000 Analysis Services) untersucht. Diese Abfrage ist zwar relativ einfach bezüglich des Resultsets, für Wartungszwecke ist sie jedoch zu lang und schwer zu handhaben.  
  
```  
SELECT  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]} ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
 Sie können die Wartung der obigen MDX-Abfrage vereinfachen, indem Sie mit dem WITH-Schlüsselwort eine benannte Menge für die Abfrage erstellen. Der folgende Code zeigt, wie mit dem WITH-Schlüsselwort eine benannte Menge, `[ChardonnayChablis]`, erstellt wird und wie durch diese Menge die SELECT-Anweisung verkürzt und ihre Wartung vereinfacht wird.  
  
```  
WITH SET [ChardonnayChablis] AS  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]}  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
### Verwenden von Funktionen zusammen mit dem WITH-Schlüsselwort  
 Sie können zwar jedes Element einer benannten Menge explizit definieren, dies kann jedoch zu einer sehr langen Anweisung führen. Um die Erstellung und Wartung einer benannten Menge zu vereinfachen, können Sie die Elemente mithilfe von MDX-Funktionen definieren.  
  
 Beispielsweise verwendet die folgende MDX-Abfrage die Funktionen [Filter](../../../mdx/filter-mdx.md), [CurrentMember](../../../mdx/currentmember-mdx.md)und [Name](../../../mdx/name-mdx.md) sowie die VBA-Funktion InStr, um die benannte Menge `[ChardonnayChablis]` zu erstellen. Diese Version der benannten Menge `[ChardonnayChablis]` ist identisch mit der explizit definierten Version weiter oben in diesem Thema.  
  
```  
WITH SET [ChardonnayChablis] AS  
   'Filter([Product].Members, (InStr(1, [Product].CurrentMember.Name, "chardonnay") <> 0) OR (InStr(1, [Product].CurrentMember.Name, "chablis") <> 0))'  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
  
```  
  
## Siehe auch  
 [SELECT-Anweisung &#40;MDX&#41;](../Topic/SELECT%20Statement%20\(MDX\).md)   
 [Erstellen benannter Mengen im Bereich einer Sitzung &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/creating-session-scoped-named-sets-mdx.md)  
  
  