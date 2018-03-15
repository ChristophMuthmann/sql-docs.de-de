---
title: sql_variant (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 9/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql_variant
- sql_variant_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sql_variant comparisons
- storing data [SQL Server], sql_variant
- sql_variant data type
- storage [SQL Server], sql_variant
ms.assetid: 01229779-8bc1-4c7d-890a-8246d4899250
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 01a11cca67bbf24afa7d74d5e776a969d62920dc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sqlvariant-transact-sql"></a>sql_variant (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Ein Datentyp, der Werte verschiedener von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützter Datentypen speichert.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
sql_variant  
```  
  
## <a name="remarks"></a>Remarks  
**sql_variant** kann in Spalten, Parametern, Variablen und Rückgabewerten von benutzerdefinierten Funktionen verwendet werden. **sql_variant** ermöglicht, dass diese Datenbankobjekte auch Werte mit anderen Datentypen unterstützen.
  
Eine Spalte vom Datentyp **sql_variant** enthält möglicherweise Zeilen verschiedener Datentypen. Beispielsweise können in einer als **sql_variant** definierten Spalte die Werte **int**, **binary** und **char** gespeichert sein.
  
**sql_variant** kann eine maximale Länge von 8016 Bytes besitzen. Dies schließt sowohl die Basistypinformationen als auch den Basistypwert ein. Die maximale Länge des Basistypwerts ist 8.000 Byte.
  
Ein **sql_variant**-Datentyp muss zuerst in den Wert seines Basisdatentyps umgewandelt werden, bevor er in Operationen, beispielsweise Addition oder Subtraktion, verwendet werden kann.
  
**sql_variant** kann ein Standardwert zugewiesen werden. Dieser Datentyp kann auch NULL als zugrunde liegenden Wert haben, den NULL-Werten ist jedoch kein Basistyp zugeordnet. Außerdem kann **sql_variant** nicht der Basistyp für einen andren **sql_variant**-Datentyp sein.
  
Eindeutige Schlüssel sowie Primär- oder Fremdschlüssel können Spalten vom Datentyp **sql_variant** enthalten. Die Gesamtlänge der Datenwerte, aus denen ein Schlüssel für eine vorhandene Zeile besteht, sollte jedoch die maximale Länge eines Index nicht überschreiten. Diese beträgt 900 Bytes.
  
Eine Tabelle kann über eine beliebige Anzahl von **sql_variant**-Spalten verfügen.
  
**sql_variant** kann nicht in CONTAINSTABLE und FREETEXTTABLE verwendet werden.
  
ODBC unterstützt **sql_variant** nicht vollständig. Deshalb werden Abfragen von **sql_variant**-Spalten bei Verwendung von Microsoft OLE DB-Anbietern für ODBC (MSDASQL) als Binärdaten zurückgegeben. Eine **sql_variant**-Spalte mit den Zeichenfolgendaten „PS2091“ wird als 0x505332303931 zurückgegeben.
  
## <a name="comparing-sqlvariant-values"></a>Vergleichen von sql_variant-Werten  
Der **sql_variant**-Datentyp steht im oberen Bereich in der Hierarchieliste der Datentypen für die Konvertierung. Für **sql_variant**-Vergleiche wird die Reihenfolge der Datentyphierarchie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Datentypfamilien unterteilt.
  
|Datentyphierarchie|Datentypfamilie|  
|---|---|
|**sql_variant**|sql_variant |  
|**datetime2**|Datum und Uhrzeit|  
|**datetimeoffset**|Datum und Uhrzeit|  
|**datetime**|Datum und Uhrzeit|  
|**smalldatetime**|Datum und Uhrzeit|  
|**Datum**|Datum und Uhrzeit|  
|**Uhrzeit**|Datum und Uhrzeit|  
|**float**|Ungefährer numerischer Wert|  
|**real**|Ungefährer numerischer Wert|  
|**decimal**|Genauer numerischer Wert|  
|**money**|Genauer numerischer Wert|  
|**smallmoney**|Genauer numerischer Wert|  
|**bigint**|Genauer numerischer Wert|  
|**int**|Genauer numerischer Wert|  
|**smallint**|Genauer numerischer Wert|  
|**tinyint**|Genauer numerischer Wert|  
|**bit**|Genauer numerischer Wert|  
|**nvarchar**|Unicode|  
|**nchar**|Unicode|  
|**varchar**|Unicode|  
|**char**|Unicode|  
|**varbinary**|Binär (Binary)|  
|**binary**|Binär (Binary)|  
|**uniqueidentifier**|Uniqueidentifier |  
  
Für **sql_variant**-Vergleiche gelten die folgenden Regeln:
-   Wenn **sql_variant**-Werte unterschiedlicher Basisdatentypen verglichen werden und die Basisdatentypen verschiedenen Datentypfamilien angehören, wird der Wert als der höhere eingestuft, dessen Datentypfamilie sich weiter oben in der Hierarchieliste befindet.  
-   Wenn **sql_variant**-Werte unterschiedlicher Basisdatentypen verglichen werden und die Basisdatentypen derselben Datentypfamilie angehören, wird der Wert, dessen Basisdatentyp sich weiter unten in der Hierarchieliste befindet, implizit in den anderen Datentyp konvertiert, und dann wird der Vergleich durchgeführt.  
-   Wenn **sql_variant**-Werte der Datentypen **char**, **varchar**, **nchar** oder **nvarchar** verglichen werden, stützt sich der Vergleich zunächst auf folgende Kriterien: LCID, LCID-Version, Vergleichsflags und Sortier-ID. Diese Kriterien werden als ganzzahlige Werte und in der genannten Reihenfolge verglichen. Sind alle diese Kriterien gleich, werden die tatsächlichen Zeichenfolgenwerte entsprechend der Sortierreihenfolge verglichen.  
  
## <a name="converting-sqlvariant-data"></a>Konvertieren von sql_variant-Daten  
Bei der Verarbeitung von **sql_variant**-Datentypen unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die impliziten Konvertierungen von Objekten mit anderen Datentypen in den Typ **sql_variant**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt jedoch keine impliziten Konvertierungen von **sql_variant**-Daten in ein Objekt mit einem anderen Datentyp.
  
## <a name="restrictions"></a>Restrictions  
In der folgenden Tabelle werden die Typen von Werten aufgelistet, die nicht mithilfe von **sql_variant** gespeichert werden können:
  
|||  
|-|-|  
|**varchar(max)**|**varbinary(max)**|  
|**nvarchar(max)**|**xml**|  
|**text**|**ntext**|  
|**image**|**rowversion** (**timestamp**)|  
|**sql_variant**|**geography**|  
|**hierarchyid**|**Geometrie**|  
|Benutzerdefinierte Typen|**datetimeoffset**|  

## <a name="examples"></a>Beispiele  

### <a name="a-using-a-sqlvariant-in-a-table"></a>A. Verwenden von sql_variant in einer Tabelle  
 Im folgenden Beispiel wird eine Tabelle mit einem sql_variant-Datentyp erstellt. Dann wird im Beispiel `SQL_VARIANT_PROPERTY`-Informationen über den `colA`-Wert `46279.1` abgerufen, wobei `colB` =`1689` und `tableA` über `colA` vom Typ `sql_variant` und `colB` verfügt.  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Beachten Sie, dass jeder dieser drei Werte vom Datentyp **sql_variant** ist.  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>B. Verwenden von sql_variant als Variable   
 Das folgende Beispiel erstellt eine Variable unter Verwendung des sql_variant-Datentyps und ruft dann `SQL_VARIANT_PROPERTY`-Informationen zu einer Variable mit dem Namen @v1 ab.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```    


## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  
