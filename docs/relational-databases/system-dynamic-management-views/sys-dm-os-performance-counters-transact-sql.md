---
title: sys.dm_os_performance_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql-non-specified
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
- dm_os_performance_counters
- sys.dm_os_performance_counters_TSQL
- dm_os_performance_counters_TSQL
- sys.dm_os_performance_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_performance_counters dynamic management view
ms.assetid: a1c3e892-cd48-40d4-b6be-2a9246e8fbff
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8ae698ff1dbf5be9cd99dda33c6a3f0e7d6f89ea
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmosperformancecounters-transact-sql"></a>sys.dm_os_performance_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Gibt eine Zeile pro Leistungsindikator zurück, der vom Server verwaltet wird. Informationen zu einzelnen Leistungsindikatoren finden Sie unter [verwenden, SQL Server-Objekten](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_performance_counters**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|Kategorie, zu der dieser Leistungsindikator gehört.|  
|**counter_name**|**nchar(128)**|Name des Leistungsindikators. Um weitere Informationen zu einem Leistungsindikator zu erhalten, ist dies der Name des Themas, wählen Sie aus der Liste der Leistungsindikatoren im [verwenden, SQL Server-Objekten](../../relational-databases/performance-monitor/use-sql-server-objects.md). |  
|**instance_name**|**nchar(128)**|Name der spezifischen Instanz des Leistungsindikators. Enthält oft den Datenbanknamen.|  
|**cntr_value**|**bigint**|Aktueller Wert des Leistungsindikators.<br /><br /> **Hinweis:** für die Leistungsindikatoren der pro Sekunde, ist dieser Wert kumulativ. Der Ratenwert muss durch Stichproben des Werts zu diskreten Zeitintervallen berechnet werden. Der Unterschied zwischen zwei aufeinander folgenden Werten ist gleich der Rate für das verwendete Zeitintervall.|  
|**cntr_type**|**int**|Typ des Leistungsindikators, wie von der Windows-Leistungsarchitektur definiert. Finden Sie unter [WMI Performance Counter Types](http://msdn2.microsoft.com/library/aa394569.aspx) auf MSDN oder in der Windows Server-Dokumentation weitere Informationen zu Leistungsindikatortypen.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn die Installationsinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Leistungsindikatoren des Windows-Betriebssystems nicht anzeigt, ermitteln Sie mit der folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfrage, ob die Leistungsindikatoren deaktiviert wurden.  
  
```  
SELECT COUNT(*) FROM sys.dm_os_performance_counters;  
```  
  
 Wenn der Rückgabewert 0 Zeilen ist, wurden die Leistungsindikatoren deaktiviert. Suchen Sie daraufhin im Setupprotokoll nach dem Fehler 3409 "Installieren Sie 'sqlctr.ini' für diese Instanz neu, und stellen Sie sicher, dass das Anmeldekonto der Instanz über die richtigen Registrierungsberechtigungen verfügt."  Hiermit wird angegeben, dass Leistungsindikatoren nicht aktiviert wurden. Die Fehlermeldungen unmittelbar vor dem Fehler 3409 sollten die Ursache für das Fehlschlagen der Leistungsindikator-Aktivierung angeben. Weitere Informationen zu Setupprotokolldateien finden Sie unter [anzeigen und Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="permission"></a>Berechtigung

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
 
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Leistungsindikatorwerte zurückgegeben.  
  
```  
SELECT object_name, counter_name, instance_name, cntr_value, cntr_type  
FROM sys.dm_os_performance_counters;  
  
```  
  
## <a name="see-also"></a>Siehe auch  
  [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  


