---
title: Prinzipale (Datenbankmodul) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.roleproperties.selectroll.f1
- sql13.swb.databaseuser.permissions.user.f1--May use common.permissions
helpviewer_keywords:
- certificates [SQL Server], principals
- roles [SQL Server], principals
- permissions [SQL Server], principals
- '##MS_SQLAuthenticatorCertificate##'
- principals [SQL Server]
- '##MS_SQLResourceSigningCertificate##'
- groups [SQL Server], principals
- '##MS_AgentSigningCertificate##'
- authentication [SQL Server], principals
- schemas [SQL Server], principals
- principals [SQL Server], about principals
- security [SQL Server], principals
- users [SQL Server], principals
- '##MS_SQLReplicationSigningCertificate##'
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ab67ccf5240ad3797bf744b56e615a92fa95d9bd
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="principals-database-engine"></a>Prinzipale (Datenbankmodul)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  *Prinzipale* sind Entitäten, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressourcen anfordern können. Wie bei anderen Komponenten des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Autorisierungsmodells können Prinzipale hierarchisch angeordnet werden. Der Einflussbereich eines Prinzipals richtet sich nach dem Definitionsbereich des Prinzipals (Windows, Server, Datenbank) und danach, ob der Prinzipal unteilbar ist oder es sich um eine Auflistung handelt. Ein Windows-Anmeldename ist ein Beispiel eines unteilbaren Prinzipals und eine Windows-Gruppe das eines Prinzipals, der eine Auflistung darstellt. Jeder Prinzipal weist eine Sicherheits-ID (SID) auf. Dieses Thema gilt für alle Versionen von SQL Server, jedoch gibt es bei Prinzipalen auf Serverebene in der SQL-Datenbank oder SQL Data Warehouse eine Reihe von Einschränkungen. 
  
## <a name="sql-server-level-principals"></a>Prinzipale auf SQL Server-Ebene  
  
-  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmelde-ID für die Authentifizierung   
-  Anmeldung mit Windows-Authentifizierung für Windows-Benutzer  
-  Anmeldung mit Windows-Authentifizierung für Windows-Gruppe   
-  Anmeldung mit Azure Active Directory-Authentifizierung für AD-Benutzer
-  Anmeldung mit Azure Active Directory-Authentifizierung für AD-Gruppe
-  Serverrolle  
  
 ## <a name="database-level-principals"></a>Prinzipale auf Datenbankebene  
  
-   Datenbankbenutzer (Es gibt 11 Benutzertypen. Weitere Informationen finden Sie unter [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md).) 
-   Datenbankrolle  
-   Anwendungsrolle  
  
## <a name="sa-login"></a>Anmeldename „sa“  
 Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `sa`-Anmeldename ist ein Prinzipal auf Serverebene. Er wird standardmäßig bei der Installation einer Instanz erstellt. Ab [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]ist die Standarddatenbank von sa „Master“. Dieses Verhalten unterscheidet sich von früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Der `sa`-Anmeldename ist ein Mitglied der festen Datenbankrolle `sysadmin`. Der `sa`-Anmeldename besitzt alle Berechtigungen auf dem Server und kann nicht beschränkt werden. Der `sa`-Anmeldename kann nicht gelöscht werden. Jedoch kann er deaktiviert werden, sodass er nicht verwendet werden kann.

## <a name="dbo-user-and-dbo-schema"></a>dbo-Benutzer und dbo-Schema

Der `dbo`-Benutzer ist ein bestimmter Benutzerprinzipal in jeder Datenbank. Alle SQL Server-Administratoren, Mitglieder der festen Serverrolle `sysadmin`, `sa`-Anmeldenamen und Besitzer der Datenbank treten in Datenbanken als `dbo`-Benutzer ein. Der `dbo`-Benutzer besitzt alle Berechtigungen in der Datenbank und kann nicht beschränkt oder gelöscht werden. `dbo` steht für Datenbankbesitzer. Doch das `dbo`-Benutzerkonto ist nicht identisch mit der festen Datenbankrolle `db_owner`, und die feste Datenbankrolle `db_owner` ist wiederum nicht identisch mit dem Benutzerkonto, das als Besitzer der Datenbank aufgezeichnet ist.     
Der `dbo`-Benutzer besitzt das `dbo`-Schema. Das `dbo`-Schema ist das Standardschema für alle Benutzer, sofern kein anderes Schema angegeben wird.  Das `dbo`-Schema kann nicht gelöscht werden.
  
## <a name="public-server-role-and-database-role"></a>Serverrolle und Datenbankrolle „public“  
Jeder Anmeldename gehört zu der festen Serverrolle `public`, und jeder Datenbankbenutzer gehört zu der Datenbankrolle `public`. Wenn einem Anmeldenamen oder Benutzer keine bestimmten Berechtigungen für ein sicherungsfähiges Element erteilt oder verweigert werden, erbt der Anmeldename oder Benutzer die Berechtigungen, die der Datenbankrolle public für dieses sicherungsfähige Element erteilt wurden. Die feste Serverrolle `public` und die feste Datenbankrolle `public` können nicht gelöscht werden. Sie können jedoch Berechtigungen für die Rollen `public` widerrufen. Es gibt viele Berechtigungen, die den Rollen `public` standardmäßig zugewiesen sind. Die meisten dieser Berechtigungen sind für Routinevorgänge in der Datenbank erforderlich. Diese Vorgänge sollten von jedem ausgeführt werden können. Gehen Sie beim Aufheben der Berechtigungen von public-Anmeldenamen oder -Benutzern vorsichtig vor, da sich die Aufhebung auf alle Anmeldenamen/Benutzer auswirkt. Im Allgemeinen sollten Sie public-Berechtigungen nicht verweigern, da die DENY-Anweisung alle GRANT-Anweisungen außer Kraft setzt, die Sie möglicherweise einzelnen Benutzern gewähren. 
  
## <a name="informationschema-and-sys-users-and-schemas"></a>INFORMATION_SCHEMA und sys-Benutzer und -Schemas 
 Jede Datenbank enthält zwei Entitäten, die in Katalogsichten als Benutzer angezeigt werden: `INFORMATION_SCHEMA` und `sys`. Diese Entitäten sind für die interne Verwendung durch das Datenbankmodul erforderlich. Sie können nicht geändert oder gelöscht werden.  
  
## <a name="certificate-based-sql-server-logins"></a>Zertifikatbasierte SQL Server-Anmeldenamen  
 Serverprinzipale, deren Name von doppelten Nummernzeichen (##) eingeschlossen ist, sind nur für die systeminterne Verwendung vorgesehen. Die folgenden Prinzipale werden bei der Installation von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aus Zertifikaten erstellt und sollten nicht gelöscht werden.  
  
-   \##MS_SQLResourceSigningCertificate##    
-   \##MS_SQLReplicationSigningCertificate##    
-   \##MS_SQLAuthenticatorCertificate##    
-   \##MS_AgentSigningCertificate##   
-   \##MS_PolicyEventProcessingLogin##   
-   \##MS_PolicySigningCertificate##   
-   \##MS_PolicyTsqlExecutionLogin##   
 
 Diese Prinzipalkonten verfügen nicht über Kennwörter, die vom Administrator geändert werden können, da sie auf den an Microsoft ausgestellten Zertifikaten basieren.
  
## <a name="the-guest-user"></a>Der guest-Benutzer  
 Jede Datenbank enthält einen `guest`. Dem `guest` -Benutzer erteilte Berechtigungen werden von Benutzern geerbt, die Zugriff auf die Datenbank, jedoch kein Benutzerkonto in der Datenbank besitzen. Der `guest`-Benutzer kann nicht gelöscht werden. Er kann jedoch deaktiviert werden, indem seine CONNECT-Berechtigung aufgehoben wird. Die CONNECT-Berechtigung kann durch Ausführen von `REVOKE CONNECT FROM GUEST;` in einer beliebigen Datenbank mit Ausnahme der `master`- oder `tempdb`-Datenbank aufgehoben werden.  
  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Informationen zum Entwerfen eines Berechtigungssystems finden Sie unter [Getting Started with Database Engine Permissions](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
 Dieser Abschnitt der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Onlinedokumentation umfasst die folgenden Themen:  
  
-   [Verwalten von Anmeldungen, Benutzern und Schemas: Vorgehensweisen](../../../relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [Rollen auf Serverebene](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [Rollen auf Datenbankebene](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [Anwendungsrollen](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern von SQL Server](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [Rollen auf Serverebene](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Rollen auf Datenbankebene](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  
