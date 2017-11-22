---
title: MSSQLSERVER_10538 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10538 (Database Engine error)
ms.assetid: 284d19b4-4979-4cbe-a9be-ac1104433c69
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c93dfdc81a37d06e6da2d1f1d2329ac378893090
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10538"></a>MSSQLSERVER_10538
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10538|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PG_INVALID_PLANGUIDE_HANDLE|  
|Meldungstext|Die Planhinweisliste wurde nicht gefunden, weil die angegebene Planhinweislisten-ID NULL oder ungültig ist oder weil Sie keine Berechtigung für das Objekt besitzen, auf das die Planhinweisliste verweist. Vergewissern Sie sich, dass die Planhinweislisten-ID gültig ist, die aktuelle Sitzung auf den korrekten Datenbankkontext eingestellt ist und Sie entweder die ALTER DATABASE-Berechtigung oder die ALTER-Berechtigung für das Objekt besitzen, auf das die Planhinweisliste verweist.|  
  
## <a name="explanation"></a>Erklärung  
Die ID der angegebenen Planhinweisliste ist NULL oder ungültig, oder Sie besitzen nicht die Berechtigung für das Objekt, auf das die Planhinweisliste verweist.  
  
## <a name="user-action"></a>Benutzeraktion  
Vergewissern Sie sich, dass die Planhinweislisten-ID gültig, die aktuelle Sitzung auf den korrekten Datenbankkontext eingestellt ist und Sie die ALTER DATABASE-Berechtigung oder die ALTER-Berechtigung für das Objekt besitzen, auf das die Planhinweisliste verweist.  
  
## <a name="see-also"></a>Siehe auch  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Planhinweislisten](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
