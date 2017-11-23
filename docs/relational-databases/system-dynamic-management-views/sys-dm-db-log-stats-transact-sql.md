---
title: Sys.dm_db_log_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/17/2017
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
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_stats dynamic management function
ms.assetid: 
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba933bad47beead99ea5f645a910b1783caa280e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdblogstats-transact-sql"></a>Sys.dm_db_log_stats (Transact-SQL)   
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Gibt Informationen und Attribute der Zusammenfassung auf Transaktionsprotokolldateien Datenbanken zurück. Verwenden Sie diese Informationen für die Überwachung und Diagnose Transaction Log SoH an.   
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>Argumente  

*Database_id* | NULL | **Standard**

Ist die ID der Datenbank. `database_id`is `int`. Gültige Eingaben sind die ID einer Datenbank `NULL`, oder `DEFAULT`. Der Standardwert ist `NULL`. `NULL`und `DEFAULT` sind gleichwertig im Kontext der aktuellen Datenbank.  
Die integrierte Funktion `DB_ID` kann angegeben werden. Bei Verwendung `DB_ID` ohne Angabe eines Datenbanknamens, muss der Kompatibilitätsgrad der aktuellen Datenbank 90 oder höher sein.

  
## <a name="tables-returned"></a>Zurückgegebene Tabellen  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |Datenbank-ID |  
|recovery_model |**nvarchar(60)**   |   Das Wiederherstellungsmodell der Datenbank. Zulässige Werte: <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   Aktuelle Start-LSN im Transaktionsprotokoll. |  
|log_end_lsn    |**nvarchar(24)**   |   LSN des letzten Protokolldatensatzes im Transaktionsprotokoll. |  
|current_vlf_sequence_number    |**bigint** |   Aktuelle VLF Sequenznummer zum Zeitpunkt der Ausführung. |  
|current_vlf_size_mb    |**float**  |   Aktuelle VLF-Größe in MB. |   
|total_vlf_count    |**bigint** |   Die Gesamtanzahl der VLFs im Transaktionsprotokoll. |  
|total_log_size_mb  |**float**  |   Gesamtgröße des Transaktionsprotokolls Protokollgröße in MB. |  
|active_vlf_count   |**bigint** |   Die Gesamtanzahl der aktiven VLFs im Transaktionsprotokoll. |  
|active_log_size_mb |**float**  |   Gesamtgröße des aktiven Transaktionsprotokolls Protokollgröße in MB. |  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   Melden Sie sich die Verzögerung Grund abschneiden. Der Wert ist identisch mit `log_reuse_wait_desc` Spalte `sys.databases`.  (Detailliertere Erklärungen dieser Werte finden Sie unter [das Transaktionsprotokoll](../../relational-databases/logs/the-transaction-log-sql-server.md)). <br />Zulässige Werte: <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />-Replikation<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />SONSTIGES VORÜBERGEHEND |  
|log_backup_time    |**datetime**   |   Transaction Log backup zuletzt. |   
|log_backup_lsn |**nvarchar(24)**   |   Letzten Sicherung des Transaktionsprotokolls LSN. |   
|log_since_last_log_backup_mb   |**float**  |   Protokollgröße in MB seit der letzten Sicherung des Transaktionsprotokolls LSN. |  
|log_checkpoint_lsn |**nvarchar(24)**   |   Letzten Prüfpunkt-LSN. |  
|log_since_last_checkpoint_mb   |**float**  |   Protokollgröße in MB seit dem letzten Prüfpunkt-LSN. |  
|log_recovery_lsn   |**nvarchar(24)**   |   Wiederherstellungs-LSN der Datenbank. Wenn `log_recovery_lsn` tritt ein, bevor die Prüfpunkt-LSN, `log_recovery_lsn` der ältesten aktiven Transaktion LSN, andernfalls wird `log_recovery_lsn` die Prüfpunkt-LSN ist. |  
|log_recovery_size_mb   |**float**  |   Protokollgröße in MB seit Protokoll Wiederherstellungs-LSN. |  
|recovery_vlf_count |**bigint** |   Gesamtanzahl der VLFs wiederhergestellt werden, wenn Failover oder ein Serverneustart aufgetreten. |  


## <a name="permissions"></a>Berechtigungen  
Erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="examples"></a>Beispiele  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>A. Bestimmen die Datenbanken in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz mit hohen Anzahl von Vlfs   
Die folgende Abfrage gibt die Datenbanken mit mehr als 100 Vlfs in den Protokolldateien. Große Anzahl von VLFs kann die Zeit in Start und Wiederherstellung, die Datenbank beeinträchtigen.

``` t-sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>B. Bestimmen die Datenbanken in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz mit transaktionsprotokollsicherungen, die älter sind als 4 Stunden   
Die folgende Abfrage ermittelt die letzten Protokoll Sicherungszeiten für die Datenbanken in der Instanz.

``` t-sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>Siehe auch  
[Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Datenbank verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)  

  
