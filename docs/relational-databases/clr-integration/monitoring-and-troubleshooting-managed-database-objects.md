---
title: Überwachung und Problembehandlung von verwalteten Datenbankobjekten | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- monitoring [CLR integration]
- performance [CLR integration]
ms.assetid: a7b589ac-104d-4b68-b4aa-9f5fc192b13d
caps.latest.revision: 18
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e5797bbbf25138658fd5db595a2cc1203046dd32
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="monitoring-and-troubleshooting-managed-database-objects"></a>Überwachung und Problembehandlung von verwalteten Datenbankobjekten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema erhalten Sie Informationen zu den Tools, die zum Überwachen und zur Problembehandlung von verwalteten Datenbankobjekten und Assemblys in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden können.  
  
## <a name="profiler-trace-events"></a>Profiler-Ablaufverfolgungsereignisse  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt die SQL-Ablaufverfolgung und Ereignisbenachrichtigungen bereit, um Ereignisse zu überwachen, die in der Datenbank-Engine auftreten. Durch Aufzeichnen angegebener Ereignisse können Sie mit der SQL-Ablaufverfolgung Leistungsprobleme behandeln, die Datenbankaktivität überwachen, Stichprobendaten für eine Testumgebung sammeln, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen und gespeicherte Prozeduren debuggen sowie Daten für Leistungsanalysetools sammeln. Weitere Informationen finden Sie unter [SQL-Ablaufverfolgung](../../relational-databases/sql-trace/sql-trace.md) und [Extended Events](../../relational-databases/extended-events/extended-events.md).  
  
|Ereignis|Description|  
|-----------|-----------------|  
|[Assembly Load-Ereignisklasse](http://msdn.microsoft.com/library/cfb0b69d-4ce0-4067-a3df-d82775e57886)|Wird verwendet, um Assembly-Ladeanforderungen (Erfolg und Fehler) zu überwachen.|  
|[SQL: BatchStarting-Ereignisklasse](../../relational-databases/event-classes/sql-batchstarting-event-class.md), [SQL: BatchCompleted (Ereignisklasse)](../../relational-databases/event-classes/sql-batchcompleted-event-class.md)|Stellt Informationen über [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batches bereit, die gestartet oder beendet wurden.|  
|[SP: Starting-Ereignisklasse](../../relational-databases/event-classes/sp-starting-event-class.md), [SP: Completed (Ereignisklasse)](../../relational-databases/event-classes/sp-completed-event-class.md)|Wird verwendet, um die Ausführung von gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozeduren zu überwachen.|  
|[SQL: StmtStarting-Ereignisklasse](../../relational-databases/event-classes/sql-stmtstarting-event-class.md), [SQL: StmtCompleted (Ereignisklasse)](../../relational-databases/event-classes/sql-stmtcompleted-event-class.md)|Wird verwendet, um die Ausführung von CLR- und [!INCLUDE[tsql](../../includes/tsql-md.md)]-Routinen zu überwachen.|  
  
## <a name="performance-counters"></a>Leistungsindikatoren  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Objekte und Leistungsindikatoren bereitgestellt, die vom Systemmonitor zum Überwachen der Aktivität von Computern, die eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführen, verwendet werden können. Ein Objekt ist eine beliebige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ressource, z. B. eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sperre oder ein Windows-Prozess. Jedes Objekt enthält einen oder mehrere Leistungsindikatoren, die verschiedene Aspekte der zu überwachenden Objekte ermitteln. Weitere Informationen finden Sie unter [Verwenden von SQL Server-Objekten](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
|Objekt|Description|  
|------------|-----------------|  
|[SQL Server, CLR-Objekt](../../relational-databases/performance-monitor/sql-server-clr-object.md)|Gesamtausführungszeit in CLR.|  
  
## <a name="windows-system-monitor-perfmonexe-counters"></a>Windows-Systemmonitor-Leistungsindikatoren (PERFMON.EXE)  
 Der Windows-Systemmonitor (PERFMON.EXE) enthält mehrere Leistungsindikatoren, die zur Überwachung der CLR-Integrationsanwendungen verwendet werden können. Die .NET CLR-Leistungsindikatoren können durch den Prozessnamen "sqlservr" gefiltert werden, um CLR-Integrationsanwendungen zu verfolgen, die derzeit ausgeführt werden.  
  
|Leistungsobjekt|Description|  
|------------------------|-----------------|  
|SqlServer:CLR|Stellt CPU-Statistiken für den Server bereit.|  
|.NET CLR-Ausnahmen|Erfasst die Anzahl der pro Sekunde ausgelösten Ausnahmen.|  
|.NET CLR-Ladevorgang|Stellt Informationen über die AppDomains und die Assemblys bereit, die im Server geladen sind.|  
|.NET CLR-Speicher|Stellt Informationen zur CLR-Speicherauslastung bereit. Dieses Objekt kann verwendet werden, um Warnungen auszugeben, wenn die Speicherauslastung zu groß wird.|  
|.NET-Datenanbieter für SQL Server|Erfasst die Anzahl der pro Sekunde hergestellten und getrennten Verbindungen. Dieses Objekt kann zum Überwachen der Datenbankaktivität verwendet werden.|  
  
## <a name="catalog-views"></a>Katalogsichten  
 Katalogsichten geben Informationen zurück, die von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank-Engine verwendet werden. Sie sollten Katalogsichten verwenden, da sie die allgemeinste Schnittstelle zu den Katalogmetadaten darstellen und die effizienteste Methode zum Abrufen, Transformieren und Präsentieren dieser Informationen in benutzerdefinierter Form bereitstellen. Alle für Benutzer verfügbaren Katalogmetadaten werden über Katalogsichten verfügbar gemacht. Weitere Informationen finden Sie unter [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).  
  
|-Katalogsicht|Description|  
|------------------|-----------------|  
|[sys.assemblies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)|Gibt Informationen über die Assemblys zurück, die in einer Datenbank registriert sind.|  
|[sys.assembly_references &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-references-transact-sql.md)|Identifiziert Assemblys, die auf andere Assemblys verweisen.|  
|[sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|Gibt Informationen über alle Funktionen, gespeicherten Prozeduren und Trigger zurück, die in einer Assembly definiert sind.|  
|[sys.assembly_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-files-transact-sql.md)|Gibt Informationen über die Assemblydateien zurück, die in der Datenbank registriert sind.|  
|[sys.assembly_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-types-transact-sql.md)|Identifiziert die benutzerdefinierten Typen (UDTs), die von einer Assembly definiert sind.|  
|[sys.module_assembly_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-module-assembly-usages-transact-sql.md)|Identifiziert die Assemblys, in denen CLR-Module definiert sind.|  
|[Sys. parameter_type_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md)|Gibt Informationen über Parameter zurück, die benutzerdefinierte Typen sind.|  
|[sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)|Identifiziert die Assembly, in der CLR-Trigger definiert ist.|  
|[sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)|Identifiziert die DDL-Trigger auf Serverebene auf einem Server, einschließlich der CLR-Trigger.|  
|[sys.type_assembly_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-type-assembly-usages-transact-sql.md)|Identifiziert die Assemblys, in denen benutzerdefinierten Typen definiert sind.|  
|[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)|Gibt das System und die benutzerdefinierten Typen zurück, die in der Datenbank registriert sind.|  
  
## <a name="dynamic-management-views"></a>Dynamische Verwaltungssichten  
 Dynamische Verwaltungssichten (DMVs) und -funktionen geben Serverstatusinformationen zurück, mit denen der Zustand einer Serverinstanz überwacht, Probleme diagnostiziert und die Leistung optimiert werden kann. Weitere Informationen finden Sie unter [dynamische Verwaltungssichten und-Funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
|DMV|Description|  
|---------|-----------------|  
|[sys.dm_clr_appdomains &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)|Stellt Informationen zu jeder Anwendungsdomäne auf dem Server bereit.|  
|[sys.dm_clr_loaded_assemblies &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)|Identifiziert jede auf dem Server registrierte verwaltete Assembly.|  
|[sys.dm_clr_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-properties-transact-sql.md)|Gibt Informationen zur gehosteten CLR zurück.|  
|[sys.dm_clr_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-tasks-transact-sql.md)|Identifiziert alle CLR-Tasks, die gerade ausgeführt werden.|  
|[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)|Gibt Informationen über die Abfrageausführungspläne zurück, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für schnellere Abfrageausführung zwischengespeichert werden.|  
|[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)|Gibt die Aggregatleistungsstatistik für zwischengespeicherte Abfragepläne zurück.|  
|[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|Gibt Informationen über jede einzelne Anforderung, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, zurück.|  
|[sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)|Gibt alle derzeit in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz aktiven Arbeitsspeicherclerks zurück, einschließlich CLR-Arbeitsspeicherclerks.|  
  
## <a name="see-also"></a>Siehe auch  
 [Programmierkonzepte für die Integration der Common Language Runtime &#40;CLR&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
