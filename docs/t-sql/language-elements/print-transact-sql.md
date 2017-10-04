---
title: Drucken (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51377ebe291fe4c76d8761aaba74eab8f5201108
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="print-transact-sql"></a>Drucken-Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine benutzerdefinierte Meldung an den Client zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
PRINT msg_str | @local_variable | string_expr  
```  
  
## <a name="arguments"></a>Argumente  
 *msg_str*  
 Eine Zeichen- oder Unicode-Zeichenfolgenkonstante. Weitere Informationen finden Sie unter [Konstanten &#40; Transact-SQL &#41; ](../../t-sql/data-types/constants-transact-sql.md).  
  
 **@***Local_variable*  
 Dies ist eine Variable eines beliebigen gültigen Zeichendatentyps. **@***Local_variable* muss **Char**, **Nchar**, **Varchar**, oder **Nvarchar**, oder es muss in der Lage sein implizit konvertiert in diese Datentypen.  
  
 *string_expr*  
 Ein Ausdruck, der eine Zeichenfolge zurückgibt. Er kann verkettete Literalwerte, Funktionen und Variablen enthalten. Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 Eine Meldungszeichenfolge kann bis zu 8.000 Zeichen lang sein, wenn es sich um eine Nicht-Unicode-Zeichenfolge handelt, und 4.000 Zeichen, wenn es sich um eine Unicode-Zeichenfolge handelt. Längere Zeichenfolgen werden abgeschnitten. Die **varchar(max)** und **nvarchar(max)** Datentypen werden abgeschnitten, um Datentypen, die nicht als größer **vom Datentyp varchar(8000)** und **nvarchar(4000)**.  
  
 RAISERROR kann auch zum Zurückgeben von Meldungen verwendet werden. RAISERROR hat im Vergleich zu PRINT die folgenden Vorteile:  
  
-   RAISERROR unterstützt das Ersetzen von Argumenten in eine Fehlermeldungs-Zeichenfolge. Dabei wird ein Mechanismus verwendet, der auf der printf-Funktion der Standardbibliothek der C-Programmiersprache modelliert wurde.  
  
-   RAISERROR kann neben der Textmeldung eine eindeutige Fehlernummer, einen Schweregrad und einen Statuscode angeben.  
  
-   RAISERROR kann verwendet werden, zum Zurückgeben von benutzerdefinierten Meldungen, die mithilfe der gespeicherten Systemprozedur Sp_addmessage erstellt.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-conditionally-executing-print"></a>C. Bedingt ausgeführte Print-Anweisung  
 Das folgende Beispiel verwendet die `PRINT`-Anweisung zur bedingten Rückgabe einer Meldung.  
  
```  
IF DB_ID() = 1  
    PRINT N'The current database is master.';  
ELSE  
    PRINT N'The current database is not master.';  
GO  
```  
  
### <a name="d-building-and-displaying-a-string"></a>D. Erstellung und Anzeigen einer Zeichenfolge  
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
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [RAISERROR &#40; Transact-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  


