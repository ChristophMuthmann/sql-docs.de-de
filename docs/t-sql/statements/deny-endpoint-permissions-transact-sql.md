---
title: DENY (Endpunktberechtigungen) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- endpoints [SQL Server], permissions
- DENY statement, endpoints
- denying permissions [SQL Server], endpoints
- permissions [SQL Server], endpoints
ms.assetid: 3ac40457-7529-4eda-95a4-5247345cc8cf
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a263d6a5a576b4f4e06bb44a6c6fb40c99e64660
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="deny-endpoint-permissions-transact-sql"></a>DENY (Endpunktberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verweigert Berechtigungen für einen Endpunkt.  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DENY permission  [ ,...n ] ON ENDPOINT :: endpoint_name  
    TO < server_principal >  [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für einen Endpunkt verweigert werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 AUF dem ENDPUNKT **::***Endpoint_name*  
 Gibt den Endpunkt an, für den die Berechtigung verweigert wird. Der bereichsqualifizierer (**::**) ist erforderlich.  
  
 UM \<Server_principal >  
 Gibt den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, für den die Berechtigung verweigert wird.  
  
 *SQL_Server_login*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_Windows_login*  
 Gibt einen aus einem Windows-Anmeldenamen erstellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_certificate*  
 Gibt einen einem Zertifikat zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_AsymKey*  
 Gibt einen einem asymmetrischen Schlüssel zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 CASCADE  
 Gibt an, dass die verweigerte Berechtigung auch anderen Prinzipalen verweigert wird, denen diese Berechtigung von diesem Prinzipal erteilt wurde.  
  
 AS *SQL_Server_login*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Verweigern der Berechtigung ableitet.  
  
## <a name="remarks"></a>Hinweise  
 Berechtigungen im Serverbereich können verweigert werden, nur, wenn die aktuelle Datenbank ist **master**.  
  
 Informationen zu Endpunkten werden in der [sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md) -Katalogsicht angezeigt. Informationen zu Serverberechtigungen werden in der [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) -Katalogsicht und Informationen zu serverprinzipalen werden in der [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) -Katalogsicht angezeigt.  
  
 Ein Endpunkt ist ein sicherungsfähiges Element auf Serverebene. Die spezifischsten und restriktivsten Berechtigungen, die für einen Endpunkt verweigert werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Endpunktberechtigung|Impliziert durch die Endpunktberechtigung|Impliziert durch die Serverberechtigung|  
|-------------------------|------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY ENDPOINT|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für den Endpunkt oder die ALTER ANY ENDPOINT-Berechtigung für den Server.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-denying-view-definition-permission-on-an-endpoint"></a>A. Verweigern der VIEW DEFINITION-Berechtigung für einen Endpunkt  
 Im folgenden Beispiel wird verweigert `VIEW DEFINITION` Berechtigung für den Endpunkt `Mirror7` auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung `ZArifin`.  
  
```  
USE master;  
DENY VIEW DEFINITION ON ENDPOINT::Mirror7 TO ZArifin;  
GO  
```  
  
### <a name="b-denying-take-ownership-permission-with-cascade-option"></a>B. Verweigern der TAKE OWNERSHIP-Berechtigung mit CASCADE-Option  
 Im folgenden Beispiel wird die `TAKE OWNERSHIP`-Berechtigung für den Endpunkt `Shipping83` für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer `PKomosinski` und für alle Prinzipale verweigert, denen von `PKomosinski` die `TAKE OWNERSHIP`-Berechtigung erteilt wurde.  
  
```  
USE master;  
DENY TAKE OWNERSHIP ON ENDPOINT::Shipping83 TO PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT (Endpunktberechtigungen) (Transact-SQL)](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [REVOKE (Endpunktberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [Endpunkte-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Sys.Endpoints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

