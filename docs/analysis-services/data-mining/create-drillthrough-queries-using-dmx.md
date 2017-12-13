---
title: Erstellen von Drillthroughabfragen mit DMX | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 42c896ee-e5ee-4017-b66e-31d1fe66d369
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3b9487131e474dd00a25390a53cb5f3f11d07d2c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="create-drillthrough-queries-using-dmx"></a>Erstellen von Drillthroughabfragen mit DMX
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Für alle Modelle, die Drillthrough unterstützen, können Sie Fall- und Strukturdaten durch Erstellen einer DMX-Abfrage in abrufen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder einem anderen Client, die DMX unterstützt.  
  
> [!WARNING]  
>  Zum Anzeigen der Daten muss Drillthrough aktiviert werden, wofür Sie die entsprechenden Berechtigungen benötigen.  
  
## <a name="specifying-drillthrough-options"></a>Angeben von Drillthroughoptionen  
 Die allgemeine Syntax zum Abrufen von Modell- und Strukturfällen sieht folgendermaßen aus:  
  
```  
SELECT <model column list>, StructureColumn('<structure column name') FROM <modelname>.CASES  
```  
  
 Weitere Informationen zur Verwendung von DMX-Abfragen zum Zurückgeben von Falldaten finden Sie unter [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](../../dmx/select-from-model-cases-dmx.md) und [SELECT FROM &#60;structure&#62;.CASES](../../dmx/select-from-structure-cases.md).  
  
## <a name="examples"></a>Beispiele  
 Bei der folgenden DMX-Abfrage werden die Falldaten für eine bestimmte Produktreihe von einem Zeitreihenmodell zurückgegeben. Die Abfrage gibt außerdem die Spalte **Amount**zurück, die zwar nicht im Modell verwendet wurde, jedoch in der Miningstruktur verfügbar ist.  
  
```  
SELECT [DateSeries], [Model Region], Quantity, StructureColumn('Amount') AS [M200 Pacific Amount]  
FROM Forecasting.CASES  
WHERE [Model Region] = 'M200 Pacific'  
```  
  
 In diesem Beispiel wird ein Alias verwendet, um die Strukturspalte umzubenennen. Wenn Sie der Strukturspalte keinen Alias zuordnen, wird die Spalte mit dem Namen "Expression" zurückgegeben. Dies ist das Standardverhalten für alle unbenannten Spalten.  
  
## <a name="see-also"></a>Siehe auch  
 [Drillthroughabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [Drillthrough für Miningstrukturen](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  
