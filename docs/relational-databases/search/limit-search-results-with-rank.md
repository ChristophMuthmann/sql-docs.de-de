---
title: "Einschränken von Suchergebnissen mit RANK | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- row ranking [full-text search]
- relevance ranking values [full-text search]
- full-text search [SQL Server], rankings
- index rankings [full-text search]
- ranked results [full-text search]
- rankings [full-text search]
- per-row rank values [full-text search]
ms.assetid: 06a776e6-296c-4ec7-9fa5-0794709ccb17
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aec9bea3dabdf53867f6346ac10ee42d7b2e297a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="limit-search-results-with-rank"></a>Einschränken von Suchergebnissen mit RANK
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Die Funktionen [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) und [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) geben eine Spalte mit dem Namen RANK zurück, die Ordinalwerte zwischen 0 und 1.000 (Rangwerte) enthält. Diese Werte werden verwendet, um die Rangfolge der zurückgegebenen Zeilen gemäß ihrer Übereinstimmung mit den Auswahlkriterien festzulegen. Die Rangwerte geben lediglich eine relative Relevanzreihenfolge der Zeilen im Resultset an, wobei ein niedrigerer Wert eine niedrigere Relevanz anzeigt. Die tatsächlichen Werte sind nicht von Bedeutung und unterscheiden sich i. d. R. bei jeder Ausführung der Abfrage.  
  
> [!NOTE]  
>  Die CONTAINS- und FREETEXT-Prädikate geben keine Rangwerte zurück.  
  
 Die Anzahl der Elemente, die eine Suchbedingung erfüllen, ist oft sehr groß. Damit CONTAINSTABLE- oder FREETEXTTABLE-Abfragen nicht zu viele Übereinstimmungen zurückgeben, können Sie den optionalen *top_n_by_rank* -Parameter verwenden, mit dem nur eine Teilmenge der Zeilen zurückgegeben wird. *top_n_by_rank* ist ein Integer-Wert ( *n*) mit dem festgelegt wird, dass nur die *n* höchsten Übereinstimmungen in absteigender Reihenfolge zurückgegeben werden. Wenn *top_n_by_rank* mit anderen Parametern kombiniert wird, werden von der Abfrage möglicherweise weniger Zeilen zurückgegeben als die Anzahl von Zeilen, die mit allen Prädikaten übereinstimmen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ordnet die Übereinstimmungen nach Rang und gibt nur die angegebene Anzahl Zeilen zurück. Diese Einschränkung kann zu einer deutlichen Leistungssteigerung führen. So wird z. B. eine Abfrage, die normalerweise 100.000 Zeilen aus einer Tabelle mit 1 Million Zeilen zurückgeben würde, bedeutend schneller verarbeitet, wenn nur die obersten 100 Zeilen angefordert werden.  
  
##  <a name="examples"></a> Beispiele zur Verwendung von RANK zum Einschränken der Suchergebnisse  
  
### <a name="example-a-searching-for-only-the-top-three-matches"></a>Beispiel A: Suchen nach ausschließlich den obersten drei Übereinstimmungen  
 Im folgenden Beispiel werden mit CONTAINSTABLE nur die obersten drei Übereinstimmungen zurückgegeben.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT K.RANK, AddressLine1, City  
FROM Person.Address AS A  
  INNER JOIN  
  CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("des*",  
    Rue WEIGHT(0.5),  
    Bouchers WEIGHT(0.9))',  
    3) AS K  
  ON A.AddressID = K.[KEY]  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
RANK        Address                          City  
----------- -------------------------------- ------------------------------  
172         9005, rue des Bouchers           Paris  
172         5, rue des Bouchers              Orleans  
172         5, rue des Bouchers              Metz  
  
(3 row(s) affected)  
```  
  
  
### <a name="example-b-searching-for-the-top-ten-matches"></a>Beispiel B: Suchen nach ausschließlich den obersten zehn Übereinstimmungen  
 Im folgenden Beispiel wird CONTAINSTABLE verwendet, um die Beschreibung der ersten 5 Produkte zurückzugeben, bei denen die `Description` -Spalte das Wort "aluminium" in der Nähe des Worts "light" oder "lightweight" enthält.  
  
```  
USE AdventureWorks2012  
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
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
GO  
```  
  
  
##  <a name="how"></a> Ordnen von Suchabfrageergebnissen nach Rang  
 Die Volltextsuche in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann eine optionale Bewertung (einen Rangwert) generieren, die die Relevanz der von einer Volltextabfrage zurückgegebenen Daten angibt. Dieser Rangwert wird für jede Zeile berechnet und als Sortierkriterium verwendet, um das Resultset einer bestimmten Abfrage nach Relevanz zu sortieren. Die Rangwerte geben lediglich eine relative Relevanzreihenfolge der Zeilen im Resultset an. Die tatsächlichen Werte sind nicht von Bedeutung und unterscheiden sich i. d. R. bei jeder Ausführung der Abfrage. Der Rangwert hat keinerlei abfrageüberschreitende Bedeutung.  
  
### <a name="statistics-for-ranking"></a>Statistiken für die Rangfolge  
 Beim Erstellen eines Indexes werden Statistiken für die Reihenfolgebestimmung gesammelt. Der Vorgang der Erstellung eines Volltextkatalogs führt nicht direkt zu einer einzelnen Indexstruktur. Stattdessen erstellt das Volltextsuchmodul für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Indizieren der Daten Zwischenindizes. Anschließend werden diese Indizes vom Volltextsuchmodul bei Bedarf in einen größeren Index zusammengeführt. Dieser Vorgang kann mehrfach wiederholt werden. Das Volltextsuchmodul führt einen "Mastermergeprozess" aus, bei dem alle Zwischenindizes zu einem größeren Masterindex kombiniert werden.  
  
 Auf jeder Zwischenstufe werden Statistiken erhoben. Die Statistiken werden beim Zusammenführen der Indizes zusammengeführt. Einige statistische Werte können nur während des Mastermergeprozesses generiert werden.  
  
 Beim Generieren der Rangfolge für ein Abfrageresultset verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Statistiken vom größten Zwischenindex. Dies hängt davon ab, ob Zwischenindizes zusammengeführt wurden oder nicht. Demzufolge kann die Rangfolgestatistik unterschiedlich genau ausfallen, wenn die Zwischenindizes nicht zusammengeführt wurden. Dies erklärt, warum dieselbe Abfrage zu verschiedenen Zeitpunkten unterschiedliche Rangergebnisse zurückgeben kann, wenn volltextindizierte Daten hinzugefügt, geändert und gelöscht werden und wenn die kleineren Indizes zusammengeführt werden.  
  
 Häufig werden die Statistiken gerundet, um die Größe des Indexes und die Komplexität der Berechnung zu minimieren.  
  
 Die nachstehende Liste enthält einige häufig verwendete Begriffe und statistische Werte, die beim Berechnen des Rangs wichtig sind:  
  
 Eigenschaft  
 Eine volltextindizierte Spalte der Zeile.  
  
 Dokument  
 Die Entität, die in Abfragen zurückgegeben wird. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entspricht dies einer Zeile. Ein Dokument kann mehrere Eigenschaften aufweisen, ebenso wie eine Zeile mehrere volltextindizierte Spalten aufweisen kann.  
  
 Index  
 Ein einzelner invertierter Index mindestens eines Dokuments. Er kann sich vollständig im Arbeitsspeicher oder auf dem Datenträger befinden. Viele Abfragestatistiken sind relativ zu dem jeweiligen Index, mit dem der Vergleich ausgeführt wurde.  
  
 Volltextkatalog  
 Eine Auflistung von Zwischenindizes, die für Abfragen als eine Entität behandelt wird. Kataloge sind die Organisationseinheit, die für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Administrator sichtbar ist.  
  
 Wort, Token oder Element  
 Die Vergleichseinheit im Volltextmodul. Textströme aus Dokumenten werden durch eine sprachspezifische Wörtertrennung in Wörter oder Token zerlegt.  
  
 Vorkommen  
 Der von der Wörtererkennung bestimmte Offset eines Worts in einer Dokumenteigenschaft. Das erste Wort stellt Vorkommen 1 dar, das nächste 2 usw. Um falsche Treffer in Ausdrucks- und NEAR-Abfragen zu vermeiden, bewirken Satzende- und Absatzendezeichen größere Abstände zwischen den Vorkommen.  
  
 TermFrequency  
 Die Anzahl der Vorkommen des Schlüsselwerts in einer Zeile.  
  
 IndexedRowCount  
 Gesamtanzahl der indizierten Zeilen. Diese wird aus den in den Zwischenindizes geführten Zählern berechnet. Die Genauigkeit der Anzahl kann variieren.  
  
 KeyRowCount  
 Gesamtanzahl der Zeilen im Volltextkatalog, die einen bestimmten Schlüssel enthalten.  
  
 MaxOccurrence  
 Das größte in einem Volltextkatalog gespeicherte Vorkommen für eine bestimmte Eigenschaft in einer Zeile.  
  
 MaxQueryRank  
 Der maximale Rang, 1000, der vom Volltextsuchmodul zurückgegeben wird.  
  
  
### <a name="rank-computation-issues"></a>Gesichtspunkte bei der Rangberechnung  
 Der Vorgang der Rangberechnung hängt von mehreren Faktoren ab.  Die Wörtererkennung für unterschiedliche Sprachen zerlegt Text unterschiedlich in Wörter. So könnte z. B. die Zeichenfolge "dog-house" von einer Wörtererkennung in "dog" "house" und von einer anderen in "dog-house" zerlegt werden. Dies bedeutet, dass Vergleiche und Rangfolgenberechnung je nach der angegebenen Sprache unterschiedliche Ergebnisse liefern, da nicht nur die Wörter unterschiedlich sind, sondern auch die Dokumentlänge. Die unterschiedliche Dokumentlänge kann sich auf die Rangfolgenberechnung für alle Abfragen auswirken.  
  
 Statistiken wie **IndexRowCount** können stark variieren. Hat z. B. ein Katalog 2 Milliarden Zeilen im Masterindex, wird ein einzelnes neues Dokument in einen im Arbeitsspeicher befindlichen Zwischenindex indiziert, und die Ränge für das Dokument, die auf der Anzahl der Dokumente im Index im Arbeitsspeicher basieren, können im Vergleich zu den Rängen für Dokumente aus dem Masterindex verfälscht sein. Daher wird empfohlen, dass die Indizes nach jeder Auffüllung, durch die viele Zeilen indiziert oder neu indiziert werden, in einen Masterindex zusammengeführt werden, mithilfe der ALTER FULLTEXT CATALOG ... REORGANIZE [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung. Entsprechend bestimmten Parametern, wie Anzahl und Größe der Zwischenindizes, werden die Indizes auch automatisch vom Volltextsuchmodul zusammengeführt.  
  
 **MaxOccurrence** -Werte werden in den Bereich 1 bis 32 normalisiert. Das heißt, dass z. B. ein 50 Wörter langes Dokument genau so behandelt wird wie ein 100 Wörter langes. Die zur Normalisierung verwendete Tabelle ist unten aufgeführt. Da die Dokumentlängen im Bereich zwischen den benachbarten Tabellenwerten 32 und 128 liegen, werden sie behandelt, als hätten sie dieselbe Länge, nämlich 128 (32 < **docLength** <= 128).  
  
```  
{ 16, 32, 128, 256, 512, 725, 1024, 1450, 2048, 2896, 4096, 5792, 8192, 11585,   
16384, 23170, 28000, 32768, 39554, 46340, 55938, 65536, 92681, 131072, 185363,   
262144, 370727, 524288, 741455, 1048576, 2097152, 4194304 };  
  
```  
  
  
### <a name="ranking-of-containstable"></a>Rangfolge von CONTAINSTABLE  
 Beim Generieren der Rangfolge für[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) wird der folgende Algorithmus verwendet:  
  
```  
StatisticalWeight = Log2( ( 2 + IndexedRowCount ) / KeyRowCount )  
Rank = min( MaxQueryRank, HitCount * 16 * StatisticalWeight / MaxOccurrence )  
```  
  
 Der Rang von Übereinstimmungen in Ausdrücken wird genauso bestimmt wie einzelne Schlüssel, außer dass **KeyRowCount** (die Anzahl von Zeilen, die den Ausdruck enthalten) geschätzt wird und somit ungenau und höher als die tatsächliche Anzahl ausfallen kann.  
  
 **Rangfolge von NEAR**  
  
 CONTAINSTABLE unterstützt das Abfragen von zwei oder mehr Suchbegriffen mithilfe der NEAR-Option hinsichtlich ihrer Nähe zueinander. Der Rangwert der einzelnen zurückgegebenen Zeilen basiert auf mehreren Parametern. Ein Hauptrangfaktor ist die Gesamtzahl der Übereinstimmungen (oder *Treffer*) in Bezug auf die Länge des Dokuments. Wenn beispielsweise ein Dokument mit 100 Wörtern und ein Dokument mit 900 Wörtern identische Übereinstimmungen enthalten, wird dem Dokument mit 100 Wörtern ein höherer Rangwert zugewiesen.  
  
 Die Gesamtlänge der einzelnen Treffer in einer Zeile trägt ebenfalls zum Rangwert der betreffenden Zeile bei, wobei die Entfernung zwischen dem ersten und dem letzten Suchbegriff des jeweiligen Treffers zugrunde gelegt wird. Je kleiner die Entfernung, desto relevanter ist der Treffer für den Rangwert der Zeile. Wenn eine Volltextabfrage keine ganze Zahl angibt (z. B. die maximale Entfernung), weist ein Dokument, das nur Treffer enthält, deren Entfernungen weiter als 100 logische Begriffe auseinander liegen, einen Rang von 0 (null) auf.  
  
 **Rangfolge von ISABOUT**  
  
 CONTAINSTABLE unterstützt das Abfragen von gewichteten Begriffen mit der ISABOUT-Option. ISABOUT ist eine Vektorraumabfrage in traditioneller Information Retrieval-Terminologie. Der verwendete Standardalgorithmus zur Rangfolgenberechnung ist Jaccard, eine bekannte Formel. Die Rangfolge wird für jeden Begriff in der Abfrage berechnet und anschließend wie nachstehend beschrieben kombiniert.  
  
```  
ContainsRank = same formula used for CONTAINSTABLE ranking of a single term (above).  
Weight = the weight specified in the query for each term. Default weight is 1.  
WeightedSum = Σ[key=1 to n] ContainsRankKey * WeightKey  
Rank =  ( MaxQueryRank * WeightedSum ) / ( ( Σ[key=1 to n] ContainsRankKey^2 )   
      + ( Σ[key=1 to n] WeightKey^2 ) - ( WeightedSum ) )  
  
```  
  
  
### <a name="ranking-of-freetexttable"></a>Rangfolge von FREETEXTTABLE  
 Die Rangfolgenberechnung für[FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) basiert auf der OKAPI BM25-Rangfolgenformel. Bei FREETEXTTABLE-Abfragen werden der Abfrage durch Wortformengenerierung Flexionsformen der ursprünglichen Abfragewörter hinzugefügt; diese Wörter werden als separate Wörter ohne besondere Beziehung zu den Wörtern behandelt, aus denen sie generiert wurden. Aus der Thesaurus-Funktion generierte Synonyme werden als separate, gleich gewichtete Begriffe behandelt. Jedes Wort in der Abfrage wird bei der Rangberechnung einbezogen.  
  
```  
Rank = Σ[Terms in Query] w ( ( ( k1 + 1 ) tf ) / ( K + tf ) ) * ( ( k3 + 1 ) qtf / ( k3 + qtf ) ) )  
Where:   
w is the Robertson-Sparck Jones weight.   
In simplified form, w is defined as:   
w = log10 ( ( ( r + 0.5 ) * ( N – R + r + 0.5 ) ) / ( ( R – r + 0.5 ) * ( n – r + 0.5 ) )  
N is the number of indexed rows for the property being queried.   
n is the number of rows containing the word.   
K is ( k1 * ( ( 1 – b ) + ( b * dl / avdl ) ) ).   
dl is the property length, in word occurrences.   
avdl is the average length of the property being queried, in word occurrences.   
k1, b, and k3 are the constants 1.2, 0.75, and 8.0, respectively.   
tf is the frequency of the word in the queried property in a specific row.   
qtf is the frequency of the term in the query.   
```  
  
  
## <a name="see-also"></a>Siehe auch  
 [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md)  
  
  
