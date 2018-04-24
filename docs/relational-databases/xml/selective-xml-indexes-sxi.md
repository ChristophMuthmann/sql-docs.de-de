---
title: Selektive XML-Indizes (SXI) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 598ecdcd-084b-4032-81b2-eed6ae9f5d44
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4edc8cd05def83db0800067c6f71921ba4079ed
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="selective-xml-indexes-sxi"></a>Selektive XML-Indizes (SXI)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Selektive XML-Indizes sind ein weiterer Typ von XML-Index, der Ihnen zusätzlich zu den herkömmlichen XML-Indizes zur Verfügung steht. Die Ziele der selektiven XML-Indexfunktion sind Folgende:  
  
-   Verbessern der Leistung von Abfragen zu XML-Daten, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeichert sind.  
  
-   Unterstützen einer schnelleren Indizierung großer XML-Datenlasten.  
  
-   Verbessern der Skalierbarkeit durch das Reduzieren der Speicherkosten für XML-Indizes.  
  
 Die Haupteinschränkung bei herkömmlichen XML-Indizes liegt darin, dass sie das gesamte XML-Dokument indizieren. Dies führt zu mehreren bedeutenden Nachteilen, z. B. verringerter Abfrageleistung und höheren Kosten für die Indexwartung, die sich in der Regel auf die Indexspeicherkosten beziehen.  
  
 Mit der selektiven XML-Indexfunktion können Sie nur bestimmte Pfade aus den XML-Dokumenten zum Index höherstufen. Bei der Indexerstellung werden diese Pfade ausgewertet, und die Knoten, auf die sie verweisen, werden aufgeteilt und in einer relationalen Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeichert. Diese Funktion verwendet einen effizienten Zuordnungsalgorithmus, der in Zusammenarbeit mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Produktteam von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Research entwickelt wurde. Dieser Algorithmus ordnet die XML-Knoten einer einzelnen relationalen Tabelle zu und erzielt eine herausragende Leistung bei sehr geringem Speicherbedarf.  
  
 Die selektive XML-Indexfunktion unterstützt auch sekundäre selektive XML-Indizes für Knoten, die von einem selektiven XML-Index indiziert wurden. Diese sekundären selektiven Indizes sind effizient und verbessern die Leistung von Abfragen noch weiter.  
  
##  <a name="benefits"></a> Vorteile selektiver XML-Indizes  
 Selektive XML-Indizes bieten die folgenden Vorteile:  
  
1.  Deutlich verbesserte Abfrageleistung für den XML-Datentyp bei typische Abfragelasten.  
  
2.  Im Vergleich zu herkömmlichen XML-Indizes reduzierte Speicheranforderungen.  
  
3.  Im Vergleich zu herkömmlichen XML-Indizes reduzierte Indexwartungskosten.  
  
4.  Anwendungen müssen nicht aktualisiert werden, um die Vorteile selektiver XML-Indizes nutzen zu können.  
  
  
##  <a name="compare"></a> Selektive XML-Indizes und primäre XML-Indizes  
  
> [!IMPORTANT]  
>  Im Hinblick auf eine bessere Leistung und einen effizienteren Speicher erstellen Sie in den meisten Fällen einen selektiven XML-Index anstatt eines gewöhnlichen XML-Indexes.  
  
 Ein selektiver XML-Index wird jedoch nicht empfohlen, wenn eine der beiden folgenden Bedingungen zutrifft:  
  
-   Sie ordnen eine große Anzahl von Knotenpfaden zu.  
  
-   Sie unterstützen Abfragen für unbekannte Elemente oder Elemente in einer unbekannten Position in der Dokumentstruktur.  
  
  
##  <a name="example"></a> Einfaches Beispiel für einen selektiven XML-Index  
 Betrachten Sie das folgende XML-Fragment, das ein XML-Dokument in einer Tabelle mit ungefähr 500.000 Zeilen darstellt:  
  
```xml  
<book>  
    <created>2004-03-01</created>   
    <authors>Various</authors>  
    <subjects>  
        <subject>English wit and humor -- Periodicals</subject>  
        <subject>AP</subject>   
    </subjects>  
    <title>Punch, or the London Charivari, Volume 156, April 2, 1919</title>  
    <id>etext11617</id>  
</book>  
```  
  
 Die Erstellung eines primären XML-Index über so viele Zeilen dieses einfachen Schemas hinweg dauert sehr lange. Die Abfrage dieser Daten wird zusätzlich noch dadurch erschwert, dass ein primärer XML-Index keine selektive Indizierung unterstützt.  
  
 Wenn Sie diese Daten nur über den `/book/title` -Pfad und den `/book/subjects` -Pfad abfragen müssen, können Sie den folgenden selektiven XML-Index erstellen:  
  
```sql  
CREATE SELECTIVE XML INDEX SXI_index  
ON Tbl(xmlcol)  
FOR   
(  
    pathTitle = '/book/title/text()' AS XQUERY 'xs:string',   
    pathAuthors = '/book/authors' AS XQUERY 'node()',  
    pathId = '/book/id' AS SQL NVARCHAR(100)  
)  
```  
  
 Die vorangehende Anweisung ist ein gutes Beispiel für die CREATE-Syntax, die Sie zum Erstellen eines selektiven XML-Index verwenden. Sie geben in der CREATE-Anweisung zuerst einen Namen für den Index an und identifizieren die Tabelle und die XML-Spalte, die Sie indizieren möchten. Anschließend stellen Sie die zu indizierende Pfade bereit. Ein Pfad besteht aus drei Teilen:  
  
1.  Einem Namen, der den Pfad eindeutig angibt.  
  
2.  Einem XQuery-Ausdruck, der den Pfad beschreibt.  
  
3.  Optionalen Optimierungshinweise.  
  
 Weitere Informationen zu diesen Elementen finden Sie unter [Verwandte Aufgaben](#reltasks).  
  
  
## <a name="supported-features-prerequisites-and-limitations"></a>Unterstützte Funktionen, Voraussetzungen und Einschränkungen  
  
###  <a name="features"></a> Unterstützte XML-Funktionen  
 Selektive XML-Indizes unterstützen die XQuery, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in den exist()-, value()- und nodes()-Methoden unterstützt werden.  
  
-   Für die exist()-, value()- und nodes()-Methoden enthalten selektive XML-Indizes ausreichende Informationen, um den gesamten Ausdruck zu transformieren.  
  
-   Für die query()- und modify()-Methoden können selektive XML-Indizes möglicherweise nur zum Filtern von Knoten verwendet werden.  
  
-   Für die query()-Methode werden selektive XML-Indizes nicht zum Abrufen von Ergebnissen verwendet.  
  
-   Für die modify()-Methode werden selektive XML-Indizes nicht zum Aktualisieren von XML-Dokumenten verwendet.  
  
  
###  <a name="unsupported"></a> Nicht unterstützte XML-Funktionen  
 Selektive XML-Indizes unterstützen nicht die folgenden Funktionen, die in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Implementierung von XML unterstützt werden:  
  
-   Indizieren von Knoten mit komplexen XS-Typen: Union-Typen, Sequenztypen, und Listtypen.  
  
-   Indizieren von Knoten mit binären XS-Typen: z. B. base64Binary und hexBinary.  
  
-   Angeben von Knoten, die mit XPath-Ausdrücken indiziert werden sollen und am Ende das Platzhalterzeichen `*` aufweisen: z. B.  `/a/b/c/*`, `/a//b/*`oder `/a/b/*:c`.  
  
-   Indizieren einer anderen Achse als untergeordnetes Element, Attribut oder Nachfolger. Der `//<step>` -Fall ist als spezieller Fall zulässig.  
  
-   Indizieren von XML-Verarbeitungsanweisungen und -Kommentaren.  
  
-   Angeben und Abrufen des Bezeichners für einen Knoten mit der id()-Funktion.  
  
  
###  <a name="prereq"></a> Erforderliche Komponenten  
 Die folgenden Voraussetzungen müssen erfüllt sein, bevor Sie einen selektiven XML-Index für eine XML-Spalte in einer Benutzertabelle erstellen können:  
  
-   Für den Primärschlüssel der Benutzertabelle muss ein gruppierter Index vorhanden sein.  
  
-   Der Primärschlüssel der Benutzertabelle ist auf eine Größe von 128 Byte beschränkt, wenn er zusammen mit selektiven XML-Indizes verwendet wird.  
  
-   Der Gruppierungsschlüssel der Benutzertabelle ist auf 15 Spalten beschränkt, wenn er zusammen mit selektiven XML-Indizes verwendet wird.  
  
  
###  <a name="limits"></a> Einschränkungen  
 **Allgemeine Anforderungen und Einschränkungen**  
  
-   Jeder selektive XML-Index kann nur für eine einzige XML-Spalte erstellt werden.  
  
-   Für eine Spalte, die keine XML-Spalte ist, kann kein selektiver XML-Index erstellt werden.  
  
-   Jede XML-Spalte in einer Tabelle kann nur über einen selektiven XML-Index verfügen.  
  
-   Jede Tabelle kann bis zu 249 selektive XML-Indizes enthalten.  
  
 **Einschränkungen für unterstützte Objekte**  
  
 Für die folgenden Objekte können keine selektiven XML-Indizes erstellt werden:  
  
1.  XML-Spalten in einer Sicht.  
  
2.  Tabellenwertvariable mit XML-Spalten.  
  
3.  XML-Typvariablen.  
  
4.  Berechnete XML Spalten.  
  
5.  XML-Spalten mit einer Tiefe von mehr als 128 geschachtelten Knoten.  
  
 **Auf Speicher bezogene Einschränkungen**  
  
 Die Anzahl der Knoten aus dem XML-Dokument, die dem Index hinzugefügt werden können, ist beschränkt. Ein selektiver XML-Index ordnet XML-Dokumente einer einzelnen relationalen Tabelle zu. Daher kann er nicht mehr als 1024 Spalten mit Nicht-NULL-Werten in den Spalten der Tabelle aufweisen. Weiterhin gelten viele der Einschränkungen von Sparsespalten auch für selektive XML-Indizes, da die Indizes Sparsespalten zum Speichern verwenden.  
  
 Die maximale Anzahl von Nicht-NULL-Spalten, die in einer Zeile unterstützt werden, hängt von der Größe der Daten in den Spalten ab:  
  
-   Im besten Fall werden 1024 Nicht-NULL-Spalten unterstützt, wenn alle Spalten den Typ **bit**haben.  
  
-   Im schlimmsten Fall werden nur 236 Nicht-NULL-Spalten unterstützt, wenn alle Spalten große Objekte des Typs **varchar**sind.  
  
 Selektive XML-Indizes verwenden intern ein bis vier Spalten für jeden Knotenpfad, der indiziert wird. Die Gesamtzahl der Knoten, die indizierte werden können, reicht von 60 bis zu mehreren hundert Knoten, abhängig von der tatsächlichen Größe der Daten in den indizierten Pfaden.  
  
-   Im schlimmsten Fall, wenn einige oder alle Knoten in der Knotenpfaddefinition mit `//` zugeordnet sind, beträgt die maximale Anzahl indizierter Knoten 60.  
  
-   Im besten Fall, wenn Knoten ohne `//` in der Knotenpfaddefinition zugeordnet werden, beträgt die maximale Anzahl indizierter Knoten 200.  
  
 **Selektive XML-Indizes werden neu erstellt, wenn Sie CREATE oder ALTER für den Index ausführen.**  
  
 Wenn Sie einen selektiven XML-Index erstellen (CREATE) oder ändern (ALTER), wird er im Singlethread-Offlinemodus neu erstellt. Die häufige Verwendung von ALTER-Anweisungen wirkt sich negativ auf die Leistung von Abfragen für die XML-Dokumente aus.  
  
 **Weitere Einschränkungen**  
  
-   Selektive XML-Indizes werden nicht in Abfragehinweisen unterstützt.  
  
-   Selektive XML-Indizes und sekundäre selektive XML-Indizes werden nicht vom Datenbankoptimierungsratgeber unterstützt.  
  
  
##  <a name="reltasks"></a> Verwandte Aufgaben  
  
|||  
|-|-|  
|**Task**|**Thema**|  
|Angeben der zu indizierenden Knotenpfade und optionalen Optimierungshinweise, wenn Sie einen selektiven XML-Index erstellen oder ändern.|[Angeben von Pfaden und Optimierungshinweisen für selektive XML-Indizes](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)|  
|Erstellen, Ändern oder Löschen eines selektiven XML-Indexes.|[Erstellen, Ändern und Löschen selektiver XML-Indizes](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)|  
|Erstellen, Ändern oder Löschen eines sekundären selektiven XML-Indexes.|[Erstellen, Ändern und Löschen sekundärer, selektiver XML-Indizes](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)|  
  
  
  
