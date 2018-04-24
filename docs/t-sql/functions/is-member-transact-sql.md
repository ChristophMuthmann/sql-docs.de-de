---
title: IS_MEMBER (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ebb422957d8b984a98fff93541f1f884e5d65536
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
 **'** *group* **'**  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Der Name der Windows-Gruppe, die überprüft wird. Dieser muss das Format *Domäne*\\*Gruppe* aufweisen. *group* ist vom Datentyp **sysname**.  
  
 **'** *role* **'**  
 Der Name der zu überprüfenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rolle. *role* ist vom Datentyp **sysname** und kann feste Datenbankrollen oder benutzerdefinierte Rollen, nicht jedoch Serverrollen einschließen.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Remarks  
 IS_MEMBER gibt folgende Werte zurück.  
  
|Rückgabewert|Description|  
|------------------|-----------------|  
|0|Der aktuelle Benutzer ist kein Mitglied von *group* oder *role*.|  
|1|Der aktuelle Benutzer ist ein Mitglied von *group* oder *role*.|  
|NULL|Entweder *group* oder *role* ist ungültig. Bei Abfrage durch eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung oder eine Anmeldung, die eine Anwendungsrolle verwendet, wird NULL für eine Windows-Gruppe zurückgegeben.|  
  
 IS_MEMBER bestimmt die Windows-Gruppenmitgliedschaft durch Analysieren eines Zugriffstokens, das von Windows erstellt wird. Das Zugriffstoken spiegelt keine Änderungen an der Gruppenmitgliedschaft wider, die vorgenommen werden, nachdem ein Benutzer eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hergestellt hat. Die Windows-Gruppenmitgliedschaft kann nicht von einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung oder einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anwendungsrolle abgefragt werden.  
  
 Um einer Datenbankrolle Elemente hinzuzufügen bzw. um diese aus ihr zu entfernen, verwenden Sie [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md). Um einer Serverrolle Elemente hinzuzufügen bzw. um diese aus ihr zu entfernen, verwenden Sie [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Diese Funktion wertet die Rollenmitgliedschaft aus, nicht die zugrunde liegende Berechtigung. Die feste Datenbankrolle **db_owner** besitzt z.B. die Berechtigung **CONTROL DATABASE**. Wenn der Benutzer die **CONTROL DATABASE**-Berechtigung besitzt, aber nicht Mitglied der Rolle ist, meldet diese Funktion ordnungsgemäß, dass der Benutzer nicht Mitglied der **db_owner**-Rolle ist, obwohl er dieselben Berechtigungen besitzt.  
  
 Mitglieder der festen Serverrolle **sysadmin** treten jeder Datenbank als **dbo**-Benutzer bei. Wenn die Berechtigungen der Mitglieder der festen **sysadmin**-Serverrolle überprüft werden, werden auch die Berechtigungen für **dbo**, aber nicht die ursprünglichen Anmeldeinformationen, überprüft. Da **dbo** nicht zu einer Datenbankrolle hinzugefügt werden kann und in Windows-Gruppen nicht vorhanden ist, gibt **dbo** immer 0 (null) (oder NULL, wenn die Rolle nicht vorhanden ist) zurück.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
 Um zu bestimmen, ob ein anderer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename Mitglied einer Datenbankrolle ist, verwenden Sie [IS_ROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md). Zum Bestimmen, ob ein anderer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename ein Mitglied einer Datenbankrolle ist, verwenden Sie [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
