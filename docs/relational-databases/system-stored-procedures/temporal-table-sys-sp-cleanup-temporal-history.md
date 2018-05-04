---
title: Sys.sp_cleanup_temporal_history | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.service: sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
caps.latest.revision: 4
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ebea6e162bb047f6c6224001e70dede74b5d58cc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysspcleanuptemporalhistory-transact-sql"></a>Sys.sp_cleanup_temporal_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

Entfernt alle Zeilen aus temporale Verlaufstabelle, die konfigurierten HISTORY_RETENTION Zeitraum innerhalb einer einzelnen Transaktion zu entsprechen.
  
## <a name="syntax"></a>Syntax  
```  
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```  
  
## <a name="arguments"></a>Argumente  

*@table_name*

Der Name der temporalen Tabelle, für welche, die Aufbewahrung Bereinigung aufgerufen wird.

*schema_name*

Der Name des Schemas, zu der aktuellen temporalen Tabelle gehört

*Row_count_var* [Ausgabe]

Die Output-Parameter, der Anzahl der gelöschten Zeilen zurückgibt. Dieser Parameter gibt zurück, wenn die Verlaufstabelle columnstore-Index gruppiert ist, immer 0.
  
## <a name="remarks"></a>Hinweise
Diese gespeicherte Prozedur kann nur mit temporären Tabellen verwendet werden, begrenzte Beibehaltungsdauer angegeben haben.
Verwenden Sie diese gespeicherte Prozedur nur, wenn Sie sofort alle veraltete Zeilen aus der Verlaufstabelle zu bereinigen müssen. Sie sollten wissen, dass er erheblichen Einfluss auf das Datenbankprotokoll und e/a-Subsystem verfügen kann, wie alle geeignete Zeilen innerhalb derselben Transaktion gelöscht. 

Es wird immer eine interne Hintergrundtask für den Cleanup vertrauen, dass entfernt Zeilen mit der minimalen Auswirkungen auf die normale arbeitsauslastungen und die Datenbank im Allgemeinen veraltete empfohlen.

## <a name="permissions"></a>Berechtigungen  
 Erfordert Db_owner-Berechtigungen.  

## <a name="example"></a>Beispiel

```
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="see-also"></a>Siehe auch

[Aufbewahrungsrichtlinie für die temporale Tabellen](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
