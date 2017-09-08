---
title: REVOKE (Endpunktberechtigungen) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
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
- REVOKE statement, endpoints
- permissions [SQL Server], endpoints
ms.assetid: 826f513e-9ad0-46b9-87ad-7525713638c8
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad8770d584c82fc6c5de12104059717030d21f87
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-endpoint-permissions-transact-sql"></a>REVOKE (Endpunktberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Hebt die Berechtigungen auf, die für einen Endpunkt erteilt oder verweigert wurden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON ENDPOINT :: endpoint_name  
    { FROM | TO } <server_principal> [ ,...n ]  
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
 Gibt eine Berechtigung an, die für einen Endpunkt erteilt werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 AUF dem ENDPUNKT **::***Endpoint_name*  
 Gibt den Endpunkt an, für den die Berechtigung erteilt wird. Der bereichsqualifizierer (**::**) ist erforderlich.  
  
 {AUS | AN} \<Server_principal > Gibt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung, die von dem die Berechtigung aufgehoben wird.  
  
 *SQL_Server_login*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_Windows_login*  
 Gibt einen aus einem Windows-Anmeldenamen erstellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_certificate*  
 Gibt einen einem Zertifikat zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_AsymKey*  
 Gibt einen einem asymmetrischen Schlüssel zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 GRANT OPTION  
 Gibt an, dass das Recht zum Erteilen der angegebenen Berechtigung für andere Prinzipale aufgehoben wird. Die Berechtigung selbst wird nicht aufgehoben.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 CASCADE  
 Gibt an, dass die aufgehobene Berechtigung auch für andere Prinzipale aufgehoben wird, denen sie von diesem Prinzipal erteilt oder verweigert wurde.  
  
> [!CAUTION]  
>  Durch ein kaskadiertes Aufheben einer Berechtigung, die mit GRANT OPTION erteilt wurde, werden sowohl GRANT als auch DENY für diese Berechtigung aufgehoben.  
  
 AS *SQL_Server_login*  
 Gibt den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Aufheben der Berechtigung ableitet.  
  
## <a name="remarks"></a>Hinweise  
 Berechtigungen im Serverbereich können nur, wenn die aktuelle Datenbank ist gesperrt werden **master**.  
  
 Informationen zu Endpunkten werden in der [sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md) -Katalogsicht angezeigt. Informationen zu Serverberechtigungen werden in der [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) -Katalogsicht und Informationen zu serverprinzipalen werden in der [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) -Katalogsicht angezeigt.  
  
 Ein Endpunkt ist ein sicherungsfähiges Element auf Serverebene. Die spezifischsten und restriktivsten Berechtigungen, die für einen Endpunkt aufgehoben werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
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
  
### <a name="a-revoking-view-definition-permission-on-an-endpoint"></a>A. Aufheben der VIEW DEFINITION-Berechtigung für einen Endpunkt  
 Im folgenden Beispiel wird die `VIEW DEFINITION`-Berechtigung für den Endpunkt `Mirror7` für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `ZArifin` aufgehoben.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON ENDPOINT::Mirror7 FROM ZArifin;  
GO  
```  
  
### <a name="b-revoking-take-ownership-permission-with-the-cascade-option"></a>B. Aufheben der TAKE OWNERSHIP-Berechtigung mit der CASCADE-Option  
 Das folgende Beispiel hebt `TAKE OWNERSHIP` Berechtigung für den Endpunkt `Shipping83` aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Benutzer `PKomosinski` und für alle Prinzipale, `PKomosinski` gewährt `TAKE OWNERSHIP` auf `Shipping83`.  
  
```  
USE master;  
REVOKE TAKE OWNERSHIP ON ENDPOINT::Shipping83 FROM PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT (Endpunktberechtigungen) (Transact-SQL)](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [DENY (Endpunktberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [Endpunkte-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Sys.Endpoints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  


