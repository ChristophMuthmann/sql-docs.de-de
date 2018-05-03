---
title: TopCount (DMX) | Microsoft Docs
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
- TOPCOUNT
dev_langs:
- DMX
helpviewer_keywords:
- TopCount function
ms.assetid: cbe031c9-4ff0-45df-9810-ebaebacf161d
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: cd3ed46a927a40804b09e674fe6d814d2b085ab1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die durch einen Ausdruck angegebene Anzahl von obersten Zeilen in absteigender Rangreihenfolge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>Gilt für  
 Ein Ausdruck, der eine Tabelle, wie z. B. zurückgibt eine \<Tabelle Spaltenverweis >, oder eine Funktion, die eine Tabelle zurückgibt.  
  
## <a name="return-type"></a>Rückgabetyp  
 \<Tabellenausdruck >  
  
## <a name="remarks"></a>Hinweise  
 Der Wert, der durch die \<rank Expression > Argument bestimmt die absteigende Rangreihenfolge für die Zeilen, die in bereitgestellt werden die \<Tabellenausdruck > Argument und der Anzahl von obersten Zeilen, die im angegebenen der \<Anzahl > zurückgegeben.  
  
 Die TopCount-Funktion wurde ursprünglich eingeführt werden, um assoziative Vorhersagen zu ermöglichen und die gleichen Ergebnisse wie eine Anweisung, im Allgemeinen erzeugt **SELECT TOP** und **ORDER BY** Klauseln. Sie erhalten eine bessere Leistung bei assoziativen Vorhersagen bei Verwendung der **Vorhersagen (DMX)** -Funktion, die eine Anzahl von zurückzugebenden Vorhersagen spezifiziert.  
  
 Es gibt jedoch Situationen, in denen Sie dennoch eventuell TopCount verwenden. DMX unterstützt beispielsweise nicht die **oben** Qualifizierer in einer untergeordneten select-Anweisung. Die ["PredictHistogram" &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) Funktion nicht unterstützt, ist das Hinzufügen von **oben**.  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen werden Vorhersageabfragen für das Association-Modell, die Sie erstellen, mit der [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Die Abfragen geben die gleichen Ergebnisse zurück, aber im ersten Beispiel wird die TopCount und im zweiten Beispiel wird die Vorhersagefunktion.  
  
 Um zu verstehen, wie TopCount funktioniert, ist es möglicherweise hilfreich, zunächst eine Vorhersageabfrage auszuführen, die lediglich die geschachtelte Tabelle zurückgibt.  
  
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
  
 Die TopCount-Funktion verwendet die Ergebnisse dieser Abfrage und gibt die angegebene Anzahl von Zeilen mit kleinsten Werten zurück.  
  
```  
SELECT   
TopCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Das erste Argument für die TopCount-Funktion ist der Name einer Tabellenspalte. In diesem Beispiel wird die geschachtelte Tabelle zurückgegeben, durch die Predict-Funktion aufrufen und das INCLUDE_STATISTICS-Argument verwenden.  
  
 Das zweite Argument an die TopCount-Funktion ist die Spalte in der geschachtelten Tabelle, die Sie zum Sortieren der Ergebnisse verwenden. In diesem Beispiel gibt die INCLUDE_STATISTICS-Option die Spalten $SUPPORT, $PROBABILTY und $ADJUSTED PROBABILITY zurück. In diesem Beispiel werden die Ergebnisse mithilfe von $SUPPORT sortiert.  
  
 Das dritte Argument die TopCount-Funktion gibt die Anzahl der Zeilen, die als ganze Zahl zurück. Für die obersten drei Produkte, sortiert nach $ SUPPORT, geben Sie 3 ein.  
  
 Beispielergebnisse:  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29…|0.25…|  
|Water Bottle|2866|0.19…|0.17…|  
|Patchkit|2113|0.14…|0.13…|  
  
 Dieser Abfragetyp kann jedoch die Leistung in einer Produktionseinstellung beeinträchtigen. Das liegt daran, dass die Abfrage einen Satz aller Vorhersagen für den Algorithmus zurückgibt, diese Vorhersagen sortiert und die obersten 3 Vorhersagen zurückgibt.  
  
 Das folgende Beispiel enthält eine alternative Anweisung, die die gleichen Ergebnisse zurückgibt, aber bedeutend schneller ausgeführt wird. Dieses Beispiel ersetzt die TopCount mit der Predict-Funktion, die eine Anzahl von Vorhersagen als Argument akzeptiert. Dieses Beispiel verwendet außerdem die **$SUPPORT** Schlüsselwort direkt Spalte der geschachtelten Tabelle abgerufen.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 Die Ergebnisse enthalten die obersten 3 Vorhersagen sortiert nach dem Unterstützungswert. Sie können $SUPPORT durch $PROBABILITY oder $ADJUSTED_PROBABILITY ersetzen, um nach Wahrscheinlichkeit oder angepasster Wahrscheinlichkeit sortierte Vorhersagen zurückzugeben. Weitere Informationen finden Sie unter **Vorhersagen (DMX)**.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)   
 [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)   
 [TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)  
  
  
