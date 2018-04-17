---
title: Sp_helparticledts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_helparticledts
- sp_helparticledts_TSQL
helpviewer_keywords:
- sp_helparticledts
ms.assetid: cd1aed60-e056-4ff3-86ee-62b19433d890
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70823adfe5fe3cece72f0ac0a6fa492f646253ab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sphelparticledts-transact-sql"></a>sp_helparticledts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ruft Informationen zu den benutzerdefinierten Tasknamen ab, die beim Erstellen eines Transformationsabonnements mithilfe von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic verwendet werden sollen. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helparticledts [ @publication = ] 'publication', [ @article = ] 'article'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication =**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@article=**] **"***Artikel***"**  
 Der Name eines Artikels in der Veröffentlichung. *Artikel* ist **Sysname**, hat keinen Standardwert.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**pre_script_ignore_error_task_name**|**sysname**|Taskname für den Programmiertask, der auftritt, bevor die Momentaufnahmedaten kopiert werden. Die Programmausführung soll beim Auftreten eines Skriptfehlers fortgesetzt werden.|  
|**pre_script_task_name**|**sysname**|Taskname für den Programmiertask, der auftritt, bevor die Momentaufnahmedaten kopiert werden. Die Programmausführung wird beim Auftreten eines Fehlers beendet.|  
|**transformation_task_name**|**sysname**|Taskname für den Programmiertask, wenn der Task Datengesteuerte Abfrage verwendet wird.|  
|**post_script_ignore_error_task_name**|**sysname**|Taskname für den Programmiertask, der auftritt, nachdem die Momentaufnahmedaten kopiert wurden. Die Programmausführung soll beim Auftreten eines Skriptfehlers fortgesetzt werden.|  
|**post_script_task_name**|**sysname**|Taskname für den Programmiertask, der auftritt, nachdem die Momentaufnahmedaten kopiert wurden. Die Programmausführung wird beim Auftreten eines Fehlers beendet.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helparticledts** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 Beim Benennen von Tasks in einem Replikations-DTS-Programm (Data Transformation Services) müssen für die Replikations-Agents bestimmte Namenskonventionen eingehalten werden. Für benutzerdefinierte Tasks, wie z. B. den Task SQL ausführen, stellt der Name eine verkettete Zeichenfolge dar, die aus dem Artikelnamen, einem Präfix und einem optionalen Teil besteht. Wenn Sie den Code schreiben und sich nicht sicher sind, wie die Tasknamen lauten sollen, dann weist das Resultset die zu verwendenden Tasknamen zu.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle "" und die **Db_owner** feste Datenbankrolle können ausführen **Sp_helparticledts**.  
  
  
