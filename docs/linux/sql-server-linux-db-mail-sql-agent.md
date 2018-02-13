---
title: "DB-E-Mails und e-Mail-Benachrichtigungen mit SQL-Agent für Linux | Microsoft Docs"
description: Dieser Artikel beschreibt, wie DB E-Mails und e-Mail-Benachrichtigungen mit SQL Server on Linux
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: tbd
ms.workload: Inactive
ms.openlocfilehash: d5d9dd84a7c3489c96e4e1aeaeb6d0928140a83f
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="db-mail-and-email-alerts-with-sql-agent-on-linux"></a>DB-E-Mails und e-Mail-Benachrichtigungen mit SQL-Agent für Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Die folgenden Schritte veranschaulichen, wie DB Mail einrichten und verwenden es mit SQL Server-Agent (**Mssql-Server-Agent**) unter Linux. 

> [!NOTE]
> Um die DB-Mail mit SQL Server on Linux verwenden zu können, müssen Sie SQL Server 2017 RC1 verwenden oder höher.

## <a name="prerequisites"></a>Erforderliche Komponenten

- SQL Server 2017 RC1 und höher
- SQL Server-Agent v14.0.800.90-2 und höher (Wenn Sie e-Mail-Dienst für Benachrichtigungen verwenden möchten)

## <a name="1-enable-db-mail"></a>1. DB-Mail aktivieren

```sql
USE master 
GO 
sp_configure 'show advanced options',1 
GO 
RECONFIGURE WITH OVERRIDE 
GO 
sp_configure 'Database Mail XPs', 1 
GO 
RECONFIGURE  
GO  
```

## <a name="2-create-a-new-account"></a>2. Neues Konto erstellen
```sql
EXECUTE msdb.dbo.sysmail_add_account_sp 
@account_name = 'SQLAlerts', 
@description = 'Account for Automated DBA Notifications', 
@email_address = 'sqlagenttest@gmail.com', 
@replyto_address = 'sqlagenttest@gmail.com', 
@display_name = 'SQL Agent', 
@mailserver_name = 'smtp.gmail.com', 
@port = 587, 
@enable_ssl = 1, 
@username = 'sqlagenttest@gmail.com', 
@password = '<password>' 
GO
```

## <a name="3-create-a-default-profile"></a>3. Erstellen Sie ein Standardprofil

```sql
EXECUTE msdb.dbo.sysmail_add_profile_sp 
@profile_name = 'default', 
@description = 'Profile for sending Automated DBA Notifications' 
GO
```

## <a name="4-add-the-database-mail-account-to-a-database-mail-profile"></a>4. Fügen Sie das Database Mail-Konto zu einem Database Mail-Profil
```sql
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp 
@profile_name = 'default', 
@principal_name = 'public', 
@is_default = 1 ; 
 ```
 
## <a name="5-add-account-to-profile"></a>5. Konto zum Profil hinzufügen 
```sql
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp   
@profile_name = 'default',   
@account_name = 'SQLAlerts',   
@sequence_number = 1;  
 ```
 
## <a name="6-send-test-email"></a>6. -E-Testmail senden
> [!NOTE]
> Möglicherweise müssen Sie Ihre e-Mail-Client werden, und aktivieren, die "erlauben unsicherer Clients zum Senden von e-Mails". Nicht alle Clients erkennen DB E-Mail als eine e-Mail-Daemon.

```
EXECUTE msdb.dbo.sp_send_dbmail 
@profile_name = 'default', 
@recipients = 'recipient-email@gmail.com', 
@Subject = 'Testing DBMail', 
@Body = 'This message is a test for DBMail' 
GO
```

## <a name="7-set-db-mail-profile-using-mssql-conf-or-environment-variable"></a>7. Festlegen Sie DB-Mailprofil mithilfe von Mssql-Conf oder Umgebungsvariable
Sie können der Mssql-Conf-Hilfsprogramm oder Umgebungsvariablen verwenden, um Ihre DB-Mailprofil zu registrieren. In diesem Fall nennen wir unsere Profil-Standard.

```bash
# via mssql-conf
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile default
# via environment variable
MSSQL_AGENT_EMAIL_PROFILE=default
```

## <a name="8-set-up-an-operator-for-sqlagent-job-notifications"></a>8. Richten Sie einen Operator für SQLAgent-auftragsbenachrichtigungen 

```sql
EXEC msdb.dbo.sp_add_operator 
@name=N'JobAdmins',  
@enabled=1, 
@email_address=N'recipient-email@gmail.com',  
@category_name=N'[Uncategorized]' 
GO 
```

## <a name="9-send-email-when-agent-test-job-succeeds"></a>9. Nach der erfolgreichen "Agentauftrag Test" Senden Sie e-Mail 

```
EXEC msdb.dbo.sp_update_job 
@job_name='Agent Test Job', 
@notify_level_email=1, 
@notify_email_operator_name=N'JobAdmins' 
GO
```

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Verwendung von SQL Server-Agent erstellen, Planen und Ausführen von Aufträgen finden Sie unter [führen Sie einen SQL Server-Agent-Auftrag unter Linux](sql-server-linux-run-sql-server-agent-job.md).
