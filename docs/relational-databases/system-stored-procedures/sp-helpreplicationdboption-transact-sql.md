---
title: Sp_helpreplicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpreplicationdboption_TSQL
- sp_helpreplicationdboption
helpviewer_keywords:
- sp_helpreplicationdboption
ms.assetid: 143ce689-108b-49d7-9892-fd3a86897f38
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d53bf08bf26d8682093d72e55f290701d0b3c625
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpreplicationdboption-transact-sql"></a>sp_helpreplicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt an, ob die Datenbanken auf dem Verleger für die Replikation aktiviert sind. Diese gespeicherte Prozedur wird auf dem Verleger für jede Datenbank ausgeführt. *Für Oracle-Verlegern unterstützt nicht.*  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpreplicationdboption [ [ @dbname =] 'dbname' ]  
    [ , [ @type = ] 'type' ]  
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@dbname=**] **"***Dbname***"**  
 Der Name der Datenbank. *Dbname* ist **Sysname**, hat den Standardwert  **%** . Wenn  **%** , klicken Sie dann das Resultset enthält alle Datenbanken auf dem Verleger, andernfalls nur Informationen für die angegebene Datenbank zurückgegeben. Es werden keine Informationen für Datenbanken zurückgegeben, für die der Benutzer wie nachstehend beschrieben keine entsprechenden Berechtigungen besitzt.  
  
 [  **@type=**] **"***Typ***"**  
 Beschränkt das Resultset enthält nur Datenbanken, für die der angegebenen Replikationsoption *Typ* Wert aktiviert wurde. *Typ* ist **Sysname**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Veröffentlichen**|Transaktionsreplikation ist zulässig.|  
|**Veröffentlichen von Merge**|Mergereplikation ist zulässig.|  
|**Replikation zulässig** (Standard)|Transaktionsreplikation und Mergereplikation sind zulässig.|  
  
 [  **@reserved=** ] *reservierte*  
 Gibt an, ob Informationen zu vorhandenen Veröffentlichungen und Abonnements zurückgegeben werden. *reservierte* ist **Bit**, hat den Standardwert 0. Wenn **1**, enthält das Resultset Informationen dazu, ob die angegebene Datenbank über vorhandene Veröffentlichungen oder Abonnements verfügt.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name der Datenbank.|  
|**id**|**int**|Datenbankbezeichner.|  
|**transpublish**|**bit**|Wenn die Datenbank für Momentaufnahme- oder transaktionsveröffentlichungen aktiviert wurde; ein Wert von **1** bedeutet, dass Momentaufnahme- oder transaktionsveröffentlichungen aktiviert ist.|  
|**mergepublish**|**bit**|Wenn die Datenbank für die Mergereplikation, die publishing aktiviert wurde; ein Wert von **1** bedeutet, dass mergeveröffentlichungen aktiviert ist.|  
|**dbowner**|**bit**|Wenn der Benutzer Mitglied ist die **Db_owner** festen Datenbankrolle ""; der Wert **1** gibt an, dass der Benutzer ein Mitglied dieser Rolle ist.|  
|**dbReadOnly**|**bit**|Ist, wenn die Datenbank als schreibgeschützt markiert ist. ein Wert von **1** bedeutet, dass die Datenbank schreibgeschützt ist.|  
|**haspublications**|**bit**|Ist, wenn die Datenbank vorhandenen Veröffentlichungen aufweist. ein Wert von **1** bedeutet, dass Veröffentlichungen vorhanden sind.|  
|**haspullsubscriptions**|**bit**|Ist, wenn die Datenbank vorhandene Pullabonnements verfügt. ein Wert von **1** bedeutet, dass Pullabonnements vorhanden sind.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpreplicationdboption** wird bei Momentaufnahme-, Transaktions- und Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Mitglied der **Sysadmin** -Serverrolle kann ausführen **Sp_helpreplicationdboption** für eine beliebige Datenbank. Mitglieder der **Db_owner** feste Datenbankrolle können ausführen **Sp_helpreplicationdboption** für diese Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_replicationdboption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
