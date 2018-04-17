---
title: Sp_unregister_custom_scripting (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1d2d1e9e081984645fcad82d59d6229f30225502
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spunregistercustomscripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese gespeicherte Prozedur entfernt eine benutzerdefinierte benutzerdefinierte gespeicherte Prozedur oder [!INCLUDE[tsql](../../includes/tsql-md.md)] Skriptdatei, die durch das Ausführen registriert war [Sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md). Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@type** =] **"***Typ***"**  
 Der Typ der benutzerdefinierten gespeicherten Prozedur oder des Skripts, die bzw. das entfernt wird. *Typ* ist **varchar(16)**, hat keinen Standardwert und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**insert**|Registrierte benutzerdefinierte gespeicherte Prozedur oder Skript wird ausgeführt, wenn eine INSERT-Anweisung repliziert wird.|  
|**Update**|Registrierte benutzerdefinierte gespeicherte Prozedur oder Skript wird ausgeführt, wenn eine UPDATE-Anweisung repliziert wird.|  
|**Löschen**|Registrierte benutzerdefinierte gespeicherte Prozedur oder Skript wird ausgeführt, wenn eine DELETE-Anweisung repliziert wird.|  
|**custom_script**|Registrierte benutzerdefinierte gespeicherte Prozedur oder Skript wird am Ende des DDL-Triggers (Data Definition Language) ausgeführt.|  
  
 [ **@publication** =] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, für die die benutzerdefinierte gespeicherte Prozedur bzw. das Skript entfernt wird. *Veröffentlichung* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@article** =] **"***Artikel***"**  
 Der Name des Artikels, für den die benutzerdefinierte gespeicherte Prozedur bzw. das Skript entfernt wird. *Artikel* ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_unregister_custom_scripting** wird bei der Momentaufnahme- und Transaktionsreplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle die **Db_owner** feste Datenbankrolle oder der **Db_ddladmin** feste Datenbankrolle können ausführen **"sp_" Unregister_custom_scripting**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_register_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
