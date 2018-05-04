---
title: Vorhanden ist (DMX) | Microsoft Docs
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
- Exists
dev_langs:
- DMX
helpviewer_keywords:
- Exists function
ms.assetid: 3b54dd93-f0a8-4f9a-96ae-a38bf977dda1
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9e741b37b167fcb4568fd38fe069224e669cda0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt **"true"** , wenn die angegebene Unterabfrage mindestens eine Zeile zurückgibt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>Argumente  
 *subquery*  
 Eine SELECT-Anweisung der Form SELECT * FROM \<Spaltenname > [, in denen \<prädikatliste >].  
  
## <a name="result-type"></a>Ergebnistyp  
 Gibt **"true"** Wenn von der Unterabfrage zurückgegebene Resultset mindestens eine Zeile enthält, andernfalls **"false"**.  
  
## <a name="remarks"></a>Hinweise  
 Sie können das NOT-Schlüsselwort vor EXISTS verwenden, z. B. `WHERE NOT EXISTS (<subquery>)`.  
  
 Die Spaltenliste, die zum Unterabfrageargument EXISTS hinzugefügt wird, ist nicht relevant. Die Funktion überprüft lediglich, ob eine Zeile existiert, auf die die Bedingung zutrifft.  
  
## <a name="examples"></a>Beispiele  
 Sie können mit EXISTS und NOT EXISTS überprüfen, ob Bedingungen in einer geschachtelten Tabelle zutreffen. Dies ist hilfreich beim Erstellen eines Filters zum Überprüfen der Daten, die zum Trainieren oder Testen eines Data Mining-Modells verwendet werden. Weitere Informationen finden Sie unter [Filter für Miningmodelle &#40;Analysis Services – Data Mining&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 Das folgende Beispiel basiert auf der `[Association]` Miningstruktur und ein Miningmodell, die Sie in erstellt die [Data Mining-Grundlagen](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Die Abfrage gibt nur die Fälle zurück, in denen der Kunde mindestens ein Patchkit gekauft hat.  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 Eine weitere Möglichkeit zum Anzeigen der gleichen Daten, die von dieser Abfrage zurückgegeben wird, öffnen Sie das Modell im Viewer Zuordnung der rechten Maustaste auf das Itemset ist **Patch Kit = Existing**, wählen die **Drillthrough** aus, und wählen Sie dann **nur Modellfälle**.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Modellfiltersyntax und Beispiele für &#40;Analysis Services – Datamining&#41;](../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)  
  
  
