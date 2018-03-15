---
title: int, bigint, smallint und tinyint (Transact-SQL) | Microsoft-Dokumentation
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

Exakte Zahlendatentypen für ganzzahlige Daten. Wenn Sie Speicherplatz in der Datenbank sparen möchten, verwenden Sie den kleinsten Datentyp, der auf jeden Fall alle möglichen Werte enthalten kann. tinyint wäre z.B. ausreichend für das Alter einer Person, da niemand älter als 255 Jahre wird. tinyint wäre allerdings für das Alter eines Gebäudes nicht ausreichend, da ein Gebäude länger als 255 Jahren stehen bleiben kann.
  
|Datentyp|Bereich|Speicherung|  
|---|---|---|
|**bigint**|-2^63 (-9.223.372.036.854.775.808) bis 2^63-1 (9.223.372.036.854.775.807)|8 Byte|  
|**int**|-2^31 (-2.147.483.648) bis 2^31-1 (2.147.483.647)|4 Byte|  
|**smallint**|-2^15 (-32,768) bis 2^15-1 (32,767)|2 Byte|  
|**tinyint**|0 bis 255|1 Byte|  
  
## <a name="remarks"></a>Remarks  
Der **int**-Datentyp ist der primäre Integerdatentyp in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Der **bigint**-Datentyp ist für Fälle bestimmt, in denen ganzzahlige Werte den durch den **int**-Datentyp unterstützten Bereich überschreiten.
  
**bigint** passt zwischen **smallmoney** und **int** in der Rangfolge der Datentypen.
  
Die Funktionen geben **bigint** nur dann zurück, wenn der Parameterausdruck vom Datentyp **bigint** ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stuft andere Integerdatentypen (**tinyint**, **smallint** und **int**) nicht automatisch auf **bigint** herauf.
  
> [!CAUTION]  
>  Wenn Sie die arithmetischen Operatoren +, -, \*, / oder % verwenden, um eine implizite oder explizite Konvertierung der konstanten Werte **int**, **smallint**, **tinyint** oder **bigint** in die Datentypen **float**, **real**, **decimal** oder **numeric** auszuführen, wendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Berechnen des Datentyps und der Genauigkeit der Ausdrucksergebnisse unterschiedliche Regeln an, je nachdem, ob die Abfrage automatisch parametrisiert wurde oder nicht.  
>   
>  Aus diesem Grund können ähnliche Ausdrücke in Abfragen unterschiedliche Ergebnisse erzeugen. Wenn eine Abfrage nicht automatisch parametrisiert wird, wird der konstante Wert vor dem Konvertieren in den angegebenen Datentyp zunächst in den **numeric**-Datentyp konvertiert, dessen Genauigkeit für den Wert der Konstanten genau ausreicht. Der konstante Wert 1 wird beispielsweise in **numeric (1, 0)** und der konstante Wert 250 in **numeric (3, 0)** konvertiert.  
>   
>  Wenn eine Abfrage automatisch parametrisiert wird, wird der konstante Wert vor dem Konvertieren in den endgültigen Datentyp immer in **numeric (10, 0)** konvertiert. Wenn der Operator / verwendet wird, kann bei ähnlichen Abfragen nicht nur die Genauigkeit des Ergebnistyps variieren, sondern auch der Ergebniswert. Der Ergebniswert einer automatisch parametrisierten Abfrage, die den Ausdruck `SELECT CAST (1.0 / 7 AS float)` einschließt, weicht beispielsweise vom Ergebniswert derselben Abfrage ab (die nicht automatisch parametrisiert wurde), da die Ergebnisse der automatisch parametrisierten Abfrage abgeschnitten werden, d.h., sie werden an die Länge des **numeric (10, 0)**-Datentyps angepasst.  
  
## <a name="converting-integer-data"></a>Konvertieren von Integerdaten
Wenn ganze Zahlen implizit in einen Zeichendatentyp konvertiert werden und die ganze Zahl für das Zeichenfeld zu groß ist, fügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das ASCII-Zeichen 42 (Sternchen (*)) ein.
  
Integerkonstanten, die größer als 2.147.483.647 sind, werden in den **decimal**-Datentyp konvertiert und nicht in den **bigint**-Datentyp. Das folgende Beispiel zeigt, dass bei Überschreitung des Schwellenwerts der Datentyp des Ergebnisses von einem **int** in einen **decimal**-Datentyp geändert wird.
  
```sql
SELECT 2147483647 / 2 AS Result1, 2147483649 / 2 AS Result2 ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result1      Result2  
1073741823   1073741824.500000  
```  
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird eine Tabelle mit den Datentypen **bigint**, **int**, **smallint** und **tinyint** erstellt. Werte werden in jede Spalte eingefügt und in der SELECT-Anweisung zurückgegeben.
  
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
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
