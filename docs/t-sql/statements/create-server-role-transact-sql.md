---
title: Erstellen Sie die SERVERROLLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SERVER_ROLE_TSQL
- CREATE SERVER ROLE
- SERVER ROLE
- CREATE_SERVER_ROLE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- SERVER ROLE
- SERVER ROLE, CREATE
- CREATE SERVER ROLE statement
- ROLE
- user-defined server roles [SQL Server]
- roles, server
ms.assetid: 30c92f80-f7f6-4a84-ae89-16e69add0de6
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3ffe7b33392bcdab6efb3ec9c172f9839015b88b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="create-server-role-transact-sql"></a>CREATE SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

  Erstellt eine neue benutzerdefinierte Serverrolle.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE SERVER ROLE role_name [ AUTHORIZATION server_principal ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Rollenname*  
 Der Name der zu erstellenden Serverrolle.  
  
 Autorisierung *Server_principal*  
 Der Anmeldename, der die neue Serverrolle besitzt. Wenn kein Anmeldename angegeben wird, besitzt der Anmeldename, der CREATE SERVER ROLE ausführt, diese Serverrolle.  
  
## <a name="remarks"></a>Hinweise  
 Serverrollen sind sicherungsfähige Elemente auf Serverebene. Nachdem Sie eine Serverrolle erstellt haben, konfigurieren Sie die Berechtigungen der Rolle auf Serverebene mithilfe von GRANT, DENY und REVOKE. Verwenden Sie zum Hinzufügen von Anmeldungen, oder Entfernen von Anmeldenamen aus einer Serverrolle, [ALTER SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md). Verwenden Sie zum Löschen einer Serverrolle [DROP SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/drop-server-role-transact-sql.md). Weitere Informationen finden Sie unter [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 Sie können die Serverrollen anzeigen, durch Abfragen der [server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) und [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) Katalogsichten.  
  
 Serverrollen kann keine Berechtigung für sicherungsfähige Elemente auf Datenbankebene gewährt werden. Informationen zum Erstellen von Datenbankrollen finden Sie unter [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md).  
  
 Informationen zum Entwerfen eines Berechtigungssystems finden Sie unter [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE SERVER ROLE-Berechtigung oder die Mitgliedschaft in der festen sysadmin-Serverrolle.  
  
 Erfordert für Anmeldenamen außerdem IMPERSONATE für den *server_principal* , die ALTER-Berechtigung für Serverrollen, die als *server_principal*verwendet werden, oder die Mitgliedschaft in einer Windows-Gruppe, die als server_principal verwendet wird.  
  
 Dies wird der Audit Server Principal Management-Ereignis ausgelöst, mit dem Objekttyp Serverrolle festgelegt und das Ereignis des Typs hinzufügen.  
  
 Wenn Sie die AUTHORIZATION-Option verwenden, um den Besitz für Serverrollen zuzuweisen, sind außerdem folgende Berechtigungen erforderlich:  
  
-   Um einer Serverrolle einen anderen Anmeldenamen als Besitzer zuzuweisen, ist die IMPERSONATE-Berechtigung für diesen Anmeldenamen erforderlich.  
  
-   Um einer Serverrolle eine andere Serverrolle als Besitzer zuzuweisen, ist die Mitgliedschaft in der Empfängerserverrolle oder die ALTER-Berechtigung für diese Serverrolle erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-server-role-that-is-owned-by-a-login"></a>A. Erstellen einer Serverrolle, deren Besitzer ein Anmeldename ist  
 Im folgenden Beispiel wird die `buyers`-Serverrolle erstellt, deren Besitzer der Anmeldename `BenMiller` ist.  
  
```  
USE master;  
CREATE SERVER ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-server-role-that-is-owned-by-a-fixed-server-role"></a>B. Erstellen einer Serverrolle, deren Besitzer eine feste Serverrolle ist  
 Im folgenden Beispiel wird die `auditors`-Serverrolle erstellt, deren Besitzer die feste `securityadmin`-Serverrolle ist.  
  
```  
USE master;  
CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DROP SERVER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Erste Schritte mit Berechtigungen für das Datenbankmodul](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  
