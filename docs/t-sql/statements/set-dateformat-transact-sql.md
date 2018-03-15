---
title: SET DATEFORMAT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEFORMAT
- SET DATEFORMAT
- SET_DATEFORMAT_TSQL
- DATEFORMAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], formats
- dates [SQL Server], ordering date parts
- SET DATEFORMAT option [SQL Server]
- DATEFORMAT option [SQL Server]
- date and time [SQL Server], SET DATEFORMAT
- options [SQL Server], date
- date and time [SQL Server], DATEFORMAT
- dateparts [SQL Server], dateformat
ms.assetid: da217878-7ec4-477e-aa13-604073c948f8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3b1e233508eaedab627b57a3ce6938b90a9e196d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="set-dateformat-transact-sql"></a>SET DATEFORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Legt die Reihenfolge der Datumsteile für den Tag, den Monat und das Jahr fest, um die Zeichenfolgen **date**, **smalldatetime**, **datetime**, **datetime2** und **datetimeoffset** zu interpretieren.  
  
 Eine Übersicht über alle Datums- und Uhrzeitdatentypen und zugehörige Funktionen für [!INCLUDE[tsql](../../includes/tsql-md.md)] finden Sie unter [Datums- und Uhrzeitdatentypen und zugehörige Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SET DATEFORMAT { format | @format_var }   
```  
  
## <a name="arguments"></a>Argumente  
 *format* | **@***format_var*  
 Reihenfolge der Datumsteile. Gültige Parameter sind **mdy**, **dmy**, **ymd**, **ydm**, **myd**, and **dym**. Kann entweder in Unicode oder in Doppelbyte-Zeichensätzen (Double-Byte Character Set, DBCS), die in Unicode konvertiert wurden, dargestellt werden. Der Standardparameter Der Standard für Englisch ist **mdy**. Die standardmäßige DATEFORMAT-Einstellung aller Unterstützungssprachen finden Sie unter [sp_helplanguage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Die DATEFORMAT-Einstellung **ydm** wird für die Datentypen **date**, **datetime2** und **datetimeoffset** nicht unterstützt.  
  
 Die Auswirkungen der DATEFORMAT-Einstellung auf die Interpretation der Zeichenfolgen können für die Werte von **datetime** und **smalldatetime** sowie für die Werte von**date**, **datetime2** und **datetimeoffset** je nach Zeichenfolgenformat unterschiedlich sein. Diese Einstellung wirkt sich nur auf die Interpretation von Zeichenfolgen bei der Konvertierung in Datumswerte zum Speichern in der Datenbank aus. Sie wirkt sich nicht auf die Anzeige der Werte für Datumsdatentypen, die in der Datenbank gespeichert sind, oder auf das Speicherformat aus.  
  
 Einige Zeichenfolgenformate, z. B. ISO 8601, werden unabhängig von der DATEFORMAT-Einstellung interpretiert.  
  
 Die Einstellung von SET DATEFORMAT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 SET DATEFORMAT überschreibt die implizite Einstellung für das Datumsformat von [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden andere Datumszeichenfolgen als Eingaben in Sitzungen mit derselben `DATEFORMAT`-Einstellung verwendet.  
  
```  
-- Set date format to day/month/year.  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar datetime2 = '31/12/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: 2008-12-31 09:01:01.123  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar datetime2 = '12/31/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: Msg 241: Conversion failed when converting date and/or time -- from character string.  
  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

