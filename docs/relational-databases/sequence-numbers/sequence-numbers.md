---
title: Sequenznummern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sequence number object, overview
- sequence [Database Engine]
- autonumbers, sequences
- sequence numbers [SQL Server]
- sequence number object
ms.assetid: c900e30d-2fd3-4d5f-98ee-7832f37e79d1
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be2100277326fafec2dd32609b977de0f72cb9b4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="sequence-numbers"></a>Sequenznummern
  Als Sequenz wird ein benutzerdefiniertes schemagebundenes Objekt bezeichnet, das eine Sequenz numerischer Werte anhand der Spezifikation generiert, mit der die Sequenz erstellt wurde. Die Sequenz von numerischen Werten wird in aufsteigender oder absteigender Reihenfolge in einem definierten Intervall generiert, und je nach Anforderung wird ein Zyklus (Wiederholungen) ausgeführt. Sequenzen werden anders als Identitätsspalten keinen Tabellen zugeordnet. Eine Anwendung verweist auf ein Sequenzobjekt, um den nächsten Wert zu empfangen. Die Beziehung zwischen Sequenzen und Tabellen wird von der Anwendung gesteuert. Benutzeranwendungen können auf ein Sequenzobjekt verweisen und die Werteschlüssel in mehreren Zeilen und Tabellen koordinieren.  
  
 Eine Sequenz wird unabhängig von den Tabellen mithilfe der **CREATE SEQUENCE** -Anweisung erstellt. Mithilfe von Optionen können Sie das Inkrement, Maximal- und Minimalwerte, den Anfangspunkt, die automatische Neustartfunktion sowie das Zwischenspeichern konfigurieren, um die Leistung zu verbessern. Weitere Informationen zu den Optionen finden Sie unter [CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md).  
  
 Im Unterschied zu Identitätsspaltenwerten, die beim Einfügen von Zeilen generiert werden, kann eine Anwendung durch Aufrufen der [NEXT VALUE FOR](../../t-sql/functions/next-value-for-transact-sql.md) -Funktion die nächste Sequenznummer abrufen, bevor die Zeile eingefügt wird. Die Sequenznummer wird beim Aufruf von NEXT VALUE FOR zugeordnet, selbst wenn die Nummer nie in eine Tabelle eingefügt wird. Die NEXT VALUE FOR-Funktion kann als Standardwert für eine Spalte in einer Tabellendefinition verwendet werden. Mit [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) können Sie einen Bereich von mehreren Sequenznummern gleichzeitig abrufen.  
  
 Eine Sequenz kann als beliebiger ganzzahliger Datentyp definiert werden. Wenn kein Datentyp nicht angegeben ist, wird eine Sequenz standardmäßig auf **bigint**festgelegt.  
  
## <a name="using-sequences"></a>Verwenden von Sequenzen  
 Verwenden Sie in den folgenden Szenarios Sequenzen anstelle der Identitätsspalten:  
  
-   Die Anwendung fordert eine Nummer an, bevor die Einfügung in die Tabelle ausgeführt wird.  
  
-   Die Anwendung erfordert das Freigeben einer einzelnen Reihe von Nummern zwischen mehreren Tabellen oder mehreren Spalten innerhalb einer Tabelle.  
  
-   Die Anwendung muss die Nummernreihe neu starten, wenn eine angegebene Nummer erreicht wurde. Beispiel: Nachdem die Werte 1 bis 10 zugewiesen wurden, beginnt die Anwendung erneut mit dem Zuweisen der Werte 1 bis 10.  
  
-   Die Anwendung erfordert, dass Sequenzwerte nach einem weiteren Feld sortiert werden. Die NEXT VALUE FOR-Funktion kann die OVER-Klausel auf den Funktionsaufruf anwenden. Die OVER-Klausel garantiert, dass die zurückgegebenen Werte in der Reihenfolge der ORDER BY-Klausel der OVER-Klausel generiert werden.  
  
-   Eine Anwendung erfordert, dass mehrere Nummern gleichzeitig zugewiesen werden. Eine Anwendung muss z. B. fünf sequenzielle Nummern reservieren. Wenn Identitätswerte angefordert werden, können Lücken in der Reihe entstehen, wenn andere Prozesse gleichzeitig Nummern ausgeben. Durch einen Aufruf von sp_sequence_get_range können mehrere Nummern in der Sequenz gleichzeitig abgerufen werden.  
  
-   Sie müssen die Spezifikation der Sequenz ändern (z. B. den Inkrementwert).  
  
## <a name="limitations"></a>Einschränkungen  
 Im Unterschied zu Identitätsspalten, deren Werte nicht geändert werden können, werden Sequenzwerte nach dem Einfügen in die Tabelle nicht automatisch geschützt. Um das Ändern von Sequenzwerten zu verhindern, verwenden Sie für die Tabelle einen Updatetrigger, um einen Rollback der Änderungen auszuführen.  
  
 Die Eindeutigkeit von Sequenzwerten wird nicht automatisch erzwungen. Sequenzwerte sind so konzipiert, dass sie wiederverwendet werden können. Wenn Sequenzwerte in einer Tabelle eindeutig sein müssen, erstellen Sie für die Spalte einen eindeutigen Index. Wenn Sequenzwerte in einer Tabelle für eine ganze Gruppe von Tabellen eindeutig sein müssen, erstellen Sie Trigger, mit denen verhindert wird, dass durch Updateanweisungen oder Sequenznummerzyklen Duplikate erzeugt werden.  
  
 Das Sequenzobjekt generiert Nummern entsprechend seiner Definition, es steuert jedoch nicht die Verwendung dieser Nummern. In eine Tabelle eingefügte Sequenznummern können Lücken aufweisen, wenn ein Rollback für eine Transaktion ausgeführt wird, wenn ein Sequenzobjekt von mehreren Tabellen gemeinsam verwendet wird oder wenn Sequenznummern zugeordnet sind, ohne dass sie in Tabellen verwendet werden. Bei Erstellung mit der CACHE-Option können die Sequenznummern im Cache durch unerwartetes Herunterfahren, z. B. bei einem Stromausfall, verloren gehen.  
  
 Wenn mehrere Instanzen der **NEXT VALUE FOR** -Funktion denselben Sequenz-Generator in einer einzelnen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung angeben, geben all diese Instanzen den gleichen Wert für eine bestimmte Zeile zurück, die von dieser [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung erstellt. Dieses Verhalten ist mit dem ANSI-Standard konsistent.  
  
## <a name="typical-use"></a>Typische Verwendung  
 Verwenden Sie die folgende Anweisung, um eine ganzzahlige Sequenznummer zu erstellen, die von -2.147.483.648 bis 2.147.483.647 um jeweils 1 inkrementiert wird.  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    INCREMENT BY 1 ;  
```  
  
 Verwenden Sie die folgende Anweisung, um eine ganzzahlige Sequenznummer zu erstellen, die einer Identitätsspalte ähnelt, die von 1 bis 2.147.483.647 um jeweils 1 inkrementiert wird.  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
  
```  
  
## <a name="managing-sequences"></a>Verwalten von Sequenzen  
 Weitere Informationen zu Sequenzen erhalten Sie durch Abfragen von [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Es werden zusätzliche Beispiele in den Themen [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md), [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md) und [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) behandelt.  
  
### <a name="a-using-a-sequence-number-in-a-single-table"></a>A. Verwenden einer Sequenznummer in einer einzelnen Tabelle  
 Im folgenden Beispiel werden das Schema „Test“, die Tabelle „Orders“ sowie die Sequenz „CountBy1“ erstellt. Anschließend werden mithilfe der NEXT VALUE FOR-Funktion Zeilen in die Tabelle eingefügt.  
  
```  
--Create the Test schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Orders  
    (OrderID int PRIMARY KEY,  
    Name varchar(20) NOT NULL,  
    Qty int NOT NULL);  
GO  
  
-- Create a sequence  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
-- Insert three records  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Tire', 2) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Seat', 1) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Brake', 1) ;  
GO  
  
-- View the table  
SELECT * FROM Test.Orders ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `OrderID  Name    Qty`  
  
 `1        Tire    2`  
  
 `2        Seat    1`  
  
 `3        Brake   1`  
  
### <a name="b-calling-next-value-for-before-inserting-a-row"></a>B. Aufrufen von NEXT VALUE FOR vor dem Einfügen einer Zeile  
 Im folgenden Beispiel wird mit der in Beispiel A erstellten `Orders` -Tabelle eine Variable mit dem Namen `@nextID`erstellt. Anschließend wird die Variable mithilfe der NEXT VALUE FOR-Funktion auf die nächste verfügbare Sequenznummer festgelegt. Hierfür wird angenommen, dass die Bestellung von der Anwendung verarbeitet wird, beispielsweise, indem für den Benutzer die `OrderID` -Nummer der potenziellen Bestellung bereitgestellt wird. Anschließend wird die Bestellung validiert. Ungeachtet der Zeit, die für diese Verarbeitung benötigt wird und wie viele weitere Bestellungen während des Prozesses hinzugefügt werden, wird die ursprüngliche Nummer für die Verwendung durch diese Verbindung beibehalten. Schließlich wird die Bestellung mit der `INSERT` -Anweisung der `Orders` -Tabelle hinzugefügt.  
  
```  
DECLARE @NextID int ;  
SET @NextID = NEXT VALUE FOR Test.CountBy1;  
-- Some work happens  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (@NextID, 'Rim', 2) ;  
GO  
  
```  
  
### <a name="c-using-a-sequence-number-in-multiple-tables"></a>C. Verwenden einer Sequenznummer in mehreren Tabellen  
 In diesem Beispiel wird davon ausgegangen, dass ein Fertigungsstraßen-Überwachungsprozess Benachrichtigung über Ereignisse empfängt, die am Produktionsort auftreten. Jedem Ereignis wird eine eindeutige und stetig steigende `EventID` -Nummer zugewiesen. Für alle Ereignisse wird dieselbe `EventID` -Sequenznummer verwendet, sodass die einzelnen Ereignisse in Berichten, in denen alle Ereignisse kombiniert sind, eindeutig identifiziert werden können. Die Ereignisdaten werden jedoch in drei verschiedenen Tabellen gespeichert, je nach Typ des jeweiligen Ereignisses. Im Codebeispiel werden das Schema `Audit`, die Sequenz `EventCounter`und drei Tabellen erstellt, die jeweils die `EventCounter` -Sequenz als Standardwert verwenden. Anschließend werden den drei Tabellen Zeilen hinzugefügt, und die Ergebnisse werden abgefragt.  
  
```  
CREATE SCHEMA Audit ;  
GO  
CREATE SEQUENCE Audit.EventCounter  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
CREATE TABLE Audit.ProcessEvents  
(  
    EventID int PRIMARY KEY CLUSTERED   
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EventCode nvarchar(5) NOT NULL,  
    Description nvarchar(300) NULL  
) ;  
GO  
  
CREATE TABLE Audit.ErrorEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NULL,  
    ErrorNumber int NOT NULL,  
    EventDesc nvarchar(256) NULL  
) ;  
GO  
  
CREATE TABLE Audit.StartStopEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NOT NULL,  
    StartOrStop bit NOT NULL  
) ;  
GO  
  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 0) ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (72, 0) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (2735,   
    'Clean room temperature 18 degrees C.') ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (18, 'Spin rate threashold exceeded.') ;  
INSERT Audit.ErrorEvents (EquipmentID, ErrorNumber, EventDesc)   
    VALUES (248, 82, 'Feeder jam') ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 1) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (1841, 'Central feed in bypass mode.') ;  
-- The following statement combines all events, though not all fields.  
SELECT EventID, EventTime, Description FROM Audit.ProcessEvents   
UNION SELECT EventID, EventTime, EventDesc FROM Audit.ErrorEvents   
UNION SELECT EventID, EventTime,   
CASE StartOrStop   
    WHEN 0 THEN 'Start'   
    ELSE 'Stop'  
END   
FROM Audit.StartStopEvents  
ORDER BY EventID ;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `EventID  EventTime                Description`  
  
 `1        2009-11-02 15:00:51.157  Start`  
  
 `2        2009-11-02 15:00:51.160  Start`  
  
 `3        2009-11-02 15:00:51.167  Clean room temperature 18 degrees C.`  
  
 `4        2009-11-02 15:00:51.167  Spin rate threshold exceeded.`  
  
 `5        2009-11-02 15:00:51.173  Feeder jam`  
  
 `6        2009-11-02 15:00:51.177  Stop`  
  
 `7        2009-11-02 15:00:51.180  Central feed in bypass mode.`  
  
### <a name="d-generating-repeating-sequence-numbers-in-a-result-set"></a>D. Generieren von wiederholten Sequenznummern in einem Resultset  
 Im folgenden Beispiel werden zwei Eigenschaften von Sequenznummern veranschaulicht: die zyklische Verwendung und das Verwenden von `NEXT VALUE FOR` in einer SELECT-Anweisung.  
  
```  
CREATE SEQUENCE CountBy5  
   AS tinyint  
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 5  
    CYCLE ;  
GO  
  
SELECT NEXT VALUE FOR CountBy5 AS SurveyGroup, Name FROM sys.objects ;  
GO  
```  
  
### <a name="e-generating-sequence-numbers-for-a-result-set-by-using-the-over-clause"></a>E. Generieren von Sequenznummern für ein Resultset mit der OVER-Klausel  
 Im folgenden Beispiel wird das Resultset mithilfe der `OVER` -Klausel nach `Name` sortiert, bevor die Sequenznummernspalte hinzugefügt wird.  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Samples ;  
GO  
  
CREATE SEQUENCE Samples.IDLabel  
    AS tinyint  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="f-resetting-the-sequence-number"></a>F. Zurücksetzen der Sequenznummer  
 In Beispiel E wurden die ersten 79 der `Samples.IDLabel`-Sequenznummern verbraucht. (Ihre Version von `AdventureWorks2012` gibt möglicherweise eine andere Anzahl von Ergebnissen zurück.) Führen Sie Folgendes aus, um die nächsten 79 Sequenznummern (80 bis 158) zuzuweisen.  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
 Führen Sie die folgende Anweisung aus, um die `Samples.IDLabel` -Sequenz neu zu starten.  
  
```  
ALTER SEQUENCE Samples.IDLabel  
RESTART WITH 1 ;  
```  
  
 Führen Sie die SELECT-Anweisung erneut aus, um sich zu vergewissern, dass die `Samples.IDLabel` -Sequenz mit der Nummer 1 neu gestartet wurde.  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="g-changing-a-table-from-identity-to-sequence"></a>G. Ändern einer Tabelle von einer Identitäts- in eine Sequenztabelle  
 Im folgenden Beispiel werden ein Schema und eine Tabelle erstellt, die drei Zeilen für das Beispiel enthält. Anschließend wird eine neue Spalte hinzugefügt, und die alte Spalte wird gelöscht.  
  
```  
-- Create a schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Department  
    (  
        DepartmentID smallint IDENTITY(1,1) NOT NULL,  
        Name nvarchar(100) NOT NULL,  
        GroupName nvarchar(100) NOT NULL  
    CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC)   
    ) ;  
GO  
  
-- Insert three rows into the table  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Engineering', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Tool Design', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Sales', 'Sales and Marketing');  
GO  
  
-- View the table that will be changed  
SELECT * FROM Test.Department ;  
GO  
  
-- End of portion creating a sample table  
--------------------------------------------------------  
-- Add the new column that does not have the IDENTITY property  
ALTER TABLE Test.Department   
    ADD DepartmentIDNew smallint NULL  
GO  
  
-- Copy values from the old column to the new column  
UPDATE Test.Department  
    SET DepartmentIDNew = DepartmentID ;  
GO  
  
-- Drop the primary key constraint on the old column  
ALTER TABLE Test.Department  
    DROP CONSTRAINT [PK_Department_DepartmentID];  
-- Drop the old column  
ALTER TABLE Test.Department  
    DROP COLUMN DepartmentID ;  
GO  
  
-- Rename the new column to the old columns name  
EXEC sp_rename 'Test.Department.DepartmentIDNew',   
    'DepartmentID', 'COLUMN';  
GO  
  
-- Change the new column to NOT NULL  
ALTER TABLE Test.Department  
    ALTER COLUMN DepartmentID smallint NOT NULL ;  
-- Add the unique primary key constraint  
ALTER TABLE Test.Department  
    ADD CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC) ;  
-- Get the highest current value from the DepartmentID column   
-- and create a sequence to use with the column. (Returns 3.)  
SELECT MAX(DepartmentID) FROM Test.Department ;  
-- Use the next desired value (4) as the START WITH VALUE;  
CREATE SEQUENCE Test.DeptSeq  
    AS smallint  
    START WITH 4  
    INCREMENT BY 1 ;  
GO  
  
-- Add a default value for the DepartmentID column  
ALTER TABLE Test.Department  
    ADD CONSTRAINT DefSequence DEFAULT (NEXT VALUE FOR Test.DeptSeq)   
        FOR DepartmentID;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;   
-- Test insert  
INSERT Test.Department (Name, GroupName)  
    VALUES ('Audit', 'Quality Assurance') ;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;  
GO  
  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die `SELECT *` verwenden, empfangen die neue Spalte anstelle der ersten Spalte als letzte Spalte. Wenn dies nicht zulässig ist, müssen Sie eine völlig neue Tabelle erstellen, die Daten in diese Tabelle verschieben und die Berechtigungen für die neue Tabelle erneut erstellen.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)  
  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)  
  
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)  
  
 [IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
  
  
