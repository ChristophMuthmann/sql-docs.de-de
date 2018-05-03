---
title: Vergleichsoperatoren (DMX) | Microsoft Docs
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
dev_langs:
- DMX
helpviewer_keywords:
- comparison operators [DMX]
ms.assetid: eea3cf90-9683-4453-b1f3-da740f3a4885
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: dedc5659d4a6f0d613e3c0883e8255cfa9b680e9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="operators---comparison"></a>Operatoren – Vergleich
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Sie können Vergleichsoperatoren mit skalaren Daten in einem Data Mining Extensions (DMX)-Ausdruck [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Vergleichsoperatoren ergeben einen Wert vom booleschen Datentyp. Sie geben abhängig vom Ergebnis der getesteten Bedingung TRUE oder FALSE zurück.  
  
 In der folgenden Tabelle sind die Vergleichsoperatoren aufgeführt, die DMX unterstützt.  
  
|Operator|Description|  
|--------------|-----------------|  
|[&#60;&#40;Kleiner als&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|Gibt für Argumente, die ausgewertet ungleich NULL sind, TRUE zurück, wenn der Wert des Arguments auf der linken Seite kleiner ist als der Wert des Arguments auf der rechten Seite; gibt anderenfalls FALSE zurück. Wenn eines der Argumente oder beide Argumente ausgewertet gleich NULL sind, gibt der Operator einen NULL-Wert zurück.|  
|[&#62;&#40;Größer als&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Für Argumente, die auf einen Wert ungleich Null ausgewertet, gibt "true", wenn der Wert des Arguments auf der linken Seite größer als der Wert des Arguments auf der rechten Seite ist; Andernfalls wird "false" zurückgegeben. Wenn eines der Argumente oder beide Argumente ausgewertet gleich NULL sind, gibt der Operator einen NULL-Wert zurück.|  
|[= &#40;Gleich&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Für Argumente, die auf einen Wert ungleich Null ausgewertet, gibt "true", wenn der Wert des Arguments auf der linken Seite gleich dem Wert des Arguments auf der rechten Seite ist; Andernfalls wird "false" zurückgegeben. Wenn eines der Argumente oder beide Argumente ausgewertet gleich NULL sind, gibt der Operator einen NULL-Wert zurück.|  
|[&#60;&#62;&#40;Ungleich&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Für Argumente, die auf einen Wert ungleich Null ausgewertet, gibt "true", wenn der Wert des Arguments auf der linken Seite nicht gleich dem Wert des Arguments auf der rechten Seite ist; Andernfalls wird "false" zurückgegeben. Wenn eines der Argumente oder beide Argumente ausgewertet gleich NULL sind, gibt der Operator einen NULL-Wert zurück.|  
|[&#60;= &#40;Kleiner als oder gleich&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|Gibt für Argumente, die ausgewertet ungleich NULL sind, TRUE zurück, wenn der Wert des Arguments auf der linken Seite kleiner gleich dem Wert des Arguments auf der rechten Seite ist; gibt anderenfalls FALSE zurück. Wenn eines der Argumente oder beide Argumente ausgewertet gleich NULL sind, gibt der Operator einen NULL-Wert zurück.|  
|[&#62;= &#40;Größer als oder gleich&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Für Argumente, die auf einen Wert ungleich Null ausgewertet, gibt "true", wenn der Wert des Arguments auf der linken Seite größer als oder gleich dem Wert des Arguments auf der rechten Seite; Andernfalls wird "false" zurückgegeben. Wenn eines der Argumente oder beide Argumente ausgewertet gleich NULL sind, gibt der Operator einen NULL-Wert zurück.|  
  
 Sie können Vergleichsoperatoren in DMX-Anweisungen und -Funktionen auch verwenden, um nach einer Bedingung zu suchen.  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen & #40; DMX & #41; Referenz](../dmx/data-mining-extensions-dmx-reference.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Verweis-Funktion](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Datamining-Erweiterungen & #40; DMX & #41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Syntaxkonventionen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Syntaxelemente](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Ausdrücke &#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operatoren &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Struktur und die Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Understanding the DMX Select Statement (Grundlegendes zur SELECT-Anweisung)](../dmx/understanding-the-dmx-select-statement.md)  
  
  
