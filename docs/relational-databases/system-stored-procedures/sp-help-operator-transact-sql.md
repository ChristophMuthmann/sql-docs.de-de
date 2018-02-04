---
title: Sp_help_operator (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_operator
- sp_help_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_operator
ms.assetid: caedc43d-44b8-415a-897e-92923f6de3b8
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc89c5f6689b64aea7be0410850f373d75d876e6
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sphelpoperator-transact-sql"></a>sp_help_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu den für den Server definierten Operatoren zurück.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_operator  
     { [ @operator_name = ] 'operator_name'   
     | [ @operator_id = ] operator_id }  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@operator_name=** ] **'***operator_name***'**  
 Der Name des Operators. *Operatorname* ist **Sysname**. Wenn *Operatorname* ist nicht angegeben wird, werden Informationen zu allen Operatoren zurückgegeben.  
  
 [ **@operator_id=** ] *operator_id*  
 Die ID des Operators, für den Informationen angefordert werden. *Operator_id*ist **Int**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Operator_id* oder *Operatorname* muss angegeben werden, aber beide können nicht angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Operator-ID zurück.|  
|**name**|**sysname**|Name des Operators.|  
|**enabled**|**tinyint**|Operator steht für den Empfang von Benachrichtigungen zur Verfügung:<br /><br /> **1** = Ja<br /><br /> **0** = Nein|  
|**email_address**|**nvarchar(100)**|E-Mail-Adresse des Operators.|  
|**last_email_date**|**int**|Datum, an dem der Operator zuletzt per E-Mail benachrichtigt wurde.|  
|**last_email_time**|**int**|Uhrzeit, zu der der Operator zuletzt per E-Mail benachrichtigt wurde.|  
|**pager_address**|**nvarchar(100)**|Pageradresse des Operators.|  
|**last_pager_date**|**int**|Datum, an dem der Operator zuletzt per Pager benachrichtigt wurde.|  
|**last_pager_time**|**int**|Uhrzeit, zu der der Operator zuletzt per Pager benachrichtigt wurde.|  
|**weekday_pager_start_time**|**int**|Der Beginn des Zeitraums, während dessen der Operator an Arbeitstagen zur Verfügung steht, um Pagerbenachrichtigungen zu empfangen.|  
|**weekday_pager_end_time**|**int**|Das Ende des Zeitraums, während dessen der Operator an Arbeitstagen zur Verfügung steht, um Pagerbenachrichtigungen zu empfangen.|  
|**saturday_pager_start_time**|**int**|Der Beginn des Zeitraums, während dessen der Operator an Samstagen zur Verfügung steht, um Pagerbenachrichtigungen zu empfangen.|  
|**saturday_pager_end_time**|**int**|Das Ende des Zeitraums, während dessen der Operator an Samstagen zur Verfügung steht, um Pagerbenachrichtigungen zu empfangen.|  
|**sunday_pager_start_time**|**int**|Der Beginn des Zeitraums, während dessen der Operator an Sonntagen zur Verfügung steht, um Pagerbenachrichtigungen zu empfangen.|  
|**sunday_pager_end_time**|**int**|Das Ende des Zeitraums, während dessen der Operator an Sonntagen zur Verfügung steht, um Pagerbenachrichtigungen zu empfangen.|  
|**pager_days**|**tinyint**|Eine Bitmaske (**1** = Sonntag, **64** = Samstag) Tage die Woche, der angibt, wann der Operator für den Empfang von Pagerbenachrichtigungen verfügbar ist.|  
|**netsend_address**|**nvarchar(100)**|Operatoradresse für Benachrichtigungen per Netzwerk-Popupnachricht.|  
|**last_netsend_date**|**int**|Datum, an dem der Operator zuletzt per Netzwerk-Popupnachricht benachrichtigt wurde.|  
|**last_netsend_time**|**int**|Uhrzeit, zu der der Operator zuletzt per Netzwerk-Popupnachricht benachrichtigt wurde.|  
|**category_name**|**sysname**|Name der Operatorkategorie, zu der dieser Operator gehört.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_help_operator** muss ausgeführt werden, aus der **Msdb** Datenbank.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zum `François Ajenstat`-Operator ausgegeben.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_operator  
    @operator_name = N'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
