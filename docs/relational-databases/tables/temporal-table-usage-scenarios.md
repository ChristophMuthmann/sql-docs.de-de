---
title: "Verwendungsszenarios für temporale Tabellen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b8fa2dd-1790-4289-8362-f11e6d63bb09
caps.latest.revision: "11"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 881cdb2e9fc9d7faf8423574efa944c4149ded22
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="temporal-table-usage-scenarios"></a>Verwendungsszenarien für temporale Tabellen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Temporale Tabellen sind im Allgemeinen in Szenarien nützlich, in denen der Verlauf von Datenänderungen nachverfolgt werden muss.    
Für maßgebliche Produktivitätsvorteile wird empfohlen, temporale Tabellen in den folgenden Fällen zu verwenden.  
  
## <a name="data-audit"></a>Datenüberwachung  
 Verwenden Sie die temporale Systemversionsverwaltung für Tabellen, in denen wichtige Informationen gespeichert werden, für die Sie nachverfolgen müssen, was sich wann geändert hat, und um Datenforensik zu einem beliebigen Zeitpunkt durchzuführen.    
Temporale Tabellen mit Systemversionsverwaltung ermöglichen es Ihnen, Datenüberwachungsszenarien in den frühen Phasen des Entwicklungszyklus zu planen oder vorhandenen Anwendungen oder Lösungen bei Bedarf eine Datenüberwachung hinzuzufügen.  
  
 Das folgende Diagramm zeigt ein Szenario mit einer Mitarbeitertabelle (Employee) mit dem Datenbeispiel, einschließlich der Versionen für Zeilen mit aktuellen Daten (blau markiert) und mit Verlaufsdaten (grau markiert).   
Der rechte Bereich des Diagramms stellt die Zeilenversionen auf einer Zeitachse dar, und zeigt, welche Zeilen Sie mit verschiedenen Abfragetypen für die temporale Tabelle mit oder ohne SYSTEM_TIME-Klausel auswählen.  
  
 ![TemporalUsageScenario1](../../relational-databases/tables/media/temporalusagescenario1.png "TemporalUsageScenario1")  
  
### <a name="enabling-system-versioning-on-a-new-table-for-data-audit"></a>Aktivieren der Systemversionsverwaltung für eine neue Tabelle zur Datenüberwachung  
 Wenn Sie Informationen angegeben haben, für die eine Datenüberwachung durchgeführt werden soll, erstellen Sie die Datenbanktabellen als temporal mit Systemversionsverwaltung. Das folgende einfache Beispiel veranschaulicht ein Szenario mit Mitarbeiterinformationen in einer hypothetischen Personaldatenbank:  
  
```  
CREATE TABLE Employee   
(    
  [EmployeeID] int NOT NULL PRIMARY KEY CLUSTERED   
  , [Name] nvarchar(100) NOT NULL  
  , [Position] varchar(100) NOT NULL   
  , [Department] varchar(100) NOT NULL  
  , [Address] nvarchar(1024) NOT NULL  
  , [AnnualSalary] decimal (10,2) NOT NULL  
  , [ValidFrom] datetime2 (2) GENERATED ALWAYS AS ROW START  
  , [ValidTo] datetime2 (2) GENERATED ALWAYS AS ROW END  
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)  
 )    
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));  
```  
  
 Verschiedene Optionen zum Erstellen von temporalen Tabellen mit Systemversionsverwaltung werden unter [Erstellen einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)beschrieben.  
  
### <a name="enabling-system-versioning-on-an-existing-table-for-data-audit"></a>Aktivieren der Systemversionsverwaltung für eine vorhandene Tabelle zur Datenüberwachung  
 Wenn Sie in vorhandenen Datenbanken eine Datenüberwachung durchführen müssen, verwenden Sie ALTER TABLE, um nicht temporale Tabellen mit der Systemversionsverwaltung zu erweitern. Um zu vermeiden, dass Änderungen in Ihrer Anwendung unterbrochen werden, fügen Sie Zeitraumspalten als verborgen (HIDDEN) hinzu, wie unter [Alter Non-Temporal Table to be System-Versioned Temporal Table](https://msdn.microsoft.com/library/mt590957.aspx#Anchor_3)(Ändern von nicht temporalen Tabelle in eine temporale Tabelle mit Systemversionsverwaltung) beschrieben. Das folgende Beispiel veranschaulicht die Aktivierung der Systemversionsverwaltung für eine vorhandene Mitarbeitertabelle in einer hypothetischen Personaldatenbank:  
  
```  
/*   
Turn ON system versioning in Employee table in two steps   
(1) add new period columns (HIDDEN)   
(2) create default history table   
*/   
ALTER TABLE Employee   
ADD   
    ValidFrom datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DF_ValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , ValidTo datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo);   
  
ALTER TABLE Employee    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Employee_History));  
```  
  
 Nach dem Ausführen des obigen Skripts, werden alle Datenänderungen transparent in der Verlaufstabelle gesammelt.    
In einem typischen Szenario für die Datenüberwachung fragen Sie alle Datenänderungen ab, die innerhalb eines gewünschten Zeitraums auf eine einzelne Zeile angewendet wurden. Die Standardverlaufstabelle wird mit gruppiertem B-Struktur-Zeilenspeicher erstellt, um diesen Anwendungsfall effizient zu bearbeiten.  
  
### <a name="performing-data-analysis"></a>Durchführen der Datenanalyse  
 Nach dem Aktivieren der Systemversionsverwaltung mithilfe einem der oben genannten Ansätze, ist die Datenüberwachung nur eine Abfrage entfernt. Die folgende Abfrage sucht nach Zeilenversionen für den Mitarbeiterdatensatz mit EmployeeID = 1000, die mindestens eine Zeit lang zwischen dem 1. Januar 2014 und dem 1. Januar 2015 (einschließlich der oberen Grenze) aktiv waren:  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME    
        BETWEEN '2014-01-01 00:00:00.0000000' AND '2015-01-01 00:00:00.0000000'   
            WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 Ersetzen Sie FOR SYSTEM_TIME BETWEEN...AND durch FOR SYSTEM_TIME ALL, um den gesamten Verlauf der Datenänderungen für diesen bestimmten Mitarbeiter zu analysieren:  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME ALL WHERE    
        EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 Verwenden Sie zum Suchen von Zeilenversionen, die nur innerhalb eines Zeitraums (und nicht außerhalb davon) aktiv waren, die Anweisung CONTAINED IN. Diese Abfrage ist sehr effizient, da sie nur die Verlaufstabelle abfragt:  
  
```  
SELECT * FROM Employee FOR SYSTEM_TIME    
    CONTAINED IN ('2014-01-01 00:00:00.0000000', '2015-01-01 00:00:00.0000000')   
        WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 In einigen Überwachungsszenarien möchten Sie schließlich herausfinden, wie die gesamte Tabelle zu einem beliebigen Punkt in der Vergangenheit aussah:  
  
```  
SELECT * FROM Employee FOR SYSTEM_TIME AS OF '2014-01-01 00:00:00.0000000' ;  
```  
  
 Temporale Tabellen mit Systemversionsverwaltung speichern Werte für Zeitraumspalten in der UTC-Zeitzone, es ist jedoch immer besser, beim Filtern von Daten und Anzeigen von Ergebnissen mit der lokalen Zeitzone zu arbeiten. Im folgenden Codebeispiel wird gezeigt, wie Sie Filterbedingungen anwenden, die ursprünglich in der lokalen Zeitzone angegeben wurden und dann mit AT TIME ZONE in UTC konvertiert wurden. Dies wurde in SQL Server 2016 eingeführt:  
  
```  
/*Add offset of the local time zone to current time*/  
DECLARE @asOf DATETIMEOFFSET = GETDATE() AT TIME ZONE 'Pacific Standard Time'  
/*Convert AS OF filter to UTC*/  
SET @asOf = DATEADD (MONTH, -9, @asOf) AT TIME ZONE 'UTC';  
  
SELECT   
    EmployeeID  
    , Name  
    , Position  
    , Department  
    , [Address]  
    , [AnnualSalary]  
    , ValidFrom AT TIME ZONE 'Pacific Standard Time' AS ValidFromPT   
    , ValidTo AT TIME ZONE 'Pacific Standard Time' AS ValidToPT  
FROM Employee   
    FOR SYSTEM_TIME AS OF @asOf where EmployeeId = 1000  
  
```  
  
 AT TIME ZONE ist in allen anderen Szenarien hilfreich, in denen Tabellen mit Systemversionsverwaltung verwendet werden.  
  
> [!TIP]  
>  Filterbedingungen, die in temporalen Klauseln mit FOR SYSTEM_TIME angegeben werden, sind SARG-fähig (SQL Server kann den zugrunde liegenden gruppierten Index verwenden, um einen Suchvorgang statt eines Scanvorgangs auszuführen.   
> Wenn Sie die Verlaufstabelle direkt abfragen, stellen Sie sicher, dass die Filterbedingung ebenfalls SARG-fähig ist, indem Sie Filter in Form von \<Zeitraumspalte  {< | > | =, …} festlegen date_condition AT TIME ZONE 'UTC' angeben.  
> Wenn Sie AT TIME ZONE auf Zeitraumspalten anwenden, führt SQL Server einen Tabellen-/Indexscanvorgang durch, der sehr teuer sein kann. Vermeiden Sie folgenden Bedingungstyp in Ihren Abfragen:  
> \<Zeitraumspalte>  AT ZEIT ZONE ‘\<Ihre Zeitzone>’  >  {< | > | =, …} date_condition.  
  
 Weitere Informationen finden Sie unter [Abfragen von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md).  
  
## <a name="point-in-time-analysis-time-travel"></a>Zeitpunktanalyse (Zeitreise)  
 Im Gegensatz zur Datenüberwachung, bei der der Schwerpunkt in der Regel auf Änderungen liegt, die an einem einzelnen Datensatz vorgenommen wurden, möchten Benutzer in Zeitreiseszenarien sehen, wie sich der gesamte Dataset im Verlauf der Zeit geändert hat. Zeitreisen umfassen gelegentlich mehrere verknüpfte temporale Tabellen, die sich alle in unterschiedlichem Tempo ändern, die Sie analysieren möchten:  
  
-   Trends für wichtige Indikatoren in den Verlaufsdaten und aktuellen Daten  
  
-   Exakte Momentaufnahme der gesamten Daten „ab“ (as of) einem beliebigen Zeitpunkt in der Vergangenheit (gestern, vor einem Monat usw.)  
  
-   Unterschiede zwischen zwei interessanten Zeitpunkten (z. B. vor einem Monat im Vergleich zu vor drei Monaten)  
  
 Es gibt viele reale Szenarien, in denen eine Zeitreiseanalyse erforderlich ist. Um dieses Verwendungsszenario zu veranschaulichen, sehen Sie sich OLTP mit einem automatisch generierten Verlauf an.  
  
### <a name="oltp-with-auto-generated-data-history"></a>OLTP mit automatisch generiertem Datenverlauf  
 In Transaktionsverarbeitungssystemen ist es nicht ungewöhnlich, die Änderung von wichtigen Metriken im Verlauf der Zeit zu analysieren. Die Analyse des Verlaufs sollte idealerweise nicht die Leistung der OLTP-Anwendung beeinträchtigen, bei der der Zugriff auf den aktuellen Zustand der Daten mit minimaler Wartezeit und Datensperre erfolgen muss.  Temporale Tabellen mit Systemversionsverwaltung wurden so konzipiert, dass Benutzer den vollständigen Änderungsverlauf für eine spätere Analyse getrennt von den aktuellen Daten transparent behalten können, und das bei minimalen Auswirkungen auf die OLTP-Hauptarbeitsauslastung.  
Bei hohen Transaktionsverarbeitungsarbeitsauslastungen empfehlen wir die Verwendung von [temporalen Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md), sodass Sie aktuelle Daten und den vollständigen Änderungsverlauf auf dem Datenträger auf kostengünstige Weise speichern können.  
  
 Für die Verlaufstabelle empfehlen wir aus den folgenden Gründen die Verwendung eines gruppierten Columnstore-Indexes:  
  
-   Die typische Trendanalyse profitiert von der Abfrageleistung, die von einem gruppierten Columnstore-Index bereitgestellt wird.  
  
-   Die Datenleerungsaufgabe mit speicheroptimierten Tabellen funktioniert am besten bei hoher OLTP-Arbeitsauslastung, wenn die Verlaufstabelle über einen gruppierten Columnstore-Index verfügt.  
  
-   Ein gruppierter Columnstore-Index bietet eine hervorragende Komprimierung, besonders in Szenarien, in denen nicht alle Spalten gleichzeitig geändert werden.  
  
 Bei temporalen Tabellen mit In-Memory OLTP ist es weniger notwendig, den gesamten Dataset im Arbeitsspeicher zu behalten. Zudem haben Sie die Möglichkeit, mühelos zwischen heißen und kalten Daten zu unterscheiden.  
Beispiele für reale Szenarien, die gut in diese Kategorie passen, sind u. a. die Bestandsverwaltung oder der Devisenhandel.  
  
 Das folgende Diagramm zeigt ein vereinfachtes Datenmodell für die Bestandsverwaltung:  
  
 ![TemporalUsageInMemory](../../relational-databases/tables/media/temporalusageinmemory.png "TemporalUsageInMemory")  
  
 Das folgende Codebeispiel erstellt ProductInventory als eine temporale In-Memory-Tabelle mit Systemversionsverwaltung und mit einem gruppierten Columnstore-Index für die Verlaufstabelle (der tatsächlich den standardmäßig erstellten Zeilenspeicherindex ersetzt):  
  
> [!NOTE]  
>  Stellen Sie sicher, dass die Datenbank die Erstellung von speicheroptimierten Tabellen ermöglicht. Weitere Informationen finden Sie unter [Erstellen einer speicheroptimierten Tabelle und einer systemintern kompilierten gespeicherten Prozedur](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
```  
USE TemporalProductInventory  
GO  
  
BEGIN  
    --If table is system-versioned, SYSTEM_VERSIONING must be set to OFF first   
    IF ((SELECT temporal_type FROM SYS.TABLES WHERE object_id = OBJECT_ID('dbo.ProductInventory', 'U')) = 2)  
    BEGIN  
        ALTER TABLE [dbo].[ProductInventory] SET (SYSTEM_VERSIONING = OFF)  
    END  
    DROP TABLE IF EXISTS [dbo].[ProductInventory]  
       DROP TABLE IF EXISTS [dbo].[ProductInventoryHistory]  
END  
GO  
  
CREATE TABLE [dbo].[ProductInventory]  
(  
    ProductId int NOT NULL,  
    LocationID INT NOT NULL,  
    Quantity int NOT NULL CHECK (Quantity >=0),  
  
    SysStartTime datetime2(0) GENERATED ALWAYS AS ROW START  NOT NULL ,  
    SysEndTime datetime2(0) GENERATED ALWAYS AS ROW END  NOT NULL ,  
    PERIOD FOR SYSTEM_TIME(SysStartTime,SysEndTime),  
  
    --Primary key definition  
    CONSTRAINT PK_ProductInventory PRIMARY KEY NONCLUSTERED (ProductId, LocationId)  
)  
WITH  
(  
    MEMORY_OPTIMIZED=ON,      
    SYSTEM_VERSIONING = ON   
    (          
        HISTORY_TABLE = [dbo].[ProductInventoryHistory],          
        DATA_CONSISTENCY_CHECK = ON  
    )  
)  
  
CREATE CLUSTERED COLUMNSTORE INDEX IX_ProductInventoryHistory ON [ProductInventoryHistory]  
WITH (DROP_EXISTING = ON);  
```  
  
 Für das obige Modell könnte die Prozedur zum Verwalten des Bestands folgendermaßen aussehen:  
  
```  
CREATE PROCEDURE [dbo].[spUpdateInventory]  
@productId int,  
@locationId int,  
@quantityIncrement int  
  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT, LANGUAGE=N'English')  
    UPDATE dbo.ProductInventory  
        SET Quantity = Quantity + @quantityIncrement   
            WHERE ProductId = @productId AND LocationId = @locationId  
  
/*If zero rows were updated than this is insert of the new product for a given location*/  
    IF @@rowcount = 0  
        BEGIN  
            IF @quantityIncrement < 0  
                SET @quantityIncrement = 0  
            INSERT INTO [dbo].[ProductInventory]  
                (  
                    [ProductId]  
                    ,[LocationID]  
                    ,[Quantity]  
                )  
                VALUES  
                   (  
                        @productId  
                       ,@locationId  
                       ,@quantityIncrement  
        END  
END;  
```  
  
 Die gespeicherte Prozedur „spUpdateInventory“ fügt entweder ein neues Produkt im Bestand ein oder aktualisiert die Produktmenge für den jeweiligen Standort. Die Geschäftslogik ist sehr einfach und konzentriert sich auf die Verwaltung des aktuellen Zustands, der dauerhaft akkurat ist, indem der Wert im Mengenfeld durch eine Tabellenaktualisierung erhöht/verringert wird, während Tabellen mit Systemversionsverwaltung den Daten Verlaufsdimensionen transparent hinzufügen, wie im folgenden Diagramm dargestellt.  
  
 ![TemporalUsageInMemory2b](../../relational-databases/tables/media/temporalusageinmemory2b.png "TemporalUsageInMemory2b")  
  
 Die Abfrage des aktuellen Zustands kann effizient aus dem nativ kompilierten Modul durchgeführt werden:  
  
```  
CREATE PROCEDURE [dbo].[spQueryInventoryLatestState]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT, LANGUAGE=N'English')  
    SELECT ProductId, LocationID, Quantity, SysStartTime  
      FROM dbo.ProductInventory  
    ORDER BY ProductId, LocationId  
END;  
GO  
EXEC [dbo].[spQueryInventoryLatestState];  
```  
  
 Die Analyse von Datenänderungen im Verlauf der Zeit wird mit der FOR SYSTEM_TIME ALL-Klausel zum Kinderspiel, wie im folgenden Beispiel gezeigt:  
  
```  
DROP VIEW IF EXISTS vw_GetProductInventoryHistory;  
GO  
CREATE VIEW vw_GetProductInventoryHistory  
AS  
   SELECT ProductId, LocationId, Quantity, SysStartTime, SysEndTime   
   FROM [dbo].[ProductInventory]  
   FOR SYSTEM_TIME ALL;  
GO  
SELECT * FROM vw_GetProductInventoryHistory   
    WHERE ProductId = 2;  
```  
  
 Das folgende Diagramm zeigt den Datenverlauf für ein Produkt, der problemlos durch den Import der obigen Ansicht in Power Query, Power BI oder ähnlichen Business Intelligence-Tools dargestellt werden kann:  
  
 ![ProductHistoryOverTime](../../relational-databases/tables/media/producthistoryovertime.png "ProductHistoryOverTime")  
  
 Temporale Tabellen können in diesem Szenario verwendet werden, um andere Arten von Zeitreiseanalysen durchzuführen, z. B. Rekonstruktion des Bestandszustands ab (AS OF) einem bestimmten Zeitpunkt in der Vergangenheit oder Vergleich von Momentaufnahmen, die sich auf verschiedene Momente beziehen.  
  
 Für dieses Nutzungsszenario können Sie auch die Produkt- und Standorttabellen als temporale Tabellen erweitern, sodass Sie den Änderungsverlauf für UnitPrice und NumberOfEmployee später analysieren können.  
  
```  
ALTER TABLE Product   
ADD   
    SysStartTime datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DF_ValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , SysEndTime datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);   
  
ALTER TABLE Product    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProductHistory));  
  
ALTER TABLE [Location]  
ADD   
    SysStartTime datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DFValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , SysEndTime datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DFValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);  
  
ALTER TABLE [Location]    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.LocationHistory));  
```  
  
 Da das Datenmodell jetzt mehrere temporale Tabellen umfasst, besteht die bewährte Methode für die AS OF-Analyse darin, eine Ansicht zu erstellen, die die erforderlichen Daten aus den verknüpften Tabellen extrahiert, und FOR SYSTEM_TIME AS OF auf die Ansicht anzuwenden, da dies die Rekonstruktion des Zustands des gesamten Datenmodells maßgeblich vereinfacht:  
  
```  
DROP VIEW IF EXISTS vw_ProductInventoryDetails;  
GO  
  
CREATE VIEW vw_ProductInventoryDetails  
AS  
    SELECT PrInv.ProductId ,PrInv.LocationId, P.ProductName, L.LocationName, PrInv.Quantity  
    , P.UnitPrice, L.NumberOfEmployees  
    , P.SysStartTime AS ProductStartTime, P.SysEndTime AS ProductEndTime  
    , L.SysStartTime AS LocationStartTime, L.SysEndTime AS LocationEndTime  
    , PrInv.SysStartTime AS InventoryStartTime, PrInv.SysEndTime AS InventoryEndTime  
FROM dbo.ProductInventory as PrInv  
JOIN dbo.Product AS P ON PrInv.ProductId = P.ProductID  
JOIN dbo.Location AS L ON PrInv.LocationId = L.LocationID;  
GO  
SELECT * FROM vw_ProductInventoryDetails  
    FOR SYSTEM_TIME AS OF '2015.01.01';   
```  
  
 Das folgende Bild zeigt den Ausführungsplan, der für die SELECT-Abfrage generiert wurde. Dies veranschaulicht, dass die gesamte Komplexität im Umgangs mit temporalen Beziehungen vollständig vom SQL Server-Modul übernommen wird:  
  
 ![ASOFExecutionPlan](../../relational-databases/tables/media/asofexecutionplan.png "ASOFExecutionPlan")  
  
 Verwenden Sie den folgenden Code, um den Status des Produktbestands zwischen zwei Zeitpunkten (vor einem Tag und vor einem Monat) zu vergleichen:  
  
```  
DECLARE @dayAgo datetime2 (0) = DATEADD (day, -1, SYSUTCDATETIME());  
DECLARE @monthAgo datetime2 (0) = DATEADD (month, -1, SYSUTCDATETIME());  
  
SELECT   
    inventoryDayAgo.ProductId  
    , inventoryDayAgo.ProductName  
    , inventoryDayAgo.LocationName  
    , inventoryDayAgo.Quantity AS QuantityDayAgo,inventoryMonthAgo.Quantity AS QuantityMonthAgo  
    , inventoryDayAgo.UnitPrice AS UnitPriceDayAgo, inventoryMonthAgo.UnitPrice AS UnitPriceMonthAgo  
FROM vw_ProductInventoryDetails  
FOR SYSTEM_TIME AS OF @dayAgo AS inventoryDayAgo  
JOIN vw_ProductInventoryDetails FOR SYSTEM_TIME AS OF @monthAgo AS inventoryMonthAgo  
    ON inventoryDayAgo.ProductId = inventoryMonthAgo.ProductId AND inventoryDayAgo.LocationId = inventoryMonthAgo.LocationID;  
```  
  
## <a name="anomaly-detection"></a>Erkennung von Anomalien  
 Bei der Erkennung von Anomalien (oder Ausreißererkennung) werden Elemente identifiziert, die einem erwarteten Muster oder anderen Elementen in einem Dataset nicht entsprechen.   
Sie können temporale Tabellen mit Systemversionsverwaltung verwenden, um Anomalien zu erkennen, die in regelmäßigen Abständen oder unregelmäßig auftreten, da Sie mit temporalen Abfragen schnell bestimmte Muster auffinden können.  
Die Form der Anomalie hängt von der Art von Daten ab, die Sie sammeln, sowie von Ihrer Geschäftslogik.  
  
 Das folgende Beispiel zeigt die vereinfachte Logik zum Erkennen von „Spitzen“ in Verkaufszahlen. Angenommen, Sie arbeiten mit einer temporalen Tabelle, die den Verlauf von erworbenen Produkten erfasst:  
  
```  
CREATE TABLE [dbo].[Product]  
                (  
            [ProdID] [int] NOT NULL PRIMARY KEY CLUSTERED  
        , [ProductName] [varchar](100) NOT NULL  
        , [DailySales] INT NOT NULL  
        , [ValidFrom] [datetime2](7) GENERATED ALWAYS AS ROW START NOT NULL  
        , [ValidTo] [datetime2](7) GENERATED ALWAYS AS ROW END NOT NULL  
        , PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])  
    )  
    WITH( SYSTEM_VERSIONING = ON (HISTORY_TABLE = [dbo].[ProductHistory]   
        , DATA_CONSISTENCY_CHECK = ON ))  
  
```  
  
 Das folgende Diagramm zeigt die Verkaufszahlen im Verlauf der Zeit:  
  
 ![TemporalAnomalyDetection](../../relational-databases/tables/media/temporalanomalydetection.png "TemporalAnomalyDetection")  
  
 Angenommen die Anzahl der erworbenen Produkte weist an typischen Tagen kleine Abweichungen auf, so identifiziert die folgende Abfrage Singleton-Ausreißer – Proben, die sich im Vergleich zu ihren unmittelbaren Nachbarn erheblich unterscheiden (2x), während umgebende Proben nicht maßgeblich abweichen (weniger als 20 %):  
  
```  
WITH CTE (ProdId, PrevValue, CurrentValue, NextValue, ValidFrom, ValidTo)  
AS  
    (  
        SELECT   
            ProdId, LAG (DailySales, 1, 1) over (partition by ProdId order by ValidFrom) as PrevValue  
            , DailySales, LEAD (DailySales, 1, 1) over (partition by ProdId order by ValidFrom) as NextValue   
             , ValidFrom, ValidTo from Product  
        FOR SYSTEM_TIME ALL  
)  
  
SELECT   
    ProdId  
    , PrevValue  
    , CurrentValue  
    , NextValue  
    , ValidFrom  
    , ValidTo  
    , ABS (PrevValue - NextValue) / convert (float, (CASE WHEN NextValue > PrevValue THEN PrevValue ELSE NextValue END)) as PrevToNextDiff  
    , ABS (CurrentValue - PrevValue) / convert (float, (CASE WHEN CurrentValue > PrevValue THEN PrevValue ELSE CurrentValue END)) as CurrentToPrevDiff  
    , ABS (CurrentValue - NextValue) / convert (float, (CASE WHEN CurrentValue > NextValue THEN NextValue ELSE CurrentValue END)) as CurrentToNextDiff  
FROM CTE   
    WHERE   
        ABS (PrevValue - NextValue) / (CASE WHEN NextValue > PrevValue THEN PrevValue ELSE NextValue END) < 0.2  
            AND ABS (CurrentValue - PrevValue) / (CASE WHEN CurrentValue > PrevValue THEN PrevValue ELSE CurrentValue END) > 2  
            AND ABS (CurrentValue - NextValue) / (CASE WHEN CurrentValue > NextValue THEN NextValue ELSE CurrentValue END) > 2;  
```  
  
> [!NOTE]  
>  Dieses Beispiel wurde absichtlich vereinfacht. In den Produktionsszenarien verwenden Sie wahrscheinlich statistische Methoden, um die Proben zu ermitteln, die nicht dem allgemeinen Muster folgen.  
  
## <a name="slowly-changing-dimensions"></a>Langsam veränderliche Dimensionen  
 Dimensionen beim Data Warehousing enthalten i. d. R. relativ statische Daten zu Entitäten wie z. B. geografische Standorte, Kunden oder Produkte. Einige Szenarien erfordern jedoch ebenfalls das Nachverfolgen von Datenänderungen in Dimensionstabellen. Da Änderungen an Dimensionen sehr viel seltener, auf unvorhersehbare Weise und außerhalb des regulären Zeitplans für Faktentabellen auftreten, werden diese Typen von Dimensionstabellen als langsam veränderliche Dimensionen (SCD) bezeichnet.  
  
 Es gibt verschiedene Kategorien von langsam veränderlichen Dimensionen basierend darauf, wie der Änderungsverlauf beibehalten wird:  
  
-   Typ 0: Verlauf wird nicht beibehalten. Dimensionsattribute spiegeln die ursprünglichen Werte wider.  
  
-   Typ 1: Dimensionsattribute reflektieren die aktuellen Werte (die vorherigen Werte werden überschrieben).  
  
-   Typ 2: Jede Version des Dimensionselements wird mit einer separaten Zeile in der Tabelle dargestellt, in der Regel mit Spalten, die die Gültigkeitsdauer angeben.  
  
-   Typ 3: Der Verlauf wird für ausgewählte Attribute mit zusätzlichen Spalten in der gleichen Zeile eingeschränkt aufbewahrt.  
  
-   Typ 4: Der Verlauf wird in der separaten Tabelle aufbewahrt, während die Originaltabelle die neuesten (aktuellsten) Dimensionselementversionen beibehält.  
  
 Wenn Sie sich für die SCD-Strategie entscheiden, so ist die ETL-Ebene (Extrahieren-Transformieren-Laden) dafür verantwortlich, die Dimensionstabelle(n) korrekt beizubehalten. Dafür ist in der Regel viel Code und eine komplexe Wartung erforderlich.  
  
 Temporale Tabellen mit Systemversionsverwaltung in SQL Server 2016 können verwendet werden, um die Komplexität des Codes maßgeblich zu verringern, da der Verlauf der Daten automatisch beibehalten wird. Angesichts der Implementierung mithilfe von zwei Tabellen, entsprechen temporale Tabellen in SQL Server 2016 am ehesten dem Typ 4 SCD. Da temporale Abfragen es Ihnen jedoch nur ermöglichen, auf die aktuelle Tabelle zu verweisen, können Sie den Einsatz von temporalen Tabellen auch in Umgebungen in Betracht ziehen, in denen Sie Typ 2 SCD verwenden möchten.  
  
 Um Ihre normale Dimension in SCD zu konvertieren, erstellen Sie einfach eine neue oder ändern Sie eine vorhandene in eine temporale Tabelle mit Systemversionsverwaltung. Wenn Ihre vorhandene Dimensionstabelle Verlaufsdaten enthält, erstellen Sie eine separate Tabelle und verschieben Sie Verlaufsdaten dorthin. Behalten Sie die aktuellen (tatsächlichen) Dimensionsversionen in der ursprünglichen Dimensionstabelle. Verwenden Sie dann die ALTER TABLE-Syntax, um die Dimensionstabelle in eine temporale Tabelle mit Systemversionsverwaltung mit einer vordefinierten Verlaufstabelle zu konvertieren.  
  
 Das folgende Beispiel veranschaulicht den Prozess. Dabei wird davon ausgegangen, dass die DimLocation-Dimensionstabelle bereits über ValidFrom und ValidTo verfügt, da datetime2-Spalten keine NULL-Werte zulassen und vom ETL-Prozess aufgefüllt werden:  
  
```  
/*Move “closed” row versions into newly created history table*/  
SELECT * INTO  DimLocationHistory  
    FROM DimLocation  
        WHERE ValidTo < '9999-12-31 23:59:59.99';  
GO  
/*Create clustered columnstore index which is a very good choice in DW scenarios*/  
CREATE CLUSTERED COLUMNSTORE INDEX IX_DimLocationHistory ON DimLocationHistory  
/*Delete previous versions from DimLocation which will become current table in temporal-system-versioning configuration*/  
DELETE FROM DimLocation  
    WHERE ValidTo < '9999-12-31 23:59:59.99';  
/*Add period definition*/  
ALTER TABLE DimLocation ADD PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo);  
/*Enable system-versioning and bind histiory table to the DimLocation*/  
ALTER TABLE DimLocation SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DimLocationHistory));  
```  
  
 Beachten Sie, dass nach dem Erstellen während des Data Warehouse-Prozesses kein zusätzlicher Code erforderlich ist, um SCD zu verwalten.  
  
 Die folgende Abbildung zeigt, wie Sie temporale Tabellen in einem einfachen Szenario mit 2 SCDs (DimLocation und DimProduct) und einer Faktentabelle verwenden können.  
  
 ![TemporalSCD](../../relational-databases/tables/media/temporalscd.png "TemporalSCD")  
  
 Um die obigen SCDs in Berichten verwenden zu können, müssen Sie die Abfragen effektiv anpassen. Sie können beispielsweise den Gesamtumsatz und die durchschnittliche Anzahl der verkauften Produkte pro Kopf in den letzten sechs Monaten berechnen.  Beachten Sie, dass für beide Metriken eine Korrelation der Daten aus der Faktentabelle und den Dimensionen erforderlich ist, die ihre Attribute, die wichtig für die Analyse sind, (DimLocation.NumOfCustomers, DimProduct.UnitPrice) geändert haben könnten.  Mit der folgenden Abfrage werden die erforderlichen Metriken ordnungsgemäß berechnet:  
  
```  
DECLARE @now datetime2 = SYSUTCDATETIME()  
DECLARE @sixMonthsAgo datetime2 SET   
    @sixMonthsAgo = DATEADD (month, -12, SYSUTCDATETIME())   
  
SELECT DimProduct_History.ProductId  
   , DimLocation_History.LocationId  
    , SUM(F.Quantity * DimProduct_History.UnitPrice) AS TotalAmount  
    , AVG (F.Quantity/DimLocation_History.NumOfCustomers) AS AverageProductsPerCapita   
FROM FactProductSales F   
/* find corresponding record in SCD history in last 6 months, based on matching fact */  
JOIN DimLocation FOR SYSTEM_TIME BETWEEN @sixMonthsAgo AND @now AS DimLocation_History   
    ON DimLocation_History.LocationId = F.LocationId   
        AND F.FactDate BETWEEN DimLocation_History.ValidFrom AND DimLocation_History.ValidTo   
/* find corresponding record in SCD history in last 6 months, based on matching fact */  
JOIN DimProduct FOR SYSTEM_TIME BETWEEN @sixMonthsAgo AND @now AS DimProduct_History   
    ON DimProduct_History.ProductId = F.ProductId  
        AND F.FactDate BETWEEN DimProduct_History.ValidFrom AND DimProduct_History.ValidTo   
    WHERE F.FactDate BETWEEN @sixMonthsAgo AND @now   
GROUP BY DimProduct_History.ProductId, DimLocation_History.LocationId ;  
```  
  
 **Weitere Überlegungen:**  
  
-   Die Verwendung von temporalen Tabellen mit Systemversionsverwaltung für SCD ist dann akzeptabel, wenn die Gültigkeitsdauer anhand der Datenbanktransaktionszeit berechnet wird und zu Ihrer Geschäftslogik passt. Wenn Sie Daten mit erheblicher Verzögerung laden, ist die Transaktionszeit möglicherweise nicht akzeptabel.  
  
-   Standardmäßig ermöglichen temporale Tabellen mit Systemversionsverwaltung nicht die Änderung von Verlaufsdaten nach dem Laden. (Sie können den Verlauf ändern, nachdem Sie SYSTEM_VERSIONING auf OFF setzen.) Dies kann möglicherweise in Fällen eingeschränkt sein, bei denen die Verlaufsdaten regelmäßig geändert werden.  
  
-   Temporale Tabellen mit Systemversionsverwaltung generieren eine Zeilenversion bei jeder Spaltenänderung. Wenn Sie neue Versionen auf bestimmte Spaltenänderungen unterdrücken möchten, müssen Sie eine solche Einschränkung in die ETL-Logik integrieren.  
  
-   Wenn Sie eine erhebliche Anzahl von Zeilen mit Verlaufsdaten in SCD-Tabellen erwarten, ziehen Sie den Einsatz eines gruppierten Columnstore-Indexes als Hauptspeicheroption für die Verlaufstabelle in Betracht. Dies reduziert den Platzbedarf für die Verlaufstabelle und beschleunigt die Durchführung von analytischen Abfragen.  
  
## <a name="repairing-row-level-data-corruption"></a>Reparieren von Datenbeschädigungen auf Zeilenebene  
 Sie können Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung  verwenden, um schnell einzelne Zeilen anhand eines der zuvor erfassten Zustände zu reparieren. Diese Eigenschaft von temporalen Tabellen ist sehr nützlich, wenn Sie die betroffenen Zeilen ermitteln können und/oder den Zeitpunkt der unerwünschten Datenänderung kennen, sodass Sie die Reparatur effizient und ohne die Nutzung von Sicherungen durchführen können.  
  
 Dieser Ansatz hat mehrere Vorteile:  
  
-   Sie können den Umfang der Reparatur sehr genau steuern. Nicht betroffene Datensätze müssen den aktuellen Zustand beibehalten, wobei es sich oftmals um eine kritische Voraussetzung handelt.  
  
-   Der Vorgang ist sehr effizient, und die Datenbank bleibt für alle Arbeitsauslastungen online, bei denen die Daten verwendet werden.  
  
-   Der Reparaturvorgang selbst ist versionsspezifisch. Sie verfügen über einen Überwachungspfad für den Reparaturvorgang selbst, damit Sie später bei Bedarf analysieren können, was passiert ist.  
  
 Der Reparaturvorgang kann relativ leicht automatisiert werden. Hier ist ein Codebeispiel der gespeicherten Prozedur, mit der eine Datenreparatur für die Mitarbeitertabelle im Datenüberwachungsszenario durchgeführt wird.  
  
```  
DROP PROCEDURE IF EXISTS sp_RepairEmployeeRecord;  
GO  
  
CREATE PROCEDURE sp_RepairEmployeeRecord   
    @EmployeeID INT,  
    @versionNumber INT = 1  
AS  
  
;WITH History  
AS  
(  
        /* Order historical rows by tehir age in DESC order*/  
        SELECT ROW_NUMBER () OVER (PARTITION BY EmployeeID ORDER BY [ValidTo] DESC) AS RN, *  
        FROM Employee FOR SYSTEM_TIME ALL WHERE YEAR (ValidTo) < 9999 AND Employee.EmployeeID = @EmployeeID  
)  
  
/*Update current row by using N-th row version from history (default is 1 - i.e. last version)*/  
UPDATE Employee   
    SET [Position] = H.[Position], [Department] = H.Department, [Address] = H.[Address], AnnualSalary = H.AnnualSalary  
    FROM Employee E JOIN History H ON E.EmployeeID = H.EmployeeID AND RN = @versionNumber  
    WHERE E.EmployeeID = @EmployeeID  
  
```  
  
 Diese gespeicherte Prozedur nimmt @EmployeeID und @versionNumber als Eingabeparameter. Dieses Verfahren stellt den Zeilenzustand standardmäßig auf die letzte Version des Verlaufs (@versionNumber= 1) wieder her.  
  
 Das folgende Bild zeigt den Zustand der Zeile vor und nach dem Prozeduraufruf. Das rote Rechteck markiert die aktuelle Zeilenversion, die falsch ist; das grüne Rechteck kennzeichnet die richtige Version aus dem Verlauf.  
  
 ![TemporalUsageRepair1](../../relational-databases/tables/media/temporalusagerepair1.png "TemporalUsageRepair1")  
  
```  
EXEC sp_RepairEmployeeRecord @EmployeeID = 1, @versionNumber = 1  
```  
  
 ![TemporalUsageRepair2](../../relational-databases/tables/media/temporalusagerepair2.png "TemporalUsageRepair2")  
  
 Diese gespeicherte Reparaturprozedur kann so definiert werden, dass anstelle einer Zeilenversion ein genauer Zeitstempel akzeptiert wird. Die Zeile wird auf eine beliebige Version wiederhergestellt, die zum angegebenen Zeitpunkt aktiv war (d. h. AS OF-Zeitpunkt).  
  
```  
DROP PROCEDURE IF EXISTS sp_RepairEmployeeRecordAsOf;  
GO  
  
CREATE PROCEDURE sp_RepairEmployeeRecordAsOf   
    @EmployeeID INT,  
    @asOf datetime2  
AS  
  
/*Update current row to the state that was actual AS OF provided date*/  
UPDATE Employee   
    SET [Position] = History.[Position], [Department] = History.Department, [Address] = History.[Address], AnnualSalary = History.AnnualSalary  
    FROM Employee AS E JOIN Employee FOR SYSTEM_TIME AS OF @asOf AS History  ON E.EmployeeID = History.EmployeeID  
    WHERE E.EmployeeID = @EmployeeID  
  
```  
  
 Beim gleichen Datenbeispiel veranschaulicht das folgende Bild das Reparaturszenario mit einer Zeitbedingung. Hervorgehoben sind der @asOf-Parameter, die ausgewählte Zeile im Verlauf, die zum angegebenen Zeitpunkt aktiv war, und die neue Zeilenversion in der aktuellen Tabelle nach der Reparatur:  
  
 ![TemporalUsageRepair3](../../relational-databases/tables/media/temporalusagerepair3.png "TemporalUsageRepair3")  
  
 Datenkorrektur kann Teil des automatischen Datenladevorgangs in Data Warehousing- und Berichterstattungssystemen werden.  
Wenn ein neu aktualisierter Wert nicht korrekt ist, ist die Wiederherstellung der vorherigen Version aus dem Verlauf für viele Szenarien oftmals ausreichend. Das folgende Diagramm zeigt, wie dieser Vorgang automatisiert werden kann:  
  
 ![TemporalUsageRepair4](../../relational-databases/tables/media/temporalusagerepair4.png "TemporalUsageRepair4")  
  
## <a name="see-also"></a>Siehe auch  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Systemkonsistenzprüfungen von temporalen Tabellen](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Überlegungen und Einschränkungen zu temporalen Tabellen](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Sicherheit bei temporale Tabellen](../../relational-databases/tables/temporal-table-security.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
