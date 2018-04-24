---
title: SET CONCAT_NULL_YIELDS_NULL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
- CONCAT_NULL_YIELDS_NULL_TSQL
- SET CONCAT_NULL_YIELDS_NULL
- CONCAT_NULL_YIELDS_NULL
- SET_CONCAT_NULL_YIELDS_NULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_NULL_YIELDS_NULL option
- null values [SQL Server], concatenation results
- concatenation [SQL Server]
- SET CONCAT_NULL_YIELDS_NULL statement
ms.assetid: 3091b71c-6518-4eb4-88ab-acae49102bc5
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a07b9db8f3f444587eb23cd1dfd92c9814da9e2f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-concatnullyieldsnull-transact-sql"></a>SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Steuert die Behandlung von Verkettungsergebnissen als NULL-Werte oder als leere Zeichenfolgen.  
  
> [!IMPORTANT]  
>  In einer späteren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird CONCAT_NULL_YIELDS_NULL immer auf ON festgelegt, und jede Anwendung, die für die Option explizit OFF festlegt, löst einen Fehler aus. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
    
SET CONCAT_NULL_YIELDS_NULL { ON | OFF }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET CONCAT_NULL_YIELDS_NULL ON    
```  
  
## <a name="remarks"></a>Remarks  
 Wenn SET CONCAT_NULL_YIELDS_NULL auf ON festgelegt ist, führt die Verkettung eines NULL-Wertes mit einer Zeichenfolge zum Ergebnis NULL. `SELECT 'abc' + NULL` ergibt beispielsweise `NULL`. Wenn SET CONCAT_NULL_YIELDS_NULL auf OFF festgelegt ist, erzeugt die Verkettung eines NULL-Wertes mit einer Zeichenfolge als Ergebnis die Zeichenfolge (der NULL-Wert wird als leere Zeichenfolge behandelt). `SELECT 'abc' + NULL` ergibt beispielsweise `abc`.  
  
 Wenn SET CONCAT_NULL_YIELDS_NULL nicht angegeben ist, gilt die Einstellung der **CONCAT_NULL_YIELDS_NULL**-Datenbankoption.  
  
> [!NOTE]  
>  SET CONCAT_NULL_YIELDS_NULL stimmt mit der CONCAT_NULL_YIELDS_NULL-Einstellung von ALTER DATABASE überein.  
  
 Die Einstellung von SET CONCAT_NULL_YIELDS_NULL wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 SET CONCAT_NULL_YIELDS_NULL muss beim Erstellen oder Ändern von Indizes für berechnete Spalten oder indizierte Sichten auf ON festgelegt sein. Wenn SET CONCAT_NULL_YIELDS_NULL auf OFF festgelegt ist, treten bei CREATE-, UPDATE-, INSERT- und DELETE-Anweisungen in Tabellen mit Indizes für berechnete Spalten oder indizierten Sichten Fehler auf. Weitere Informationen zu den erforderlichen Einstellungen der SET-Option mit indizierten Sichten und Indizes für berechnete Spalten finden Sie in den Überlegungen zum Verwenden der SET-Anweisungen unter [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 Wenn CONCAT_NULL_YIELDS_NULL auf OFF festgelegt wird, ist die Zeichenfolgenverkettung über Servergrenzen hinweg nicht möglich.  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus.  
  
```  
DECLARE @CONCAT_NULL_YIELDS_NULL VARCHAR(3) = 'OFF';  
IF ( (4096 & @@OPTIONS) = 4096 ) SET @CONCAT_NULL_YIELDS_NULL = 'ON';  
SELECT @CONCAT_NULL_YIELDS_NULL AS CONCAT_NULL_YIELDS_NULL;  
  
```  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Verwendung beider `SET CONCAT_NULL_YIELDS_NULL`-Einstellungen.  
  
```  
PRINT 'Setting CONCAT_NULL_YIELDS_NULL ON';  
GO  
-- SET CONCAT_NULL_YIELDS_NULL ON and testing.  
SET CONCAT_NULL_YIELDS_NULL ON;  
GO  
SELECT 'abc' + NULL ;  
GO  
  
-- SET CONCAT_NULL_YIELDS_NULL OFF and testing.  
SET CONCAT_NULL_YIELDS_NULL OFF;  
GO  
SELECT 'abc' + NULL;   
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
