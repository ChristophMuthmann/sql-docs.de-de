---
title: BINARY_CHECKSUM (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9ff8368877b3fb2153685554f1484b5fbbcc7c3a
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="binarychecksum--transact-sql"></a>BINARY_CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Gibt den binären Prüfsummenwert zurück, der für eine Zeile einer Tabelle oder eine Liste von Ausdrücken berechnet wurde.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
BINARY_CHECKSUM ( * | expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argumente  
*\**  
Gibt an, dass die Berechnung für alle Spalten der Tabelle erfolgt. BINARY_CHECKSUM ignoriert in seiner Berechnung jede Spalte, die einen nicht vergleichbaren Datentyp hat. Folgende Datentypen zählen zu den nicht vergleichbaren Datentypen: **text**, **ntext**, **image**, **cursor** und **xml** sowie nicht vergleichbare, benutzerdefinierte CLR-Typen (Common Language Runtime).
  
*expression*  
Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) beliebigen Typs. BINARY_CHECKSUM ignoriert in seiner Berechnung jeden Ausdruck, der einen nicht vergleichbaren Datentyp hat.

## <a name="return-types"></a>Rückgabetypen  
 **int**
  
## <a name="remarks"></a>Remarks  
Wird BINARY_CHECKSUM(*) für eine beliebige Zeile einer Tabelle berechnet, gibt die Anweisung den gleichen Wert zurück, solange die Zeile nicht nachfolgend geändert wird. BINARY_CHECKSUM erfüllt die Eigenschaften einer Hashfunktion: Wenn BINARY_CHECKSUM auf zwei beliebige Listen mit Ausdrücken angewendet wird, wird immer derselbe Wert zurückgegeben, falls die entsprechenden Elemente der beiden Listen vom gleichen Typ sind und bezüglich des Vergleichs mit dem Gleichheitsoperator (=) gleich sind. Bei dieser Definition wird für NULL-Werte eines angegebenen Typs angenommen, dass sie bei einem Vergleich "gleich" sind. Wenn sich einer der Werte in der Liste mit Ausdrücken ändert, ändert sich gewöhnlich auch die Prüfsumme der Liste. Es besteht jedoch eine geringe Möglichkeit, dass sich die Prüfsumme nicht ändert. Aus diesem Grund wird nicht empfohlen, BINARY_CHECKSUM für die Überprüfung auf geänderte Werte zu verwenden, außer es spielt für die Anwendung keine große Rolle, wenn gelegentlich eine Änderung nicht erkannt wird. Sie sollten in Betracht ziehen, stattdessen HashBytes verwenden. Wenn ein MD5-Hashalgorithmus angegeben wird, ist die Wahrscheinlichkeit, dass HashBytes für zwei verschiedene Eingaben dasselbe Ergebnis zurückgibt, wesentlich geringer als bei BINARY_CHECKSUM.
  
BINARY_CHECKSUM kann auf eine Liste von Ausdrücken angewendet werden und gibt den gleichen Wert für eine angegebene Liste zurück. Wenn BINARY_CHECKSUM auf zwei beliebige Listen von Ausdrücken angewendet wird, wird stets der gleiche Wert zurückgegeben, wenn die entsprechenden Elemente der beiden Listen denselben Typ und dieselbe Bytedarstellung haben. Für diese Definition wird bei NULL-Werten eines angegebenen Datentyps angenommen, dass sie dieselbe Bytedarstellung haben.
  
BINARY_CHECKSUM und CHECKSUM können zur Berechnung eines Prüfsummenwerts für eine Liste mit Ausdrücken verwendet werden, wobei der berechnete Wert von der Reihenfolge der Ausdrücke abhängt. Die Reihenfolge von Spalten für BINARY_CHECKSUM(*) entspricht der in der Tabellen- oder Sichtdefinition angegebenen Reihenfolge von Spalten. Dazu gehören berechnete Spalten.
  
CHECKSUM und BINARY_CHECKSUM geben unterschiedliche Werte für die Zeichenfolgen-Datentypen zurück, bei denen aufgrund des Gebietsschemas unterschiedliche Repräsentationen als gleich betrachtet werden können. Die Zeichenfolgendatentypen lauten **char**, **varchar**, **nchar**, **nvarchar**, oder **sql_variant** (wenn es sich bei dem Basistyp von **sql_variant** um einen Zeichenfolgendatentyp handelt). Die BINARY_CHECKSUM-Werte für die Zeichenfolgen "McCavity" und "Mccavity" sind unterschiedlich. Bei einem Server ohne Unterscheidung nach Groß-/Kleinschreibung gibt CHECKSUM jedoch für diese Zeichenfolgen dieselben Prüfsummenwerte zurück. CHECKSUM-Werte sollten nicht mit BINARY_CHECKSUM-Werten verglichen werden.
 
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
[Aggregate Functions &#40;Transact-SQL&#41; (Aggregatfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
  
  
