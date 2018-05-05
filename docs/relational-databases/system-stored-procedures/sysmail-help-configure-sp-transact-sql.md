---
title: Sysmail_help_configure_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 823d7549fdf6f2f4e452c5b46f3c914d24528647
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailhelpconfiguresp-transact-sql"></a>sysmail_help_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt Konfigurationseinstellungen für Datenbank-E-Mail an.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [**@parameter_name** =] **"***Parameter_name***"**  
 Der Name der abzurufenden Konfigurationseinstellung. Wenn angegeben, wird der Wert der Konfigurationseinstellung zurückgegeben, der **@parameter_value** OUTPUT-Parameter. Wenn kein **@parameter_name** angegeben ist, wird diese gespeicherte Prozedur gibt ein Resultset mit allen Database Mail Konfigurationseinstellungen in der Instanz zurück.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Wenn kein **@parameter_name** angegeben wird, gibt ein Resultset mit den folgenden Spalten zurück.  
  
||||  
|-|-|-|  
|Spaltenname|Datentyp|Description|  
|**paramname**|**nvarchar(256)**|Der Name des Konfigurationsparameters.|  
|**paramvalue**|**nvarchar(256)**|Der Wert des Konfigurationsparameters.|  
|**description**|**nvarchar(256)**|Die Beschreibung des Konfigurationsparameters.|  
  
## <a name="remarks"></a>Hinweise  
 Die gespeicherte Prozedur **sysmail_help_configure_sp** führt die aktuellen Konfigurationseinstellungen für Datenbank-E-Mail für die Instanz auf.  
  
 Wenn eine **@parameter_name** angegeben ist, jedoch kein Ausgabeparameter dient zur **@parameter_value**, diese gespeicherte Prozedur erzeugt keine Ausgabe.  
  
 Die gespeicherte Prozedur **sysmail_help_configure_sp** befindet sich in der **msdb** -Datenbank und im Besitz des **dbo** -Schemas. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen aufgerufen werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Liste der Mail von Datenbank-Konfigurationseinstellungen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.  
  
```  
EXECUTE msdb.dbo.sysmail_help_configure_sp ;  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde:  
  
```  
paramname                       paramvalue      description  
------------------------------- --------------- -----------------------------------------------------------------------------  
AccountRetryAttempts            1               Number of retry attempts for a mail server  
AccountRetryDelay               5000            Delay between each retry attempt to mail server  
DatabaseMailExeMinimumLifeTime  600             Minimum process lifetime in seconds  
DefaultAttachmentEncoding       MIME            Default attachment encoding  
LoggingLevel                    2               Database Mail logging level: normal - 1, extended - 2 (default), verbose - 3  
MaxFileSize                     1000000         Default maximum file size  
ProhibitedExtensions            exe,dll,vbs,js  Extensions not allowed in outgoing mails  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
