---
title: "&#196;ndern von Daten in einer temporalen Tabelle mit Systemversionsverwaltung | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/28/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5f398470-c531-47b5-84d5-7c67c27df6e5
caps.latest.revision: 8
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 8
---
# &#196;ndern von Daten in einer temporalen Tabelle mit Systemversionsverwaltung
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Daten in temporalen Tabellen mit Systemversionsverwaltung werden mithilfe von regulären DML-Anweisungen geändert, mit einem wichtigen Unterschied: Zeitraumspaltendaten können nicht direkt geändert werden. Wenn die Daten aktualisiert werden, werden sie mit einer Versionsangabe versehen, die vorherige Version jeder aktualisierten Zeile wird in die Verlaufstabelle eingefügt. Wenn Daten gelöscht werden, ist der Löschvorgang logisch, die Zeile wird aus der aktuellen Tabelle in die Verlaufstabelle verschoben und nicht endgültig gelöscht.  
  
## Einfügen von Daten  
 Wenn Sie neue Daten einfügen, müssen Sie die **PERIOD**-Spalten bedenken falls sie nicht **HIDDEN** sind. Bei temporalen Tabellen mit Systemversionsverwaltung können Sie auch Partitionsaustausch verwenden.  
  
### Einfügen von neuen Daten mit sichtbaren Zeitraumspalten  
 Sie können wie folgt Ihre **INSERT**-Anweisung erstellen, wenn Sie über sichtbare **PERIOD**-Spalten verfügen, um die neuen **PERIOD**-Spalten zu berücksichtigen:  
  
-   Falls Sie die Spaltenliste in Ihrer **INSERT**-Anweisung angeben, können Sie die **PERIOD**-Spalten auslassen, da das System automatisch Werte für jede dieser Spalten erstellen wird.  
  
    ```  
    --Insert with column list and without period columns   
    INSERT INTO [dbo].[Department] ([DeptID] ,[DeptName] ,[ManagerID] ,[ParentDeptID])   
    VALUES(10, 'Marketing', 101, 1);  
  
    ```  
  
-   Falls Sie die **PERIOD**-Spalten in der Spaltenliste in Ihrer **INSERT**-Anweisung angeben, müssen Sie **DEFAULT** als ihren Wert angeben.  
  
    ```  
    INSERT INTO [dbo].[Department] ([DeptID] ,[DeptName] ,[ManagerID] ,[ParentDeptID], SysStartTime, SysEndTime)   
    VALUES(11, 'Sales', 101, 1, default, default);  
  
    ```  
  
-   Falls Sie die Spaltenliste in Ihrer **INSERT**-Anweisung nicht angeben, geben Sie **DEFAULT** für **PERIOD**-Spalten an.  
  
    ```  
    --Insert without  column list and DEFAULT values for period columns   
    INSERT INTO [dbo].[Department]    
    VALUES(12, 'Production', 101, 1, default, default);  
  
    ```  
  
### Einfügen von Daten in eine Tabelle mit ausgeblendeten Zeitraumspalten  
 Falls **PERIOD**-Spalten als versteckt (HIDDEN) spezifiziert sind, dann müssen Sie, wenn Sie INSERT verwenden, nur die Werte für die sichtbaren Spalten angeben, ohne Angabe der Spaltenliste. Es ist nicht erforderlich, dass Sie die neuen **PERIOD**-Spalten in Ihrer **INSERT**-Anweisung bedenken. Dieses Verhalten garantiert, dass Ihre älteren Anwendungen weiterhin funktionieren, wenn Sie die Systemversionsverwaltung für die Tabellen aktivieren, die von der Versionsverwaltung profitieren.  
  
```  
CREATE TABLE [dbo].[CompanyLocation]  
(   
     [LocID] [int] IDENTITY(1,1) NOT NULL PRIMARY KEY  
   , [LocName] [varchar](50) NOT NULL  
   , [City] [varchar](50) NOT NULL  
   , [SysStartTime] [datetime2](0) GENERATED ALWAYS AS ROW START HIDDEN NOT NULL   
   , [SysEndTime] [datetime2](0) GENERATED ALWAYS AS ROW END HIDDEN NOT NULL   
PERIOD FOR SYSTEM_TIME ([SysStartTime], [SysEndTime])   
)    
WITH ( SYSTEM_VERSIONING = ON );   
GO   
INSERT INTO [dbo].[CompanyLocation]   
VALUES  ('Headquarters', 'New York');  
  
```  
  
### Einfügen von Daten mithilfe des Partitionsaustauschs  
 Falls die aktuelle Tabelle partitioniert ist, können Sie den Partitionsaustausch als effizienten Mechanismus zum Laden von Daten in eine leere Partition oder zum parallelen Laden in mehrere Partitionen verwenden.   
Für die Stagingtabelle, die in der **PARTITION SWITCH IN**-Anweisung mit einer temporalen Tabelle mit Systemversionsverwaltung verwendet wird, muss **SYSTEM_TIME PERIOD** definiert sein, aber es muss sich nicht um eine temporale Tabelle mit Systemversionsverwaltung handeln.    
Das stellt sicher, dass temporale Konsistenzprüfungen während der Dateneinfügung in eine Stagingtabelle durchgeführt werden, oder wenn SYSTEM_TIME-Zeitraum einer im Voraus ausgefüllten Stagingtabelle hinzugefügt wird.  
  
```  
/*Create staging table with period definition for SWITCH IN temporal table*/   
CREATE TABLE [dbo].[Staging_Department_Partition2]  
(   
     [DeptID] [int] NOT NULL  
   , [DeptName] [varchar](50)  NOT NULL  
   , [ManagerID] [int] NULL  
   , [ParentDeptID] [int] NULL  
   , [SysStartTime] [datetime2](7) GENERATED ALWAYS AS ROW START NOT NULL  
   , [SysEndTime] [datetime2](7) GENERATED ALWAYS AS ROW END NOT NULL  
   , PERIOD FOR SYSTEM_TIME ( [SysStartTime], [SysEndTime] )   
) ON [PRIMARY]   
  
/*Create aligned primary key*/   
ALTER TABLE [dbo].[Staging_Department_Partition2]    
ADD CONSTRAINT [Staging_Department_Partition2_PK]  
   PRIMARY KEY CLUSTERED  
   (  [DeptID] ASC )     
   ON [PRIMARY]   
  
/*   
Create and enforce constraints for partition boundaries.   
Partition 2 contains rows with DeptID > 100 and DeptID <=200   
*/   
ALTER TABLE [dbo].[Staging_Department_Partition2]      
   WITH CHECK ADD  CONSTRAINT [chk_staging_Department_partition_2]     
   CHECK  ([DeptID]>N'100' AND [DeptID]<=N'200')   
ALTER TABLE [dbo].[Staging_Department_Partition2]    
   CHECK CONSTRAINT [chk_staging_Department_partition_2]   
  
/*Load data into staging table*/   
INSERT INTO [dbo].[staging_Department] ([DeptID],[DeptName],[ManagerID],[ParentDeptID])   
VALUES (101,'D101',1,NULL)  
  
/*Use PARTITION SWITCH IN to efficiently add data to current table */    
ALTER TABLE [Staging_Department]    
SWITCH TO [dbo].[Department] PARTITION 2;  
  
```  
  
 Falls Sie versuchen, einen Partitionsaustausch (PARTITION SWITCH) aus einer Tabelle ohne Zeitraumdefinitionen auszuführen, erhalten Sie eine Fehlermeldung: `Msg 13577, Level 16, State 1, Line 25    ALTER TABLE SWITCH statement failed on table 'MyDB.dbo.Staging_Department_2015_09_26' because target table has SYSTEM_TIME PERIOD while source table does not have it.`  
  
## Aktualisieren von Daten  
 Sie aktualisieren Daten in der aktuellen Tabelle mit einer regulären **UPDATE**-Anweisung. Im Notfall können Sie die Daten in der aktuellen Tabelle auch mithilfe der Verlaufstabelle aktualisieren. Sie können jedoch **PERIOD**-Spalten nicht aktualisieren, und Sie können die Daten in der Verlaufstabelle nicht direkt aktualisieren während **SYSTEM_VERSIONING = ON** gilt.   
Legen Sie **SYSTEM_VERSIONING = OFF** fest, und aktualisieren Sie Zeilen aus der aktuellen Tabelle und der Verlaufstabelle, aber beachten Sie dabei, dass das System bei dieser Vorgehensweise keinen Änderungsverlauf beibehält.  
  
### Aktualisieren der aktuellen Tabelle  
 In diesem Beispiel wird die Spalte ManagerID für jede Zeile aktualisiert, in denen die DeptID = 10. Auf die **PERIOD**-Spalten wird in keiner Weise verwiesen.  
  
```  
UPDATE [dbo].[Department] SET [ManagerID] = 501 WHERE [DeptID] = 10  
```  
  
 Sie können jedoch keine **PERIOD**-Spalte aktualisieren und Sie können die Verlaufstabelle nicht aktualisieren.  In diesem Beispiel schlägt der Versuch, eine **PERIOD**-Spalte zu aktualisieren, fehl.  
  
```  
UPDATE [dbo].[Department]    
SET SysStartTime = '2015-09-23 23:48:31.2990175'    
WHERE DeptID = 10 ;  
  
Msg 13537, Level 16, State 1, Line 3   
Cannot update GENERATED ALWAYS columns in table 'TmpDev.dbo.Department'.  
  
```  
  
### Aktualisieren der aktuellen Tabelle aus der Verlaufstabelle  
 Sie können **UPDATE** für die aktuelle Tabelle verwenden, um den tatsächlichen Zeilenzustand auf einen gültigen Zustand zu einem bestimmten Zeitpunkt in der Vergangenheit wieder herzustellen („Wiederherstellen einer letzten bekannten guten Zeilenversion“). In diesem Beispiel wird gezeigt, wie zu den Werten in der Verlaufstabelle zum 25.4.2015 zurückgekehrt wird, wo DeptID = 10.  
  
```  
UPDATE Department   
SET DeptName = History.DeptName   
FROM Department    
FOR SYSTEM_TIME AS OF '2015-04-25' AS History   
WHERE History.DeptID  = 10   
AND Department.DeptID = 10 ;  
  
```  
  
## Löschen von Daten  
 Sie löschen Daten in der aktuellen Tabelle mit einer regulären **DELETE**-Anweisung. Die Endzeitraums-Spalte für gelöschte Zeilen wird mit der Anfangszeit der zugrundeliegenden Transaktion aufgefüllt.   
Sie können keine Zeilen direkt aus der Verlaufstabelle löschen während **SYSTEM_VERSIONING = ON** gilt.   
Legen Sie **SYSTEM_VERSIONING = OFF** fest, und löschen Sie Zeilen aus der aktuellen Tabelle und der Verlaufstabelle, aber beachten Sie dabei, dass das System bei dieser Vorgehensweise keinen Änderungsverlauf beibehält.   
**TRUNCATE**, **SWITCH PARTITION OUT** der aktuellen Tabelle und **SWITCH PARTITION IN**-Verlaufstabelle werden nicht unterstützt während **SYSTEM_VERSIONING = ON** gilt.  
  
## Verwenden von MERGE zum Ändern von Daten in der temporalen Tabelle  
 **MERGE**-Vorgang wird mit den gleichen Einschränkungen unterstützt, die **INSERT**- und **UPDATE**-Anweisungen in Hinblick auf **PERIOD**-Spalten haben.  
  
```  
CREATE TABLE DepartmentStaging (DeptId INT, DeptName varchar(50));   
GO   
INSERT INTO DepartmentStaging VALUES (1, 'Company Management');   
INSERT INTO DepartmentStaging VALUES (10, 'Science & Research');   
INSERT INTO DepartmentStaging VALUES (15, 'Process Management');   
  
MERGE dbo.Department AS target   
USING (SELECT DeptId, DeptName FROM DepartmentStaging) AS source (DeptId, DeptName)   
ON (target.DeptId = source.DeptId)   
WHEN MATCHED THEN    
    UPDATE   
   SET DeptName = source.DeptName   
WHEN NOT MATCHED THEN   
   INSERT (DeptName)   
   VALUES (source.DeptName);  
  
```  
  
## Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Modifying%20Data%20in%20a%20System-Versioned%20Temporal%20Table%20page).  
  
## Siehe auch  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erstellen einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Abfragen von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Ändern vom Schema einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [Beenden der Versionsverwaltung auf einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  