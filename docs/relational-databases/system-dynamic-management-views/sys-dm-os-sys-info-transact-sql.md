---
title: Sys. dm_os_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_sys_info_TSQL
- dm_os_sys_info
- dm_os_sys_info_TSQL
- sys.dm_os_sys_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_info dynamic management view
- time [SQL Server], instance started
- starting time
ms.assetid: 20f6bc9c-839a-4fa4-b3f3-a6c47d1b69af
caps.latest.revision: 57
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d5284112257c5d1c2d23f354ec7690fab6abb90b
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmossysinfo-transact-sql"></a>sys.dm_os_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt verschiedene nützliche Informationen zum Computer und den Ressourcen zurück, die für [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] zur Verfügung stehen und verwendet werden.  
  
> **Hinweis:** von Aufrufen [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_sys_info**.  
  
|Spaltenname|Datentyp|Beschreibung und versionsspezifische Hinweise |  
|-----------------|---------------|-----------------|  
|**cpu_ticks**|**bigint**|Gibt die aktuelle CPU-Taktanzahl an. Die CPU-Takte stammen vom RDTSC-Leistungsindikator des Prozessors. Es handelt sich um eine monoton steigende Zahl. Lässt keine NULL-Werte zu.|  
|**ms_ticks**|**bigint**|Gibt die Anzahl der Millisekunden seit dem Starten des Computers an. Lässt keine NULL-Werte zu.|  
|**cpu_count**|**int**|Gibt die Anzahl der logischen CPUs im System an. Lässt keine NULL-Werte zu.|  
|**hyperthread_ratio**|**int**|Gibt das Verhältnis der Anzahl von logischen oder physischen Kernen an, die von einem physischen Prozessorpaket verfügbar gemacht werden. Lässt keine NULL-Werte zu.|  
|**physical_memory_in_bytes**|**bigint**|**Gilt für: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Gibt die Gesamtmenge des physischem Speichers auf dem Computer an. Lässt keine NULL-Werte zu.|  
|**physical_memory_kb**|**bigint**|**Gilt für: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Gibt die Gesamtmenge des physischem Speichers auf dem Computer an. Lässt keine NULL-Werte zu.|  
|**virtual_memory_in_bytes**|**bigint**|**Gilt für: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Umfang des virtuellen Arbeitsspeichers, der dem Prozess im Benutzermodus zur Verfügung steht. Damit kann bestimmt werden, ob SQL Server mithilfe eines 3-GB-Schalters gestartet wurde.|  
|**virtual_memory_kb**|**bigint**|**Gilt für: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Gibt die Gesamtmenge des virtuellem Adressraums für den Prozess im Benutzermodus an. Lässt keine NULL-Werte zu.|  
|**bpool_commited**|**int**|**Gilt für: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Stellt den Arbeitsspeicher im Speicher-Manager in Kilobyte (KB) dar, für den ein Commit ausgeführt wurde. Reservierter Arbeitsspeicher im Speicher-Manager ist nicht eingeschlossen. Lässt keine NULL-Werte zu.|  
|**committed_kb**|**int**|**Gilt für: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Stellt den Arbeitsspeicher im Speicher-Manager in Kilobyte (KB) dar, für den ein Commit ausgeführt wurde. Reservierter Arbeitsspeicher im Speicher-Manager ist nicht eingeschlossen. Lässt keine NULL-Werte zu.|  
|**bpool_commit_target**|**int**|**Gilt für: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Stellt den Arbeitsspeicher in Kilobytes (KB) dar, der von SQL Server-Speicher-Manager genutzt werden kann.|  
|**committed_target_kb**|**int**|**Gilt für: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Stellt den Arbeitsspeicher in Kilobytes (KB) dar, der von SQL Server-Speicher-Manager genutzt werden kann. Die Zielmenge wird anhand einer Vielzahl von Eingaben berechnet, darunter die folgenden:<br /><br /> -der aktuelle Status des Systems einschließlich der Auslastung<br /><br /> -der von aktuellen Prozessen angeforderten Arbeitsspeichers<br /><br /> -die Menge an Arbeitsspeicher auf dem Computer installiert<br /><br /> -Konfigurationsparameter<br /><br /> Wenn **Committed_target_kb** ist größer als **Committed_kb**, der Speicher-Manager versucht, zusätzlichen Arbeitsspeicher zu erhalten. Wenn **Committed_target_kb** ist kleiner als **Committed_kb**, versucht der Speicher-Manager so verkleinern Sie die Größe des Arbeitsspeichers, die ein Commit ausgeführt. Die **Committed_target_kb** enthält immer entnommenen und reservierten Arbeitsspeicher. Lässt keine NULL-Werte zu.|  
|**bpool_visible**|**int**|**Gilt für: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Anzahl von 8-KB-Puffern im Pufferpool, die im virtuellen Prozessadressraum direkt adressierbar sind. Wenn AWE (Address Windowing Extensions) nicht verwendet wird und wenn der Pufferpool sein Arbeitsspeicherziel erreicht hat (bpool_committed = bpool_commit_target), entspricht der Wert von bpool_visible dem Wert von bpool_committed. Wenn AWE in einer 32-Bit-Version von SQL Server verwendet wird, stellt bpool_visible die Größe des AWE-Zuordnungsfensters dar, das verwendet wird, um auf den vom Pufferpool zugewiesenen physischen Speicher zuzugreifen. Da die Größe des Zuordnungsfensters durch den Prozessadressraum gebunden ist, ist der sichtbare Umfang geringer als der zugesicherte Umfang, und er kann durch interne Komponenten weiter reduziert werden, die zu anderen Zwecken als für Datenbankseiten Arbeitsspeicher belegen. Ist der Wert von bpool_visible zu niedrig, treten möglicherweise Fehler aufgrund von nicht genügend Arbeitsspeicher auf.|  
|**visible_target_kb**|**int**|**Gilt für: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Entspricht dem **Committed_target_kb**. Lässt keine NULL-Werte zu.|  
|**stack_size_in_bytes**|**int**|Gibt die Größe der Aufrufliste für jeden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellten Thread an. Lässt keine NULL-Werte zu.|  
|**os_quantum**|**bigint**|Stellt das Quantum für einen nicht präemptiven Task dar, gemessen in Millisekunden. Quantum (in Sekunden) = **Os_quantum** / CPU-Takt. Lässt keine NULL-Werte zu.|  
|**os_error_mode**|**int**|Gibt den Fehlermodus für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess an. Lässt keine NULL-Werte zu.|  
|**os_priority_class**|**int**|Gibt die Prioritätsklasse für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess an. NULL-Werte sind zulässig.<br /><br /> 32 = normal (Fehlerprotokoll besagt, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei normaler Prioritätsbasis (= 7) startet.)<br /><br /> 128 = Hoch (Fehlerprotokoll besagt, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf hoher Prioritätsbasis ausgeführt wird.)  (=13).)<br /><br /> Weitere Informationen finden Sie unter [Configure the priority boost Server Configuration Option](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md).|  
|**max_workers_count**|**int**|Stellt die maximale Anzahl von Arbeitsthreads dar, die erstellt werden können. Lässt keine NULL-Werte zu.|  
|**scheduler_count**|**int**|Stellt die Anzahl der im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess konfigurierten Benutzer-Zeitplanungsmodule dar. Lässt keine NULL-Werte zu.|  
|**scheduler_total_count**|**int**|Stellt die Gesamtanzahl der Zeitplanungsmodule in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dar. Lässt keine NULL-Werte zu.|  
|**deadlock_monitor_serial_number**|**int**|Gibt die ID der aktuellen Deadlocküberwachungssequenz an. Lässt keine NULL-Werte zu.|  
|**sqlserver_start_time_ms_ticks**|**bigint**|Stellt die **Ms_tick** Anzahl beim [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zuletzt gestartet wurde. Vergleicht diesen Wert mit dem aktuellen Wert in der ms_ticks-Spalte. Lässt keine NULL-Werte zu.|  
|**sqlserver_start_time**|**datetime**|Gibt das Datum und die Uhrzeit an, wann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum letzten Mal gestartet wurde. Lässt keine NULL-Werte zu.|  
|**affinity_type**|**int**|**Gilt für: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]**  über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt den Typ der Server-CPU-Prozessaffinität an, die derzeit verwendet wird. Lässt keine NULL-Werte zu. Weitere Informationen finden Sie unter [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md).<br /><br /> 1 = MANUELL<br /><br /> 2 = AUTO|  
|**affinity_type_desc**|**varchar(60)**|**Gilt für: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Beschreibt die **Affinity_type** Spalte. Lässt keine NULL-Werte zu.<br /><br /> MANUELL = Die Affinität wurde für mindestens eine CPU festgelegt.<br /><br /> AUTO = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann Threads zwischen CPUs frei verschieben.|  
|**process_kernel_time_ms**|**bigint**|**Gilt für: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] über [! INCLUDE [SsCurrent]**(.. /Token/ssCurrent_md.MD)].<br /><br /> Benötigte Gesamtzeit in Millisekunden für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Threads im Kernelmodus. Dieser Wert kann größer als eine einzelne Prozessoruhr sein, da er die Zeit für alle Prozessoren auf dem Server enthält. Lässt keine NULL-Werte zu.|  
|**process_user_time_ms**|**bigint**|**Gilt für: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Benötigte Gesamtzeit in Millisekunden für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Threads im Benutzermodus. Dieser Wert kann größer als eine einzelne Prozessoruhr sein, da er die Zeit für alle Prozessoren auf dem Server enthält. Lässt keine NULL-Werte zu.|  
|**time_source**|**int**|**Gilt für: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Gibt die API an, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird, um die Wanduhrzeit abzurufen. Lässt keine NULL-Werte zu.<br /><br /> 0 = QUERY_PERFORMANCE_COUNTER<br /><br /> 1 = MULTIMEDIA_TIMER|  
|**time_source_desc**|**nvarchar(60)**|**Gilt für: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Beschreibt die **Time_source** Spalte. Lässt keine NULL-Werte zu.<br /><br /> QUERY_PERFORMANCE_COUNTER = die [QueryPerformanceCounter](http://go.microsoft.com/fwlink/?LinkId=163095) API ruft die wanduhrzeit ab.<br /><br /> MULTIMEDIA_TIMER = die [multimedia-Zeitgeber](http://go.microsoft.com/fwlink/?LinkId=163094) -API, die wanduhrzeit abruft.|  
|**virtual_machine_type**|**int**|**Gilt für: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Gibt an, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einer virtualisierten Umgebung ausgeführt wird.  Lässt keine NULL-Werte zu.<br /><br /> 0 = NONE<br /><br /> 1 = HYPERVISOR<br /><br /> 2 = OTHER|  
|**virtual_machine_type_desc**|**nvarchar(60)**|**Gilt für: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Beschreibt die **Virtual_machine_type** Spalte. Lässt keine NULL-Werte zu.<br /><br /> NONE = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht auf einem virtuellen Computer ausgeführt wird.<br /><br /> HYPERVISOR = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird in einem Hypervisor ausgeführt, der eine hardwareunterstützte Virtualisierung bedeutet. Bei der Installation der Hyper_V-Rolle hostet der Hypervisor das Betriebssystem, damit eine Serverinstanz, die auf dem Hostbetriebssystem im Hypervisor ausgeführt wird.<br /><br /> OTHER = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird auf einem virtuellen Computer ausgeführt, der keinen Hardware-Assistenten z. B. Microsoft Virtual PC verwendet.|  
|**softnuma_configuration**|**int**|**Gilt für: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Gibt an, dass die Möglichkeit NUMA-Knoten konfiguriert sind. Lässt keine NULL-Werte zu.<br /><br /> 0 = OFF gibt an Standardeinstellung Hardware<br /><br /> 1 = automatische Soft-NUMA<br /><br /> 2 = manuellen Soft-NUMA über Registrierung|  
|**softnuma_configuration_desc**|**nvarchar(60)**|**Gilt für: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> OFF = Soft-NUMA-Funktion ist deaktiviert<br /><br /> AUF SQL Server automatisch = bestimmt die Größe der NUMA-Knoten für den Soft-NUMA<br /><br /> MANUELL = manuell konfigurierten Soft-NUMA|
|**process_physical_affinity**|**nvarchar(3072)** |**Gilt für: ab [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]** .<br /><br />Informationen noch bereitgestellt. |
|**sql_memory_model**|**int**|**Gilt für: [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4 und ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1**.<br /><br />Gibt das Zuweisen von Arbeitsspeicher von SQL Server verwendeten Arbeitsspeicher-Modell. Lässt keine NULL-Werte zu.<br /><br />1 = konventionellen Arbeitsspeicher gespeicherten Modells<br />2 = Lock Pages in Memory<br /> 3 = große Seiten im Speicher|
|**sql_memory_model_desc**|**nvarchar(120)**|**Gilt für: [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4 und ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1**.<br /><br />Gibt das Zuweisen von Arbeitsspeicher von SQL Server verwendeten Arbeitsspeicher-Modell. Lässt keine NULL-Werte zu.<br /><br />**HERKÖMMLICHE** = SQL Server verwendeten Modells konventionellen Arbeitsspeicher belegt werden. Dies ist die Standardmodell Sql-Speicher, wenn SQL Server-Dienstkonto nicht Sperren von Seiten im Speicher Berechtigungen während des Starts verfügt.<br />**LOCK_PAGES** = SQL Server verwendet Sperren von Seiten im Arbeitsspeicher belegt werden. Dies ist der Standard-Sql-Speicher-Manager, wenn SQL Server-Dienstkonto über Sperren von Seiten im Speicher-Berechtigung verfügen, während des Starts von SQL Server.<br /> **LARGE_PAGES** = SQL Server verwendeten große Seiten im Arbeitsspeicher belegt werden. SQL Server verwendete große Seiten Allocator Speicher nur mit Enterprise Edition, wenn SQL Server-Dienstkonto Sperren von Seiten im Speicher-Berechtigung besitzen, während des Serverstarts und wenn die Trace Flag 834 aktiviert ist.|
|**pdw_node_id**|**int**|**Gilt für: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
|**socket_count** |**int** | **Gilt für: ab [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]** .<br /><br />Gibt die Anzahl von prozessorsockets verfügbar im System an. |  
|**cores_per_socket** |**int** | **Gilt für: ab [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].**.<br /><br />Gibt die Anzahl der Prozessoren pro Socket verfügbar im System an. |  
|**numa_node_count** |**int** | **Gilt für: ab [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].**.<br /><br />Gibt die Anzahl der verfügbaren Numa-Knoten auf dem System an. Diese Spalte enthält die physischen Numa-Knoten als auch von soft-Numa-Knoten. |  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   

## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



