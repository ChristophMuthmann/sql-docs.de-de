---
title: BottomSum (DMX) | Microsoft Docs
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
- BOTTOMSUM
dev_langs:
- DMX
helpviewer_keywords:
- BottomSum function
ms.assetid: fd4b0418-f814-4d83-b2fe-850117e1beb7
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8f6d13ccce9bc25f08e1f0f86b026b24ea75d375
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="bottomsum-dmx"></a>BottomSum (DMX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt in aufsteigender Rangreihenfolge die untersten Zeilen einer Tabelle zurück, deren kumulativer Gesamtwert mindestens so groß wie ein angegebener Wert ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BottomSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>Gilt für  
 Ein Ausdruck, der eine Tabelle, wie z. B. zurückgibt eine \<Tabelle Spaltenverweis >, oder eine Funktion, die eine Tabelle zurückgibt.  
  
## <a name="return-type"></a>Rückgabetyp  
 \<Tabellenausdruck >  
  
## <a name="remarks"></a>Hinweise  
 Die **BottomSum** Funktion gibt die untersten Zeilen in aufsteigender Rangreihenfolge zurück. Der Rang basiert auf dem ausgewerteten Wert des der \<rank Expression >-Arguments für jede Zeile so, dass die Summe aus der \<rank Expression > Werte wird mindestens ein Gesamtwert, der angegeben wird die \<Summe > Argument. **BottomSum** die kleinste Anzahl von Elementen gibt mögliche zurück, denen der angegebene Summenwert erreicht.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel erstellt eine Vorhersageabfrage für das Association-Modell, die Sie erstellen, mit der [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Um zu verstehen, wie die BottomSum funktioniert, ist es möglicherweise hilfreich, zunächst eine Vorhersageabfrage auszuführen, die lediglich die geschachtelte Tabelle zurückgibt.  
  
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
  
 Die BottomSum-Funktion verwendet die Ergebnisse dieser Abfrage und gibt den Zeilen mit den niedrigsten Werten ergeben, die die angegebene Anzahl.  
  
```  
SELECT   
BottomSum  
    (  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $PROBABILITY,  
    .1)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Das erste Argument für die BottomSum-Funktion ist der Name einer Tabellenspalte. In diesem Beispiel wird die geschachtelte Tabelle zurückgegeben, durch die Predict-Funktion aufrufen und das INCLUDE_STATISTICS-Argument verwenden.  
  
 Die BottomSum-Funktion das zweite Argument ist die Spalte in der geschachtelten Tabelle, die Sie zum Sortieren der Ergebnisse verwenden. In diesem Beispiel gibt die INCLUDE_STATISTICS-Option die Spalten $SUPPORT, $PROBABILTY und $ADJUSTED PROBABILITY zurück. In diesem Beispiel wird $PROBABILITY zum Zurückgeben von Zeilen verwendet, die mindestens eine Wahrscheinlichkeit von 50 % ergeben.  
  
 Das dritte Argument die BottomSum-Funktion gibt die zielsumme als Double-Wert. Geben Sie .1 ein, um die Zeilen für die Produkte mit der niedrigsten Anzahl zu erhalten, die 10 Prozent Wahrscheinlichkeit ergeben.  
  
 Beispielergebnisse:  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.08…|0.07…|  
|Mountain Bottle Cage|1367|0.09…|0.08…|  
  
 **Hinweis** in diesem Beispiel wird nur bereitgestellt, um die Verwendung von BottomSum veranschaulichen. Je nach Größe des Datasets kann die Ausführung dieser Abfrage lange dauern.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomPercent &#40; DMX &#41;](../dmx/bottompercent-dmx.md)  
  
  

