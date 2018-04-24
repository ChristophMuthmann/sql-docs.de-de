---
title: PRINT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PRINT_TSQL
- PRINT
dev_langs:
- TSQL
helpviewer_keywords:
- PRINT statement
- user-defined messages [SQL Server]
- messages [SQL Server], PRINT statement
- displaying user-defined messages
- viewing user-defined messages
- conditionally returning messages [SQL Server]
ms.assetid: 32ba0729-c4b5-4cfb-a5aa-e8b9402be028
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9a7c213e9d80d46d4616a4062242e8a6fe259638
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="print-transact-sql"></a>PRINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine benutzerdefinierte Meldung an den Client zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
PRINT msg_str | @local_variable | string_expr  
```  
  
## <a name="arguments"></a>Argumente  
 *msg_str*  
 Eine Zeichen- oder Unicode-Zeichenfolgenkonstante. Weitere Informationen finden Sie unter [Konstanten &#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md).  
  
 **@** *local_variable*  
 Dies ist eine Variable eines beliebigen gültigen Zeichendatentyps. **@***local_variable* muss auf **char**, **nchar**, **varchar** oder **nvarchar** festgelegt sein oder implizit in diese Datentypen konvertierbar sein.  
  
 *string_expr*  
 Ein Ausdruck, der eine Zeichenfolge zurückgibt. Er kann verkettete Literalwerte, Funktionen und Variablen enthalten. Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Eine Meldungszeichenfolge kann bis zu 8.000 Zeichen lang sein, wenn es sich um eine Nicht-Unicode-Zeichenfolge handelt, und 4.000 Zeichen, wenn es sich um eine Unicode-Zeichenfolge handelt. Längere Zeichenfolgen werden abgeschnitten. Die Datentypen**varchar(max)** und **nvarchar(max)** werden abgeschnitten und ergeben Datentypen, die nicht größer sind als **varchar(8000)** und **nvarchar(4000)**.  
  
 RAISERROR kann auch zum Zurückgeben von Meldungen verwendet werden. RAISERROR hat im Vergleich zu PRINT die folgenden Vorteile:  
  
-   RAISERROR unterstützt das Ersetzen von Argumenten in eine Fehlermeldungs-Zeichenfolge. Dabei wird ein Mechanismus verwendet, der auf der printf-Funktion der Standardbibliothek der C-Programmiersprache modelliert wurde.  
  
-   RAISERROR kann neben der Textmeldung eine eindeutige Fehlernummer, einen Schweregrad und einen Statuscode angeben.  
  
-   Mit RAISERROR lassen sich mithilfe der gespeicherten Systemprozedur sp_addmessage benutzerdefinierte Meldungen zurückgeben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-conditionally-executing-print-if-exists"></a>A. Bedingt ausgeführte PRINT-Anweisung (IF EXISTS)  
 Das folgende Beispiel verwendet die `PRINT`-Anweisung zur bedingten Rückgabe einer Meldung.  
  
```  
IF @@OPTIONS & 512 <> 0  
    PRINT N'This user has SET NOCOUNT turned ON.';  
ELSE  
    PRINT N'This user has SET NOCOUNT turned OFF.';  
GO  
```  
  
### <a name="b-building-and-displaying-a-string"></a>B. Erstellung und Anzeigen einer Zeichenfolge  
 Das folgende Beispiel konvertiert die Ergebnisse der `GETDATE`-Funktion in einen `nvarchar`-Datentyp und verkettet sie mit Literaltext. Das Ergebnis der Verkettung wird von `PRINT` zurückgegeben.  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
-- This was required in SQL Server 7.0 or earlier.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="c-conditionally-executing-print"></a>C. Bedingt ausgeführte PRINT-Anweisung  
 Das folgende Beispiel verwendet die `PRINT`-Anweisung zur bedingten Rückgabe einer Meldung.  
  
```  
IF DB_ID() = 1  
    PRINT N'The current database is master.';  
ELSE  
    PRINT N'The current database is not master.';  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DEKLARIEREN SIE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

