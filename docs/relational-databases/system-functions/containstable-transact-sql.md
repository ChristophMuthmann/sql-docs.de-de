---
title: CONTAINSTABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONTAINSTABLE
- CONTAINSTABLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- precise or fuzzy (less precise) matches [full-text search]
- fuzzy (less precise) word or phrase search [full-text search]
- word searches [full-text search]
- weighted values [full-text search]
- values [SQL Server], ranked
- LANGUAGE option
- NEAR option [full-text search]
- RANK column
- phrase searches [full-text search]
- conditions [SQL Server], CONTAINSTABLE
- relevance ranking values [full-text search]
- proximity searches [full-text search]
- CONTAINSTABLE function (Transact-SQL)
- ranked results [full-text search]
- rankings [full-text search]
- less precise (fuzzy) searches [full-text search]
ms.assetid: e580c210-cf57-419d-9544-7f650f2ab814
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3d624c4a1569b6b42683463f4a2448273b7283f1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="containstable-transact-sql"></a>CONTAINSTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Tabelle mit 0 (null), einer oder mehreren Zeilen für alle Spalten mit genauen oder ungenauen (Fuzzy-) Übereinstimmungen mit einzelnen Wörtern und Satzteilen, für den Abstand von Wörtern innerhalb einer bestimmten Entfernung voneinander oder gewichtete Übereinstimmungen. CONTAINSTABLE wird verwendet, der [FROM-Klausel](../../t-sql/queries/from-transact-sql.md) von einem [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT-Anweisung und als handele es sich um einen regulären Tabellennamen verwiesen wird. Es wird eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Volltextsuche für volltextindizierte Spalten mit zeichenbasierten Datentypen durchgeführt.  
  
 CONTAINSTABLE eignet sich für dieselben Arten von Übereinstimmungen als die [CONTAINS-Prädikat](../../t-sql/queries/contains-transact-sql.md) und verwendet die gleichen suchbedingungen wie CONTAINS.  
  
 Im Gegensatz zu CONTAINS werden bei Abfragen mit CONTAINSTABLE ein Relevanzrangfolgenwert (Relevance Ranking Value, RANK) und ein Volltextschlüssel (KEY) für jede Zeile zurückgeben.  Informationen zu den Formen der Volltextsuche, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt werden, finden Sie unter [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CONTAINSTABLE   
( table , { column_name | ( column_list ) | * } , ' <contains_search_condition> '   
     [ , LANGUAGE language_term]   
  [ , top_n_by_rank ]   
)   
  
<contains_search_condition> ::=   
    { <simple_term>   
    | <prefix_term>   
    | <generation_term>   
    | <generic_proximity_term>   
    | <custom_proximity_term>   
    |  <weighted_term>   
    }   
    | { ( <contains_search_condition> )   
    { { AND | & } | { AND NOT | &! } | { OR | | } }   
     <contains_search_condition> [ ...n ]   
    }  
  
<simple_term> ::=   
     { word | "phrase" }  
<prefix term> ::=   
     { "word*" | "phrase*" }   
<generation_term> ::=   
     FORMSOF ( { INFLECTIONAL | THESAURUS } , <simple_term> [ ,...n ] )   
  
<generic_proximity_term> ::=   
     { <simple_term> | <prefix_term> } { { { NEAR | ~ }   
     { <simple_term> | <prefix_term> } } [ ...n ] }  
  
<custom_proximity_term> ::=   
  NEAR (   
     {  
        { <simple_term> | <prefix_term> } [ ,…n ]  
     |  
        ( { <simple_term> | <prefix_term> } [ ,…n ] )   
      [, <maximum_distance> [, <match_order> ] ]  
     }  
       )   
  
      <maximum_distance> ::= { integer | MAX }  
      <match_order> ::= { TRUE | FALSE }   
  
<weighted_term> ::=   
     ISABOUT  
    ( { {   
  <simple_term>   
  | <prefix_term>   
  | <generation_term>   
  | <proximity_term>   
  }   
   [ WEIGHT ( weight_value ) ]   
   } [ ,...n ]   
    )  
  
```  
  
## <a name="arguments"></a>Argumente  
 *table*  
 Der Name einer Tabelle, die volltextindiziert wurde. *Tabelle* kann ein ein-, zwei-, drei- oder vierteiliger Datenbankobjekt-Name sein. Bei der Abfrage einer Sicht kann nur eine volltextindizierte Basistabelle verwendet werden.  
  
 *Tabelle* dürfen keinen Servernamen und nicht in Abfragen auf Verbindungsservern verwendet werden.  
  
 *column_name*  
 Der Name einer oder mehreren Spalten, die für die Volltextsuche indiziert werden. Die Spalten können vom Typ **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** oder **varbinary(max)** sein.  
  
 *column_list*  
 Gibt an, dass verschiedene, durch Trennzeichen getrennte Spalten angegeben werden können. *column_list* muss in Klammern stehen. Sofern nicht *language_term* angegeben ist, muss die Sprache aller Spalten von *column_list* identisch sein.  
  
 \*  
 Gibt an, dass alle volltextindizierten Spalten in indizierten *Tabelle* sollte verwendet werden, um nach der angegebenen Suchbedingung zu suchen. Sofern *language_term* nicht angegeben ist, muss die Sprache aller Spalten in der Tabelle identisch sein.  
  
 LANGUAGE *language_term*  
 Ist die Sprache, deren Ressourcen für die wörtertrennung, wortstammerkennung und Thesaurus und Füllwörtern verwendet werden (oder [Stoppwort](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) als Teil der Abfrage entfernen. Dieser Parameter ist optional und kann als Zeichenfolge, ganze Zahl oder Hexadezimalwert entsprechend dem Gebietsschemabezeichner (Locale Identifier – LCID) einer Sprache angegeben werden. Wird *language_term* angegeben, wird die entsprechende Sprache auf alle Elemente der Suchbedingung angewendet. Wird kein Wert angegeben, wird die Volltextsprache der Spalte verwendet.  
  
 Wenn Dokumente anderer Sprachen zusammen als BLOBs (Binary Large Objects) in einer einzelnen Spalte gespeichert werden, legt der Gebietsschemabezeichner (LCID) eines bestimmten Dokuments die zur Indizierung seines Inhalts zu verwendende Sprache fest. Beim Abfragen einer solchen Spalte kann die Angabe von *LANGUAGE**language_term* die Wahrscheinlichkeit einer hohen Übereinstimmung steigern.  
  
 Wenn als eine Zeichenfolge angegeben *Language_term* entspricht der **Alias** Spaltenwert in der [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) -kompatibilitätssicht angezeigt.  Die Zeichenfolge muss in einfache Anführungszeichen gesetzt werden, z.B. '*language_term*'. In Form einer ganzen Zahl ist *language_term* der eigentliche Gebietsschemabezeichner, der die Sprache identifiziert. In Form eines Hexadezimalwerts ist *language_term* gleich 0x, gefolgt vom Hexadezimalwert des Gebietsschemabezeichners. Der Hexadezimalwert darf acht Ziffern nicht überschreiten, einschließlich führender Nullen.  
  
 Wird der Wert im Format Doppelbyte-Zeichensatz (Double-Byte Character Set, DBCS) angegeben, wird er von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Unicode konvertiert.  
  
 Ist die angegebene Sprache ungültig oder sind keine Ressourcen installiert, die dieser Sprache entsprechen, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler zurück. Geben Sie 0x0 als *language_term* an, um neutrale Sprachressourcen zu verwenden.  
  
 *top_n_by_rank*  
 Gibt an, dass nur die *n* höchste Übereinstimmungen in absteigender Reihenfolge zurückgegeben werden. Gilt nur, wenn auf einen ganzzahligen Wert *n*, angegeben ist. Wenn *top_n_by_rank* mit anderen Parametern kombiniert wird, werden von der Abfrage möglicherweise weniger Zeilen zurückgegeben als die Anzahl von Zeilen, die mit allen Prädikaten übereinstimmen. *Top_n_by_rank* können Sie die abfrageleistung zu erhöhen, indem Sie nur die relevantesten Treffer erneut aufrufen.  
  
 <contains_search_condition>  
 Gibt den Suchtext in *column_name* und die Bedingungen für eine Übereinstimmung an. Informationen zu suchbedingungen finden Sie unter [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 Volltextprädikate und -funktionen gelten für eine einzelne Tabelle, die im FROM-Prädikat enthalten ist. Um eine Suche in mehreren Tabellen auszuführen, können Sie eine verknüpfte Tabelle in der FROM-Klausel verwenden, um in einem Resultset zu suchen, das aus mindestens zwei Tabellen erstellt wird.  
  
 Die zurückgegebene Tabelle besitzt eine Spalte namens **Schlüssel** , Volltext-Schlüsselwerte enthält. Jede volltextindizierte Tabelle besitzt, eine Spalte, deren Werte garantiert eindeutig sein, und die Rückgabewerte die **Schlüssel** Spalte sind die Volltext-Schlüsselwerte der Zeilen, die die angegebenen Auswahlkriterien in entsprechen die Suche enthält Bedingung. Die **TableFulltextKeyColumn** Eigenschaft, die von der OBJECTPROPERTYEX-Funktion stellt die Identität des diese eindeutige Schlüsselspalte bereit. Verwenden Sie zum Abrufen der ID der Spalte der Volltextschlüssel für den Volltextindex zugeordnete **fulltext_indexes**. Weitere Informationen finden Sie unter [fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
 Geben Sie einen Join mit den CONTAINSTABLE-Zeilen an, um die gewünschten Zeilen der Originaltabelle zu erhalten. CONTAINSTABLE wird meist in folgender Form in der FROM-Klausel einer SELECT-Anweisung verwendet:  
  
```  
SELECT select_list  
FROM table AS FT_TBL INNER JOIN  
   CONTAINSTABLE(table, column, contains_search_condition) AS KEY_TBL  
   ON FT_TBL.unique_key_column = KEY_TBL.[KEY];  
```  
  
 Die von CONTAINSTABLE erstellte Tabelle enthält eine Spalte namens **Rang**. Die **Rang** Spalte ist ein Wert (von 0 bis 1000) für jede Zeile, der angibt, wie gut eine Zeile mit den Auswahlkriterien übereinstimmen. Dieser Rangwert wird in der SELECT-Anweisung üblicherweise auf folgende Weise verwendet:  
  
-   In der ORDER BY-Klausel, um die Zeilen, die in der Rangfolge oben liegen, als erste Zeilen der Tabelle zurückzugeben.  
  
-   In der Auswahlliste, um den zugeordneten Rangfolgenwert jeder Zeile anzuzeigen.  
  
## <a name="permissions"></a>Berechtigungen  
 Ausführungsberechtigungen sind nur für Benutzer mit den entsprechenden SELECT-Privilegien für die Tabelle oder die referenzierten Tabellenspalten verfügbar.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-example"></a>A. Einfaches Beispiel  
 Das folgende Beispiel erstellt und füllt eine einfache Tabelle zwei Spalten auflisten 3 Countys und die Farben in ihre Flags. Der It erstellt und füllt einen Volltextkatalog und den Index der Tabelle. Die **CONTAINSTABLE** wird die Syntax veranschaulicht. In diesem Beispiel wird veranschaulicht, wie der Rangwert höher wächst, wenn der Wert für die Suche mehrere Male erfüllt ist. In der letzten Abfrage hat Tansania der grünen und schwarzen enthält einen höheren Rang als Italien nur eines der abgefragten Farben aufweisen.  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM CONTAINSTABLE (Flags, FlagColors, 'Green') ORDER BY RANK DESC;  
SELECT * FROM CONTAINSTABLE (Flags, FlagColors, 'Green or Black') ORDER BY RANK DESC;  
```  
  
### <a name="b-returning-rank-values"></a>B. Zurückgeben von Rangwerten  
 Im folgenden Beispiel wird nach allen Produktnamen gesucht, die die Wörter "frame", "whell" oder "tire" enthalten, wobei jedes Wort anders gewichtet wird. Für jede zurückgegebene Zeile, die diese Suchkriterien entsprechen wird die relative Nähe (rangfolgenbewertung) der Übereinstimmung angezeigt. Darüber hinaus werden die Zeilen, die die höchste Einstufung erhielten, als Erstes zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Name, KEY_TBL.RANK  
    FROM Production.Product AS FT_TBL   
        INNER JOIN CONTAINSTABLE(Production.Product, Name,   
        'ISABOUT (frame WEIGHT (.8),   
        wheel WEIGHT (.4), tire WEIGHT (.2) )' ) AS KEY_TBL  
            ON FT_TBL.ProductID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
### <a name="c-returning-rank-values-greater-than-a-specified-value"></a>C. Zurückgeben von Rangwerten, die größer sind als ein angegebener Wert  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
 Im folgenden Beispiel wird in der `bracket`-Tabelle mit NEAR nach "`reflector`" in der Nähe von "`Production.Document`" gesucht. Es werden nur Zeilen mit einem Rangwert von mindestens 50 zurückgegeben.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
> [!NOTE]  
>  Wenn eine Volltextabfrage keine ganze Zahl als maximalen Abstand angibt, entspricht ein Dokument, das nur Treffer enthält, deren Abstand größer als 100 logische Begriffe ist, die NEAR-Anforderungen nicht, und der Rang ist 0.  
  
### <a name="d-returning-top-5-ranked-results-using-topnbyrank"></a>D. Zurückgeben der obersten 5 Ergebnisse mithilfe von top_n_by_rank  
 Im folgenden Beispiel wird die Beschreibung der ersten 5 Produkte zurückgegeben, bei denen die `Description`-Spalte das Wort "aluminium" in der Nähe des Worts "light" oder "lightweight" enthält.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY];  
GO  
```  
  
 `GO`  
  
### <a name="e-specifying-the-language-argument"></a>E. Angeben des LANGUAGE-Arguments  
 Im folgenden Beispiel wird die Verwendung des `LANGUAGE`-Arguments dargestellt.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      LANGUAGE N'English',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY];  
GO  
```  
  
> [!NOTE]  
>  Die Sprache *Language_term* Argumentis nicht erforderlich, für die Verwendung von *Top_n_by_rank.*  
  
## <a name="see-also"></a>Siehe auch  
 [Einschränken von Suchergebnissen mit RANK](../../relational-databases/search/limit-search-results-with-rank.md)   
 [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md)   
 [Erstellen von Volltextsuchabfragen &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  
