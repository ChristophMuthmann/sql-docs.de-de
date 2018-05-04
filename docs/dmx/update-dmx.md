---
title: UPDATE (DMX) | Microsoft Docs
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
- UPDATE
dev_langs:
- DMX
helpviewer_keywords:
- NODE_CAPTION column
- mining models [Analysis Services], content changes
- modifying mining model content
- UPDATE statement [SQL Server], DMX
ms.assetid: 8a2b0942-c490-410c-b1cf-ff2e0fd8e24b
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c8b479dc74fe63a9eff4245be64a9eef5429101c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="update-dmx"></a>UPDATE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ändert die **NODE_CAPTION** Spalte in der Datamining-Modell.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
UPDATE <model>.CONTENT  
SET NODE_CAPTION='new caption'  
[WHERE <condition expression>]  
```  
  
## <a name="arguments"></a>Argumente  
 *model*  
 Ein Modellbezeichner.  
  
 *neue Beschriftung*  
 Eine Zeichenfolge, enthält den neuen Namen für, die **NODE_CAPTION** Spalte.  
  
 *Bedingungsausdruck*  
 Optional. Eine Bedingung, die die Werte einschränkt, die für die Spaltenliste zurückgegeben werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel die **UPDATE** -Anweisung ändert den Standardnamen `Cluster 1`, für Cluster `001` in den aussagekräftigeren Namen `Likely Customers`.  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40;DMX&#41; -Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen & #40; DMX & #41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
