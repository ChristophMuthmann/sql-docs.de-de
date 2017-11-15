---
title: MSSQLSERVER_8710 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 427ae245dc58fddae8b9c78145a8a6601839ed7e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|MSSQLSERVER|  
|Ereignis-ID|8710|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|Meldungstext|Aggregatfunktionen, die mit CUBE-, ROLLUP- oder GROUPING SET-Abfragen verwendet werden, müssen das Zusammenführen von Unteraggregaten bereitstellen. Entfernen Sie die Aggregatfunktion, oder schreiben Sie die Abfrage mit UNION ALL über GROUP BY-Klauseln, um das Problem zu beheben.|  
  
## <a name="explanation"></a>Erklärung  
Es wurde eine Aggregatfunktion mit CUBE, ROLLUP oder GROUPING SETS verwendet, die keine Methode zum Zusammenführen von Unteraggregaten zur Verfügung stellt.  
  
## <a name="user-action"></a>Benutzeraktion  
Entfernen Sie die Aggregatfunktion, oder schreiben Sie die Abfrage mit UNION ALL über GROUP BY-Klauseln, um das Problem zu beheben.  
  
