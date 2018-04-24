---
title: MSSQLSERVER_10533 | Microsoft-Dokumentation
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
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b4985c0d5d664bdd4ae48cd293abc3794d1939d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver10533"></a>MSSQLSERVER_10533
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10533|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PG_NAME_TOO_BIG|  
|Meldungstext|Die Planhinweisliste „%.*ls“ kann nicht erstellt werden, weil der Name der Planhinweisliste länger als die maximal zulässige Zeichenanzahl von 124 ist. Legen Sie einen Namen mit weniger als 125 Zeichen fest.|  
  
## <a name="explanation"></a>Erklärung  
Die Planhinweisliste überschreitet die maximal zulässige Zeichenanzahl von 124.  
  
## <a name="user-action"></a>Benutzeraktion  
Legen Sie einen Namen mit weniger als 125 Zeichen fest.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Planhinweislisten](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
