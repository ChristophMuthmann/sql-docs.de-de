---
title: Int, Bigint, Smallint und Tinyint (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 9/8/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bigint_TSQL
- smallint
- bigint
- smallint_TSQL
- tinyint_TSQL
- int_TSQL
- int
- tinyint
dev_langs:
- TSQL
helpviewer_keywords:
- exact numeric data [SQL Server]
- numeric data
- tinyint data type
- int data type
- smallint data type
ms.assetid: 9bda5b0b-2380-4931-a1c8-f362fdefa99b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2e99ccb97dc5c36f8b7870a042963d6302b3f1eb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="int-bigint-smallint-and-tinyint-transact-sql"></a>int, bigint, smallint und tinyint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Exakte Zahlendatentypen für ganzzahlige Daten. Um Speicherplatz in der Datenbank zu speichern, verwenden Sie den kleinsten-Datentyp, der zuverlässig alle möglichen Werte enthalten kann. Beispielsweise würde "tinyint" für Alter einer Person ausreichend sein, da kein aktiv ist, mehr als 255 Jahre alt sein. Aber "tinyint" würde nicht ausreichend, damit ein Gebäude Age werden, da ein Erstellen von mehr als 255 Jahre alt sein kann.
  
|Datentyp|Bereich|Speicherung|  
|---|---|---|
|**bigint**|-2^63 (-9.223.372.036.854.775.808) bis 2^63-1 (9.223.372.036.854.775.807)|8 bytes|  
|**int**|-2^31 (-2.147.483.648) bis 2^31-1 (2.147.483.647)|4 bytes|  
|**smallint**|-2^15 (-32,768) bis 2^15-1 (32,767)|2 Byte|  
|**tinyint**|0 bis 255|1 byte|  
  
## <a name="remarks"></a>Hinweise  
Die **Int** -Datentyp ist der primäre ganzzahlige Datentyp in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die **"bigint"** -Datentyp dient zur Verwendung bei ganzzahligen Werten des Bereichs möglicherweise, die vom unterstützt überschreitet die **Int** -Datentyp.
  
**"bigint"** passt zwischen **Smallmoney** und **Int** in der Rangfolge der Datentypen.
  
Return-Funktionen **"bigint"** nur, wenn der Parameterausdruck ein **"bigint"** -Datentyp. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Stuft andere ganzzahlige Datentypen nicht automatisch (**"tinyint"**, **"smallint"**, und **Int**) zu **"bigint"**.
  
> [!CAUTION]  
>  Bei Verwendung der +, -, \*, /, oder % arithmetische Operatoren, die implizite oder explizite Konvertierung von **Int**, **"smallint"**, **"tinyint"**, oder  **"bigint"** Konstantenwerten der **"float"**, **echte**, **decimal** oder **numerischen** Datentypen, die Regeln [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gilt, wenn sie den Datentyp und die Genauigkeit der Ausdrucksergebnisse zu unterscheiden, je nachdem, ob die Abfrage automatisch parametrisiert wird berechnet.  
>   
>  Aus diesem Grund können ähnliche Ausdrücke in Abfragen unterschiedliche Ergebnisse erzeugen. Wenn eine Abfrage nicht parametrisiert ist, wird der Konstante Wert zuerst in konvertiert **numerischen**, Precision wird gerade groß genug für den Wert der Konstante vor dem Konvertieren in den angegebenen Datentyp. Z. B. der Konstante Wert 1 konvertiert wird, um **Numeric (1, 0)**, und der Konstante Wert 250 in konvertiert **Numeric (3, 0)**.  
>   
>  Wenn eine Abfrage automatisch parametrisiert wird, wird der Konstante Wert immer in konvertiert **Numeric (10, 0)** vor dem Konvertieren in den endgültigen Datentyp. Wenn der Operator / verwendet wird, kann bei ähnlichen Abfragen nicht nur die Genauigkeit des Ergebnistyps variieren, sondern auch der Ergebniswert. Der Ergebniswert z. B. von einer automatisch parametrisierten Abfrage, die der Ausdruck umfasst `SELECT CAST (1.0 / 7 AS float)`, unterscheidet sich von der Ergebniswert derselben Abfrage, die nicht automatisch parametrisiert werden, da die Ergebnisse der Abfrage automatisch parametrisiert werden abgeschnitten, um passt die **Numeric (10, 0)** -Datentyp.  
  
## <a name="converting-integer-data"></a>Konvertieren von ganzzahligen Daten
Wenn ganze Zahlen implizit in einen Zeichendatentyp konvertiert werden und die ganze Zahl für das Zeichenfeld zu groß ist, fügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das ASCII-Zeichen 42 (Sternchen (*)) ein.
  
Ganzzahlige Konstanten größer 2.147.483.647 konvertiert werden, um die **decimal** -Datentyp, nicht die **"bigint"** -Datentyp. Das folgende Beispiel zeigt, dass wenn der Schwellenwert überschritten wird, ändert sich der Datentyp des Ergebnisses aus einer **Int** zu einem **decimal**.
  
```sql
SELECT 2147483647 / 2 AS Result1, 2147483649 / 2 AS Result2 ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result1      Result2  
1073741823   1073741824.500000  
```  
  
## <a name="examples"></a>Beispiele  
Im folgende Beispiel wird eine Tabelle mit den **"bigint"**, **Int**, **"smallint"**, und **"tinyint"** -Datentypen. Werte werden in jede Spalte eingefügt und in der SELECT-Anweisung zurückgegeben.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyBigIntColumn bigint  
,MyIntColumn  int
,MySmallIntColumn smallint
,MyTinyIntColumn tinyint
);  
  
GO  
  
INSERT INTO dbo.MyTable VALUES (9223372036854775807, 2147483647,32767,255);  
 GO  
SELECT MyBigIntColumn, MyIntColumn, MySmallIntColumn, MyTinyIntColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyBigIntColumn       MyIntColumn MySmallIntColumn MyTinyIntColumn  
-------------------- ----------- ---------------- ---------------  
9223372036854775807  2147483647  32767            255  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Sys.Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
