---
title: DROP ROLE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP ROLE
- DROP_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting roles
- database roles [SQL Server], removing
- removing roles
- DROP ROLE statement
- roles [SQL Server], removing
- dropping roles
ms.assetid: 1f6f13ae-56a2-4ef1-93f5-8e6151b83e1d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d3ab74cca51d7fc52edb134d29887bb30abb4499
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="drop-role-transact-sql"></a>DROP ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Entfernt eine Rolle aus der Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
  
DROP ROLE [ IF EXISTS ] role_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP ROLE role_name  
```  
  
## <a name="arguments"></a>Argumente  
 *IF EXISTS*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Löscht die Rolle nur, wenn diese bereits vorhanden ist.  
  
 *role_name*  
 Gibt die Rolle an, die aus der Datenbank gelöscht werden soll.  
  
## <a name="remarks"></a>Remarks  
 Rollen, die sicherungsfähige Elemente besitzen, können nicht aus der Datenbank gelöscht werden. Wenn eine Datenbankrolle mit sicherungsfähigen Elementen gelöscht werden soll, müssen Sie zunächst den Besitz dieser sicherungsfähigen Elemente übertragen oder sie aus der Datenbank löschen. Rollen mit Mitgliedern können nicht aus der Datenbank gelöscht werden. Zum Löschen einer Rolle mit Mitgliedern müssen Sie zunächst die Mitglieder der Rolle entfernen.  
  
 Um Mitglieder aus einer Datenbankrolle zu entfernen, verwenden Sie [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md).  
  
 DROP ROLE kann nicht zum Löschen einer festen Datenbankrolle verwendet werden.  
  
 Informationen zur Rollenmitgliedschaft können in der sys.database_role_members-Katalogsicht angezeigt werden.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
 Verwenden Sie [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md), um eine Serverrolle zu entfernen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **ALTER ANY ROLE**-Berechtigung für die Datenbank, die **CONTROL**-Berechtigung für die Rolle oder die Mitgliedschaft in **db_securityadmin**.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Datenbankrolle `purchasing` aus der `AdventureWorks2012`-Datenbank entfernt.  
  
```  
DROP ROLE purchasing;  
GO  
```  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  


