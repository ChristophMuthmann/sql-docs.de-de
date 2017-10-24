---
title: BINARY_CHECKSUM (Transact-SQL) | Microsoft Docs
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
- BINARY_CHECKSUM
- BINARY_CHECKSUM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BINARY_CHECKSUM function
- binary [SQL Server], checksum values
ms.assetid: 07fece4d-58e3-446e-a3b5-92fe24d2d1fb
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b84847f3efe7224c6fa0ad945b03f3afbc1381b9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="binarychecksum--transact-sql"></a>BINARY_CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Gibt den binären Prüfsummenwert zurück, der für eine Zeile einer Tabelle oder eine Liste von Ausdrücken berechnet wurde.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
BINARY_CHECKSUM ( * | expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argumente  
*\**  
Gibt an, dass die Berechnung für alle Spalten der Tabelle erfolgt. BINARY_CHECKSUM ignoriert in seiner Berechnung jede Spalte, die einen nicht vergleichbaren Datentyp hat. Nicht vergleichbare Datentypen umfassen **Text**, **Ntext**, **Image**, **Cursor**, **Xml**, und nicht vergleichbare Typen common Language Runtime (CLR) eine benutzerdefinierte.
  
*expression*  
Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Typs. BINARY_CHECKSUM ignoriert in seiner Berechnung jeden Ausdruck, der einen nicht vergleichbaren Datentyp hat.
  
## <a name="remarks"></a>Hinweise  
Wird BINARY_CHECKSUM(*) für eine beliebige Zeile einer Tabelle berechnet, gibt die Anweisung den gleichen Wert zurück, solange die Zeile nicht nachfolgend geändert wird. BINARY_CHECKSUM erfüllt die Eigenschaften einer Hashfunktion: BINARY_CHECKSUM auf zwei beliebige Listen mit Ausdrücken angewendet wird derselbe Wert zurückgegeben, wenn die entsprechenden Elemente der beiden Listen denselben Typ haben und bei einem Vergleich mit dem Gleichheitsoperator (=) gleich sind. Bei dieser Definition wird für NULL-Werte eines angegebenen Typs angenommen, dass sie bei einem Vergleich "gleich" sind. Wenn sich einer der Werte in der Liste mit Ausdrücken ändert, ändert sich gewöhnlich auch die Prüfsumme der Liste. Es besteht jedoch eine geringe Möglichkeit, dass sich die Prüfsumme nicht ändert. Aus diesem Grund wird nicht empfohlen mit BINARY_CHECKSUM um zu erkennen, ob die Werte geändert haben, es sei denn, Ihre Anwendung tolerieren kann gelegentlich eine Änderung. Erwägen Sie stattdessen HashBytes. Wenn ein MD5-Hash-Algorithmus angegeben wird, ist die Wahrscheinlichkeit, dass HashBytes für zwei verschiedene Eingaben dasselbe Ergebnis zurückgeben wesentlich geringer als bei BINARY_CHECKSUM.
  
BINARY_CHECKSUM kann auf eine Liste von Ausdrücken angewendet werden und gibt den gleichen Wert für eine angegebene Liste zurück. Wenn BINARY_CHECKSUM auf zwei beliebige Listen von Ausdrücken angewendet wird, wird stets der gleiche Wert zurückgegeben, wenn die entsprechenden Elemente der beiden Listen denselben Typ und dieselbe Bytedarstellung haben. Für diese Definition wird bei NULL-Werten eines angegebenen Datentyps angenommen, dass sie dieselbe Bytedarstellung haben.
  
BINARY_CHECKSUM und CHECKSUM können zur Berechnung eines Prüfsummenwerts für eine Liste mit Ausdrücken verwendet werden, wobei der berechnete Wert von der Reihenfolge der Ausdrücke abhängt. Die Reihenfolge von Spalten für BINARY_CHECKSUM(*) entspricht der in der Tabellen- oder Sichtdefinition angegebenen Reihenfolge von Spalten. Dazu gehören berechnete Spalten.
  
CHECKSUM und BINARY_CHECKSUM geben unterschiedliche Werte für die Zeichenfolgen-Datentypen zurück, bei denen aufgrund des Gebietsschemas unterschiedliche Repräsentationen als gleich betrachtet werden können. Die Zeichenfolgen-Datentypen sind **Char**, **Varchar**, **Nchar**, **Nvarchar**, oder **Sql_variant** (wenn die der Basistyp des **Sql_variant** ist ein String-Datentyp). Die BINARY_CHECKSUM-Werte für die Zeichenfolgen "McCavity" und "Mccavity" sind unterschiedlich. Bei einem Server ohne Unterscheidung nach Groß-/Kleinschreibung gibt CHECKSUM jedoch für diese Zeichenfolgen dieselben Prüfsummenwerte zurück. CHECKSUM-Werte sollten nicht mit BINARY_CHECKSUM-Werten verglichen werden.
 
BINARY_CHECKSUM unterstützt bis zu 8.000 Zeichen vom Typ **varbinary(max)** und bis zu 255 Zeichen vom Typ **nvarchar(max)**.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird `BINARY_CHECKSUM` verwendet, um Änderungen in einer Zeile einer Tabelle zu erkennen.
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable (column1 int, column2 varchar(256));  
GO  
INSERT INTO myTable VALUES (1, 'test');  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
UPDATE myTable set column2 = 'TEST';  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[Aggregatfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[CHECKSUM &#40; Transact-SQL &#41;](../../t-sql/functions/checksum-transact-sql.md)  
[CHECKSUM_AGG &#40; Transact-SQL &#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
  
  

