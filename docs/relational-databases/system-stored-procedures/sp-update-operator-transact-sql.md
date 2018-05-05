---
title: Sp_update_operator (Transact-SQL) | Microsoft Docs
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
- sp_update_operator_TSQL
- sp_update_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_operator
ms.assetid: 231750a6-4828-4d03-afe6-b91d38c42ed3
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: de401baa9ebff88d7745f7bc3af03660af3b0da2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spupdateoperator-transact-sql"></a>sp_update_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert Informationen zu einem Operator (Benachrichtigungsempfänger) für die Verwendung mit Warnungen und Aufträgen.  
  
   ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_update_operator   
     [ @name =] 'name'   
     [ , [ @new_name = ] 'new_name' ]   
     [ , [ @enabled = ] enabled]   
     [ , [ @email_address = ] 'email_address' ]  
     [ , [ @pager_address = ] 'pager_number']   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]  
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]  
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]  
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @name=] '*name*'  
 Der Name des zu ändernden Operators. *Namen* ist **Sysname**, hat keinen Standardwert.  
  
 [ @new_name=] '*New_name*"  
 Der neue Name des Operators. Dieser Name muss eindeutig sein. *New_name* ist **Sysname**, hat den Standardwert NULL.  
  
 [ @enabled=] *enabled*  
 Eine Zahl, aktuellen Status des Operators (**1** Wenn derzeit aktiviert, **0** anderenfalls). *aktiviert* ist **"tinyint"**, hat den Standardwert NULL. Bei deaktivierter Option empfängt der Operator keine Warnbenachrichtigungen.  
  
 [ @email_address=] '*email_address*'  
 Die E-Mail-Adresse des Operators. Diese Zeichenfolge wird direkt an das E-Mail-System übergeben. *Email_address* ist **nvarchar(100)**, hat den Standardwert NULL.  
  
 [ @pager_address=] '*pager_number*'  
 Gibt die Pageradresse des Operators an. Diese Zeichenfolge wird direkt an das E-Mail-System übergeben. *pager_address* ist **nvarchar(100)**, hat den Standardwert NULL.  
  
 [ @weekday_pager_start_time=] *weekday_pager_start_time*  
 Gibt die Uhrzeit an, nach der von Montag bis Freitag eine Pagerbenachrichtigung an diesen Operator gesendet werden kann. *Weekday_pager_start_time*ist **Int**, hat den Standardwert NULL, muss im Format HHMMSS für die Verwendung mit einem 24-Stunden-Format eingegeben werden.  
  
 [ @weekday_pager_end_time=] *weekday_pager_end_time*  
 Gibt die Uhrzeit an, nach der von Montag bis Freitag eine Pagerbenachrichtigung nicht an den angegebenen Operator gesendet werden kann. *Weekday_pager_end_time*ist **Int**, hat den Standardwert NULL, muss im Format HHMMSS für die Verwendung mit einem 24-Stunden-Format eingegeben werden.  
  
 [ @saturday_pager_start_time=] *saturday_pager_start_time*  
 Gibt die Uhrzeit an, nach der samstags eine Pagerbenachrichtigung an den angegebenen Operator gesendet werden kann. *Saturday_pager_start_time*ist **Int**, hat den Standardwert NULL, muss im Format HHMMSS für die Verwendung mit einem 24-Stunden-Format eingegeben werden.  
  
 [ @saturday_pager_end_time=] *saturday_pager_end_time*  
 Gibt die Uhrzeit an, nach der samstags eine Pagerbenachrichtigung nicht an den angegebenen Operator gesendet werden kann. *Saturday_pager_end_time*ist **Int**, hat den Standardwert NULL, muss im Format HHMMSS für die Verwendung mit einem 24-Stunden-Format eingegeben werden.  
  
 [ @sunday_pager_start_time=] *sunday_pager_start_time*  
 Gibt die Uhrzeit an, nach der sonntags eine Pagerbenachrichtigung an den angegebenen Operator gesendet werden kann. *Sunday_pager_start_time*ist **Int**, hat den Standardwert NULL, muss im Format HHMMSS für die Verwendung mit einem 24-Stunden-Format eingegeben werden.  
  
 [ @sunday_pager_end_time=] *sunday_pager_end_time*  
 Gibt die Uhrzeit an, nach der sonntags eine Pagerbenachrichtigung nicht an den angegebenen Operator gesendet werden kann. *Sunday_pager_end_time*ist **Int**, hat den Standardwert NULL, muss im Format HHMMSS für die Verwendung mit einem 24-Stunden-Format eingegeben werden.  
  
 [ @pager_days=] *pager_days*  
 Gibt an, an welchen Tagen der Operator für den Empfang von Seiten zur Verfügung steht (vorbehaltlich der angegebenen Start-/Beendigungszeiten). *Pager_days*ist **"tinyint"**, hat den Standardwert NULL und muss ein Wert von **0** über **127**. *Pager_days* berechnet, indem die einzelnen Werte für die erforderlichen Tage addiert. Beispielsweise wird von Montag bis Freitag **2**+**4**+**8**+**16** + **32** = **64**.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Sonntag|  
|**2**|Montag|  
|**4**|Dienstag|  
|**8**|Mittwoch|  
|**16**|Donnerstag|  
|**32**|Freitag|  
|**64**|Samstag|  
  
 [ @netsend_address=] '*netsend_address*'  
 Die Netzwerkadresse des Operators, an die die Netzwerknachricht gesendet wird. *Netsend_address*ist **nvarchar(100)**, hat den Standardwert NULL.  
  
 [ @category_name=] '*category*'  
 Der Name der Kategorie für diese Warnung. *Kategorie* ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 sp_update_operator muss aus der msdb-Datenbank ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Berechtigungen zur Ausführung dieser Prozedur erhalten standardmäßig Mitglieder der festen Serverrolle sysadmin.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Operatorstatus zu 'enabled' aktualisiert und die Tage festgelegt (von Montag bis Freitag, 8:00 Uhr bis 17:00 Uhr), an denen der Operator per Pager erreichbar ist.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_operator   
    @name = N'François Ajenstat',  
    @enabled = 1,  
    @email_address = N'françoisa',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 64 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
