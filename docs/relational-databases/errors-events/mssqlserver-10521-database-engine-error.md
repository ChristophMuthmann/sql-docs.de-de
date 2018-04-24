---
title: MSSQLSERVER_10521 | Microsoft-Dokumentation
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
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ade493d38009758782076372d2414c582796512
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver10521"></a>MSSQLSERVER_10521
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10521|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PG_PARAM_NEEDED|  
|Meldungstext|Die Planhinweisliste „%.\*ls“ kann nicht erstellt werden, weil **@type** als „%ls“ angegeben wurde und der „%ls“-Parameter NULL ist. Dieser Typ erfordert einen Wert ungleich NULL für den Parameter. Geben Sie einen Wert ungleich NULL für den Parameter an, oder ändern Sie den Typ in einen Typ, der NULL-Werte für den Parameter zulässt.|  
  
## <a name="explanation"></a>Erklärung  
Der in **@type** angegebene Typ erfordert einen Wert ungleich NULL für den angegebenen Parameter. Es wurde jedoch ein NULL-Wert angegeben.  
  
## <a name="user-action"></a>Benutzeraktion  
Geben Sie einen Wert ungleich NULL für den Parameter an, oder ändern Sie den Typ in einen Typ, der NULL-Werte für den Parameter zulässt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Planhinweislisten](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
