---
title: Sp_change_users_login (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/13/2016
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
- sp_change_users_login
- sp_change_users_login_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_change_users_login
ms.assetid: 1554b39f-274b-4ef8-898e-9e246b474333
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 207272f7644ab39055b7c6bb330faf6053353601
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spchangeuserslogin-transact-sql"></a>sp_change_users_login (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Ordnet einen vorhandenen Datenbankbenutzer einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen zu. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [ALTER USER](../../t-sql/statements/alter-user-transact-sql.md) stattdessen.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_change_users_login [ @Action = ] 'action'   
    [ , [ @UserNamePattern = ] 'user' ]   
    [ , [ @LoginName = ] 'login' ]   
    [ , [ @Password = ] 'password' ]  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @Action=] '*Aktion*"  
 Beschreibt die von der Prozedur durchzuführende Aktion. *Aktion* ist **varchar(10)**. *Aktion* kann einen der folgenden Werte aufweisen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Auto_fix**|Verknüpft einen Benutzereintrag in der sys.database_principals-Systemkatalogsicht in der aktuellen Datenbank mit einem gleichlautenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen. Ist kein gleichlautender Anmeldename vorhanden, wird er erstellt. Überprüfen Sie das Ergebnis der **Auto_Fix** Anweisung, um sicherzustellen, dass tatsächlich der richtige Link erstellt wurde. Vermeiden Sie die Verwendung **Auto_Fix** in sicherheitskritischen Situationen.<br /><br /> Bei Verwendung von **Auto_Fix**, müssen Sie angeben, *Benutzer* und *Kennwort* Wenn der Anmeldename nicht bereits vorhanden ist, andernfalls müssen Sie angeben *Benutzer*jedoch *Kennwort* werden ignoriert. *Anmeldung* muss NULL sein. *Benutzer* muss ein gültiger Benutzer in der aktuellen Datenbank sein. Dem Anmeldenamen kann kein anderer Benutzer zugeordnet werden.|  
|**Bericht**|Listet die Benutzer und entsprechenden Sicherheits-IDs (SIDs) in der aktuellen Datenbank auf, die mit keinem Anmeldenamen verknüpft sind. *Benutzer*, *Anmeldung*, und *Kennwort* muss NULL oder nicht angegeben.<br /><br /> Um die Berichtsoption durch eine Abfrage mit Bezug auf die Systemtabellen zu ersetzen, vergleichen Sie die Einträge in **server_prinicpals** mit den Einträgen in **Sys. database_principals**.|  
|**Update_One**|Verknüpft den angegebenen *Benutzer* in der aktuellen Datenbank zu einem vorhandenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Anmeldung*. *Benutzer* und *Anmeldung* muss angegeben werden. *Kennwort* muss NULL oder nicht angegeben.|  
  
 [ @UserNamePattern=] '*Benutzer*"  
 Der Name eines Benutzers in der aktuellen Datenbank. *Benutzer* ist **Sysname**, hat den Standardwert NULL.  
  
 [ @LoginName=] '*Anmeldung*"  
 Der Name einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung. *login* ist vom Datentyp **sysname**und hat den Standardwert NULL.  
  
 [ @Password=] '*Kennwort*"  
 Zugewiesene Kennwort in ein neues [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung durch die Angabe erstellte **Auto_Fix**. Wenn kein entsprechender Anmeldename vorhanden ist, die Benutzer und Anmeldenamen zugeordnet sind und *Kennwort* wird ignoriert. Wenn kein entsprechender Anmeldename nicht existiert, erstellt Sp_change_users_login einen neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen und weist ihm *Kennwort* als Kennwort für den neuen Anmeldenamen. *Kennwort* ist **Sysname**, und darf nicht NULL sein.  
  
> **WICHTIG!** Verwenden Sie immer eine [sicheres Kennwort!](../../relational-databases/security/strong-passwords.md)
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|UserName|**sysname**|Datenbank-Benutzername.|  
|UserSID|**varbinary (85)**|Sicherheits-ID des Benutzers.|  
  
## <a name="remarks"></a>Hinweise  
 Mithilfe von sp_change_users_login kann ein Datenbankbenutzer in der aktuellen Datenbank mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen verknüpft werden. Wenn sich der Anmeldename für einen Benutzer geändert hat, verknüpfen Sie den Benutzer mithilfe von sp_change_users_login mit dem neuen Anmeldenamen, ohne die Benutzerberechtigungen zu verlieren. Die neue *Anmeldung* darf nicht sa sein, und die *Benutzer*darf nicht Dbo, Guest oder ein INFORMATION_SCHEMA-Benutzer.  
  
 sp_change_users_login kann nicht zum Erstellen einer Zuordnung zwischen Datenbankbenutzern und Prinzipalen, Zertifikaten oder asymmetrischen Schlüsseln auf Windows-Ebene verwendet werden.  
  
 sp_change_users_login kann nicht mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung, die anhand eines Windows-Prinzipals erstellt wurde, oder mit einer vom Benutzer (mithilfe von CREATE USER WITHOUT LOGIN) erstellten Anmeldung verwendet werden.  
  
 sp_change_users_login kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Datenbankrolle "db_owner". Nur Mitglieder der festen Serverrolle Sysadmin können angeben, die **Auto_Fix** Option.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-showing-a-report-of-the-current-user-to-login-mappings"></a>A. Anzeigen eines Berichts der aktuellen Zuordnungen zwischen Benutzern und Anmeldenamen  
 Im folgenden Beispiel wird ein Bericht über die Benutzer in der aktuellen Datenbank und ihre Sicherheits-IDs erstellt.  
  
```  
EXEC sp_change_users_login 'Report';  
```  
  
### <a name="b-mapping-a-database-user-to-a-new-sql-server-login"></a>B. Zuordnen eines Datenbankbenutzers zu einer neuen SQL Server-Anmeldung  
 Im folgenden Beispiel wird ein Datenbankbenutzer einem neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen zugeordnet. Datenbankbenutzer `MB-Sales`, der zunächst einem anderen Anmeldenamen zugeordnet ist, wird dem Anmeldenamen `MaryB` zugeordnet.  
  
```  
--Create the new login.  
CREATE LOGIN MaryB WITH PASSWORD = '982734snfdHHkjj3';  
GO  
--Map database user MB-Sales to login MaryB.  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Update_One', 'MB-Sales', 'MaryB';  
GO  
```  
  
### <a name="c-automatically-mapping-a-user-to-a-login-creating-a-new-login-if-it-is-required"></a>C. Automatisches Zuordnen eines Benutzers zu einer Anmeldung und ggf. Erstellen einer neuen Anmeldung  
 Im folgenden Beispiel wird veranschaulicht, wie mithilfe von `Auto_Fix` eine Zuordnung zwischen einem vorhandenen Benutzer und einem gleichlautenden Anmeldenamen erstellt wird oder wie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename `Mary` mit dem Kennwort `B3r12-3x$098f6` erstellt wird, wenn der Anmeldename `Mary` nicht vorhanden ist.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Auto_Fix', 'Mary', NULL, 'B3r12-3x$098f6';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [Sp_helplogins &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
