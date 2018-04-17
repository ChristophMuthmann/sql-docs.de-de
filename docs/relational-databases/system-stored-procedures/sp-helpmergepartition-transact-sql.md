---
title: Sp_helpmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpmergepartition
- sp_helpmergepartition_TSQL
helpviewer_keywords:
- sp_helpmergepartition
ms.assetid: 184188cc-f519-445d-97ce-aae38f1eb550
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95cf9955591a1c36ce294e8d7448b296a3399230
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpmergepartition-transact-sql"></a>sp_helpmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Partitionsinformationen für die angegebene Mergeveröffentlichung zurück. Diese gespeicherte Prozedur wird auf dem Verleger für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpmergepartition [ @publication= ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]  
    [ , [ @host_name = ] 'host_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@suser_sname=** ] **"***Suser_sname***"**  
 Der SUSER_SNAME-Wert, mit dem eine Partition definiert wird. *SUSER_SNAME* ist **Sysname**, hat den Standardwert NULL. Geben Sie diesen Parameter an, um das Resultset auf die Partitionen einzuschränken, bei denen SUSER_SNAME zu dem angegebenen Wert aufgelöst wird.  
  
> [!NOTE]  
>  Wenn *Suser_sname* angegeben wird, *Host_name* darf NULL sein.  
  
 [  **@host_name=** ] **"***Host_name***"**  
 Der HOST_NAME-Wert, mit dem eine Partition definiert wird. *HOST_NAME* ist **Sysname**, hat den Standardwert NULL. Geben Sie diesen Parameter an, um das Resultset auf die Partitionen einzuschränken, bei denen HOST_NAME zu dem angegebenen Wert aufgelöst wird.  
  
> [!NOTE]  
>  Wenn *Suser_sname* angegeben wird, *Host_name* darf NULL sein.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Partition**|**int**|Identifiziert die Abonnentenpartition.|  
|**HOST_NAME**|**sysname**|Verwendete Wert beim Erstellen der Partition für ein Abonnement, durch den Wert des gefiltert wird die [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) -Funktion beim Abonnenten.|  
|**SUSER_SNAME**|**sysname**|Verwendete Wert beim Erstellen der Partition für ein Abonnement, durch den Wert des gefiltert wird die [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) -Funktion beim Abonnenten.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Speicherort der gefilterten Datenmomentaufnahme für die Abonnentenpartition.|  
|**date_refreshed**|**datetime**|Das Datum, an dem der Momentaufnahmeauftrag zuletzt ausgeführt wurde, um eine gefilterte Datenmomentaufnahme für die Partition zu generieren.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|Identifiziert den Auftrag, der die gefilterte Datenmomentaufnahme für eine Partition erstellt.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpmergepartition** wird bei der Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle "" und die **Db_owner** feste Datenbankrolle können ausführen **Sp_helpmergepartition**.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_addmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [Sp_dropmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)  
  
  
