---
title: Binary und Varbinary (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 8/16/2017
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
- binary_TSQL
- varbinary_TSQL
- binary
- varbinary
dev_langs:
- TSQL
helpviewer_keywords:
- varbinary data type
- binary [SQL Server], about binary data type
ms.assetid: bcce65f9-10db-4b3e-bfaf-dfc06c6f820f
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e6aaf00b8e846316c92897360932703a013150e8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="binary-and-varbinary-transact-sql"></a>binary und varbinary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Binäre Datentypen mit fester Länge bzw. mit variabler Länge.
  
## <a name="arguments"></a>Argumente  
**binäre** [(  *n*  )] Binärdaten fester Länge, mit einer Länge von  *n*  Bytes, wobei  *n*  ist ein Wert zwischen 1 und 8.000 sein. Die Speichergröße beträgt  *n*  Bytes.
  
**Varbinary** [(  *n*   |  **max**)] Binärdaten variabler Länge. *n*ein Wert zwischen 1 und 8.000 kann sein. **Max.** gibt an, dass die maximale Speichergröße 2 ^ 31-1 Byte beträgt. Die Speicherplatzgröße ist die tatsächliche Länge der eingegebenen Daten + 2 Byte. Die eingegebenen Daten können 0 Byte lang sein. Der ANSI SQL-Synonym für **Varbinary** ist **binary varying**.
  
## <a name="remarks"></a>Hinweise  
Wenn  *n*  ist nicht angegeben in einer Datendefinitions- oder variablendeklarationsanweisung, die Standardlänge 1. Wenn  *n*  ist nicht angegeben mit der CAST-Funktion, die Standardlänge ist 30.

| Datentyp | Verwenden Sie in folgenden Fällen... |
| --- | --- |
| **binary** | die Größen der spaltendateneinträge entsprechen.|
| **varbinary** | die Größen der spaltendateneinträge variieren erheblich.|
| **varbinary(max)** | die spaltendateneinträge überschreiten 8.000 Byte.|


## <a name="converting-binary-and-varbinary-data"></a>Konvertieren von binary- und Varbinary-Daten
Wenn Daten von einem Zeichenfolgen-Datentyp konvertiert werden (**Char**, **Varchar**, **Nchar**, **Nvarchar**, **binären**, **Varbinary**, **Text**, **Ntext**, oder **Image**) zu einem **binäre** oder **Varbinary** Datentyp anderer Länge [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgefüllt oder die Daten auf der rechten Seite abgeschnitten. Wenn andere Datentypen konvertiert **binäre** oder **Varbinary**, die Daten nach links aufgefüllt oder links abgeschnitten. Für die Auffüllung werden hexadezimale Nullen verwendet.
  
Konvertieren von Daten in der **binäre** und **Varbinary** Datentypen ist nützlich, wenn **binäre** Daten ist der einfachste Weg, um Daten zu verschieben. Geben Sie auf einem großen binären Wert ausreichend und dann wieder in den Typ führt immer den gleichen Wert, wenn beide Konvertierungen auf die gleiche Version von stattfinden Konvertieren aller Werte eines beliebigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die binäre Darstellung eines Werts kann sich zwischen den Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ändern.
  
Sie können konvertieren **Int**, **"smallint"**, und **"tinyint"** auf **binäre** oder **Varbinary**, jedoch möglich, wenn Sie Konvertieren der **binäre** Wert wieder in einen ganzzahligen Wert, dieser Wert wird von der ursprünglichen ganzzahlige Wert abgeschnitten wurde abweichen. Die folgende SELECT-Anweisung zeigt beispielsweise, dass der ganzzahlige Wert `123456` in der Regel als binärer Wert `0x0001e240` gespeichert wird:
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
Allerdings die folgenden `SELECT` Anweisung zeigt, dass bei der **binäre** Ziel ist zu klein, um den gesamten Wert aufzunehmen, die vorangestellten Nullen automatisch abgeschnitten, damit die gleiche Anzahl als gespeichert wird `0xe240`:
  
```sql
SELECT CAST( 123456 AS BINARY(2) );  
```  
  
Der folgende Batch zeigt, dass sich das automatische Abschneiden des Werts auf arithmetische Operationen auswirken kann, ohne dass ein Fehler ausgelöst wird:
  
```sql
DECLARE @BinaryVariable2 BINARY(2);  
  
SET @BinaryVariable2 = 123456;  
SET @BinaryVariable2 = @BinaryVariable2 + 1;  
  
SELECT CAST( @BinaryVariable2 AS INT);  
GO  
```  
  
Das endgültige Ergebnis ist `57921` und nicht `123457`.
  
> [!NOTE]  
>  Geben Sie Konvertierungen zwischen einem beliebigen und **binäre** Datentypen sind nicht unbedingt identisch zwischen verschiedenen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Datentypkonvertierung &#40; Datenbankmodul &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

