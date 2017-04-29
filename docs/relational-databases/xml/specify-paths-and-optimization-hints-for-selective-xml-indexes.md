---
title: "Angeben von Pfaden und Optimierungshinweisen für selektive XML-Indizes | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 486ee339-165b-4aeb-b760-d2ba023d7d0a
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3c07b191fe73f8cab21a9f3876230d344ad99968
ms.lasthandoff: 04/11/2017

---
# <a name="specify-paths-and-optimization-hints-for-selective-xml-indexes"></a>Angeben von Pfaden und Optimierungshinweisen für selektive XML-Indizes
  In diesem Thema wird beschrieben, wie Sie Knotenpfade zum Index angeben, und es werden Optimierungshinweise für die Indizierung aufgeführt, wenn Sie selektive XML-Indizes erstellen oder ändern.  
  
 Sie geben Knotenpfade und Optimierungshinweise gleichzeitig in einer der folgenden Anweisungen an:  
  
-   In der **FOR** -Klausel einer **CREATE** -Anweisung. Weitere Informationen finden Sie unter [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
-   In der **ADD** -Klausel einer **ALTER** -Anweisung. Weitere Informationen finden Sie unter [ALTER INDEX &#40;Selective XML Indexes&#41;](../../t-sql/statements/alter-index-selective-xml-indexes.md).  
  
 Weitere Informationen über selektive XML-Indizes finden Sie unter [Selektive XML-Indizes &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
##  <a name="untyped"></a> Grundlegendes zu XQuery- und SQL Server-Typen in nicht typisiertem XML  
 Selektive XML-Indizes unterstützen zwei Typsysteme: XQuery-Typen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Typen. Der indizierte Pfad kann verwendet werden, um entweder eine Entsprechung für einen XQuery-Ausdruck oder um eine Entsprechung für den Rückgabetyp der value()-Methode des XML-Datentyps zu finden.  
  
-   Wenn ein zu indizierender Pfad nicht kommentiert ist oder mit dem XQUERY-Schlüsselwort kommentiert ist, entspricht der Pfad einem XQuery-Ausdruck. Es gibt zwei Varianten von XQUERY-kommentierten Knotenpfaden:  
  
    -   Wenn Sie das XQUERY-Schlüsselwort und den XQuery-Datentyp nicht angeben, werden Standardzuordnungen verwendet. In der Regel sind Leistung und Speicher dann nicht optimal.  
  
    -   Wenn Sie das XQUERY-Schlüsselwort und den XQuery-Datentyp sowie optional andere Optimierungshinweise angeben, können Sie die bestmögliche Leistung und den effizientesten möglichen Speicher erzielen. Eine Umwandlung kann jedoch fehlschlagen.  
  
-   Wenn ein zu indizierender Pfad mit dem SQL-Schlüsselwort kommentiert ist, entspricht der Pfad dem Rückgabetyp der value()-Methode des XML-Datentyps. Geben Sie den entsprechenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp an, bei dem es sich um den Rückgabetypen handelt, den Sie von der value()-Methode erwarten.  
  
 Es gibt feine Unterschiede zwischen dem XML-Typsystem der XQuery-Ausdrücke und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Typsystem, das für die value()-Methode des XML-Datentyps angewendet wird. Zu diesen Unterschieden gehören unter anderem:  
  
-   Das XQuery-Typsystem beachtet Leerzeichen. So sind zum Beispiel der Semantik des XQuery-Typs nach die Zeichenfolgen"abc" und "abc " nicht identisch, wohingegen diese Zeichenfolgen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identisch sind.  
  
-   XQuery-Gleitkommadatentypen unterstützen die speziellen Werte von +/- 0 (null) und +/- Unendlichkeit. Diese speziellen Werte werden in den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Gleitkommadatentypen nicht unterstützt.  
  
### <a name="xquery-types-in-untyped-xml"></a>XQuery-Typen in nicht typisiertem XML  
  
-   XQuery-Typen entsprechen den XQuery-Ausdrücken in allen Methoden des XML-Datentyps, einschließlich der value()-Methode.  
  
-   XQuery-Typen unterstützen diese Optimierungshinweise: node(), SINGLETON, DATA TYPE und MAXLENGTH.  
  
 Für XQuery-Ausdrücke über nicht typisiertem XML können Sie zwischen zwei Vorgangsmodi auswählen:  
  
-   **Standardmäßiger Zuordnungsmodus**. In diesem Modus geben Sie nur den Pfad an, wenn Sie einen selektiven XML-Index erstellen.  
  
-   **Vom Benutzer angegebener Zuordnungsmodus**. In diesem Modus geben Sie sowohl den Pfad als auch optionale Optimierungshinweise an.  
  
 Der Standardzuordnungsmodus verwendet eine konservative Speicheroption, die immer sicher und allgemein ist. Sie kann jedem Ausdruckstyp entsprechen. Eine Einschränkung des Standardzuordnungsmodus ist die nicht optimale Leistung, da eine größere Anzahl von Laufzeitumwandlungen erforderlich ist, und sekundäre Indizes nicht verfügbar sind.  
  
 Hier ist ein Beispiel für einen selektiven, mit Standardzuordnungen erstellten XML-Index. Für alle drei Pfade werden der Standardknotentyp (**xs:untypedAtomic**) und Kardinalität verwendet.  
  
```tsql  
CREATE SELECTIVE XML INDEX example_sxi_UX_default  
ON Tbl(xmlcol)  
FOR  
(  
mypath01 =  '/a/b',  
mypath02 = '/a/b/c',  
mypath03 = '/a/b/d'  
)  
```  
  
 Mit dem vom Benutzer angegebene Zuordnungsmodus können Sie einen Typen und die Kardinalität für den Knoten angeben, um eine bessere Leistung zu erzielen. Diese verbesserte Leistung wird jedoch nur durch Verzicht auf Sicherheit (da eine Umwandlung fehlschlagen kann) und durch Verzicht auf Allgemeinheit (da nur der angegebene Typ mit dem selektiven XML-Index verglichen wird) erreicht.  
  
 Die für nicht typisiertes XML unterstützten XQuery-Typen sind:  
  
-   **xs:boolean**  
  
-   **xs:double**  
  
-   **xs:string**  
  
-   **xs:date**  
  
-   **xs:time**  
  
-   **xs:dateTime**  
  
 Wenn der Typ nicht angegeben wird, wird davon ausgegangen, dass der Knoten den **xs:untypedAtomic** -Datentyp aufweist.  
  
 Sie können den selektiven XML-Index wie nachfolgend aufgeführt optimieren:  
  
```tsql  
CREATE SELECTIVE XML INDEX example_sxi_UX_optimized  
ON Tbl(xmlcol)  
FOR  
(  
mypath= '/a/b' as XQUERY 'node()',  
pathX = '/a/b/c' as XQUERY 'xs:double' SINGLETON,  
pathY = '/a/b/d' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
)  
-- mypath – Only the node value is needed; storage is saved.  
-- pathX – Performance is improved; secondary indexes are possible.  
-- pathY - Performance is improved; secondary indexes are possible; storage is saved.  
```  
  
### <a name="sql-server-types-in-untyped-xml"></a>SQL Server-Typen in nicht typisiertem XML  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Typen entsprechen dem Rückgabewert der value()-Methode.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Typen unterstützen diesen Optimierungshinweis: SINGLETON.  
  
 Die Angabe eines Typs ist für Pfade erforderlich, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Typen zurückgeben. Verwenden Sie den gleichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Typ, den Sie in der value()-Methode verwenden würden.  
  
 Betrachten Sie die folgende Abfrage:  
  
```tsql  
SELECT T.record,  
    T.xmldata.value('(/a/b/d)[1]', 'NVARCHAR(200)')  
FROM myXMLTable T  
```  
  
 Die angegebene Abfrage gibt einen Wert des Pfads `/a/b/d` zurück, der in einen NVARCHAR(200)-Datentyp gepackt ist, sodass der für den Knoten anzugebende Datentyp offensichtlich ist. Es gibt jedoch kein Schema, um die Kardinalität des Knotens in nicht typisiertem XML anzugeben. Um diesen Knoten anzugeben ( `d` tritt höchstens einmal unter dem übergeordneten Knoten `b`auf), erstellen Sie einen selektiven XML-Index, der den Optimierungshinweis SINGLETON wie folgt verwendet:  
  
```tsql  
CREATE SELECTIVE XML INDEX example_sxi_US  
ON Tbl(xmlcol)  
FOR  
(  
node1223 = '/a/b/d' as SQL NVARCHAR(200) SINGLETON  
)  
```  
  
  
##  <a name="typed"></a> Grundlegendes zu selektiver XML-Indexunterstützung für typisiertes XML  
 Typisiertes XML in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist ein Schema, das einem bestimmten XML-Dokument zugeordnet ist. Das Schema definiert die Gesamtdokumentstruktur und Typen von Knoten. Ist ein Schema vorhanden, wendet der selektive XML-Index die Schemastruktur an, wenn der Benutzer Pfade höher stuft. Daher ist es nicht notwendig, die XQUERY-Typen für Pfade anzugeben.  
  
 Ein selektiver XML-Index unterstützt die folgenden XSD-Typen:  
  
-   **xs:anyUri**  
  
-   **xs:boolean**  
  
-   **xs:date**  
  
-   **xs:dateTime**  
  
-   **xs:day**  
  
-   **xs:decimal**  
  
-   **xs:double**  
  
-   **xs:float**  
  
-   **xs:int**  
  
-   **xs:integer**  
  
-   **xs:language**  
  
-   **xs:long**  
  
-   **xs:name**  
  
-   **xs:NCName**  
  
-   **xs:negativeInteger**  
  
-   **xs:nmtoken**  
  
-   **xs:nonNegativeInteger**  
  
-   **xs:nonPositiveInteger**  
  
-   **xs:positiveInteger**  
  
-   **xs:qname**  
  
-   **xs:short**  
  
-   **xs:string**  
  
-   **xs:time**  
  
-   **xs:token**  
  
-   **xs:unsignedByte**  
  
-   **xs:unsignedInt**  
  
-   **xs:unsignedLong**  
  
-   **xs:unsignedShort**  
  
 Wenn ein selektiver XML-Index für ein Dokument erstellt wird, dem ein Schema zugeordnet ist, tritt beim Angeben eines XQUERY-Typs bei der Indexerstellung oder bei der Änderung ein Fehler auf. Der Benutzer kann SQL-Typanmerkungen bei der Pfadheraufstufung verwenden. Der SQL-Typ muss eine gültige Konvertierung des XSD-Typs sein, der im Schema definiert ist, oder es wird ein Fehler ausgelöst. Es werden alle SQL-Typen unterstützt, die in XSD über eine entsprechende Darstellung verfügen, mit Ausnahme der Typen für Datum/Uhrzeit.  
  
> [!NOTE]  
>  Der selektive Index wird verwendet, wenn der bei der Pfadhöherstufung des selektiven XML-Index angegebene Typ mit dem Rückgabewert der value()-Methode identisch ist.  
  
 Die folgenden Optimierungshinweise können mit typisierten XML-Dokumenten verwendet werden:  
  
-   node()-Optimierungshinweis.  
  
-   Der MAXLENGTH-Optimierungshinweis kann mit xs:string-Typen verwendet werden, um den indizierten Wert zu kürzen.  
  
 Weitere Informationen zu Optimierungshinweisen finden Sie unter [Angeben von Optimierungshinweisen](#hints).  
  
##  <a name="paths"></a> Angeben von Pfaden  
 Mit einem selektiven XML-Index können Sie nur eine Teilmenge der Knoten aus den gespeicherten XML-Daten, die für die voraussichtlich durchgeführten Abfragen relevant sind, indizieren. Wenn die Teilmenge der relevanten Knoten viel kleiner als die Gesamtzahl der Knoten im XML-Dokument ist, speichert der selektive XML-Index nur die relevanten Knoten. Um von einem selektiven XML-Index profitieren zu können, identifizieren Sie die richtige Teilmenge der Knoten für die Indizierung.  
  
### <a name="choosing-the-nodes-to-index"></a>Auswählen der zu indizierenden Knoten  
 Mithilfe der beiden folgenden einfachen Prinzipien können Sie die richtige Teilmenge der Knoten ermitteln, die einem selektiven XML-Index hinzugefügt werden soll.  
  
1.  **Prinzip 1**: Indizieren Sie alle Knoten, die Sie untersuchen müssen, um einen bestimmten XQuery-Ausdruck auszuwerten.  
  
    -   Indizieren Sie alle Knoten, deren Vorhandensein oder Wert im XQuery-Ausdruck verwendet wird.  
  
    -   Indizieren Sie alle Knoten im XQuery-Ausdruck, auf den XQuery-Prädikate angewendet werden.  
  
     Betrachten Sie die folgende einfache Abfrage des [Beispiel-XML-Dokuments](#sample) in diesem Thema:  
  
    ```tsql  
    SELECT T.record FROM myXMLTable T  
    WHERE T.xmldata.exist('/a/b[./c = "43"]') = 1  
    ```  
  
     Um die XML-Instanzen zurückzugeben, die diese Abfrage erfüllen, muss ein selektiver XML-Index zwei Knoten in jeder XML-Instanz untersuchen:  
  
    -   Knoten `c`, da sein Wert im XQuery-Ausdruck verwendet wird.  
  
    -   Knoten `b`, da ein Prädikat auf den Knoten`b` im XQuery-Ausdruck angewendet wird.  
  
2.  **Prinzip 2**: Um eine optimale Leistung zu erzielen, indizieren Sie alle Knoten, die für die Auswertung eines bestimmten XQuery-Ausdrucks erforderlich sind. Wenn Sie nur einige der Knoten indizieren, dann verbessert der selektive XML-Index die Auswertung der Teilausdrücke, die nur indizierte Knoten umfassen.  
  
 Um die Leistung der oben aufgeführten SELECT-Anweisung zu verbessern, können Sie den folgenden selektiven XML-Index erstellen:  
  
```tsql  
CREATE SELECTIVE XML INDEX simple_sxi  
ON Tbl(xmlcol)  
FOR  
(  
    path123 =  '/a/b',  
    path124 =  '/a/b/c'  
)  
```  
  
### <a name="indexing-identical-paths"></a>Indizieren von identischen Pfaden  
 Sie können keine identischen Pfade als gleichen Datentyp unter verschiedenen Pfadnamen höher stufen. Die folgende Abfrage löst z. B. einen Fehler aus, da `pathOne` und `pathTwo` identisch sind:  
  
```tsql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:string',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
 Sie können jedoch identische Pfade als andere Datentypen mit anderen Namen höher stufen. So ist die folgende Abfrage beispielsweise jetzt akzeptabel, da die Datentypen verschieden sind:  
  
```tsql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:double',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
### <a name="examples"></a>Beispiele  
 Hier sind einige weitere Beispiele zum Auswählen der richtigen Knoten, die für verschiedene XQuery-Typen zu indizieren sind.  
  
 **Beispiel 1**  
  
 Hier ist eine einfache XQuery aufgeführt, die die exist()-Methode verwendet:  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e/h') = 1  
```  
  
 In der folgenden Tabelle sind die Knoten aufgeführt, die indiziert werden müssen, damit diese Abfrage den selektiven XML-Index verwendet.  
  
|In den Index einzuschließender Knoten|Grund zum Indizieren dieses Knotens|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e/h**|Das Vorhandensein des Knotens `h` wird in der exist()-Methode ausgewertet.|  
  
 **Beispiel 2**  
  
 Hier ist eine komplexere Variante der vorherigen XQuery mit einem angewendeten Prädikat aufgeführt:  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e[./f = "SQL"]') = 1  
```  
  
 In der folgenden Tabelle sind die Knoten aufgeführt, die indiziert werden müssen, damit diese Abfrage den selektiven XML-Index verwendet.  
  
|In den Index einzuschließender Knoten|Grund zum Indizieren dieses Knotens|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|Ein Prädikat wird auf den Knoten `e`angewendet.|  
|**/a/b/c/d/e/f**|Der Wert des Knotens `f` wird innerhalb des Prädikats ausgewertet.|  
  
 **Beispiel 3**  
  
 Hier ist eine komplexe Abfrage mit einer value()-Klausel aufgeführt:  
  
```tsql  
SELECT T.record,  
    T.xmldata.value('(/a/b/c/d/e[./f = "SQL"]/g)[1]', 'nvarchar(100)')  
FROM myXMLTable T  
```  
  
 In der folgenden Tabelle sind die Knoten aufgeführt, die indiziert werden müssen, damit diese Abfrage den selektiven XML-Index verwendet.  
  
|In den Index einzuschließender Knoten|Grund zum Indizieren dieses Knotens|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|Ein Prädikat wird auf den Knoten `e`angewendet.|  
|**/a/b/c/d/e/f**|Der Wert des Knotens `f` wird innerhalb des Prädikats ausgewertet.|  
|**/a/b/c/d/e/g**|Der Wert des Knotens `g` wird von der value()-Methode zurückgegeben.|  
  
 **Beispiel 4**  
  
 Hier ist eine Abfrage aufgeführt, die eine FLWOR-Klausel innerhalb einer exist()-Klausel verwendet. (Der Name "FLWOR" leitet sich von den fünf Klauseln ab, aus denen sich ein FLWOR-Ausdruck von XQuery zusammensetzen kann: for, let, where, order by und return.)  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('  
  For $x in /a/b/c/d/e  
  Where $x/f = "SQL"  
  Return $x/g  
') = 1  
```  
  
 In der folgenden Tabelle sind die Knoten aufgeführt, die indiziert werden müssen, damit diese Abfrage den selektiven XML-Index verwendet.  
  
|In den Index einzuschließender Knoten|Grund zum Indizieren dieses Knotens|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|Das Vorhandensein des Knotens `e` wird in der FLWOR-Klausel ausgewertet.|  
|**/a/b/c/d/e/f**|Der Wert des Knotens `f` wird in der FLWOR-Klausel ausgewertet.|  
|**/a/b/c/d/e/g**|Das Vorhandensein des Knotens `g` wird von der exist()-Methode ausgewertet.|  
  
  
##  <a name="hints"></a> Angeben von Optimierungshinweisen  
 Sie können optionale Optimierungshinweise verwenden, um zusätzliche Mappingdetails für einen Knoten anzugeben, der von einem selektiven XML-Index indiziert wird. Sie können z. B. den Datentyp und die Kardinalität des Knotens sowie bestimmte Informationen zur Struktur der Daten angeben. Diese zusätzlichen Informationen unterstützen eine bessere Zuordnung. Sie ermöglichen darüber hinaus eine Verbesserungen der Leistung und Speichereinsparungen oder sogar beides.  
  
 Die Verwendung von Optimierungshinweisen ist optional. Sie können stets die Standardzuordnungen übernehmen, die zuverlässig sind, möglicherweise jedoch keine optimale Leistung und Speicher bereitstellen.  
  
 Einige Optimierungshinweise, z. B. der SINGLETON-Hinweis, führen Sie Einschränkungen der Daten. In einigen Fällen werden möglicherweise Fehler ausgelöst, wenn diese Einschränkungen nicht erfüllt werden.  
  
### <a name="benefits-of-optimization-hints"></a>Vorteile von Optimierungshinweisen  
 In der folgenden Tabelle sind die Optimierungshinweise aufgeführt, die einen effizienteren Speicher oder eine verbesserte Leistung ermöglichen.  
  
|Optimierungshinweis|Effizienterer Speicher|Verbesserte Leistung|  
|-----------------------|----------------------------|--------------------------|  
|**node()**|Ja|Nein|  
|**SINGLETON**|Nein|Ja|  
|**DATA TYPE**|Ja|Ja|  
|**MAXLENGTH**|Ja|Ja|  
  
### <a name="optimization-hints-and-data-types"></a>Optimierungshinweise und Datentypen  
 Sie können Knoten als XQuery-Datentypen oder als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen indizieren. In der folgenden Tabelle ist aufgeführt, welche Optimierungshinweise für die einzelnen Datentypen unterstützt werden.  
  
|Optimierungshinweis|XQuery-Datentypen|SQL-Datentypen|  
|-----------------------|-----------------------|--------------------|  
|**node()**|Ja|Nein|  
|**SINGLETON**|Ja|Ja|  
|**DATA TYPE**|Ja|Nein|  
|**MAXLENGTH**|Ja|Nein|  
  
### <a name="node-optimization-hint"></a>node()-Optimierungshinweis  
 Gilt für: XQuery-Datentypen  
  
 Sie können mithilfe der node()-Optimierung einen Knoten angeben, dessen Wert nicht erforderlich ist, um die typische Abfrage auszuwerten. Dieser Hinweis reduziert Speicheranforderungen, wenn die typische Abfrage nur das Vorhandensein des Knotens auswerten muss. (Standardmäßig speichert ein selektiver XML-Index den Wert für alle höher gestuften Knoten, außer komplexen Knotentypen.)  
  
 Betrachten Sie das folgende Beispiel:  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b[./c=5]') = 1  
```  
  
 Um einen selektiven XML-Index zum Auswerten dieser Abfrage zu verwenden, stufen Sie die Knoten `b` und `c`höher. Da jedoch der Wert des Knotens `b` nicht erforderlich ist, können Sie den node()-Hinweis mit der folgenden Syntax verwenden:  
  
 `/a/b/ as node()`  
  
 Wenn eine Abfrage den Wert eines Knotens erfordert, der mit dem node()-Hinweis indiziert wurde, dann kann der selektive XML-Index nicht verwendet werden.  
  
### <a name="singleton-optimization-hint"></a>SINGLETON-Optimierungshinweis  
 Gilt für: XQuery- oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen  
  
 Der SINGLETON-Optimierungshinweis gibt die Kardinalität eines Knotens an. Dieser Hinweis verbessert die Abfrageleistung, da im Voraus bekannt ist, dass ein Knoten höchstens einmal in seinem übergeordneten Element oder Vorgänger angezeigt wird.  
  
 Beachten Sie das [Beispiel-XML-Dokument](#sample) in diesem Thema.  
  
 Um einen selektiven XML-Index zum Abfragen dieses Dokuments zu verwenden, können Sie den SINGLETON-Hinweis für den Knoten `d` angeben, da er höchstens einmal in seinem übergeordneten Element vorkommt.  
  
 Wenn der SINGLETON-Hinweis angegeben wurde, ein Knoten jedoch mehr als einmal in seinem übergeordneten Element oder Vorgänger vorkommt, dann wird ein Fehler ausgelöst, wenn Sie den Index (für vorhandene Daten) erstellen, oder wenn Sie eine Abfrage (für neue Daten) ausführen.  
  
### <a name="data-type-optimization-hint"></a>DATA TYPE-Optimierungshinweis  
 Gilt für: XQuery-Datentypen  
  
 Mit dem DATA TYPE-Optimierungshinweis können Sie eine XQuery oder einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp für den indizierten Knoten angeben. Der Datentyp wird in der Datentabelle des selektiven XML-Indexes für die Spalte verwendet, die dem indizierten Knoten entspricht.  
  
 Wenn es bei der Umwandlung eines vorhandenen Werts in den angegebenen Datentyp zu einem Fehler kommt, verursacht der Einfügevorgang (in den Index) keinen Fehler. Es wird jedoch ein NULL-Wert in die Datentabelle des Index eingefügt.  
  
### <a name="maxlength-optimization-hint"></a>MAXLENGTH-Optimierungshinweis  
 Gilt für: XQuery-Datentypen  
  
 Mit dem MAXLENGTH-Optimierungshinweis können Sie die Länge der xs:string-Daten einschränken. MAXLENGTH ist nicht relevant für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen, da Sie die Länge angeben, wenn Sie den VARCHAR- oder NVARCHAR-Datentyp angeben.  
  
 Wenn eine vorhandene Zeichenfolge länger als der angegebene Wert für MAXLENGTH ist, kommt es beim Einfügen dieses Werts zu einem Fehler.  
  
  
##  <a name="sample"></a> Beispiel-XML-Dokument für Beispiele  
 Auf das folgende Beispiel-XML-Dokument wird in den Beispielen in diesem Thema verwiesen:  
  
```xml  
<a>  
    <b>  
         <c atc="aa">10</c>  
         <c atc="bb">15</c>  
         <d atd1="dd" atd2="ddd">md </d>  
    </b>  
     <b>  
        <c></c>  
        <c atc="">117</c>  
     </b>  
</a>  
```  
  
  
## <a name="see-also"></a>Siehe auch  
 [Selektive XML-Indizes &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Erstellen, Ändern und Löschen selektiver XML-Indizes](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  
