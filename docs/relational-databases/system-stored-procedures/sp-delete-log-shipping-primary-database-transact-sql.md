---
title: Sp_delete_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8f6999fab47e30748646174dcb72ed881359f3c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletelogshippingprimarydatabase-transact-sql"></a>sp_delete_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Diese gespeicherte Prozedur entfernt den Protokollversand der primären Datenbank, einschließlich des Sicherungsauftrags, sowie den lokalen und Remoteverlauf. Verwenden Sie diese gespeicherte Prozedur nur, nachdem Sie die sekundäre Datenbank mithilfe von **sp_delete_log_shipping_primary_secondary**entfernt haben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@database =** ] "*Datenbank*"  
 Der Name der primären Datenbank des Protokollversands. *database* ist vom Datentyp **sysname**, hat keinen Standardwert und darf nicht NULL sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine.  
  
## <a name="remarks"></a>Hinweise  
 **sp_delete_log_shipping_primary_database** muss in der **master** -Datenbank auf dem primären Server ausgeführt werden. Diese gespeicherte Prozedur führt folgende Aktionen aus:  
  
1.  Löscht den Sicherungsauftrag für die angegebene primäre Datenbank.  
  
2.  Entfernt den lokalen Überwachungsdatensatz in **log_shipping_monitor_primary** auf dem primären Server.  
  
3.  Entfernt die entsprechenden Einträge in **log_shipping_monitor_history_detail** und **log_shipping_monitor_error_detail**.  
  
4.  Falls der Überwachungsserver nicht mit dem primären Server übereinstimmt, wird der Überwachungsdatensatz in **log_shipping_monitor_primary** auf dem Überwachungsserver entfernt.  
  
5.  Entfernt die entsprechenden Einträge in **log_shipping_monitor_history_detail** und **log_shipping_monitor_error_detail** auf dem Überwachungsserver.  
  
6.  Entfernt den Eintrag in **log_shipping_primary_databases** für diese primäre Datenbank.  
  
7.  Ruft **sp_delete_log_shipping_alert_job** auf dem Überwachungsserver auf.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können diese Prozedur ausführen.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird die Verwendung von **sp_delete_log_shipping_primary_database** zum Löschen der primären **AdventureWorks2012**-Datenbank erläutert.  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand & #40; SQLServer & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
