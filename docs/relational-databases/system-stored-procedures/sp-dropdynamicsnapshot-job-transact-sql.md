---
title: "ausgeführt werden kann (Transact-SQL) | Microsoft Docs"
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
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3cc6dc65589951513a5d05dbfad68cecb8d92745
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spdropdynamicsnapshotjob-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt einen Auftrag für eine Momentaufnahme gefilterter Daten für eine Veröffentlichung mit parametrisierten Zeilenfiltern. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt. Wenn der Auftrag gelöscht wird, wird alle zugehörigen Daten gelöscht, von der [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) -Systemtabelle.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, aus der der Auftrag für die Momentaufnahme gefilterter Daten entfernt wird. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@dynamic_snapshot_jobname** =] **"***Dynamic_snapshot_jobname***"**  
 Der Name des Auftrags für die Momentaufnahme gefilterter Daten, der entfernt wird. *Dynamic_snapshot_jobname*ist vom Datentyp Sysname und ist er nicht angegebenen Standardwerte Auftragsnamen zugeordneten *Dynamic_snapshot_jobid*.  
  
 [  **@dynamic_snapshot_jobid** =] **"***Dynamic_snapshot_jobid***"**  
 Der Bezeichner des Auftrags für die Momentaufnahme gefilterter Daten, der entfernt wird. *Dynamic_snapshot_jobid*ist **"uniqueidentifier"**, mit dem Standardwert NULL.  
  
> [!IMPORTANT]  
>  Nur *Dynamic_snapshot_jobid*oder *Dynamic_snapshot_jobname* kann angegeben werden. Wenn Sie Werte für entweder nicht bereitgestellt werden *Dynamic_snapshot_jobid*oder *Dynamic_snapshot_jobname*, für die Veröffentlichung aller dynamischen Momentaufnahme-Agentaufträge werden entfernt.  
  
 [  **@ignore_distributor =**] *Ignore_distributor*  
 *Ignore_distributor* ist **Bit**, hat den Standardwert **0**. Dieser Parameter kann verwendet werden, um einen Auftrag für eine dynamische Momentaufnahme zu löschen, ohne Cleanuptasks auf dem Verteiler auszuführen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dropdynamicsnapshot** wird bei der Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_dropdynamicsnapshot**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_adddynamicsnapshot_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
