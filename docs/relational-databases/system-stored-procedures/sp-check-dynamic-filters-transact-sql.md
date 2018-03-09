---
title: Sp_check_dynamic_filters (Transact-SQL) | Microsoft Docs
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
- dynamic_filters_TSQL
- sp_check_TSQL
- check
- sp_check_dynamic filter
- check_TSQL
- filters_TSQL
- check_dynamic_filters_TSQL
- dynamic filters
- filters
- check dynamic filters
- sp_check_dynamic filter_TSQL
- sp_check_for_sync_trigger_TSQL
- sp_check
helpviewer_keywords:
- sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 096c6ff70b712b283191afeddbb7e9d9c6afd36a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spcheckdynamicfilters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt Informationen zu parametrisierten Zeilenfiltereigenschaften für eine Veröffentlichung an, insbesondere die Funktionen, die zum Generieren einer gefilterten Datenpartition für eine Veröffentlichung verwendet werden, und ob die Veröffentlichung vorausberechnete Partitionen verwenden kann. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication** =] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Ist, ob die Veröffentlichung Vorausberechnete Partitionen verwenden. wobei **1** bedeutet, dass Partitionen verwendet werden können vorausberechnete, und **0** bedeutet, dass sie nicht verwendet werden.|  
|**has_dynamic_filters**|**bit**|Ist, wenn mindestens ein parametrisierter Zeilenfilter in der Veröffentlichung definiert wurde. wobei **1** bedeutet, die eine oder mehrere parametrisierte Zeilenfilter vorhanden sind, und **0** bedeutet, die keine dynamischen Filter vorhanden sind.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Die Liste der Funktionen, die zum Filtern von Artikeln in einer Veröffentlichung verwendet werden. Die einzelnen Funktionen werden hierbei durch ein Semikolon getrennt.|  
|**validate_subscriber_info**|**nvarchar(500)**|Die Liste der Funktionen, die zum Filtern von Artikeln in einer Veröffentlichung verwendet werden. Die einzelnen Funktionen werden hierbei durch ein Pluszeichen (+) getrennt.|  
|**uses_host_name**|**bit**|Wenn die [HOST_NAME()](../../t-sql/functions/host-name-transact-sql.md) -Funktion in parametrisierten Zeilenfiltern verwendet wird, in denen **1** bedeutet, dass diese Funktion für das dynamische Filtern verwendet wird.|  
|**uses_suser_sname**|**bit**|Wenn die [SUSER_SNAME()](../../t-sql/functions/suser-sname-transact-sql.md) -Funktion in parametrisierten Zeilenfiltern verwendet wird, in denen **1** bedeutet, dass diese Funktion für das dynamische Filtern verwendet wird.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_check_dynamic_filters** wird bei der Mergereplikation verwendet.  
  
 Wenn eine Veröffentlichung definiert wurde, verwenden Sie Vorausberechnete Partitionen **Sp_check_dynamic_filters** überprüft, ob Verstöße gegen die Einschränkungen für Vorausberechnete Partitionen. Ist dies der Fall, wird ein Fehler zurückgegeben. Weitere Informationen finden Sie unter [Optimieren Parametrisierter Filter-Leistung mit Vorausberechneten Partitionen ](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
 Wenn eine Veröffentlichung laut Definition über parametrisierte Zeilenfilter verfügt, jedoch keine parametrisierten Zeilenfilter gefunden werden, wird ein Fehler zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_check_dynamic_filters**.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Partitionen für eine Mergeveröffentlichung mit parametrisierten Filtern](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [Sp_check_join_filter &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [Sp_check_subset_filter &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
