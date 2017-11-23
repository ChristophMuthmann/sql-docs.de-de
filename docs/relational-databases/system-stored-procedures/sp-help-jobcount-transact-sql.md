---
title: Sp_help_jobcount (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_jobcount
- sp_help_jobcount_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_jobcount
ms.assetid: ae8ef851-646c-4889-bc11-c8ec78762572
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eae74b9745c8b5ad4f5e2cc5b9268e5a297b03b2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpjobcount-transact-sql"></a>sp_help_jobcount (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Anzahl von Aufträgen an, an die ein Zeitplan angefügt ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_jobcount   
     [ @schedule_name = ] 'schedule_name' ,  
     [ @schedule_id = ] schedule_id   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@schedule_id=** ] *Schedule_id*  
 Der Bezeichner des Zeitplans, der aufgelistet werden soll. *Schedule_id* ist **Int**, hat keinen Standardwert. Entweder *Schedule_id* oder *Schedule_name* kann angegeben werden.  
  
 [  **@schedule_name=** ] **"***Schedule_name***"**  
 Der Name des Zeitplans, der aufgelistet werden soll. *Schedule_name* ist **Sysname**, hat keinen Standardwert. Entweder *Schedule_id* oder *Schedule_name* kann angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt das folgende Resultset zurück:  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**JobCount**|**int**|Anzahl von Aufträgen für den angegebenen Zeitplan.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Prozedur wird die Anzahl von Aufträgen aufgelistet, die an den angegebenen Zeitplan angefügt sind.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Nur Mitglieder der **Sysadmin** kann die Anzahl von Aufträgen, die von anderen Benutzern gehören anzeigen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Anzahl der dem Zeitplan `NightlyJobs` angefügten Aufträge aufgelistet.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_jobcount  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Agent-gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Sp_add_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Sp_attach_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [Sp_delete_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [Sp_detach_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
