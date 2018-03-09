---
title: Sp_updatestats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9a735dd514a7a7ca2b99dcbd4db92e165266bc2c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spupdatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Führt UPDATE STATISTICS für alle benutzerdefinierten und internen Tabellen der aktuellen Datenbank aus.  
  
 Weitere Informationen zu UPDATE STATISTICS, finden Sie unter [UPDATE STATISTICS &#40; Transact-SQL &#41; ](../../t-sql/statements/update-statistics-transact-sql.md). Weitere Informationen zu Statistiken finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="arguments"></a>Argumente  
 [  **@resample**  =] **'resample'**  
 Gibt an, dass **Sp_updatestats** die RESAMPLE-Option von der [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) Anweisung. Wird **'resample'** nicht angegeben, aktualisiert **sp_updatestats** Statistiken mithilfe der Standardstichprobe. **resample** ist vom Datentyp **varchar(8)** . Der Standardwert ist NO.  
  
## <a name="remarks"></a>Hinweise  
 **sp_updatestats** führt UPDATE STATISTICS durch Angeben des Schlüsselworts ALL für alle benutzerdefinierten und internen Tabellen in der Datenbank aus. Sp_updatestats zeigt Meldungen über den Fortschritt an. Nach Abschluss des Updates wird gemeldet, dass die Statistiken für alle Tabellen aktualisiert wurden.  
  
 sp_updatestats aktualisiert Statistiken für deaktivierte nicht gruppierte Indizes und nicht für deaktivierte gruppierte Indizes.  
  
 Für datenträgerbasierte Tabellen **Sp_updatestats** aktualisiert Statistiken, die auf der Grundlage der **Modification_counter** Informationen in der **Sys. dm_db_stats_properties** -Katalogsicht Aktualisieren von Statistiken, in denen mindestens eine Zeile geändert wurde. Statistiken für speicheroptimierte Tabellen werden immer aktualisiert, wenn **sp_updatestats**ausgeführt wird. Deshalb sollte **sp_updatestats** nicht häufiger als nötig ausgeführt werden.  
  
 **sp_updatestats** kann die Neukompilierung von gespeicherten Prozeduren oder anderem kompilierten Code auslösen. Allerdings kann **sp_updatestats** unter Umständen keine Neukompilierung verursachen, wenn nur ein Abfrageplan für die Tabellen, auf die verwiesen wird, und die Indizes möglich ist. Eine Neukompilierung wäre in diesen Fällen nicht erforderlich, selbst wenn die Statistiken aktualisiert werden.  
  
 Bei Datenbanken mit einem Kompatibilitätsgrad unter 90 wird beim Ausführen von **sp_updatestats** die letzte NORECOMPUTE-Einstellung für bestimmte Statistiken nicht beibehalten. Bei Datenbanken mit einem Kompatibilitätsgrad von 90 oder höher behält Sp_updatestats die letzte NORECOMPUTE-Option für bestimmte Statistiken bei. Weitere Informationen zu deaktivieren und erneutes Aktivieren von Statistikupdates finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Setzt die Mitgliedschaft in der festen Serverrolle **sysadmin** oder den Besitz der Datenbank (**dbo**) voraus.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel aktualisiert die Statistiken für Tabellen in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [Sp_autostats &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [Sp_createstats &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Gespeicherte Systemprozeduren](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
