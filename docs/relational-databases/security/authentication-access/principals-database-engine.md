---
title: "Prinzipale (Datenbankmodul) | Microsoft Docs"
ms.custom: ""
ms.date: "01/09/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.roleproperties.selectroll.f1"
  - "sql13.swb.databaseuser.permissions.user.f1--May use common.permissions"
helpviewer_keywords: 
  - "Zertifikate [SQL Server], Prinzipale"
  - "Rollen [SQL Server], Prinzipale"
  - "Berechtigungen [SQL Server], Prinzipale"
  - "##MS_SQLAuthenticatorCertificate##"
  - "Prinzipale [SQL Server]"
  - "##MS_SQLResourceSigningCertificate##"
  - "Gruppen [SQL Server], Prinzipale"
  - "##MS_AgentSigningCertificate##"
  - "Authentifizierung [SQL Server], Prinzipale"
  - "Schemas [SQL Server], Prinzipale"
  - "Prinzipale [SQL Server], Informationen zu Prinzipalen"
  - "Sicherheit [SQL Server], Prinzipale"
  - "Benutzer [SQL Server], Prinzipale"
  - "##MS_SQLReplicationSigningCertificate##"
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
caps.latest.revision: 57
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 55
---
# Prinzipale (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  *Prinzipale* sind Entitäten, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressourcen anfordern können. Wie bei anderen Komponenten des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Autorisierungsmodells können Prinzipale hierarchisch angeordnet werden. Der Einflussbereich eines Prinzipals richtet sich nach dem Definitionsbereich des Prinzipals (Windows, Server, Datenbank) und danach, ob der Prinzipal unteilbar ist oder es sich um eine Auflistung handelt. Ein Windows-Anmeldename ist ein Beispiel eines unteilbaren Prinzipals und eine Windows-Gruppe das eines Prinzipals, der eine Auflistung darstellt. Jeder Prinzipal weist eine Sicherheits-ID (SID) auf.  
  
 **Prinzipale auf Windows-Ebene**  
  
-   Windows-Domänenanmeldename  
  
-   Lokaler Windows-Anmeldename  
  
 **SQL Server**-**Ebenen** **Prinzipale**  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldename  
  
-   Serverrolle  
  
 **Prinzipale auf Datenbankebene**  
  
-   Datenbankbenutzer  
  
-   Datenbankrolle  
  
-   Anwendungsrolle  
  
## Der SQL Server-Anmeldename sa  
 Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldename „sa“ ist ein Prinzipal auf Serverebene. Er wird standardmäßig bei der Installation einer Instanz erstellt. Ab [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ist die Standarddatenbank von sa „Master“. Dieses Verhalten unterscheidet sich von früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## Datenbankrolle public  
 Jeder Datenbankbenutzer gehört der Datenbankrolle public an. Wenn einem Benutzer keine bestimmten Berechtigungen für ein sicherungsfähiges Element erteilt oder verweigert werden, erbt der Benutzer die Berechtigungen, die der Datenbankrolle public für dieses sicherungsfähige Element erteilt wurden.  
  
## INFORMATION_SCHEMA und sys  
 Jede Datenbank enthält zwei Entitäten, die in Katalogsichten als Benutzer angezeigt werden: INFORMATION_SCHEMA und sys. Diese Entitäten werden von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] benötigt. Es handelt sich dabei nicht um Prinzipale, die geändert oder gelöscht werden können.  
  
## Zertifikatbasierte SQL Server-Anmeldenamen  
 Serverprinzipale, deren Name von doppelten Nummernzeichen (##) eingeschlossen ist, sind nur für die systeminterne Verwendung vorgesehen. Die folgenden Prinzipale werden bei der Installation von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aus Zertifikaten erstellt und sollten nicht gelöscht werden.  
  
-   \##MS_SQLResourceSigningCertificate##  
  
-   \##MS_SQLReplicationSigningCertificate##  
  
-   \##MS_SQLAuthenticatorCertificate##  
  
-   \##MS_AgentSigningCertificate##  
  
-   \##MS_PolicyEventProcessingLogin##  
  
-   \##MS_PolicySigningCertificate##  
  
-   \##MS_PolicyTsqlExecutionLogin##  
  
## Der guest-Benutzer  
 Jede Datenbank enthält einen **Gast**. Dem **guest** -Benutzer erteilte Berechtigungen werden von Benutzern geerbt, die Zugriff auf die Datenbank, jedoch kein Benutzerkonto in der Datenbank besitzen. Der **guest** -Benutzer kann nicht gelöscht werden. Er kann jedoch deaktiviert werden, indem seine **CONNECT** -Berechtigung aufgehoben wird. Die **CONNECT**-Berechtigung kann durch Ausführen von `REVOKE CONNECT FROM GUEST` in einer beliebigen Datenbank mit Ausnahme der master- oder tempdb-Datenbank aufgehoben werden.  
  
## Client und Datenbankserver  
 Laut Definition sind ein Client und ein Datenbankserver Sicherheitsprinzipale und können gesichert werden. Diese Entitäten können gegenseitig authentifiziert werden, bevor eine sichere Netzwerkverbindung hergestellt wird. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt das [Kerberos](http://go.microsoft.com/fwlink/?LinkId=100758) -Authentifizierungsprotokoll, das festlegt, wie Clients mit einem Netzwerkauthentifizierungsdienst interagieren.  
  
## Verwandte Aufgaben  
 Informationen zum Entwerfen eines Berechtigungssystems finden Sie unter [Getting Started with Database Engine Permissions](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
 Dieser Abschnitt der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Onlinedokumentation umfasst die folgenden Themen:  
  
-   [Verwalten von Anmeldungen, Benutzern und Schemas: Vorgehensweisen](../../../relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [Rollen auf Serverebene](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [Rollen auf Datenbankebene](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [Anwendungsrollen](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## Siehe auch  
 [Sichern von SQL Server](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [Rollen auf Serverebene](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Rollen auf Datenbankebene](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  