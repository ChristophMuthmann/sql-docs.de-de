---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 377db445118e55f1bdeec220f1e6701e9f89706c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

Verkettet eine Variable Anzahl von Argumenten mit einem Trennzeichen im 1. Argument angegeben. (`CONCAT_WS` gibt *mit Trennzeichen verketten*.)

##  <a name="syntax"></a>Syntax   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>Argumente   
Trennzeichen  
Ist ein Ausdruck eines beliebigen Typs Zeichen (`nvarchar`, `varchar`, `nchar`, oder `char`).

Argument1, argument2, Argument*N*  
Ist ein Ausdruck eines beliebigen Typs.

## <a name="return-types"></a>Rückgabetypen
Zeichenfolge. Die Länge und den Typ abhängen der Eingabe.

## <a name="remarks"></a>Hinweise   
`CONCAT_WS`eine Variable Anzahl von Argumenten akzeptiert, und verkettet diese in eine einzelne Zeichenfolge, die das erste Argument als Trennzeichen verwenden. Es muss ein Trennzeichen und mindestens zwei Argumente; Andernfalls wird ein Fehler ausgelöst. Alle Argumente werden implizit in Zeichenfolgentypen konvertiert und dann verkettet werden. 

Die implizite Konvertierung in Zeichenfolgen erfolgt basierend auf den vorhandenen Regeln für Datentypkonvertierungen. Weitere Informationen zum Verhalten und typkonvertierungen finden Sie unter [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md).

### <a name="treatment-of-null-values"></a>Behandlung von NULL-Werte

`CONCAT_WS`ignoriert die `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}` Einstellung.

Wenn alle Argumente null, eine leere Zeichenfolge vom Typ `varchar(1)` zurückgegeben wird. 

NULL-Werte werden während der Verkettung ignoriert, und es werden keine Trennzeichen hinzugefügt. Dies erleichtert das gängige Szenario der Verkettung von Zeichenfolgen, die häufig leere Werte, z. B. eine zweite Adressfeld aufweisen. Siehe Beispiel b.

Wenn Ihr Szenario null-Werte enthalten, mit einem Trennzeichen erforderlich ist, finden Sie unter Beispiel C für die Verwendung der `ISNULL` Funktion.

## <a name="examples"></a>Beispiele   

### <a name="a--concatenating-values-with-separator"></a>A.  Verketten der Werte mit Trennzeichen
Im folgende Beispiel werden drei Spalten in der sys.databases-Tabelle, trennen die Werte mit verkettet eine `- `.   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1 - SIMPLE - KEINE |
|2 - SIMPLE - KEINE |
|3 VOLLSTÄNDIGE – - KEINE |
|4 - SIMPLE - KEINE |


### <a name="b--skipping-null-values"></a>B.  Überspringen von NULL-Werte
Im folgenden Beispiel wird ignoriert `NULL` Werte in der Argumentliste.

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  Generieren von CSV-Datei aus der Tabelle
Im folgenden Beispiel verwendet ein Komma als Trennzeichen und fügt das Wagenrücklaufzeichen, um das Spaltenformat getrennte Werte führen.

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

CONCAT_WS werden in den Spalten NULL-Werte ignoriert. Wenn einige der Spalten NULL-Werte zulassen sind, umschließen mit `ISNULL` -Funktion, und geben Sie Standardwert wie im folgenden Beispiel:

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>Siehe auch
[Zeichenfolgenfunktionen (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
[CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)      


