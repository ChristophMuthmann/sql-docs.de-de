---
title: Sp_password (Transact-SQL) | Microsoft Docs
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
- sp_password
- sp_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_password
ms.assetid: 0ecbec81-e637-44a9-a61e-11bf060ef084
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b461f601e94756d1406da13f1da99f8b1df50198
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sppassword-transact-sql"></a>sp_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Hinzufügt oder ändert ein Kennwort für ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_password [ [ @old = ] 'old_password' , ]  
     { [ @new =] 'new_password' }  
     [ , [ @loginame = ] 'login' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@old=** ] **"***Old_password***"**  
 Ist das alte Kennwort. *Old_password* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@new=** ] **"***Neues_Kennwort***"**  
 Ist das neue Kennwort. *Neues_Kennwort* ist **Sysname**, hat keinen Standardwert. *Old_password* muss angegeben werden, wenn keine benannten Parameter verwendet werden.  
  
> [!IMPORTANT]  
>  Verwenden Sie kein NULL-Kennwort. Verwenden Sie ein sicheres Kennwort. Weitere Informationen finden Sie unter [Strong Passwords](../../relational-databases/security/strong-passwords.md).  
  
 [  **@loginame=** ] **"***Anmeldung***"**  
 Der Name der von der Kennwortänderung betroffenen Anmeldung. *login* ist vom Datentyp **sysname**und hat den Standardwert NULL. *Anmeldung* muss bereits vorhanden und kann nur von Mitgliedern der angegeben werden die **Sysadmin** oder **"securityadmin"** festen Serverrollen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_password** ruft ALTER LOGIN. Diese Anweisung unterstützt weitere Optionen. Informationen zum Ändern von Kennwörtern finden Sie unter [ALTER LOGIN &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-login-transact-sql.md).  
  
 **Sp_password** kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY LOGIN-Berechtigung. Darüber hinaus wird die CONTROL SERVER-Berechtigung zum Zurücksetzen eines Kennworts ohne Bereitstellen des alten Kennworts benötigt; diese ist auch erforderlich, wenn der zu ändernde Anmeldename über die CONTROL SERVER-Berechtigung verfügt.  
  
 Ein Prinzipal kann sein eigenes Kennwort ändern.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-password-of-a-login-without-knowing-the-old-password"></a>A. Ändern des Kennwortes einer Anmeldung ohne Kenntnis des alten Kennworts  
 Das folgende Beispiel veranschaulicht, wie mit `ALTER LOGIN` das Kennwort für den Anmeldenamen `Victoria` in `B3r1000d#2-36` geändert wird. Dies ist die bevorzugte Methode. Der Benutzer, der diesen Befehl ausführt, benötigt die CONTROL SERVER-Berechtigung.  
  
```  
ALTER LOGIN Victoria WITH PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
### <a name="b-changing-a-password"></a>B. Ändern eines Kennwortes  
 Das folgende Beispiel veranschaulicht, wie mit `ALTER LOGIN` das Kennwort für den Anmeldenamen `Victoria` von `B3r1000d#2-36` in `V1cteAmanti55imE` geändert wird. Dies ist die bevorzugte Methode. Der Benutzer `Victoria` kann diesen Befehl ohne zusätzliche Berechtigungen ausführen. Andere Benutzer benötigen die ALTER ANY LOGIN-Berechtigung.  
  
```  
ALTER LOGIN Victoria WITH   
     PASSWORD = 'V1cteAmanti55imE'   
     OLD_PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
