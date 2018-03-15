---
title: CONTAINS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONTAINS_TSQL
- CONTAINS
dev_langs:
- TSQL
helpviewer_keywords:
- precise or fuzzy (less precise) matches [full-text search]
- CONTAINS predicate (Transact-SQL)
- conditions [SQL Server], CONTAINS
- fuzzy (less precise) word or phrase search [full-text search]
- word weighting values [full-text search]
- word searches [full-text search]
- weighted values [full-text search]
- LANGUAGE option
- word inflectionally generated from another [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- word near another word search [full-text search]
- full-text search [SQL Server], searching on a property
- proximity searches [full-text search]
- less precise (fuzzy) searches [full-text search]
- property searching [SQL Server], searching on a property
- inflectional forms [full-text search]
- prefix searches [full-text search]
ms.assetid: 996c72fc-b1ab-4c96-bd12-946be9c18f84
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 81b231ce95ae1b87bbda2f2fd786d12cb709e9fe
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="contains-transact-sql"></a>CONTAINS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Sucht nach genauen oder ungenauen (Fuzzy-)Übereinstimmungen mit einzelnen Wörtern und Satzteilen, für innerhalb einer bestimmten Entfernung angrenzende Wörter sowie für gewichtete Übereinstimmungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. CONTAINS ist ein Prädikat, das in der [WHERE](../../t-sql/queries/where-transact-sql.md)-Klausel einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-SELECT-Anweisung verwendet wird, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Volltextsuchvorgänge für volltextindizierte Spalten mit zeichenbasierten Datentypen durchzuführen.  
  
 Folgendes kann mit CONTAINS gesucht werden:  
  
-   Ein Wort oder ein Ausdruck.  
  
-   Das Präfix eines Worts oder eines Ausdrucks.  
  
-   Ein Wort, das einem anderen Wort ähnlich ist.  
  
-   Ein Wort, das mithilfe von Beugung aus einem anderen generiert wurde (z. B. stellt das Wort drive den Beugungsstamm von drives, drove, driving und driven dar.)  
  
-   Ein Wort, das ein Synonym für ein anderes Wort ist (das Wort Metall kann z. B. über die Synonyme Aluminium und Stahl verfügen). Dazu wird ein Thesaurus verwendet.  
  
 Informationen zu den Formen der Volltextsuche, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt werden, finden Sie unter [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md).  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CONTAINS (   
     {   
        column_name | ( column_list )   
      | *   
      | PROPERTY ( { column_name }, 'property_name' )    
     }   
     , '<contains_search_condition>'  
     [ , LANGUAGE language_term ]  
   )   
  
<contains_search_condition> ::=   
  {   
      <simple_term>   
    | <prefix_term>   
    | <generation_term>   
    | <generic_proximity_term>   
    | <custom_proximity_term>   
    | <weighted_term>   
    }   
  |   
    { ( <contains_search_condition> )   
        [ { <AND> | <AND NOT> | <OR> } ]   
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
   ( {   
        {   
          <simple_term>   
        | <prefix_term>   
        | <generation_term>   
        | <proximity_term>   
        }   
      [ WEIGHT ( weight_value ) ]   
      } [ ,...n ]   
   )   
  
<AND> ::=   
  { AND | & }  
  
<AND NOT> ::=   
  { AND NOT | &! }  
  
<OR> ::=   
  { OR | | }  
  
```  
  
## <a name="arguments"></a>Argumente  
 *column_name*  
 Der Name einer volltextindizierten Spalte der in der FROM-Klausel angegebenen Tabelle. Die Spalten können vom Typ **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** oder **varbinary(max)** sein.  
  
 *column_list*  
 Gibt zwei oder mehr durch Trennzeichen getrennte Spalten an. *column_list* muss in Klammern stehen. Sofern nicht *language_term* angegeben ist, muss die Sprache aller Spalten von *column_list* identisch sein.  
  
 \*  
 Gibt an, dass die Abfrage alle volltextindizierten Spalten in der Tabelle durchsucht, die in der FROM-Klausel für die festgelegte Suchbedingung angegeben werden. Die Spalten in der CONTAINS-Klausel müssen aus einer einzelnen Tabelle mit einem Volltextindex stammen. Sofern *language_term* nicht angegeben ist, muss die Sprache aller Spalten in der Tabelle identisch sein.  
  
 PROPERTY ( *column_name* , '*property_name*')  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Gibt eine Dokumenteigenschaft an, in der nach der angegebenen Suchbedingung gesucht werden soll.  
  
> [!IMPORTANT]  
>  Damit von der Abfrage Zeilen zurückgegeben werden können, muss *property_name* in der Sucheigenschaftenliste des Volltextindexes angegeben werden, und der Volltextindex muss eigenschaftenspezifische Einträge für *property_name* enthalten. Weitere Informationen finden Sie unter [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
 LANGUAGE *language_term*  
 Die Sprache, die für Wörtertrennung, Wortstammerkennung, Thesauruserweiterungen und -ersetzungen sowie die Entfernung von Füllwörtern (oder [Stoppwörtern](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) im Rahmen der Abfrage verwendet werden soll. Dieser Parameter ist optional.  
  
 Wenn Dokumente anderer Sprachen zusammen als BLOBs (Binary Large Objects) in einer einzelnen Spalte gespeichert werden, bestimmt der Gebietsschemabezeichner (LCID) eines bestimmten Dokuments die zur Indizierung seines Inhalts zu verwendende Sprache. Beim Abfragen einer solchen Spalte kann die Angabe von LANGUAGE *language_term* die Wahrscheinlichkeit einer hohen Übereinstimmung steigern.  
  
 *language_term* kann als Zeichenfolge, Integer oder Hexadezimalwert entsprechend dem LCID einer Sprache angegeben werden. Wird *language_term* angegeben, wird die entsprechende Sprache auf alle Elemente der Suchbedingung angewendet. Wird kein Wert angegeben, wird die Volltextsprache der Spalte verwendet.  
  
 In Form einer Zeichenfolge entspricht *language_term* dem Wert der **alias**-Spalte in der [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)-Kompatibilitätssicht. Die Zeichenfolge muss in einfache Anführungszeichen gesetzt werden, z.B. '*language_term*'. In Form einer ganzen Zahl ist *language_term* der eigentliche Gebietsschemabezeichner, der die Sprache identifiziert. In Form eines Hexadezimalwerts ist *language_term* gleich 0x, gefolgt vom Hexadezimalwert des Gebietsschemabezeichners. Der Hexadezimalwert darf acht Ziffern nicht überschreiten, einschließlich führender Nullen.  
  
 Wird der Wert im Format DBCS (Double-Byte Character Set, Doppelbyte-Zeichensatz) angegeben, wird er von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Unicode konvertiert.  
  
 Ist die angegebene Sprache ungültig oder sind keine Ressourcen installiert, die dieser Sprache entsprechen, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler zurück. Geben Sie 0x0 als *language_term* an, um neutrale Sprachressourcen zu verwenden.  
  
 \<*contains_search_condition*>  
 Gibt den Suchtext in *column_name* und die Bedingungen für eine Übereinstimmung an.  
  
*\<contains_search_condition>* ist vom Datentyp **nvarchar**. Wird ein anderer Zeichendatentyp als Eingabe verwendet, findet eine implizite Konvertierung statt. Die großen Zeichenfolgendatentypen nvarchar(max) und varchar(max) können nicht verwendet werden. Im folgenden Beispiel verursacht die `@SearchWord`-Variable, die als `varchar(30)` definiert ist, eine implizite Konvertierung im `CONTAINS`-Prädikat.
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord varchar(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 Da die „Parameterermittlung“ zusammen mit der Konvertierung nicht funktionsfähig ist, sollten Sie aus Leistungsgründen **nvarchar** verwenden. Deklarieren Sie im Beispiel `@SearchWord` als `nvarchar(30)`.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 In Fällen, in denen ein nicht optimaler Plan generiert wird, können Sie auch den OPTIMIZE FOR-Abfragehinweis verwenden.  
  
 *word*  
 Eine Zeichenfolge ohne Leerzeichen oder Satzzeichen.  
  
 *phrase*  
 Ein Wort oder mehrere Wörter, die durch Leerzeichen getrennt sind.  
  
> [!NOTE]  
>  Einige Sprachen, wie z. B. die in einigen Teilen von Asien verwendeten Sprachen, können Ausdrücke besitzen, die aus mehreren Wörtern ohne Leerzeichen bestehen.  
  
\<simple_term>  
Gibt eine Übereinstimmung für ein genaues Wort oder einen genauen Ausdruck an. Beispiele für gültige einfache Begriffe sind "blue berry", blueberry und "Microsoft SQL Server". Ausdrücke müssen in doppelte Anführungszeichen ("") gesetzt werden. Die Wörter eines Ausdrucks werden nur dann in der Datenbank gefunden, wenn sie unter *\<contains_search_condition>* in der gleichen Reihenfolge angegeben werden. Bei der Suche nach Zeichen in einem Wort oder einem Ausdruck wird nicht zwischen Groß- und Kleinschreibung unterschieden. Füllwörter (oder [Stoppwörter](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)), z.B. „ein“, „und“ oder „die“, aus volltextindizierten Spalten werden nicht im Volltextindex gespeichert. Wenn das einzige gesuchte Wort ein Füllwort ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Fehlermeldung zurück, die angibt, dass lediglich Füllwörter als Suchbegriffe übergeben wurden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält eine Standardliste der Füllwörter im Verzeichnis \Mssql\Binn\FTERef für jede Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Satzzeichen werden nicht beachtet. Mit `CONTAINS(testing, "computer failure")` wird daher auch eine Zeile mit dem Wert "Where is my computer? Failure to find it would be expensive." gefunden. Weitere Informationen zum Worttrennungsverhalten finden Sie unter [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
 \<prefix_term>  
 Gibt eine Suche nach Wörtern oder Ausdrücken an, die mit dem angegebenen Text beginnen. Setzen Sie einen Präfixausdruck (prefix_term) in doppelte Anführungszeichen (""), und setzen Sie ein Sternchen (\*) vor das schließende Anführungszeichen, sodass jeglicher Text gefunden wird, der mit dem einfachen Ausdruck beginnt, der vor dem Sternchen steht. Die Klausel sollte wie folgt angegeben werden: `CONTAINS (column, '"text*"')` Das Sternchen entspricht keinem, einem oder mehreren Zeichen (des Hauptworts bzw. der Hauptwörter im Ausdruck). Wenn der Text und das Sternchen nicht in doppelten Anführungszeichen stehen, sodass das Prädikat als `CONTAINS (column, 'text*')` gelesen wird, wird das Sternchen bei der Volltextsuche als Zeichen behandelt, und es wird nach exakten Übereinstimmungen mit `text*` gesucht. Von der Volltext-Engine werden keine Wörter mit Sternchen (\*) gefunden, da dieses Zeichen in der Regel von der Wörtertrennung ignoriert wird.  
  
 Ist *\<prefix_term>* ein Ausdruck, wird jedes Wort, das in dem Ausdruck vorhanden ist, als separates Präfix behandelt. Daher werden bei einer Abfrage des Präfixbegriffs "local wine*" als Übereinstimmung alle Zeilen mit dem Text "local winery", "locally wined and dined" usw. ausgegeben.  
  
 \<generation_term>  
 Gibt eine Suche nach Wörtern an, wenn die enthaltenen einfachen Begriffe Varianten des ursprünglichen Worts enthalten, nach dem gesucht werden soll.  
  
 INFLECTIONAL  
 Gibt an, dass die sprachenabhängige Wortstammerkennung für den angegebenen einfachen Ausdruck verwendet werden soll. Das Verhalten der Wortstammerkennung wird auf der Grundlage von Wortstammerkennungsregeln für jede Sprache einzeln definiert. Der neutralen Sprache ist keine Wortstammerkennung zugeordnet. Auf die gewünschte Wortstammerkennung wird anhand der Spaltensprache der abgefragten Spalten verwiesen. Falls *language_term* angegeben ist, wird die dieser Sprache entsprechende Wortstammerkennung verwendet.  
  
 Ein angegebener *\<simple_term>*-Wert innerhalb von *\<generation_term>* kann nicht sowohl mit Substantiven als auch mit Verben übereinstimmen.  
  
 THESAURUS  
 Gibt an, dass der Thesaurus verwendet wird, der der Volltext-Spaltensprache oder der in der Abfrage angegebenen Sprache entspricht. Die längsten Muster aus *\<simple_term>* werden mit dem Thesaurus verglichen, und weitere Ausdrücke werden generiert, um das ursprüngliche Muster zu erweitern oder zu ersetzen. Wird für den ganzen Ausdruck oder für Teile von *\<simple_term>* keine Übereinstimmung gefunden, wird der nicht übereinstimmende Teil als *simple_term* behandelt. Weitere Informationen zum Thesaurus der Volltextsuche finden Sie unter [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
 \<generic_proximity_term>  
 Legt eine Übereinstimmung für Wörter oder Ausdrücke fest, die im durchsuchten Dokument vorhanden sein müssen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Es wird empfohlen, \<custom_proximity_term> zu verwenden.  
  
 NEAR | ~  
 Gibt an, dass das Wort oder der Ausdruck auf beiden Seiten des NEAR-Operators bzw. ~-Operators in einem Dokument vorhanden sein muss, damit eine Übereinstimmung zurückgegeben wird. Sie müssen zwei Suchbegriffe angeben. Ein Suchbegriff kann ein einzelnes Wort oder ein Ausdruck sein, der in doppelte Anführungszeichen ("*Ausdruck*") eingeschlossen wird.  
  
 Mehrere NEAR-Begriffe können wie in `a NEAR b NEAR c` oder `a ~ b ~ c` verkettet werden. Damit eine Übereinstimmung zurückgegeben wird, müssen alle verketteten Ausdrücke, die nahe beieinander stehen sollen, im Dokument vorhanden sein.  
  
 Beispielsweise geben `CONTAINS(*column_name*, 'fox NEAR chicken')` und `CONTAINSTABLE(*table_name*, *column_name*, 'fox ~ chicken')` alle Dokumente in der angegebenen Spalte zurück, die sowohl „Fuchs“ als auch „Huhn“ enthalten. Außerdem gibt CONTAINSTABLE einen nach dem Abstand von "Fuchs" und "Huhn" bestimmten Rang für jedes Dokument zurück. Wenn ein Dokument etwa den Satz "Der Fuchs fraß das Huhn." enthält, wäre sein Rang hoch, da die Begriffe näher beieinander sind als in anderen Dokumenten.  
  
 Weitere Informationen zu generischen NEAR-Begriffen finden Sie unter [Suchen von Wörtern in der Nähe eines anderen Worts mit NEAR](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md).  
  
 \<custom_proximity_term>  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
 Gibt eine Übereinstimmung von Wörtern oder Ausdrücken sowie optional den maximalen Abstand zwischen den Suchbegriffen an. Sie können auch angeben, dass Suchbegriffe in der exakten Reihenfolge gesucht werden müssen, in der Sie sie (\<match_order>) angegeben haben.  
  
 Ein Suchbegriff kann ein einzelnes Wort oder ein Ausdruck sein, der in doppelte Anführungszeichen ("*Ausdruck*") eingeschlossen wird. Damit eine Übereinstimmung zurückgegeben wird, müssen alle angegeben Ausdrücke im Dokument vorhanden sein. Sie müssen mindestens zwei Suchbegriffe angeben. Die maximale Anzahl von Suchbegriffen ist 64.  
  
 Standardmäßig werden vom benutzerdefinierten NEAR-Begriff alle Zeilen zurückgegeben, die die angegebenen Begriffe enthalten, unabhängig vom Abstand dazwischen und unabhängig von der Reihenfolge. Beispielsweise müsste eine Dokument nur `term1` und "`term3 term4`" an beliebiger Position und in beliebiger Reihenfolge enthalten, um der Abfrage zu entsprechen:  
  
```  
CONTAINS(column_name, 'NEAR(term1,"term3 term4")')  
```  
  
 Die optionalen Parameter lauten wie folgt:  
  
 \<maximum_distance>  
 Gibt den maximal zulässigen Abstand zwischen den Suchbegriffen am Anfang und Ende einer Zeichenfolge an, damit diese als Übereinstimmung gilt.  
  
 *integer*  
 Gibt eine positive ganze Zahl zwischen 0 und 4294967295 an. Mit diesem Wert wird festgelegt, wie viele Begriffe, die keine Suchbegriffe sind, mit Ausnahme weiterer angegebener Suchbegriffe zwischen dem ersten und dem letzten Suchbegriff stehen dürfen.  
  
 Beispielsweise wird mit der folgenden Abfrage nach `AA` und `BB` gesucht. Die Reihenfolge ist dabei nicht vorgegeben, und der maximale Abstand zwischen den beiden Suchbegriffen darf fünf Wörter betragen.  
  
```  
CONTAINS(column_name, 'NEAR((AA,BB),5)')  
```  
  
 Die Zeichenfolge `AA one two three four five BB` stellt eine Übereinstimmung dar. Im folgenden Beispiel werden von der Abfrage drei Suchbegriffe (`AA`, `BB` und `CC`) mit einem maximalen Abstand von fünf Wörtern angegeben:  
  
```  
CONTAINS(column_name, 'NEAR((AA,BB,CC),5)')  
```  
  
 Diese Abfrage würde der folgenden Zeichenfolge mit dem Gesamtabstand fünf Wörter entsprechen:  
  
 `BB   one two   CC   three four five A  A`  
  
 Beachten Sie, dass der innere Suchbegriff `CC` nicht mitgezählt wird.  
  
 **MAX**  
 Gibt alle Zeilen zurück, die die angegebenen Begriffe enthalten, unabhängig von der Entfernung dazwischen. Dies ist die Standardeinstellung.  
  
 \<match_order>  
 Gibt an, ob die Begriffe in der angegebenen Reihenfolge auftreten müssen, um von einer Suchabfrage zurückgegeben zu werden. Wenn Sie \<match_order> verwenden möchten, müssen Sie auch \<maximum_distance> angeben.  
  
 \<match_order> akzeptiert einen der folgenden Werte:  
  
 **TRUE**  
 Erzwingt die angegebene Reihenfolge in Begriffen. Beispielsweise würde `NEAR(A,B)` nur `A … B` entsprechen.  
  
 **FALSE**  
 Ignoriert die angegebene Reihenfolge. Beispielsweise würde `NEAR(A,B)` sowohl `A … B` als auch `B … A` entsprechen.  
  
 Dies ist die Standardeinstellung.  
  
 Beispielsweise wird in den folgenden NEAR-Suchvorgängen nach den Wörtern "`Monday`", "`Tuesday`" und "`Wednesday`" in der angegebene Reihenfolge gesucht, unabhängig vom Abstand zwischen den Begriffen:  
  
```  
CONTAINS(column_name, 'NEAR ((Monday, Tuesday, Wednesday), MAX, TRUE)')  
```  
  
 Weitere Informationen zu benutzerdefinierten NEAR-Begriffen finden Sie unter [Suchen von Wörtern in der Nähe eines anderen Worts mit NEAR](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md).  
  
 \<weighted_term>  
 Gibt an, dass die übereinstimmenden Zeilen (die von der Abfrage zurückgegeben werden) mit einer Liste von Wörtern und Ausdrücken übereinstimmen müssen, die optional jeweils mit einem Gewichtungswert versehen sind.  
  
 ISABOUT  
 Gibt das Schlüsselwort *\<weighted_term>* an.  
  
 WEIGHT(*weight_value*)  
 Gibt einen Gewichtungswert von 0,0 bis 1,0 an. Jede Komponente in *\<weighted_term>* kann auch einen *weight_value* enthalten. *weight_value* kann die Art und Weise beeinflussen, wie sich verschiedene Teilabfragen auf den Rangwert auswirken, der jeder mit der Abfrage übereinstimmenden Zeile zugewiesen ist. WEIGHT hat keine Auswirkung auf die Ergebnisse von CONTAINS-Abfragen, beeinflusst jedoch den Rang in [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)-Abfragen.  
  
> [!NOTE]  
>  Das Dezimaltrennzeichen ist immer ein Punkt, unabhängig vom Betriebssystemgebietsschema.  
  
 { AND | & } | { AND NOT | &! } | { OR | | }   
 Gibt einen logischen Vorgang zwischen zwei CONTAINS-Suchbedingungen an.  
  
 { AND | & }  
 Gibt an, dass die beiden CONTAINS-Suchbedingungen für eine Übereinstimmung erfüllt sein müssen. Das kaufmännische Und-Zeichen (&) kann an Stelle des AND-Schlüsselworts zur Darstellung des AND-Operators verwendet werden.  
  
 { AND NOT | &! }  
 Gibt an, dass die zweite CONTAINS-Suchbedingung für eine Übereinstimmung nicht erfüllt sein darf. Das kaufmännische Und-Zeichen gefolgt von einem Ausrufezeichen (&!) kann an Stelle des AND NOT-Schlüsselworts zur Darstellung des AND NOT-Operators verwendet werden.  
  
 { OR | | }  
 Gibt an, dass eine der beiden CONTAINS-Suchbedingungen für eine Übereinstimmung erfüllt sein muss. Der senkrechte Strich (|) kann an Stelle des OR-Schlüsselsorts zur Darstellung des OR-Operators verwendet werden.  
  
 Wenn in *\<contains_search_condition>* in Klammern gesetzte Gruppen enthalten sind, werden diese zuerst ausgewertet. Nach der Auswertung der in Klammern gesetzten Gruppen gelten folgende Regeln bei der Verwendung der logischen Operatoren mit den CONTAINS-Suchbedingungen:  
  
-   NOT wird vor AND angewendet.  
  
-   NOT kann nur nach AND auftreten, wie in AND NOT. Der Operator OR NOT ist nicht zugelassen. NOT kann nicht vor dem ersten Ausdruck angegeben werden. Beispielsweise ist Folgendes nicht zulässig: `CONTAINS (mycolumn, 'NOT "phrase_to_search_for" ' )`.  
  
-   AND wird vor OR angewendet.  
  
-   Da boolesche Operatoren des gleichen Typs (AND, OR) assoziativ sind, können sie in beliebiger Reihenfolge angewendet werden.  
  
 *n*  
 Ein Platzhalter, der anzeigt, dass mehrere CONTAINS-Suchbedingungen und darin enthaltene Begriffe angegeben werden können.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Volltextprädikate und -funktionen gelten für eine einzelne Tabelle, die im FROM-Prädikat enthalten ist. Um eine Suche in mehreren Tabellen auszuführen, können Sie eine verknüpfte Tabelle in der FROM-Klausel verwenden, um in einem Resultset zu suchen, das aus mindestens zwei Tabellen erstellt wird.  
  
 Volltextprädikate sind in der [OUTPUT-Klausel](../../t-sql/queries/output-clause-transact-sql.md) nicht zulässig, wenn der Kompatibilitätsgrad der Datenbank auf 100 festgelegt ist.  
  
## <a name="querying-remote-servers"></a>Abfragen von Remoteservern  
 Sie können einen vierteiligen Namen im CONTAINS- oder [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)-Prädikat zum Abfragen von volltextindizierten Spalten der Zieltabellen auf einem Verbindungsserver verwenden. Erstellen Sie zum Vorbereiten eines Remoteservers für den Empfang von Volltextabfragen einen Volltextindex für die Zieltabellen und -spalten auf dem Remoteserver, und fügen Sie anschließend den Remoteserver als Verbindungsserver hinzu.  
  
## <a name="comparison-of-like-to-full-text-search"></a>Vergleich zwischen LIKE und der Volltextsuche  
 Im Gegensatz zur Volltextsuche verarbeitet das [LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)]-Prädikat ausschließlich Zeichenmuster. Darüber hinaus können Sie mit dem LIKE-Prädikat keine formatierten Binärdaten abfragen. Eine LIKE-Abfrage in umfangreichen unstrukturierten Textdaten ist sehr viel langsamer als eine entsprechende Volltextabfrage in denselben Daten. Eine LIKE-Abfrage für Millionen von Zeilen von Textdaten kann Minuten in Anspruch nehmen; eine Volltextabfrage kann dagegen in Sekunden oder weniger für dieselben Daten ein Ergebnis liefern, je nach Anzahl und Größe der zurückgegebenen Zeilen. Ein weiterer Aspekt ist, dass mit LIKE nur eine einfache Mustersuche in einer ganzen Tabelle durchgeführt wird. Bei einer Volltextabfrage wird hingegen die Sprache beachtet und zur Indizierungs- und Abfragezeit werden bestimmte Transformationen vorgenommen, beispielsweise das Filtern von Stoppwörtern oder Anwenden von Thesaurus- und Flexionserweiterungen. Diese Transformationen helfen Volltextabfragen, die Genauigkeit von Rückrufen sowie die abschließende Rangfolge der Ergebnisse zu verbessern.  
  
## <a name="querying-multiple-columns-full-text-search"></a>Abfragen mehrerer Spalten (Volltextsuche)  
 Sie können mehrere Spalten abfragen, indem Sie eine Liste von Spalten angeben, die durchsucht werden sollen. Die Spalten müssen sich in derselben Tabelle befinden.  
  
 Beispielsweise wird mit der folgenden CONTAINS-Abfrage nach dem Begriff `Red` in den Spalten `Name` und `Color` der Tabelle `Production.Product` für die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Beispieldatenbank gesucht.  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Name, Color   
FROM Production.Product  
WHERE CONTAINS((Name, Color), 'Red');  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-contains-with-simpleterm"></a>A. Verwenden von CONTAINS mit \<simple_term>  
 Im folgenden Beispiel werden alle Produkte mit einem Preis von `$80.99` gesucht, die das Wort `Mountain`enthalten.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain');  
GO  
```  
  
### <a name="b-using-contains-and-phrase-with-simpleterm"></a>B. Verwenden von CONTAINS und einem Ausdruck mit \<simple_term>  
 Im folgenden Beispiel werden alle Produkte zurückgegeben, die entweder den Ausdruck `Mountain` oder `Road` enthalten.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' Mountain OR Road ')  
GO  
```  
  
### <a name="c-using-contains-with-prefixterm"></a>C. Verwenden von CONTAINS mit \<prefix_term>  
 Im folgenden Beispiel werden alle Produktnamen zurückgegeben, die mindestens ein Wort enthalten, das mit dem Präfix chain in der `Name`-Spalte beginnt.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' "Chain*" ');  
GO  
```  
  
### <a name="d-using-contains-and-or-with-prefixterm"></a>D. Verwenden von CONTAINS und OR mit \<prefix_term>  
 Im folgenden Beispiel werden alle Kategoriebeschreibungen zurückgegeben, die Zeichenfolgen mit dem Präfix `chain` oder `full` enthalten.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, '"chain*" OR "full*"');  
GO  
```  
  
### <a name="e-using-contains-with-proximityterm"></a>E. Verwenden von CONTAINS mit \<proximity_term>  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Im folgenden Beispiel wird in der `Production.ProductReview`-Tabelle nach allen Kommentaren gesucht, die das Wort `bike` maximal 10 Begriffe vom Wort `control` entfernt und in der angegebenen Reihenfolge enthalten (d.h. `bike` vor `control`).  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments , 'NEAR((bike,control), 10, TRUE)');  
GO  
```  
  
### <a name="f-using-contains-with-generationterm"></a>F. Verwenden von CONTAINS mit \<generation_term>  
 Im folgenden Beispiel wird nach allen Produkten gesucht, bei denen Wortformen von `ride` verwendet werden: "riding", "ridden" usw.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, ' FORMSOF (INFLECTIONAL, ride) ');  
GO  
```  
  
### <a name="g-using-contains-with-weightedterm"></a>G. Verwenden von CONTAINS mit \<weighted_term>  
 Im folgenden Beispiel wird nach allen Produktnamen gesucht, die die Wörter `performance`, `comfortable` oder `smooth` enthalten, wobei jedes Wort anders gewichtet wird.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, 'ISABOUT (performance weight (.8),   
comfortable weight (.4), smooth weight (.2) )' );  
GO  
```  
  
### <a name="h-using-contains-with-variables"></a>H. Verwenden von CONTAINS mit Variablen  
 Im folgenden Beispiel wird kein bestimmter Suchbegriff, sondern eine Variable verwendet.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'Performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
GO  
```  
  
### <a name="i-using-contains-with-a-logical-operator-and"></a>I. Verwenden von CONTAINS mit einem logischen Operator (AND)  
 Im folgenden Beispiel wird die ProductDescription-Tabelle der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank verwendet. In der Abfrage wird das CONTAINS-Prädikat für die Suche nach Beschreibungen verwendet, deren Beschreibungs-ID ungleich 5 ist und die das Wort `Aluminum` sowie das Wort `spindle` enthalten. In der Suchbedingung wird der boolesche AND-Operator verwendet.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'Aluminum AND spindle');  
GO  
```  
  
### <a name="j-using-contains-to-verify-a-row-insertion"></a>J. Verwenden von CONTAINS, um eine Zeileneinfügung zu überprüfen  
 Im folgenden Beispiel wird CONTAINS in einer SELECT-Unterabfrage verwendet. Mithilfe der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank ruft die Abfrage den Kommentarwert aller Kommentare in der ProductReview-Tabelle für einen bestimmten Zyklus ab. In der Suchbedingung wird der boolesche AND-Operator verwendet.  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Production.ProductReview   
  (ProductID, ReviewerName, EmailAddress, Rating, Comments)   
VALUES  
  (780, 'John Smith', 'john@fourthcoffee.com', 5,   
'The Mountain-200 Silver from AdventureWorks2008 Cycles meets and exceeds expectations. I enjoyed the smooth ride down the roads of Redmond');  
  
-- Given the full-text catalog for these tables is Adv_ft_ctlg,   
-- with change_tracking on so that the full-text indexes are updated automatically.  
WAITFOR DELAY '00:00:30';     
-- Wait 30 seconds to make sure that the full-text index gets updated.  
  
SELECT r.Comments, p.Name  
FROM Production.ProductReview AS r  
JOIN Production.Product AS p   
    ON r.ProductID = p.ProductID  
    AND r.ProductID = (SELECT ProductID  
FROM Production.ProductReview  
WHERE CONTAINS (Comments,   
    ' AdventureWorks2008 AND   
    Redmond AND   
    "Mountain-200 Silver" '));  
GO  
```  
  
### <a name="k-querying-on-a-document-property"></a>K. Abfragen von Dokumenteigenschaften  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Die folgende Abfrage sucht nach einer indizierten Eigenschaft (`Title`) in der `Document`-Spalte der `Production.Document`-Tabelle. Die Abfrage gibt nur Dokumente zurück, deren `Title`-Eigenschaft die Zeichenfolge `Maintenance` oder `Repair` enthält.  
  
> [!NOTE]  
>  Damit bei einer Eigenschaftensuche, Zeilen zurückgegeben werden können, muss die angegebene Eigenschaften von den Filtern extrahiert werden, die die Spalte während der Indexierung analysieren. Zudem muss der Volltextindex der jeweiligen Tabelle so konfiguriert sein, dass er die Eigenschaft einschließt. Weitere Informationen finden Sie unter [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Document 
FROM Production.Document  
WHERE CONTAINS(PROPERTY(Document,'Title'), 'Maintenance OR Repair');  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erste Schritte mit der Volltextsuche](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Erstellen und Verwalten von Volltextkatalogen](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md)   
 [Volltextsuche](../../relational-databases/search/full-text-search.md)   
 [Erstellen von Volltextsuchabfragen &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
