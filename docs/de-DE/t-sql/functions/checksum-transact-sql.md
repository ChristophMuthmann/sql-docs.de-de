---
title: CHECKSUM (Transact-SQL) | Microsoft-Dokumentation
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
- CHECKSUM_TSQL
- CHECKSUM
dev_langs:
- TSQL
helpviewer_keywords:
- hash indexes
- CHECKSUM function
- checksum values
ms.assetid: e26d3339-845c-49c2-9d89-243376874c13
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fb7fdf7e2eeb45fea9881fd2fecf8c769679b3aa
ms.sourcegitcommit: f3aa02a0f27cc1d3d5450f65cc114d6228dd9d49
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2018
---
# <a name="checksum-transact-sql"></a>CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Die `CHECKSUM`-Funktion gibt den Prüfsummenwert zurück, der für eine Zeile einer Tabelle oder eine Liste mit Ausdrücken berechnet wurde. Verwenden Sie `CHECKSUM`, um Hashindizes zu erstellen.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CHECKSUM ( * | expression [ ,...n ] )  
```  
  
## <a name="arguments"></a>Argumente  
\*  
Dieses Argument gibt an, dass die Berechnung der Prüfsumme für alle Tabellenspalten gilt. `CHECKSUM` gibt einen Fehler zurück, wenn eine Spalte einen nicht vergleichbaren Datentyp aufweist. Die folgenden Datentypen sind z.B. nicht vergleichbar:

- **Cursor**
- **image**
- **ntext**
- **text**
- **XML**

Ein weiterer nicht vergleichbarer Datentypen ist **sql_variant** mit einem der vorstehenden Typen als Basistyp.
  
*expression*  
Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Typs mit Ausnahme eines nicht vergleichbaren Datentyps.
  
## <a name="return-types"></a>Rückgabetypen
 **int**  
  
## <a name="remarks"></a>Remarks  
CHECKSUM berechnet aus der Liste der Argumente einen Hashwert, der Prüfsumme genannt wird. Verwenden Sie diesen Hashwert zum Erstellen von Hashindizes. Wenn die `CHECKSUM`-Funktion Spaltenargumente aufweist, ist das Ergebnis ein Hashindex, und ein Index für den berechneten CHECKSUM-Wert wird erstellt. Dieser kann für Gleichheitssuchen in den Spalten verwendet werden.
  
Die Funktion `CHECKSUM` erfüllt die Eigenschaften einer Hashfunktion: Wenn `CHECKSUM` auf zwei beliebige Listen mit Ausdrücken angewendet wird, wird immer derselbe Wert zurückgegeben, falls die entsprechenden Elemente der beiden Listen vom gleichen Datentyp sind und bezüglich des Vergleichs mit dem Gleichheitsoperator (=) gleich sind. NULL-Werte eines angegebenen Typs werden definiert, um zu prüfen, ob sie gleich sind (zu Zwecken der `CHECKSUM`-Funktion). Wenn sich einer der Werte in der Liste mit Ausdrücken ändert, ändert sich gewöhnlich auch die Prüfsumme der Liste. Dies ist jedoch nicht immer der Fall. Daher wird empfohlen, `CHECKSUM` nur zur Ermittlung von Änderungen der Daten zu verwenden, wenn Ihre Anwendung auch bei gelegentlich nicht ausgeführten Änderungen weiter ausgeführt werden kann. Sie sollten andernfalls in Betracht ziehen, stattdessen [HashBytes](../../t-sql/functions/hashbytes-transact-sql.md) zu verwenden. Wenn ein MD5-Hashalgorithmus angegeben ist, ist die Wahrscheinlichkeit, dass HashBytes für zwei verschiedene Eingaben dasselbe Ergebnis zurückgibt, wesentlich geringer als bei der Verwendung von CHECKSUM.
  
Die Ausdrucksreihenfolge wirkt sich auf den berechneten `CHECKSUM`-Wert aus. Die Spaltenreihenfolge, die bei CHECKSUM(\*) verwendet wird, ist die Spaltenreihenfolge, die in der Tabellen- oder Sichtdefinition angegeben ist. Dies schließt die berechneten Spalten ein.
  
Der CHECKSUM-Wert ist von der Sortierung abhängig. Der gleiche Wert gibt einen anderen CHECKSUM-Wert zurück, wenn er mit einer anderen Sortierung gespeichert ist.
  
## <a name="examples"></a>Beispiele  
In diesen Beispielen wird veranschaulicht, wie Sie mit `CHECKSUM` Hashindizes erstellen können.
  
Im ersten Beispiel wird eine Spalte für die berechnete Prüfsumme der zu indizierenden Tabelle hinzugefügt, um einen Hashindex zu erstellen. Dann wird ein Index in der Prüfsummenspalte erstellt. 
  
```sql
-- Create a checksum index.  
SET ARITHABORT ON;  
USE AdventureWorks2012;   
GO  
ALTER TABLE Production.Product  
ADD cs_Pname AS CHECKSUM(Name);  
GO  
CREATE INDEX Pname_index ON Production.Product (cs_Pname);  
GO  
```  
  
In diesem Beispiel wird veranschaulicht, wie der Prüfsummenindex als Hashindex verwendet werden kann. So verläuft die Indizierung schneller, wenn die zu indizierende Spalte eine Spalte mit langen Zeichen ist. Der Prüfsummenindex kann für die Gleichheitssuche verwendet werden.
  
```sql
/*Use the index in a SELECT query. Add a second search   
condition to catch stray cases where checksums match,   
but the values are not the same.*/  
SELECT *   
FROM Production.Product  
WHERE CHECKSUM(N'Bearing Ball') = cs_Pname  
AND Name = N'Bearing Ball';  
GO  
```  
  
Durch Erstellen des Indexes für die berechnete Spalte wird die Prüfsummenspalte materialisiert, und die Änderungen des `ProductName`-Werts werden an die Prüfsummenspalte weitergegeben. Alternativ können Sie einen Index direkt in der zu indizierenden Spalte erstellen. Bei langen Schlüsselwerten ist die Leistung eines normales Indexes wahrscheinlich geringer als die eines Prüfsummenindexes.
  
## <a name="see-also"></a>Siehe auch
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)  
[HASHBYTES &#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
[BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)
  
  
