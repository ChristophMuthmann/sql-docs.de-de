---
title: MSSQLSERVER_10502 | Microsoft-Dokumentation
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
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82095a7b857bc9166779ac16324b7850f5eebdd1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver10502"></a>MSSQLSERVER_10502
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10502|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PG_DUP_FOUND|  
|Meldungstext|Die Planhinweisliste „%.*ls“ kann nicht erstellt werden, weil die mit @stmt und @module_or_batch oder @plan_handle und @statement_start_offset angegebene Anweisung mit der vorhandenen Planhinweisliste „%.\*ls“ in der Datenbank übereinstimmt. Löschen Sie die vorhandene Planhinweisliste, bevor Sie die neue Planhinweisliste erstellen.|  
  
## <a name="explanation"></a>Erklärung  
Für die angegebene Anweisung ist eine Planhinweisliste vorhanden.  
  
## <a name="user-action"></a>Benutzeraktion  
Löschen Sie die vorhandene Planhinweisliste, bevor Sie die neue Planhinweisliste erstellen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Planhinweislisten](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
