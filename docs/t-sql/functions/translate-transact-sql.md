---
title: TRANSLATE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 7fad4e27c4e0c198d093b1502affe9706b2e2269
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="translate-transact-sql"></a>TRANSLATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Gibt die Zeichenfolge zurück, die als erstes Argument bereitgestellt wurde, nachdem einige durch das zweite Argument angegebene Zeichen in einen Zielzeichensatz übersetzt wurden.

## <a name="syntax"></a>Syntax   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>Argumente   

inputString   
Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Zeichentyps (nvarchar, varchar, nchar, char).

Buchstaben   
Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Zeichentyps, der zu ersetzende Zeichen enthält.

Übersetzungen   
Ist ein [Zeichenausdruck](../../t-sql/language-elements/expressions-transact-sql.md), der mit dem Typ und der Länge des zweiten Arguments übereinstimmt.

## <a name="return-types"></a>Rückgabetypen   
Gibt einen Zeichenausdruck vom gleichen Typ wie `inputString` zurück, bei dem die Zeichen des zweiten Arguments durch die entsprechenden Zeichen des dritten Arguments ersetzt werden.

## <a name="remarks"></a>Remarks   

Die `TRANSLATE`-Funktion gibt einen Fehler zurück, wenn die Länge von Zeichen und Übersetzungen sich unterscheidet. Die `TRANSLATE`-Funktion sollte die Eingabe ohne Änderungen zurückgeben, wenn NULL-Werte als Zeichen oder Ersetzungsargumente bereitgestellt werden. Das Verhalten der `TRANSLATE`-Funktion sollte mit dem der [REPLACE](../../t-sql/functions/replace-transact-sql.md)-Funktion übereinstimmen.   

Das Verhalten der `TRANSLATE`-Funktion entspricht dem Verwenden mehrerer `REPLACE`-Funktionen.

Bei `TRANSLATE` werden SC-Sortierungen immer beachtet.

## <a name="examples"></a>Beispiele   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. Ersetzen von eckigen und geschweiften Klammern durch reguläre Klammern    
Die folgende Abfrage ersetzt eckige und geschweifte Klammern in der Eingabezeichenfolge durch Klammern:
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  Die `TRANSLATE`-Funktion in diesem Beispiel entspricht dieser Funktionsweise ebenfalls, ist jedoch einfacher als die folgende Anweisung, die `REPLACE` verwendet: `SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');` 


###  <a name="b-convert-geojson-points-into-wkt"></a>B. Konvertieren von GeoJSON-Punkten in WKT    
GeoJSON ist ein Format für das Codieren von vielen verschiedenen geografischen Datenstrukturen. Mit der `TRANSLATE`-Funktion können Entwickler GeoJSON-Punkte einfach in das WKT-Format (und umgekehrt) konvertieren. Die folgende Abfrage ersetzt eckige und geschweifte Klammern in der Eingabe durch reguläre Klammern:   
```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|Punkt  |Koordinaten |  
---------|--------- |
(137,4; 72,3) |[137,4; 72,3] |


## <a name="see-also"></a>Weitere Informationen finden Sie unter
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [Zeichenfolgenfunktionen (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   

