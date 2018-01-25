---
title: ALTER RESOURCE GOVERNOR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER RESOURCE GOVERNOR
- ALTER_RESOURCE_GOVERNOR_TSQL
- ALTER RESOURCE GOVERNOR RECONFIGURE
- ALTER_RESOURCE_GOVERNOR_RECONFIGURE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ALTER RESOURCE GOVERNOR
- RECONFIGURE, ALTER RESOURCE GOVERNOR
ms.assetid: 442c54bf-a0a6-4108-ad20-db910ffa6e3c
caps.latest.revision: "49"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7650a9eec60108a5dbd228b21a27573cc72ca4fc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="alter-resource-governor-transact-sql"></a>ALTER RESOURCE GOVERNOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese Anweisung wird verwendet, um die folgenden Aktionen für die Ressourcenkontrolle in ausführen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Übernehmen Sie die konfigurationsänderungen angegeben, wenn der CREATE | ALTER | DROP WORKLOAD GROUP oder der CREATE | ALTER | DROP RESOURCE POOL oder der CREATE | ALTER | DROP EXTERNAL RESOURCE POOL-Anweisungen ausgegeben werden.  
  
-   Aktivieren bzw. Deaktivieren der Ressourcenkontrolle.  
  
-   Konfigurieren der Klassifizierung für eingehende Anforderungen.  
  
-   Zurücksetzen der Statistik für Arbeitsauslastungsgruppen und Ressourcenpools.  
  
-   Festlegen der maximalen E/A-Vorgänge pro Datenträgervolume.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER RESOURCE GOVERNOR   
      { DISABLE | RECONFIGURE }  
    | WITH ( CLASSIFIER_FUNCTION = { schema_name.function_name | NULL } )  
    | RESET STATISTICS  
    | WITH ( MAX_OUTSTANDING_IO_PER_VOLUME = value )   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 DISABLE  
 Deaktiviert die Ressourcenkontrolle. Das Deaktivieren der Ressourcenkontrolle hat die folgenden Ergebnisse:  
  
-   Die Klassifizierungsfunktion wird nicht ausgeführt.  
  
-   Alle neuen Verbindungen werden automatisch der Standardgruppe zugewiesen.  
  
-   Vom System initiierte Anforderungen werden der internen Arbeitsauslastungsgruppe zugewiesen.  
  
-   Alle Einstellungen für bestehende Arbeitsauslastungsgruppen und Ressourcenpools werden auf die Standardwerte zurückgesetzt. In diesem Fall werden keine Ereignisse ausgelöst, wenn Grenzwerte erreicht werden.  
  
-   Die reguläre Systemüberwachung bleibt unbeeinflusst.  
  
-   Änderungen an der Konfiguration vorgenommen werden können, aber die Änderungen werden wirksam, bis die Ressourcenkontrolle aktiviert ist.  
  
-   Beim Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lädt die Ressourcenkontrolle nicht ihre Konfiguration, sondern enthält lediglich die Standardgruppen und -pools sowie die internen Gruppen und Pools.  
  
 RECONFIGURE  
 Wenn die Ressourcenkontrolle nicht aktiviert ist, wird sie durch RECONFIGURE aktiviert. Das Aktivieren der Ressourcenkontrolle hat die folgenden Ergebnisse:  
  
-   Die Klassifizierungsfunktion wird für neue Verbindungen ausgeführt, damit deren Arbeitsauslastung Arbeitsauslastungsgruppen zugeordnet werden kann.  
  
-   Die in der Konfiguration der Ressourcenkontrolle angegebenen Ressourcengrenzwerte werden überprüft und durchgesetzt.  
  
-   Anforderungen, die bereits bestanden, bevor die Ressourcenkontrolle sind alle konfigurationsänderungen betroffen, die vorgenommen wurden, wenn die Ressourcenkontrolle deaktiviert wurde.  
  
 Wenn die Ressourcenkontrolle ausgeführt wird, gilt RECONFIGURE Konfiguration Änderungen erforderlich, wenn der CREATE | ALTER | DROP WORKLOAD GROUP oder der CREATE | ALTER | DROP RESOURCE POOL oder der CREATE | ALTER | DROP EXTERNAL RESOURCE POOL-Anweisungen werden ausgeführt.  
  
> [!IMPORTANT]  
>  ALTER RESOURCE GOVERNOR RECONFIGURE muss ausgegeben werden, damit Konfigurationsänderungen wirksam werden.  
  
 CLASSIFIER_FUNCTION = { *Schema_name***.*** Funktionsname* | NULL}  
 Registriert die Klassifizierungsfunktion durch angegebenen *function_name*. Diese Funktion klassifiziert jede neue Sitzung und weist die Sitzungsanforderungen und Abfragen einer Arbeitsauslastungsgruppe zu. Bei Verwendung von NULL werden neue Sitzungen automatisch der Standardarbeitsauslastungsgruppe zugewiesen.  
  
 RESET STATISTICS  
 Setzt die Statistik für alle Arbeitsauslastungsgruppen und Ressourcenpools zurück. Weitere Informationen finden Sie unter [dm_resource_governor_workload_groups &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md) und [dm_resource_governor_resource_pools &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
 MAX_OUTSTANDING_IO_PER_VOLUME = *value*  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Legt die maximale Anzahl an E/A-Vorgängen in der Warteschlange pro Datenträgervolume fest. Bei diesen E/A-Vorgängen kann es sich um Lese- oder Schreibvorgänge beliebiger Größe handeln.  Der Maximalwert für MAX_OUTSTANDING_IO_PER_VOLUME ist 100. Der Wert ist kein Prozentsatz. Diese Einstellung ist so konzipiert, dass sie die E/A-Ressourcenkontrolle auf die E/A-Eigenschaften eines Datenträgervolumes abstimmt. Es wird empfohlen, verschiedene Werte auszuprobieren und ggf. ein Kalibrierungstool wie IOMeter, [DiskSpd](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223), oder SQLIO (veraltet), um den Maximalwert für das Speichersubsystem festzulegen. Diese Einstellung bietet eine Sicherheitsprüfung auf Systemebene, die es SQL Server ermöglicht, den minimalen IOPS-Wert für Ressourcenpools einzuhalten, auch wenn die MAX_IOPS_PER_VOLUME-Einstellung anderer Pools auf einen unbegrenzten Wert festgelegt ist. Weitere Informationen zu MAX_IOPS_PER_VOLUME finden Sie unter [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 ALTER RESOURCE GOVERNOR DISABLE, ALTER RESOURCE GOVERNOR RECONFIGURE und ALTER RESOURCE GOVERNOR RESET STATISTICS können nicht in einer Benutzertransaktion verwendet werden.  
  
 Die RECONFIGURE-Parameter ist Teil der Syntax der Ressourcenkontrolle und darf nicht mit verwechselt werden [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md), dies ist eine separate DDL-Anweisung.  
  
 Sie sollten mit den Status der Ressourcenkontrolle vertraut sein, bevor Sie DDL-Anweisungen ausführen. Weitere Informationen finden Sie unter [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-starting-the-resource-governor"></a>A. Starten der Ressourcenkontrolle  
 Nach der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist die Ressourcenkontrolle zunächst deaktiviert. Im folgenden Beispiel wird die Ressourcenkontrolle gestartet. Sobald die Anweisung ausgeführt wurde, ist die Ressourcenkontrolle gestartet und kann die vordefinierten Arbeitsauslastungsgruppen und Ressourcenpools verwenden.  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="b-assigning-new-sessions-to-the-default-group"></a>B. Zuweisen neuer Sitzungen zur Standardgruppe  
 Im folgenden Beispiel werden alle neuen Sitzungen der Standardarbeitsauslastungsgruppe zugewiesen, indem alle vorhandenen Klassifizierungsfunktionen aus der Konfiguration der Ressourcenkontrolle entfernt werden. Wenn keine Funktion als Klassifizierungsfunktion festgelegt ist, werden alle neuen Sitzungen der Standardarbeitsauslastungsgruppe zugewiesen. Diese Änderung gilt nur für neue Sitzungen. Vorhandene Sitzungen werden nicht beeinflusst.  
  
```  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = NULL);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="c-creating-and-registering-a-classifier-function"></a>C. Erstellen und Registrieren einer Klassifizierungsfunktion  
 Im folgenden Beispiel wird die Klassifizierungsfunktion `dbo.rgclassifier_v1` erstellt. Diese Funktion klassifiziert jede neue Sitzung anhand des Benutzer- oder Anwendungsnamens und weist die Sitzungsanforderungen und Abfragen einer bestimmten Arbeitsauslastungsgruppe zu. Sitzungen, die nicht mit dem angegebenen Benutzer- oder Anwendungsnamen übereinstimmen, werden der Standardarbeitsauslastungsgruppe zugewiesen. Anschließend wird die Klassifizierungsfunktion registriert, und die Konfigurationsänderung wird angewendet.  
  
```  
-- Store the classifier function in the master database.  
USE master;  
GO  
SET ANSI_NULLS ON;  
GO  
SET QUOTED_IDENTIFIER ON;  
GO  
CREATE FUNCTION dbo.rgclassifier_v1() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
-- Declare the variable to hold the value returned in sysname.  
    DECLARE @grp_name AS sysname  
-- If the user login is 'sa', map the connection to the groupAdmin  
-- workload group.   
    IF (SUSER_NAME() = 'sa')  
        SET @grp_name = 'groupAdmin'  
-- Use application information to map the connection to the groupAdhoc  
-- workload group.  
    ELSE IF (APP_NAME() LIKE '%MANAGEMENT STUDIO%')  
        OR (APP_NAME() LIKE '%QUERY ANALYZER%')  
            SET @grp_name = 'groupAdhoc'  
-- If the application is for reporting, map the connection to  
-- the groupReports workload group.  
    ELSE IF (APP_NAME() LIKE '%REPORT SERVER%')  
        SET @grp_name = 'groupReports'  
-- If the connection does not map to any of the previous groups,  
-- put the connection into the default workload group.  
    ELSE  
        SET @grp_name = 'default'  
    RETURN @grp_name  
END;  
GO  
-- Register the classifier user-defined function and update the   
-- the in-memory configuration.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION=dbo.rgclassifier_v1);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
### <a name="d-resetting-statistics"></a>D. Zurücksetzen von Statistiken  
 Im folgenden Beispiel wird die gesamte Statistik für Arbeitsauslastungsgruppen und Ressourcenpools zurückgesetzt.  
  
```  
ALTER RESOURCE GOVERNOR RESET STATISTICS;  
```  
  
### <a name="e-setting-the-maxoutstandingiopervolume-option"></a>E. Festlegen der MAX_OUTSTANDING_IO_PER_VOLUME-Option  
 Im folgenden Beispiel wird die MAX_OUTSTANDING_IO_PER_VOLUME-Option auf 20 festgelegt.  
  
```  
ALTER RESOURCE GOVERNOR  
WITH (MAX_OUTSTANDING_IO_PER_VOLUME = 20);   
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Sys. dm_resource_governor_workload_groups &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)  
  
  
