---
title: STRING_AGG (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords:
- STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: f2bcc8b02b0228dc403fffc4ef1c6b82557872a4
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="stringagg-transact-sql"></a>STRING_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Verkettet die Werte von Zeichenfolgenausdrücken und platziert Trennzeichenwerte zwischen diesen. Das Trennzeichen wird am Ende einer Zeichenfolge nicht hinzugefügt.
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>Argumente 

*Trennzeichen*  
Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) vom Typ `NVARCHAR` oder `VARCHAR`, der als Trennzeichen für verkettete Zeichenfolgen verwendet wird. Dieser kann ein Literal oder eine Variable sein. 

*expression*  
Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) beliebigen Typs. Ausdrücke werden während der Verkettung in `NVARCHAR`- oder `VARCHAR`-Typen konvertiert. Typen, die keine Zeichenfolgen darstellen, werden in den `NVARCHAR`-Typ konvertiert.


<order_clause>   
Geben Sie mithilfe der `WITHIN GROUP`-Klausel optional die Reihenfolge der verketteten Ergebnisse an:
```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
<order_by_expression_list>   
 
  Eine Liste von nicht konstanten [Ausdrücken](../../t-sql/language-elements/expressions-transact-sql.md), die für das Sortieren von Ergebnissen verwendet werden kann. Nur ein `order_by_expression`-Element ist pro Abfrage zulässig. Standardmäßig wird die Sortierung in aufsteigender Reihenfolge vorgenommen.   
  

## <a name="return-types"></a>Rückgabetypen 

Der Rückgabetyp hängt vom ersten Argument (Ausdruck) ab. Wenn das Eingabeargument ein Zeichenfolgentyp (`NVARCHAR`, `VARCHAR`) ist, entspricht der Ergebnistyp dem Eingabetyp. In der folgenden Tabelle werden die automatischen Konvertierungen aufgeführt:  

|Typ des Eingabeausdrucks |Ergebnis | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR(1…4000) |NVARCHAR(4000) |
|VARCHAR(1…8000) |VARCHAR(8000) |
|int, bigint, smallint, tinyint, numeric, float, real, bit, decimal, smallmoney, money, datetime, datetime2 |NVARCHAR(4000) |


## <a name="remarks"></a>Remarks  
 
Bei `STRING_AGG` handelt es sich um eine Aggregatfunktion, die alle Ausdrücke aus Zeilen zu einer einzelnen Zeichenfolge verkettet. Ausdruckswerte werden implizit in Zeichenfolgentypen konvertiert und dann verkettet. Die implizite Konvertierung in Zeichenfolgen erfolgt basierend auf den vorhandenen Regeln für Datentypkonvertierungen. Weitere Informationen zu Datentypkonvertierungen finden Sie unter [CAST und CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md). 

Wenn der Eingabeausdruck den Typ `VARCHAR` aufweist, kann das Trennzeichen nicht vom Typ `NVARCHAR` sein. 

NULL-Werte werden ignoriert, und das entsprechende Trennzeichen wird nicht hinzugefügt. Verwenden Sie wie in Beispiel B dargestellt die `ISNULL`-Funktion, um einen Platzhalter für NULL-Werte zurückzugeben.

`STRING_AGG` ist in jedem Kompatibilitätsgrad verfügbar.


## <a name="examples"></a>Beispiele 

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>A. Generieren einer Liste von Namen, die in neuen Zeilen getrennt sind 
Im folgenden Beispiel wird eine Liste von Namen in einer einzelnen Ergebniszelle erstellt, die mit Wagenrückläufen getrennt sind.
```sql
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

`NULL`-Werte, die in `name`-Zellen gefunden werden, werden im Ergebnis nicht zurückgegeben.   
> [!NOTE]  
>  Wenn Sie den Abfrage-Editor von Management Studio verwenden, kann die Option **Ergebnisse in Raster** den Wagenrücklauf nicht implementieren. Wechseln Sie zu **Ergebnisse in Text**, um das Resultset ordnungsgemäß anzuzeigen.   


### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>B. Generieren einer Liste von Namen ohne NULL-Werte, die mit Trennzeichen getrennt ist   
Im folgenden Beispiel werden NULL-Werte durch „N/A“ ersetzt. Weiterhin werden die Namen durch Trennzeichen getrennt in einer einzelnen Ergebniszelle zurückgegeben.  
```sql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
 

|CSV | 
|--- |
|John,N/A,Mike,Peter,N/A,N/A,Alice,Bob |  


### <a name="c-generate-comma-separated-values"></a>C. Generieren von durch Trennzeichen getrennten Werten 

```sql   
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Namen | 
|--- |
|Ken Sánchez (Feb 8 2003 12:00AM) <br />Terri Duffy (Feb 24 2002 12:00AM) <br />Roberto Tamburello (Dec 5 2001 12:00AM) <br />Rob Walters (Dec 29 2001 12:00AM) <br />... |

> [!NOTE]  
>  Wenn Sie den Abfrage-Editor von Management Studio verwenden, kann die Option **Ergebnisse in Raster** den Wagenrücklauf nicht implementieren. Wechseln Sie zu **Ergebnisse in Text**, um das Resultset ordnungsgemäß anzuzeigen.   
 

### <a name="d-return-news-articles-with-related-tags"></a>D. Zurückgeben von Artikeln mit zugehörigen Tags 

Artikel und Tags werden in unterschiedliche Tabellen aufgeteilt. Der Entwickler möchte eine Zeile mit allen zugehörigen Tags pro Artikel zurückgeben. Dafür wird folgende Abfrage verwendet: 
```sql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags 
FROM dbo.Article AS a       
LEFT JOIN dbo.ArticleTag AS t 
    ON a.ArticleId = t.ArticleId 
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|articleId |title |Transponder |
|--- |--- |--- |
|172 |Umfragen deuten auf knappe Wahlergebnisse hin |politics,polls,city council | 
|176 |Neue Autobahn soll Überlastung reduzieren |NULL |
|177 |Hunde sind weiterhin beliebter als Katzen |polls,animals| 

### <a name="e-generate-list-of-emails-per-towns"></a>E. Generieren einer Liste von E-Mails pro Stadt

Die folgende Abfrage sucht die E-Mail-Adressen der Angestellten und gruppiert diese nach Städten: 
```sql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Stadt |E-Mail-Adresse |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

Die E-Mail-Adressen, die in der Spalte „E-Mail-Adresse“ zurückgegeben werden, können direkt verwendet werden, um E-Mails an mehrere Personen zu senden, die in bestimmten Städten arbeiten. 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. Generieren einer sortierten Liste von E-Mails pro Stadt   
   
Ähnlich wie beim vorherigen Beispiel sucht die folgende Abfrage die E-Mail-Adressen der Angestellten, gruppiert diese nach Stadt und sortiert die E-Mail-Adressen alphabetisch:   
```sql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Stadt |E-Mail-Adresse |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |


## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Aggregate Functions &#40;Transact-SQL&#41; (Aggregatfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/aggregate-functions-transact-sql.md)  
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/string-functions-transact-sql.md)  

