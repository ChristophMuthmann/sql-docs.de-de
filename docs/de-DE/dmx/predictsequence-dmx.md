---
title: PredictSequence (DMX) | Microsoft Docs
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
- PredictSequence
dev_langs:
- DMX
helpviewer_keywords:
- PredictSequence function
ms.assetid: c2992dfc-b99d-4430-8dcd-21ad3ffd4590
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b8ef0b3f0ba361e368695b31d15b26cd013ed6e8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Sagt zukünftige Sequenzwerte für eine angegebene Gruppe von Sequenzdaten voraus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 Ein \<Tabellenausdruck >.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die *n* Parameter angegeben wird, gibt die folgenden Werte:  
  
-   Wenn *n* ist größer als 0 (null), die am wahrscheinlichsten Sequence-Werte in der nächsten *n* Schritte.  
  
-   Wenn beide *n Boot-* und *n-End-* angegeben sind, die Sequenzwerte von *n Boot-* auf *n-End-*.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird basierend auf dem Sequence Clustering-Miningmodell eine Sequenz der fünf Produkte in der [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]-Datenbank zurückgegeben, bei denen die Wahrscheinlichkeit am größten ist, dass sie von einem Kunden gekauft werden.  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40;DMX&#41; Verweis-Funktion](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
