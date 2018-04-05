---
title: Vorhersagen (DMX) | Microsoft Docs
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
- PREDICT
dev_langs:
- DMX
helpviewer_keywords:
- Predict function
ms.assetid: f02ff4b3-9bd7-409d-ad14-ead67b3206c4
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 448507936bab886a8d081ee487ab323a3a4a2ef4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Die **Predict** Funktion gibt einen vorhergesagten Wert oder eine Gruppe von Werten für eine angegebene Spalte zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>Gilt für  
 Einen Verweis auf eine skalare Spalte oder einen Verweis auf eine Tabellenspalte.  
  
## <a name="return-type"></a>Rückgabetyp  
 \<skalarspaltenverweis >  
  
 oder  
  
 \<Tabelle der Spaltenverweis >  
  
 Der Rückgabetyp hängt vom Typ der Spalte ab, auf die diese Funktion angewendet wird.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY und INCLUDE_STATISTICS gelten nur für Verweise auf Tabellenspalten, und EXCLUDE_NULL und INCLUDE_NULL gelten nur für Verweise auf skalare Spalten.  
  
## <a name="remarks"></a>Remarks  
 Zu den Optionen gehören EXCLUDE_NULL (Standardwert), INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (Standardwert), INPUT_ONLY und INCLUDE_STATISTICS.  
  
> [!NOTE]  
>  Für zeitreihenmodelle wird die Vorhersagefunktion INCLUDE_STATISTICS nicht unterstützt.  
  
 Der INCLUDE_NODE_ID-Parameter gibt die $NODEID-Spalte im Ergebnis zurück. NODE_ID ist der Inhaltsknoten, für den die Vorhersage in einem bestimmten Fall ausgeführt wird. Dieser Parameter ist optional, bei Verwendung von Vorhersagen für Tabellenspalten.  
  
 Die  *n*  Parameter gilt für Tabellenspalten. Er legt fest, wie viele Zeilen entsprechend dem Typ der Vorhersage zurückgegeben werden sollen. Wenn die zugrunde liegende Spalte Sequenz ist, ruft es die **PredictSequence** Funktion. Wenn die zugrunde liegende Spalte zeitreihenspalte ist, ruft es die **PredictTimeSeries** Funktion. Für assoziative Vorhersagen, ruft er die **PredictAssociation** Funktion.  
  
 Die **Predict** -Funktion unterstützt Polymorphie.  
  
 Häufig werden die folgenden alternativen Kurzformen verwendet:  
  
-   [Gender] ist eine Alternative für **Predict**([Gender], EXCLUDE_NULL).  
  
-   [Products Purchases] ist eine Alternative für **Predict**([Products Purchases], EXCLUDE_NULL, EXCLUSIVE).  
  
    > [!NOTE]  
    >  Der Rückgabetyp dieser Funktion wird als Spaltenverweis angesehen. Dies bedeutet, dass die **Predict** Funktion kann verwendet werden, als Argument in anderen Funktionen, die einen Spaltenverweis als Argument akzeptieren (mit Ausnahme der **Predict** Funktion selbst).  
  
 Die Spalten hinzugefügt, INCLUDE_STATISTICS an eine Vorhersage für eine tabellenwertspalte übergeben **$Probability** und **$Support** , die sich ergebende Tabelle. Diese Spalten beschreiben die Wahrscheinlichkeit des Vorhandenseins für den Datensatz der zugeordneten geschachtelten Tabelle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Vorhersagefunktion, geben Sie die vier Produkte in der Adventure Works-Datenbank, die höchstwahrscheinlich zusammen verkauft werden. Da die Funktion für eine Zuordnungsregel Miningmodell Vorhersagen ist, verwendet es automatisch die **PredictAssociation** funktionieren wie zuvor beschrieben.  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 Beispielergebnisse:  
  
 Diese Abfrage gibt eine einzelne Zeile mit Daten in einer Spalte (`Expression`) zurück, diese Spalte enthält jedoch die folgende geschachtelte Tabelle.  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patchkit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
