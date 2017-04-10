---
title: "Erstellen von Drillthroughabfragen mit DMX | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42c896ee-e5ee-4017-b66e-31d1fe66d369
caps.latest.revision: 5
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 5
---
# Erstellen von Drillthroughabfragen mit DMX
  Für alle Modelle, die Drillthrough unterstützen, können Fall- und Strukturdaten durch Erstellen einer DMX-Abfrage in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder einem beliebigen anderen Client abgerufen werden.  
  
> [!WARNING]  
>  Zum Anzeigen der Daten muss Drillthrough aktiviert werden, wofür Sie die entsprechenden Berechtigungen benötigen.  
  
## Angeben von Drillthroughoptionen  
 Die allgemeine Syntax zum Abrufen von Modell- und Strukturfällen sieht folgendermaßen aus:  
  
```  
SELECT <model column list>, StructureColumn('<structure column name') FROM <modelname>.CASES  
```  
  
 Weitere Informationen zur Verwendung von DMX-Abfragen zum Zurückgeben von Falldaten finden Sie unter [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](../Topic/SELECT%20FROM%20%3Cmodel%3E.CASES%20\(DMX\).md) und [SELECT FROM &#60;structure&#62;.CASES](../Topic/SELECT%20FROM%20%3Cstructure%3E.CASES.md).  
  
## Beispiele  
 Bei der folgenden DMX-Abfrage werden die Falldaten für eine bestimmte Produktreihe von einem Zeitreihenmodell zurückgegeben. Die Abfrage gibt außerdem die Spalte **Amount**zurück, die zwar nicht im Modell verwendet wurde, jedoch in der Miningstruktur verfügbar ist.  
  
```  
SELECT [DateSeries], [Model Region], Quantity, StructureColumn('Amount') AS [M200 Pacific Amount]  
FROM Forecasting.CASES  
WHERE [Model Region] = 'M200 Pacific'  
```  
  
 In diesem Beispiel wird ein Alias verwendet, um die Strukturspalte umzubenennen. Wenn Sie der Strukturspalte keinen Alias zuordnen, wird die Spalte mit dem Namen "Expression" zurückgegeben. Dies ist das Standardverhalten für alle unbenannten Spalten.  
  
## Siehe auch  
 [Drillthroughabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [Drillthrough in Miningstrukturen](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  