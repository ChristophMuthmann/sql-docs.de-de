---
title: SET ANSI_WARNINGS (Transact-SQL) | Microsoft-Dokumentation
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
- SET ANSI_WARNINGS
- ANSI_WARNINGS_TSQL
- ANSI_WARNINGS
- SET_ANSI_WARNINGS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], ISO standard behavior
- warnings [SQL Server]
- SET ANSI_WARNINGS statement
- ANSI_WARNINGS option
ms.assetid: f82aaab0-334f-427b-89b0-de4af596b4fa
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9adfe935ef69c55f44c62906eeedb90a968b7260
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-ansiwarnings-transact-sql"></a>SET ANSI_WARNINGS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt das ISO-Standardverhalten für verschiedene Fehlerbedingungen an.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax
  
```
-- Syntax for SQL Server and Azure SQL Database
  
SET ANSI_WARNINGS { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_WARNINGS ON
```

## <a name="remarks"></a>Remarks  
 SET ANSI_WARNINGS betrifft die folgenden Bedingungen:  
  
-   Bei ON wird eine Warnmeldung generiert, wenn NULL-Werte in Aggregatfunktionen, wie z. B. SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP oder COUNT, auftreten. Bei OFF wird keine Warnung ausgegeben.  
  
-   Bei ON bewirken Fehler aufgrund einer Division durch Null und arithmetische Überlauffehler, dass für die Anweisung ein Rollback ausgeführt und eine Fehlermeldung generiert wird. Bei OFF bewirken Fehler aufgrund einer Division durch Null und arithmetische Überlauffehler, dass NULL-Werte zurückgegeben werden. Das Verhalten, bei dem Fehler aufgrund einer Division durch 0 (null) oder arithmetischer Überlauffehler bewirken, dass NULL-Werte zurückgegeben werden, tritt auf, wenn ein INSERT- oder UPDATE-Vorgang in einer Spalte des Typs **character**, Unicode oder **binary** versucht wird und die Länge eines der neuen Werte die maximale Spaltengröße überschreitet. Wenn SET ANSI_WARNINGS auf ON festgelegt ist, wird der INSERT- oder UPDATE-Vorgang gemäß ISO-Standard abgebrochen. Nachfolgende Leerzeichen werden in Zeichenspalten ignoriert, und nachfolgende Nullen werden in Binärspalten ignoriert. Bei OFF werden Daten auf die Spaltengröße abgeschnitten, und die Anweisung wird erfolgreich ausgeführt.  
  
    > [!NOTE]  
    >  Wenn Abschneidevorgänge bei beliebigen Konvertierungen in oder von **binary**- oder **varbinary**-Daten auftreten, werden keine Warnungen oder Fehler ausgelöst, unabhängig von den SET-Optionen.  
  
    > [!NOTE]  
    >  ANSI_WARNINGS wird beim Übergeben von Parametern in einer gespeicherten Prozedur oder einer benutzerdefinierten Funktion oder beim Deklarieren und Festlegen von Variablen in einer Batchanweisung nicht berücksichtigt. Wird beispielsweise eine Variable als **char(3)** definiert und dann auf einen Wert festgelegt, der länger als drei Zeichen ist, werden die Daten auf die definierte Größe abgeschnitten, und die Anweisung INSERT oder UPDATE wird erfolgreich ausgeführt.  
  
 Mithilfe der Benutzeroptionen-Option von sp_configure können Sie die Standardeinstellung für ANSI_WARNINGS für alle Verbindungen mit dem Server festlegen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)noch nicht kennen.  
  
 SET ANSI_WARNINGS muss beim Erstellen oder Bearbeiten von Indizes für berechnete Spalten oder indizierte Sichten auf ON festgelegt sein. Wenn SET ANSI_WARNINGS auf OFF festgelegt ist, schlagen die CREATE-, UPDATE-, INSERT- und DELETE-Anweisungen in Tabellen mit Indizes auf berechneten Spalten oder indizierten Sichten fehl. Weitere Informationen zu den erforderlichen Einstellungen der SET-Option mit indizierten Sichten und Indizes für berechnete Spalten finden Sie in den Überlegungen zum Verwenden der SET-Anweisungen unter [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schließt die ANSI_WARNINGS-Datenbankoption ein. Diese entspricht SET ANSI_WARNINGS. Wenn SET ANSI_WARNINGS auf ON festgelegt ist, werden Fehler- oder Warnmeldungen bei Division durch Null, bei einer für eine Datenbankspalte zu großen Zeichenfolge und bei ähnlichen Fehlern ausgelöst. Wenn SET ANSI_WARNINGS auf OFF festgelegt ist, werden diese Fehler und Warnungen nicht ausgelöst. Der Standardwert in der model-Datenbank für SET ANSI_WARNINGS ist OFF. Wird kein Wert angegeben, gilt die Einstellung von ANSI_WARNINGS. Wird SET ANSI_WARNINGS auf OFF festgelegt, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Wert der is_ansi_warnings_on-Spalte in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)-Katalogsicht.  
  
 ANSI_WARNINGS sollte zum Ausführen von verteilten Abfragen auf ON festgelegt sein.  
  
 Der ODBC-Treiber von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client und der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] legen für ANSI_WARNINGS beim Herstellen einer Verbindung automatisch ON fest. Diese Einstellung kann in ODBC-Datenquellen und ODBC-Verbindungsattributen konfiguriert werden, die in der Anwendung festgelegt werden, bevor die Verbindung hergestellt wird. Der Standardwert für SET ANSI_WARNINGS für Verbindungen von DB-Library-Anwendungen ist OFF.  
  
 Ist SET ANSI_DEFAULTS auf ON festgelegt, so ist SET ANSI_WARNINGS aktiviert.  
  
 Die Einstellung von SET ANSI_WARNINGS wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Auch wenn SET ARITHABORT oder SET ARITHIGNORE auf OFF und SET ANSI_WARNINGS auf ON festgelegt sind, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Fehlermeldung zurück, wenn ein Fehler aufgrund einer Division durch Null oder ein Überlauffehler auftritt.  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus.  
  
```  
DECLARE @ANSI_WARN VARCHAR(3) = 'OFF';  
IF ( (8 & @@OPTIONS) = 8 ) SET @ANSI_WARN = 'ON';  
SELECT @ANSI_WARN AS ANSI_WARNINGS;  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die drei zuvor beschriebenen Situationen gezeigt, wobei SET ANSI_WARNINGS von ON auf OFF wechselt.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE T1   
(  
   a int,   
   b int NULL,   
   c varchar(20)  
);  
GO  
  
SET NOCOUNT ON;  
  
INSERT INTO T1   
VALUES (1, NULL, '')   
      ,(1, 0, '')  
      ,(2, 1, '')  
      ,(2, 2, '');  
  
SET NOCOUNT OFF;  
GO  
  
PRINT '**** Setting ANSI_WARNINGS ON';  
GO  
  
SET ANSI_WARNINGS ON;  
GO  
  
PRINT 'Testing NULL in aggregate';  
GO  
SELECT a, SUM(b)   
FROM T1   
GROUP BY a;  
GO  
  
PRINT 'Testing String Overflow in INSERT';  
GO  
INSERT INTO T1   
VALUES (3, 3, 'Text string longer than 20 characters');  
GO  
  
PRINT 'Testing Divide by zero';  
GO  
SELECT a / b AS ab   
FROM T1;  
GO  
  
PRINT '**** Setting ANSI_WARNINGS OFF';  
GO  
SET ANSI_WARNINGS OFF;  
GO  
  
PRINT 'Testing NULL in aggregate';  
GO  
SELECT a, SUM(b)   
FROM T1   
GROUP BY a;  
GO  
  
PRINT 'Testing String Overflow in INSERT';  
GO  
INSERT INTO T1   
VALUES (4, 4, 'Text string longer than 20 characters');  
GO  
SELECT a, b, c   
FROM T1  
WHERE a = 4;  
GO  
  
PRINT 'Testing Divide by zero';  
GO  
SELECT a / b AS ab   
FROM T1;  
GO  
  
DROP TABLE T1  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
