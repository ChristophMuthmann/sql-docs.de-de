---
title: Sp_autostats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_autostats_TSQL
- sp_autostats
dev_langs: TSQL
helpviewer_keywords: sp_autostats
ms.assetid: d1df8c15-ee73-49eb-9d13-6e98943c3e38
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a88a5d19b80ccb69272fab4c2b3e4ba7f87894a7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spautostats-transact-sql"></a>sp_autostats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Zeigt die AUTO_UPDATE_STATISTICS-Option zum automatischen Statistikupdate für einen Index, ein Statistikobjekt, eine Tabelle oder eine indizierte Sicht an oder ändert sie.  
  
 Weitere Informationen zur AUTO_UPDATE_STATISTICS-Option finden Sie unter [ALTER DATABASE SET-Optionen &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) und [Statistiken](../../relational-databases/statistics/statistics.md).  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_autostats [ @tblname = ] 'table_or_indexed_view_name'   
    [ , [ @flagc = ] 'stats_value' ]   
    [ , [ @indname = ] 'statistics_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@tblname=** ] **"***Table_or_indexed_view_name***"**  
 Der Name der Tabelle oder indizierten Sicht, für die die AUTO_UPDATE_STATISTICS-Option angezeigt werden soll. *Table_or_indexed_view_name* ist **nvarchar(776)**, hat keinen Standardwert.  
  
 [  **@flagc=** ] **"***Stats_value***"**  
 Aktualisiert die AUTO_UPDATE_STATISTICS-Option auf einen dieser Werte:  
  
 **ON** = ON  
  
 **OFF** = OFF  
  
 Wenn *Stats_flag* ist nicht angegeben wird, die aktuelle AUTO_UPDATE_STATISTICS-Einstellung angezeigt. *Stats_value* ist **varchar(10)**, hat den Standardwert NULL.  
  
 [  **@indname=** ] **"***Statistics_name***"**  
 Der Name der Statistik, für die die AUTO_UPDATE_STATISTICS-Option angezeigt oder aktualisiert werden soll. Um die Statistik für einen Index anzuzeigen, können Sie den Namen des Indexes verwenden. Ein Index und das dazugehörige Statistikobjekt verfügen über den gleichen Namen.  
  
 *Statistics_name* ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Wenn *Stats_flag* angegeben wird, **Sp_autostats** meldet die Aktion, die erstellt wurde, jedoch kein Resultset zurückgegeben.  
  
 Wenn *Stats_flag* nicht angegeben ist, **Sp_autostats** gibt das folgende Resultset zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Indexname**|**varchar(60)**|Der Name des Indexes oder der Statistik.|  
|**AUTOSTATS**|**varchar(3)**|Aktueller Wert für die AUTO_UPDATE_STATISTICS-Option.|  
|**Zuletzt aktualisiert**|**datetime**|Das Datum des letzten Statistikupdates.|  
  
 Das Resultset für eine Tabelle oder indizierte Sicht Statistiken für Indizes, Statistiken für einzelne Spalten generiert, mit der AUTO_CREATE_STATISTICS-Option erstellt wurden umfasst und Statistiken erstellt, mit der [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) Anweisung.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der angegebene Index deaktiviert ist oder die angegebene Tabelle einen deaktivierten gruppierten Index enthält, wird eine Fehlermeldung angezeigt.  
  
 AUTO_UPDATE_STATISTICS ist für speicheroptimierte Tabellen immer auf OFF festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ändern der AUTO_UPDATE_STATISTICS-Option muss n Mitgliedschaft der **Db_owner** der festen Datenbankrolle oder ALTER-Berechtigung auf *Table_name*. Zum Anzeigen der AUTO_UPDATE_STATISTICS-Option erfordert die Mitgliedschaft in der **öffentlichen** Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-display-the-status-of-all-statistics-on-a-table"></a>A. Anzeigen des Status aller Statistiken für eine Tabelle  
 Das folgende Beispiel zeigt den Status aller Statistiken für die `Product`-Tabelle an.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product';  
GO  
```  
  
### <a name="b-enable-autoupdatestatistics-for-all-statistics-on-a-table"></a>B. Aktivieren von AUTO_UPDATE_STATISTICS für alle Statistiken zu einer Tabelle  
 Im folgenden Beispiel wird die AUTO_UPDATE_STATISTICS-Option für alle Statistiken zur `Product`-Tabelle aktiviert.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'ON';  
GO  
```  
  
### <a name="c-disable-autoupdatestatistics-for-a-specific-index"></a>C. Deaktivieren von AUTO_UPDATE_STATISTICS für einen bestimmten Index  
 Im folgenden Beispiel wird die AUTO_UPDATE_STATISTICS-Option für den `AK_Product_Name`-Index der `Product`-Tabelle deaktiviert.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'OFF', AK_Product_Name;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statistiken](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [Sp_createstats &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
