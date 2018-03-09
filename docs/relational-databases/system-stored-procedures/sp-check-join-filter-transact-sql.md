---
title: Sp_check_join_filter (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- filter_TSQL
- sp_check_TSQL
- sp_check_join_filter
- sp_check_join_filter_TSQL
- join
- join_TSQL
- filter
- sp_check
helpviewer_keywords:
- sp_check_join_filter
ms.assetid: e9699d59-c8c9-45f6-a561-f7f95084a540
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab650e6465ac5c872e90acc890a83d17f286b446
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spcheckjoinfilter-transact-sql"></a>sp_check_join_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wird dazu verwendet, einen Joinfilter zwischen zwei Tabellen zu überprüfen, um festzustellen, ob die Joinfilterklausel gültig ist. Diese gespeicherte Prozedur gibt außerdem Informationen zum angegebenen Joinfilter zurück, u. a. mit dem Hinweis, ob der Filter für die angegebene Tabelle zusammen mit vorausberechneten Partitionen verwendet werden kann. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichung ausgeführt. Weitere Informationen finden Sie unter [Optimieren Parametrisierter Filter-Leistung mit Vorausberechneten Partitionen ](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@filtered_table** =] **"***Filtered_table***"**  
 Der Name einer gefilterten Tabelle. *Filtered_table* ist **nvarchar(400)**, hat keinen Standardwert.  
  
 [  **@join_table** =] **"***Join_table***"**  
 Der Name einer Tabelle mit *Filtered_table*. *Join_table* ist **nvarchar(400)**, hat keinen Standardwert.  
  
 [  **@join_filterclause**  =] **"***Join_filterclause***"**  
 Die Joinfilterklausel, die getestet wird. *Join_filterclause* ist **nvarchar(1000)**, hat keinen Standardwert.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Ist, ob die Veröffentlichung für Vorausberechnete Partitionen. wobei **1** bedeutet, dass Vorausberechnete Partitionen verwendet werden können, und **0** bedeutet, dass sie nicht verwendet werden.|  
|**has_dynamic_filters**|**bit**|Ist, wenn die angegebene Filterklausel mindestens eine parametrisierte Filterfunktion enthält. wobei **1** bedeutet, dass eine parametrisierte Filterfunktion verwendet wird, und **0** bedeutet, dass eine solche Funktion nicht verwendet wird.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Liste der Funktionen in der Filterklausel, die einen parametrisierten Filter für einen Artikel definieren. Dabei sind die einzelnen Funktionen durch ein Semikolon voneinander getrennt.|  
|**uses_host_name**|**bit**|Wenn die [HOST_NAME()](../../t-sql/functions/host-name-transact-sql.md) Funktion in der Filterklausel verwendet wird, in denen **1** bedeutet, dass diese Funktion vorhanden ist.|  
|**uses_suser_sname**|**bit**|Wenn die [SUSER_SNAME()](../../t-sql/functions/suser-sname-transact-sql.md) Funktion in der Filterklausel verwendet wird, in denen **1** bedeutet, dass diese Funktion vorhanden ist.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_check_join_filter** wird bei der Mergereplikation verwendet.  
  
 **Sp_check_join_filter** kann für alle verknüpften Tabellen ausgeführt werden, selbst wenn sie nicht veröffentlicht werden. Mit dieser gespeicherten Prozedur kann eine Joinfilterklausel überprüft werden, bevor ein Joinfilter zwischen zwei Artikeln definiert wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_check_join_filter**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
