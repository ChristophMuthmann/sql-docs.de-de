---
title: SET ARITHABORT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ARITHABORT_TSQL
- ARITHABORT
- SET ARITHABORT
- SET_ARITHABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- terminating queries
- queries [SQL Server], terminating
- overflow errors [SQL Server]
- ARITHABORT option
- divide-by-zero errors
- SET ARITHABORT statement
- ending queries [SQL Server]
- stopping queries
ms.assetid: f938a666-fdd1-4233-b97f-719f27b1a0e6
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3699e84e04e821cdc982f957a88bd8b181ebdd25
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-arithabort-transact-sql"></a>SET ARITHABORT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Beendet eine Abfrage, wenn während der Abfrage ein Überlauffehler oder ein Fehler aufgrund einer Division durch Null auftritt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```
-- Syntax for SQL Server and Azure SQL Database
  
SET ARITHABORT { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ARITHABORT ON
```
  
## <a name="remarks"></a>Remarks  
 Sie sollten ARITHABORT in Anmeldesitzungen immer auf ON festlegen. Wenn ARITHABORT auf OFF festgelegt wird, kann dies negative Auswirkungen auf die Abfrageoptimierung haben und zu Leistungsproblemen führen.  
  
> [!WARNING]  
>  Der Standardwert der ARITHABORT-Einstellung für [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ist ON. Wenn ARITHABORT für Clientanwendungen auf OFF festgelegt ist, können diese unterschiedliche Abfragepläne empfangen, was die Problembehandlung von Abfragen mit schlechter Leistung erschwert. Das heißt, dieselbe Abfrage kann in Management Studio schnell, in der Anwendung jedoch langsam ausgeführt werden. Gleichen Sie die ARITHABORT-Einstellung des Clients bei der Problembehandlung von Abfragen mit [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] immer ab.  
  
 Wenn SET ARITHABORT auf ON und SET ANSI WARNINGS auf ON festgelegt ist, bewirken diese Fehlerbedingungen, dass die Abfrage beendet wird.  
  
 Wenn SET ARITHABORT auf ON und SET ANSI WARNINGS auf OFF festgelegt ist, bewirken diese Fehlerbedingungen, dass der Batch beendet wird. Treten die Fehler in einer Transaktion auf, so wird für die Transaktion ein Rollback durchgeführt. Wenn SET ARITHABORT auf OFF festgelegt ist und einer dieser Fehler auftritt, wird eine Warnmeldung angezeigt und dem Ergebnis der arithmetischen Operation NULL zugewiesen.  
  
 Wenn SET ARITHABORT und SET ANSI WARNINGS auf OFF festgelegt sind und einer dieser Fehler auftritt, wird eine Warnmeldung angezeigt und dem Ergebnis der arithmetischen Operation NULL zugewiesen.  
  
> [!NOTE]  
>  Wenn weder SET ARITHABORT noch SET ARITHIGNORE festgelegt sind, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULL zurück und gibt nach dem Ausführen der Abfrage eine Warnmeldung zurück.  
  
 Durch Festlegen von ANSI_WARNINGS auf ON wird implizit ARITHABORT auf ON festgelegt, wenn der Kompatibilitätsgrad der Datenbank auf 90 oder höher festgelegt ist. Wird der Kompatibilitätsgrad der Datenbank auf 80 oder niedriger festgelegt, muss die ARITHABORT-Option explizit auf ON festgelegt werden.  
  
 Wenn in einer INSERT-, DELETE- oder UPDATE-Anweisung ein arithmetischer Fehler (Überlauf, Division durch Null oder Bereichsfehler) bei der Auswertung eines Ausdrucks auftritt und SET ARITHABORT auf OFF festgelegt ist, fügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen NULL-Wert ein oder aktualisiert ihn. Wenn die Zielspalte keine NULL-Werte zulässt, schlägt das Einfügen oder Aktualisieren fehl, und dem Benutzer wird ein Fehler angezeigt.  
  
 Auch wenn SET ARITHABORT oder SET ARITHIGNORE auf OFF und SET ANSI_WARNINGS auf ON festgelegt sind, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Fehlermeldung zurück, wenn ein Fehler aufgrund einer Division durch Null oder ein Überlauffehler auftritt.  
  
 Wenn SET ARITHABORT auf OFF festgelegt ist und bei der Auswertung der booleschen Bedingung einer IF-Anweisung ein Abbruchfehler auftritt, wird der FALSE-Zweig ausgeführt.
  
 SET ARITHABORT muss beim Erstellen oder Ändern von Indizes für berechnete Spalten oder indizierte Sichten auf ON festgelegt sein. Wenn SET ARITHABORT auf OFF festgelegt ist, schlagen die CREATE-, UPDATE-, INSERT- und DELETE-Anweisungen in Tabellen mit Indizes auf berechneten Spalten oder indizierten Sichten fehl.
  
 Die Einstellung von SET ARITHABORT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus:
  
```  
DECLARE @ARITHABORT VARCHAR(3) = 'OFF';  
IF ( (64 & @@OPTIONS) = 64 ) SET @ARITHABORT = 'ON';  
SELECT @ARITHABORT AS ARITHABORT;  
  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Fehler aufgrund einer Division durch Null und Überlauffehler mit beiden `SET ARITHABORT`-Einstellungen veranschaulicht.  
  
```  
-- SET ARITHABORT  
-------------------------------------------------------------------------------  
-- Create tables t1 and t2 and insert data values.  
CREATE TABLE t1 (  
   a TINYINT,   
   b TINYINT  
);  
CREATE TABLE t2 (  
   a TINYINT  
);  
GO  
INSERT INTO t1   
VALUES (1, 0);  
INSERT INTO t1   
VALUES (255, 1);  
GO  
  
PRINT '*** SET ARITHABORT ON';  
GO  
-- SET ARITHABORT ON and testing.  
SET ARITHABORT ON;  
GO  
  
PRINT '*** Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab   
FROM t1;  
GO  
  
PRINT '*** Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
  
PRINT '*** Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '*** Resulting data - should be no data';  
GO  
SELECT *   
FROM t2;  
GO  
  
-- Truncate table t2.  
TRUNCATE TABLE t2;  
GO  
  
-- SET ARITHABORT OFF and testing.  
PRINT '*** SET ARITHABORT OFF';  
GO  
SET ARITHABORT OFF;  
GO  
  
-- This works properly.  
PRINT '*** Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab    
FROM t1;  
GO  
  
-- This works as if SET ARITHABORT was ON.  
PRINT '*** Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
PRINT '*** Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '*** Resulting data - should be 0 rows';  
GO  
SELECT *   
FROM t2;  
GO  
  
-- Drop tables t1 and t2.  
DROP TABLE t1;  
DROP TABLE t2;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ARITHIGNORE &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithignore-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
