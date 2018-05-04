---
title: Sys.dm_pdw_resource_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6089b18ba68dab6c0d667b0a1ae6397788679ee7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwresourcewaits-transact-sql"></a>Sys.dm_pdw_resource_waits (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Warten Sie, zeigt Informationen für alle Ressourcentypen in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Die Position der Anforderung in der Liste warten.|0-basierte Ordnungszahl. Dies ist in allen Wait-Einträgen nicht eindeutig.|  
|session_id|**nvarchar(32)**|ID der Sitzung, in der der Wartezustand aufgetreten ist.|Finden Sie unter Session_id in [sys.dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|Typ|**nvarchar(255)**|Der Typ des Wartevorgangs, diesen Eintrag darstellt.|Mögliche Werte:<br /><br /> Verbindung<br /><br /> Lokale Abfragen Parallelität<br /><br /> Verteilte Abfragen Parallelität<br /><br /> DMS-Parallelität<br /><br /> Backup Parallelität|  
|object_type|**nvarchar(255)**|Typ des Objekts, das den Wartevorgang betroffen ist.|Mögliche Werte:<br /><br /> **OBJEKT**<br /><br /> **DATABASE**<br /><br /> **SYSTEM**<br /><br /> **SCHEMA**<br /><br /> **ANWENDUNG**|  
|object_name|**nvarchar(386)**|Der Name oder die GUID des angegebenen Objekts, das den Wartevorgang betroffen war.|Tabellen und Sichten werden mit dreiteilige Namen angezeigt.<br /><br /> Indizes und Statistiken werden mit vierteiligen Namen angezeigt.<br /><br /> Namen, die Prinzipale und die Datenbanken sind Zeichenfolgennamen.|  
|request_id|**nvarchar(32)**|Die ID der Anforderung auf der der Wartezustand aufgetreten ist.|QID Bezeichner der Anforderung.<br /><br /> GUID-Bezeichner für ladeanforderungen.|  
|request_time|**datetime**|Der Zeitpunkt, an dem die Sperre oder eine Ressource angefordert wurde.||  
|acquire_time|**datetime**|Der Zeitpunkt, an dem die Sperre oder eine Ressource eingerichtet wurde.||  
|state|**nvarchar(50)**|Status des den Wartezustand.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Die Priorität des Elements warten.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|Anzahl der Slots für Parallelität (max. 32) für diese Anforderung reserviert.|1 – für SmallRC<br /><br /> 3 – für MediumRC<br /><br /> 7 für LargeRC<br /><br /> 22 – für XLargeRC|  
|resource_class|**nvarchar(20)**|Die Ressourcenklasse für diese Anforderung.|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Data Warehouse-dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
