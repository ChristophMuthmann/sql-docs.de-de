---
title: Abfragen mit Volltextsuche | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
caps.latest.revision: 80
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2c6a53f071ef3a49d36d4551346a8e0c66e68cbe
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="query-with-full-text-search"></a>Abfragen mit Volltextsuche
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Verwenden Sie zum Schreiben von Volltextabfragen die Prädikate **CONTAINS** und **FREETEXT** und die Rowsetwertfunktionen **CONTAINSTABLE** und **FREETEXTTABLE** mit einer **SELECT**-Anweisung. Dieser Artikel enthält Beispiele für jedes Prädikat und jede Funktion und hilft Ihnen dabei, das beste Prädikat bzw. die beste Funktion auszuwählen.

-   Verwenden Sie **CONTAINS** und **CONTAINSTABLE**, um Wörter und Ausdrücke zuzuordnen.
-   Verwenden Sie **FREETEXT** und **FREETEXTTABLE**,um eine Bedeutung, aber keinen genauen Wortlaut zuzuordnen.

## <a name="examples_simple"></a> Beispiele für alle Prädikate und Funktionen

In den folgenden Beispielen wird die Beispieldatenbank Adventure Works verwendet. Informationen zum endgültigen Release von Adventure Works finden Sie unter [Adventure Works Databases and Scripts for SQL Server 2016 CTP3 (Adventure Works-Datenbanken und -Skripte für SQL Server 2016 CTP3)](https://www.microsoft.com/download/details.aspx?id=49502). Sie müssen zusätzlich die Volltextsuche einrichten, um die Beispielabfragen auszuführen. Weitere Informationen finden Sie unter [Erste Schritte mit der Volltextsuche](get-started-with-full-text-search.md). 

### <a name="example---contains"></a>Beispiel - CONTAINS  
Im folgenden Beispiel werden alle Produkte mit einem Preis von `$80.99` gesucht, die das Wort `"Mountain"` enthalten:
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
### <a name="example---freetext"></a>Beispiel - FREETEXT 
 Im folgenden Beispiel wird nach allen Dokumenten gesucht, die Wörter im Zusammenhang mit `vital safety components` enthalten:
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```

### <a name="example---containstable"></a>Beispiel - CONTAINSTABLE  
 Das folgende Beispiel gibt die Beschreibungs-ID und die Beschreibung aller Produkte zurück, bei denen in der Spalte **Description** das Wort „aluminum“ in der Nähe des Worts „light“ oder „lightweight“ enthalten ist. Ausschließlich Zeilen mit einem Rang von mindestens 2 werden zurückgegeben.  
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
### <a name="example---freetexttable"></a>Beispiel: FREETEXTTABLE  
 Das folgende Beispiel erweitert eine FREETEXTTABLE-Abfrage so, dass die Zeilen mit dem höchsten Rangfolgenwert zuerst zurückgegeben werden und die Rangfolge jeder Zeile zur Auswahlliste hinzugefügt wird. Um eine ähnliche Abfrage schreiben zu können, müssen Sie wissen, dass **ProductDescriptionID** die eindeutige Schlüsselspalte der **ProductDescription**-Tabelle ist.  
  
```sql 
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
Im Folgenden finden Sie eine Erweiterung derselben Abfrage, die nur Zeilen mit einem Rang von 10 oder höher zurückgibt:  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK >= 10  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  

## <a name="match-words-or-match-meaning"></a>Übereinstimmung von Wörtern oder Bedeutungen

`CONTAINS`/`CONTAINSTABLE` und `FREETEXT` / `FREETEXTTABLE` eignen sich für verschiedene Übereinstimmungsarten. Nachfolgend finden Sie Informationen dazu, wie Sie das beste Prädikat oder die beste Funktion für die Abfrage auswählen können:

### <a name="containscontainstable"></a>CONTAINS/CONTAINSTABLE

-   Suchen Sie nach einzelnen Wörtern und Ausdrücken mit genauen oder (ungenauen) Fuzzy-Matches.
-   Sie haben außerdem folgende Möglichkeiten:
    -   Geben Sie den Abstand von Wörtern in einer bestimmten Entfernung voneinander an.
    -   Geben Sie gewichtete Übereinstimmungen zurück.
    -   Kombinieren Sie Suchbedingungen mit logischen Operatoren. Weitere Informationen finden Sie unter [Verwenden von booleschen Operatoren (AND, OR und NOT)](#Using_Boolean_Operators) weiter unten in diesem Artikel.

### <a name="freetextfreetexttable"></a>FREETEXT/FREETEXTTABLE

-   Sucht nach der Bedeutung, nicht nach dem genauen Wortlaut der angegebenen Wörter, Ausdrücke oder Sätze (*Freitextzeichenfolgen*).
-   Übereinstimmungen werden dann generiert, wenn ein Begriff oder eine Form eines Begriffs im Volltextindex einer angegebenen Spalte gefunden wird.

## <a name="compare-predicates-and-functions"></a>Vergleichen Sie Prädikate und Funktionen

Die Prädikate `CONTAINS` / `FREETEXT` und die Rowsetwertfunktionen `CONTAINSTABLE` / `FREETEXTTABLE` besitzen eine unterschiedliche Syntax und unterschiedliche Optionen. Nachfolgend finden Sie Informationen dazu, wie Sie das beste Prädikat oder die beste Funktion für die Abfrage auswählen können:

### <a name="predicates-contains-and-freetext"></a>Die Prädikate CONTAINS und FREETEXT

**Verwendung:** Verwenden Sie die Volltext-**-Prädikate** CONTAINS und FREETEXT in der WHERE- oder HAVING-Klausel einer SELECT-Anweisung.

**Ergebnisse:** Die Prädikate CONTAINS und FREETEXT geben einen TRUE- oder FALSE-Wert zurück, der angibt, ob eine bestimmte Zeile mit der Volltextabfrage übereinstimmt. Übereinstimmende Zeilen werden im Resultset zurückgegeben.

**Weitere Optionen:** Sie können diese Prädikate mit beliebigen anderen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prädikaten kombinieren, wie z.B. LIKE und BETWEEN.

Sie können entweder eine einzelne Spalte, eine Liste mit Spalten oder alle Spalten der Tabelle für die Suche auswählen.

Optional können Sie die Sprache angeben, deren Ressourcen bei der Volltextabfrage für die Wörtertrennung, die Wortstammerkennung und Thesaurus-Suchen sowie die Entfernung von Füllwörtern verwendet werden.

Sie können einen vierteiligen Namen im CONTAINS- oder FREETEXT-Prädikat zum Abfragen von volltextindizierten Spalten der Zieltabellen auf einem Verbindungsserver verwenden. Erstellen Sie zum Vorbereiten eines Remoteservers für den Empfang von Volltextabfragen einen Volltextindex für die Zieltabellen und -spalten auf dem Remoteserver, und fügen Sie anschließend den Remoteserver als Verbindungsserver hinzu.

**Weitere Informationen:** Weitere Informationen zur Syntax und zu den Argumenten dieser Prädikate finden Sie unter [CONTAINS](../../t-sql/queries/contains-transact-sql.md) und [FREETEXT](../../t-sql/queries/freetext-transact-sql.md).

### <a name="rowset-valued-functions-containstable-and-freetexttable"></a>Rowsetwertfunktionen CONTAINSTABLE und FREETEXTTABLE

**Verwendung:** Verwenden Sie die **Funktionen** CONTAINSTABLE- und FREETEXTTABLE-Funktionen wie einen herkömmlichen Tabellennamen in der FROM-Klausel einer SELECT-Anweisung.

Sie müssen die Basistabelle festlegen, um zu suchen, wenn Sie eine dieser Funktionen verwenden. Wie bei den Prädikaten können Sie eine einzelne Spalte, eine Liste mit Spalten oder alle Spalten in der Tabelle für die Suche auswählen. Außerdem können Sie optional die Sprache angeben, deren Ressourcen bei der Volltextabfrage verwendet werden sollen.

In der Regel müssen Sie die Ergebnisse von CONTAINSTABLE oder FREETEXTTABLE mit der Basistabelle verknüpfen. Um die Tabellen zusammenzufügen, müssen Sie den eindeutigen Namen der Schlüsselspalte kennen. Mit dieser Spalte, die in jeder volltextfähigen Tabelle enthalten ist, wird die Eindeutigkeit von Zeilen für die Tabelle erzwungen (die *UNIQUE**KEY-Spalte*). Weitere Informationen über die Schlüsselspalte, finden Sie unter [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md).

**Ergebnisse:** Diese Funktionen geben eine Tabelle mit null, einer oder mehreren Zeilen zurück, die mit der Volltextabfrage übereinstimmen. Die zurückgegebene Tabelle enthält nur Zeilen aus der Basistabelle, die die angegebenen Auswahlkriterien in der Volltextsuchbedingung der Funktion erfüllen.

Abfragen, die eine dieser Funktionen verwenden, geben auch wie im Folgenden dargestellt einen Relevanzrangfolgenwert (RANK) und einen Volltextschlüssel (KEY) für jede Zeile zurück:

-   **Schlüssel**-Spalte. Die KEY-Spalte gibt eindeutige Werte der zurückgegebenen Zeilen zurück. Die KEY-Spalte kann verwendet werden, um Auswahlkriterien anzugeben.
-   **Rank**-Spalte. Die RANK-Spalte gibt einen *Rangwert* für jede Zeile zurück, der angibt, wie gut die Zeilen mit den Auswahlkriterien übereinstimmen. Je höher der Rangwert des Textes oder Dokuments in einer Zeile ist, desto relevanter ist die Zeile für die betreffende Volltextabfrage. Unterschiedliche Zeilen können denselben Rang haben. Sie können die Anzahl zurückgegebener Übereinstimmungen mit dem optionalen Parameter *top_n_by_rank* einschränken. Weitere Informationen finden Sie unter [Einschränken von Suchergebnissen mit RANK](../../relational-databases/search/limit-search-results-with-rank.md).

**Weitere Informationen:** Weitere Informationen zur Syntax und den Argumenten dieser Funktionen finden Sie unter [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) und [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md).

## <a name="examples_specific"></a> Bestimmte Suchvorgangsarten

###  <a name="Simple_Term"></a>Suchen Sie nach einem bestimmten Wort oder Ausdruck (einfacher Begriff)  
 Sie können in einer Tabelle mithilfe von [CONTAINS](../../t-sql/queries/contains-transact-sql.md), [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md), [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)oder [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) nach einem bestimmten Wort oder Ausdruck suchen. Wenn Sie z.B. die Tabelle **ProductReview** in der Datenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nach allen Kommentaren zu einem Produkt mit dem Begriff „learning curve“ durchsuchen möchten, können Sie das CONTAINS-Prädikat wie folgt verwenden:  
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
Die Suchbedingung, in diesem Fall „learning curve“, kann komplex sein und aus einem oder mehreren Begriffen bestehen.

#### <a name="more-info-about-simple-term-searches"></a>Weitere Informationen zu Suchvorgängen nach Begriffen

Bei der Volltextsuche handelt es sich bei einem *Wort* (oder einem *Token*) um eine Zeichenfolge, deren Grenzen gemäß den linguistischen Regeln der angegebenen Sprache von entsprechenden Wörtertrennungen identifiziert werden. Ein gültiger *Ausdruck* besteht aus mehreren Wörtern mit oder ohne Satzzeichen dazwischen.

So ist z. B. "croissant" ein Wort, während "café au lait" ein Ausdruck ist. Solche Wörter und Ausdrücke werden als einfache Begriffe bezeichnet.

[CONTAINS](../../t-sql/queries/contains-transact-sql.md) und [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) suchen nach einer genauen Entsprechung für den Ausdruck. [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) und [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) teilen den Ausdruck in separate Wörter auf.

###  <a name="Prefix_Term"></a>Suche nach einem Wort mit einem Präfix (Präfixbegriff)  
 Sie können [CONTAINS](../../t-sql/queries/contains-transact-sql.md) oder [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) verwenden, um nach Wörtern oder Ausdrücken mit einem angegebenen Präfix zu suchen. Alle Einträge in der Spalte, die Text enthalten und mit dem angegebenen Präfix beginnen, werden zurückgegeben. So suchen Sie beispielsweise nach allen Zeilen die das Präfix `top`enthalten, z. B. `top``ple`, `top``ping`und `top`. Die Abfrage sieht folgendermaßen aus:  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 Es werden alle Textstellen zurückgegeben, die mit dem Text vor dem Sternchen (*) übereinstimmen. Wenn der Text und das Sternchen nicht in doppelte Anführungszeichen eingeschlossen sind, wie in `CONTAINS (DESCRIPTION, 'top*')`, wird das Sternchen von der Volltextsuche nicht als Platzhalter betrachtet.  
  
 Ist der Präfixbegriff ein Ausdruck, wird jedes Token, das Teil des Ausdrucks ist, als gesonderter Präfixbegriff behandelt. Es werden alle Zeilen mit Wörtern, die mit den Präfixbegriffen beginnen, zurückgegeben. So werden z.B. mit dem Präfixbegriff „light bread*“ Zeilen mit dem Text „light breaded“, „lightly breaded“ oder „light bread“ gefunden, aber nicht „lightly toasted bread“.

#### <a name="more-info-about-prefix-searches"></a>Weitere Informationen zur Präfixsuche

Ein *Präfixbegriff* ist eine Zeichenfolge, die einem Wort vorangestellt ist, um ein abgeleitetes Wort oder eine Flexionsform zu erhalten.

-   Bei einem einzelnen Präfixbegriff sind alle Wörter, die mit dem angegebenen Ausdruck beginnen, Teil des Resultsets. Der Ausdruck „Auto*“ ergibt also Übereinstimmungen mit „automatic“, „automobile“ usw.

-   Im Falle eines Ausdrucks wird jedes Wort innerhalb des Ausdrucks als Präfixbegriff interpretiert. Der Begriff „auto tran\*“ entspricht z.B. „automatic transmission“ und „automobile transducer“, aber nicht „automatic motor transmission“.

Die Präfixsuche wird durch [CONTAINS](../../t-sql/queries/contains-transact-sql.md) und [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) unterstützt.
  
###  <a name="Inflectional_Generation_Term"></a>Suchen nach Flexionsformen eines bestimmten Worts (Generierungsbegriff)  
Sie können mithilfe von [CONTAINS](../../t-sql/queries/contains-transact-sql.md), [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md), [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)oder [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) nach allen unterschiedlichen Zeiten und Konjugationen eines Verbs oder sowohl die Singular- als auch die Pluralform eines Substantivs (Flexionssuche) bzw. nach Synonymen eines bestimmten Worts (Thesaurussuche) suchen.  
  
Im folgenden Beispiel wird nach einer Form von „foot“ („foot“, „feet“ usw.) in der `Comments` -Spalte der `ProductReview`-Tabelle in der `AdventureWorks`-Datenbank gesucht: 
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
Die Volltextsuche verwendet *Wortstammerkennungen*, über die Sie die unterschiedlichen Zeiten und Konjugationen eines Verbs suchen oder sowohl die Singular- als auch die Pluralform eines Substantivs suchen können. Weitere Informationen zur Wortstammerkennung finden Sie unter [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  

#### <a name="more-info-about-generation-term-searches"></a>Weitere Informationen zu Generierungsbegriffsuchen

Bei den *Flexionsformen* handelt es sich um die verschiedenen Tempora und Konjugationen eines Verbs oder die Singular- und Pluralformen eines Substantivs.

Suchen Sie z.B. nach der Flexionsform des Worts „drive“. Wenn mehrere Zeilen in der Tabelle die Wörter „drive“, „drives“, „drove“, „driving“ und „driven“ enthalten, werden alle in das Resultset aufgenommen, da jedes dieser Wörter durch Flexion aus dem Wort „drive“ generiert werden kann.

[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) und [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) suchen standardmäßig nach den Flexionsformen aller angegebenen Wörter. [CONTAINS](../../t-sql/queries/contains-transact-sql.md) und [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) unterstützen ein optionales `INFLECTIONAL`-Argument.

### <a name="search-for-synonyms-of-a-specific-word"></a>Suche nach Synonymen eines bestimmten Worts

Ein *Thesaurus* definiert vom Benutzer angegebene Synonyme für Ausdrücke. Weitere Informationen zu Thesaurusdateien finden Sie unter [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).

Wird einem Thesaurus beispielsweise ein Eintrag „{car, automobile, truck, van}“ hinzugefügt, können Sie nach der Thesaurusform des Worts „car“ suchen. Alle Zeilen in der abgefragten Tabelle, die die Wörter „automobile“, „truck“, „van“ oder „car“ enthalten, werden im Resultset angezeigt, weil jedes dieser Wörter zum Synonymerweiterungssatz gehört, der das Wort „car“ enthält.

[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) und [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) verwenden standardmäßig den Thesaurus. [CONTAINS](../../t-sql/queries/contains-transact-sql.md) und [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) unterstützen ein optionales `THESAURUS`-Argument.

### <a name="search-for-a-word-near-another-word"></a>Suche nach einem Wort, das in der Nähe eines anderen Worts auftaucht (NEAR-Suche)

Ein *Näherungsbegriff* bezeichnet Wörter oder Ausdrücke, die sich in Nähe zueinander befinden. Sie können auch die maximale Anzahl von nicht als Suchkriterium festgelegten Begriffen angeben, die zwischen dem ersten und dem letzten Suchbegriff liegen. Außerdem können Sie in einer beliebigen Reihenfolge oder in der angegebenen Reihenfolge nach Wörtern oder Ausdrücken suchen.

Suchen Sie beispielsweise die Zeilen, in denen sich das Wort „ice“ in der Nähe des Worts „hockey“ oder sich der Ausdruck „ice skating“ in der Nähe des Ausdrucks „ice hockey“ befindet. 

[CONTAINS](../../t-sql/queries/contains-transact-sql.md) und [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)

Weitere Informationen zur NEAR-Suche finden Sie unter [Suchen von Wörtern in der Nähe eines anderen Worts mit NEAR](search-for-words-close-to-another-word-with-near.md).

###  <a name="Weighted_Term"></a>Suchen Sie nach Wörtern oder Ausdrücken mit gewichteten Werten (gewichteter Begriff)  
Sie können [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) verwenden, um nach Wörtern oder Ausdrücken zu suchen und einen Gewichtungswert anzugeben. Die Gewichtung, gemessen als eine Zahl von 0,0 bis 1,0, gibt die Bedeutung für jedes Wort und jeden Ausdruck in einer Gruppe von Wörtern und Ausdrücken an. Der Gewichtungswert 0.0 ist der niedrigste, und 1.0 ist der höchste mögliche Wert.  
  
Im folgenden Beispiel ist eine Abfrage dargestellt, die mithilfe von Gewichtungen nach allen Kundenadressen sucht, in denen Text, der mit der Zeichenfolge „Bay“ beginnt, entweder „Street“ oder „View“ enthält. Die Zeilen, die mehrere der angegebenen Wörter enthalten, erhalten einen höheren Rang in den Ergebnissen.  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT AddressLine1, KEY_TBL.RANK   
FROM Person.Address AS Address INNER JOIN  
CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("Bay*,"   
         Street WEIGHT(0.9),   
         View WEIGHT(0.1)  
         ) ' ) AS KEY_TBL  
ON Address.AddressID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 Ein gewichteter Begriff kann in Verbindung mit jedem einfachen Begriff, einem Präfixbegriff, einem Generierungsbegriff oder einem NEAR-Begriff verwendet werden.

#### <a name="more-info-about-weighted-term-searches"></a>Weitere Informationen zu Suchvorgängen nach gewichteten Begriffen

In einer Suche nach einem gewichteten Begriff gibt der *Gewichtungswert* für jedes Wort und jeden Ausdruck in einer Gruppe von Wörtern und Ausdrücken den Grad der Wichtigkeit an. Der Gewichtungswert 0,0 ist der niedrigste, und 1,0 ist der höchste mögliche Wert.

Sie können beispielsweise in einer Abfrage, in der nach mehreren Begriffen gesucht wird, jedem Suchwort einen Gewichtungswert zuweisen, der dessen Bedeutung im Vergleich zu den anderen Wörtern in der Suchbedingung angibt. In den Ergebnissen für diesen Abfragetyp werden die relevantesten Zeilen zuerst zurückgegeben, entsprechend der relativen Gewichtung, die Sie den Suchwörtern zugewiesen haben. Das Resultset enthält Dokumente oder Zeilen mit beliebigen angegebenen Ausdrücken (bzw. dem umgebenden Inhalt). Einige Ergebnisse werden jedoch als relevanter bewertet, weil den einzelnen Suchausdrücken verschiedene Gewichtungswerte zugeordnet sind.

Die Suche nach dem gewichteten Begriff wird durch [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) unterstützt.

##  <a name="Using_Boolean_Operators"></a> Verwenden der booleschen Operatoren AND, OR und NOT
 
Das CONTAINS-Prädikat und die CONTAINSTABLE-Funktion verwenden dieselben Suchbedingungen. Beide unterstützen das Kombinieren mehrerer Suchbegriffe mit booleschen Operatoren – AND, OR, und NOT –, um logische Operationen auszuführen. Mit AND können Sie z.B. Zeilen suchen, die sowohl „Latte“ als auch „New York-style bagel“ enthalten. Mit AND NOT können Sie z.B. Zeilen suchen, die zwar „Bagel“, aber nicht „cream cheese“ enthalten.  
  
Im Gegensatz dazu behandeln FREETEXT und FREETEXTTABLE die booleschen Begriffe als Wörter, nach denen gesucht werden soll.  
  
 Informationen zum Kombinieren von CONTAINS mit anderen Prädikaten, die die logischen Operatoren AND, OR und NOT unterstützen, finden Sie unter [Suchbedingung &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das CONTAINS-Prädikat für die Suche nach Beschreibungen verwendet, deren Beschreibungs-ID ungleich 5 ist und die das Wort "Aluminum" und das Wort "spindle" enthalten. In der Suchbedingung wird der boolesche AND-Operator verwendet. In diesem Beispiel wird die ProductDescription-Tabelle der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
##  <a name="Additional_Considerations"></a> Groß-/Kleinschreibung, Stoppwörter, Sprache und Thesaurus

 Beim Schreiben von Volltextabfragen können Sie auch die folgenden Optionen angeben:
  
-   **Unterscheidung nach Groß-/Kleinschreibung**. Bei Volltextabfragen wird nicht nach Groß- und Kleinschreibung unterschieden. Im Japanischen gibt es allerdings mehrere phonetische Orthografien, bei denen das Konzept der orthografischen Normalisierung ähnlich der Nichtunterscheidung nach Groß-/Kleinschreibung ist (z. B. kana = keine Unterscheidung). Diese Art orthografischer Normalisierung wird nicht unterstützt.  

-   **Stoppwörter**. Wenn Sie eine Volltextabfrage definieren, ignoriert das Volltextmodul Stoppwörter (auch als Füllwörter bezeichnet) in den Suchkriterien. Stoppwörter sind Wörter wie Artikel ("ein" oder "der"), Konjunktionen ("und") oder Hilfsverben ("ist"), die häufig vorkommen können, jedoch bei der Suche nach bestimmtem Text nicht hilfreich sind. Stoppwörter werden in einer Stoppliste aufgelistet. Jedem Volltextindex ist eine bestimmte Stoppliste zugeordnet, die festlegt, welche Stoppwörter bei Abfragen oder im Index während der Indizierung ignoriert werden. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  

-   **Sprache**, mit der **Language**-Option. Viele Abfrageausdrücke hängen sehr vom Verhalten bei Wörtertrennungen ab. Um sicherzustellen, dass Sie die richtige Wörtertrennung (und Wortstammerkennung) sowie die richtige Thesaurusdatei verwenden, wird empfohlen, die LANGUAGE-Option anzugeben. Weitere Informationen finden Sie unter [Auswählen einer Sprache beim Erstellen eines Volltextindex](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
-   **Thesaurus**. FREETEXT- und FREETEXTTABLE-Abfragen verwenden standardmäßig den Thesaurus. CONTAINS und CONTAINSTABLE unterstützen ein optionales THESAURUS-Argument. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](configure-and-manage-thesaurus-files-for-full-text-search.md).
  
##  <a name="tokens"></a>Überprüfen Sie die Ergebnisse der Tokenisierung

Nachdem Sie eine entsprechende Kombination aus Wörtertrennung, Thesaurus und Stoppliste auf eine Abfrage angewendet haben, können Sie sehen, wie die Volltextsuche die Ergebnisse zerlegt, indem Sie die dynamische Verwaltungssicht **sys.dm_fts_parser** verwenden. Weitere Informationen finden Sie unter [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [Erstellen von Volltextsuchabfragen &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [Verbessern der Leistung von Volltextabfragen](../../relational-databases/search/improve-the-performance-of-full-text-queries.md)
 
