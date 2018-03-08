---
title: Rollen auf Serverebene | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.Security.NT_AUTHORITY.SYSTEM
- sql13.Security.BUILTIN.administrators
helpviewer_keywords:
- roles [SQL Server], server-level
- principals [SQL Server], server-level
- CONTROL SERVER permission
- fixed server roles [SQL Server]
- credentials [SQL Server], roles
- sysadmin fixed server role
- server-level roles [SQL Server]
- authentication [SQL Server], roles
ms.assetid: 7adf2ad7-015d-4cbe-9e29-abaefd779008
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a095d9f3e7839a2f3cfa14a2bf49790776f0cd1b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="server-level-roles"></a>Rollen auf Serverebene
[!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md](../../../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] stellt Rollen auf Serverebene bereit, um Sie beim Verwalten der Berechtigungen auf einem Server zu unterstützen. Bei diesen Rollen handelt es sich um Sicherheitsprinzipale, in denen andere Prinzipale gruppiert sind. Der Geltungsbereich der Berechtigungen von Rollen auf Serverebene erstreckt sich auf den gesamten Server. (*Rollen* entsprechen den *Gruppen* im Betriebssystem Windows.)  
  
 Feste Serverrollen werden der Einfachheit halber und zur Gewährung der Abwärtskompatibilität bereitgestellt. Weisen Sie nach Möglichkeit spezifischere Berechtigungen zu.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sind neun feste Serverrollen verfügbar. Die den festen Serverrollen (außer **public**) erteilten Berechtigungen können nicht geändert werden. Ab [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] können Sie benutzerdefinierte Serverrollen erstellen und diesen Berechtigungen auf Serverebene hinzufügen.  
  
 Sie können Prinzipale auf Serverebene ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldungen, Windows-Konten und Windows-Gruppen) zu Rollen auf Serverebene zusammenfassen. Jedes Mitglied einer festen Serverrolle kann der gleichen Rolle andere Anmeldenamen hinzufügen. Mitglieder benutzerdefinierter Serverrollen können der Rolle keine weiteren Serverprinzipale hinzufügen.  
>  [!NOTE]
>  Berechtigungen auf Serverebene sind in der SQL-Datenbank oder SQL Data Warehouse nicht verfügbar. Weitere Informationen zur SQL-Datenbank finden Sie unter [Steuern und Gewähren des Datenbankzugriffs](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).
  
## <a name="fixed-server-level-roles"></a>Feste Rollen auf Serverebene  
 In der folgenden Tabelle werden die festen Rollen auf Serverebene und deren Möglichkeiten angezeigt.  
  
|Feste Rolle auf Serverebene|Beschreibung|  
|------------------------------|-----------------|  
|**sysadmin**|Mitglieder der festen Serverrolle **sysadmin** können alle Aktivitäten auf dem Server ausführen.|  
|**serveradmin**|Mitglieder der festen Serverrolle **serveradmin** können serverweite Konfigurationsoptionen ändern und den Server herunterfahren.|  
|**securityadmin**|Mitglieder der festen Serverrolle **securityadmin** können Anmeldungen und deren Eigenschaften verwalten. Sie können Berechtigungen auf Serverebene erteilen (`GRANT`), verweigern (`DENY`) und widerrufen (`REVOKE`). Sie verfügen auf Datenbankebene auch über die Berechtigungen `GRANT`, `DENY` und `REVOKE`, sofern sie Zugriff eine Datenbank haben. Sie können außerdem Kennwörter für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldungen zurücksetzen.<br /><br /> **WICHTIG**: Durch die Möglichkeit, Zugriff auf [!INCLUDE[ssDE](../../../includes/ssde-md.md)] zu gewähren und Benutzerberechtigungen zu konfigurieren, kann der Sicherheitsadministrator die meisten Serverberechtigungen zuweisen. Die Rolle **securityadmin** muss als Entsprechung der Rolle **sysadmin** behandelt werden.|  
|**processadmin**|Mitglieder der festen Serverrolle **processadmin** können Prozesse beenden, die in einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausgeführt werden.|  
|**setupadmin**|Mitglieder der festen Serverrolle **setupadmin** können Verbindungsserver mithilfe von [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisungen hinzufügen und entfernen. (Die Verwendung von [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] erfordert die Mitgliedschaft in **sysadmin**.)|  
|**bulkadmin**|Mitglieder der festen Serverrolle **bulkadmin** können die `BULK INSERT`-Anweisung ausführen.|  
|**diskadmin**|Die feste Serverrolle **diskadmin** wird zum Verwalten von Datenträgerdateien verwendet.|  
|**dbcreator**|Mitglieder der festen Serverrolle **dbcreator** können beliebige Datenbanken erstellen, ändern, löschen und wiederherstellen.|  
|**öffentlich**|Jede [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldung gehört zur Serverrolle **public**. Wenn einem Serverprinzipal keine bestimmten Berechtigungen für ein sicherungsfähiges Objekt erteilt oder verweigert werden, erbt der Benutzer die Berechtigungen, die der Rolle public für dieses Objekt erteilt wurden. Weisen Sie einem Objekt nur dann public-Berechtigungen zu, wenn das Objekt für alle Benutzer verfügbar sein soll. Sie können keine Mitgliedschaft in „public“ ändern.<br /><br /> **Hinweis:** **Public** wird anders implementiert als andere Rollen, und Berechtigungen können der öffentlichen festen Serverrolle gewährt, ihr verweigert oder für sie widerrufen werden.|  
  
## <a name="permissions-of-fixed-server-roles"></a>Berechtigungen fester Serverrollen  
 Jede feste Serverrolle besitzt bestimmte Berechtigungen. Die folgende Grafik zeigt die den Serverrollen zugewiesenen Berechtigungen:   
![fixed_server_role_permissions](../../../relational-databases/security/authentication-access/media/permissions-of-server-roles.png)   
  
> [!IMPORTANT]  
>  Die Berechtigung **CONTROL SERVER** ist ähnlich, aber nicht identisch mit der festen Serverrolle **sysadmin** . Berechtigungen umfassen keine Rollenmitgliedschaften, und Rollenmitgliedschaften gewähren keine Berechtigungen. (D. h. **CONTROL SERVER** impliziert nicht die Mitgliedschaft in der festen Serverrolle **sysadmin**. Es ist jedoch manchmal möglich, die Identität zwischen Rollen und entsprechenden Berechtigungen zu wechseln. Die meisten **DBCC** -Befehle und viele Systemprozeduren erfordern die Mitgliedschaft in der festen Serverrolle **sysadmin** . Eine Liste mit 171 gespeicherten Systemprozeduren, die eine **sysadmin** -Mitgliedschaft erfordern, finden Sie im folgenden Blogbeitrag von Andreas Wolter: [CONTROL gegen sysadmin/sa: Berechtigungen, Systemprozeduren, DBCC, automatische Schema-Erstellung und Privilegienausweitung – Fallstricke](http://www.insidesql.org/blogs/andreaswolter/2013/08/control-server-vs-sysadmin-sa-permissions-privilege-escalation-caveats).  
  
## <a name="server-level-permissions"></a>Berechtigung auf Serverebene  
 Benutzerdefinierten Serverrollen können nur Berechtigungen auf Serverebene hinzugefügt werden. Führen Sie zum Auflisten der Berechtigungen auf Serverebene die folgende Anweisung aus. Folgende Berechtigungen gelten auf Serverebene:  
  
```  
SELECT * FROM sys.fn_builtin_permissions('SERVER') ORDER BY permission_name;  
```  
  
 Weitere Informationen zu Berechtigungen finden Sie unter [Berechtigungen &#40;Datenbankmodul&#41;](../../../relational-databases/security/permissions-database-engine.md) und [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md).  
  
## <a name="working-with-server-level-roles"></a>Arbeiten mit Rollen auf Serverebene  
 In der folgenden Tabelle werden die Befehle, Sichten und Funktionen erklärt, die Sie beim Arbeiten mit Rollen auf Serverebene verwenden können.  
  
|Funktion|Typ|Beschreibung|  
|-------------|----------|-----------------|  
|[sp_helpsrvrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)|Metadaten|Gibt eine Liste von Rollen auf Serverebene zurück.|  
|[sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)|Metadaten|Gibt Informationen zu Mitgliedern einer Rolle auf Serverebene zurück.|  
|[sp_srvrolepermission &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)|Metadaten|Zeigt die Berechtigungen einer Rolle auf Serverebene an.|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-srvrolemember-transact-sql.md)|Metadaten|Gibt an, ob eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldung Mitglied der angegebenen Rolle auf Serverebene ist.|  
|[sys.server_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)|Metadaten|Gibt eine Zeile für jedes Mitglied jeder Rolle auf Serverebene zurück.|  
|[sp_addsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)|Befehl|Fügt einen Benutzernamen als Mitglied einer Rolle auf Serverebene hinzu. Veraltet. Verwenden Sie stattdessen [ALTER SERVER ROLE](../../../t-sql/statements/alter-server-role-transact-sql.md) .|  
|[sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)|Befehl|Entfernt einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldenamen oder einen Windows-Benutzer bzw. eine -Gruppe aus einer Rolle auf Serverebene. Veraltet. Verwenden Sie stattdessen [ALTER SERVER ROLE](../../../t-sql/statements/alter-server-role-transact-sql.md) .|  
|[CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-role-transact-sql.md)|Befehl|Erstellt eine benutzerdefinierte Serverrolle.|  
|[ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md)|Befehl|Ändert die Mitgliedschaft einer Serverrolle oder ändert Namen einer benutzerdefinierten Serverrolle.|  
|[DROP SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-role-transact-sql.md)|Befehl|Entfernt eine benutzerdefinierte Serverrolle.|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-srvrolemember-transact-sql.md)|Funktion|Bestimmt die Mitgliedschaft einer Serverrolle.|  
  
## <a name="see-also"></a>Siehe auch  
 [Rollen auf Datenbankebene](../../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)   
 [Sichern von SQL Server](../../../relational-databases/security/securing-sql-server.md)   
 [GRANT (Berechtigungen für Serverprinzipal) &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [REVOKE (Berechtigungen für Serverprinzipal) &#40;Transact-SQL&#41;](../../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [DENY (Berechtigungen für Serverprinzipal) &#40;Transact-SQL&#41;](../../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)   
 [Erstellen einer Serverrolle](../../../relational-databases/security/authentication-access/create-a-server-role.md)  
  
  
