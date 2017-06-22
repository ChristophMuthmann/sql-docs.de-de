---
title: Verwenden von Tabellenwertparameter (Datenbankmodul) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table-valued parameters
- table-valued parameters, about table-valued parameters
- parameters [SQL Server], table-valued
- TVP See table-valued parameters
ms.assetid: 5e95a382-1e01-4c74-81f5-055612c2ad99
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 021177aa350c47474e48453f7d9a5735e1083b04
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="use-table-valued-parameters-database-engine"></a>Verwenden von Tabellenwertparameter (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Tabellenwertparameter werden mit benutzerdefinierten Tabellentypen deklariert. Mit Tabellenwertparametern können Sie mehrere Datenzeilen an eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung oder an eine Routine übergeben, z. B. eine gespeicherte Prozedur oder eine Funktion, ohne eine temporäre Tabelle oder viele Parameter erstellen zu müssen.  
  
 Tabellenwertparameter entsprechen Parameterarrays in OLE DB und ODBC, bieten jedoch eine größere Flexibilität und eine engere Integration mit [!INCLUDE[tsql](../../includes/tsql-md.md)]. Ein weiterer Vorteil von Tabellenwertparametern besteht darin, dass sie in setbasierten Vorgängen verwendet werden können.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] übergibt Tabellenwertparameter mittels Verweise an Routinen, sodass keine Kopie der Eingabedaten erstellt werden muss. Sie können [!INCLUDE[tsql](../../includes/tsql-md.md)] -Routinen mit Tabellenwertparametern erstellen und ausführen und diese über [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code, verwaltete und Native Clients in jeder beliebigen verwalteten Sprache aufrufen.  
  
 **In diesem Thema:**  
  
 [Vorteile](#Benefits)  
  
 [Einschränkungen](#Restrictions)  
  
 [Tabellenwertparameter im Vergleich zu BULK INSERT-Vorgängen](#BulkInsert)  
  
 [Beispiel](#Example)  
  
##  <a name="Benefits"></a> Vorteile  
 Der Bereich eines Tabellenwertparameters entspricht wie auch bei anderen Parametern der gespeicherten Prozedur, der Funktion oder dem dynamischen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Text. Ebenso entspricht der Bereich einer Tabellentypvariablen dem Bereich einer beliebigen lokalen Variablen, die mit einer DECLARE-Anweisung erstellt wurde. Sie können Tabellenwertvariablen in dynamischen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen deklarieren und diese Variablen dann als Tabellenwertparameter an gespeicherte Prozeduren und Funktionen übergeben.  
  
 Tabellenwertparameter bieten mehr Flexibilität und in einigen Fällen auch eine bessere Systemleistung als temporäre Tabellen oder andere Methoden zum Übergeben von Parameterlisten. Tabellenwertparameter bieten die folgenden Vorteile:  
  
-   Erfordern keine Sperren für die erste Auffüllung mit Daten von einem Client  
  
-   Stellen ein einfaches Programmiermodell bereit  
  
-   Ermöglichen die Einbindung komplexer Geschäftslogik in eine einzelne Routine  
  
-   Weniger Roundtrips zum Server  
  
-   Unterstützen Tabellenstrukturen mit unterschiedlicher Kardinalität  
  
-   Weisen eine starke Typbindung auf  
  
-   Ermöglichen die Angabe von Sortierreihenfolge und eindeutigen Schlüsseln über den Client  
  
-   Werden bei der Verwendung in einer gespeicherten Prozedur wie eine temporäre Tabelle zwischengespeichert. Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]werden Tabellenwertparameter auch für parametrisierte Abfragen zwischengespeichert.  
  
##  <a name="Restrictions"></a> Einschränkungen  
 Für Tabellenwertparameter gelten die folgenden Einschränkungen:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Spaltenstatistiken für Tabellenwertparameter werden nicht verwaltet.  
  
-   Tabellenwertparameter müssen als READONLY-Eingabeparameter an [!INCLUDE[tsql](../../includes/tsql-md.md)] -Routinen übergeben werden. Für Tabellenwertparameter im Hauptteil einer Routine können keine DML-Vorgänge wie UPDATE, DELETE oder INSERT durchgeführt werden.  
  
-   Tabellenwertparameter können nicht als Ziel einer SELECT INTO-Anweisung oder einer INSERT EXEC-Anweisung verwendet werden. Tabellenwertparameter können in der FROM-Klausel von SELECT INTO oder in der Zeichenfolge oder gespeicherten Prozedur von INSERT EXEC enthalten sein.  
  
##  <a name="BulkInsert"></a> Tabellenwertparameter vs. BULK INSERT-Vorgänge  
 Die Verwendung von Tabellenwertparametern ist mit anderen Methoden zur Verwendung setbasierter Variablen vergleichbar. Sehr große Datasets können mit Tabellenwertparametern jedoch häufig schneller verarbeitet werden. Im Vergleich zu Massenvorgängen, bei denen die Startkosten höher sind, eignen sich Tabellenwertparameter optimal zum Einfügen von weniger als 1000 Zeilen.  
  
 Wiederverwendete Tabellenparameter nutzen den Zwischenspeicher für temporäre Tabellen. Diese Zwischenspeicherung ermöglicht eine bessere Skalierbarkeit als vergleichbare BULK INSERT-Vorgänge. Bei kleineren Vorgängen zum Einfügen von Zeilen können Sie u. U. eine bessere Leistung erzielen, wenn Sie Parameterlisten oder Batch-Anweisungen statt BULK INSERT-Vorgänge oder Tabellenwertparameter verwenden. Die Programmierung dieser Methoden ist allerdings komplexer, und die Leistung nimmt mit steigender Zeilenanzahl schnell ab.  
  
 Tabellenwertparameter eignen sich mindestens so gut wie vergleichbare Parameterarray-Implementierungen.  
  
##  <a name="Example"></a> Beispiel  
 Im folgenden Beispiel wird [!INCLUDE[tsql](../../includes/tsql-md.md)] verwendet. Es zeigt, wie Sie einen Tabellenwertparameter erstellen, eine Variable deklarieren, die darauf verweist, Daten in die Parameterliste einfügen und die Werte dann an eine gespeicherte Prozedur übergeben.  
  
```  
USE AdventureWorks2012;  
GO  
  
/* Create a table type. */  
CREATE TYPE LocationTableType AS TABLE   
( LocationName VARCHAR(50)  
, CostRate INT );  
GO  
  
/* Create a procedure to receive data for the table-valued parameter. */  
CREATE PROCEDURE dbo. usp_InsertProductionLocation  
    @TVP LocationTableType READONLY  
    AS   
    SET NOCOUNT ON  
    INSERT INTO AdventureWorks2012.Production.Location  
           (Name  
           ,CostRate  
           ,Availability  
           ,ModifiedDate)  
        SELECT *, 0, GETDATE()  
        FROM  @TVP;  
        GO  
  
/* Declare a variable that references the type. */  
DECLARE @LocationTVP AS LocationTableType;  
  
/* Add data to the table variable. */  
INSERT INTO @LocationTVP (LocationName, CostRate)  
    SELECT Name, 0.00  
    FROM AdventureWorks2012.Person.StateProvince;  
  
/* Pass the table variable data to a stored procedure. */  
EXEC usp_InsertProductionLocation @LocationTVP;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [DEKLARIEREN SIE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys.parameter_type_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
  
  
