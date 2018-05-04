---
title: Sys.dm_os_job_object (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a381366960236b1881b103d68df48cee6f52e1c5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosjobobject-azure-sql-database"></a>Sys.dm_os_job_object (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Gibt eine einzelne Zeile beschreiben die Konfiguration von Job-Objekt, das SQL Server-Prozess als auch bestimmte Ressourcenverbrauch Statistiken auf der Objektebene Auftrags verwaltet. Gibt ein leeres Resultset zurück, wenn SQL Server nicht in einem Job-Objekt ausgeführt wird. 

Job-Objekt ist ein Windows-basiertes Konstrukt, die CPU, Arbeitsspeicher und e/a-Ressourcenkontrolle auf Betriebssystemebene implementiert. Weitere Informationen zu Auftragsobjekte, finden Sie unter [Auftragsobjekte](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx). 

> [!NOTE]
> Die sys.dm_os_job_object DMV derzeit möglicherweise als sys.dm_job_object angezeigt werden. Dies ist temporärer: `sys.dm_os_job_object` der permanente Name dieser DMV. 
  
|Spalten|Datentyp|Description|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|Gibt den Teil des Prozessorzyklen, die die SQL Server-Threads während jedes Intervall für die Planung verwenden können. Der Wert wird als Prozentsatz der verfügbaren Zyklen in ein Intervall für die Planung der 10000-Zyklus gemeldet. Der Wert 100 bedeutet, dass Threads CPU-Kerne verwenden, können sind z. B. der vollen Kapazität.|
|cpu_affinity_mask|**bigint**|Eine Bitmaske, beschreibt die logischen Prozessoren können SQL Server-Prozess in prozessorgruppe. Beispielsweise Cpu_affinity_mask 255 (1111 1111 binär) bedeutet, dass die ersten acht logische Prozessoren genutzt werden.|
|cpu_affinity_group|**int**|Die Anzahl der Gruppe "Prozessor", die von SQL Server verwendet wird.|
|memory_limit_mb|**bigint**|Die maximale Menge des zugesicherten Arbeitsspeichers in MB, der alle Prozesse in die Job-Objekt, einschließlich SQL Server, kumulativ verwenden können.| 
|process_memory_limit_mb |**bigint**|Die maximale Menge des zugesicherten Arbeitsspeichers in MB, der einen einzelner Prozess in die Job-Objekt, z. B. SQL-Server verwenden können.|
|workingset_limit_mb |**bigint**|Die Höchstmenge des Speichers in MB, der das SQL Server-Workingset verwenden kann.|
|non_sos_mem_gap_mb|**bigint**|Die Menge des Arbeitsspeichers in MB "," ist für Threadstapel, DLLs und andere nicht SOS-speicherbelegungen reservieren. SOS-Zielspeicher ist der Unterschied zwischen `process_memory_limit_mb` und `non_sos_mem_gap_mb`.| 
|low_mem_signal_threshold_mb|**bigint**|Ein Schwellenwert zur in MB. Wenn die Menge des verfügbaren Arbeitsspeichers für das Auftragsobjekt unter diesem Schwellenwert liegt, wird ein wenig Arbeitsspeicher-Benachrichtigung-Signal an den SQL Server-Prozess gesendet. |
|total_user_time|**bigint**|Die Gesamtanzahl von 100 ns Ticks, die Threads in die Job-Objekt im Benutzermodus benötigt haben, seit der Erstellung der Job-Objekt. |
|total_kernel_time |**bigint**|Die Gesamtanzahl von 100 ns Ticks, die Threads in die Job-Objekt im Kernel-Modus benötigt haben, seit die Job-Objekt erstellt wurde. |
|write_operation_count |**bigint**|Die Gesamtanzahl der schreiben e/a-Vorgänge auf lokalen Datenträgern, die von SQL Server ausgegeben werden, da die Job-Objekt erstellt wurde. |
|read_operation_count |**bigint**|Die Gesamtanzahl der e/a-Lesevorgänge auf lokalen Datenträgern, die von SQL Server ausgegeben werden, da die Job-Objekt erstellt wurde. |
|peak_process_memory_used_mb|**bigint**|Höhepunktarbeitsspeichers des Arbeitsspeichers in MB, der ein einzelnen Prozess, in die Job-Objekt, z. B. SQL Server, wurde verwendet, da die Job-Objekt erstellt wurde.| 
|peak_job_memory_used_mb|**bigint**|Höhepunktarbeitsspeichers des Arbeitsspeichers in MB, der alle Prozesse im Auftragsobjekt kumulativ, da die Job-Objekt verwendet haben erstellt wurde.|
  
## <a name="permissions"></a>Berechtigungen  
Auf SQL-Datenbank verwaltete Instanz erfordert `VIEW SERVER STATE` Berechtigung. Auf SQL-Datenbank erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.  
 
## <a name="see-also"></a>Siehe auch  

Weitere Informationen zu verwalteten Instanzen finden Sie unter [verwalteten SQL-Datenbankinstanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
  
