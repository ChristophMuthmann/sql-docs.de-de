---
title: Sp_defaultlanguage (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfd63d6dddf3cc553ffee62dffbacff891d1991c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spdefaultlanguage-transact-sql"></a>sp_defaultlanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Standardsprache für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@loginame =** ] **"***Anmeldung***"**  
 Der Anmeldename. *login* ist vom Datentyp **sysname**und hat keinen Standardwert. *Anmeldung* kann eine vorhandene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung, einem Windows-Benutzer oder Gruppe.  
  
 [  **@language =** ] **"***Sprache***"**  
 Die Standardsprache der Anmeldung. *language* ist vom Datentyp **sysname**und hat den Standardwert NULL. *Sprache* muss eine gültige Sprache auf dem Server sein. Wenn *Sprache* nicht angegeben ist, *Sprache* festgelegt ist, um die Standardsprache des Servers; Standardsprache wird definiert, indem die **Sp_configure** Konfigurationsvariable **Standardsprache**. Wird die Standardsprache des Servers geändert, ändert sich dadurch nicht die Standardsprache der vorhandenen Anmeldenamen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_defaultlanguage** ruft ALTER LOGIN auf, wodurch zusätzliche Optionen unterstützt. Informationen zum Ändern anderer Standardwerte für Anmeldenamen finden Sie unter [ALTER LOGIN &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-login-transact-sql.md).  
  
 Mit der SET LANGUAGE-Anweisung können Sie die Sprache der aktuellen Sitzung ändern. Verwenden der @@LANGUAGE Funktion, um die aktuelle Spracheinstellung anzeigen.  
  
 Wenn die Standardsprache eines Anmeldenamens vom Server gelöscht wird, übernimmt der Anmeldename die Standardsprache des Servers. **Sp_defaultlanguage** kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
 Informationen zu den auf dem Server installierten Sprachen werden in der **sys.syslanguages** -Katalogsicht angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY LOGIN-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `ALTER LOGIN` zum Ändern der Standardsprache für den Anmeldenamen `Fathima` auf Arabisch geändert. Dies ist die bevorzugte Methode.  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [Sys.syslanguages &#40; Transact-SQL &#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
