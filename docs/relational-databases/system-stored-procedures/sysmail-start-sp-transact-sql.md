---
title: Sysmail_start_sp (Transact-SQL) | Microsoft Docs
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
- sysmail_start_sp
- sysmail_start_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_start_sp
ms.assetid: 25fd7bb6-cfdd-463f-bea8-c6fcb805d3f5
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9789d454961e9bb22e5d35c36b4be47056ef7739
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailstartsp-transact-sql"></a>sysmail_start_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Startet Datenbank-E-Mail durch Starten der vom externen Programm verwendeten [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Objekte.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_start_sp  
```  
  
## <a name="arguments"></a>Argumente  
 Keine  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Database Mail nicht aktiviert oder unangetastet[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Installation. Verwenden Sie den Assistenten zum Konfigurieren von Datenbank-E-Mail zum Aktivieren und Installieren der Datenbank-E-Mail-Objekte.  
  
 Diese gespeicherte Prozedur wird in der **msdb** -Datenbank gespeichert. Diese gespeicherte Prozedur startet die Datenbank-E-Mail-Warteschlange, die ausgehende Benachrichtigungsanforderungen enthält, und aktiviert die [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Unterstützung für das externe Programm.  
  
 Wenn die Warteschlangen gestartet werden, kann das externe Datenbank-E-Mail-Programm Nachrichten verarbeiten. Mit dieser Prozedur können Sie die Warteschlangen erneut starten, nachdem die Warteschlangen beendet wurden die **Sysmail_stop_sp** gespeicherte Prozedur.  
  
> [!NOTE]  
>  Mit dieser gespeicherten Prozedur werden nur die Warteschlangen der Datenbank-E-Mail gestartet. Diese gespeicherte Prozedur aktiviert die [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Nachrichtenübermittlung in der Datenbank nicht.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt Database Mail ab der **Msdb** Datenbank. Im Rahmen des Beispiels wird davon ausgegangen, dass die Datenbank-E-Mail aktiviert wurde.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_start_sp ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail XPs-Serverkonfigurationsoption](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)   
 [sysmail_stop_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)   
 [Database Mail gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
