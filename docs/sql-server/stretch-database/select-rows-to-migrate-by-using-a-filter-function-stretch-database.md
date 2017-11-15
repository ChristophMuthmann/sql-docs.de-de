---
title: "Auswählen zu migrierender Zeilen mithilfe einer Filterfunktion (Stretch Database) | Microsoft-Dokumentation"
ms.custom: SQL2016_New_Updated
ms.date: 06/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, predicates
- predicates for Stretch Database
- Stretch Database, inline table-valued functions
- inline table-valued functions for Stretch Database
ms.assetid: 090890ee-7620-4a08-8e15-d2fbc71dd12f
caps.latest.revision: "43"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 290d0a17271d7099904eb7f4f50ffd8280fe2264
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="select-rows-to-migrate-by-using-a-filter-function-stretch-database"></a>Auswählen zu migrierender Zeilen mithilfe einer Filterfunktion (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Wenn Sie kalte Daten in einer separaten Tabelle speichern, können Sie Stretch-Datenbank zum Migrieren der gesamten Tabelle konfigurieren. Wenn Ihre Tabelle sowohl heiße als auch kalte Daten enthält, können Sie ein Filterprädikat zum Auswählen der zu migrierenden Zeilen angeben. Das Filterprädikat ist eine Inline-Tabellenwertfunktion. In diesem Thema wird beschrieben, wie Sie eine Inline-Tabellenwertfunktion schreiben, um die zu migrierenden Zeilen auszuwählen.  
  
> [!IMPORTANT]
> Wenn Sie eine schwache Filterfunktion angeben, wird die Datenmigration ebenfalls unzureichend ausgeführt. Stretch-Datenbank wendet die Filterfunktion mithilfe des CROSS APPLY-Operators auf die Tabelle an.  
  
 Wenn Sie keine Filterfunktion angeben, wird die gesamte Tabelle migriert.  
  
 Wenn Sie den Assistenten zum Aktivieren von Stretch für eine Datenbank ausführen, können Sie eine gesamte Tabelle migrieren oder eine Filterfunktion im Assistenten angeben. Wenn Sie zum Auswählen zu migrierender Zeilen eine andere Art von Filterfunktion verwenden möchten, führen Sie einen der folgenden Schritte aus.  
  
-   Beenden Sie den Assistenten, und führen Sie die ALTER TABLE-Anweisung aus, um Stretch für die Tabelle zu aktivieren und eine Filterfunktion anzugeben.  
  
-   Führen Sie die ALTER TABLE-Anweisung aus, um eine Filterfunktion anzugeben, nachdem Sie den Assistenten beendet haben.  
  
 Die ALTER TABLE-Syntax zum Hinzufügen einer Funktion wird weiter unten in diesem Thema beschrieben.  
  
## <a name="basic-requirements-for-the-filter-function"></a>Grundlegende Anforderungen für die Filterfunktion  
 Die Inline-Tabellenwertfunktion, die für ein Filterprädikat einer Stretch-Datenbank erforderlich ist, sieht wie im folgenden Beispiel aus.  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate(@column1 datatype1, @column2 datatype2 [, ...n])  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE <predicate>  
```  
  
 Die Parameter für die Funktion müssen Bezeichner für Spalten der Tabelle sein.  
  
 Die Schemabindung ist erforderlich, um zu verhindern, dass Spalten, die von der Filterfunktion verwendet werden, gelöscht oder geändert werden.  
  
### <a name="return-value"></a>Rückgabewert  
 Wenn die Funktion ein nicht leeres Ergebnis zurückgibt, ist die Zeile für die Migration geeignet. Wenn die Funktion hingegen kein Ergebnis zurückgibt, ist die Zeile nicht für die Migration geeignet.  
  
### <a name="conditions"></a>Bedingungen  
 Das &lt;*Prädikat*&gt; kann aus einer oder mehreren Bedingungen bestehen, die mit dem logischen AND-Operator verknüpft sind.  
  
```  
<predicate> ::= <condition> [ AND <condition> ] [ ...n ]  
```  
  
 Jede Bedingung kann wiederum aus einer oder mehreren primitiven Bedingungen bestehen, die mit dem logischen OR-Operator verknüpft sind.  
  
```  
<condition> ::= <primitive_condition> [ OR <primitive_condition> ] [ ...n ]  
```  
  
### <a name="primitive-conditions"></a>Primitive Bedingungen  
 Eine primitive Bedingung eignet sich für die folgenden Vergleiche.  
  
```  
<primitive_condition> ::=   
{  
<function_parameter> <comparison_operator> constant  
| <function_parameter> { IS NULL | IS NOT NULL }  
| <function_parameter> IN ( constant [ ,...n ] )  
}  
  
```  
  
-   Vergleichen eines Funktionsparameters mit einem konstanten Ausdruck. Beispiel: `@column1 < 1000`.  
  
     Es folgt ein Beispiel, das überprüft, ob der Wert einer *date* -Spalte &lt; 1.1.2016 ist.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
    GO  
  
    ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(date),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
-   Anwenden des Operators IS NULL oder IS NOT NULL auf einen Funktionsparameter.  
  
-   Verwenden des IN-Operators, um einen Funktionsparameter mit einer Liste konstanter Werte zu vergleichen.  
  
     Es folgt ein Beispiel, das überprüft, ob der Wert einer *shipment_status*  -Spalte `IN (N'Completed', N'Returned', N'Cancelled')`ist.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate(@column1 nvarchar(15))  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ALTER TABLE table1 SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(shipment_status),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
### <a name="comparison-operators"></a>Vergleichsoperatoren  
 Die folgenden Vergleichsoperatoren werden unterstützt.  
  
 `<, <=, >, >=, =, <>, !=, !<, !>`  
  
```  
<comparison_operator> ::= { < | <= | > | >= | = | <> | != | !< | !> }  
```  
  
### <a name="constant-expressions"></a>Konstante Ausdrücke  
 Bei den Konstanten, die Sie in einer Filterfunktion verwenden, kann es sich um einen beliebigen deterministischen Ausdruck handeln, der beim Definieren der Funktion ausgewertet werden kann. Konstante Ausdrücke können Folgendes enthalten.  
  
-   Literale. Beispiel: `N’abc’, 123`.  
  
-   Algebraische Ausdrücke. Beispiel: `123 + 456`.  
  
-   Deterministische Funktionen. Beispiel: `SQRT(900)`.  
  
-   Deterministische Konvertierungen, die CAST oder CONVERT verwenden. Beispiel: `CONVERT(datetime, '1/1/2016', 101)`.  
  
### <a name="other-expressions"></a>Andere Ausdrücke  
 Sie können die Operatoren BETWEEN und NOT BETWEEN verwenden, wenn die resultierende Funktion den hier beschriebenen Regeln entspricht, nachdem Sie die Operatoren BETWEEN und NOT BETWEEN durch die entsprechenden AND- und OR-Ausdrücke ersetzt haben.  
  
 Sie können keine Unterabfragen oder nicht deterministische Funktionen wie RAND() oder GETDATE() verwenden.  
  
## <a name="add-a-filter-function-to-a-table"></a>Hinzufügen einer Filterfunktion zu einer Tabelle  
 Fügen Sie einer Tabelle eine Filterfunktion hinzu, indem Sie die **ALTER TABLE** -Anweisung ausführen und eine vorhandene Inline-Tabellenwertfunktion als Wert des Parameters **FILTER_PREDICATE** angeben. Beispiel:  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = dbo.fn_stretchpredicate(column1, column2),  
    MIGRATION_STATE = <desired_migration_state>  
) )  
  
```  
  
 Nachdem Sie die Funktion als Prädikat an die Tabelle gebunden haben, gilt Folgendes:  
  
-   Bei der nächsten Datenmigration werden nur die Zeilen migriert, für die die Funktion einen nicht leeren Wert zurückgibt.  
  
-   Die von der Funktion verwendeten Spalten sind schemagebunden. Sie können diese Spalten nicht ändern, solange eine Tabelle die Funktion als ihr Filterprädikat nutzt.  
  
 Sie können die Inline-Tabellenwertfunktion nicht löschen, solange eine Tabelle die Funktion als ihr Filterprädikat nutzt. 

> [!TIP]
> Erstellen Sie einen Index für die Spalten, die von der Funktion verwendet werden, um die Leistung der Filterfunktion zu verbessern.

 ### <a name="passing-column-names-to-the-filter-function"></a>Übergeben von Spaltennamen an die Filterfunktion
 
 Wenn Sie einer Tabelle eine Filterfunktion zuweisen, geben Sie die an die Filterfunktion übergebenen Spaltennamen mit einem einteiligen Namen an. Wenn Sie beim Übergeben der Spaltennamen einen dreiteiligen Namen angeben, treten bei nachfolgenden Abfragen der Stretch-aktivierten Tabelle Fehler auf.

Wenn Sie z.B. einen dreiteiligen Spaltennamen angeben, wie im folgenden Beispiel dargestellt, wird die Anweisung erfolgreich ausgeführt, bei nachfolgenden Abfragen der Tabelle treten jedoch Fehler auf.

```sql
ALTER TABLE SensorTelemetry 
  SET ( REMOTE_DATA_ARCHIVE = ON (
    FILTER_PREDICATE=dbo.fn_stretchpredicate(dbo.SensorTelemetry.ScanDate),
    MIGRATION_STATE = OUTBOUND )
  )
```

Geben Sie die Filterfunktion stattdessen mit einem einteiligen Namen an, wie im folgenden Beispiel dargestellt.

```sql
ALTER TABLE SensorTelemetry 
  SET ( REMOTE_DATA_ARCHIVE = ON  (
    FILTER_PREDICATE=dbo.fn_stretchpredicate(ScanDate),
    MIGRATION_STATE = OUTBOUND )
  )
```
  
## <a name="addafterwiz"></a>Hinzufügen einer Filterfunktion nach Ausführen des Assistenten  
  
Wenn Sie eine Funktion verwenden möchten, die Sie im Assistenten **zum Aktivieren von Stretch für eine Datenbank** nicht erstellen können, können Sie die **ALTER TABLE** -Anweisung ausführen, um nach Beenden des Assistenten eine Funktion anzugeben. Bevor eine Funktion angewendet werden kann, müssen Sie jedoch die Datenmigration anhalten, die bereits in Bearbeitung ist, und migrierte Daten zurückbringen. (Weitere Informationen dazu, warum dies notwendig ist, finden Sie im Abschnitt [Ersetzen einer vorhandenen Filterfunktion](#replacePredicate)).
  
1. Kehren Sie die Migrationsrichtung um, und bringen Sie bereits migrierte Daten zurück. Dieser Vorgang kann nach dem Start nicht mehr abgebrochen werden. Es fallen auf Azure auch Kosten für ausgehende Datenübertragungen an. Weitere Informationen finden Sie unter [Datenübertragungen – Preisdetails](https://azure.microsoft.com/pricing/details/data-transfers/).  
  
    ```sql  
    ALTER TABLE <table name>  
        SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ;   
    ```  
  
2. Warten Sie, bis die Migration abgeschlossen ist. Sie können den Status unter **Stretch Database-Überwachung** in SQL Server Management Studio überprüfen oder die Sicht **sys.dm_db_rda_migration_status** abfragen. Weitere Informationen finden Sie unter [Monitor and troubleshoot data migration](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) (Überwachung und Problembehandlung für die Datenmigration) oder [sys.dm_db_rda_migration_status](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
3. Erstellen Sie die Filterfunktion, die auf die Tabelle angewendet werden soll.  
  
4. Fügen Sie die Funktion der Tabelle hinzu, und starten Sie die Datenmigration zu Azure neu.  
  
    ```sql  
    ALTER TABLE <table name>  
        SET ( REMOTE_DATA_ARCHIVE  
            (           
                FILTER_PREDICATE = <predicate>,  
                MIGRATION_STATE = OUTBOUND  
            )  
            );   
    ```  
  
## <a name="filter-rows-by-date"></a>Filtern von Zeilen nach Datum  
 Im folgenden Beispiel werden Zeilen migriert, in denen die Spalte **date** einen Wert vor dem 1. Januar 2016 enthält.  
  
```sql  
-- Filter by date  
--  
CREATE FUNCTION dbo.fn_stretch_by_date(@date datetime2)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
       RETURN SELECT 1 AS is_eligible WHERE @date < CONVERT(datetime2, '1/1/2016', 101)  
GO  
  
```  
  
## <a name="filter-rows-by-the-value-in-a-status-column"></a>Filtern von Zeilen nach dem Wert in einer Statusspalte  
 Im folgenden Beispiel werden Zeilen migriert, in denen die Spalte **status** einen der angegebenen Werte enthält.  
  
```sql  
-- Filter by status column  
--  
CREATE FUNCTION dbo.fn_stretch_by_status(@status nvarchar(128))  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
       RETURN SELECT 1 AS is_eligible WHERE @status IN (N'Completed', N'Returned', N'Cancelled')  
GO  
  
```  
  
## <a name="filter-rows-by-using-a-sliding-window"></a>Filtern von Zeilen mithilfe eines gleitenden Fensters  
 Um Zeilen mithilfe eines gleitenden Fensters zu filtern, beachten Sie die folgenden Anforderungen an die Filterfunktion.  
  
-   Die Funktion muss deterministisch sein. Sie können daher keine Funktion erstellen, die das gleitende Fenster im Ablauf der Zeit neu berechnet.  
  
-   Die Funktion verwendet die Schemabindung. Daher können Sie die Funktion nicht einfach täglich „direkt“ aktualisieren, indem Sie **ALTER FUNCTION** aufrufen, um das gleitende Fenster zu bewegen.  
  
 Beginnen Sie mit einer Filterfunktion wie im folgenden Beispiel, bei dem Zeilen migriert werden, in denen die Spalte **systemEndTime** einen Wert vor dem 1. Januar 2016 enthält.  
  
```sql  
CREATE FUNCTION dbo.fn_StretchBySystemEndTime20160101(@systemEndTime datetime2)   
RETURNS TABLE   
WITH SCHEMABINDING    
AS    
RETURN SELECT 1 AS is_eligible   
  WHERE @systemEndTime < CONVERT(datetime2, '2016-01-01T00:00:00', 101) ;  
  
```  
  
 Wenden Sie die Filterfunktion auf die Tabelle an.  
  
```sql  
ALTER TABLE <table name>   
SET (   
        REMOTE_DATA_ARCHIVE = ON   
                (   
                        FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20160101(SysEndTime)  
                                , MIGRATION_STATE = OUTBOUND   
                )  
        )   
;  
  
```  
  
 Wenn Sie das gleitende Fenster aktualisieren möchten, gehen Sie folgendermaßen vor.  
  
1.  Erstellen Sie eine neue Funktion, die das neue gleitende Fenster angibt. Das folgende Beispiel wählt Datumsangaben vor dem 2. Januar 2016 statt vor dem 1. Januar 2016 aus.  
  
2.  Ersetzen Sie die vorherige Filterfunktion durch die neue, indem Sie **ALTER TABLE**aufrufen, wie im folgenden Beispiel dargestellt.  
  
3.  Löschen Sie optional die vorherige Filterfunktion, die Sie nicht mehr verwenden, indem Sie **DROP FUNCTION**aufrufen. (Dieser Schritt ist nicht im Beispiel dargestellt.)  
  
```sql  
BEGIN TRAN  
GO  
        /*(1) Create new predicate function definition */  
        CREATE FUNCTION dbo.fn_StretchBySystemEndTime20160102(@systemEndTime datetime2)  
        RETURNS TABLE  
        WITH SCHEMABINDING   
        AS   
        RETURN SELECT 1 AS is_eligible  
               WHERE @systemEndTime < CONVERT(datetime2,'2016-01-02T00:00:00', 101)  
        GO  
  
        /*(2) Set the new function as the filter predicate */  
        ALTER TABLE <table name>  
        SET   
        (  
               REMOTE_DATA_ARCHIVE = ON  
               (  
                       FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20160102(SysEndTime),  
                       MIGRATION_STATE = OUTBOUND  
               )  
        )   
COMMIT ;  
  
```  
  
## <a name="more-examples-of-valid-filter-functions"></a>Weitere Beispiele gültiger Filterfunktionen  
  
-   Das folgende Beispiel kombiniert die beiden primitiven Bedingungen mithilfe des logischen Operators AND.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate((@column1 datetime, @column2 nvarchar(15))  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
      WHERE @column1 < N'20150101' AND @column2 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ALTER TABLE table1 SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(date, shipment_status),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
-   Im folgenden Beispiel werden verschiedene Bedingungen und eine deterministische Konvertierung mit CONVERT verwendet.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example1(@column1 datetime, @column2 int, @column3 nvarchar)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2015', 101) AND (@column2 < -100 OR @column2 > 100 OR @column2 IS NULL) AND @column3 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ```  
  
-   Im folgenden Beispiel werden die mathematische Operatoren und Funktionen verwendet.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example2(@column1 float)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < SQRT(400) + 10  
    GO  
  
    ```  
  
-   Im folgenden Beispiel werden die Operatoren BETWEEN und NOT BETWEEN verwendet. Diese Verwendung ist möglich, da die resultierende Funktion den hier beschriebenen Regeln entspricht, nachdem Sie die Operatoren BETWEEN und NOT BETWEEN durch die entsprechenden AND- und OR-Ausdrücke ersetzt haben.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example3(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 BETWEEN 0 AND 100  
                AND (@column2 NOT BETWEEN 200 AND 300 OR @column1 = 50)  
    GO  
  
    ```  
  
     Die vorhergehende Funktion entspricht der folgenden Funktion nach dem Ersetzen der Operatoren BETWEEN und NOT BETWEEN durch die entsprechenden AND- und OR-Ausdrücke.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example4(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 >= 0 AND @column1 <= 100 AND (@column2 < 200 OR @column2 > 300 OR @column1 = 50)  
    GO  
  
    ```  
  
## <a name="examples-of-filter-functions-that-arent-valid"></a>Beispiele ungültiger Filterfunktionen  
  
-   Die folgende Funktion ist ungültig, da sie eine nicht deterministische Konvertierung enthält.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example5(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < CONVERT(datetime, '1/1/2016')  
    GO  
  
    ```  
  
-   Die folgende Funktion ist ungültig, da sie einen nicht deterministischen Funktionsaufruf enthält.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example6(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < DATEADD(day, -60, GETDATE())  
    GO  
  
    ```  
  
-   Die folgende Funktion ist ungültig, da sie eine Unterabfrage enthält.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example7(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 IN (SELECT SupplierID FROM Supplier WHERE Status = 'Defunct')  
    GO  
  
    ```  
  
-   Die folgenden Funktionen sind ungültig, da Ausdrücke, die algebraische Operatoren oder integrierte Funktionen verwenden, beim Definieren der Funktion in eine Konstante ausgewertet werden müssen. Sie können keine Verweise auf Spalten in algebraische Ausdrücke oder Funktionsaufrufe einschließen.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example8(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 % 2 =  0  
    GO  
  
    CREATE FUNCTION dbo.fn_example9(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE SQRT(@column1) = 30  
    GO  
  
    ```  
  
-   Die folgende Funktion ist ungültig, da sie gegen die hier beschriebenen Regeln verstößt, nachdem Sie den Operator BETWEEN durch den entsprechenden AND-Ausdruck ersetzt haben.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example10(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
    AS  
    RETURN  SELECT 1 AS is_eligible  
            WHERE (@column1 BETWEEN 1 AND 200 OR @column1 = 300) AND @column2 > 1000  
    GO  
  
    ```  
  
     Die vorhergehende Funktion entspricht der folgenden Funktion nach dem Ersetzen des Operators BETWEEN durch den entsprechenden AND-Ausdruck. Diese Funktion ist ungültig, da primitive Bedingungen nur den logischen Operator OR verwenden können.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example11(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE (@column1 >= 1 AND @column1 <= 200 OR @column1 = 300) AND @column2 > 1000  
    GO  
  
    ```  
  
## <a name="how-stretch-database-applies-the-filter-function"></a>So wendet Stretch-Datenbank die Filterfunktion an  
 Stretch-Datenbank wendet die Filterfunktion mithilfe des CROSS APPLY-Operators auf die Tabelle an und bestimmt geeignete Zeilen. Beispiel:  
  
```sql  
SELECT * FROM stretch_table_name CROSS APPLY fn_stretchpredicate(column1, column2)  
```  
  
 Wenn die Funktion ein nicht leeres Ergebnis für die Zeile zurückgibt, ist die Zeile für die Migration geeignet.  
  
## <a name="replacePredicate"></a>Ersetzen einer vorhandenen Filterfunktion  
 Sie können eine zuvor angegebene Filterfunktion ersetzen, indem Sie die **ALTER TABLE** -Anweisung erneut ausführen und einen neuen Wert für den Parameter **FILTER_PREDICATE** angeben. Beispiel:  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = dbo.fn_stretchpredicate2(column1, column2),  
    MIGRATION_STATE = <desired_migration_state>  
  
```  
  
 Die neue Inline-Tabellenwertfunktion hat die folgenden Anforderungen.  
  
-   Die neue Funktion muss weniger restriktiv als die vorherige Funktion sein.  
  
-   Alle Operatoren, die in der alten Funktion vorhanden waren, müssen in der neuen Funktion vorhanden sein.  
  
-   Die neue Funktion darf keine Operatoren enthalten, die in der alten Funktion nicht vorhanden waren.  
  
-   Der Reihenfolge der Operatorargumente kann sich nicht ändern.  
  
-   Nur konstante Werte, die Teil eines `<, <=, >, >=`  -Vergleichs sind, können in einer Weise geändert werden, die die Funktion weniger restriktiv macht.  
  
### <a name="example-of-a-valid-replacement"></a>Beispiel einer gültigen Ersetzung  
 Angenommen, die folgende Funktion ist die aktuelle Filterfunktion.  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate_old(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
GO  
  
```  
  
 Die folgende Funktion ist eine gültige Ersetzung, da die neue Datumskonstante (die ein späteres Umstellungsdatum angibt) die Funktion weniger restriktiv macht.  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate_new(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '2/1/2016', 101)  
            AND (@column2 < -50 OR @column2 > 50)  
GO  
  
```  
  
### <a name="examples-of-replacements-that-arent-valid"></a>Beispiele für ungültige Ersetzungen  
 Die folgende Funktion ist keine gültige Ersetzung, da die neue Datumskonstante (die ein früheres Umstellungsdatum angibt) die Funktion nicht weniger restriktiv macht.  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_1(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2015', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
GO  
  
```  
  
 Die folgende Funktion ist keine gültige Ersetzung, weil einer der Vergleichsoperatoren entfernt wurde.  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_2(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -50)  
GO  
  
```  
  
 Die folgende Funktion ist keine gültige Ersetzung, da eine neue Bedingung mit dem logischen Operator AND hinzugefügt wurde.  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_3(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
            AND (@column2 <> 0)  
GO  
  
```  
  
## <a name="remove-a-filter-function-from-a-table"></a>Entfernen einer Filterfunktion von einer Tabelle  
 Entfernen Sie die vorhandene Funktion, indem Sie **FILTER_PREDICATE**  auf NULL festlegen, um anstelle ausgewählter Zeilen die gesamte Tabelle zu migrieren. Beispiel:  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = NULL,  
    MIGRATION_STATE = <desired_migration_state>  
) )  
  
```  
  
 Nachdem Sie die Filterfunktion entfernt haben, sind alle Zeilen in der Tabelle für die Migration geeignet. Sie können daher nicht später eine Filterfunktion für dieselbe Tabelle angeben, es sei denn, Sie bringen zuerst alle Remotedaten für die Tabelle von Azure zurück. Diese Einschränkung gilt, um die Situation zu vermeiden, in der Zeilen, die nicht für die Migration geeignet sind, bei Angabe einer neuen Filterfunktion bereits in Azure migriert wurden.  
  
## <a name="check-the-filter-function-applied-to-a-table"></a>Überprüfen der auf eine Tabelle angewendeten Filterfunktion  
 Öffnen Sie zum Überprüfen der Filterfunktion, die auf eine Tabelle angewendet wurde, die Katalogsicht **sys.remote_data_archive_tables** , und überprüfen Sie den Wert der Spalte **filter_predicate** . Falls der Wert NULL ist, ist die gesamte Tabelle für die Archivierung geeignet. Weitere Informationen finden Sie unter [sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md).  
  
## <a name="security-notes-for-filter-functions"></a>Sicherheitshinweise für Filterfunktionen  
Ein kompromittiertes Konto mit db_owner-Berechtigungen kann folgende Aktionen ausführen.  
  
-   Erstellen und Anwenden einer Tabellenwertfunktion, die große Mengen an Serverressourcen verbraucht oder für einen längeren Zeitraum wartet, was zu einem Denial of Service führt.  
  
-   Erstellen und Anwenden einer Tabellenwertfunktion, die es ermöglicht, den Inhalt einer Tabelle abzuleiten, für die dem Benutzer explizit der Lesezugriff verweigert wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
