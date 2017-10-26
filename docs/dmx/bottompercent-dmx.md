---
title: BottomPercent (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BOTTOMPERCENT
dev_langs:
- DMX
helpviewer_keywords:
- BottomPercent function
ms.assetid: 984eb18a-c55c-49f3-81fa-918dfc983174
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cdc60cbc61d0c84953f2e80a5896dbd8465bdb8a
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="bottompercent-dmx"></a>BottomPercent (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt in aufsteigender Rangreihenfolge die untersten Zeilen einer Tabelle zurück, deren kumulativer Gesamtwert mindestens so groß wie ein angegebener Prozentsatz ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BottomPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="arguments"></a>Argumente  
 *\<Tabellenausdruck >*  
 Der Name der geschachtelten Tabelle oder des Tabellenwertausdrucks.  
  
 *\<Rank Expression >*  
 Eine Spalte in der geschachtelten Tabelle oder ein Ausdruck, der eine Spalte auswertet.  
  
 *\<% >*  
 Ein doppelter Wert, der den gesamten Zielprozentsatz angibt.  
  
## <a name="result-type"></a>Ergebnistyp  
 Tabelle  
  
## <a name="remarks"></a>Hinweise  
 Die **BottomPercent** Funktion gibt die untersten Zeilen in aufsteigender Rangreihenfolge zurück. Der Rang basiert auf dem ausgewerteten Wert des der \<rank Expression >-Arguments für jede Zeile so, dass die Summe aus der \<rank Expression > Werte ist mit mindestens der Prozentsatz sein muss, die von angegeben wird die \<Prozent > Argument. **BottomPercent** die kleinste Anzahl von Elementen gibt mögliche zurück, denen der angegebene Prozentwert erreicht.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel erstellt eine Vorhersageabfrage für das Association-Modell, die Sie, in erstellt der [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Um zu verstehen, wie die BottomPercent funktioniert, ist es möglicherweise hilfreich, zunächst eine Vorhersageabfrage auszuführen, die lediglich die geschachtelte Tabelle zurückgibt.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  In diesem Beispiel enthält der als Eingabe bereitgestellte Wert ein einzelnes Anführungszeichen und muss daher mit Escapezeichen versehen werden, indem ihm ein weiteres einzelnes Anführungszeichen vorangestellt wird. Wenn Sie über die Syntax zum Einfügen von Escapezeichen nicht sicher sind, können Sie den Generator für Vorhersageabfragen verwenden, um die Abfrage zu erstellen. Wenn Sie den Wert aus der Dropdownliste auswählen, wird das erforderliche Escapezeichen automatisch eingefügt. Weitere Informationen finden Sie unter [Erstellen einer Singleton-Abfrage im Data Mining-Designer](../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md).  
  
 Beispielergebnisse:  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patchkit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Fender Set – Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
  
 Die BottomPercent-Funktion verwendet die Ergebnisse dieser Abfrage und gibt die Zeilen mit kleinsten Werten ergeben, die den angegebenen Prozentsatz.  
  
```  
SELECT   
BottomPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Das erste Argument für die BottomPercent-Funktion ist der Name einer Tabellenspalte. In diesem Beispiel wird die geschachtelte Tabelle zurückgegeben, durch die Predict-Funktion aufrufen und das INCLUDE_STATISTICS-Argument verwenden.  
  
 Die BottomPercent-Funktion das zweite Argument ist die Spalte in der geschachtelten Tabelle, die Sie zum Sortieren der Ergebnisse verwenden. In diesem Beispiel gibt die INCLUDE_STATISTICS-Option die Spalten $SUPPORT, $PROBABILTY und $ADJUSTED PROBABILITY zurück. In diesem Beispiel wird $SUPPORT verwendet, da diese Werte keine Bruchteile besitzen und daher leichter zu überprüfen sind.  
  
 Das dritte Argument die BottomPercent-Funktion gibt den Prozentsatz als Double-Wert. Geben Sie 50 ein, um die Zeilen zu erhalten, die die unteren 50 Prozent der Unterstützungswerte darstellen.  
  
 Beispielergebnisse:  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Fender Set – Mountain|1415|0.095100477|0.090718432|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
  
 **Hinweis** in diesem Beispiel wird nur bereitgestellt, um die Verwendung von BottomPercent veranschaulichen. Je nach Größe des Datasets kann die Ausführung dieser Abfrage lange dauern.  
  
> [!WARNING]  
>  Die MDX-Funktionen für TOPPERCENT und BOTTOMPERCENT können unerwartete Ergebnisse generieren, wenn die Werte zur Berechnung des Prozentsatzes negative Zahlen enthalten. Dieses Verhalten wirkt sich nicht auf die DMX-Funktionen aus. Weitere Informationen finden Sie unter [BottomPercent &#40; MDX &#41; ](../mdx/bottompercent-mdx.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)  
  
  

