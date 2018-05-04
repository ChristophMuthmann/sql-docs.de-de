---
title: Sys.dm_db_log_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: 4
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e791e9d48e6dad1ab3514caa1d1faa0fb3c259a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbloginfo-transact-sql"></a>Sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Gibt [virtuelle Protokolldatei (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) Informationen des Transaktionsprotokolls. Beachten Sie, dass es sich bei allen Transaktionsprotokolldateien in der Tabellenausgabe kombiniert werden. Jede Zeile in der Ausgabe eine VLF im Transaktionsprotokoll darstellt und bietet Informationen zu diesem VLF im Protokoll.

## <a name="syntax"></a>Syntax  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>Argumente  
 *Database_id* | NULL | STANDARDWERT  
 Ist die ID der Datenbank. *database_id* ist vom Datentyp **int**. Gültige Eingaben sind die ID einer Datenbank, NULL oder DEFAULT. Die Standardeinstellung ist NULL. NULL und DEFAULT sind gleichwertig im Kontext der aktuellen Datenbank.
 
 Geben Sie NULL an, wenn VLF-Informationen der aktuellen Datenbank zurückgegeben.

 Die integrierte Funktion [DB_ID](../../t-sql/functions/db-id-transact-sql.md) kann angegeben werden. Bei Verwendung `DB_ID` ohne Angabe eines Datenbanknamens, muss der Kompatibilitätsgrad der aktuellen Datenbank 90 oder höher sein.  

## <a name="table-returned"></a>Zurückgegebene Tabelle  

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Datenbank-ID|
|file_id|**smallint**|Datei-Id des Transaktionsprotokolls.|  
|vlf_begin_offset|**bigint** |Speicherort der Offset der [virtuelle Protokolldatei (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) vom Anfang der Transaktionsprotokolldatei.|
|vlf_size_mb |**float** |[virtuelle Protokolldatei (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) Größe in MB "," auf 2 Dezimalstellen gerundet.|     
|vlf_sequence_number|**bigint** |[virtuelle Protokolldatei (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) Sequenznummer in der Reihenfolge erstellt. Zur eindeutigen Identifizierung der VLFs in Protokolldatei verwendet.|
|vlf_active|**bit** |Gibt an, ob [virtuelle Protokolldatei (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) verwendet wird, oder nicht. <br />0 – wird VLF nicht verwendet.<br />1 - VLF ist aktiv.|
|vlf_status|**int** |Status der [virtuelle Protokolldatei (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). Mögliche Werte sind: <br />0 – VLF ist inaktiv <br />1 - VLF wird initialisiert, aber nicht verwendete <br /> 2 – VLF ist aktiv.|
|vlf_parity|**tinyint** |Parität [virtuelle Protokolldatei (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). Wird intern verwendet, um das Ende des Protokolls in eine VLF zu bestimmen.|
|vlf_first_lsn|**nvarchar(48)** |[Protokollsequenznummer (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) des ersten Protokolldatensatzes in der [virtuelle Protokolldatei (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).|
|vlf_create_lsn|**nvarchar(48)** |[Protokollsequenznummer (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) des Protokolls zu zeichnen, erstellt der [virtuelle Protokolldatei (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).|

## <a name="remarks"></a>Hinweise
Die `sys.dm_db_log_info` dynamische Verwaltungsfunktion ersetzt die `DBCC LOGINFO` Anweisung.    
 
## <a name="permissions"></a>Berechtigungen  
Erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. Ermittlung von Datenbanken in einer SQL Server-Instanz mit hohen Anzahl von VLFs
Die folgende Abfrage ermittelt die Datenbanken mit mehr als 100 VLFs in den Protokolldateien, die Zeit für die Datenbank starten und Wiederherstellung, beeinträchtigen können.

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. Die Position des letzten feststellen `VLF` im Transaktionsprotokoll vor dem Verkleinern der Protokolldatei.

Die folgende Abfrage kann verwendet werden, um zu bestimmen die Position von der letzten aktiven VLF vor dem Ausführen von Shrinkfile auf Transaktionsprotokoll, um zu bestimmen, ob das Transaktionsprotokoll verkleinert werden kann.

```sql
USE AdventureWorks2016
GO

;WITH cte_vlf AS (
SELECT ROW_NUMBER() OVER(ORDER BY vlf_begin_offset) AS vlfid, DB_NAME(database_id) AS [Database Name], vlf_sequence_number, vlf_active, vlf_begin_offset, vlf_size_mb
    FROM sys.dm_db_log_info(DEFAULT)),
cte_vlf_cnt AS (SELECT [Database Name], COUNT(vlf_sequence_number) AS vlf_count,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 0) AS vlf_count_inactive,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS vlf_count_active,
    (SELECT MIN(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_min_vlf_active,
    (SELECT MIN(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS min_vlf_active,
    (SELECT MAX(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_max_vlf_active,
    (SELECT MAX(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS max_vlf_active
    FROM cte_vlf
    GROUP BY [Database Name])
SELECT [Database Name], vlf_count, min_vlf_active, ordinal_min_vlf_active, max_vlf_active, ordinal_max_vlf_active,
((ordinal_min_vlf_active-1)*100.00/vlf_count) AS free_log_pct_before_active_log,
((ordinal_max_vlf_active-(ordinal_min_vlf_active-1))*100.00/vlf_count) AS active_log_pct,
((vlf_count-ordinal_max_vlf_active)*100.00/vlf_count) AS free_log_pct_after_active_log
FROM cte_vlf_cnt
GO
```

## <a name="see-also"></a>Siehe auch  
[Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Datenbank verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

