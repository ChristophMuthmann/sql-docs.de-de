---
title: Sp_addlogin (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addlogin
- sp_addlogin_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 09a8425f9c3d773af00a0418ff4430839c221d87
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spaddlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen, der es einem Benutzer ermöglicht, eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung herzustellen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) stattdessen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addlogin [ @loginame = ] 'login'   
    [ , [ @passwd = ] 'password' ]   
    [ , [ @defdb = ] 'database' ]   
    [ , [ @deflanguage = ] 'language' ]   
    [ , [ @sid = ] sid ]   
    [ , [ @encryptopt = ] 'encryption_option' ]   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @loginame=] '*Anmeldung*"  
 Der Name der Anmeldung. *login* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
 [ @passwd=] '*Kennwort*"  
 Ist das Kennwort der Anmeldung. *Kennwort* ist **Sysname**, hat den Standardwert NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb=] '*Datenbank*"  
 Ist die Standarddatenbank des Anmeldenamens (die Datenbank, mit der der Anmeldename nach dem Anmelden zuerst verbunden wird). *Datenbank* ist **Sysname**, hat den Standardwert **master**.  
  
 [ @deflanguage=] '*Sprache*"  
 Die Standardsprache der Anmeldung. *language* ist vom Datentyp **sysname**und hat den Standardwert NULL. Wenn *Sprache* nicht angegeben ist, der Standardwert *Sprache* für den neuen Anmeldenamen auf die aktuelle Standardsprache des Servers festgelegt ist.  
  
 [ @sid=] '*Sid*"  
 Die Sicherheits-ID (SID). *SID* ist **varbinary(16)**, hat den Standardwert NULL. Wenn *Sid* NULL ist, der vom System generiert einer SID für den neuen Anmeldenamen. Trotz der Verwendung von einem **Varbinary** Datentyp, andere Werte als NULL muss genau 16 Byte lang sein und darf nicht bereits vorhanden sein. Angeben von *Sid* ist nützlich, z. B. Wenn Sie Skripts oder Verschieben von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldungen von einem Server in eine andere und Sie möchten die Anmeldungen auf verschiedenen Servern die gleiche SID haben.  
  
 [ @encryptopt=] '*Encryption_option*"  
 Gibt an, ob das Kennwort als Klartext oder als Hash des Klartextkennworts weitergegeben wird. Dabei ist zu beachten, dass keine Verschlüsselung stattfindet. Der Begriff "verschlüsseln" wird in diesem Zusammenhang aus Gründen der Abwärtskompatibilität verwendet. Wenn ein Klartextkennwort übergeben wird, geschieht dies in Form eines Hashs. Der Hash wird gespeichert. *Encryption_option* ist **varchar(20)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|NULL|Das Kennwort wird als Klartext übergeben. Dies ist die Standardeinstellung.|  
|**skip_encryption**|Es wurde bereits ein Hashwert aus dem Kennwort erstellt. [!INCLUDE[ssDE](../../includes/ssde-md.md)] sollte den Wert ohne erneutes Hashing speichern.|  
|**skip_encryption_old**|Es wurde ein Hashwert des bereitgestellten Kennworts von einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt. [!INCLUDE[ssDE](../../includes/ssde-md.md)] sollte den Wert ohne erneutes Hashing speichern. Diese Option dient lediglich Upgradezwecken.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen können zwischen 1 und 128 Zeichen (einschließlich Buchstaben, Sonderzeichen und Ziffern) enthalten. Anmeldungen können einen umgekehrten Schrägstrich enthalten (\\); werden keine reservierten Anmeldenamen, z. B. sa oder Public, bereits vorhanden ist; oder nicht NULL oder eine leere Zeichenfolge (`''`).  
  
 Wenn der Name einer Standarddatenbank angegeben wird, ist die Verbindung mit dieser Datenbank ohne das Ausführen der USE-Anweisung möglich. Sie können nicht jedoch die Standarddatenbank verwenden, bis Sie Zugriff auf diese Datenbank vom Datenbankbesitzer erteilt werden (mit [Sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) oder [Sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) oder [Sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md).  
  
 Die SID ist ein GUID, die den Anmeldenamen auf dem Server eindeutig identifiziert.  
  
 Wird die Standardsprache des Servers geändert, ändert sich dadurch nicht die Standardsprache der bestehenden Anmeldenamen. Um die Standardsprache des Servers zu ändern, verwenden Sie [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Mit **Skip_encryption** zum Unterdrücken kennworthashings ist dann nützlich, wenn das Kennwort bereits einen Hashwert darstellt, wenn der Anmeldename hinzugefügt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn das Kennwort von einer früheren Version von ein Hash erzeugt wurde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verwenden Sie **Skip_encryption_old**.  
  
 sp_addlogin kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
 In der folgenden Tabelle werden verschiedene gespeicherte Prozeduren angezeigt, die mit sp_addlogin verwendet werden.  
  
|Gespeicherte Prozedur|Description|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|Fügt einen Windows-Benutzer oder eine Windows-Gruppe hinzu.|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|Ändert das Kennwort eines Benutzers.|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|Ändert die Standarddatenbank eines Benutzers.|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|Ändert die Standardsprache eines Benutzers.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY LOGIN-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-sql-server-login"></a>A. Erstellen einer SQL Server-Anmeldung  
 Im folgenden Beispiel wird ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename für den Benutzer `Victoria` mit dem Kennwort `B1r12-36` erstellt, ohne dass eine Standarddatenbank angegeben wird.  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>B. Erstellen einer SQL Server-Anmeldung mit einer Standarddatenbank  
 Im folgenden Beispiel wird ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename für den Benutzer `Albert` mit dem Kennwort `B5432-3M6` erstellt; dabei wird `corporate` als Standarddatenbank angegeben.  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>C. Erstellen einer SQL Server-Anmeldung mit einer anderen Standardsprache  
 Im folgenden Beispiel wird ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename für den Benutzer `TzTodorov` mit dem Kennwort `709hLKH7chjfwv` erstellt; dabei werden `AdventureWorks2012` als Standarddatenbank und `Bulgarian` als Standardsprache angegeben.  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>D. Erstellen einer SQL Server-Anmeldung mit einer bestimmten SID  
 Im folgenden Beispiel wird ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename für den Benutzer `Michael` mit dem Kennwort `B548bmM%f6` erstellt; dabei werden `AdventureWorks2012` als Standarddatenbank, `us_english` als Standardsprache und `0x0123456789ABCDEF0123456789ABCDEF` als SID angegeben.  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [Sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Xp_logininfo &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
