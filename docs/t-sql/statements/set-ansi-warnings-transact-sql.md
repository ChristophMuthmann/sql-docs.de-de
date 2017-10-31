---
title: SET ANSI_WARNINGS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: feee804808cb9ba8d6e3dd97fb512a3a73301e17
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansiwarnings-transact-sql"></a>SET ANSI_WARNINGS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt das ISO-Standardverhalten für verschiedene Fehlerbedingungen an.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET ANSI_WARNINGS { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_WARNINGS ON;  
```  
  
## <a name="remarks"></a>Hinweise  
 SET ANSI_WARNINGS betrifft die folgenden Bedingungen:  
  
-   Bei ON wird eine Warnmeldung generiert, wenn NULL-Werte in Aggregatfunktionen, wie z. B. SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP oder COUNT, auftreten. Wenn OFF festgelegt, wird keine Warnung ausgegeben.  
  
-   Bei ON bewirken Fehler aufgrund einer Division durch Null und arithmetische Überlauffehler, dass für die Anweisung ein Rollback ausgeführt und eine Fehlermeldung generiert wird. Bei OFF bewirken Fehler aufgrund einer Division durch Null und arithmetische Überlauffehler, dass NULL-Werte zurückgegeben werden. Das Verhalten in der ein Fehler aufgrund einer Division durch null oder arithmetische Überlauffehler bewirken, dass null-Werte zurückgegeben werden, tritt auf, wenn eine INSERT- oder UPDATE versucht wird, auf eine **Zeichen**, Unicode oder **binäre** Spalte, in der die Länge ein neuer Wert ist größer als die Maximalgröße der Spalte. Wenn SET ANSI_WARNINGS ON ist, der INSERT- oder UPDATE wird abgebrochen, gemäß dem ISO-Standard. Nachfolgende Leerzeichen werden in Zeichenspalten ignoriert, und nachfolgende Nullen werden in Binärspalten ignoriert. Bei OFF werden Daten auf die Spaltengröße abgeschnitten, und die Anweisung wird erfolgreich ausgeführt.  
  
    > [!NOTE]  
    >  Bei Kürzung in beliebigen Konvertierungen in oder aus **binäre** oder **Varbinary** Daten, die keine Warnungen oder Fehler ausgegeben wird, unabhängig von der SET-Optionen.  
  
    > [!NOTE]  
    >  ANSI_WARNINGS wird beim Übergeben von Parametern in einer gespeicherten Prozedur oder einer benutzerdefinierten Funktion oder beim Deklarieren und Festlegen von Variablen in einer Batchanweisung nicht berücksichtigt. Angenommen, eine Variable definiert ist, als **char(3)**, und klicken Sie dann auf einen Wert größer als 3 Zeichen festgelegt, die Daten auf die definierte Größe und die Einfügung abgeschnitten oder UPDATE-Anweisung erfolgreich ausgeführt wird.  
  
 Mithilfe der Benutzeroptionen-Option von sp_configure können Sie die Standardeinstellung für ANSI_WARNINGS für alle Verbindungen mit dem Server festlegen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)noch nicht kennen.  
  
 SET ANSI_WARNINGS muss beim Erstellen oder Bearbeiten von Indizes für berechnete Spalten oder indizierte Sichten auf ON festgelegt sein. Wenn SET ANSI_WARNINGS auf OFF festgelegt ist, schlagen die CREATE-, UPDATE-, INSERT- und DELETE-Anweisungen in Tabellen mit Indizes auf berechneten Spalten oder indizierten Sichten fehl. Weitere Informationen zu den erforderlichen Einstellungen der SET-Option mit indizierten Sichten und Indizes für berechnete Spalten finden Sie unter "Überlegungen beim Sie mithilfe der SET-Anweisungen in [SET-Anweisungen &#40; Transact-SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schließt die ANSI_WARNINGS-Datenbankoption ein. Diese entspricht SET ANSI_WARNINGS. Wenn SET ANSI_WARNINGS auf ON festgelegt ist, werden Fehler- oder Warnmeldungen bei Division durch Null, bei einer für eine Datenbankspalte zu großen Zeichenfolge und bei ähnlichen Fehlern ausgelöst. Wenn SET ANSI_WARNINGS auf OFF festgelegt ist, werden diese Fehler und Warnungen nicht ausgelöst. Der Standardwert in der model-Datenbank für SET ANSI_WARNINGS ist OFF. Wird kein Wert angegeben, gilt die Einstellung von ANSI_WARNINGS. Wenn SET ANSI_WARNINGS auf OFF festgelegt ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet den Wert der Is_ansi_warnings_on-Spalte in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt.  
  
 ANSI_WARNINGS sollte zum Ausführen von verteilten Abfragen auf ON festgelegt sein.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch ANSI_WARNINGS auf ON festgelegt, wenn eine Verbindung herstellen. Diese Einstellung kann in ODBC-Datenquellen und ODBC-Verbindungsattributen konfiguriert werden, die in der Anwendung festgelegt werden, bevor die Verbindung hergestellt wird. Der Standardwert für SET ANSI_WARNINGS für Verbindungen von DB-Library-Anwendungen ist OFF.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [SESSIONPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  

