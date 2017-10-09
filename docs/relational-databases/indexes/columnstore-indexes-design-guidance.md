---
title: Columnstore-Indizes - Designrichtlinien | Microsoft Dokumentation
ms.custom: 
ms.date: 01/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc3e22c2-3165-4ac9-87e3-bf27219c820f
caps.latest.revision: 16
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 22b8b23b9bbee402de83a5327ea7fb8b7ec734e2
ms.contentlocale: de-de
ms.lasthandoff: 09/30/2017

---
# <a name="columnstore-indexes---design-guidance"></a>Columnstore-Indizes - Designrichtlinien
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Allgemeine Empfehlungen für das Entwerfen von Columnstore-Indizes. Mit wenigen guten Entwurfsentscheidungen erzielen Sie die hohe Datenkomprimierung und Abfrageleistung, für die Columnstore-Indizes entworfen wurden. 

## <a name="prerequisites"></a>Erforderliche Komponenten

In diesem Artikel wird davon ausgegangen, dass Sie mit der Columnstore-Architektur und -Terminologie vertraut sind. Weitere Informationen finden Sie unter [Columnstore-Indizes – Übersicht](../../relational-databases/indexes/columnstore-indexes-overview.md) und [Columnstore-Indizes – Architektur](../../relational-databases/indexes/columnstore-indexes-architecture.md).

### <a name="know-your-data-requirements"></a>Informationen zur Datenanforderungen
Bevor Sie einen Columnstore-Index erstellen, sollten Sie Ihre Datenanforderungen so gut wie möglich kennen. Überlegen Sie sich beispielsweise die Antworten auf die folgenden Fragen:

- Wie groß ist Ihre Tabelle?
- Werden mit meinen Abfragen überwiegend Analysen durchgeführt, bei denen große Wertebereiche gescannt werden?  Columnstore-Indizes sind für das Scannen großer Bereiche besser geeignet als für das Suchen bestimmter Werte.
- Werden im Rahmen Ihrer Arbeitsauslastung zahlreiche Aktualisierungen und Löschvorgänge durchgeführt? Columnstore-Indizes eignen sich gut für stabile Daten. Bei Abfragen sollten weniger als 10 % der Zeilen aktualisiert und gelöscht werden.
- Verfügen Sie über Fakten- und Dimensionstabellen für ein Data Warehouse?
- Müssen Sie Analysen für eine Transaktionsarbeitsauslastung ausführen? In diesem Fall finden Sie Informationen zu operativen Echtzeitanalysen in den Designrichtlinien für Columnstore-Indizes.

Möglicherweise benötigen Sie keinen Columnstore-Index. Rowstore-Indizes mit Heaps oder gruppierten Indizes zeigen die beste Leistung bei Abfragen, die in den Daten suchen, nach einem bestimmten Wert suchen oder einen kleinen Bereich von Werten abfragen. Verwenden Sie Rowstore-Indizes für Transaktionsarbeitsauslastungen, da sie tendenziell eher Suchvorgänge in Tabellen als Scans umfangreicher Tabellen erfordern.  

## <a name="choose-the-best-columnstore-index-for-your-needs"></a>Auswählen des für Ihre Anforderungen am besten geeigneten Columnstore-Indexes

Ein Columnstore-Index ist ein gruppierter oder ein nicht gruppierter Index.  Ein gruppierter Columnstore-Index kann über einen oder mehrere nicht gruppierte BTree-Indizes verfügen. Sie können Columnstore-Indizes ganz einfach ausprobieren. Wenn Sie eine Tabelle als Columnstore-Index erstellen, können Sie diese problemlos wieder in eine Rowstore-Tabelle konvertieren, indem Sie den Columnstore-Index löschen. 

Im Folgenden finden Sie eine Übersicht über die Optionen und Empfehlungen. 

| Columnstore-Option | Empfehlungen für die Verwendung | Komprimierung |
| :----------------- | :------------------- | :---------- |
| Gruppierter Columnstore-Index | Verwendung für:<br></br>1) Herkömmliche Data Warehouse-Arbeitsauslastung mit einem Stern- oder Schneeflockenschema<br></br>2) Bei IoT-Arbeitsauslastungen (Internet der Dinge), bei denen mit minimalen Aktualisierungen und Löschvorgängen große Datenmengen eingefügt werden | Durchschnittlich zehnfach |
| Nicht gruppierte BTree-Indizes in einem gruppierten Columnstore-Index | Verwendungszweck:<br></br>    1) Durchsetzen von Primärschlüssel- und Fremdschlüsseleinschränkungen bei einem gruppierten Columnstore-Index<br></br>    2) Beschleunigen von Abfragen, die nach bestimmten Werten oder kleinen Wertebereichen suchen.<br></br>    3) Beschleunigen von Updates und Löschvorgängen von bestimmten Zeilen.| Durchschnittlich zehnfach plus zusätzlicher Speicher für die nicht gruppierten Indizes|
| Nicht gruppierter Columnstore-Index in einem datenträgerbasierten Heap- oder BTree-Index | Verwendung für: <br></br>1) Eine OLTP-Arbeitsauslastung mit einigen Analyseabfragen. Sie können für Analysen erstellte BTree-Indizes löschen und durch einen nicht gruppierten Columnstore-Index ersetzen.<br></br>2) Zahlreiche herkömmliche OLTP-Arbeitsauslastungen, die ETL-Vorgänge (Extract Transform and Load) durchführen, um Daten in ein separates Data Warehouse zu verschieben. Wenn Sie einen nicht gruppierten Columnstore-Index erstellen, benötigen Sie bei einigen OLTP-Tabellen weder ETL-Vorgänge noch ein separates Data Warehouse. | Ein nicht gruppierter Columnstore-Index ist ein zusätzlicher Index, der im Durchschnitt einen um 10% größeren Speicher erforderlich macht.|
| Columnstore-Index in einer In-Memory-Tabelle | Dieselben Empfehlungen gelten für den nicht gruppierten Columnstore-Index in einer datenträgerbasierten Tabelle, wobei es sich bei der Basistabelle jedoch um eine In-Memory-Tabelle handelt. | Der Columnstore-Index ist ein zusätzlicher Index.|


## <a name="use-a-clustered-columnstore-index-for-large-data-warehouse-tables"></a>Verwenden eines Columnstore-Indexes für umfangreiche Data Warehouse-Tabellen
Der gruppierte Columnstore-Index ist nicht nur ein Index, sondern er ist der primäre Tabellenspeicher. Er erreicht beim Data Warehousing eine hohe Datenkomprimierung sowie eine deutlich bessere Abfrageleistung bei umfangreichen Fakten- und Dimensionstabellen. Gruppierte Columnstore-Indizes eignen sich weniger gut für Transaktionsabfragen, jedoch besonders gut für Analyseabfragen, da bei Analyseabfragen in der Regel Operationen für große Wertebereiche durchgeführt werden und nicht nach bestimmten Werten gesucht wird. 

Überlegen Sie in folgenden Fällen, ob ein gruppierter Columnstore-Index sinnvoll ist:

- Jede Partition besteht aus mindestens einer Million Zeilen. Columnstore-Indizes enthalten in jeder Partition Zeilengruppen. Wenn die Tabelle zu klein ist, um eine Zeilengruppe in jeder Partition zu füllen, können Sie nicht von den Vorteilen der Columnstore-Komprimierung und Abfrageleistung profitieren.
- Abfragen führen in erster Linie Analysen für Wertebereiche durch. Bei einer Abfrage müssen beispielsweise alle Spaltenwerte gescannt werden, um den Durchschnittswert einer Spalte zu ermitteln. Anschließend werden die Werte durch Summieren gesammelt, um den Durchschnittswert zu ermitteln.
- Die meisten Einfügevorgänge werden für umfangreiche Datenvolumen mit minimalen Aktualisierungen und Löschvorgängen durchgeführt. Bei vielen Arbeitsauslastungen wie beim Internet der Dinge (Internet of Things, IOT) werden mit minimalen Aktualisierungen und Löschvorgängen große Datenvolumen eingefügt. Diese Arbeitsauslastungen können von der besseren Komprimierung und Abfrageleistung profitieren, die sich aus der Verwendung eines gruppierten Columnstore-Indexes ergibt.

Verwenden Sie in den folgenden Fällen keinen gruppierten Columnstore-Index:

* Die Tabelle erfordert die Datentypen varchar(max), nvarchar(max) oder varbinary(max). Oder entwerfen Sie den Columnstore-Index so, dass er diese Spalten nicht enthält.
* Die Tabellendaten sind nicht dauerhaft. Überlegen Sie, ob die Verwendung einer Heap-Tabelle oder einer temporären Tabelle sinnvoll ist, wenn Sie die Daten schnell speichern und löschen müssen.
* Die Tabelle hat weniger als einer Million Zeilen pro Partition. 
* Mehr als 10 % der Vorgänge in der Tabelle sind Aktualisierungs- und Löschvorgänge. Eine große Anzahl von Aktualisierungs- und Löschvorgängen führt zu einer Fragmentierung. Die Fragmentierung wirkt sich auf die Komprimierungsraten und die Abfrageleistung aus, bis Sie eine Reorganisation durchführen, bei der alle Daten in den Columnstore gezwungen werden und eine Defragmentierung durchgeführt wird. Weitere Informationen finden Sie unter [Minimieren der Indexfragmentierung in Columnstore-Indizes](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/).

Weitere Informationen finden Sie unter [Columnstore-Indizes - Data Warehousing](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md).

## <a name="add-btree-nonclustered-indexes-for-efficient-table-seeks"></a>Hinzufügen eines nicht gruppierten BTree-Indexes für eine effiziente Tabellensuche

Ab SQL Server 2016 können Sie nicht gruppierte BTree-Indizes als sekundäre Indizes für einen gruppierten Columnstore-Index erstellen. Der nicht gruppierte BTree-Index wird bei Änderungen am Columnstore-Index aktualisiert. Diese leistungsstarke Funktion können Sie sich zunutze machen. 

Mithilfe des sekundären BTree-Indexes können Sie effizient nach bestimmten Zeilen suchen, ohne alle Zeilen scannen zu müssen.  Auch weitere Optionen werden dadurch verfügbar. Beispielsweise können Sie eine Primär- oder Fremdschlüsseleinschränkung durchsetzen, indem Sie eine UNIQUE-Bedingung auf den BTree-Index anwenden. Da ein nicht eindeutiger Wert nicht in den BTree-Index eingefügt werden kann, kann SQL Server den Wert nicht in den Columnstore einfügen. 

Einen BTree-Index sollten Sie in folgenden Fällen in einem Columnstore-Index verwenden:
* Ausführen von Abfragen, die nach bestimmten Werten oder kleinen Wertebereichen suchen.
* Durchsetzen einer Einschränkung wie etwa einer Primärschlüssel- oder Fremdschlüsseleinschränkung.
* Effizientes Durchführen von Aktualisierungs- und Löschvorgängen. Mit dem BTree-Index können die Zeilen für Aktualisierungen und Löschvorgänge schnell gefunden werden, ohne die gesamte Tabelle oder Partition einer Tabelle scannen zu müssen.
* Ihnen steht zusätzlicher Speicherplatz zum Speichern des BTree-Indexes zur Verfügung.

## <a name="use-a-nonclustered-columnstore-index-for-real-time-analytics"></a>Verwendung eines nicht gruppierten Columnstore-Indexes für die Echtzeitanalyse

Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] können Sie einen nicht gruppierten Columnstore-Index in einer datenträgerbasierten Rowstore-Tabelle oder in einer In-Memory-Tabelle verwenden. Dadurch ist es möglich, die Analyse für eine Transaktionstabelle in Echtzeit auszuführen. Transaktionen werden in der zugrunde liegenden Tabelle ausgeführt. Eine Analyse können Sie dagegen für den Columnstore-Index ausführen. Da beide Indizes von einer Tabelle verwaltet werden, sind Änderungen sowohl für Rowstore- als auch für Columnstore-Indizes in Echtzeit verfügbar.

Da mit einem Columnstore-Index im Vergleich zu einem Rowstore-Index eine zehnfach höhere Datenkomprimierung erzielt werden kann, ist nur wenig zusätzlicher Speicherplatz erforderlich. Während die komprimierte Rowstore-Tabelle beispielsweise 20 GB belegt, benötigt der Columnstore-Index nur 2 GB zusätzlich. Wie viel zusätzlicher Speicher erforderlich ist, hängt auch von der Anzahl der Spalten im nicht gruppierten Columnstore-Index ab. 

 Überlegen Sie in folgenden Fällen, ob ein nicht gruppierter Columnstore-Index sinnvoll ist:

* Ausführen von Analysen für eine Rowstore-Transaktionstabelle in Echtzeit Sie können vorhandene BTree-Indizes ersetzen, die für die Analyse eines nicht gruppierten Columnstore-Indexes erstellt wurden. 
  
*   Ein separates Data Warehouse ist nicht erforderlich. Bisher haben Unternehmen Transaktionen für eine Rowstore-Tabelle ausgeführt und die Daten zur Analyse in ein separates Data Warehouse geladen. Bei vielen Arbeitsauslastungen sind der Ladevorgang und das separate Data Warehouse nicht mehr erforderlich, wenn ein nicht gruppierter Columnstore-Index für Transaktionstabellen erstellt wird.

  SQL Server 2016 bietet verschiedene Strategien, damit dieses Szenario leistungsfähig wird. Es lässt sich sehr einfach ausprobieren, da Sie einen nicht gruppierten Columnstore-Index ohne Änderungen an der OLTP-Anwendung aktivieren können. 

Sie können die Analyse für eine lesbare sekundäre Datenbank ausführen, um zusätzliche Verarbeitungsressourcen hinzuzufügen. Bei Verwendung einer lesbaren sekundären Datenbank werden die Verarbeitung der Transaktionsarbeitsauslastung und die der Analysearbeitsauslastung voneinander getrennt. 

Weitere Informationen finden Sie unter [Erste Schritte mit Columnstore-Indizes für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).

Weitere Informationen zur Auswahl des am besten geeigneten Columnstore-Indexes finden Sie im Blog [Which columnstore index is right for my workload? (Welcher Columnstore-Index eignet sich für meine Arbeitsauslastung)](https://blogs.msdn.microsoft.com/sql_server_team/columnstore-index-which-columnstore-index-is-right-for-my-workload) von Sunil Agarwal.

## <a name="use-table-partitions-for-data-management-and-query-performance"></a>Verwenden von Tabellenpartitionen für eine bessere Datenverwaltung und Abfrageleistung
Columnstore-Indizes unterstützen die Partitionierung, die eine gute Möglichkeit zum Verwalten und Archivieren von Daten bietet. Durch die Partitionierung wird die Abfrageleistung verbessert, da Vorgänge auf eine oder mehrere Partitionen begrenzt werden.

### <a name="use-partitions-to-make-the-data-easier-to-manage"></a>Verwenden von Partitionen zur einfacheren Verwaltung von Daten
Bei umfangreichen Tabelle lassen sich Datenbereiche praktisch nur mithilfe von Partitionen verwalten. Die Vorteile von Partitionen für Rowstore-Tabellen gelten auch für Columnstore-Indizes. 

Sowohl in Rowstore- als auch in Columnstore-Tabellen werden Partitionen in folgenden Fällen verwendet:

- Steuern der Größe von inkrementellen Sicherungen. Sie können Partitionen sichern, um Dateigruppen zu trennen und sie anschließend als schreibgeschützt zu kennzeichnen. Auf diese Weise werden die schreibgeschützten Dateigruppen bei zukünftigen Sicherungen übersprungen. 
- Sparen bei Speicherkosten durch Verschieben älterer Partitionen in kostengünstigeren Speicher. Durch Partitionswechsel können Sie beispielsweise eine Partition an einen kostengünstigeren Speicherort verschieben.
- Effizientes Durchführen von Vorgängen durch Begrenzen der Vorgänge auf eine Partition. Sie können beispielsweise nur die fragmentierten Partitionen für die Indexwartung verwenden.

Zudem erreichen Sie mit der Partitionierung bei einem Columnstore-Index Folgendes:

* Sparen Sie weitere 30 % Speicherkosten. Ältere Partitionen können Sie mit den COLUMNSTORE_ARCHIVE-Komprimierungsoptionen komprimieren. Die Daten werden aus Gründen der Abfrageleistung langsamer. Das ist akzeptabel, wenn die Partition unregelmäßig abgefragt wird.

### <a name="use-partitions-to-improve-query-performance"></a>Verwenden von Partitionen zum Steigern der Abfrageleistung

Durch die Verwendung von Partitionen können Sie für Ihre Abfragen festlegen, dass nur bestimmte Partitionen gescannt werden. Dadurch wird die Anzahl der Zeilen begrenzt, die gescannt werden müssen. Wenn der Index beispielsweise nach Jahr partitioniert ist und mit der Abfrage Daten aus dem letzten Jahr analysiert werden, müssen nur die Daten in einer Partition gescannt werden. 

### <a name="use-fewer-partitions-for-a-columnstore-index"></a>Verwenden von weniger Partitionen für einen Columnstore-Index

Ein Columnstore-Index zeigt die beste Leistung, wenn Sie im Vergleich zu einem Rowstore-Index weniger Partitionen verwenden, außer Sie verfügen über eine ausreichend große Datengröße. Wenn die Partitionen nicht jeweils mindestens eine Million Zeilen aufweisen, gelangen die meisten Zeilen in den Deltastore. Dort profitieren sie nicht von der Leistungssteigerung der Columnstore-Komprimierung. Wenn Sie beispielsweise eine Million Zeilen in eine Tabelle mit 10 Partitionen laden und jede Partition erhält 100.000 Zeilen, gelangen alle Zeilen in Delta-Zeilengruppen. 

Beispiel:
* Laden Sie 1.000.000 Zeilen in eine Partition oder in eine nicht partitionierte Tabelle. Daraufhin erhalten Sie eine komprimierte Zeilengruppe mit 1.000.000 Zeilen. Dies ist für eine starke Datenkomprimierung und eine optimale Abfrageleistung nützlich.
* Laden Sie 1.000.000 Zeilen gleichmäßig in 10 Partitionen. Jede Partition erhält 100.000 Zeilen, also weniger als die Mindestanzahl für die Columnstore-Komprimierung. Daher kann der Columnstore-Index 10 Delta-Zeilengruppen mit je 100.000 Zeilen aufweisen. Es gibt Möglichkeiten, ein Ablegen der Delta-Zeilengruppen im Columnstore durchzusetzen. Wenn dies jedoch die einzigen Zeilen im Columnstore-Index sind, sind die komprimierten Zeilengruppen zu klein für eine optimale Komprimierung und Abfrageleistung.

Weitere Informationen zur Partitionierung finden Sie im Blogbeitrag [Should I partition my columnstore index? (Sollte ich meinen Columnstore-Index partitionieren)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-should-i-partition-my-columnstore-index/) von Sunil Agarwal.

## <a name="choose-the-appropriate-data-compression-method"></a>Auswählen der geeigneten Datenkomprimierungsmethode
Der Columnstore-Index biete zwei Möglichkeiten für die Datenkomprimierung: die Columnstore-Komprimierung und die Archivkomprimierung. Sie können eine Komprimierungsoption wählen, wenn Sie den Index erstellen oder die Einstellung später mit [ALTER INDEX anpassen. REBUILD](../../t-sql/statements/alter-index-transact-sql.md) ändern.

### <a name="use-columnstore-compression-for-best-query-performance"></a>Verwenden der Columnstore-Komprimierung für eine optimale Abfrageleistung
Mit der Columnstore-Komprimierung werden im Vergleich zu Rowstore-Indizes in der Regel zehnfach höhere Komprimierungsraten erzielt. Sie ist die Standardkomprimierungsmethode für Columnstore-Indizes und ermöglicht eine hohe Abfrageleistung. 

### <a name="use-archive-compression-for-best-data-compression"></a>Verwenden der Archivkomprimierung für eine optimale Datenkomprimierung
Die Archivkomprimierung ist in Fällen, in denen die Abfrageleistung eine untergeordnete Rolle spielt, für eine maximale Komprimierung vorgesehen. Sie erzielt im Vergleich zur Columnstore-Komprimierung höhere Datenkomprimierungsraten, hat jedoch ihren Preis. Die Komprimierung und Dekomprimierung der Daten dauert länger. Daher eignet sich diese Methode nicht für eine hohe Abfrageleistung. 

## <a name="use-optimizations-when-you-convert-a-rowstore-table-to-a-columnstore-index"></a>Verwenden von Optimierungen beim Konvertieren einer Rowstore-Tabelle in einen Columnstore-Index

Wenn sich Ihre Daten bereits in einer Rowstore-Tabelle befinden, können Sie die Tabelle mit [CREATE COLUMNSTORE INDEX](../../t-sql/statements/create-columnstore-index-transact-sql.md) in einen gruppierten Columnstore-Index konvertieren. Es gibt einige Optimierungen, mit deren Hilfe sich die Abfrageleistung nach der Konvertierung der Tabelle verbessert.

### <a name="use-maxdop-to-improve-rowgroup-quality"></a>Verwenden von MAXDOP zur Verbesserung der Zeilengruppenqualität
Sie können die maximale Anzahl von Prozessoren für die Konvertierung eines Heap-Indexes oder eines gruppierten BTree-Indexes in einen Columnstore-Index konfigurieren. Verwenden Sie für die Konfiguration der Prozessoren die Option für den maximalen Grad an Parallelität (Maximum Degree of Parallelism, MAXDOP). 

Wenn Sie über große Datenmengen verfügen, ist MAXDOP 1 voraussichtlich zu langsam.  Erhöhen Sie in diesem Fall auf MAXDOP 4. Wenn dabei einige Zeilengruppen entstehen, die keine optimale Zeilenzahl aufweisen, können Sie [ALTER INDEX REORG](../../t-sql/statements/alter-index-transact-sql.md) ausführen, um sie im Hintergrund zusammenzuführen.

### <a name="keep-the-sorted-order-of-a-btree-index"></a>Beibehalten der Sortierreihenfolge eines BTree-Indexes
Da der BTree-Index Zeilen bereits in sortierter Folge speichert, können Sie die Abfrageleistung steigern, indem Sie diese Reihenfolge beim Komprimieren der Zeilen im Columnstore-Index beibehalten.

Im Columnstore-Index werden die Daten nicht sortiert. Es werden jedoch Metadaten zum Überwachen der Mindest- und Höchstwerte der einzelnen Spaltensegmente in den jeweiligen Zeilengruppen verwendet.  Beim Scannen eines Wertebereichs kann schnell berechnet werden, wenn eine Zeilengruppe übersprungen werden kann. Wenn die Daten sortiert werden, können mehr Zeilengruppen übersprungen werden. 

So können Sie die Sortierreihenfolge bei der Konvertierung beibehalten:
* Verwenden Sie [CREATE COLUMNSTORE INDEX](../../t-sql/statements/create-columnstore-index-transact-sql.md) mit der DROP_EXISTING-Klausel. Dadurch wird auch der Name des Indexes beibehalten. Wenn Sie Skripts verwenden, in denen der Name des Rowstore-Indexes enthalten ist, müssen Sie diese nicht aktualisieren. 

    In diesem Beispiel wird ein gruppierter Rowstore-Index in einer Tabelle mit dem Namen ```MyFactTable``` in einen gruppierten Columnstore-Index konvertiert. Der Indexname ```ClusteredIndex_d473567f7ea04d7aafcac5364c241e09``` bleibt unverändert.

    ```sql
    CREATE CLUSTERED COLUMNSTORE INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
    ON MyFactTable  
    WITH (DROP_EXISTING = ON);  
    ```

## <a name="related-tasks"></a>Verwandte Aufgaben  
Hierbei handelt es sich um Aufgaben zum Erstellen und Verwalten von Columnstore-Indizes. 
  
|Task|Referenzthemen|Hinweise|  
|----------|----------------------|-----------|  
|Erstellen einer Tabelle als Columnstore.|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]können Sie die Tabelle als gruppierten Columnstore-Index erstellen. Sie brauchen nicht zuerst eine Rowstore-Tabelle zu erstellen, die Sie anschließend in Columnstore konvertieren.|  
|Erstellen Sie eine In-Memory-Tabelle mit einem Columnstore-Index.|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]können Sie eine speicheroptimierte Tabelle mit einem Columnstore-Index erstellen. Der Columnstore-Index kann auch nach dem Erstellen der Tabelle mit der ALTER TABLE ADD INDEX-Syntax hinzugefügt werden.|  
|Konvertieren einer Rowstore-Tabelle in eine Columnstore-Tabelle.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Konvertieren Sie einen vorhandenen Heap oder eine binäre Struktur in einen Columnstore. Aus den Beispielen können Sie ersehen, wie vorhandene Indizes und der Name des Index beim Durchführen der Konvertierung behandelt werden.|  
|Konvertieren einer Columnstore-Tabelle in einen Rowstore.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Normalerweise ist das nicht erforderlich, aber es kann vorkommen, dass Sie diese Konvertierung durchführen müssen. Aus den Beispielen ist zu ersehen, wie ein Columnstore in einen Heap oder einen gruppierten Index konvertiert werden kann.|  
|Erstellen eines Columnstore-Index für eine Rowstore-Tabelle.|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Eine Rowstore-Tabelle kann über einen Columnstore-Index verfügen.  Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]kann der Columnstore-Index eine Filterbedingung aufweisen. In den Beispielen wird die grundlegende Syntax verwendet.|  
|Erstellen leistungsfähiger Indizes für Betriebsanalysen.|[Erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)|Beschreibt, wie sich ergänzende Columnstore- und B-Strukturindizes erstellt werden, sodass OLTP-Abfragen die B-Strukturindizes und Analyseabfragen die Columnstore-Indizes verwenden.|  
|Erstellen leistungsfähiger Columnstore-Indizes für Data Warehousing|[Columnstore-Indizes - Data Warehousing](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)|Beschreibt, wie B-Strukturindizes für Columnstore-Tabellen verwendet werden können, um leistungsstarke Data Warehousing-Abfragen zu erstellen.|  
|Verwenden eines B-Strukturindex zum Durchsetzen einer Primärschlüsseleinschränkung für einen Columnstore-Index.|[Columnstore-Indizes - Data Warehousing](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)|Zeigt, wie B-Struktur- und Columnstore-Indizes kombiniert werden können, um Primärschlüsseleinschränkungen für den Columnstore-Indizes durchzusetzen.|  
|Löschen eines Columnstore-Index|[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)|Beim Löschen eines Columnstore-Index wird die standardmäßige DROP INDEX-Syntax verwendet, die auch für B-Strukturindizes verwendet wird. Beim Löschen eines gruppierten Columnstore-Index wird die Columnstore-Tabelle in einen Heap konvertiert.|  
|Löschen einer Zeile aus einem Columnstore-Index|[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|Verwenden Sie [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) zum Löschen einer Zeile.<br /><br /> **columnstore** -Zeile: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] markiert die Zeile als logisch gelöscht, der physische Speicherplatz für die Zeile wird jedoch erst wieder freigegeben, wenn der Index neu erstellt wird.<br /><br /> **deltastore** -Zeile: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] löscht die Zeile logisch und physisch.|  
|Aktualisieren einer Zeile im columnstore-Index|[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|Verwenden Sie [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) , um eine Zeile zu aktualisieren.<br /><br /> **columnstore** -Zeile:  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] markiert die Zeile als logisch gelöscht und fügt dann die aktualisierte Zeile in den Deltastore ein.<br /><br /> **deltastore** -Zeile: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert die Zeile im Deltastore.|  
|Durchsetzen, dass alle Zeilen im Deltastore in den Columnstore wechseln.|[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) ... REBUILD<br /><br /> [Columnstore-Indizes für Defragmentierung](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)|ALTER INDEX mit der REBUILD-Option erzwingt die Übernahme aller Zeilen in den Columnstore.|  
|Defragmentieren eines Columnstore-Index|[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)|ALTER INDEX … REORGANIZE defragmentiert-Columnstore-Indizes online.|  
|Zusammenführen von Tabellen mit Columnstore-Indizes.|[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)|


## <a name="next-steps"></a>Nächste Schritte
So erstellen Sie einen leeren Columnstore-Index für:

* SQL Server, verwenden Sie [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)
* SQL Database, verwenden Sie [CREATE TABLE in der Azure SQL-Datenbank](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1)
* SQL Data Warehouse, verwenden Sie [CREATE TABLE (Azure SQL Data Warehouse)](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)

Zum Konvertieren eines Heap- oder BTree-Indexes einer vorhandenen Rowstore-Tabelle in einen gruppierten Columnstore-Index oder zum Erstellen eines nicht gruppierten Columnstore-Indexes verwenden Sie folgende Anweisung:

* [CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)







  


