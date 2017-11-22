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
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: "4"
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: b7250943f4e92d60888a75d9e577388f3cc6b1ed
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbloginfo-transact-sql"></a>Sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Gibt `VLF` Informationen von den Transaktionsprotokolldateien. (Alle Protokolldateien werden in der Tabellenausgabe kombiniert). Jede Zeile in der Ausgabe stellt eine `VLF` im Transaktionsprotokoll und stellt Informationen zu diesem VLF im Protokoll.

## <a name="syntax"></a>Syntax  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>Argumente  
 *Database_id* | NULL | STANDARDWERT  
 Ist die ID der Datenbank. *Database_id* ist **Int**. Gültige Eingaben sind die ID einer Datenbank, NULL oder DEFAULT. Die Standardeinstellung ist NULL. NULL und DEFAULT sind gleichwertig im Kontext der aktuellen Datenbank.
 
 Geben Sie NULL zurückzugebenden `VLF` Informationen von der aktuellen Datenbank.

 Die integrierte Funktion [DB_ID](../../t-sql/functions/db-id-transact-sql.md) kann angegeben werden. Wenn DB_ID verwendet wird, ohne dass ein Datenbankname angegeben wird, muss der Kompatibilitätsgrad der aktuellen Datenbank 90 oder höher sein.  

## <a name="table-returned"></a>Zurückgegebene Tabelle  

|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Datenbank-ID|
|file_id|**smallint**|Datei-Id des Transaktionsprotokolls.|  
|vlf_begin_offset|**bigint** |Speicherort der Offset der `VLF` vom Anfang der Transaktionsprotokolldatei.|
|vlf_size_mb |**float** |`VLF`Größe (MB) auf 2 Dezimalstellen gerundet.|     
|vlf_sequence_number|**bigint** |`VLF`Sequenznummer in der Reihenfolge erstellt. Zur eindeutigen Identifikation `VLFs` in der Protokolldatei.|
|vlf_active|**bit** |Gibt an, ob VLF verwendet oder nicht. <br />0 – wird vlf nicht verwendet.<br />1 – `VLF` aktiv ist.|
|vlf_status|**int** |Status der `VLF`. Mögliche Werte sind: <br />0 – `VLF` ist inaktiv <br />1 - vlf wird initialisiert, aber nicht verwendete <br /> 2 – `VLF` aktiv ist.|
|vlf_parity|**tinyint** |Parität `VLF`. Wird intern verwendet, um zu bestimmen, das Ende des Protokolls in eine `VLF`.|
|vlf_first_lsn|**nvarchar(48)** |LSN des ersten Protokolldatensatzes in der `VLF`.|
|vlf_create_lsn|**nvarchar(48)** |LSN des Protokolls zu zeichnen, erstellt die `VLF`.|

## <a name="remarks"></a>Hinweise
 Die `sys.dm_db_log_info` dynamische Verwaltungsfunktion ersetzt die `DBCC LOGINFO` Anweisung. 
 
## <a name="permissions"></a>Berechtigungen  
 Erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. Ermittlung von Datenbanken in einer SQL Server-Instanz mit hohen Anzahl von`VLFs`
Die folgende Abfrage ermittelt die Datenbanken mit mehr als 100 `VLFs` in den Protokolldateien kann der Start und Wiederherstellung, Zeit der Datenbank beeinträchtigen.

```sql
SELECT name,count(l.database_id) as 'vlf_count' from sys.databases s
cross apply sys.dm_db_log_info(s.database_id) l
group by name
having count(l.database_id)> 100
```

### <a name="b-determing-the-status-of-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. Feststellen des Status des letzten `VLF` im Transaktionsprotokoll vor dem Verkleinern der Protokolldatei.

Die folgende Abfrage kann verwendet werden, um zu bestimmen, den Status des letzten `VLF` vor dem Ausführen von Shrinkfile auf Transaktionsprotokoll, um zu bestimmen, ob das Transaktionsprotokoll verkleinert werden kann.

```sql
USE <database name>
GO

SELECT top 1 DB_NAME(database_id) as "Database Name",file_id,vlf_size_mb,vlf_sequence_number, vlf_active, vlf_status
from sys.dm_db_log_info(DEFAULT)
order by vlf_sequence_number desc
```


## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
  



