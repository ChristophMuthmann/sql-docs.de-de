---
title: SELECT FROM &lt;Modell&gt; PREDICTION JOIN (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PREDICTION
- PREDICTION_JOIN
- SELECT
- join
- FROM
- PREDICTION JOIN
dev_langs:
- DMX
helpviewer_keywords:
- prediction joins [DMX]
- PREDICTION JOIN statement
- natural prediction joins [DMX]
- open query predictions
- singleton query predictions [DMX]
- SELECT FROM <model> PREDICTION JOIN statement
ms.assetid: 7ca37fec-4a50-4d79-b1d6-1c7c12176946
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 315ab1f6f066cad8a0a6652bac5fb24617ac29c9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>SELECT FROM &lt;Modell&gt; PREDICTION JOIN (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Verwendet ein Miningmodell dazu, die Status von Spalten vorherzusagen, die zu einer externen Datenquelle gehören. Die **PREDICTION JOIN** -Anweisung gleicht jeden Fall aus der Quellabfrage mit dem Modell.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <select expression list>   
FROM <model> | <sub select> [NATURAL] PREDICTION JOIN   
<source data query> [ON <join mapping list>]   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumente  
 *n*  
 Optional. Eine ganze Zahl, die angibt, wie viele Zeilen zurückgegeben werden sollen.  
  
 *Select-Ausdrucksliste*  
 Eine durch Trennzeichen getrennte Liste mit Spaltenbezeichnern und Ausdrücken, die aus dem Miningmodell abgeleitet sind.  
  
 *model*  
 Ein Modellbezeichner.  
  
 *Sub auswählen*  
 Eine eingebettete SELECT-Anweisung.  
  
 *quelldatenabfrage*  
 Die Quellabfrage.  
  
 *Liste der JOIN-Zuordnung*  
 Optional. Ein logischer Ausdruck, in dem Spalten aus dem Modell mit Spalten aus der Quellabfrage verglichen werden.  
  
 *Bedingungsausdruck*  
 Optional. Eine Bedingung, die die Werte einschränkt, die für die Spaltenliste zurückgegeben werden.  
  
 *expression*  
 Optional. Ein Ausdruck, der einen Skalarwert zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die ON-Klausel definiert die Zuordnung zwischen den Spalten aus der Quellabfrage und den Spalten aus dem Miningmodell. Diese Zuordnung wird verwendet, um Spalten aus der Quellabfrage auf Spalten im Miningmodell zu richten, sodass die Spalten als Eingaben verwendet werden können, um die Vorhersagen zu erstellen. Spalten in der \< *Zuordnung Verknüpfungsliste*> stehen mit einem Gleichheitszeichen (=), wie im folgenden Beispiel gezeigt:  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 Wenn Sie in der ON-Klausel eine geschachtelte Tabelle binden, müssen Sie die Schlüsselspalte mit Nichtschlüsselspalten verknüpfen, damit der Algorithmus ermitteln kann, zu welchem Fall der Datensatz der geschachtelten Spalte gehört.  
  
 Die Quellabfrage für den PREDICTION JOIN kann eine Tabellen- oder eine SINGLETON-Abfrage sein.  
  
 Sie können angeben, dass Vorhersagefunktionen, die einen Tabellenausdruck in keine Zurückgeben der \< *select-Ausdrucksliste*> und der \< *Bedingung Ausdruck*>.  
  
 **NATÜRLICHE PREDICTION JOIN** ordnet automatisch zusammen Spaltennamen aus der Quellabfrage, die Spaltennamen im Modell entsprechen. Bei Verwendung von **natürliche PREDICTION**, können Sie die ON-Klausel auslassen.  
  
 Die WHERE-Bedingung kann nur auf vorhersagbare Spalten oder verknüpfte Spalten angewendet werden.  
  
 Die ORDER BY-Klausel lässt nur eine einzelne Spalte als Argument zu, d. h. Sie können nicht nach mehreren Spalten sortieren.  
  
## <a name="example-1-singleton-query"></a>Beispiel 1: SINGLETON-Abfrage  
 Im folgenden Beispiel wird erläutert, wie eine Abfrage erstellt wird, die in Echtzeit vorhersagt, ob eine bestimmte Person ein Fahrrad kauft. In dieser Abfrage werden die Daten nicht in einer Tabelle oder einer anderen Datenquelle gespeichert, sondern direkt in die Abfrage eingegeben. Die Person in der Abfrage hat folgende Merkmale:  
  
-   35 Jahre alt  
  
-   Besitzt ein Haus  
  
-   Besitzt zwei Autos  
  
-   Hat zwei Kinder, die zu Hause leben  
  
 Das TM Decision Tree-Miningmodell und die bekannten Merkmalen über das Subjekt verwenden, die Abfrage gibt einen booleschen Wert, der angibt, ob die Person das Fahrrad und einen Satz von tabellarischen zurückgegebenen Werte gekauft haben die ["PredictHistogram" &#40;DMX &#41; ](../dmx/predicthistogram-dmx.md) Funktion, die beschreiben, wie die Vorhersage getroffen wurde.  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  PredictHistogram([Bike Buyer])  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 35 AS [Age],  
  '5-10 Miles' AS [Commute Distance],  
  '1' AS [House Owner Flag],  
  2 AS [Number Cars Owned],  
  2 AS [Total Children]) AS t  
```  
  
## <a name="example-2-using-openquery"></a>Beispiel 2: Verwenden von OPENQUERY  
 Im folgende Beispiel wird gezeigt, wie eine batchvorhersageabfrage erstellt wird, wird mit einer Liste potenzieller Kunden, die in einem externen Dataset gespeichert. Da die Tabelle einer Datenquellensicht gehört, die in einer Instanz von definiert wurde [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], können Sie die Abfrage [OPENQUERY](../dmx/source-data-query-openquery.md) zum Abrufen der Daten. Da die Namen der Spalten in der Tabelle von denen in das Miningmodell unterscheiden, sind die **ON** -Klausel verwendet werden muss, um die Spalten in der Tabelle den Spalten im Modell zuzuordnen.  
  
 Die Abfrage gibt Folgendes zurück: den Vor- und Nachnamen jeder Person in der Tabelle sowie eine boolesche Spalte, die angibt, ob die Personen voraussichtlich ein Fahrrad kauften, dabei bedeutet 0 „wird vermutlich kein Fahrrad kaufen“ und 1 „wird vermutlich ein Fahrrad kaufen“. Die letzte Spalte enthält die Wahrscheinlichkeit für das vorhergesagte Ergebnis.  
  
```  
SELECT  
  t.[LastName],  
  t.[FirstName],  
  [TM Decision Tree].[Bike Buyer],  
  PredictProbability([Bike Buyer])  
From  
  [TM Decision Tree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [LastName],  
      [FirstName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [Education],  
      [Occupation],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
  [TM Decision Tree].[Gender] = t.[Gender] AND  
  [TM Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM Decision Tree].[Total Children] = t.[TotalChildren] AND  
  [TM Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM Decision Tree].[Education] = t.[Education] AND  
  [TM Decision Tree].[Occupation] = t.[Occupation] AND  
  [TM Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
```  
  
 Um das Dataset auf die Kunden zu beschränken, die voraussichtlich ein Fahrrad kaufen werden, und um die Liste anschließend nach Kundennamen zu sortieren, können Sie dem vorstehenden Beispiel eine WHERE-Klausel und eine ORDER BY-Klausel hinzufügen.  
  
```  
WHERE [BIKE Buyer]  
ORDER BY [LastName] ASC  
```  
  
## <a name="example-3-predicting-associations"></a>Beispiel 3: Vorhersagen von Zuordnungen  
 Das folgende Beispiel zeigt, wie eine Vorhersage durch Verwenden eines Modells erstellt wird, das über den [!INCLUDE[msCoName](../includes/msconame-md.md)] Association-Algorithmus erstellt wurde. Vorhersagen über ein Zuordnungsmodell können verwendet werden, um zugehörige Produkte zu empfehlen. Die folgende Abfrage gibt beispielsweise die drei Produkte zurück, die höchstwahrscheinlich zusammen gekauft werden:  
  
-   Mountain Bottle Cage  
  
-   Mountain Tire Tube  
  
-   Mountain-200  
  
 Die [Predict &#40;DMX&#41; ](../dmx/predict-dmx.md) Funktion ist polymorph und kann mit allen Modelltypen verwendet werden. Sie verwenden den Wert3 als Argument für die Funktion, um die Anzahl der Elemente zu begrenzen, die von der Abfrage zurückgegeben werden. Die **wählen** Liste, die die NATURAL PREDICTION JOIN-Klausel folgt bereitstellt, die Werte, die als Eingabe für die Vorhersage verwendet.  
  
```  
SELECT FLATTENED  
  PREDICT([Association].[v Assoc Seq Line Items], 3)  
FROM  
  [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
  UNION SELECT 'Mountain Tire Tube' AS [Model]  
  UNION SELECT 'Mountain-200' AS [Model]) AS [v Assoc Seq Line Items ]) AS t  
```  
  
 Beispielergebnisse:  
  
|Expression.Model|  
|----------------------|  
|HL Mountain Tire|  
|Water Bottle|  
|Fender Set – Mountain|  
  
 Da die Spalte, die das vorhersagbare Attribut `[v Assoc Seq Line Items]` enthält, eine Tabellenspalte ist, gibt die Abfrage eine einzelne Spalte zurück, die eine geschachtelte Tabelle enthält. Die Spalte der geschachtelten Tabelle erhält standardmäßig den Namen `Expression`. Wenn Ihr Anbieter keine hierarchischen Rowsets unterstützt, können Sie mithilfe der **FLATTENED** Schlüsselwort, wie im folgenden Beispiel gezeigt, um die Ergebnisse übersichtlicher zu gestalten.  
  
## <a name="see-also"></a>Siehe auch  
 [WÄHLEN SIE &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen & #40; DMX & #41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
