---
title: dm_io_pending_io_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_io_pending_io_requests
- dm_io_pending_io_requests
- dm_io_pending_io_requests_TSQL
- sys.dm_io_pending_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_pending_io_requests dynamic management view
ms.assetid: d1fb46dd-5c74-4c04-9ecf-8934b1bedb5b
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b94ec40d19936983b960814cdc6d24c27f59aefb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmiopendingiorequests-transact-sql"></a>sys.dm_io_pending_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Gibt eine Zeile für jede ausstehende E/A-Anforderung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_io_pending_io_requests**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**io_completion_request_address**|**varbinary(8)**|Arbeitsspeicheradresse der E/A-Anforderung. Lässt keine NULL-Werte zu.|  
|**io_type**|**vom Datentyp varchar(7)**|Typ der ausstehenden E/A-Anforderung. Lässt keine NULL-Werte zu.|  
|**io_pending**|**int**|Gibt an, ob die E/A-Anforderung ausstehend ist oder von Windows abgeschlossen wurde. Eine E/A-Anforderung kann noch ausstehend sein, selbst wenn Windows die Anforderung abgeschlossen hat, aber [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] noch keinen Kontextwechsel ausgeführt hat, bei dem die E/A-Anforderung verarbeitet und aus dieser Liste entfernt würde. Lässt keine NULL-Werte zu.|  
|**io_completion_routine_address**|**varbinary(8)**|Interne Funktion, die nach Abschluss der E/A-Anforderung aufgerufen wird. Lässt NULL-Werte zu.|  
|**io_user_data_address**|**varbinary(8)**|Nur interne Verwendung. Lässt NULL-Werte zu.|  
|**scheduler_address**|**varbinary(8)**|Das Zeitplanungsmodul, in dem diese E/A-Anforderung ausgestellt wurde. Die E/A-Anforderung wird in der Liste ausstehender E/A-Anforderungen des Zeitplanungsmoduls angezeigt. Weitere Informationen finden Sie unter [DM_OS_SCHEDULERS &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). Lässt keine NULL-Werte zu.|  
|**io_handle**|**varbinary(8)**|Dateihandle der Datei, die in der E/A-Anforderung verwendet wird. Lässt NULL-Werte zu.|  
|**io_offset**|**bigint**|Offset der E/A-Anforderung. Lässt keine NULL-Werte zu.|  
|**io_pending_ms_ticks**|**int**|Nur interne Verwendung. Lässt keine NULL-Werte zu.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Ich O dynamische Verwaltungssichten und-Funktionen im Zusammenhang &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


