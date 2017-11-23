---
title: Sp_register_custom_scripting (Transact-SQL) | Microsoft Docs
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
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords: sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16274b71d1ce14b2a143e5d6ce723bcb64cbaebd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mithilfe der Replikation ist es möglich, mindestens eine der bei der Transaktionsreplikation verwendeten Standardprozeduren durch benutzerdefinierte gespeicherte Prozeduren zu ersetzen. Wenn an einer replizierten Tabelle eine Schemaänderung vorgenommen wird, werden diese gespeicherten Prozeduren neu erstellt. **Sp_register_custom_scripting** registriert eine gespeicherte Prozedur oder [!INCLUDE[tsql](../../includes/tsql-md.md)] Skriptdatei, die ausgeführt wird, wenn das Skript die Definition für eine neue benutzerdefinierte benutzerdefinierte gespeicherte Prozedur eine schemaänderung erfolgt. Diese neue, benutzerdefinierte gespeicherte Prozedur sollte das neue Schema für die Tabelle wiedergeben. **Sp_register_custom_scripting** auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt wird und die registrierte Skriptdatei bzw. gespeicherte Prozedur auf dem Abonnenten ausgeführt wird, sobald eine schemaänderung erfolgt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@type**  =] **"***Typ***"**  
 Der Typ der benutzerdefinierten gespeicherten Prozedur oder des Skripts, die bzw. das registriert wird. *Typ* ist **varchar(16)**, hat keinen Standardwert und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Einfügen**|Die registrierte, benutzerdefinierte gespeicherte Prozedur wird ausgeführt, wenn eine INSERT-Anweisung repliziert wird.|  
|**Aktualisieren**|Die registrierte, benutzerdefinierte gespeicherte Prozedur wird ausgeführt, wenn eine UPDATE-Anweisung repliziert wird.|  
|**Löschen**|Die registrierte, benutzerdefinierte gespeicherte Prozedur wird ausgeführt, wenn eine DELETE-Anweisung repliziert wird.|  
|**custom_script**|Das Skript wird am Ende des DDL-Triggers (Data Definition Language) ausgeführt.|  
  
 [  **@value** =] **"***Wert***"**  
 Der Name einer gespeicherten Prozedur oder der Name und vollqualifizierter Pfad der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skriptdatei, die registriert wird. *Wert* ist **nvarchar(1024)**, hat keinen Standardwert.  
  
> [!NOTE]  
>  Angeben von NULL für *Wert*Parameter die Registrierung eines zuvor registrierten Skripts, die die gleiche als aktiv ist [Sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md).  
  
 Wenn der Wert der *Typ* ist **Custom_script**, den Namen und den vollständigen Pfad ein [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skriptdatei erwartet. Andernfalls *Wert* muss der Name einer registrierten gespeicherten Prozedur sein.  
  
 [  **@publication** =] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, für die die benutzerdefinierte gespeicherte Prozedur bzw. das Skript registriert wird. *Veröffentlichung* ist **Sysname**, hat den Standardwert **NULL**.  
  
 [  **@article** =] **"***Artikel***"**  
 Der Name des Artikels, für den die benutzerdefinierte gespeicherte Prozedur bzw. das Skript registriert wird. *Artikel* ist **Sysname**, hat den Standardwert **NULL**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_register_custom_scripting** wird bei der Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 Diese gespeicherte Prozedur sollte ausgeführt werden, bevor Schemaänderungen an einer replizierten Tabelle vorgenommen werden. Weitere Informationen zur Verwendung dieser gespeicherten Prozedur finden Sie unter [neu generieren benutzerdefinierter transaktionale Verfahren zum Schemaänderungen widerspiegeln](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle die **Db_owner** feste Datenbankrolle oder der **Db_ddladmin** feste Datenbankrolle können ausführen **"sp_" Register_custom_scripting**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_unregister_custom_scripting &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
