---
title: Sys.dm_db_log_info (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: 661647715d2fcff3a4821250dfaa65e0fea07d6e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="sysdmdbloginfo-transact-sql"></a>Sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Gibt [virtuelle Protokolldatei (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) Informationen des Transaktionsprotokolls. Beachten Sie, dass es sich bei allen Transaktionsprotokolldateien in der Tabellenausgabe kombiniert werden. Jede Zeile in der Ausgabe eine VLF im Transaktionsprotokoll darstellt und bietet Informationen zu diesem VLF im Protokoll.

## <a name="syntax"></a>Syntax  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>Argumente  
 *Database_id* | NULL | STANDARDWERT  
 Ist die ID der Datenbank. *Database_id* ist **Int**. Gültige Eingaben sind die ID einer Datenbank, NULL oder DEFAULT. Die Standardeinstellung ist NULL. NULL und DEFAULT sind gleichwertig im Kontext der aktuellen Datenbank.
 
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

## <a name="remarks"></a>Remarks
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

### <a name="b-determing-the-status-of-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. Feststellen des Status des letzten `VLF` im Transaktionsprotokoll vor dem Verkleinern der Protokolldatei.

Die folgende Abfrage kann verwendet werden, um zu bestimmen, den Status der letzten VLF vor dem Ausführen von Shrinkfile auf Transaktionsprotokoll, um zu bestimmen, ob das Transaktionsprotokoll verkleinert werden kann.

```sql
USE AdventureWorks2016
GO

SELECT TOP 1 DB_NAME(database_id) AS "Database Name", file_id, vlf_size_mb, vlf_sequence_number, vlf_active, vlf_status
FROM sys.dm_db_log_info(DEFAULT)
ORDER BY vlf_sequence_number DESC
```


## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Datenbank verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[Sys.dm_db_log_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

