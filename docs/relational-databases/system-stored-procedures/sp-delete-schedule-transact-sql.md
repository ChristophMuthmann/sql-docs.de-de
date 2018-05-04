---
title: Sp_delete_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_schedule
- sp_delete_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_schedule
ms.assetid: 18b2c985-47b8-49c8-82d1-8a4af3d7d33a
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a02340dd4d5ca2e17044f34e521bc9ead793ed50
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdeleteschedule-transact-sql"></a>sp_delete_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht einen Zeitplan.  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_delete_schedule { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @force_delete = ] force_delete  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@schedule_id=** ] *Schedule_id*  
 Die Zeitplan-ID des zu löschenden Zeitplans. *Schedule_id* ist **Int**, hat den Standardwert NULL.  
  
> **Hinweis:** entweder *Schedule_id* oder *Schedule_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@schedule_name=** ] **"***Schedule_name***"**  
 Der Name des zu löschenden Zeitplan. *Schedule_name* ist **Sysname**, hat den Standardwert NULL.  
  
> **Hinweis:** entweder *Schedule_id* oder *Schedule_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [ **@force_delete** = ] *force_delete*  
 Gibt an, ob die Prozedur einen Fehler verursachen soll, wenn der Zeitplan an einen Auftrag angefügt wird. *Force_delete* bit und hat den Standardwert **0**. Wenn *Force_delete* ist **0**, die gespeicherte Prozedur fehlschlägt, wenn der Zeitplan einem Auftrag angefügt ist. Wenn *Force_delete* ist **1**, der Zeitplan gelöscht, unabhängig davon, ob der Zeitplan einem Auftrag angefügt ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Standardmäßig kann ein Zeitplan nicht gelöscht werden, wenn der Zeitplan einem Auftrag angefügt ist. Um einen Zeitplan zu löschen, die einem Auftrag angefügt ist, geben Sie den Wert **1** für *Force_delete*. Durch das Löschen eines Zeitplans werden derzeit ausgeführte Aufträge nicht beendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Hinweis: Der Auftragsbesitzer kann einem Zeitplan einen Auftrag anfügen oder diesen von ihm trennen, und zwar ohne der Zeitplanbesitzer sein zu müssen. Allerdings kann kein Zeitplan gelöscht werden, wenn das Trennen keine Aufträge lassen würde, wenn der Aufrufer der Zeitplanbesitzer ist.  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Nur Mitglieder der **Sysadmin** Rolle kann einen Zeitplan für Aufträge, die von einem anderen Benutzer gehört zu löschen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-deleting-a-schedule"></a>A. Löschen eines Zeitplans  
 Im folgenden Beispiel wird der Zeitplan `NightlyJobs` gelöscht. Wenn der Zeitplan einem Auftrag angefügt ist, kann der Zeitplan im Rahmen des Beispiels nicht gelöscht werden.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="b-deleting-a-schedule-attached-to-a-job"></a>B. Löschen eines an einen Auftrag angefügten Zeitplans  
 Im folgenden Beispiel wird der Zeitplan `RunOnce` gelöscht, unabhängig davon, ob der Zeitplan einem Auftrag angefügt ist.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = 'RunOnce',  
    @force_delete = 1;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von Aufträgen](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
  
