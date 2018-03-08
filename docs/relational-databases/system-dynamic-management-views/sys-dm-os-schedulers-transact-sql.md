---
title: DM_OS_SCHEDULERS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_schedulers
- sys.dm_os_schedulers_TSQL
- sys.dm_os_schedulers
- dm_os_schedulers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_schedulers dynamic management view
ms.assetid: 3a09d81b-55d5-416f-9cda-1a3a5492abe0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aa32726893d196cc4c2830e79703f5583d661793
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosschedulers-transact-sql"></a>sys.dm_os_schedulers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile pro Zeitplanungsmodul in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück, wobei jedes Zeitplanungsmodul einem einzelnen Prozessor zugeordnet ist. Mithilfe dieser Sicht können Sie den Zustand eines Zeitplanungsmoduls überwachen oder Endlostasks identifizieren.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_schedulers**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|scheduler_address|**varbinary(8)**|Speicheradresse des Zeitplanungsmoduls. Lässt keine NULL-Werte zu.|  
|parent_node_id|**int**|ID des Knotens, zu dem das Zeitplanungsmodul gehört, der auch als übergeordneter Knoten bezeichnet wird. Dies stellt einen NUMA-Knoten (Non-Uniform Memory Access) dar. Lässt keine NULL-Werte zu.|  
|scheduler_id|**int**|ID des Zeitplanungsmoduls. Alle Zeitplanungsmodule, die zum Ausführen regulärer Abfragen verwendet werden, weisen IDs unter 1048576 auf. Zeitplanungsmodule mit IDs größer oder gleich 1048576 werden intern von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, wie z. B. das Zeitplanungsmodul für dedizierte Administratorverbindungen. Lässt keine NULL-Werte zu.|  
|cpu_id|**smallint**|Die zugewiesene CPU-ID des Zeitplanungsmoduls.<br /><br /> Lässt keine NULL-Werte zu.<br /><br /> **Hinweis:** 255 nicht keine Affinität an, wie in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. See [sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md) for additional affinity information.|  
|status|**nvarchar(60)**|Zeigt den Status des Zeitplanungsmoduls an. Folgende Werte sind möglich:<br /><br /> -   HIDDEN ONLINE<br />-AUSGEBLENDET OFFLINE<br />-SICHTBAR ONLINE<br />-SICHTBAR OFFLINE<br />-ONLINE SICHTBAR (DAC)<br />-   HOT_ADDED<br /><br /> Lässt keine NULL-Werte zu.<br /><br /> Zeitplanungsmodule im Status HIDDEN werden zur Verarbeitung von Anforderungen verwendet, die intern für [!INCLUDE[ssDE](../../includes/ssde-md.md)] sind. Zeitplanungsmodule im Status VISIBLE dienen zur Verarbeitung von Benutzeranforderungen.<br /><br /> Zeitplanungsmodule im Status OFFLINE sind Prozessoren zugeordnet, die in der Affinitätsmaske als offline markiert sind und daher nicht zur Verarbeitung von Anforderungen verwendet werden. Zeitplanungsmodule im Status ONLINE sind Prozessoren zugeordnet, die in der Affinitätsmaske als online markiert sind und zur Verarbeitung von Threads zur Verfügung stehen.<br /><br /> DAC bezeichnet das Zeitplanungsmodul, das über eine dedizierte Administratorverbindung ausgeführt wird.<br /><br /> HOT ADDED gibt an, dass die Zeitplanungsmodule als Reaktion auf ein Hinzufügen von CPUs im laufenden Systembetrieb hinzugefügt wurden.|  
|is_online|**bit**|Wurde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] so konfiguriert, dass nur einige der verfügbaren Prozessoren verwendet werden, kann diese Konfiguration bedeuten, dass einige Zeitplanungsmodule Prozessoren zugeordnet werden, die nicht in der Affinitätsmaske enthalten sind. In diesem Fall gibt diese Spalte 0 zurück. Dieser Wert bedeutet, dass das Zeitplanungsmodul nicht für die Verarbeitung von Abfragen oder Batches verwendet wird.<br /><br /> Lässt keine NULL-Werte zu.|  
|is_idle|**bit**|1 = Das Zeitplanungsmodul befindet sich im Leerlauf. Zurzeit werden keine Arbeitsthreads ausgeführt. Lässt keine NULL-Werte zu.|  
|preemptive_switches_count|**int**|Häufigkeit, mit der Arbeitsthreads in diesem Zeitplanungsmodul in den präemptiven Modus gewechselt sind.<br /><br /> Für die Ausführung von Code außerhalb von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (z. B. erweiterte gespeicherte Prozeduren und verteilte Abfragen) muss ein Thread außerhalb der Steuerung des nicht präemptiven Zeitplanungsmoduls ausgeführt werden. Dazu wechselt ein Arbeitsthread in den präemptiven Modus.|  
|context_switches_count|**int**|Anzahl der Kontextwechsel in diesem Zeitplanungsmodul. Lässt keine NULL-Werte zu.<br /><br /> Damit andere Arbeitsthreads ausgeführt werden können, muss der aktuelle Arbeitsthread die Steuerung des Zeitplanungsmoduls freiwillig aufgeben oder den Kontext wechseln.<br /><br /> **Hinweis:** , wenn ein Arbeitsthread im Zeitplanungsmodul und sich selbst in der ausführbaren Warteschlange fügt und dann keine anderen Arbeitsthreads gefunden, wird der Arbeitsthread wählen selbst. In diesem Fall wird context_switches_count nicht aktualisiert, yield_count wird jedoch aktualisiert.|  
|idle_switches_count|**int**|Häufigkeit, mit der das Zeitplanungsmodul im Leerlauf auf ein Ereignis gewartet hat. Diese Spalte entspricht context_switches_count. Lässt keine NULL-Werte zu.|  
|current_tasks_count|**int**|Anzahl von aktuellen Tasks, die diesem Zeitplanungsmodul zugeordnet sind. Dazu gehören die folgenden:<br /><br /> – Aufgaben, die ein Worker ihrer Ausführung warten.<br />– Aufgaben, die zurzeit warten oder ausgeführt werden (Status SUSPENDED oder RUNNABLE).<br /><br /> Nach Abschluss eines Tasks wird diese Anzahl verringert. Lässt keine NULL-Werte zu.|  
|runnable_tasks_count|**int**|Anzahl von Arbeitsthreads mit zugewiesenen Tasks, die darauf warten, in die ausführbare Warteschlange eingereiht zu werden. Lässt keine NULL-Werte zu.|  
|current_workers_count|**int**|Anzahl von diesem Zeitplanungsmodul zugeordneten Arbeitsthreads. Dies schließt Arbeitsthreads ein, die keinem Task zugeordnet sind. Lässt keine NULL-Werte zu.|  
|active_workers_count|**int**|Anzahl der aktiven Arbeitsthreads. Ein aktiver Arbeitsthread ist nie präemptiv, muss über einen zugewiesenen Task verfügen und wird entweder ausgeführt, ist ausführbar oder wurde angehalten. Lässt keine NULL-Werte zu.|  
|work_queue_count|**bigint**|Anzahl von Tasks in der ausstehenden Warteschlange. Diese Tasks warten darauf, von einem Arbeitsthread abgerufen zu werden. Lässt keine NULL-Werte zu.|  
|pending_disk_io_count|**int**|Anzahl von ausstehenden E/A-Vorgängen, die abgeschlossen werden sollen. Jedes Zeitplanungsmodul verfügt über eine Liste ausstehender E/A-Vorgänge, die überprüft werden, um bei einem Kontextwechsel zu bestimmen, ob sie abgeschlossen wurden. Die Anzahl wird um Eins inkrementiert, wenn die Anforderung eingefügt wird. Diese Anzahl wird um Eins verringert, wenn die Anforderung abgeschlossen ist. Diese Anzahl gibt nicht den Status der E/A-Vorgänge an. Lässt keine NULL-Werte zu.|  
|load_factor|**int**|Interner Wert, der die Belastung dieses Zeitplanungsmoduls angibt. Mit diesem Wert wird bestimmt, ob ein neuer Task an dieses Zeitplanungsmodul oder ein anderes Zeitplanungsmodul gerichtet werden soll. Dieser Wert eignet sich vor allem zu Debugzwecken, wenn die Belastung der Zeitplanungsmodule nicht gleichmäßig verteilt zu sein scheint. Die Entscheidung über die Weiterleitung basiert auf der Belastung des Zeitplanungsmoduls. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet auch einen Ladefaktor für Knoten und Zeitplanungsmodule, um die optimale Ressourcenquelle einfacher zu bestimmen. Nach dem Einreihen eines Tasks in die Warteschlange wird der Ladefaktor erhöht. Nach Abschluss eines Tasks wird der Ladefaktor verringert. Mithilfe von Ladefaktoren kann das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Betriebssystem (SQLOS) die Arbeitsauslastung besser verteilen. Lässt keine NULL-Werte zu.|  
|yield_count|**int**|Interner Wert zur Angabe des Fortschritts in diesem Zeitplanungsmodul. Mit diesem Wert wird von der Zeitplanungsmodul-Überwachung bestimmt, ob im Zeitplanungsmodul ein Arbeitsthread vorhanden ist, dessen Position nicht rechtzeitig für andere Arbeitsthreads freigegeben wird. Dieser Wert gibt nicht an, dass der Arbeitsthread oder Task in einen neuen Arbeitsthread gewechselt hat. Lässt keine NULL-Werte zu.|  
|last_timer_activity|**bigint**|Der letzte Zeitpunkt in CPU-Takten, zu dem die Zeitgeberwarteschlange des Zeitplanungsmoduls vom Zeitplanungsmodul überprüft wurde. Lässt keine NULL-Werte zu.|  
|failed_to_create_worker|**bit**|Bei der Einstellung 1 konnte kein neuer Arbeitsthread in diesem Zeitplanungsmodul erstellt werden. Dies tritt in der Regel aufgrund von Speicherbeschränkungen auf. Lässt NULL-Werte zu.|  
|active_worker_address|**varbinary(8)**|Speicheradresse des derzeit aktiven Arbeitsthreads. Lässt NULL-Werte zu. Weitere Informationen finden Sie unter [dm_os_workers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|memory_object_address|**varbinary(8)**|Speicheradresse des Speicherobjekts des Zeitplanungsmoduls. Lässt keine NULL-Werte zu.|  
|task_memory_object_address|**varbinary(8)**|Speicheradresse des Speicherobjekts des Tasks. Lässt keine NULL-Werte zu. Weitere Informationen finden Sie unter [Sys. dm_os_memory_objects &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).|  
|quantum_length_us|**bigint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] Macht das von SQLOS verwendete Zeitplanungsmodul-Quantum verfügbar.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.   
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-monitoring-hidden-and-nonhidden-schedulers"></a>A. Überwachend ausgeblendeter und eingeblendeter Zeitplanungsmodule  
 In der folgenden Abfrage wird der Status von Arbeitsthreads und Tasks in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in allen Zeitplanungsmodulen ausgegeben. Diese Abfrage wurde auf einem Computersystem mit folgenden Eigenschaften ausgeführt:  
  
-   Zwei Prozessoren (CPUs)  
  
-   Zwei (NUMA-)Knoten  
  
-   Eine CPU pro NUMA-Knoten  
  
-   Auf `0x03` festgelegte Affinitätsmaske.  
  
```  
SELECT  
    scheduler_id,  
    cpu_id,  
    parent_node_id,  
    current_tasks_count,  
    runnable_tasks_count,  
    current_workers_count,  
    active_workers_count,  
    work_queue_count  
  FROM sys.dm_os_schedulers;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
scheduler_id cpu_id parent_node_id current_tasks_count  
------------ ------ -------------- -------------------  
0            1      0              9                    
257          255    0              1                    
1            0      1              10                   
258          255    1              1                    
255          255    32             2                    
  
runnable_tasks_count current_workers_count  
-------------------- ---------------------  
0                    11                     
0                    1                      
0                    18                     
0                    1                      
0                    3                      
  
active_workers_count work_queue_count  
-------------------- --------------------  
6                    0  
1                    0  
8                    0  
1                    0  
1                    0  
```  
  
 Die Ausgabe stellt die folgenden Informationen bereit:  
  
-   Es gibt fünf Zeitplanungsmodule. Zwei Zeitplanungsmodule besitzen einen ID-Wert < 1048576. Zeitplanungsmodule mit einer ID >= 1048576 werden als ausgeblendete Zeitplanungsmodule bezeichnet. Das Zeitplanungsmodul `255` stellt die dedizierte Administratorverbindung (Dedicated Administrator Connection, DAC) dar. Es gibt ein DAC-Zeitplanungsmodul pro Instanz. Ressourcenmonitore, die knappen Arbeitsspeicher koordinieren, verwenden die Zeitplanungsmodule `257` und `258`, einen pro NUMA-Knoten.  
  
-   In der Ausgabe gibt es 23 aktive Tasks. Zu diesen Tasks gehören Benutzeranforderungen sowie Ressourcenverwaltungstasks, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wurden. Beispiele für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tasks sind RESOURCE MONITOR (einer pro NUMA-Knoten), LAZY WRITER (einer pro NUMA-Knoten), LOCK MONITOR, CHECKPOINT und LOG WRITER.  
  
-   Der NUMA-Knoten `0` wird der CPU `1` zugeordnet und der NUMA-Knoten `1` der CPU `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] startet in der Regel in einem anderen NUMA-Knoten als dem Knoten 0.  
  
-   Wenn `runnable_tasks_count` den Wert `0` zurückgibt, gibt es keine aktiv ausgeführten Tasks. Es sind jedoch möglicherweise aktive Sitzungen vorhanden.  
  
-   Dem Zeitplanungsmodul `255`, das DAC darstellt, sind `3` Arbeitsthreads zugeordnet. Diese Arbeitsthreads werden beim Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugeordnet und nicht geändert. Diese Arbeitsthreads werden nur zur Verarbeitung von DAC-Abfragen verwendet. Die beiden Tasks in diesem Zeitplanungsmodul stellen einen Verbindungs-Manager und einen im Leerlauf befindlichen Arbeitsthread dar.  
  
-   `active_workers_count`Stellt alle Arbeitsthreads, die über zugeordnete Tasks verfügen und mit nicht präemptiven Modus ausgeführt wird. Einige Tasks, z. B. zur Netzwerküberwachung, werden mit präemptiver Zeitplanung ausgeführt.  
  
-   Verborgene Zeitplanungsmodule verarbeiten keine typischen Benutzeranforderungen. Das DAC-Zeitplanungsmodul ist die Ausnahme. Dieses DAC-Zeitplanungsmodul verfügt über einen Thread zum Verarbeiten von Anforderungen.  
  
### <a name="b-monitoring-nonhidden-schedulers-in-a-busy-system"></a>B. Überwachen von eingeblendeten Zeitplanungsmodulen in einem ausgelasteten System  
 In der folgenden Abfrage wird der Status von stark ausgelasteten nicht verborgenen Zeitplanungsmodulen angezeigt, bei denen mehr Anforderungen vorhanden sind, als von verfügbaren Arbeitsthreads verarbeitet werden können. In diesem Beispiel werden 256 Arbeitsthreads Tasks zugewiesen. Einige Tasks warten auf die Zuweisung zu einem Arbeitsthread. Eine niedrige Anzahl von ausführbaren Tasks impliziert, dass mehrere Tasks auf eine Ressource warten.  
  
> [!NOTE]  
>  Sie können den Status von Arbeitsthreads herausfinden, indem Sie sys.dm_os_workers abfragen. Weitere Informationen finden Sie unter [dm_os_workers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).  
  
 So sieht die Abfrage aus:  
  
```  
SELECT  
    scheduler_id,  
    cpu_id,  
    current_tasks_count,  
    runnable_tasks_count,  
    current_workers_count,  
    active_workers_count,  
    work_queue_count  
  FROM sys.dm_os_schedulers  
  WHERE scheduler_id < 255;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
scheduler_id current_tasks_count runnable_tasks_count  
------------ ------------------- --------------------  
0            144                 0                     
1            147                 1                     
  
current_workers_count active_workers_count work_queue_count  
--------------------- -------------------- --------------------  
128                   125                  16  
128                   126                  19  
```  
  
 Im Vergleich dazu werden im folgenden Ergebnis mehrere ausführbare Tasks angezeigt, wobei kein Task darauf wartet, einen Arbeitsthread zu erhalten. Der Wert von `work_queue_count` beträgt für beide Zeitplanungsmodule `0`.  
  
```  
scheduler_id current_tasks_count runnable_tasks_count  
------------ ------------------- --------------------  
0            107                 98                    
1            110                 100                   
  
current_workers_count active_workers_count work_queue_count  
--------------------- -------------------- --------------------  
128                   104                  0  
128                   108                  0  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Betriebssystem in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


