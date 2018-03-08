---
title: MSSQLSERVER_10537 | Microsoft-Dokumentation
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
helpviewer_keywords: 10537 (Database Engine error)
ms.assetid: 728469a4-6523-4a37-925f-a950d75420fa
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3329a982d09e38614d6297d1776f7f58e5586f5b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10537"></a>MSSQLSERVER_10537
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10537|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PG_DUP_ENABLED|  
|Meldungstext|Die Planhinweisliste '%.*ls' kann nicht aktiviert werden, weil die aktivierte Planhinweisliste '%.\*ls' denselben Bereich und Startoffsetwert wie die Anweisung enthält. Deaktivieren Sie die vorhandene Planhinweisliste, bevor Sie die angegebene Planhinweisliste aktivieren.|  
  
## <a name="explanation"></a>Erklärung  
Eine vorhandene Planhinweisliste enthält denselben Bereich und Startoffsetwert wie die Anweisung in der angegebenen Planhinweisliste.  
  
## <a name="user-action"></a>Benutzeraktion  
Deaktivieren Sie die vorhandene Planhinweisliste, bevor Sie die angegebene Planhinweisliste aktivieren.  
  
## <a name="see-also"></a>Siehe auch  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Planhinweislisten](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
