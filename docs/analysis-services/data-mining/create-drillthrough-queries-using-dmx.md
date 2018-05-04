---
title: Erstellen von Drillthroughabfragen mit DMX | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54183e4c9d56b67e8fd4cf966122069b7fc18ff0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-drillthrough-queries-using-dmx"></a>Erstellen von Drillthroughabfragen mit DMX
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Für alle Modelle, die Drillthrough unterstützen, können Fall- und Strukturdaten durch Erstellen einer DMX-Abfrage in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder einem beliebigen anderen Client abgerufen werden.  
  
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
 [Drillthroughabfragen & #40; Datamining & #41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [Drillthrough in Miningstrukturen](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  
