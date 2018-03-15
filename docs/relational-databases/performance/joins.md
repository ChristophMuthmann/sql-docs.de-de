---
title: Joins (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/18/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology:
- joins
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- HASH join
- NESTED LOOPS join
- MERGE join
- joins [SQL Server], about joins
- join hints [SQL Server]
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f4b2bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7cecbf07ab49ca9f5e4545e6ca5376a200c6fe3d
ms.sourcegitcommit: 7e9380e53341755df13fce130ab3287918a8e44c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
# <a name="joins-sql-server"></a>Joins (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verwendet bei Sortier-, Schnittmengen-, Vereinigungs- und Vorgängen zum Feststellen von Unterschieden arbeitsspeicherinterne Sortierverfahren und Hashjointechniken. Beim Verwenden dieses Abfrageplantyps unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die vertikale Tabellenpartitionierung, auch spaltenweise Speicherung genannt.   

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Unterstützt drei Typen von Joinvorgängen:    
-   Joins geschachtelter Schleifen     
-   Zusammenführungsjoins   
-   Hashjoins   

## <a name="fundamentals"></a> Grundlegende Informationen zu Joins
Mithilfe von Joins können Sie Daten aus zwei oder mehr Tabellen basierend auf logischen Beziehungen zwischen den Tabellen abrufen. Joins zeigen an, wie Microsoft SQL Server Daten aus einer Tabelle zum Auswählen der Zeilen in einer anderen Tabelle verwenden soll.    

Eine Joinbedingung definiert die Beziehung zweier Tabellen in einer Abfrage auf folgende Art:    
-   Sie gibt die Spalte aus jeder Tabelle an, die für den Join verwendet werden soll. Eine typische Joinbedingung gibt einen Fremdschlüssel aus einer Tabelle und den zugehörigen Schlüssel in der anderen Tabelle an.    
-   Sie gibt einen logischen Operator (z. B. = oder <>) an, der zum Vergleichen von Werten aus den Spalten verwendet wird.    

Innere Joins können in `FROM`- oder in `WHERE`-Klauseln angegeben werden. Äußere Joins können nur in der `FROM`-Klausel angegeben werden. Die Joinbedingungen in Verbindung mit `WHERE`- und `HAVING`-Suchbedingungen steuern, welche Zeilen aus den Basistabellen ausgewählt werden, auf die in der `FROM`-Klausel verwiesen wird.    

Das Angeben der Joinbedingungen in der `FROM`-Klausel trägt dazu bei, dass diese von anderen, möglicherweise in einer `WHERE`-Klausel angegebenen Suchbedingungen getrennt werden. Dies ist die empfohlene Methode zur Angabe von Joins. Das Folgende ist eine vereinfachte ISO-Joinssyntax für eine FROM-Klausel:

```
FROM first_table join_type second_table [ON (join_condition)]
```

*join_type* gibt an, welche Art von Join ausgeführt wird: innerer Join, äußerer Join oder Cross Join. *join_condition* definiert das Prädikat, das für jedes verknüpfte Zeilenpaar ausgewertet werden soll. Es folgt ein Beispiel für eine Joinangabe in einer FROM-Klausel:

```sql
FROM Purchasing.ProductVendor JOIN Purchasing.Vendor
     ON (ProductVendor.BusinessEntityID = Vendor.BusinessEntityID)
```

Es folgt eine einfache SELECT-Anweisung, die diesen Join verwendet:

```sql
SELECT ProductID, Purchasing.Vendor.BusinessEntityID, Name
FROM Purchasing.ProductVendor JOIN Purchasing.Vendor
    ON (Purchasing.ProductVendor.BusinessEntityID = Purchasing.Vendor.BusinessEntityID)
WHERE StandardPrice > $10
  AND Name LIKE N'F%'
GO
```

Die SELECT-Anweisung gibt die Produkt- und Lieferanteninformationen für alle Kombinationen von Teilen zurück, die von einer Firma geliefert werden, deren Firmenname mit dem Buchstaben F beginnt, und bei denen der Produktpreis über 10 $ liegt.   

Wenn in einer einzigen Abfrage auf mehrere Tabellen verwiesen wird, müssen alle Spaltenverweise eindeutig sein. Im vorherigen Beispiel verfügen sowohl die ProductVendor-Tabelle als auch die Vendor-Tabelle über eine Spalte mit dem Namen „BusinessEntityID“. Alle Spaltennamen, die in zwei oder mehr Tabellen vorkommen, auf die in der Abfrage verwiesen wird, müssen mit dem Tabellennamen gekennzeichnet werden. Alle Verweise auf die Vendor-Spalten im Beispiel sind gekennzeichnet.   

Wenn ein Spaltenname nicht in zwei oder mehr in der Abfrage verwendeten Tabellen vorkommt, brauchen Verweise darauf nicht mit dem Tabellennamen gekennzeichnet zu werden. Dies ist im vorherigen Beispiel dargestellt. Eine solche SELECT-Anweisung ist manchmal schwer verständlich, weil nicht angezeigt wird, welche Spalte aus welcher Tabelle stammt. Die Lesbarkeit der Abfrage wird verbessert, indem alle Spalten mit dem entsprechenden Tabellennamen gekennzeichnet werden. Die Übersichtlichkeit kann weiterhin durch Verwenden von Tabellenaliasnamen verbessert werden, besonders, wenn die Tabellennamen mit dem Datenbank- und Besitzernamen gekennzeichnet werden müssen. Das folgende Beispiel unterscheidet sich vom vorherigen nur dadurch, dass Tabellenaliasnamen zugewiesen und die Spalten der Übersichtlichkeit halber mit Tabellenaliasnamen gekennzeichnet wurden:

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv 
JOIN Purchasing.Vendor AS v
    ON (pv.BusinessEntityID = v.BusinessEntityID)
WHERE StandardPrice > $10
    AND Name LIKE N'F%';
```

In den vorhergehenden Beispielen wurden die Joinbedingungen in der FROM-Klausel angegeben. Dies ist die bevorzugte Methode. Die folgende Abfrage enthält dieselbe Joinbedingung, die in der WHERE-Klausel angegeben wird:

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv, Purchasing.Vendor AS v
WHERE pv.BusinessEntityID=v.BusinessEntityID
    AND StandardPrice > $10
    AND Name LIKE N'F%';
```

Die SELECT-Liste für einen Join kann auf alle Spalten in den verknüpften Tabellen oder auf eine beliebige Teilmenge der Spalten verweisen. Es ist nicht erforderlich, dass die SELECT-Liste Spalten aus allen Tabellen in dem Join enthält. So kann z. B. in einem Join dreier Tabellen nur eine Tabelle verwendet werden, um die anderen Tabellen zu verbinden, und in der Auswahlliste muss auf keine der Spalten aus der mittleren Tabelle verwiesen werden.   

Obwohl Joinbedingungen normalerweise Übereinstimmungsvergleiche (=) enthalten, können andere Vergleichsoperatoren oder relationale Operatoren ebenso wie andere Prädikate angegeben werden. Weitere Informationen finden Sie unter [Vergleichsoperatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md) und [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md).  

Beim Verarbeiten von Joins durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wählt das Abfragemodul aus verschiedenen Möglichkeiten die effizienteste Methode aus. Die physische Ausführung von verschiedenen Joins kann viele verschiedene Optimierungen verwenden, weshalb keine zuverlässige Einschätzung möglich ist.   

Spalten, die in einer Joinbedingung verwendet werden, müssen nicht den gleichen Namen oder Datentyp haben. Die Datentypen müssen jedoch kompatibel sein, falls sie nicht identisch sind, oder es müssen Datentypen sein, die SQL Server implizit konvertieren kann. Wenn die Datentypen nicht implizit konvertiert werden können, muss die Joinbedingung den Datentyp mithilfe der `CAST`-Funktion explizit konvertieren. Weitere Informationen zur impliziten und expliziten Konvertierung finden Sie unter [Datentypkonvertierung &#40;Datenbank-Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md).    

Die meisten Abfragen, die einen Join verwenden, können in eine Unterabfrage (eine in eine andere Abfrage geschachtelte Abfrage) umgeschrieben werden, und die meisten Unterabfragen können in Joins umgeschrieben werden. Weitere Informationen zu Unterabfragen finden Sie unter [Unterabfragen](../../relational-databases/performance/subqueries.md).   

> [!NOTE]
> Tabellen können nicht direkt über ntext-, text- oder image-Spalten verknüpft werden. Sie können jedoch mithilfe von `SUBSTRING` indirekt über ntext- , text- oder image-Spalten verknüpft werden.    
> `SELECT * FROM t1 JOIN t2 ON SUBSTRING(t1.textcolumn, 1, 20) = SUBSTRING(t2.textcolumn, 1, 20)` führt z.B. einen inneren Join zwischen zwei Tabellen auf den ersten 20 Zeichen jeder Textspalte in den Tabellen t1 und t2 aus.   
> Außerdem können ntext- oder text-Spalten aus zwei Tabellen verglichen werden, indem die Längen der Spalten mithilfe einer `WHERE`-Klausel wie im folgenden Beispiel verglichen werden: `WHERE DATALENGTH(p1.pr_info) = DATALENGTH(p2.pr_info)`.

## <a name="nested_loops"></a> Grundlegendes zu Nested Loops-Joins
Wenn eine Joineingabe klein (weniger als 10 Zeilen) und die andere Joineingabe relativ umfangreich ist und indizierte Joinspalten aufweist, ist ein indizierter Nested Loops-Join der schnellste Joinvorgang, da sie mit dem geringsten E/A-Aufkommen und den wenigsten Vergleichen auskommen. 

Der Join geschachtelter Schleifen, auch *geschachtelte Iteration* genannt, verwendet eine Joineingabe als äußere Eingabetabelle (im grafischen Ausführungsplan als obere Eingabe dargestellt) und eine zweite Joineingabe als innere (untere) Eingabetabelle. Die äußere Schleife verarbeitet die äußere Eingabetabelle zeilenweise. Die innere Schleife wird für jede äußere Zeile ausgeführt und sucht übereinstimmende Zeilen in der inneren Eingabetabelle.   

Im einfachsten Fall wird beim Suchvorgang eine Tabelle oder ein Index vollständig gescannt. Dieser Vorgang wird als *naiver Join geschachtelter Schleifen* bezeichnet. Wird beim Suchvorgang ein Index verwendet, wird dies *indizierter Join geschachtelter Schleifen* genannt. Wird der Index als Teil des Abfrageplans erstellt (und nach Beendigung der Abfrage gelöscht), wird dies *temporärer indizierter Join geschachtelter Schleifen* genannt. Alle beschriebenen Varianten werden vom Abfrageoptimierer berücksichtigt.   

Ein Nested Loops-Join ist besonders wirksam, wenn die äußere Eingabe klein und die innere Eingabe vorindiziert und umfangreich ist. In vielen kleinen Transaktionen, die beispielsweise nur wenige Zeilen betreffen, sind indizierte Nested Loops-Joins sowohl Zusammenführungsjoins als auch Hashjoins überlegen. In umfangreichen Abfragen dagegen sind Nested Loops-Joins häufig nicht die optimale Wahl.    

## <a name="merge"></a> Grundlegendes zu Zusammenführungsjoins
Sind beide Joineingaben nicht klein, aber nach ihrer Joinspalte sortiert (was beispielsweise der Fall ist, wenn sie beim Scannen sortierter Indizes gewonnen wurden), so ist ein Zusammenführungsjoin der schnellste Joinvorgang. Sind beide Joineingaben umfangreich und etwa gleich groß, so bietet ein Zusammenführungsjoin mit vorherigem Sortiervorgang und ein Hashjoin vergleichbares Leistungsverhalten. Hashjoinvorgänge sind jedoch häufig erheblich schneller, wenn sich beide Eingaben im Umfang deutlich unterscheiden.       

Der Zusammenführungsjoin setzt voraus, dass beide Eingaben nach den Zusammenführungsspalten sortiert sind; diese werden von den Gleichheitsoperatoren des Joinprädikats (in der ON-Klausel) definiert. Der Abfrageoptimierer scannt in der Regel einen Index, falls ein Index für die geeigneten Spalten vorhanden ist, oder platziert einen Sort-Operator unter den Zusammenführungsjoin. In seltenen Fällen treten mehrere Gleichheitsklauseln auf, jedoch werden die Zusammenführungsspalten nur von einigen der verfügbaren Gleichheitsklauseln genommen.    

Da die Eingaben sortiert vorliegen, ruft der **Merge Join**-Operator von jeder Eingabe jeweils eine Zeile ab und vergleicht diese. Beispielsweise werden bei inneren Joins die Zeilen zurückgegeben, wenn sie gleich sind. Sind sie nicht gleich, wird die Zeile mit dem kleineren Wert verworfen, und von der betreffenden Eingabe wird die nächste Zeile abgerufen. Dieser Vorgang wird wiederholt, bis alle Zeilen verarbeitet wurden.    

Die Zusammenführungsjoinoperation kann eine reguläre oder eine n:n-Operation sein. Ein n:n-Zusammenführungsjoin verwendet eine temporäre Tabelle, um Zeilen zu speichern. Treten bei den Eingaben doppelte Werte auf, so muss eine Eingabe bis zum ersten Duplikat zurückgespult werden, damit alle Duplikate der anderen Eingabe verarbeitet werden können.    

Ist ein Residualprädikat vorhanden, so werten alle Zeilen, die dem Zusammenführungsprädikat genügen, das Residualprädikat aus. Nur die Zeilen werden zurückgegeben, die auch dem Residualprädikat genügen.   

Der Zusammenführungsjoin ist sehr schnell, kann aber eine teure Wahl darstellen, wenn Sortieroperationen erforderlich sind. Wenn jedoch die Datenmenge umfangreich ist und die gewünschten Daten vorsortiert aus vorhandenen B-Baum-Indizes abgerufen werden können, ist der Zusammenführungsjoin häufig der schnellste Joinalgorithmus.    

## <a name="hash"></a> Grundlegendes zu Hashjoins
Hashjoins können umfangreiche, unsortierte, nicht indizierte Eingaben effizient verarbeiten. Sie sind für Zwischenergebnisse in komplexen Abfragen aus folgenden Gründen nützlich:
-   Zwischenergebnisse sind nicht indiziert (es sei denn, sie werden explizit auf einem Datenträger gespeichert und dann indiziert) und häufig nicht für den nächste Vorgang im Abfrageplan passend sortiert.
-   Abfrageoptimierer schätzen nur die Größe von Zwischenergebnissen ab. Weil Schätzungen in komplexen Abfragen sehr ungenau sein können, müssen Algorithmen zum Verarbeiten von Zwischenergebnissen nicht nur effizient sein, sondern auch kontrolliert beendet werden können, wenn ein Zwischenergebnis viel umfangreicher als erwartet ausfällt.   

Der Hashjoin lässt Reduktionen bei der Denormalisierung zu. Die Denormalisierung wird in der Regel verwendet, um bessere Leistung durch Reduzierung der Joinvorgänge zu erreichen, und zwar trotz der Redundanzgefahr wie beispielsweise durch inkonsistente Updates. Hashjoins vermindern den Bedarf, die Denormalisierung durchzuführen. Hashjoins ermöglichen die vertikale Partitionierung (die Darstellung von Spaltengruppen aus einer einzelnen Tabelle in separate Dateien oder Indizes), wodurch sie zu einer beachtenswerten Option für den physischen Datenbankentwurf wird.     

Der Hashjoin verfügt über zwei Eingaben: die **Erstellungseingabe** und die **Untersuchungseingabe**. Der Abfrageoptimierer weist diese Rollen so zu, dass die kleinere Eingabe als Erstellungseingabe verwendet wird.    

Hashjoins werden für viele ergebnismengenorientierte Operationen verwendet: INNER JOIN (innerer Join); LEFT, RIGHT und FULL OUTER JOIN (linker, rechter und vollständiger äußerer Join); LEFT SEMI-JOIN und RIGHT SEMI-JOIN (linker und rechter Semijoin); INTERSECTION (Schnittmenge); UNION (Vereinigungsmenge) und DIFFERENCE (Restmenge). Darüber hinaus können mit einer Variante des Hashjoins Duplikate entfernt und Gruppierungen vorgenommen werden, z.B. `SUM(salary) GROUP BY department`. Diese Varianten verwenden dieselbe Eingabe als Erstellungseingabe und Untersuchungseingabe.   

In den folgenden Abschnitten werden verschiedene Typen von Hashjoins beschrieben: arbeitsspeicherinterne Hashjoins, schrittweise Hashjoins und rekursive Hashjoins.    

### <a name="inmem_hash"></a> Arbeitsspeicherinterne Hashjoins

Der Hashjoin scannt oder berechnet zuerst die gesamte Erstellungseingabe und erstellt dann eine Hashtabelle im Arbeitsspeicher. Jede Zeile wird in ein Hashbucket eingefügt, abhängig von dem für den Hashschlüssel berechneten Hashwert. Wenn die gesamte Erstellungseingabe kleiner als der verfügbare Arbeitsspeicher ist, können alle Zeilen in die Hashtabelle eingefügt werden. Auf diese Erstellungsphase folgt die Untersuchungsphase. Die gesamte Untersuchungseingabe wird zeilenweise gescannt oder berechnet, und für jede Untersuchungszeile wird der Wert des Hashschlüssels berechnet, das entsprechende Hashbucket wird gescannt, und die Übereinstimmungen werden erzeugt.    

### <a name="grace_hash"></a> GRACE-Hashjoins

Wenn die Erstellungseingabe nicht vollständig in den Arbeitsspeicher passt, wird der Hashjoin in mehreren Schritten durchgeführt. Dies wird als schrittweiser Hashjoin bezeichnet. Jeder Schritt besteht aus einer Erstellungsphase und einer Untersuchungsphase. Zuerst wird die gesamte Erstellungseingabe und Untersuchungseingabe verarbeitet und (durch Anwenden einer Hashfunktion auf die Hashschlüssel) in mehrere Dateien aufgeteilt. Durch Anwenden der Hashfunktion auf die Hashschlüssel wird sichergestellt, dass die zwei zu verknüpfenden Datensätze sich stets in demselben Dateipaar befinden. So wird die Aufgabe, zwei umfangreiche Eingaben zu verknüpfen, auf mehrere kleinere gleichartige Teilaufgaben reduziert. Der Hashjoin wird dann auf jedes Paar partitionierter Dateien angewendet.    

### <a name="recursive_hash"></a> Rekursive Hashjoins

Wenn die Erstellungseingabe so umfangreich ist, dass Eingaben für einen standardmäßigen externen Mergeprozess mehrere Mergeebenen erfordern würden, sind mehrere Partitionierungsschritte und mehrere Partitionierungsebenen erforderlich. Sind nur einige Partitionen umfangreich, so sind zusätzliche Partitionierungsschritte nur für diese Partitionen erforderlich. Um alle Partitionierungsschritte möglichst schnell zu machen, werden umfangreiche, asynchrone E/A-Operationen verwendet, sodass bereits ein Thread mehrere Datenträger auslastet.    

> [!NOTE]
> Wenn die Erstellungseingabe nur wenig umfangreicher als der verfügbare Arbeitsspeicher ist, werden Elemente des schrittweisen und des arbeitsspeicherinternen Hashjoin in einem Schritt kombiniert, sodass ein hybrider Hashjoin entsteht.   

Bei der Optimierung kann nicht in jedem Fall ermittelt werden, welcher Hashjoin verwendet wird. Daher verwendet SQL Server zunächst einen arbeitsspeicherinternen Hashjoin und geht, abhängig von der Größe der Erstellungseingabe, sukzessive zum GRACE- und rekursiven Hashjoin über.    

Wenn der Abfrageoptimierer falsch einschätzt, welche Eingabe kleiner ist und daher als Erstellungseingabe verwendet werden müsste, werden die Rollen der Erstellungs- und der Untersuchungseingabe dynamisch vertauscht. Der Hashjoin stellt sicher, dass die kleinere Überlaufdatei als Erstellungseingabe verwendet wird. Diese Technik wird als Rollentausch bezeichnet. Ein Rollentausch tritt innerhalb des Hashjoins nach mindestens einem Überlauf auf den Datenträger auf.     

> [!NOTE]
> Der Rollentausch tritt unabhängig von Abfragehinweisen oder von der Struktur auf. Der Rollentausch wird nicht im Abfrageplan angezeigt. Wenn ein solcher Vorgang auftritt, erfolgt er transparent für den Benutzer.

### <a name="hash_bailout"></a> Hashabbruch

Der Begriff „Hashabbruch“ wird manchmal zur Beschreibung von GRACE- oder rekursiven Hashjoins verwendet.    

> [!NOTE]
> Rekursive Hashjoins oder Hashabbrüche verursachen eine reduzierte Leistung auf dem Server. Wenn in einer Ablaufverfolgung viele Hash Warning-Ereignisse angezeigt werden, sollten Sie die Statistiken für die verknüpften Spalten aktualisieren.    

Weitere Informationen zu Hashabbrüchen finden Sie unter [Hash Warning-Ereignisklasse](../../relational-databases/event-classes/hash-warning-event-class.md).    
  
## <a name="nulls_joins"></a> NULL-Werte und Joins
Wenn die Spalten der zu verknüpfenden Tabellen NULL-Werte enthalten, werden diese Werte nicht als übereinstimmend angesehen. Das Vorhandensein von NULL-Werten in einer Spalte aus einer der verknüpften Tabellen kann nur mithilfe eines äußeren Joins zurückgegeben werden (wenn die `WHERE`-Klausel keine NULL-Werte ausschließt).     

Es folgen zwei Tabellen, bei denen NULL in der Spalte enthalten ist, die Bestandteil des Joins ist.     

```
table1                          table2
a           b                   c            d
-------     ------              -------      ------
      1        one                 NULL         two
   NULL      three                    4        four
      4      join4
```    

Ein Join, der die Werte in der a-Spalte mit denen der c-Spalte vergleicht, erhält keine Übereinstimmung für die Zeilen, die NULL-Werte enthalten:

```sql
SELECT *
FROM table1 t1 JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```  

Nur eine Zeile mit dem Wert 4 in der a-Spalte und der c-Spalte wird zurückgegeben:

```
a           b      c           d      
----------- ------ ----------- ------ 
4           join4  4           four   

(1 row(s) affected)
```   

Außerdem sind aus einer Basistabelle zurückgegebene NULL-Werte schwer von den von einem äußeren Join zurückgegebenen NULL-Werten zu unterscheiden. Die folgende `SELECT`-Anweisung führt z. B. einen linken äußeren Join für diese beiden Tabellen aus:   

```sql
SELECT *
FROM table1 t1 LEFT OUTER JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```   

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]   

```
a           b      c           d      
----------- ------ ----------- ------ 
NULL        three  NULL        NULL 
1           one    NULL        NULL 
4           join4  4           four   

(3 row(s) affected)
```   

In den Ergebnissen ist ein NULL-Wert in den Daten nicht ohne Weiteres von einem NULL-Wert zu unterscheiden, der einen fehlgeschlagenen Join darstellt. Wenn NULL-Werte in den zu verknüpfenden Daten enthalten sind, empfiehlt es sich, sie durch einen normalen Join aus den Ergebnissen auszuschließen.    

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Referenz zu logischen und physischen Showplanoperatoren](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
[Vergleichsoperatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)    
[Datentypkonvertierung &#40;Datenbank-Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
[Unterabfragen](../../relational-databases/performance/subqueries.md)      
[Adaptive Joins](../../relational-databases/performance/adaptive-query-processing.md#batch-mode-adaptive-joins)    


  
  
