---
title: Xp_logininfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_logininfo_TSQL
- xp_logininfo
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logininfo
ms.assetid: ee7162b5-e11f-4a0e-a09c-1878814dbbbd
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3eb400fed1fe0cbd25ef884dc56a89fe448717fe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xplogininfo-transact-sql"></a>xp_logininfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu Windows-Benutzern und Windows-Gruppen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
xp_logininfo [ [ @acctname = ] 'account_name' ]   
     [ , [ @option = ] 'all' | 'members' ]   
     [ , [ @privilege = ] variable_name OUTPUT]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@acctname =** ] **"***Account_name***"**  
 Der Name eines Windows-Benutzers oder einer Gruppe gewährt Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *account_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Wenn *account_name* nicht angegeben wird, werden alle Windows-Gruppen und Windows-Benutzer ausgegeben, denen explizit Anmeldeberechtigungen gewährt wurden. *account_name* muss vollqualifiziert sein. Beispiel: 'ADVWKS4\macraes' oder 'VORDEFINIERT\Administratoren'.  
  
 **'all'** | **'members'**  
 Gibt an, ob für das Konto die Informationen zu allen Berechtigungspfaden oder nur die Informationen zu den Mitgliedern der Windows-Gruppe ausgegeben werden sollen. **@option** ist **varchar(10)**, hat den Standardwert NULL. Sofern nicht **all** angegeben wurde, wird nur der erste Berechtigungspfad angezeigt.  
  
 [  **@privilege =** ] *Variable_name*  
 Ein Ausgabeparameter, der die Berechtigungsstufe des angegebenen Windows-Kontos zurückgibt. *variable_name* ist vom Datentyp **varchar(10)**. Der Standardwert ist "Not wanted". Die zurückgegebene Privilegstufe ist **user**, **admin**oder **null**.  
  
 OUTPUT  
 Wenn dieser Parameter angegeben wird, wird *variable_name* in den Ausgabeparameter platziert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Kontoname**|**sysname**|Der vollqualifizierte Windows-Kontoname.|  
|**type**|**char(8)-Wert zurück**|Der Windows-Kontotyp. Gültige Werte sind **user** oder **group**.|  
|**Berechtigung**|**char(9)**|Zugriffsprivileg für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gültige Werte sind **admin**, **user**oder **null**.|  
|**zugeordnete Anmeldename**|**sysname**|Für Benutzerkonten, die Benutzerprivileg **Anmeldename zugeordnet** der zugeordnete Anmeldename angezeigt, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versucht, bei der Anmeldung mit diesem Konto zugeordneten Regeln mit dem Domänennamen zu verwenden.|  
|**Berechtigungspfad**|**sysname**|Die Gruppenmitgliedschaft, die dem Konto den Zugriff ermöglicht hat.|  
  
## <a name="remarks"></a>Hinweise  
 Wird *account_name* angegeben, meldet **xp_logininfo** die höchste Privilegstufe des angegebenen Windows-Benutzers bzw. der angegebenen Windows-Gruppe. Wenn ein Windows-Benutzer Zugriff als Systemadministrator und als Domänenbenutzer hat, wird er nur als Systemadministrator gemeldet. Wenn der Benutzer Mitglied mehrerer Windows-Gruppen Privilegstufe ist, nur die Gruppe, die beim Zugriff erteilt hat [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gemeldet wird.  
  
 Wenn *Account_name* ist eine gültige Windows-Benutzer oder Gruppe, die nicht zugeordnet ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung ein leeres Resultset zurückgegeben. Wenn *account_name* nicht als gültiger Windows-Benutzer oder als gültige Windows-Gruppe identifiziert werden kann, wird ein Fehler gemeldet.  
  
 Werden *account_name* und **all** angegeben, werden sämtliche Berechtigungspfade für den Windows-Benutzer oder die Windows-Gruppe zurückgegeben. Wenn *Account_name* ist Mitglied mehrerer Gruppen, denen erteilt wurde Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mehrere Zeilen zurückgegeben. Die **Admin** Berechtigung Zeilen werden zurückgegeben, bevor Sie die **Benutzer** -Privileg innerhalb einer Privilegstufe werden die Zeilen in der Reihenfolge, in denen zurückgegeben das entsprechende [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen erstellt wurden.  
  
 Wenn *account_name* und **members** angegeben werden, wird eine Liste der Gruppenmitglieder der nächsten Ebene zurückgegeben. Ist *account_name* der Name einer lokalen Gruppe, kann die Liste lokale Benutzer, Domänenbenutzer und Gruppen enthalten. Wenn *account_name* ein Domänenkonto ist, besteht die Liste aus Domänenbenutzern. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss eine Verbindung mit dem Domänencontroller herstellen, um Informationen zu Gruppenmitgliedschaften abzurufen. Falls der Server keine Verbindung mit dem Domänencontroller herstellen kann, werden keine Informationen zurückgegeben.  
  
 **xp_logininfo** gibt nur Informationen von globalen Active Directory-Gruppen zurück und nicht für universelle Gruppen.  
  
## <a name="permissions"></a>Berechtigungen  
 Mitgliedschaft in der festen Serverrolle **sysadmin** bzw. Mitgliedschaft in der festen Datenbankrolle **public** in der **master** -Datenbank mit erteilter EXECUTE-Berechtigung erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zur Windows-Gruppe `BUILTIN\Administrators` angezeigt.  
  
```  
EXEC xp_logininfo 'BUILTIN\Administrators';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte allgemeine erweiterte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
