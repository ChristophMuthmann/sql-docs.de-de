---
title: IS_SRVROLEMEMBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_SRVROLEMEMBER_TSQL
- IS_SRVROLEMEMBER
dev_langs: TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_SRVROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 3241a44a-6958-415b-b8b7-2a1207c36ab3
caps.latest.revision: "65"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 342eadd8e537611cc292c95ebfa41b98c222c920
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="issrvrolemember-transact-sql"></a>IS_SRVROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt an, ob eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung Element der angegebenen Serverrolle ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IS_SRVROLEMEMBER ( 'role' [ , 'login' ] )  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Rolle* **"**  
 Der Name der zu überprüfenden Serverrolle. *Rolle* ist **Sysname**.  
  
 Gültige Werte für *Rolle* sind benutzerdefinierte Serverrollen, sowie die folgenden festen Serverrollen:  
  
|||  
|-|-|  
|sysadmin|serveradmin|  
|dbcreator|setupadmin|  
|bulkadmin|securityadmin|  
|diskadmin|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> öffentlich|  
|processadmin||  
  
 **"** *Anmeldung* **"**  
 Der Name des der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung überprüfen. *login* ist vom Datentyp **sysname**und hat den Standardwert NULL. Wenn kein Wert angegeben wird, basiert das Ergebnis auf den aktuellen Ausführungskontext liefert. Wenn der Parameter das Wort NULL enthalten ist, wird NULL zurückgegeben.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
|Rückgabewert|Description|  
|------------------|-----------------|  
|0|*Anmeldung* ist kein Mitglied der *Rolle*.<br /><br /> In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], gibt diese Anweisung immer 0 zurück.|  
|1|*Anmeldung* Mitglied *Rolle*.|  
|NULL|*Rolle* oder *Anmeldung* ist ungültig, oder Sie haben nicht die Berechtigung zum Anzeigen der Rollenmitgliedschaft.|  
  
## <a name="remarks"></a>Hinweise  
 UseIS_SRVROLEMEMBER zu bestimmen, ob der aktuelle Benutzer eine Aktion, die Berechtigungen der Serverrolle erforderlich sind.  
  
 Wenn für eine Windows-Anmeldung, z. B. Contoso\Mary5, angegeben wird *Anmeldung*, **IS_SRVROLEMEMBER** gibt **NULL**, es sei denn, die Anmeldung gewährt oder verweigert direkten Zugriff auf wurde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Wenn das optionale *Anmeldung* Parameter wird nicht bereitgestellt wird und *Anmeldung* eine Windows-domänenanmeldung ist möglicherweise ein Mitglied einer festen Serverrolle über die Mitgliedschaft in einer Windows-Gruppe. Um derartige indirekte Mitgliedschaften aufzulösen, fordert IS_SRVROLEMEMBER Informationen zu Windows-Gruppenmitgliedschaften vom Domänencontroller an. Wenn der Domänencontroller nicht zugegriffen werden kann oder nicht reagiert, **IS_SRVROLEMEMBER** gibt Informationen zur Rollenmitgliedschaft nach Buchhaltung für den Benutzer und nur die lokalen Gruppen zurück. Wenn der angegebene Benutzer nicht der aktuelle Benutzer ist, kann sich der durch IS_SRVROLEMEMBER zurückgegebene Wert vom letzten Datenupdate des Authentifikators (z. B. Active Directory) für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterscheiden.  
  
 Wenn der optionale Anmeldeparameter bereitgestellt wird, muss die Windows-Anmeldung, die abgefragt wird in Sys. server_principals vorhanden sein, oder IS_SRVROLEMEMBER gibt NULL zurück. Dies gibt an, dass die Anmeldung ungültig ist.  
  
 Wenn der Anmeldeparameter eine Domänenanmeldung ist oder auf einer Windows-Gruppe basiert und auf den Domänencontroller nicht zugegriffen werden kann, schlagen Aufrufe von IS_SRVROLEMEMBER fehl und können falsche oder unvollständige Daten zurückgeben.  
  
 Wenn der Domänencontroller nicht verfügbar ist, gibt der Aufruf von IS_SRVROLEMEMBER genaue Informationen zurück, wenn der Windows-Prinzipal lokal authentifiziert werden kann, z. B. ein lokales Windows-Konto oder eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung.  
  
 **IS_SRVROLEMEMBER** gibt immer 0 zurück, wenn eine Windows-Gruppe als anmeldeargument verwendet wird, und diese Windows-Gruppe ein Mitglied einer anderen Windows-Gruppe ist, die wiederum Mitglied der angegebenen Serverrolle ist.  
  
 Die Einstellung der Benutzerkontensteuerung (UAC) kann auch dazu führen, dass die zurückgegebenen Ergebnisse aus verschiedenen. Dies hängt davon ab, ob der Benutzer auf den Server als Mitglied einer Windows-Gruppe oder als ein bestimmter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer zugreift.  
  
 Diese Funktion wertet die Rollenmitgliedschaft aus, nicht die zugrunde liegende Berechtigung. Z. B. die **Sysadmin** feste Serverrolle besitzt die **CONTROL SERVER** Berechtigung. Wenn der Benutzer hat die **CONTROL SERVER** Berechtigung, ist aber kein Mitglied der Rolle, die diese Funktion meldet ordnungsgemäß, dass der Benutzer nicht Mitglied der **Sysadmin** -Rolle ist, obwohl der Benutzer hat die gleiche Berechtigungen.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
 Um zu bestimmen, ob der aktuelle Benutzer ein Mitglied der angegebenen Windows-Gruppe oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbankrolle verwenden [IS_MEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-member-transact-sql.md). Um zu bestimmen, ob eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung ist Mitglied einer Datenbankrolle, verwenden Sie [IS_ROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-rolemember-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DEFINITION-Berechtigung für die Serverrolle.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt an, ob die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung für den aktuellen Benutzer Mitglied der festen Serverrolle `sysadmin` ist.  
  
```  
IF IS_SRVROLEMEMBER ('sysadmin') = 1  
   print 'Current user''s login is a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') = 0  
   print 'Current user''s login is NOT a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') IS NULL  
   print 'ERROR: The server role specified is not valid.';  
```  
  
 Das folgende Beispiel gibt an, ob die domänenanmeldung Pat Mitglied ist die **Diskadmin** festen Serverrolle "".  
  
```  
SELECT IS_SRVROLEMEMBER('diskadmin', 'Contoso\Pat');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [IS_MEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
