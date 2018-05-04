---
title: Sp_dropsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropsubscription
- sp_dropsubscription_TSQL
helpviewer_keywords:
- sp_dropsubscription
ms.assetid: 7551f345-5510-4684-ab53-f9057249d13a
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d6477b090fd3a98626b79a6db83cea729b4dec07
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdropsubscription-transact-sql"></a>sp_dropsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht Abonnements für bestimmte Artikel, Veröffentlichungen oder Abonnementgruppen auf dem Verleger. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
        , [ @subscriber= ] 'subscriber'  
    [ , [ @destination_db= ] 'destination_db' ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=** ] **"***Veröffentlichung***"**  
 Der Name der zugeordneten Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert NULL. Wenn **alle**, alle Abonnements für alle Veröffentlichungen für den angegebenen Abonnenten gelöscht. *Veröffentlichung* ist ein erforderlicher Parameter.  
  
 [  **@article=** ] **"***Artikel***"**  
 Der Name des Artikels. *Artikel* ist **Sysname**, hat den Standardwert NULL. Wenn **alle**, Abonnements für alle Artikel für jeden angegebenen Veröffentlichungen und Abonnenten gelöscht werden. Verwendung **alle** für Veröffentlichungen, die sofortige zulassen aktualisieren.  
  
 [  **@subscriber=** ] **"***abonnieren*r**" **  
 Der Name des Abonnenten, dessen Abonnements gelöscht werden. *Abonnenten* ist **Sysname**, hat keinen Standardwert. Wenn **alle**, alle Abonnements für alle Abonnenten gelöscht werden.  
  
 [  **@destination_db=** ] **"***Destination_db***"**  
 Der Name der Zieldatenbank. *Destination_db* ist **Sysname**, hat den Standardwert NULL. Bei einem Wert von NULL werden alle Abonnements dieses Abonnenten gelöscht.  
  
 [  **@ignore_distributor =** ] *Ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@reserved=** ] **"***reservierte***"**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dropsubscription** wird bei der Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 Wenn Sie das Abonnement für den Artikel einer immediate-sync-Veröffentlichung löschen, können Sie das Abonnement nur wieder hinzufügen, wenn Sie die Abonnements für alle Artikel der Veröffentlichung löschen und sie alle in einem Schritt wieder hinzufügen.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropsubscription-tran_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** festen Datenbankrolle "" oder der Benutzer, der das Abonnement erstellt kann ausführen **Sp_dropsubscription**.  
  
## <a name="see-also"></a>Siehe auch  
 [Löschen eines Pushabonnements](../../relational-databases/replication/delete-a-push-subscription.md)   
 [Sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [Sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
