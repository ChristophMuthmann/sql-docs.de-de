---
title: STRING_SPLIT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 049bdf1021d57e28ed94e11c89aa997ee0eba5e5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Teilt das angegebene Trennzeichen mit Zeichenausdruck.  
  
> [!NOTE]  
>  Die **STRING_SPLIT** -Funktion steht nur für Kompatibilitätsgrad 130 zur Verfügung. Wenn der Kompatibilitätsgrad Ihrer Datenbank kleiner als 130 ist, SQL Server ist nicht möglich zu suchen und auszuführen **STRING_SPLIT** Funktion. Sie können den Kompatibilitätsgrad der Datenbank mithilfe des folgenden Befehls ändern:  
> ALTER DATABASE Datenbankname SET COMPATIBILITY_LEVEL = 130  
>   
>  Beachten Sie, dass es sich bei Kompatibilitätsgrad 120 sogar in neuen Azure SQL-Datenbanken in der Standardeinstellung werden kann.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>Argumente  
 *Zeichenfolge*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Typs Zeichen (d. h. **Nvarchar**, **Varchar**, **Nchar** oder **Char**).  
  
 *Trennzeichen*  
 Ist ein einzelnes Zeichen [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Typs Zeichen (z. B. **nvarchar(1)**, **varchar(1)**, **NCHAR(1)-Wert** oder  **char(1)**), die als Trennzeichen für die verketteten Zeichenfolgen verwendet wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt eine einspaltige Tabelle mit Fragmenten. Der Name der Spalte ist **Wert**. Gibt **Nvarchar** Wenn keines der Eingabeargumente eines **Nvarchar** oder **Nchar**. Andernfalls gibt **Varchar**. Die Länge des Rückgabetyps ist identisch mit der Länge der Zeichenfolgenargument.  
  
## <a name="remarks"></a>Hinweise  
 **STRING_SPLIT** akzeptiert eine Zeichenfolge, die geteilt werden sollte und das Trennzeichen, die zum Teilen der Zeichenfolge verwendet werden. Es gibt eine einspaltige Tabelle mit Teilzeichenfolgen zurück. Z. B. die folgende Anweisung `SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');` mit Leerzeichen als Trennzeichen, folgende Ergebnistabelle zurückgegeben:  
  
|value|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|Amet.|  
  
 Wenn die Eingabezeichenfolge **NULL**, **STRING_SPLIT** Tabellenwert-Funktion eine leere Tabelle zurückgibt.  
  
 **STRING_SPLIT** erfordert, dass mindestens Kompatibilitätsmodus 130.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-split-comma-separated-value-string"></a>A. Teilung durch Kommas getrennte Zeichenfolge für den  
 Eine durch Trennzeichen getrennte Liste von Werten zu analysieren, und geben Sie alle nicht leeren Token zurück:  
  
```  
  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
  
```  
  
 STRING_SPLIT zurück leere Zeichenfolge, wenn es nichts zwischen Trennzeichen. Bedingung RTRIM(value) <> '' leere Token werden entfernt.  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. Teilung durch Kommas getrennte Zeichenfolge in einer Spalte  
 Product-Tabelle enthält die Spalte mit durch Trennzeichen getrennte Liste der Tags, die im folgenden Beispiel gezeigt:  
  
|"ProductID"|Name|Tags|  
|---------------|----------|----------|  
|1|Komplette Handschuhe|Clothing, Straße, touring bike|  
|2|LL Kopfhörer|Bike|  
|3|HL Mountain Frame|Fahrrad, mountain|  
  
 Folgende Abfrage transformiert jede Liste von Tags und verknüpft sie mit der ursprünglichen Zeile:  
  
```  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|"ProductID"|Name|value|  
|---------------|----------|-----------|  
|1|Komplette Handschuhe|clothing|  
|1|Komplette Handschuhe|Straße|  
|1|Komplette Handschuhe|Touring|  
|1|Komplette Handschuhe|Bike|  
|2|LL Kopfhörer|Bike|  
|3|HL Mountain Frame|Bike|  
|3|HL Mountain Frame|Mountain|  
  
### <a name="c-aggregation-by-values"></a>C. Aggregation von Werten  
 Benutzer müssen einen Bericht erstellen, die die Anzahl der Produkte pro jeden Tag, geordnet nach Anzahl der Produkte und keine weiteren Tags mit mehr als 2 Produkten zu filtern.  
  
```  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>D. Suchen Sie nach der Tag-Wert  
 Entwickler müssen Abfragen erstellen, die Artikel nach Schlüsselwörtern suchen. Sie können folgende Abfragen verwenden:  
  
 Um Produkte mit einem Tag (Bekleidung) zu suchen:  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
 Suchen von Produkten mit zwei angegebenen Tags (Bekleidung und Road):  
  
```  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>E. Suchen nach Zeilen nach Liste von Werten  
 Entwickler müssen eine Abfrage erstellen, die von einer Liste von Ids Artikel findet. Sie können folgende Abfrage:  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
 Dies ist ein Ersatz für allgemeine Antimuster z. B. das Erstellen einer dynamischen SQL-Zeichenfolge in die Anwendungsebene oder [!INCLUDE[tsql](../../includes/tsql-md.md)], oder mithilfe von LIKE-Operator:  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [TEILZEICHENFOLGE &#40; Transact-SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  

