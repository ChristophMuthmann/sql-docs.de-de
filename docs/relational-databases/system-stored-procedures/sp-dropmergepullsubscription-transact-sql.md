---
title: Sp_dropmergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- sp_dropmergepullsubscription
- sp_dropmergepullsubscription_TSQL
helpviewer_keywords: sp_dropmergepullsubscription
ms.assetid: 9301dd80-72f7-4adb-9b13-87e7f9114248
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 20bae9a8d1a27e0ec4a02a6cb3dc632fa50924ae
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spdropmergepullsubscription-transact-sql"></a>sp_dropmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht ein Mergepullabonnement. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropmergepullsubscription [ @publication= ] 'publication'   
        , [ @publisher= ] 'publisher'   
        , [ @publisher_db= ] 'publisher_db'   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter ist erforderlich. Geben Sie den Wert **alle** um Abonnements für alle Veröffentlichungen zu entfernen.  
  
 [  **@publisher=**] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher*ist **Sysname**, hat den Standardwert NULL. Dieser Parameter ist erforderlich.  
  
 [  **@publisher_db=**] **"***Publisher_db***"**  
 Der Name der Verlegerdatenbank. *Publisher_db*ist **Sysname**, hat den Standardwert NULL. Dieser Parameter ist erforderlich.  
  
 [  **@reserved=**] **"***reservierte***"**  
 Ist für die zukünftige Verwendung reserviert. *reservierte* ist **Bit**, hat den Standardwert **0**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dropmergepullsubscription** wird bei der Mergereplikation verwendet.  
  
 **Sp_dropmergepullsubscription** löscht den Merge-Agent für dieses Mergepullabonnement, obwohl der Merge-Agent nicht in erstellt wird **Sp_addmergepullsubscription**.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepullsubscrip_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** feste Serverrolle oder der Benutzer, der das Mergepullabonnement erstellt kann ausführen **Sp_dropmergepullsubscription**. Die **Db_owner** festen Datenbankrolle "" ist nur in der Lage, führen Sie **Sp_dropmergepullsubscription** , wenn der Benutzer, der das Mergepullabonnement erstellt, die dieser Rolle gehört.  
  
## <a name="see-also"></a>Siehe auch  
 [Löschen eines Pullabonnements](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [Sp_addmergepullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [Sp_changemergepullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [Sp_dropmergesubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [Sp_helpmergepullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)  
  
  
