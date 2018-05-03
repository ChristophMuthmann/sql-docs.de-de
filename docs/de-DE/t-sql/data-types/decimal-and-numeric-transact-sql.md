---
title: decimal und numeric (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- decimal
- decimal_TSQL
- numeric
- numeric_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decimal data type
- decimal data type, about decimal data type
- numeric data type
- numeric data type, about numeric data type
ms.assetid: 9d862a90-e6b7-4692-8605-92358dccccdf
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 629e74bfffef65546c15ea6aa4c3404bbdafa972
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="decimal-and-numeric-transact-sql"></a>decimal und numeric (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Numerische Datentypen mit fester Genauigkeit und fester Anzahl von Dezimalstellen. decimal und numeric sind Synonyme und können austauschbar verwendet werden.
  
## <a name="arguments"></a>Argumente  
**decimal**[ **(***p*[ **,***s*] **)**] und **numeric**[ **(***p*[ **,***s*] **)**]  
Zahlen mit fester Genauigkeit und mit fester Anzahl von Dezimalstellen. Wenn maximale Genauigkeit verwendet wird, liegen gültige Werte zwischen - 10^38 +1 und 10^38 - 1. Die ISO-Synonyme für **decimal** lauten **dec** und **dec(***p*, *s***)**. **numeric** ist die funktionelle Entsprechung von **decimal**.
  
p (Precision = Genauigkeit)  
Die maximale Gesamtanzahl von Dezimalstellen, sowohl links als auch rechts vom Dezimalkomma, die gespeichert wird. Die Genauigkeit muss ein Wert zwischen 1 und der maximalen Genauigkeit von 38 sein. Die Standardgenauigkeit beträgt 18.
  
> [!NOTE]  
>  Informatica unterstützt unabhängig von der angegebenen Präzision und dem Dezimalstellenwert nur 16 signifikante Ziffern.  
  
*s* (Dezimalstellenwert)  
Die Anzahl von Dezimalstellen rechts vom Dezimalkomma, die gespeichert wird. Diese Anzahl wird von *p* subtrahiert, um die maximale Anzahl der Stellen links von der Dezimalstelle zu bestimmen. Die maximal speicherbare Zahl an Dezimalstellen rechts vom Dezimalkomma. Der Dezimalstellenwert muss in einem Bereich zwischen 0 und *p* liegen. Der Dezimalstellenwert kann nur angegeben werden, wenn eine Genauigkeit angegeben ist. Der Standardwert ist 0 (null). Daher gilt: 0 <= *s* \<= *p*. Die maximalen Speichergrößen variieren abhängig von der Genauigkeit.
  
|Genauigkeit|Speicherplatz in Bytes|  
|---|---|
|1 – 9|5|  
|10–19|9|  
|20–28|13|  
|29–38|17|  
  
> [!NOTE]  
>  Informatica (über den SQL Server PDW-Informatica-Connector verbunden) unterstützt unabhängig von der angegebenen Präzision und dem Dezimalstellenwert nur 16 signifikante Ziffern.  
  
## <a name="converting-decimal-and-numeric-data"></a>Konvertieren von decimal- und numeric-Daten
Im Fall der Datentypen **decimal** und **numeric** sieht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] jede auftretende Kombination aus Genauigkeit und Anzahl der Dezimalstellen als einen anderen Datentyp an. **decimal(5,5)** und **decimal(5,0)** werden beispielsweise als unterschiedliche Datentypen erachtet.
  
In [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen wird eine Konstante mit einem Dezimaltrennzeichen automatisch in einen Wert des **numeric**-Datentyps konvertiert. Hierbei werden die mindestens erforderliche Genauigkeit und die Anzahl von Dezimalstellen verwendet. Die Konstante 12.345 wird z.B. in einen **numeric**-Wert mit einer Genauigkeit von 5 und 3 Dezimalstellen konvertiert.
  
Wenn Sie eine Konvertierung von **decimal** oder **numeric** in **float** oder **real** vornehmen, kann ein gewisses Maß an Genauigkeit verloren gehen. Wenn Sie eine Konvertierung von **int**, **smallint**, **tinyint**, **float**, **real**, **money** oder **smallmoney** in **decimal** oder **numeric** vornehmen, kann es zu einem Überlauf kommen.
  
Bei der Konvertierung einer Zahl in einen Wert des Typs **decimal** oder **numeric** mit einer geringeren Genauigkeit und einer geringeren Anzahl von Dezimalstellen wird der Wert standardmäßig von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerundet. Wenn allerdings die Option SET ARITHABORT auf ON festgelegt ist, löst [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei Auftreten eines Überlaufs einen Fehler aus. Eine Verringerung der Genauigkeit und der Anzahl der Dezimalstellen reicht zum Auslösen eines Fehlers nicht aus.
  
Beim Konvertieren von float- oder real-Werten in decimal oder numeric umfasst der decimal-Wert nie mehr als 17 Dezimalstellen. float-Werte < 5E-18 werden immer in 0 konvertiert.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird eine Tabelle mit **decimal**- und **numeric**-Datentypen erstellt.  Werte werden in jede Spalte eingefügt, und die Ergebnisse werden mithilfe einer SELECT-Anweisung zurückgegeben.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyDecimalColumn decimal(5,2)  
,MyNumericColumn numeric(10,5)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (123, 12345.12);  
GO  
SELECT MyDecimalColumn, MyNumericColumn  
FROM dbo.MyTable;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyDecimalColumn                         MyNumericColumn  
--------------------------------------- ---------------------------------------  
123.00                                  12345.12000  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Siehe auch
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
