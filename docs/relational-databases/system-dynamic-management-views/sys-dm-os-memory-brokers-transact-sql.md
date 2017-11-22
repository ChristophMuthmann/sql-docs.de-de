---
title: dm_os_memory_brokers (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_brokers
- dm_os_memory_brokers_TSQL
- sys.dm_os_memory_brokers_TSQL
- dm_os_memory_brokers
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_memory_brokers dynamic management view
ms.assetid: 48dd6ad9-0d36-4370-8a12-4921d0df4b86
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2b1a1d13e4a15df92d79bf74d1358352a93266a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosmemorybrokers-transact-sql"></a>sys.dm_os_memory_brokers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Interne Zuordnungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden den Speicher-Manager von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nachverfolgung der Unterschiede zwischen der Prozess Arbeitsspeicher-Leistungsindikatoren von **dm_os_process_memory** und interne Indikatoren können die arbeitsspeichernutzung von externen Komponenten an die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] belegten Speicherplatz.  
  
 Speicherbroker verteilen Speicherbelegungen gleichmäßig auf die verschiedenen Komponenten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf Basis der aktuellen und der prognostizierten Auslastung. Speicherbroker führen keine Zuordnungen durch. Sie verfolgen Zuordnungen nur zum Berechnen der Verteilung.  
  
 Die folgende Tabelle enthält Informationen zu Speicherbrokern.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_memory_brokers**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|ID des Ressourcenpools, wenn er einem Ressourcenkontrollenpool zugeordnet ist.|  
|**memory_broker_type**|**nvarchar(60)**|Typ des Speicherbrokers. Es gibt derzeit drei Typen von speicherbrokern in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], unten mit ihren Beschreibungen aufgelistet.<br /><br /> **MEMORYBROKER_FOR_CACHE** : für die Verwendung von zugeordneten Arbeitsspeichers zwischengespeicherte Objekte.<br /><br /> **MEMORYBROKER_FOR_STEAL** : Arbeitsspeicher an, die aus dem Pufferpool gestohlen wird. Dieser Speicher ist erst dann zur Wiederverwendung durch andere Komponenten verfügbar, wenn er durch den aktuellen Besitzer freigegeben wird.<br /><br /> **MEMORYBROKER_FOR_RESERVE** : Arbeitsspeicher für die zukünftige Verwendung durch momentan ausgeführte Anforderungen reserviert.|  
|**allocations_kb**|**bigint**|Größe des Arbeitsspeichers in Kilobyte (KB), der diesem Typ Broker zugeordnet wurde.|  
|**allocations_kb_per_sec**|**bigint**|Rate der Speicherbelegungen in Kilobyte (KB) pro Sekunde. Dieser Wert kann für die Aufhebung von Arbeitsspeicherzuordnungen negativ sein.|  
|**predicted_allocations_kb**|**bigint**|Vorhergesagte Größe des durch den Broker belegten Arbeitsspeichers. Dieser Wert basiert auf dem Speicherauslastungsmuster.|  
|**target_allocations_kb**|**bigint**|Empfohlene Größe des belegten Speichers in Kilobyte (KB) auf Basis der aktuellen Einstellungen und des Speicherverwendungsmusters. Dieser Broker sollte auf diesen Wert vergrößert oder verkleinert werden.|  
|**future_allocations_kb**|**bigint**|Prognostizierte Anzahl der Zuordnungen in Kilobyte (KB), die in den nächsten Sekunden erfolgen werden.|  
|**overall_limit_kb**|**bigint**|Die Höchstmenge an Arbeitsspeicher, die der Broker zuordnen kann, in Kilobyte (KB).|  
|**last_notification**|**nvarchar(60)**|Speicherauslastungsempfehlung auf Basis der aktuellen Einstellungen und des Verwendungsmusters. Gültige Werte sind:<br /><br /> grow<br /><br /> shrink<br /><br /> stable|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.  s  
  
## <a name="see-also"></a>Siehe auch  

  [SQL Server-Betriebssystem in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


