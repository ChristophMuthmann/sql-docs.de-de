---
title: SELECT FROM &lt;Modell&gt; (DMX) | Microsoft Docs
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
- SELECT
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- empty prediction joins [DMX]
- SELECT FROM <model> statement
ms.assetid: dc5b9a01-e308-4ee8-84fc-ba4b991c60aa
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 064c5514e014b8ba976c21001665626bcb71722e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="select-from-ltmodelgt-dmx"></a>SELECT FROM &lt;Modell&gt; (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt einen leeren Vorhersagejoin aus und gibt den wahrscheinlichsten Wert oder die wahrscheinlichsten Werte für die angegebenen Spalten zurück. Für das Erstellen der Vorhersage wird ausschließlich der Inhalt aus dem Miningmodell verwendet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SELECT <expression list> [TOP <n>] FROM <model>   
[WHERE <condition list>]   
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumente  
 *Liste der Ausdrücke*  
 Eine durch Trennzeichen getrennte Liste mit Ausdrücken oder mit PREDICT- bzw. PREDICT ONLY-Spalten.  
  
 *n*  
 Optional. Eine ganze Zahl, die angibt, wie viele Zeilen zurückgegeben werden sollen.  
  
 *model*  
 Ein Modellbezeichner.  
  
 *Liste der Bedingungen*  
 Optional. Bedingungen, die die Werte einschränken, die für die Spaltenliste zurückgegeben werden.  
  
 *expression*  
 Optional. Ein Ausdruck, der einen Skalarwert zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die Spalten in der *Ausdrucksliste* müssen als predict oder only Predict definiert, oder im Zusammenhang mit einer vorhersagbaren Spalte.  
  
## <a name="naive-bayes-example"></a>Beispiel für Naive Bayes-Algorithmus  
 Im folgenden Beispiel wird ein leerer Vorhersagejoin für die Bike Buyer-Spalte ausgeführt und der für das TM Naive Bayes-Miningmodell wahrscheinlichste Status zurückgegeben.  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>Beispiel für den Time Series-Algorithmus  
 Im folgenden Beispiel wird eine Vorhersage für die Amount-Spalte des Forecasting-Modells ausgeführt, und die nächsten vier Schritte werden zurückgegeben. In der Model Region-Spalte sind die Fahrradmodelle und die Regionen zu jeweils einem Bezeichner kombiniert. Die Abfrage verwendet die [PredictTimeSeries &#40;DMX&#41; ](../dmx/predicttimeseries-dmx.md) Funktion, um die Vorhersage auszuführen.  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>Siehe auch  
 [WÄHLEN SIE &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen & #40; DMX & #41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
