---
title: Parameter | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- user-defined functions [SQL Server], parameters
ms.assetid: c1f9bd93-3271-4098-a23b-7bd7a19ab65b
caps.latest.revision: 2
author: pmasl
ms.author: pelopes
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6ce682595af9808521480f0b1360ec57f33f0706
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="parameters"></a>Parameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Parameter werden zum Austauschen von Daten zwischen gespeicherten Prozeduren und Funktionen und der Anwendung bzw. dem Tool verwendet, von der bzw. von dem die gespeicherte Prozedur oder Funktion aufgerufen wurde. 

*  Eingabeparameter ermöglichen dem Aufrufer die Übergabe eines Datenwerts an die gespeicherte Prozedur oder die Funktion.
*  Ausgabeparameter ermöglichen der gespeicherten Prozedur das Übergeben eines Datenwerts oder einer Cursorvariablen zurück an den Aufrufer. Benutzerdefinierte Funktionen können keine Ausgabeparameter angeben.
*  Jede gespeicherte Prozedur gibt einen ganzzahligen Rückgabecode an den Aufrufer zurück. Falls die gespeicherte Prozedur nicht explizit einen Wert für den Rückgabecode festlegt, ist der Rückgabecode 0.

Die folgende gespeicherte Prozedur zeigt die Verwendung eines Eingabeparameters, eines Ausgabeparameters und eines Rückgabecodes:
```
-- Create a procedure that takes one input parameter and returns one output parameter and a return code.
CREATE PROCEDURE SampleProcedure @EmployeeIDParm INT,
         @MaxTotal INT OUTPUT
AS
-- Declare and initialize a variable to hold @@ERROR.
DECLARE @ErrorSave INT
SET @ErrorSave = 0

-- Do a SELECT using the input parameter.
SELECT FirstName, LastName, JobTitle
FROM HumanResources.vEmployee
WHERE EmployeeID = @EmployeeIDParm

-- Save any nonzero @@ERROR value.
IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Set a value in the output parameter.
SELECT @MaxTotal = MAX(TotalDue)
FROM Sales.SalesOrderHeader;

IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Returns 0 if neither SELECT statement had an error; otherwise, returns the last error.
RETURN @ErrorSave
GO
```

Wenn eine gespeicherte Prozedur oder eine Funktion ausgeführt wird, können die Eingabeparameter entweder auf eine Konstante festgelegt werden oder den Wert einer Variablen verwenden. Ausgabeparameter und Rückgabecodes müssen ihre Werte in eine Variable zurückgeben. Parameter und Rückgabecodes können Datenwerte mit Transact-SQL-Variablen oder Anwendungsvariablen austauschen.

Falls eine gespeicherte Prozedur von einem Batch oder Skript aufgerufen wird, können für die Parameter und Rückgabecodewerte im selben Batch definierte Transact-SQL-Variablen verwendet werden. Das folgende Beispiel ist ein Batch, der die zuvor erstellte Prozedur ausführt. Der Eingabeparameter wird als Konstante angegeben; die Werte des Ausgabeparameters und des Rückgabecodes werden in Transact-SQL-Variablen gespeichert:
```
-- Declare the variables for the return code and output parameter.
DECLARE @ReturnCode INT
DECLARE @MaxTotalVariable INT

-- Execute the stored procedure and specify which variables
-- are to receive the output parameter and return code values.
EXEC @ReturnCode = SampleProcedure @EmployeeIDParm = 19,
   @MaxTotal = @MaxTotalVariable OUTPUT

-- Show the values returned.
PRINT ' '
PRINT 'Return code = ' + CAST(@ReturnCode AS CHAR(10))
PRINT 'Maximum Quantity = ' + CAST(@MaxTotalVariable AS CHAR(10))
GO
```

Eine Anwendung kann an Programmvariablen gebundene Parametermarkierungen zum Austausch von Daten zwischen Anwendungsvariablen, Parametern und Rückgabecodes verwenden.

## <a name="see-also"></a>Weitere Informationen finden Sie unter
[CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)   
 [Parameter und Wiederverwendung von Ausführungsplänen](../../relational-databases/query-processing-architecture-guide.md)   
 [Variablen (Transact-SQL)](../../t-sql/language-elements/variables-transact-sql.md)
