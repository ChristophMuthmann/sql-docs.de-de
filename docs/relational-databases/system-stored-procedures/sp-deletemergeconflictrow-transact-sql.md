---
title: Sp_deletemergeconflictrow (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e085a7010f25f40b95a45d8ddd0c7b455d7266c6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spdeletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht Zeilen aus einer Konflikttabelle oder [MSmerge_conflicts_info &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) Tabelle. Diese gespeicherte Prozedur wird für jede Datenbank auf dem Computer ausgeführt, auf dem die Konflikttabelle gespeichert ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_deletemergeconflictrow [ [ @conflict_table = ] 'conflict_table' ]  
    [ , [ @source_object = ] 'source_object' ]  
    { , [ @rowguid = ] 'rowguid'  
        , [ @origin_datasource = ] 'origin_datasource' ] }  
    [ , [ @drop_table_if_empty = ] 'drop_table_if_empty' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@conflict_table=**] **"***Conflict_table***"**  
 Der Name der Konflikttabelle. *Conflict_table* ist **Sysname**, hat den Standardwert  **%** . Wenn die *Conflict_table* als NULL angegeben ist oder  **%** , der Konflikt wird davon ausgegangen, dass ein Delete-Konflikt und der Zeile entspricht *Rowguid* und *Origin_datasource* und *Source_object* wird gelöscht, von der [MSmerge_conflicts_info &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) Tabelle.  
  
 [  **@source_object=**] **"***Source_object***"**  
 Der Name der Quelltabelle. *Source_object* ist **nvarchar(386)**, hat den Standardwert NULL.  
  
 [  **@rowguid =**] **"***Rowguid***"**  
 Die Zeilen-ID für den Löschkonflikt. *ROWGUID* ist **"uniqueidentifier"**, hat keinen Standardwert.  
  
 [  **@origin_datasource=**] **"***Origin_datasource***"**  
 Der Ursprung des Konflikts. *Origin_datasource* ist **varchar(255)**, hat keinen Standardwert.  
  
 [  **@drop_table_if_empty=**] **"***Drop_table_if_empty***"**  
 Ein Flag gibt an, dass die *Conflict_table* soll, wenn gelöscht werden, ist leer. *Drop_table_if_empty* ist **varchar(10)**, hat den Standardwert "false".  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_deletemergeconflictrow** wird bei der Mergereplikation verwendet.  
  
 [MSmerge_conflicts_info &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) Tabelle eine Systemtabelle und wird nicht aus der Datenbank gelöscht, selbst wenn sie leer ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_deletemergeconflictrow**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
