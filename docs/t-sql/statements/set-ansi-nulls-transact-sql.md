---
title: SET ANSI_NULLS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SET_ANSI_NULLS_TSQL
- ANSI_NULLS
- SET ANSI_NULLS
- ANSI_NULLS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET ANSI_NULLS statement
- not equal to operator (<>)
- ANSI_NULLS option
- equals operator (=)
- null values [SQL Server], comparison operators
- comparison operators [SQL Server], null values
ms.assetid: aae263ef-a3c7-4dae-80c2-cc901e48c755
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4581fc2b98249f58100f448c30ecb2975ccb593b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-ansinulls-transact-sql"></a>SET ANSI_NULLS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt an, dass sich die Vergleichsoperatoren Gleich (=) und Ungleich (<>) bei Verwendung mit NULL-Werten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ISO-konform verhalten müssen.  
  
> [!IMPORTANT]  
>  In einer späteren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird ANSI_NULLS auf ON festgelegt, und jede Anwendung, die für die Option explizit OFF festlegt, löst einen Fehler aus. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden.
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>Syntax

```
-- Syntax for SQL Server

SET ANSI_NULLS { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_NULLS ON
```

## <a name="remarks"></a>Remarks  
 Wenn SET ANSI_NULLS auf ON festgelegt ist, gibt eine SELECT-Anweisung, in der WHERE *column_name* = **NULL** verwendet wird, auch dann 0 Zeilen zurück, wenn sich NULL-Werte in *column_name* befinden. Eine SELECT-Anweisung, die WHERE *column_name* <> **NULL** verwendet, gibt auch dann 0 Zeilen zurück, wenn sich Werte ungleich NULL in *column_name* befinden.  
  
 Wenn SET ANSI_NULLS auf OFF festgelegt ist, folgen die Vergleichsoperatoren Gleich (=) und Ungleich (<>) nicht dem ISO-Standard. Eine SELECT-Anweisung, in der WHERE *column_name* = **NULL** verwendet wird, gibt die Zeilen zurück, die NULL-Werte in *column_name* enthalten. Eine SELECT-Anweisung, die WHERE *column_name* <> **NULL** verwendet, gibt die Zeilen mit Werten ungleich NULL in der Spalte zurück. Außerdem gibt eine SELECT-Anweisung, in der *column_name* <> *XYZ_value* verwendet wird, alle Zeilen zurück, die nicht gleich *XYZ_value* und nicht NULL sind.  
  
 Wenn SET ANSI_NULLS auf ON festgelegt ist, werden alle Vergleiche mit einem NULL-Wert zu UNKNOWN ausgewertet. Wenn SET ANSI_NULLS auf OFF festgelegt ist, werden alle Datenvergleiche mit einem NULL-Wert zu TRUE ausgewertet, falls der Datenwert NULL ist. Falls SET ANSI_NULLS nicht angegeben ist, gilt die Einstellung der Option ANSI_NULLS der aktuellen Datenbank. Weitere Informationen zur Datenbankoption ANSI_NULLS finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 SET ANSI_NULLS ON hat nur dann Auswirkungen auf einen Vergleich, wenn einer der Operanden des Vergleichs entweder eine Variable, die NULL ist, oder ein Literal NULL ist. Falls beide Seiten des Vergleichs Spalten oder zusammengesetzte Ausdrücke sind, hat die Einstellung keine Auswirkungen auf den Vergleich.  
  
 Ein Skript wird unabhängig von der Datenbankoption ANSI_NULLS und der Einstellung von SET ANSI_NULLS wie beabsichtigt ausgeführt, wenn Sie IS NULL und IS NOT NULL in Vergleichen verwenden, die möglicherweise NULL-Werte enthalten.  
  
 SET ANSI_NULLS muss zum Ausführen von verteilten Abfragen auf ON festgelegt sein.  
  
 SET ANSI_NULLS muss auch beim Erstellen oder Ändern von Indizes für berechnete Spalten oder indizierte Sichten auf ON festgelegt sein. Wenn SET ANSI_NULLS auf OFF festgelegt ist, schlagen die CREATE-, UPDATE-, INSERT- und DELETE-Anweisungen in Tabellen mit Indizes auf berechneten Spalten oder indizierten Sichten fehl. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt einen Fehler zurück, der alle SET-Optionen auflistet, die gegen die erforderlichen Werte verstoßen. Wenn SET ANSI_NULLS auf OFF festgelegt ist, ignoriert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Ausführen einer SELECT-Anweisung die Indexwerte für berechnete Spalten oder Sichten und löst den SELECT-Vorgang so auf, als seien keine derartigen Indizes für die Tabelle oder Sicht vorhanden.  
  
> [!NOTE]  
>  ANSI_NULLS ist eine der sieben SET-Optionen, für die bestimmte Werte beim Verwenden von Indizes auf berechneten Spalten oder indizierten Sichten festgelegt sein müssen. Die Optionen ANSI_PADDING, ANSI_WARNINGS, ARITHABORT, QUOTED_IDENTIFIER und CONCAT_NULL_YIELDS_NULL müssen ebenfalls auf ON festgelegt sein, NUMERIC_ROUNDABORT jedoch auf OFF.  
  
 Der ODBC-Treiber von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client und der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] legen ANSI_NULLS beim Herstellen einer Verbindung automatisch auf ON fest. Diese Einstellung kann in ODBC-Datenquellen, in ODBC-Verbindungsattributen oder in OLE DB-Verbindungseigenschaften konfiguriert werden, die in der Anwendung festgelegt werden, bevor die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hergestellt wird. Die Standardeinstellung für SET ANSI_NULLS ist OFF.  
  
 Ist SET ANSI_DEFAULTS auf ON festgelegt, so ist SET ANSI_NULLS aktiviert.  
  
 Die Einstellung von SET ANSI_NULLS wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus:
  
```  
DECLARE @ANSI_NULLS VARCHAR(3) = 'OFF';  
IF ( (32 & @@OPTIONS) = 32 ) SET @ANSI_NULLS = 'ON';  
SELECT @ANSI_NULLS AS ANSI_NULLS;  
  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden mithilfe der Vergleichsoperatoren Gleich (`=`) und Ungleich (`<>`) Vergleiche mit `NULL`-Werten und mit Werten ungleich NULL in einer Tabelle ausgeführt. Das Beispiel zeigt ebenfalls, dass `IS NULL` durch die `SET ANSI_NULLS`-Einstellung nicht beeinflusst wird.  
  
```  
-- Create table t1 and insert values.  
CREATE TABLE dbo.t1 (a INT NULL);  
INSERT INTO dbo.t1 values (NULL),(0),(1);  
GO  
  
-- Print message and perform SELECT statements.  
PRINT 'Testing default setting';  
DECLARE @varname int;   
SET @varname = NULL;  
  
SELECT a  
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to ON and test.  
PRINT 'Testing ANSI_NULLS ON';  
SET ANSI_NULLS ON;  
GO  
DECLARE @varname int;  
SET @varname = NULL  
  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to OFF and test.  
PRINT 'Testing SET ANSI_NULLS OFF';  
SET ANSI_NULLS OFF;  
GO  
DECLARE @varname int;  
SET @varname = NULL;  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- Drop table t1.  
DROP TABLE dbo.t1;  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [= &#40;Equals&#41; &#40;Transact-SQL&#41; (= &#40;ist gleich&#41; &#40;Transact-SQL&#41;)](../../t-sql/language-elements/equals-transact-sql.md)   
 [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [&#60;&#62; &#40;Ungleich&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  
