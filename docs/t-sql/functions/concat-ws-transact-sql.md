---
title: CONCAT_WS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 171d063e746393709629720dae40eb207d45d584
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Verkettet eine variable Anzahl von Argumenten mit einem Trennzeichen, das im ersten Argument festgelegt wird. (`CONCAT_WS` gibt die Anweisung *concatenate with separator* (mit Trennzeichen verketten) an.)

##  <a name="syntax"></a>Syntax   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>Argumente   
Trennzeichen  
Ein Ausdruck beliebigen Typs (`nvarchar`, `varchar`, `nchar` oder `char`).

argument1, argument2, argument*N*  
Ein Ausdruck eines beliebigen Typs.

## <a name="return-types"></a>Rückgabetypen
Zeichenfolge. Länge und Typ sind von der Eingabe abhängig.

## <a name="remarks"></a>Remarks   
`CONCAT_WS` lässt eine variable Anzahl von Argumenten zu und verkettet sie in einer einzelnen Zeichenfolge. Dabei wird das erste Argument als Trennzeichen verwendet. Es sind ein Trennzeichen und mindestens zwei Eingabewerte erforderlich. Andernfalls wird ein Fehler ausgelöst. Alle Argumente werden implizit in Zeichenfolgentypen konvertiert und anschließend verkettet. 

Die implizite Konvertierung in Zeichenfolgen erfolgt basierend auf den vorhandenen Regeln für Datentypkonvertierungen. Weitere Informationen zu Verhaltens- und Datentypkonvertierungen finden Sie unter [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md).

### <a name="treatment-of-null-values"></a>Behandeln von NULL-Werten

`CONCAT_WS` ignoriert die `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}`-Einstellung.

Wenn alle Argumente NULL sind, wird eine leere Zeichenfolge vom Typ `varchar(1)` zurückgegeben. 

NULL-Werte werden bei der Verkettung ignoriert und fügen keine Trennzeichen hinzu. Dadurch werden häufig verwendete Szenarios zum Verketten von Zeichenfolgen vereinfacht, die regelmäßig leere Werte wie ein zweites Adressfeld beinhalten. Siehe Beispiel B.

Wenn Ihr Szenario erfordert, dass einem Trennzeichen NULL-Werte hinzugefügt werden sollen, finden Sie Informationen in Beispiel C, in dem die `ISNULL`-Funktion verwendet wird.

## <a name="examples"></a>Beispiele   

### <a name="a--concatenating-values-with-separator"></a>A.  Verketten von Werten mit einem Trennzeichen
Das folgende Beispiel verkettet drei Spalten der sys.databases-Tabelle, wobei die Werte durch das Trennzeichen `- ` voneinander getrennt werden.   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1 - SIMPLE - NONE |
|2 - SIMPLE - NONE |
|3 - FULL - NONE |
|4 - SIMPLE - NONE |


### <a name="b--skipping-null-values"></a>B.  Überspringen von NULL-Werten
Im folgenden Beispiel werden `NULL`-Werte in der Argumentliste ignoriert.

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  Generieren einer CSV-Datei aus einer Tabelle
Im folgenden wird ein Komma als Trennzeichen verwendet und ein Wagenrücklaufzeichen hinzugefügt, sodass ein durch Kommas getrenntes Werteformat entsteht.

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, recovery_model_desc, containment_desc), char(13)) AS DatabaseInfo
FROM sys.databases
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
DatabaseInfo
------------   
1,SIMPLE,NONE
2,SIMPLE,NONE
3,FULL,NONE 
4,SIMPLE,NONE 
```

CONCAT_WS ignoriert NULL-Werte in den Spalten. Wenn einige der Spalten NULL-Werte zulassen, sollten Sie diese mit der `ISNULL`-Funktion umschließen und wie im folgenden Beispiel dargestellt einen Standardwert bereitstellen:

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>Siehe auch
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen (Transact-SQL))](../../t-sql/functions/string-functions-transact-sql.md)  

