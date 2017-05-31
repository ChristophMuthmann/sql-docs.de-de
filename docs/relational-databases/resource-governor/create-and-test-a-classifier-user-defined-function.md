---
title: Erstellen und Testen einer benutzerdefinierten Klassifizierungsfunktion | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, classifier function create
- classifier function [SQL Server], test
- classifier function [SQL Server], create
- Resource Governor, classifier function test
ms.assetid: 7866b3c9-385b-40c6-aca5-32d3337032be
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 097b7e93a82b8f1cc20767c57788eebe8162729a
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="create-and-test-a-classifier-user-defined-function"></a>Erstellen und Testen einer benutzerdefinierten Klassifizierungsfunktion
  In diesem Thema wird das Erstellen und Testen einer benutzerdefinierten Klassifizierungsfunktion (User-Defined Function, UDF) erläutert. Die Schritte umfassen das Ausführen von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] -Abfrage-Editor.  
  
 Das in der folgenden Prozedur dargestellte Beispiel veranschaulicht die Möglichkeiten zum Erstellen einer recht komplexen benutzerdefinierten Klassifizierungsfunktion.  
  
 In unserem Beispiel gilt Folgendes:  
  
-   Ein Ressourcenpool (pProductionProcessing) und eine Arbeitsauslastungsgruppe (gProductionProcessing) werden zur Produktionsverarbeitung während eines angegebenen Zeitbereichs erstellt.  
  
-   Ein Ressourcenpool (pOffHoursProcessing) und eine Arbeitsauslastungsgruppe (gOffHoursProcessing) werden für das Verwalten von Verbindungen erstellt, die die Anforderungen für die Produktionsverarbeitung nicht erfüllen.  
  
-   In der Masterdatenbank wird eine Tabelle (TblClassificationTimeTable) erstellt, in der die Start- und Endzeiten gespeichert werden, die bezüglich eines Anmeldungszeitraums ausgewertet werden können. Diese Tabelle muss in der Masterdatenbank erstellt werden, da die Ressourcenkontrolle die Schemabindung für Klassifizierungsfunktionen verwendet.  
  
    > [!NOTE]  
    >  Als Vorgehensweise wird empfohlen, in der Masterdatenbank keine großen, häufig aktualisierten Tabellen zu speichern.  
  
 Die Klassifizierungsfunktion verlängert die Anmeldezeit. Eine übermäßig komplexe Funktion kann zu einem Timeout bei Anmeldungen oder zur Verlangsamung schneller Verbindungen führen.  
  
### <a name="to-create-the-classifier-user-defined-function"></a>So erstellen Sie die benutzerdefinierte Klassifizierungsfunktion  
  
1.  Erstellen und konfigurieren Sie die neuen Ressourcenpools und Arbeitsauslastungsgruppen. Weisen Sie jeder Arbeitsauslastungsgruppe den entsprechenden Ressourcenpool zu.  
  
    ```  
    --- Create a resource pool for production processing  
    --- and set limits.  
    USE master  
    GO  
    CREATE RESOURCE POOL pProductionProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 100,  
         MIN_CPU_PERCENT = 50  
    )  
    GO  
    --- Create a workload group for production processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gProductionProcessing  
    WITH  
    (  
         IMPORTANCE = MEDIUM  
    )  
    --- Assign the workload group to the production processing  
    --- resource pool.  
    USING pProductionProcessing  
    GO  
    --- Create a resource pool for off-hours processing  
    --- and set limits.  
  
    CREATE RESOURCE POOL pOffHoursProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 50,  
         MIN_CPU_PERCENT = 0  
    )  
    GO  
    --- Create a workload group for off-hours processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gOffHoursProcessing  
    WITH  
    (  
         IMPORTANCE = LOW  
    )  
    --- Assign the workload group to the off-hours processing  
    --- resource pool.  
    USING pOffHoursProcessing  
    GO  
    ```  
  
2.  Aktualisieren Sie die Konfiguration im Arbeitsspeicher.  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
    ```  
  
3.  Erstellen Sie eine Tabelle, und definieren Sie die Start- und Endzeiten für den Zeitbereich der Produktionsverarbeitung.  
  
    ```  
    USE master  
    GO  
    CREATE TABLE tblClassificationTimeTable  
    (  
         strGroupName     sysname          not null,  
         tStartTime       time              not null,  
         tEndTime         time              not null  
    )  
    GO  
    --- Add time values that the classifier will use to  
    --- determine the workload group for a session.  
    INSERT into tblClassificationTimeTable VALUES('gProductionProcessing', '6:35 AM', '6:15 PM')  
    go  
    ```  
  
4.  Erstellen Sie die Klassifizierungsfunktion, die Zeitfunktionen und -werte verwendet, die bezüglich der Zeiten in der Suchtabelle ausgewertet werden können. Informationen zum Verwenden von Nachschlagetabellen in einer Klassifizierungsfunktion finden Sie unter "Best Practices für die Verwendung von Nachschlagetabellen in Klassifizierungsfunktionen" in diesem Thema.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] wurde ein erweiterter Satz von Datums- und Uhrzeitdatentypen und zugehörigen Funktionen eingeführt. Weitere Informationen finden Sie unter [Datums- und Uhrzeitdatentypen und zugehörige Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
    ```  
    CREATE FUNCTION fnTimeClassifier()  
    RETURNS sysname  
    WITH SCHEMABINDING  
    AS  
    BEGIN  
         DECLARE @strGroup sysname  
         DECLARE @loginTime time  
         SET @loginTime = CONVERT(time,GETDATE())  
         SELECT TOP 1 @strGroup = strGroupName  
              FROM dbo.tblClassificationTimeTable  
              WHERE tStartTime <= @loginTime and tEndTime >= @loginTime  
         IF(@strGroup is not null)  
         BEGIN  
              RETURN @strGroup  
         END  
    --- Use the default workload group if there is no match  
    --- on the lookup.  
         RETURN N'gOffHoursProcessing'  
    END  
    GO  
    ```  
  
5.  Registrieren Sie die Klassifizierungsfunktion, und aktualisieren Sie die Konfiguration im Arbeitsspeicher.  
  
    ```  
    ALTER RESOURCE GOVERNOR with (CLASSIFIER_FUNCTION = dbo.fnTimeClassifier)  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
    ```  
  
### <a name="to-verify-the-resource-pools-workload-groups-and-the-classifier-user-defined-function"></a>So überprüfen Sie die Ressourcenpools, die Arbeitsauslastungsgruppen und die benutzerdefinierte Klassifizierungsfunktion  
  
1.  Ermitteln Sie die Konfiguration von Ressourcenpools und Arbeitsauslastungsgruppen mit der folgenden Abfrage.  
  
    ```  
    USE master  
    SELECT * FROM sys.resource_governor_resource_pools  
    SELECT * FROM sys.resource_governor_workload_groups  
    GO  
    ```  
  
2.  Stellen Sie unter Verwendung der folgenden Abfragen sicher, dass die Klassifizierungsfunktion vorhanden und aktiviert ist.  
  
    ```  
    --- Get the classifier function Id and state (enabled).  
    SELECT * FROM sys.resource_governor_configuration  
    GO  
    --- Get the classifer function name and the name of the schema  
    --- that it is bound to.  
    SELECT   
          object_schema_name(classifier_function_id) AS [schema_name],  
          object_name(classifier_function_id) AS [function_name]  
    FROM sys.dm_resource_governor_configuration  
  
    ```  
  
3.  Rufen Sie mit der folgenden Abfrage die aktuellen Laufzeitdaten für die Ressourcenpools und Arbeitsauslastungsgruppen ab.  
  
    ```  
    SELECT * FROM sys.dm_resource_governor_resource_pools  
    SELECT * FROM sys.dm_resource_governor_workload_groups  
    GO  
    ```  
  
4.  Ermitteln Sie mit der folgenden Abfrage, welche Sitzungen in jeder Gruppe vorhanden sind.  
  
    ```  
    SELECT s.group_id, CAST(g.name as nvarchar(20)), s.session_id, s.login_time, CAST(s.host_name as nvarchar(20)), CAST(s.program_name AS nvarchar(20))  
              FROM sys.dm_exec_sessions s  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
              ON g.group_id = s.group_id  
    ORDER BY g.name  
    GO  
    ```  
  
5.  Ermitteln Sie mit der folgenden Abfrage, welche Anforderungen in jeder Gruppe vorhanden sind.  
  
    ```  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, r.start_time, r.command, r.sql_handle, t.text   
               FROM sys.dm_exec_requests r  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
                ON g.group_id = r.group_id  
         CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name  
    GO  
    ```  
  
6.  Ermitteln Sie mit der folgenden Abfrage, welche Anforderungen in der Klassifizierung ausgeführt werden.  
  
    ```  
    SELECT s.group_id, g.name, s.session_id, s.login_time, s.host_name, s.program_name   
               FROM sys.dm_exec_sessions s  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
               ON g.group_id = s.group_id  
                     AND 'preconnect' = s.status  
    ORDER BY g.name  
    GO  
  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, r.start_time, r.command, r.sql_handle, t.text   
               FROM sys.dm_exec_requests r  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
               ON g.group_id = r.group_id  
                     AND 'preconnect' = r.status  
         CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name  
    GO  
    ```  
  
### <a name="best-practices-for-using-lookup-tables-in-a-classifier-function"></a>Best Practices für die Verwendung von Nachschlagetabellen in Klassifizierungsfunktionen  
  
1.  Verwenden Sie Nachschlagetabellen nur, wenn es unbedingt notwendig ist. Wenn Sie eine Nachschlagetabelle verwenden müssen, kann diese in die Funktion selbst hartcodiert werden. Dies muss jedoch unter Berücksichtigung der Komplexität und der dynamischen Änderungen der Klassifizierungsfunktion geschehen.  
  
2.  Begrenzen Sie die E/A, die für Nachschlagetabellen ausgeführt wird.  
  
    1.  Verwenden Sie TOP 1, um nur eine Zeile zurückzugeben.  
  
    2.  Minimieren Sie die Anzahl der Zeilen in der Tabelle.  
  
    3.  Stellen Sie sicher, dass alle Zeilen der Tabelle auf einer einzigen oder einer kleinen Anzahl von Seiten vorliegen.  
  
    4.  Stellen Sie sicher, dass Zeilen, die mithilfe von Index Seek-Vorgängen gefunden werden, so viele Suchspalten wie möglich verwenden.  
  
    5.  Denormalisieren Sie auf eine einzige Tabelle, wenn Sie die Verwendung mehrerer Tabellen mit Joins erwägen.  
  
3.  Verhindern Sie ein Blockieren der Nachschlagetabelle.  
  
    1.  Verwenden Sie den Hinweis `NOLOCK` , um Blockierungen zu verhindern, oder verwenden Sie in der Funktion die Option `SET LOCK_TIMEOUT` mit einem Maximalwert von 1000 Millisekunden.  
  
    2.  Die Tabelle(n) muss bzw. müssen in der Masterdatenbank vorhanden sein. (Die Masterdatenbank ist die einzige Datenbank, die mit Sicherheit wiederhergestellt wird, wenn die Clientcomputer versuchen, eine Verbindung herzustellen.)  
  
    3.  Der Tabellenname muss mit dem Schema stets vollqualifiziert werden. Da es sich um die Masterdatenbank handeln muss, ist kein Datenbankname erforderlich.  
  
    4.  Keine Trigger für die Tabelle.  
  
    5.  Wenn Sie die Tabelleninhalte aktualisieren, stellen Sie sicher, dass eine Momentaufnahme-Isolationsstufentransaktion verwendet wird, um das Blockieren von Lesern (Readers) durch einen Schreiber (Writer) zu verhindern. Beachten Sie, dass die Verwendung des Hinweises `NOLOCK` dies ebenfalls verhindern kann.  
  
    6.  Deaktivieren Sie beim Ändern der Tabelleninhalte die Klassifizierungsfunktion, wenn möglich.  
  
        > [!WARNING]  
        >  Es wird dringend empfohlen, diese Best Practices zu befolgen. Wenn Sie die Best Practices aufgrund von Problemen nicht befolgen können, wenden Sie sich an den Microsoft Support, um zukünftigen Problemen vorzubeugen.  
  
## <a name="see-also"></a>Siehe auch  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Aktivieren der Ressourcenkontrolle](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Arbeitsauslastungsgruppe der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Konfigurieren der Ressourcenkontrolle mit einer Vorlage](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Anzeigen der Eigenschaften der Ressourcenkontrolle](../../relational-databases/resource-governor/view-resource-governor-properties.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
