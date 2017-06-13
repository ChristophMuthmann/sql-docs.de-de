---
title: "Indizes für speicheroptimierte Tabellen | Microsoft-Dokumentation"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b468f44444a9c6cc031ea892f44849db401e0ab7
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="indexes-for-memory-optimized-tables"></a>Indizes für speicheroptimierte Tabellen
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
Dieser Artikel beschreibt die Typen von Indizes, die für eine speicheroptimierte Tabelle zur Verfügung stehen. Der Artikel enthält Folgendes:  
  
- Kurze Codebeispiele zum Veranschaulichen der Transact-SQL-Syntax  
- Beschreibung, inwiefern speicheroptimierte Indizes sich von herkömmlichen datenträgerbasierten Indizes unterscheiden  
- Erläuterungen zu den Umständen, wann die einzelnen Typen von speicheroptimierten Indizes am besten geeignet sind  
  
  
*Hashindizes* werden ausführlicher in einem [eng verwandte Artikel](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)behandelt.  
  
  
*Columnstore* -Indizes werden in einem [anderen Artikel](~/relational-databases/indexes/columnstore-indexes-overview.md)behandelt.  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>A. Syntax für speicheroptimierte Indizes  
  
Jede CREATE TABLE-Anweisung für eine speicheroptimierte Tabelle muss zwischen 1 und 8 Klauseln zum Deklarieren von Indizes enthalten. Bei dem Index muss es sich um einen der folgenden handeln:  
  
- Hashindex  
- Nicht gruppierter Index (d.h. die interne Standardstruktur einer B-Struktur).  
  
  
Für eine Deklaration mit dem Standard DURABILITY = SCHEMA_AND_DATA muss die speicheroptimierte Tabelle einen Primärschlüssel haben. Die PRIMARY KEY NONCLUSTERED-Klausel in der folgenden CREATE TABLE-Anweisung erfüllt zwei Anforderungen:  
  
- Sie stellt einen Index bereit, um die Mindestanforderung von einem Index in der CREATE TABLE-Anweisung zu erfüllen.  
- Sie stellt den Primärschlüssel bereit, der für die SCHEMA_AND_DATA-Klausel erforderlich ist.  
  
  
  
    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    )  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
  
  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 Codebeispiel für Syntax  
  
Dieser Unterabschnitt enthält einen Transact-SQL-Codeblock, der die Syntax zum Erstellen von verschiedenen Indizes für eine speicheroptimierte Tabelle darstellt. Der Code veranschaulicht Folgendes:  
  
  
1. Erstellen Sie eine speicheroptimierte Tabelle.  
2. Verwenden Sie ALTER TABLE-Anweisungen, um zwei Indizes hinzuzufügen.  
3. Fügen Sie einige Zeilen Daten ein (INSERT).  
  
  
  
    DROP TABLE IF EXISTS SupportEvent;  
    go  
  
    CREATE TABLE SupportEvent  
    (  
      SupportEventId   int               not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  
  
      StartDateTime        datetime2     not null,  
      CustomerName         nvarchar(16)  not null,  
      SupportEngineerName  nvarchar(16)      null,  
      Priority             int               null,  
      Description          nvarchar(64)      null  
    )  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_AND_DATA);  
    go  
      
        --------------------  
      
    ALTER TABLE SupportEvent  
      ADD CONSTRAINT constraintUnique_SDT_CN  
        UNIQUE NONCLUSTERED (StartDateTime DESC, CustomerName);  
    go  
  
    ALTER TABLE SupportEvent  
      ADD INDEX idx_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 64);  -- Nonunique.  
    go  
      
        --------------------  
      
    INSERT INTO SupportEvent  
        (StartDateTime, CustomerName, SupportEngineerName, Priority, Description)  
      VALUES  
        ('2016-02-25 13:40:41:123', 'Abby', 'Zeke', 2, 'Anzeigeproblem.'     ),  
        ('2016-02-25 13:40:41:323', 'Ben' , null  , 1, 'Hilfe nicht gefunden.'    ),  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Schaltfläche ist grau.'      ),  
        ('2016-02-25 13:40:41:723', 'Dave', 'Zeke', 2, 'Ausblenden der Spalte nicht möglich.');  
    go  
  
  
  
## <a name="b-nature-of-memory-optimized-indexes"></a>B. Die Art von speicheroptimierten Indizes  
  
Für eine speicheroptimierte Tabelle wird jeder Index auch speicheroptimiert. Es gibt verschiedene Methoden, in denen sich ein Index für einen speicheroptimierten Index von einem herkömmlichen Index für eine datenträgerbasierte Tabelle unterscheidet.  
  
Jeder speicheroptimierte Index ist nur im aktiven Arbeitsspeicher vorhanden. Der Index wird nicht auf dem Datenträger dargestellt.  
  
- Speicheroptimierte Indizes werden neu erstellt, wenn die Datenbank wieder online geschaltet wird.  
  
  
Wenn eine SQL UPDATE-Anweisung Daten in einer speicheroptimierten Tabelle ändert, werden die entsprechende Änderungen an den Indizes nicht in das Protokoll geschrieben.  
  
  
Die Einträge in einem speicheroptimierten Index enthalten eine direkte Arbeitsspeicheradresse für die Zeile in der Tabelle.  
  
- Im Gegensatz dazu enthalten Einträge in einem herkömmlichen B-Strukturindex auf einem Datenträger einen Schlüsselwert, den das System zunächst verwenden muss, um die Arbeitsspeicheradresse für die zugeordnete Tabellenzeile zu suchen.  
  
  
Speicheroptimierte Indizes haben keine fixierten Seiten wie datenträgerbasierte Indizes.  
  
- Sie lassen nicht den herkömmlichen Fragmentierungstyp innerhalb einer Seite anwachsen, sodass sie keinen Füllfaktor haben.  
  
## <a name="c-duplicate-index-key-values"></a>C. Doppelte Indexschlüsselwerte

Doppelte Indexschlüsselwerte können die Leistung von Vorgängen an speicheroptimierten Tabellen beeinträchtigen. Eine große Anzahl von Duplikaten (z.B. 100+) macht das Verwalten eines Indexes ineffizient, da für die meisten Indexvorgänge doppelte Ketten durchlaufen werden müssen. Die Beeinträchtigung ist bei INSERT-, UPDATE- und DELETE-Vorgängen an speicheroptimierten Tabellen sichtbar. Dieses Problem ist sowohl aufgrund der niedrigeren Kosten pro Vorgang für Hashindizes als auch der Interferenz großer doppelter Ketten mit der Hashkollisionskette bei Hashindizes stärker sichtbar. Um die Duplizierung in einem Index zu reduzieren, verwenden Sie einen nicht gruppierten Index und fügen am Ende der Indexschlüssel zusätzliche Spalten (z.B. aus dem Primärschlüssel) zum Reduzieren der Anzahl von Duplikaten hinzu.

Nehmen wir als Beispiel eine Tabelle „Customers“ mit einem Primärschlüssel auf „CustomerId“ und einem Index auf der Spalte „CustomerCategoryID“. In der Regel wird es in einer bestimmten Kategorie viele Kunden und damit viele doppelte Werte für einen bestimmten Schlüssel im Index von „CustomerCategoryID“ geben. In diesem Szenario hat sich die Verwendung eines nicht gruppierten Indexes für („CustomerCategoryID“, „CustomerId“) bewährt. Dieser Index kann für Abfragen verwendet werden, die ein „CustomerCategoryID“ einbeziehendes Prädikat verwenden, er enthält keine Duplikate und verursacht darum keine Ineffizienz bei der Indexwartung.

Die folgende Abfrage zeigt die durchschnittliche Anzahl doppelter Indexschlüsselwerte für `CustomerCategoryID` in der Tabelle `Sales.Customers`in der Beispieldatenbank [WideWorldImporters](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx).

```Transact-SQL
    SELECT AVG(row_count) FROM
       (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

Um die durchschnittliche Anzahl der Indexschlüsselduplikate für Ihre eigene Tabelle und den Index zu evaluieren, ersetzen Sie `Sales.Customers` durch Ihren Tabellennamen und `CustomerCategoryID` durch die Liste der Indexschlüsselspalten.

## <a name="d-comparing-when-to-use-each-index-type"></a>D. Vergleichen des Verwendungszeitpunkts für jeden Indextyp  
  
  
Die Art Ihrer spezifischen Abfragen bestimmt, welche Art von Index die beste Wahl ist.  

Beim Implementieren speicheroptimierter Tabellen in einer vorhandenen Anwendung gilt die allgemeine Empfehlung, mit nicht gruppierten Indizes zu beginnen, da ihre Funktionen mehr den Funktionen herkömmlicher gruppierter und nicht gruppierter Indizes für datenträgerbasierte Tabellen ähneln. 
  
  
### <a name="d1-strengths-of-nonclustered-indexes"></a>D.1 Stärken nicht gruppierter Indizes  
  
  
Ein nicht gruppierter Index ist gegenüber einem Hashindex zu bevorzugen, wenn:  
  
- Abfragen über eine ORDER BY-Klausel für die indizierte Spalte verfügen.  
- Bei Abfragen nur die führenden Spalten eines mehrspaltigen Indexes getestet werden.  
- Abfragen die indizierte Spalte testen mithilfe einer WHERE-Klausel mit:  
  - einer Ungleichheit: *WHERE StatusCode != 'Done'*  
  - einem Wertbereich: *WHERE Quantity >= 100*  
  
  
In allen folgenden SELECT-Anweisungen wird ein nicht gruppierter Index gegenüber einem Hashindex bevorzugt:  
  
  
  
    SELECT col2 FROM TableA  
        WHERE StartDate > DateAdd(day, -7, GetUtcDate());  
      
    SELECT col3 FROM TableB  
        WHERE ActivityCode != 5;  
      
    SELECT StartDate, LastName  
        FROM TableC  
        ORDER BY StartDate;  
      
    SELECT IndexKeyColumn2  
        FROM TableD  
        WHERE IndexKeyColumn1 = 42;  
  
  
  
### <a name="d2-strengths-of-hash-indexes"></a>D.2 Stärken von Hashindizes  
  
  
Ein [Hashindex](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) ist gegenüber einem nicht gruppierten Index zu bevorzugen, wenn:  
  
- Abfragen die indizierten Spalten wie im Folgenden mithilfe einer WHERE-Klausel mit exakter Gleichheit auf allen Indexschlüsselspalten testen:  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="d3-summary-table-to-compare-index-strengths"></a>D.3 Zusammenfassende Tabelle für den Vergleich der Indexstärken  
  
  
Die folgende Tabelle enthält alle Vorgänge, die von den verschiedenen Indextypen unterstützt werden.  
  
  
| Vorgang | Speicheroptimiert, <br/> Hashindizes | Speicheroptimiert, <br/> Nicht gruppiert | Datenträgerbasiert, <br/> (nicht) gruppiert |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| Indexscan, alle Tabellenzeilen abrufen. | ja | ja | ja |  
| Indexsuche nach Gleichheitsprädikaten (=). | ja <br/> (Vollständiger Schlüssel ist erforderlich.) | ja  | ja |  
| Indexsuche nach Ungleichheits- und Bereichsprädikaten <br/> (>, <, <=, >=, BETWEEN). | Nein <br/> (Führt zu einem Indexscan.) | ja | ja |  
| Abrufen von Zeilen in einer Sortierreihenfolge, die der Indexdefinition entspricht. | Nein | ja | ja |  
| Abrufen von Zeilen in einer Sortierreihenfolge, die der umgekehrten Indexdefinition entspricht. | Nein | Nein | ja |  
  
  
In dieser Tabelle bedeutet „Ja“, dass der Index die Anforderung effizient bedienen kann, und „Nein“ bedeutet, dass der Index die Anforderung nicht effizient erfüllen kann.  

