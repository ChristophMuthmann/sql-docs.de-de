---
title: Sp_notify_operator (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
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
- sp_notify_operator_TSQL
- sp_notify_operator
dev_langs: TSQL
helpviewer_keywords: sp_notify_operator
ms.assetid: c440f5c9-9884-4196-b07c-55d87afb17c3
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ff7b50b5eef5d5ff753039bf4dd7ab501160eda
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spnotifyoperator-transact-sql"></a>sp_notify_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sendet mithilfe der Datenbank-E-Mail eine E-Mail-Nachricht an den Operator.  
  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_notify_operator  
    [ @profile_name = ] 'profilename' ,  
    [ @id = ] id ,  
    [ @name = ] 'name' ,  
    [ @subject = ] 'subject' ,  
    [ @body = ] 'message' ,  
    [ @file_attachments = ] 'attachment'  
    [ @mail_database = ] 'mail_host_database'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@profile_name=** ] **"***Profilename***"**  
 Der Name des Datenbank-E-Mail-Profils, das zum Senden der Nachricht verwendet wird. *ProfileName* ist **vom Datentyp nvarchar(128)**. Wenn *Profilename* nicht angegeben ist, wird das Standardprofil für den Datenbank-Mail verwendet.  
  
 [  **@id=** ] *Id*  
 Die ID des Operators, an den die Nachricht gesendet wird. *ID* ist **Int**, hat den Standardwert NULL. Einer der *Id* oder *Namen* muss angegeben werden.  
  
 [  **@name=** ] **"***Namen***"**  
 Der Name des Operators, an den die Nachricht gesendet wird. *Namen* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL. Einer der *Id* oder *Namen* muss angegeben werden.  
  
> **Hinweis:** eine e-Mail-Adresse muss für den Operator definiert werden, bevor sie Nachrichten empfangen können.  
  
 [  **@subject=** ] **"***Betreff***"**  
 Der Betreff der E-Mail-Nachricht. *Betreff* ist **nvarchar(256)** hat keinen Standardwert.  
  
 [  **@body=** ] **"***Nachricht***"**  
 Der Text der E-Mail-Nachricht. *Nachricht* ist **nvarchar(max)** hat keinen Standardwert.  
  
 [  **@file_attachments=** ] **"***Anlage***"**  
 Der Name einer Datei, die an die E-Mail angehängt werden soll. *Anlage* ist **vom Datentyp nvarchar(512)**, hat keinen Standardwert.  
  
 [  **@mail_database=** ] **"***Mail_host_database***"**  
 Gibt den Namen der Mailhostdatenbank an. *Mail_host_database* ist **vom Datentyp nvarchar(128)**. Wenn kein *Mail_host_database* angegeben wird, die **Msdb** Datenbank wird standardmäßig verwendet.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sendet die Nachricht an die angegebene E-Mail-Adresse des angegebenen Operators. Falls für den Operator keine E-Mail-Adresse konfiguriert ist, wird ein Fehler zurückgegeben.  
  
 Die Datenbank-E-Mail und eine Mailhostdatenbank müssen konfiguriert werden, bevor eine Benachrichtigung an einen Operator gesendet werden kann.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Benachrichtigungs-E-Mail an den Operator `François Ajenstat` mit dem Datenbank-E-Mail-Profil `AdventureWorks Administrator` gesendet. Der Betreff der E-Mail lautet `Test Notification`. Die E-Mail-Nachricht enthält den Satz "This is a test of notification via e-mail".  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_notify_operator  
   @profile_name = N'AdventureWorks Administrator',  
   @name = N'François Ajenstat',  
   @subject = N'Test Notification',  
   @body = N'This is a test of notification via e-mail.' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Agent-gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Sp_add_operator &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [Sp_help_operator &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [Sp_delete_operator &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
  
  
