---
title: IS_ROLEMEMBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_ROLEMEMBER
- IS_ROLEMEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_ROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 73efa688-ae91-4014-98bc-1cabe47321f7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fd8574c27bea00127096dc1f0040c8c3f93e96cb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="isrolemember-transact-sql"></a>IS_ROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Gibt an, ob ein angegebener Datenbankprinzipal ein Element der angegebenen Datenbankrolle ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IS_ROLEMEMBER ( 'role' [ , 'database_principal' ] )  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Rolle* **"**  
 Der Name der Datenbankrolle, die überprüft wird. *Rolle* ist **Sysname**.  
  
 **"** *Database_principal* **"**  
 Der Name des Datenbankbenutzers, der Datenbankrolle oder der Anwendungsrolle, der/die überprüft werden soll. *Database_principal* ist **Sysname**, hat den Standardwert NULL. Wenn kein Wert angegeben wird, basiert das Ergebnis auf dem aktuellen Ausführungskontext. Wenn der Parameter das Wort NULL enthalten ist, wird NULL zurückgegeben.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
|Rückgabewert|Description|  
|------------------|-----------------|  
|0|*Database_principal* ist kein Mitglied der *Rolle*.|  
|1|*Database_principal* Mitglied *Rolle*.|  
|NULL|*Database_principal* oder *Rolle* ist ungültig, oder Sie haben nicht die Berechtigung zum Anzeigen der Rollenmitgliedschaft.|  
  
## <a name="remarks"></a>Hinweise  
 Mit IS_ROLEMEMBER legen Sie fest, ob der aktuelle Benutzer eine Aktion ausführen kann, für die die Berechtigungen der Datenbankrolle erforderlich sind.  
  
 Wenn *Database_principal* basiert auf einer Windows-Anmeldung, z. B. Contoso\Mary5, IS_ROLEMEMBER NULL zurück, es sei denn, die *Database_principal* erteilt oder verweigert direkten Zugriff auf wurde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Wenn das optionale *Database_principal* Parameter wird nicht bereitgestellt wird und die *Database_principal* basiert auf einer Windows-domänenanmeldung möglicherweise ein Mitglied einer Datenbankrolle über die Mitgliedschaft in einer Windows-Gruppe . Um derartige indirekte Mitgliedschaften aufzulösen, fordert IS_ROLEMEMBER Informationen zu Windows-Gruppenmitgliedschaften vom Domänencontroller an. Wenn nicht auf den Domänencontroller zugegriffen werden kann oder der Domänencontroller nicht reagiert, berücksichtigt IS_ROLEMEMBER beim Zurückgeben der Informationen zur Rollenmitgliedschaft nur den Benutzer und die lokalen Gruppen. Wenn der angegebene Benutzer nicht der aktuelle Benutzer ist, kann sich der durch IS_ROLEMEMBER zurückgegebene Wert vom letzten Datenupdate des Authentifikators (z. B. Active Directory) für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterscheiden.  
  
 Wenn das optionale *Database_principal* -Parameter bereitgestellt wird, muss der Datenbankprinzipal, die abgefragt wird in Sys. database_principals vorhanden sein oder IS_ROLEMEMBER den Wert NULL zurück. Dies bedeutet, dass die *Database_principal* ist in dieser Datenbank nicht gültig.  
  
 Wenn die *Database_principal* Parameter basierend auf einer domänenanmeldung oder anhand einer Windows-Gruppe und der Domänencontroller nicht zugegriffen werden kann, Aufrufe von IS_ROLEMEMBER fehl und können falsche oder unvollständige Daten zurückgeben.  
  
 Wenn der Domänencontroller nicht verfügbar ist, gibt der Aufruf von IS_ROLEMEMBER genaue Informationen zurück, wenn der Windows-Prinzipal lokal authentifiziert werden kann, z. B. ein lokales Windows-Konto oder eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung.  
  
 **IS_ROLEMEMBER** gibt immer 0 zurück, wenn eine Windows-Gruppe als Datenbankprinzipal-Argument verwendet wird, und diese Windows-Gruppe ein Mitglied einer anderen Windows-Gruppe ist, die wiederum Mitglied der angegebenen Datenbankrolle ist.  
  
 Die Benutzerkontensteuerung (UAC) in gefunden [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] und Windows Server 2008 möglicherweise auch andere Ergebnisse zurück. Dies hängt davon ab, ob der Benutzer auf den Server als Mitglied einer Windows-Gruppe oder als ein bestimmter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer zugreift.  
  
 Diese Funktion wertet die Rollenmitgliedschaft aus, nicht die zugrunde liegende Berechtigung. Z. B. die **Db_owner** feste Datenbankrolle besitzt die **CONTROL DATABASE** Berechtigung. Wenn der Benutzer hat die **CONTROL DATABASE** Berechtigung, ist aber kein Mitglied der Rolle, die diese Funktion meldet ordnungsgemäß, dass der Benutzer nicht Mitglied der **Db_owner** -Rolle ist, obwohl der Benutzer hat die gleiche Berechtigungen.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
 Um zu bestimmen, ob der aktuelle Benutzer ein Mitglied der angegebenen Windows-Gruppe oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbankrolle verwenden [IS_MEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-member-transact-sql.md). Um zu bestimmen, ob eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung ist Mitglied einer Serverrolle, verwenden Sie [IS_SRVROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DEFINITION-Berechtigung für die Datenbankrolle.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt an, ob der aktuelle Benutzer Mitglied der festen Datenbankrolle `db_datareader` ist.  
  
```  
IF IS_ROLEMEMBER ('db_datareader') = 1  
   print 'Current user is a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') = 0  
   print 'Current user is NOT a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') IS NULL  
   print 'ERROR: The database role specified is not valid.';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie die Rolle "" &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [Erstellen Sie SERVER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [ALTER SERVER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [IS_MEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
