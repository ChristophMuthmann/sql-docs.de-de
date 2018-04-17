---
title: Sysmail_stop_sp (Transact-SQL) | Microsoft Docs
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
- sysmail_stop_sp_TSQL
- sysmail_stop_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_stop_sp
ms.assetid: 045ee36f-5bf0-4626-b5ee-e84db06ce16f
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 68adf78c4f9cb978b7551e65ca5afa1fe2596a97
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailstopsp-transact-sql"></a>sysmail_stop_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Beendet Datenbank-Mail durch Beenden der [!INCLUDE[ssSB](../../includes/sssb-md.md)] Objekte, die vom externen Programm verwendet.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_stop_sp  
```  
  
## <a name="arguments"></a>Argumente  
 Keine  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Diese gespeicherte Prozedur wird in der **msdb** -Datenbank gespeichert.  
  
 Diese gespeicherte Prozedur beendet die Database Mail-Warteschlange, die ausgehende benachrichtigungsanforderungen und deaktiviert die [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Aktivierung für das externe Programm.  
  
 Wenn die Warteschlangen beendet werden, verarbeitet das externe Datenbank-E-Mail-Programm keine Nachrichten. Diese gespeicherte Prozedur ermöglicht Ihnen das Beenden von Datenbank-E-Mail für die Problembehandlung oder Wartungsaufgaben.  
  
 Starten Sie Datenbank-E-Mail mithilfe von **sysmail_start_sp**. Beachten Sie, dass **Sp_send_dbmail** weiterhin akzeptiert Nachrichten, wenn die [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Objekte beendet werden.  
  
> [!NOTE]  
>  Mit dieser gespeicherten Prozedur werden nur die Warteschlangen von Datenbank-E-Mail beendet. Diese gespeicherte Prozedur nicht deaktiviert [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Nachrichtenübermittlung in der Datenbank. Mit dieser gespeicherten Prozedur werden die erweiterten gespeicherten Prozeduren von Datenbank-E-Mail zur Oberflächenreduzierung nicht deaktiviert. Deaktivieren die erweiterten gespeicherten Prozeduren finden Sie in der [Database Mail XPs-Option](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) von der **Sp_configure** gespeicherten Systemprozedur.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das Beenden von Datenbank-E-Mail in der **msdb** -Datenbank veranschaulicht. Im Rahmen des Beispiels wird davon ausgegangen, dass die Datenbank-E-Mail aktiviert wurde.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_stop_sp ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_start_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [Database Mail gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
