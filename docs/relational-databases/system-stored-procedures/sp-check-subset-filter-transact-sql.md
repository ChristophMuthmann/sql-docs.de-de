---
title: Sp_check_subset_filter (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_check_TSQL
- sp_check_subset_filter
- filter
- subset
- subset_TSQL
- sp_check
- sp_check_subset_filter_TSQL
helpviewer_keywords: sp_check_subset_filter
ms.assetid: 525cfcfc-f317-478d-ba84-72e62285f160
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3341c4f5fc6c637f74dabf913730e6c6e30dfcea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spchecksubsetfilter-transact-sql"></a>sp_check_subset_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wird zum Überprüfen einer Filterklausel gegen eine beliebige Tabelle verwendet, um die Gültigkeit der Filterklausel für die Tabelle zu ermitteln. Diese gespeicherte Prozedur gibt Informationen zum bereitgestellten Filter zurück, einschließlich der Angabe, ob der Filter mit vorausberechneten Partitionen verwendet werden kann. Diese gespeicherte Prozedur wird auf dem Verleger für die Datenbank ausgeführt, die die Veröffentlichung enthält.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@filtered_table** =] **"***Filtered_table***"**  
 Der Name einer gefilterten Tabelle. *Filtered_table* ist **nvarchar(400)**, hat keinen Standardwert.  
  
 [  **@subset_filterclause**  =] **"***Subset_filterclause***"**  
 Die Filterklausel, die getestet wird. *Subset_filterclause* ist **nvarchar(1000)**, hat keinen Standardwert.  
  
 [  **@has_dynamic_filters** =] *Has_dynamic_filters*  
 Gibt an, ob die Filterklausel einen parametrisierten Zeilenfilter festlegt. *Has_dynamic_filters* ist **Bit**, hat den Standardwert NULL und ist ein Output-Parameter. Gibt einen Wert von **1** Wenn die Filterklausel ein parametrisierter Zeilenfilter ist.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Ist, ob die Veröffentlichung Vorausberechnete Partitionen verwenden. wobei **1** bedeutet, dass Partitionen verwendet werden können vorausberechnete, und **0** bedeutet, dass sie nicht verwendet werden.|  
|**has_dynamic_filters**|**bit**|Ist, wenn die angegebene Filterklausel mindestens einen parametrisierten Zeilenfilter enthält. wobei **1** bedeutet, dass ein parametrisierter Zeilenfilter verwendet wird, und **0** bedeutet, dass eine solche Funktion nicht verwendet wird.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Liste der Funktionen in der Filterklausel, die einen Artikel dynamisch filtern, wobei die Funktionen durch Semikolon voneinander getrennt sind.|  
|**uses_host_name**|**bit**|Wenn die [HOST_NAME()](../../t-sql/functions/host-name-transact-sql.md) Funktion in der Filterklausel verwendet wird, in denen **1** bedeutet, dass diese Funktion vorhanden ist.|  
|**uses_suser_sname**|**bit**|Wenn die [SUSER_SNAME()](../../t-sql/functions/suser-sname-transact-sql.md) Funktion in der Filterklausel verwendet wird, in denen **1** bedeutet, dass diese Funktion vorhanden ist.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_check_subset_filter** wird bei der Mergereplikation verwendet.  
  
 **Sp_check_subset_filter** kann für eine Tabelle ausgeführt werden, auch wenn die Tabelle nicht veröffentlicht wird. Mit dieser gespeicherten Prozedur kann eine Filterklausel vor dem Definieren eines gefilterten Artikels überprüft werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_check_subset_filter**.  
  
## <a name="see-also"></a>Siehe auch  
 [Optimieren der Leistung parametrisierter Filter mithilfe vorausberechneter Partitionen](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
