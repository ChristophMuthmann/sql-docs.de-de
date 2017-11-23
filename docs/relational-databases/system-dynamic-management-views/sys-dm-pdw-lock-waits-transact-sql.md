---
title: Sys.dm_pdw_lock_waits (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 8ef966f8-d14e-40d3-9626-3508ada9b8fb
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 659b4750c0cad521cdc34fe7b07763dea7238581
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwlockwaits-transact-sql"></a>Sys.dm_pdw_lock_waits (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu den Anforderungen, die Sperren warten.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Die Position der Anforderung in der Liste warten.|0-basierte Ordnungszahl. Dies ist in allen Wait-Einträgen nicht eindeutig.|  
|session_id|**nvarchar(32)**|ID der Sitzung, in der der Wartezustand aufgetreten ist.|Finden Sie unter Session_id in [sys.dm_pdw_exec_sessions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|Typ|**nvarchar(255)**|Der Typ des Wartevorgangs, diesen Eintrag darstellt.|Mögliche Werte:<br /><br /> Shared<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> Exclusive|  
|object_type|**nvarchar(255)**|Typ des Objekts, das den Wartevorgang betroffen ist.|Mögliche Werte:<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> SYSTEM<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**nvarchar(386)**|Der Name oder die GUID des angegebenen Objekts, das den Wartevorgang betroffen war.|Tabellen und Sichten werden mit dreiteilige Namen angezeigt.<br /><br /> Indizes und Statistiken werden mit vierteiligen Namen angezeigt.<br /><br /> Namen, die Prinzipale und die Datenbanken sind Zeichenfolgennamen.|  
|request_id|**nvarchar(32)**|Die ID der Anforderung auf der der Wartezustand aufgetreten ist.|ID der Anforderung.<br /><br /> Dies ist eine GUID für ladeanforderungen.|  
|request_time|**datetime**|Der Zeitpunkt, an dem die Sperre oder eine Ressource angefordert wurde.||  
|acquire_time|**datetime**|Der Zeitpunkt, an dem die Sperre oder eine Ressource eingerichtet wurde.||  
|state|**nvarchar(50)**|Status des den Wartezustand.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Die Priorität des Elements warten.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
