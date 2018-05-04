---
title: dm_repl_schemas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_repl_schemas_TSQL
- dm_repl_schemas
- sys.dm_repl_schemas_TSQL
- sys.dm_repl_schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_schemas dynamic management function
ms.assetid: 6f5fefff-8492-4360-bd5b-a97287367914
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f1ae6561bc96f5d4dff4d21a6057a4c1b9816c4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmreplschemas-transact-sql"></a>sys.dm_repl_schemas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu Tabellenspalten zurück, die durch Replikation veröffentlicht wurden.  
  
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**artcache_schema_address**|**varbinary(8)**|Speicherinterne Adresse der zwischengespeicherten Schemastruktur für den veröffentlichten Tabellenartikel.|  
|**tabid**|**bigint**|ID der replizierten Tabelle.|  
|**IndexID**|**smallint**|ID eines gruppierten Indexes für die veröffentlichten Tabelle.|  
|**idSch**|**bigint**|ID des Tabellenschemas.|  
|**tabschema**|**nvarchar(510)**|Name des Tabellenschemas.|  
|**ccTabschema**|**smallint**|Zeichenlänge des Tabellenschemas.|  
|**tabname**|**nvarchar(510)**|Name der veröffentlichten Tabelle.|  
|**ccTabname**|**smallint**|Zeichenlänge des veröffentlichten Tabellennamens.|  
|**rowsetid_delete**|**bigint**|ID der gelöschten Zeile.|  
|**rowsetid_insert**|**bigint**|ID der eingefügten Zeile.|  
|**num_pk_cols**|**int**|Anzahl der Primärschlüsselspalten.|  
|**pcitee**|**Binary(8000)**|Zeiger auf die Abfrageausdrucksstruktur, die beim Auswerten der berechneten Spalte verwendet wird.|  
|**re_numtextcols**|**int**|Anzahl von BLOB-Spalten in der replizierten Tabelle.|  
|**re_schema_lsn_begin**|**Binary(8000)**|Erste Protokollsequenznummer (Log Sequence Number, LSN) der Schemaversionsprotokollierung.|  
|**re_schema_lsn_end**|**Binary(8000)**|Letzte LSN der Schemaversionsprotokollierung.|  
|**re_numcols**|**int**|Anzahl der veröffentlichten Spalten.|  
|**re_colid**|**int**|Spalten-ID auf dem Verleger.|  
|**re_awcName**|**nvarchar(510)**|Name der veröffentlichten Spalte.|  
|**re_ccName**|**smallint**|Anzahl von Zeichen im Spaltennamen.|  
|**re_pk**|**tinyint**|Gibt an, ob die veröffentlichte Spalte Teil eines Primärschlüssels ist.|  
|**re_unique**|**tinyint**|Gibt an, ob die veröffentlichte Spalte Teil eines eindeutigen Indexes ist.|  
|**re_maxlen**|**smallint**|Maximale Länge der veröffentlichten Spalte.|  
|**re_prec**|**tinyint**|Genauigkeit der veröffentlichten Spalte.|  
|**re_scale**|**tinyint**|Skalierung der veröffentlichten Spalte.|  
|**re_collatid**|**bigint**|Sortierungs-ID der veröffentlichten Spalte.|  
|**re_xvtype**|**smallint**|Typ der veröffentlichten Spalte.|  
|**re_offset**|**smallint**|Offset der veröffentlichten Spalte.|  
|**re_bitpos**|**tinyint**|Bitposition der veröffentlichten Spalte im Bytevektor.|  
|**re_fNullable**|**tinyint**|Gibt an, ob die veröffentlichte Spalte NULL-Werte unterstützt.|  
|**re_fAnsiTrim**|**tinyint**|Gibt an, ob ANSI-Kürzung in der veröffentlichten Spalte verwendet wird.|  
|**re_computed**|**smallint**|Gibt an, ob die veröffentlichte Spalte eine berechnete Spalte ist.|  
|**se_rowsetid**|**bigint**|ID des Rowsets.|  
|**se_schema_lsn_begin**|**Binary(8000)**|Erste LSN der Schemaversionsprotokollierung.|  
|**se_schema_lsn_end**|**Binary(8000)**|Letzte LSN der Schemaversionsprotokollierung.|  
|**se_numcols**|**int**|Anzahl der Spalten.|  
|**se_colid**|**int**|ID der Spalte auf dem Abonnenten.|  
|**se_maxlen**|**smallint**|Maximale Länge der Spalte.|  
|**se_prec**|**tinyint**|Genauigkeit der Spalte.|  
|**se_scale**|**tinyint**|Skalierung der Spalte.|  
|**se_collatid**|**bigint**|Sortierungs-ID der Spalte.|  
|**se_xvtype**|**smallint**|Typ der Spalte.|  
|**se_offset**|**smallint**|Offset der Spalte.|  
|**se_bitpos**|**tinyint**|Bitposition der Spalte im Bytevektor.|  
|**se_fNullable**|**tinyint**|Gibt an, ob die Spalte NULL-Werte unterstützt.|  
|**se_fAnsiTrim**|**tinyint**|Gibt an, ob ANSI-Kürzung in der Spalte verwendet wird.|  
|**se_computed**|**smallint**|Gibt an, ob die Spalte eine berechnete Spalte ist.|  
|**se_nullBitInLeafRows**|**int**|Gibt an, ob der Spaltenwert NULL ist.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung in der Veröffentlichungsdatenbank zum Aufrufen von **dm_repl_schemas**.  
  
## <a name="remarks"></a>Hinweise  
 Informationen werden nur für replizierte Datenbankobjekte zurückgegeben, die zurzeit in den Replikationsartikelcache geladen sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Replikation verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

