---
title: TERTIARY_WEIGHTS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5edddaffd94337a1538ed00085216145f9389670
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="collation-functions---tertiaryweights-transact-sql"></a>Sortierungsfunktionen: TERTIARY_WEIGHTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt eine binäre Zeichenfolge der Schriftbreiten für jedes Zeichen in einem Nicht-Unicode-Zeichenfolgenausdruck zurück, der für eine tertiäre SQL-Sortierung definiert ist.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
TERTIARY_WEIGHTS( non_Unicode_character_string_expression )  
```  
  
## <a name="arguments"></a>Argumente  
*non_Unicode_character_string_expression*  
Ein [Zeichenfolgenausdruck](../../t-sql/language-elements/expressions-transact-sql.md) vom Datentyp **char**, **varchar** oder **varchar(max)**, der für eine tertiäre SQL-Sortierung definiert ist. Eine Liste dieser Sortierungen finden Sie unter Hinweise.
  
## <a name="return-types"></a>Rückgabetypen
TERTIARY_WEIGHTS gibt **varbinary** zurück, wenn *non_Unicode_character_string_expression* vom Datentyp **char** oder **varchar** ist, und gibt **varbinary(max)** zurück, wenn *non_Unicode_character_string_expression* vom Datentyp **varchar(max)** ist.
  
## <a name="remarks"></a>Remarks  
TERTIARY_WEIGHTS gibt NULL zurück, wenn *non_Unicode_character_string_expression* nicht für eine tertiäre SQL-Sortierung definiert ist. In der folgenden Tabelle werden die tertiären SQL-Sortierungen dargestellt.
  
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
  
TERTIARY_WEIGHTS ist zum Definieren einer berechneten Spalte vorgesehen, die mit den Werten einer Spalte vom Datentyp **char**, **varchar** oder **varchar(max)** definiert wird. Das Definieren eines Index für die berechnete Spalte und die Spalte vom Datentyp **char**, **varchar** oder **varchar(max)** kann die Leistung verbessern, wenn die Spalte vom Datentyp **char**, **varchar** oder **varchar(max)** in der ORDER BY-Klausel einer Abfrage angegeben wird.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird eine berechnete Spalte in einer Tabelle erstellt, die die `TERTIARY_WEIGHTS`-Funktion auf die Werte einer Spalte vom Datentyp `char` anwendet.
  
```sql
CREATE TABLE TertColTable  
(Col1 char(15) COLLATE SQL_Latin1_General_Pref_CP437_CI_AS,  
Col2 AS TERTIARY_WEIGHTS(Col1));  
GO   
```  
  
## <a name="see-also"></a>Siehe auch
[ORDER BY-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)
  
  
