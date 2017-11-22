---
title: SET NUMERIC_ROUNDABORT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NUMERIC_ROUNDABORT
- SET_NUMERIC_ROUNDABORT_TSQL
- SET NUMERIC_ROUNDABORT
- NUMERIC_ROUNDABORT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- rounding expressions
- precision [SQL Server], rounded expressions
- expressions [SQL Server], rounding
- NUMERIC_ROUNDABORT
- SET NUMERIC_ROUNDABORT statement
ms.assetid: d20e74f1-b8da-466c-b180-9d8a8b851a77
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a78c81a9990b2a9c895776c5f51fe9046b2eb5d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="set-numericroundabort-transact-sql"></a>SET NUMERIC_ROUNDABORT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt an, welche Fehlerberichtsstufe generiert wird, wenn beim Runden in einem Ausdruck Genauigkeitsverluste entstehen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET NUMERIC_ROUNDABORT { ON | OFF }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET NUMERIC_ROUNDABORT ON;  
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn SET NUMERIC_ROUNDABORT auf ON festgelegt ist, wird ein Fehler generiert, wenn ein Genauigkeitsverlust in einem Ausdruck aufgetreten ist. Bei der Einstellung OFF werden bei Genauigkeitsverlusten keine Fehlermeldungen generiert, und das Ergebnis wird auf die Genauigkeit der Spalte oder Variablen gerundet, die das Ergebnis speichert.  
  
 Ein Genauigkeitsverlust entsteht, wenn ein Wert mit fester Genauigkeit in einer Spalte oder Variablen mit geringerer Genauigkeit gespeichert wird.  
  
 Wenn SET NUMERIC_ROUNDABORT auf ON festgelegt ist, bestimmt SET ARITHABORT den Schweregrad des generierten Fehlers. Die folgende Tabelle zeigt die Auswirkungen dieser beiden Einstellungen im Falle eines Genauigkeitsverlusts.  
  
|Einstellung|SET NUMERIC_ROUNDABORT ON|SET NUMERIC_ROUNDABORT OFF|  
|-------------|--------------------------------|---------------------------------|  
|SET ARITHABORT ON|Fehler wird generiert; es wird kein Resultset zurückgegeben.|Keine Fehler oder Warnungen, Ergebnis wird gerundet.|  
|SET ARITHABORT OFF|Warnung wird zurückgegeben; Ausdruck gibt NULL zurück.|Keine Fehler oder Warnungen, Ergebnis wird gerundet.|  
  
 Die Einstellung von SET NUMERIC_ROUNDABORT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 SET NUMERIC_ROUNDABORT muss beim Erstellen oder Ändern von Indizes für berechneten Spalten oder indizierte Sichten auf OFF festgelegt sein. Wenn SET NUMERIC_ROUNDABORT auf ON festgelegt ist, schlagen die CREATE-, UPDATE-, INSERT- und DELETE-Anweisungen in Tabellen mit Indizes für berechnete Spalten oder indizierte Sichten fehl. Weitere Informationen zu den erforderlichen Einstellungen der SET-Option mit indizierten Sichten und Indizes für berechnete Spalten finden Sie unter "Überlegungen beim Sie mithilfe der SET-Anweisungen in [SET-Anweisungen &#40; Transact-SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus.  
  
```  
DECLARE @NUMERIC_ROUNDABORT VARCHAR(3) = 'OFF';  
IF ( (8192 & @@OPTIONS) = 8192 ) SET @NUMERIC_ROUNDABORT = 'ON';  
SELECT @NUMERIC_ROUNDABORT AS NUMERIC_ROUNDABORT;  
  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden zwei Werte mit einer Genauigkeit von vier Dezimalstellen addiert und in einer Variablen mit einer Genauigkeit von zwei Dezimalstellen gespeichert. Die Ausdrücke zeigen die Auswirkungen der unterschiedlichen `SET NUMERIC_ROUNDABORT`- und `SET ARITHABORT`-Einstellungen.  
  
```  
-- SET NOCOUNT to ON,   
-- SET NUMERIC_ROUNDABORT to ON, and SET ARITHABORT to ON.  
SET NOCOUNT ON;  
PRINT 'SET NUMERIC_ROUNDABORT ON';  
PRINT 'SET ARITHABORT ON';  
SET NUMERIC_ROUNDABORT ON;  
SET ARITHABORT ON;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234 ;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
  
-- SET NUMERIC_ROUNDABORT to ON and SET ARITHABORT to OFF.  
PRINT 'SET NUMERIC_ROUNDABORT ON';  
PRINT 'SET ARITHABORT OFF';  
SET NUMERIC_ROUNDABORT ON;  
SET ARITHABORT OFF;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234 ;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
  
-- SET NUMERIC_ROUNDABORT to OFF and SET ARITHABORT to ON.  
PRINT 'SET NUMERIC_ROUNDABORT OFF';  
PRINT 'SET ARITHABORT ON';  
SET NUMERIC_ROUNDABORT OFF;  
SET ARITHABORT ON;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234 ;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
  
-- SET NUMERIC_ROUNDABORT to OFF and SET ARITHABORT to OFF.  
PRINT 'SET NUMERIC_ROUNDABORT OFF';  
PRINT 'SET ARITHABORT OFF';  
SET NUMERIC_ROUNDABORT OFF;  
SET ARITHABORT OFF;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ARITHABORT &#40; Transact-SQL &#41;](../../t-sql/statements/set-arithabort-transact-sql.md)  
  
  
