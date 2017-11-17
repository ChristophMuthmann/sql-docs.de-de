---
title: IS_MEMBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
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
- IS_MEMBER
- IS_MEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], members
- current member status
- roles [SQL Server], members
- testing member status
- members [SQL Server]
- checking member status
- IS_MEMBER function
- verifying member status
- groups [SQL Server], members
- members [SQL Server], verifying
ms.assetid: 77cb68a0-19b7-4fe1-ab17-e5587699631b
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 472d8f1cc258fdc57ef454fbb35f51e3f83b288d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="ismember-transact-sql"></a>IS_MEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Zeigt an, ob der aktuelle Benutzer ein Mitglied der angegebenen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Gruppe oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankrolle ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Gruppe* **"**  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Ist der Name der Windows-Gruppe, die überprüft wird. muss im Format *Domäne*\\*Gruppe*. *Gruppe* ist **Sysname**.  
  
 **"** *Rolle* **"**  
 Der Name des der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Rolle, die überprüft wird. *Rolle* ist **Sysname** und feste Datenbankrollen oder benutzerdefinierte Rollen, jedoch nicht von Server-Rollen enthalten kann.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 IS_MEMBER gibt folgende Werte zurück.  
  
|Rückgabewert|Description|  
|------------------|-----------------|  
|0|Aktuelle Benutzer ist kein Mitglied der *Gruppe* oder *Rolle*.|  
|1|Aktuelle Benutzer ist Mitglied der *Gruppe* oder *Rolle*.|  
|NULL|Entweder *Gruppe* oder *Rolle* ist ungültig. Bei Abfrage durch eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung oder eine Anmeldung, die eine Anwendungsrolle verwendet, wird NULL für eine Windows-Gruppe zurückgegeben.|  
  
 IS_MEMBER bestimmt die Windows-Gruppenmitgliedschaft durch Analysieren eines Zugriffstokens, das von Windows erstellt wird. Das Zugriffstoken spiegelt keine Änderungen an der Gruppenmitgliedschaft wider, die vorgenommen werden, nachdem ein Benutzer eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hergestellt hat. Windows-Gruppenmitgliedschaft kann nicht abgefragt werden, indem eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung oder eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anwendungsrolle.  
  
 Verwenden Sie zum Hinzufügen und Entfernen von Mitgliedern aus einer Datenbankrolle, [ALTER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-role-transact-sql.md). Verwenden Sie zum Hinzufügen und Entfernen von Mitgliedern aus einer Serverrolle, [ALTER SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Diese Funktion wertet die Rollenmitgliedschaft aus, nicht die zugrunde liegende Berechtigung. Z. B. die **Db_owner** feste Datenbankrolle besitzt die **CONTROL DATABASE** Berechtigung. Wenn der Benutzer hat die **CONTROL DATABASE** Berechtigung, ist aber kein Mitglied der Rolle, die diese Funktion meldet ordnungsgemäß, dass der Benutzer nicht Mitglied der **Db_owner** -Rolle ist, obwohl der Benutzer hat die gleiche Berechtigungen.  
  
 Mitglieder der **Sysadmin** festen Serverrolle "" Geben Sie jede Datenbank als die **Dbo** Benutzer. Berechtigungen für Mitglied überprüft die **Sysadmin** feste Serverrolle, überprüft die Berechtigungen für **Dbo**, nicht den ursprünglichen Anmeldenamen. Da **Dbo** kann eine Datenbankrolle hinzugefügt werden und ist nicht vorhanden, in der Windows-Gruppen **Dbo** gibt immer 0 (oder NULL, wenn die Rolle nicht vorhanden ist).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
 Um festzustellen, ob eine andere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung ist Mitglied einer Datenbankrolle, verwenden Sie [IS_ROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-rolemember-transact-sql.md). Um zu bestimmen, ob eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung ist Mitglied einer Serverrolle, verwenden Sie [IS_SRVROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird überprüft, ob der aktuelle Benutzer ein Mitglied einer Datenbankrolle oder einer Windows-Domänengruppe ist.  
  
```  
-- Test membership in db_owner and print appropriate message.  
IF IS_MEMBER ('db_owner') = 1  
   PRINT 'Current user is a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') = 0  
   PRINT 'Current user is NOT a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') IS NULL  
   PRINT 'ERROR: Invalid group / role specified';  
GO  
  
-- Execute SELECT if user is a member of ADVWORKS\Shipping.  
IF IS_MEMBER ('ADVWORKS\Shipping') = 1  
   SELECT 'User ' + USER + ' is a member of ADVWORKS\Shipping.';   
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [IS_SRVROLEMEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

