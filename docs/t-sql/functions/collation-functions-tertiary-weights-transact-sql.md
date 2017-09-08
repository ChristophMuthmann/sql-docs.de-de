---
title: TERTIARY_WEIGHTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TERTIARY_WEIGHTS_TSQL
- TERTIARY_WEIGHTS
dev_langs:
- TSQL
helpviewer_keywords:
- weights [SQL Server]
- SQL tertiary collations
- TERTIARY_WEIGHTS function
ms.assetid: 7e1f5350-260b-4c61-8c84-69bb1a214f1f
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7414f60414c14457dddc6f860201fd84409f1cb1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="collation-functions---tertiaryweights-transact-sql"></a>Sortierungsfunktionen - TERTIARY_WEIGHTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt eine binäre Zeichenfolge der Schriftbreiten für jedes Zeichen in einem Nicht-Unicode-Zeichenfolgenausdruck zurück, der für eine tertiäre SQL-Sortierung definiert ist.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
TERTIARY_WEIGHTS( non_Unicode_character_string_expression )  
```  
  
## <a name="arguments"></a>Argumente  
*non_Unicode_character_string_expression*  
Ist eine Zeichenfolge [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) des Typs **Char**, **Varchar**, oder **varchar(max)** für eine tertiäre SQL-Sortierung definiert. Eine Liste dieser Sortierungen finden Sie unter Hinweise.
  
## <a name="return-types"></a>Rückgabetypen
TERTIARY_WEIGHTS gibt **Varbinary** Wenn *Non_Unicode_character_string_expression* ist **Char** oder **Varchar**, und gibt zurück **varbinary(max)** Wenn *Non_Unicode_character_string_expression* ist **varchar(max)**.
  
## <a name="remarks"></a>Hinweise  
TERTIARY_WEIGHTS gibt NULL zurück, wenn *Non_Unicode_character_string_expression* ist nicht mit eine tertiäre SQL-Sortierung definiert. In der folgenden Tabelle werden die tertiären SQL-Sortierungen dargestellt.
  
|Sortierreihenfolge-ID|SQL-Sortierung|  
|---|---|
|33|SQL_Latin1_General_Pref_CP437_CI_AS|  
|34|SQL_Latin1_General_CP437_CI_AI|  
|43|SQL_Latin1_General_Pref_CP850_CI_AS|  
|44|SQL_Latin1_General_CP850_CI_AI|  
|49|SQL_1xCompat_CP850_CI_AS|  
|53|SQL_Latin1_General_Pref_CP1_CI_AS|  
|54|SQL_Latin1_General_CP1_CI_AI|  
|56|SQL_AltDiction_Pref_CP850_CI_AS|  
|57|SQL_AltDiction_CP850_CI_AI|  
|58|SQL_Scandinavian_Pref_CP850_CI_AS|  
|82|SQL_Latin1_General_CP1250_CI_AS|  
|84|SQL_Czech_CP1250_CI_AS|  
|86|SQL_Hungarian_CP1250_CI_AS|  
|88|SQL_Polish_CP1250_CI_AS|  
|90|SQL_Romanian_CP1250_CI_AS|  
|92|SQL_Croatian_CP1250_CI_AS|  
|94|SQL_Slovak_CP1250_CI_AS|  
|96|SQL_Slovenian_CP1250_CI_AS|  
|106|SQL_Latin1_General_CP1251_CI_AS|  
|108|SQL_Ukrainian_CP1251_CI_AS|  
|113|SQL_Latin1_General_CP1253_CS_AS|  
|114|SQL_Latin1_General_CP1253_CI_AS|  
|130|SQL_Latin1_General_CP1254_CI_AS|  
|146|SQL_Latin1_General_CP1256_CI_AS|  
|154|SQL_Latin1_General_CP1257_CI_AS|  
|156|SQL_Estonian_CP1257_CI_AS|  
|158|SQL_Latvian_CP1257_CI_AS|  
|160|SQL_Lithuanian_CP1257_CI_AS|  
|183|SQL_Danish_Pref_CP1_CI_AS|  
|184|SQL_SwedishPhone_Pref_CP1_CI_AS|  
|185|SQL_SwedishStd_Pref_CP1_CI_AS|  
|186|SQL_Icelandic_Pref_CP1_CI_AS|  
  
TERTIARY_WEIGHTS dient zur Verwendung in der Definition einer berechneten Spalte, die auf den Werten definiert ist ein **Char**, **Varchar**, oder **varchar(max)** Spalte. Definieren eines Indexes für die berechnete Spalte und die **Char**, **Varchar**, oder **varchar(max)** Spalte kann die Leistung verbessern bei der **Char**, **Varchar**, oder **varchar(max)** Spalte in der ORDER BY-Klausel einer Abfrage angegeben ist.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird eine berechnete Spalte in einer Tabelle erstellt, die die `TERTIARY_WEIGHTS`-Funktion auf die Werte einer Spalte vom Datentyp `char` anwendet.
  
```sql
CREATE TABLE TertColTable  
(Col1 char(15) COLLATE SQL_Latin1_General_Pref_CP437_CI_AS,  
Col2 AS TERTIARY_WEIGHTS(Col1));  
GO   
```  
  
## <a name="see-also"></a>Siehe auch
[ORDER BY-Klausel &#40; Transact-SQL &#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)
  
  

