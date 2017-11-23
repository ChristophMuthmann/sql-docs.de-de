---
title: Sp_help_publication_access (Transact-SQL) | Microsoft Docs
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
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords: sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1568ded984bcb38c6633fdf5ceddfb2b960df41b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelppublicationaccess-transact-sql"></a>sp_help_publication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Liste aller Anmeldenamen zurück, denen der Zugriff auf eine Veröffentlichung erteilt wurde. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, auf die zugegriffen werden soll. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@return_granted=**] **"***Return_granted***"**  
 Die Login-ID *Return_granted* ist **Bit**, hat den Standardwert 1. Wenn **0** angegeben ist und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwendet wird, werden die verfügbaren Anmelde-IDs, die auf dem Verleger, aber nicht auf dem Verteiler angezeigt werden zurückgegeben. Wenn **0** angegeben ist und Windows-Authentifizierung verwendet, die Anmeldungen, die nicht explizit verweigert zugreifen auf den Verleger oder Verteiler werden zurückgegeben.  
  
 [  **@login=**] **"***Anmeldung***"**  
 Die Standardsicherheits-Anmelde-ID. *Anmeldung* ist **Sysname**, hat den Standardwert  **%** .  
  
 [  **@initial_list =**] *Initial_list*  
 Gibt an, ob alle Elemente mit Veröffentlichungszugriff zurückgegeben werden oder nur die Elemente, die Zugriff hatten, bevor der Liste neue Elemente hinzugefügt wurden. *Initial_list* bit und hat den Standardwert **0**.  
  
 **1** gibt Informationen für alle Mitglieder der **Sysadmin** festen Serverrolle mit gültigen Anmeldenamen auf dem Verteiler, die vorhanden waren, wenn die Veröffentlichung erstellt wurde, sowie die aktuelle Anmeldung.  
  
 **0** gibt Informationen für alle Mitglieder der **Sysadmin** über gültige Anmeldenamen auf dem Verteiler, die beim Erstellen der Veröffentlichung sowie alle Benutzer in der veröffentlichungszugriffsliste vorlag, die keinen festen Serverrolle "" gehören zu den **Sysadmin** festen Serverrolle "".  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**nvarchar(256)**|Tatsächlicher Anmeldename|  
|**Isntname**|**int**|**0** = Anmeldename ist kein Windows-Benutzer.<br /><br /> **1** = Anmeldename ist ein Windows-Benutzer.|  
|**Isntgroup**|**int**|**0** = Anmeldename ist nicht mit einer Windows-Gruppe.<br /><br /> **1** = Anmeldename ist eine Windows-Gruppe.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_help_publication_access** wird für alle Replikationstypen verwendet.  
  
 Wenn beide **Isntname** und **Isntgroup** im Ergebnis sind **0**, es wird davon ausgegangen, dass der Anmeldename eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_help_publication_access**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_grant_publication_access &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [Sp_revoke_publication_access &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
