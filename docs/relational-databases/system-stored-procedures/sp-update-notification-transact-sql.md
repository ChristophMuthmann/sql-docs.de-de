---
title: Sp_update_notification (Transact-SQL) | Microsoft Docs
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
- sp_update_notification_TSQL
- sp_update_notification
dev_langs: TSQL
helpviewer_keywords: sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44b2755dca0a8d3cd2dae7d11e12cc16a708fe1e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spupdatenotification-transact-sql"></a>sp_update_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert die Benachrichtigungsmethode für eine Warnbenachrichtigung.  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@alert_name =**] **"***Warnung***"**  
 Der Name der dieser Benachrichtigung zugeordneten Warnung. *Warnung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@operator_name =**] **"***Operator***"**  
 Der Operator, der bei Auftreten der Warnung benachrichtigt wird. *Operator* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@notification_method =**] *Benachrichtigung*  
 Die Methode, durch die der Operator benachrichtigt wird. *Benachrichtigung*ist **"tinyint"**, hat keinen Standardwert und kann eine oder mehrere der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|E-Mail|  
|**2**|Pager|  
|**4**|**net send**|  
|**7**|Alle Methoden|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_update_notification** muss ausgeführt werden, aus der **Msdb** Datenbank.  
  
 Sie können eine Benachrichtigung für einen Operator, der nicht die notwendigen Adressinformationen unter Verwendung des angegebenen hat aktualisieren *Notification_method*. Wenn beim Senden einer E-Mail- oder Pagerbenachrichtigung ein Fehler auftritt, wird der Fehler im Fehlerprotokoll des Microsoft SQL Server-Agents angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Um diese gespeicherte Prozedur auszuführen, müssen Benutzer gewährt werden die **Sysadmin** festen Serverrolle "".  
  
## <a name="examples"></a>Beispiele  
 Im folgende Beispiel ändert die Benachrichtigungsmethode für Benachrichtigungen an `François Ajenstat`für die Warnung `Test Alert`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_add_notification &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [Sp_delete_notification &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [Sp_help_notification &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
