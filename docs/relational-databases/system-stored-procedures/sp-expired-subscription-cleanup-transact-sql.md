---
title: Sp_expired_subscription_cleanup (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_expired_subscription_cleanup
- SP_EXPIRED_SUBSCRIPTION_CLEANUP_TSQL
helpviewer_keywords: sp_expired_subscription_cleanup
ms.assetid: 6abc29fe-d77a-4673-9d99-ae31c688012c
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b2da325d403d6a7965cf6a211c07a4809598bdf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spexpiredsubscriptioncleanup-transact-sql"></a>sp_expired_subscription_cleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Überprüft den Status aller Abonnements für jede Veröffentlichung und löscht abgelaufene Abonnements. Diese gespeicherte Prozedur ausgeführt wird, auf dem Verleger für jede Datenbank oder auf dem Verteiler für die Verteilungsdatenbank für einen nicht-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_expired_subscription_cleanup [ [ @publisher = ] 'publisher' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publisher=** ] **"***Publisher***"**  
 Der Name eines Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verlegers. *Veröffentlichung* ist **Sysname**, hat den Standardwert NULL. Sie sollten diesen Parameter nicht für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger festlegen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_expired_subscription_cleanup** wird für alle Replikationstypen verwendet.  
  
 **Sp_expired_subscription_cleanup** vom Auftrag Cleanup abgelaufener Abonnements zu erkennen und entfernt abgelaufene Abonnements aus Veröffentlichungsdatenbanken alle 24 Stunden ausgeführt wird. Wenn ein Abonnement nicht mehr aktuell ist, wenn es also während der Beibehaltungsdauer nicht mit dem Verleger synchronisiert wurde, wird die Veröffentlichung als abgelaufen bezeichnet. Die Ablaufverfolgungsdaten des Abonnements werden dann auf dem Verleger gelöscht. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_expired_subscription_cleanup**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_mergesubscription_cleanup &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [Sp_subscription_cleanup &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
