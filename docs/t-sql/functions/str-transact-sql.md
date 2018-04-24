---
title: STR (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STR
- STR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- converting numbers to characters
- characters [SQL Server], converting
- character data [SQL Server]
- STR function
ms.assetid: de03531b-d9e7-4c3c-9604-14e582ac20c6
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d4eb6ae0f5cc4a669cf69140e406ad36d4d5bf11
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="str-transact-sql"></a>STR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Konvertiert numerische Daten in Zeichenfolgen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *float_expression*  
 Ein Ausdruck der ungefähren numerischen Datentypkategorie (**float**) mit einem Dezimalpunkt.  
  
 *length*  
 Die Gesamtlänge. Dazu gehören Dezimaltrennzeichen, Zeichen, Ziffern und Leerzeichen. Der Standardwert ist 10.  
  
 *decimal*  
 Die Anzahl der Stellen nach dem Dezimaltrennzeichen. *decimal* muss kleiner als oder gleich 16 sein. Wenn *decimal* größer als 16 ist, wird das Ergebnis bei sechzehn Stellen nach dem Dezimaltrennzeichen abgeschnitten.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varchar**  
  
## <a name="remarks"></a>Remarks  
 Falls angegeben, sollten die Werte für die Parameter *length* und *decimal* der STR-Funktion positiv sein. Die Zahl wird standardmäßig, oder wenn der Dezimalstellenparameter 0 beträgt, auf eine ganze Zahl gerundet. Die angegebene Länge sollte größer oder gleich dem Teil der Zahl vor dem Dezimalpunkt plus dem Vorzeichen (falls vorhanden) sein. Ein kurzer *float_expression*-Ausdruck wird in der angegebenen Länge rechtsbündig ausgerichtet, während ein langer *float_expression*-Ausdruck auf die angegebene Anzahl der Dezimalstellen gekürzt wird. Beispielsweise ergibt STR(12 **,** 10) den Wert 12. Dieser Wert wird im Resultset rechtsbündig ausgerichtet. STR(1223 **,** 2) schneidet das Resultset zu ** hingegen ab. Zeichenfolgenfunktionen können geschachtelt werden.  
  
> [!NOTE]  
>  Wenn Sie Daten in das Unicodeformat konvertieren wollen, verwenden Sie STR innerhalb einer CONVERT- oder [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md)-Konvertierungsfunktion.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Ausdruck, der aus fünf Ziffern und einem Dezimaltrennzeichen besteht, in eine Zeichenfolge mit sechs Stellen konvertiert. Die Stellen hinter dem Dezimalpunkt werden auf eine Dezimalstelle gerundet.  
  
```  
SELECT STR(123.45, 6, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------  
 123.5  
  
(1 row(s) affected)  
```  
  
 Falls der Ausdruck die angegebene Länge überschreitet, wird die Zeichenfolge `**` in der festgelegten Länge zurückgegeben.  
  
```  
SELECT STR(123.45, 2, 2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--  
**  
  
(1 row(s) affected)  
```  
  
 Auch wenn numerische Daten innerhalb von `STR` geschachtelt sind, werden als Ergebnis Zeichendaten mit dem angegebenen Format zurückgegeben.  
  
```  
SELECT STR (FLOOR (123.45), 8, 3;)  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
 123.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [FORMAT &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)  
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen (Transact-SQL))](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

