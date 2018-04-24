---
title: GRANT-T-SQL-Berechtigungen - Parallel Data Warehouse | Microsoft Docs
description: GRANT-T-SQL-Berechtigungen für Datenbankvorgängen in Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 01ef7b199a07be8bbc2dc1dee40d9c4d5771db1b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>GRANT-T-SQL-Berechtigungen für Parallel Data Warehouse
GRANT-T-SQL-Berechtigungen für Datenbankvorgängen in Parallel Data Warehouse.

## <a name="grant-permissions-to-submit-database-queries"></a>Erteilen Sie Berechtigungen zum Übermitteln von Datenbankabfragen
Dieser Abschnitt beschreibt, wie zum Gewähren von Berechtigungen für Datenbankrollen und Benutzer zum Abfragen von Daten auf der SQL Server PDW Appliance.  
  
Die Anweisungen zum Erteilen von Berechtigungen zum Abfragen von Daten hängt von den Bereich der gewünschten Zugriffsberechtigung ab. Die folgenden SQL-Anweisungen erstellen Sie eine Anmeldung, die mit dem Namen KimAbercrombie, die auf das Gerät zugreifen können, erstellen einen Datenbankbenutzer namens KimAbercrombie in der **AdventureWorksPDW2012** Datenbank, eine Datenbankrolle mit dem Namen PDWQueryData erstellen, fügt die Verwendung Grundlage, dass KimAbercrombie in der PDWQueryData-Rolle, und klicken Sie dann Optionen zum Gewähren des Zugriffs für Abfragen, anzeigen, ob der Zugriff auf das Objekt oder Datenbankebene gewährt wird.  
  
```sql  
USE master;  
GO  
  
CREATE LOGIN KimAbercrombie WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
USE AdventureWorksPDW2012;  
GO  
  
CREATE USER KimAbercrombie;  
GO  
  
CREATE ROLE PDWQueryData;  
GO  
  
EXEC sp_addrolemember 'PDWQueryData', 'KimAbercrombie'  
GO  
  
-- If the permission is granted against a table or view only, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO PDWQueryData;  
GO  
  
-- If the permission is granted for the database, use this syntax:  
GRANT SELECT ON DATABASE::AdventureWorksPDW2012 TO PDWQueryData;  
GO  
  
-- If KimAbercrombie is the only user that needs to access a table, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO KimAbercrombie;  
GO  
```  
  
## <a name="grant-permissions-to-use-the-admin-console"></a>Erteilen von Berechtigungen für die Verwendung der Verwaltungskonsole
Dieser Abschnitt beschreibt, wie mithilfe der Verwaltungskonsole auf Anmeldungen gewähren.  
  
**Verwenden Sie die Admin-Konsole**  
  
Mithilfe der Admin-Konsole erfordert eine Anmeldung Serverebene **VIEW SERVER STATE** Berechtigung. Die folgende SQL-Anweisung erteilt die **VIEW SERVER STATE** Berechtigung für die Anmeldung `KimAbercrombie` sodass Sven die-Verwaltungskonsole zum Überwachen der SQL Server PDW Appliance verwenden kann.  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**Beenden von Sitzungen**  
  
Wenn einer Anmeldung die Berechtigung zum Beenden von Sitzungen, erteilen Sie dem **ALTER ANY CONNECTION** Berechtigung wie folgt:  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>Erteilen von Berechtigungen zum Laden von Daten
Dieser Abschnitt beschreibt, wie zum Laden von Daten auf dem SQL Server-PDWappliance Datenbankbenutzer und Datenbankrollen Berechtigungen.  
  
Das folgende Skript zeigt, welche Berechtigungen für jede einzelne Option Laden erforderlich sind. Sie können diese Option, um Ihre speziellen Anforderungen ändern.  
  
```sql  
-- Create server login for the examples that follow.  
USE master;  
CREATE LOGIN BI_ETLUser WITH PASSWORD = '******';  
  
--Grant BULK Load permissions   
GRANT ADMINISTER BULK OPERATIONS TO BI_ETLUser;  
  
--Grant Staging database permissions  
USE stagedb;  
CREATE USER BI_ETLUser for login BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
EXEC sp_addrolemember 'db_ddladmin','BI_ETLUser';  
  
-- The CREATE TABLE permission is required for the database hosting the temporary table.  
-- This may be the staging database (if specified) or destination database.   
-- The CREATE permission is not required if loading in fastappend mode.  
GRANT CREATE TABLE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in append or fastappend mode, the INSERT permission is required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
  
-- If loading in reload mode, the INSERT and DELETE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT DELETE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in upsert mode, the INSERT and UPDATE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT UPDATE ON database::stagedb TO BI_ETLUser;  
  
-- Destination DB  
USE tpch_1gb;  
CREATE USER BI_ETLUser FOR LOGIN BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
```  
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>Gewähren von Berechtigungen für das Kopieren von Daten aus der Anwendung
Dieser Abschnitt beschreibt die Vorgehensweise zum Kopieren von Daten aus der SQL Server PDW-Anwendung auf einen Benutzer oder eine Datenbankrolle gewähren.  
  
Zum Verschieben von Daten an einen anderen Speicherort erfordert **wählen** -Berechtigung für die Tabelle mit den Daten verschoben werden soll.  
  
Wenn das Ziel für die Daten einer anderen SQL Server PDW ist, kann der Benutzer benötigt **CREATE TABLE** Berechtigung am Ziel und **ALTER SCHEMA** -Berechtigung für das Schema, das die Tabelle enthalten ist.  
  
## <a name="grant-permissions-to-manage-databases"></a>Erteilen von Berechtigungen zum Verwalten von Datenbanken
Dieser Abschnitt beschreibt das Gewähren von Berechtigungen für Datenbankbenutzer in einer Datenbank auf dem SQL Server PDW-Anwendung verwalten.  
  
In einigen Situationen weist ein Unternehmen einen für eine Datenbank-Manager. Der Manager steuert den Zugriff, den andere Anmeldenamen mit der Datenbank als auch die Daten und Objekte in der Datenbank haben. Zum Verwalten aller Objekte, Rollen und Benutzer in einer Datenbank gewähren Sie dem Benutzer die **Steuerelement** Berechtigung für die Datenbank. Die folgende Anweisung erteilt die **Steuerelement** -Berechtigung für die **AdventureWorksPDW2012** Datenbank für den Benutzer `KimAbercrombie`.  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
Um einem Benutzer die Berechtigung für alle Datenbanken auf dem Gerät steuern erteilen der **ALTER ANY DATABASE** -Berechtigung in der master-Datenbank.  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>Erteilen von Berechtigungen zum Verwalten von Anmeldungen, Benutzer und -Datenbankrollen
Dieser Abschnitt beschreibt, wie Berechtigungen zur Verwaltung von Anmeldungen, Datenbankbenutzer und Datenbankrollen gewähren.  
  
### <a name="PermsAdminConsole"></a>Erteilen von Berechtigungen zum Verwalten der Anmeldenamen  
**Hinzufügen oder Verwalten von Anmeldungen**  
  
Die folgenden SQL-Anweisungen erstellen Sie eine Anmeldung, die mit dem Namen KimAbercrombie, die neue Anmeldungen erstellen kann die [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) Anweisung und bereits vorhandener Anmeldungen ändern, indem die [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md) Anweisung.  
  
Die **ALTER ANY LOGIN** Berechtigung bietet die Möglichkeit zum Erstellen neuer Anmeldenamen und löschen vorhandene. Sobald eine Anmeldung vorhanden ist, kann die Anmeldung von Anmeldungen mit verwaltet werden die **ALTER ANY LOGIN** Berechtigung oder die **ALTER** Berechtigung für diesen Anmeldenamen. Ein Anmeldename kann das Kennwort und einer Standarddatenbank für seine eigene Anmeldung ändern.  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>Gewähren von Berechtigungen für die Anmeldung Sitzungen zu verwalten  
Erfordert die haben der Möglichkeit zum Anzeigen von allen Sitzungen auf dem Server die **VIEW SERVER STATE** Berechtigung. Das Beenden von Sitzungen in der anderen Anmeldungen erfordert die **ALTER ANY CONNECTION** Berechtigung. Im folgenden Beispiel wird die `KimAbercrombie` Anmeldung, die zuvor erstellt haben.  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>Erteilen der Berechtigung zum Verwalten von Datenbankbenutzern  
Erstellen und Löschen von Datenbankbenutzern erfordert die **ALTER ANY USER** Berechtigung. Verwalten von vorhandenen Benutzern erfordert die **ALTER ANY USER** Berechtigung oder die **ALTER** Berechtigung für diesen Benutzer. Im folgenden Beispiel wird die `KimAbercrombie` Anmeldung, die zuvor erstellt haben.  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>Erteilen Sie über die entsprechenden Berechtigungen zum Verwalten von Datenbankrollen  
Erstellen und löschen eine benutzerdefinierte Datenbankrollen erfordert die **ALTER ANY ROLE** Berechtigung. Im folgenden Beispiel wird die `KimAbercrombie` Anmelde- und verwenden, die zuvor erstellt haben.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>Anmeldung, Benutzer und Rollen Berechtigung Diagramme  
Die folgenden Diagramme können verwirrend sein, aber wie höhere Hebel Berechtigungen (z. B.-Steuerelement) zeigen enthalten spezifischere Berechtigungen, die separat (z. B. ALTER) erteilt werden können. Es wird empfohlen, immer die geringstmöglichen Berechtigungen für eine Person ihre erforderlichen Aufgaben auszuführen zu gewähren. Zu diesem Zweck spezifischere Berechtigungen, anstelle der obersten Ebene Berechtigungen zu gewähren.  
  
**Login-Berechtigungen verfügen:**  
  
![APS-sicherheitsanmeldeberechtigungen](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**Berechtigungen des Benutzers:**  
  
![APS-sicherheitsbenutzerberechtigungen](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**Rollenberechtigungen:**  
  
![APS-Sicherheitsrollenberechtigungen](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>Gewähren von Berechtigungen für die Anwendung überwachen
Die SQL Server PDW-Anwendung kann mithilfe der Verwaltungskonsole oder der SQL Server PDW-Systemsichten überwacht werden. Anmeldungen müssen Serverebene **VIEW SERVER STATE** über die Berechtigung zum Überwachen der Appliance. Anmeldungen müssen die **ALTER ANY CONNECTION** Berechtigung, um Verbindungen mit der Verwaltungskonsole zu beenden oder die **KILL** Befehl. Informationen über ausreichende Berechtigungen zum Verwenden der Verwaltungskonsole finden Sie unter [Erteilen von Berechtigungen zum Verwenden der Verwaltungskonsole &#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console).  
  
### <a name="PermsAdminConsole"></a>Erteilen der Berechtigung zum Überwachen der Appliance mithilfe von Systemsichten  
Die folgenden SQL-Anweisungen erstellen Sie eine Anmeldung, die mit dem Namen `monitor_login` und erteilt ihm die **VIEW SERVER STATE** über die Berechtigung zum der `monitor_login` Anmeldung.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>Erteilen von Berechtigungen zum Überwachen der Appliance mithilfe von Systemsichten und Verbindungen beenden  
Die folgenden SQL-Anweisungen erstellen Sie eine Anmeldung, die mit dem Namen `monitor_and_terminate_login` und erteilt ihm die **VIEW SERVER STATE** und **ALTER ANY CONNECTION** Berechtigungen für die `monitor_and_terminate_login` Anmeldung.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
Admin-Anmeldungen erstellen zu können, finden Sie unter [fester Serverrollen](pdw-permissions.md#fixed-server-roles).  
  
## <a name="see-also"></a>Siehe auch
[ANMELDUNGSERSTELLUNG](../t-sql/statements/create-login-transact-sql.md)  
[BENUTZER ERSTELLEN](../t-sql/statements/create-user-transact-sql.md)  
[ERSTELLEN DER ROLLE ""](../t-sql/statements/create-role-transact-sql.md)  
[Auslastungstest](load-overview.md)  
