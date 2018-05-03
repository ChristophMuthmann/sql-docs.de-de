---
title: BINARY_CHECKSUM (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
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
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 60f6c55bbb993b68609317c814e25e993df54603
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
Gibt an, dass die Berechnung für alle Spalten der Tabelle erfolgt. BINARY_CHECKSUM ignoriert in seiner Berechnung jede Spalte, die einen nicht vergleichbaren Datentyp hat. Die folgenden Datentypen sind z.B. nicht vergleichbar:  
* **Cursor**  
* **image**  
* **ntext**  
* **text**  
* **xml**  

Außerdem gehören auch benutzerdefinierte CLR-Typen (Common Language Runtime) zu den nicht vergleichbaren Datentypen.
  
*expression*  
Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) beliebigen Typs. BINARY_CHECKSUM ignoriert in seiner Berechnung jeden Ausdruck, der einen nicht vergleichbaren Datentyp hat.

## <a name="return-types"></a>Rückgabetypen  
 **int**
  
## <a name="remarks"></a>Remarks  
Wird BINARY_CHECKSUM(*) für eine beliebige Zeile einer Tabelle berechnet, gibt die Anweisung den gleichen Wert zurück, solange die Zeile nicht nachfolgend geändert wird. BINARY_CHECKSUM erfüllt die Eigenschaften einer Hashfunktion: Wenn BINARY_CHECKSUM auf zwei beliebige Listen mit Ausdrücken angewendet wird, wird immer derselbe Wert zurückgegeben, falls die entsprechenden Elemente der beiden Listen vom gleichen Typ sind und bezüglich des Vergleichs mit dem Gleichheitsoperator (=) gleich sind. Bei dieser Definition werden die NULL-Werte eines angegebenen Typs bei einem Vergleich als gleiche Werte angesehen. Wenn sich einer der Werte in der Liste mit Ausdrücken ändert, ändert sich gewöhnlich auch die Prüfsumme des Ausdrucks. Dies ist jedoch nicht immer der Fall. Daher wird empfohlen, BINARY_CHECKSUM nur zur Ermittlung von Änderungen der Daten zu verwenden, wenn Ihre Anwendung auch bei gelegentlich nicht ausgeführte Änderungen weiter ausgeführt werden kann. Wenn dies nicht der Fall ist, sollten Sie stattdessen die Verwendung von HASHBYTES in Betracht ziehen. Wenn ein MD5-Hashalgorithmus angegeben ist, ist die Wahrscheinlichkeit, dass HASHBYTES für zwei verschiedene Eingaben dasselbe Ergebnis zurückgibt, wesentlich geringer als bei der Verwendung von BINARY_CHECKSUM.
  
BINARY_CHECKSUM kann auf eine Liste von Ausdrücken angewendet werden und gibt den gleichen Wert für eine angegebene Liste zurück. Wenn BINARY_CHECKSUM auf zwei beliebige Listen von Ausdrücken angewendet wird, wird stets der gleiche Wert zurückgegeben, wenn die entsprechenden Elemente der beiden Listen denselben Typ und dieselbe Bytedarstellung haben. Für diese Definition wird bei NULL-Werten eines angegebenen Datentyps angenommen, dass sie dieselbe Bytedarstellung haben.
  
BINARY_CHECKSUM und CHECKSUM können zur Berechnung eines Prüfsummenwerts für eine Liste mit Ausdrücken verwendet werden, wobei der berechnete Wert von der Reihenfolge der Ausdrücke abhängt. Die Reihenfolge von Spalten für BINARY_CHECKSUM(*) entspricht der in der Tabellen- oder Sichtdefinition angegebenen Reihenfolge von Spalten. Dies schließt die berechneten Spalten ein.
  
CHECKSUM und BINARY_CHECKSUM geben unterschiedliche Werte für die String-Datentypen zurück, bei denen aufgrund des Gebietsschemas unterschiedliche Repräsentationen als gleich betrachtet werden können. String-Datentypen sind z.B.:  

* **char**  
* **nchar**  
* **nvarchar**  
* **varchar**  

oder  

* **sql_variant** (wenn der Basistyp von **sql_variant** ein String-Datentyp ist).  
  
Die BINARY_CHECKSUM-Werte für die Zeichenfolgen „McCavity“ und „Mccavity“ sind unterschiedlich. Bei einem Server ohne Unterscheidung nach Groß-/Kleinschreibung gibt CHECKSUM jedoch für diese Zeichenfolgen dieselben Prüfsummenwerte zurück. Sie sollten Vergleiche zwischen CHECKSUM-Werten und BINARY_CHECKSUM-Werten vermeiden.
 
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
  
  
