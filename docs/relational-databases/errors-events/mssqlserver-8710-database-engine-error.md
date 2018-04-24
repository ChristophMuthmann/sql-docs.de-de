---
title: MSSQLSERVER_8710 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e16fef23bb92ece7fa6be417975b662752c766cb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
