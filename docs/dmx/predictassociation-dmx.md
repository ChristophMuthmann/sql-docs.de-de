---
title: PredictAssociation (DMX) | Microsoft Docs
ms.custom: 
ms.date: 09/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PredictAssociation
dev_langs:
- DMX
helpviewer_keywords:
- PredictAssociation function
ms.assetid: 33eb66b5-84c6-449f-aaae-316345bc4ad5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1fcebadb217b3ecbf2de828cc9566f4af5ffeddd
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sagt eine assoziative Mitgliedschaft voraus.  
  
Die PredictAssociation-Funktion können Sie z. B. um den Satz von Empfehlungen den aktuellen Status der Einkaufswagen eines Kunden zu erhalten. 
  
## <a name="syntax"></a>Syntax  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>Gilt für  
 Algorithmen, die vorhersagbare geschachtelte Tabellen, einschließlich Zuordnung und einige Klassifizierungsalgorithmen enthalten. Klassifikationsalgorithmen, die Unterstützung für geschachtelte Tabellen enthalten die [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees, [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes und [!INCLUDE[msCoName](../includes/msconame-md.md)] Neural Network-Algorithmen.  
  
## <a name="return-type"></a>Rückgabetyp  
 \<Tabellenausdruck >  
  
## <a name="remarks"></a>Hinweise  
 Die Optionen für die **PredictAssociation** -Funktion sind EXCLUDE_NULL, INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (Standardwert), INPUT_ONLY, INCLUDE_STATISTICS und INCLUDE_NODE_ID.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY und INCLUDE_STATISTICS gelten nur für Verweise auf Tabellenspalten, und EXCLUDE_NULL und INCLUDE_NULL gelten nur für Verweise auf skalare Spalten.  
  
 INCLUDE_STATISTICS gibt nur zurück, **$Probability** und **$AdjustedProbability**.  
  
 Wenn der numerische Parameter  *n*  angegeben wird, die **PredictAssociation** Funktion gibt die obersten n am wahrscheinlichsten Werte, die basierend auf der Wahrscheinlichkeit zurück:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 Wenn Sie aufnehmen **$AdjustedProbability**, die Anweisung gibt die obersten  *n*  Werte auf Grundlage der **$AdjustedProbability**.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die **PredictAssociation** -Funktion zurückgibt, das die vier Produkte in der Adventure Works-Datenbank treten wahrscheinlich zusammen verkauft werden.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
Im folgende Beispiel wird veranschaulicht, wie Sie eine geschachtelte Tabelle als Eingabe für die Vorhersagefunktion können mithilfe der SHAPE-Klausel. SHAPE-Abfrage erstellt ein Rowset mit CustomerId als eine Spalte und eine geschachtelte Tabelle als eine zweite Spalte, die die Liste der Produkte enthält, werden ein Kunde bereits geschaltet wurde. 

~~~~
SELECT T.[CustomerId], PredictAssociation(MyNestedTable, 5) // returns top 5 associated items
FROM My Model
PREDICTION JOIN
SHAPE {
    OPENQUERY([Adventure Works DW],'SELECT CustomerID, OrderNumber
    FROM vAssocSeqOrders ORDER BY OrderNumber')
} APPEND (
    {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, model FROM 
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}
  RELATE OrderNumber to OrderNumber) AS T
~~~~  

  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

