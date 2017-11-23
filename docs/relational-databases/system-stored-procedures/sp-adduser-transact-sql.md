---
title: Sp_adduser (Transact-SQL) | Microsoft Docs
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
- sp_adduser
- sp_adduser_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_adduser
ms.assetid: 61a40eb4-573f-460c-9164-bd1bbfaf8b25
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 218d0e89f985b8816a5466ad3f23c7b1bb6166bb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spadduser-transact-sql"></a>sp_adduser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt der aktuellen Datenbank einen neuen Benutzer hinzu.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) stattdessen.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_adduser [ @loginame = ] 'login'   
    [ , [ @name_in_db = ] 'user' ]   
    [ , [ @grpname = ] 'role' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@loginame =** ] **"***Anmeldung***"**  
 Der Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung oder Windows-Anmeldung. *login* ist vom Datentyp **sysname**und hat keinen Standardwert. *Anmeldung* muss einem vorhandenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder Windows-Anmeldung.  
  
 [  **@name_in_db =** ] **"***Benutzer***"**  
 Der Name für den neuen Datenbankbenutzer. *Benutzer* ist ein **Sysname**, hat den Standardwert NULL. Wenn *Benutzer* nicht angegeben ist, wird standardmäßig der Name des neuen Datenbankbenutzers auf die *Anmeldung* Name. Angeben von *Benutzer* der neue Benutzer erhält einen Namen in der Datenbank, die sich von den Anmeldenamen auf Serverebene.  
  
 [  **@grpname =** ] **"***Rolle***"**  
 Die Datenbankrolle, deren Mitglied der neue Benutzer wird. *role* ist vom Datentyp **sysname**und hat den Standardwert NULL. *Rolle* muss eine gültige Datenbankrolle in der aktuellen Datenbank sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_adduser** erstellt auch ein Schema mit dem Namen des Benutzers ab.  
  
 Definieren Sie nach dem Hinzufügen eines Benutzers mit den Anweisungen GRANT, DENY und REVOKE die Berechtigungen für die Aktivitäten, die der Benutzer ausführen darf.  
  
 Verwendung **Sys. server_principals** um eine Liste gültiger Anmeldenamen anzuzeigen.  
  
 Verwendung **Sp_helprole** um eine Liste der gültigen Rollennamen anzuzeigen. Bei Angabe einer Rolle erhält der Benutzer automatisch die für diese Rolle definierten Berechtigungen. Wenn eine Rolle nicht angegeben wird, erhält der Benutzer die Berechtigungen auf den Standardwert **öffentlichen** Rolle. Zum Hinzufügen eines Benutzers zu einer Rolle, die einen Wert für die *Benutzername* muss angegeben werden. (*Benutzername* identisch sein *Anmelde-ID*.)  
  
 Benutzer **Gast** bereits in jeder Datenbank vorhanden ist. Hinzufügen des Benutzers **Gast** dieser Benutzer wird aktiviert werden, falls sie zuvor deaktiviert war. Standardmäßig Benutzer **Gast** ist in neuen Datenbanken deaktiviert.  
  
 **Sp_adduser** kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
 Sie können nicht hinzugefügt werden eine **Gast** Benutzer da eine **Gast** Benutzer bereits in jeder Datenbank vorhanden ist. So aktivieren Sie die **Gast** Benutzer, Grant **Gast** CONNECT-Berechtigung wie folgt:  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert den Besitz der Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-adding-a-database-user"></a>A. Hinzufügen eines Datenbankbenutzers  
 Im folgenden Beispiel wird der Datenbankbenutzer `Vidur` der vorhandenen Rolle `Recruiting` in der aktuellen Datenbank hinzugefügt, wobei der vorhandene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename `Vidur` verwendet wird.  
  
```  
EXEC sp_adduser 'Vidur', 'Vidur', 'Recruiting';  
```  
  
### <a name="b-adding-a-database-user-with-the-same-login-id"></a>B. Hinzufügen eines Datenbankbenutzers mit der gleichen Anmelde-ID  
 Im folgenden Beispiel wird der Benutzer `Arvind` der aktuellen Datenbank für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `Arvind` hinzugefügt. Dieser Benutzer gehört, auf den Standardwert **öffentlichen** Rolle.  
  
```  
EXEC sp_adduser 'Arvind';  
```  
  
### <a name="c-adding-a-database-user-with-a-different-name-than-its-server-level-login"></a>C. Hinzufügen eines Datenbankbenutzers mit einem anderen Namen als der Anmeldename auf Serverebene  
 Im folgenden Beispiel wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename `BjornR` der aktuellen Datenbank hinzugefügt, die den Benutzernamen `Bjorn` besitzt. Der Datenbankbenutzer `Bjorn` wird der `Production`-Datenbankrolle hinzugefügt.  
  
```  
EXEC sp_adduser 'BjornR', 'Bjorn', 'Production';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
