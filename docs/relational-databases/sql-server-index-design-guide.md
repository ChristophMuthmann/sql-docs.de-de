---
title: Handbuch zum SQL Server Indexentwurf | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index design guide
- guide, index design
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
caps.latest.revision: 3
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b56ebb9f804f575c6f1f83cb4e9e192bd4f10e15
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-index-design-guide"></a>Handbuch zum SQL Server Indexentwurf
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

Schlecht entworfene oder fehlende Indizes sind die Hauptquellen für Engpässe der Datenbankanwendung. Ein effizienter Indexentwurf ist zum Erzielen einer guten Datenbank- und Anwendungsleistung unabdinglich. Die in diesem Handbuch zum SQL Server Indexentwurf enthaltenen Informationen und Best Practices unterstützen Sie beim Entwerfen effizienter Indizes, die den Anforderungen Ihrer Anwendung entsprechen.  
    
In diesem Handbuch wird davon ausgegangen, dass der Leser grundsätzlich mit den in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]verfügbaren Indextypen vertraut ist. Eine allgemeine Beschreibung zu Indextypen finden Sie unter [Indextypen](http://msdn.microsoft.com/library/ms175049.aspx).  
  
  
##  <a name="Basics"></a> Grundlagen des Indexentwurfs  
 Ein Index ist eine Struktur auf dem Datenträger, die einer Tabelle oder einer Sicht zugeordnet ist und durch die das Abrufen von Zeilen aus der Tabelle oder Sicht beschleunigt wird. Ein Index enthält Schlüssel, die aus einer oder mehreren Spalten in der Tabelle oder Sicht erstellt werden. Diese Schlüssel werden in einer Struktur (B-Struktur) gespeichert, die es SQL Server ermöglicht, die den Schlüsselwerten zugeordneten Zeilen schnell und effizient zu finden.  
  
 Das Auswählen der richtigen Indizes für eine Datenbank und ihre Arbeitsauslastung ist ein komplexer Vorgang, bei dem ein ausgewogenes Verhältnis zwischen gewünschter Abfragegeschwindigkeit und vertretbaren Updatekosten erzielt werden muss. Schmale Indizes (Indizes mit wenigen Spalten im Indexschlüssel) erfordern weniger Speicherplatz und Wartungsaufwand. Breite Indizes decken jedoch eine größere Anzahl an Abfragen ab. Möglicherweise müssen Sie mit verschiedenen Entwürfen experimentieren, bevor Sie den effizientesten Index ermitteln. Indizes können ohne Auswirkungen auf das Datenbankschema oder den Anwendungsentwurf hinzugefügt, geändert und gelöscht werden. Daher sollten Sie in jedem Fall mit verschiedenen Indizes experimentieren.  
  
 Der Abfrageoptimierer von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wählt in der Mehrzahl der Fälle zuverlässig den effektivsten Index aus. Indexentwurfsstrategie sollte sein, dem Abfrageoptimierer eine Vielzahl von Indizes zur Auswahl bereitzustellen und sich darauf zu verlassen, dass dieser die richtige Entscheidung trifft. Auf diese Weise wird die Analysezeit verkürzt und ein gutes Leistungsverhalten in vielen unterschiedlichen Situationen erzielt. Wenn Sie anzeigen möchten, welche Indizes der Abfrageoptimierer für eine bestimmte Abfrage verwendet, wählen Sie in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]die Option **Tatsächlichen Ausführungsplan einschließen** aus dem Menü **Abfrage**aus.  
  
 Setzen Sie Indexverwendung aber nicht stets mit gutem Leistungsverhalten bzw. gute Leistung mit effizienter Indexverwendung gleich. Würde durch die Verwendung eines Indexes in jedem Fall die beste Leistung erzielt, so wäre die Arbeit des Abfrageoptimierers sehr einfach. Tatsächlich kann die Auswahl eines falschen Indexes eine Leistung bewirken, die nicht optimal ist. Daher besteht die Aufgabe des Abfrageoptimierers darin, einen Index oder eine Kombination aus Indizes nur dann auszuwählen, wenn die Leistung verbessert wird, und den indizierten Abruf zu vermeiden, wenn die Leistung negativ beeinflusst wird.  
  
### <a name="index-design-tasks"></a>Aufgaben beim Indexentwurf  
 Die folgenden Aufgaben fassen die empfohlene Strategie beim Entwerfen von Indizes zusammen:  
  
1.  Verstehen der Merkmale der Datenbank selbst. Wird die Datenbank z. B. für die Onlinetransaktionsverarbeitung (OLTP) mit häufigen Datenänderungen oder als Entscheidungsunterstützungssystem (EUS) bzw. als Data Warehousing-Datenbank (OLAP-Datenbank) verwendet, die hauptsächlich schreibgeschützte Daten enthält und sehr große Datasets schnell verarbeiten muss? In [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]ist der *speicheroptimierte xVelocity-columnstore* -Index besonders gut für typische Data Warehousing-Datasets geeignet. Columnstore-Indizes verbessern die Benutzererfahrung im Bereich Data Warehousing, da sie die schnellere Ausführung allgemeiner Data Warehousing-Abfragen, wie Filter-, Aggregierungs-, Gruppierungs- und Sternjoinabfragen ermöglichen. Weitere Informationen finden Sie unter [Columnstore-Indizes](~/relational-databases/indexes/columnstore-indexes-overview.md).  
  
2.  Verstehen der Merkmale der am häufigsten verwendeten Abfragen. Wenn Sie z. B. wissen, dass eine häufig verwendete Abfrage zwei oder mehr Tabellen verknüpft, unterstützt Sie dieses Wissen beim Ermitteln der zu verwendenden effizientesten Indextypen.  
  
3.  Verstehen der Merkmale der in den Abfragen verwendeten Spalten. Ein Index eignet sich z. B. ideal für Spalten, die einen ganzzahligen Datentyp besitzen und außerdem eindeutige oder Nicht-NULL-Spalten sind. Für Spalten, die klar definierte Teilmengen von Daten enthalten, können Sie in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] und höheren Versionen einen gefilterten Index verwenden. Weitere Informationen finden Sie unter [Richtlinien für den Entwurf gefilterter Indizes](#Filtered) in diesem Handbuch.  
  
4.  Ermitteln, welche Indexoptionen die Leistung steigern können, wenn der Index erstellt oder gewartet wird. Für das Erstellen eines gruppierten Indexes für eine vorhandene Tabelle ist z. B. die ONLINE-Indexoption vorteilhaft. Die ONLINE-Option ermöglicht, dass gleichzeitige Aktivitäten für die zugrunde liegenden Daten fortgesetzt werden können, während der Index erstellt oder neu erstellt wird. Weitere Informationen finden Sie unter [Festlegen von Indexoptionen](../relational-databases/indexes/set-index-options.md).  
  
5.  Angeben des optimalen Speicherorts für den Index. Ein nicht gruppierter Index kann in derselben Dateigruppe wie die zugrunde liegende Tabelle oder in einer anderen Dateigruppe gespeichert werden. Der Speicherort von Indizes kann die Abfrageleistung durch Optimieren der Datenträger-E/A-Leistung verbessern. Wenn Sie z. B. einen nicht gruppierten Index in einer Dateigruppe speichern, die sich auf einem anderen Datenträger als die Tabellendateigruppe befindet, kann dies die Leistung verbessern, weil mehrere Datenträger gleichzeitig gelesen werden können.  
  
     Alternativ können gruppierte und nicht gruppierte Indizes ein dateigruppenübergreifendes Partitionsschema verwenden. Durch die Partitionierung sind große Tabellen oder Indizes leichter zu verwalten, denn Sie können dadurch schnell und effizient auf Datenteilmengen zugreifen und sie verwalten, während die Integrität der gesamten Sammlung erhalten bleibt. Weitere Informationen finden Sie unter [Partitioned Tables and Indexes](../relational-databases/partitions/partitioned-tables-and-indexes.md). Wenn Sie Partitionierung in Erwägung ziehen, müssen Sie festlegen, ob der Index ausgerichtet sein soll, d. h., ob er weitgehend wie die Tabelle oder unabhängig davon partitioniert werden soll.  
  
##  <a name="General_Design"></a> Allgemeine Richtlinien zum Indexentwurf  
 Erfahrene Datenbankadministratoren sind in der Lage, einen geeigneten Satz an Indizes zu entwerfen. Es handelt sich jedoch selbst bei gemäßigt komplexen Datenbanken und Arbeitsauslastungen um eine sehr komplexe, zeitintensive und fehleranfällige Aufgabe. Das Verständnis der Merkmale der Datenbank, Abfragen und Datenspalten kann Sie beim Entwerfen optimaler Indizes unterstützen.  
  
### <a name="database-considerations"></a>Überlegungen zu Datenbanken  
 Beachten Sie beim Entwerfen eines Indexes die folgenden Datenbankrichtlinien:  
  
-   Eine große Anzahl an Indizes für eine Tabelle beeinträchtigt die Leistung von INSERT-, UPDATE-, DELETE- und MERGE-Anweisungen, da alle Indizes entsprechend angepasst werden müssen, sobald Daten in der Tabelle geändert werden. Beispiel: Wenn eine Spalte in mehreren Indizes verwendet wird und Sie eine UPDATE-Anweisung ausführen, durch die Daten in dieser Spalte geändert werden, müssen alle Indizes, die diese Spalte enthalten, sowie die Spalte in der zugrunde liegenden Basistabelle (Heap oder gruppierter Index) ebenfalls aktualisiert werden.  
  
    -   Vermeiden Sie die zu starke Indizierung häufig aktualisierter Tabellen, und halten Sie die Indizes schmal, d. h., verwenden Sie so wenig Spalten wie möglich.  
  
    -   Verwenden Sie viele Indizes, um die Abfrageleistung für Tabellen zu verbessern, die geringe Updateanforderungen und große Datenmengen aufweisen. Eine große Anzahl an Indizes kann die Leistung von Abfragen steigern, durch die keine Daten geändert werden (z. B. SELECT-Anweisungen), da der Abfrageoptimierer aus einer größeren Anzahl an Indizes auswählen kann, um die beste Methode für den schnellstmöglichen Zugriff zu ermitteln.  
  
-   Das Indizieren kleiner Tabellen ist häufig nicht die optimale Methode, da der Abfrageoptimierer in diesem Fall mitunter mehr Zeit benötigt, um die Daten über einen Index zu suchen, als für die Durchführung eines einfachen Tabellenscans erforderlich wäre. Aus diesem Grund werden Indizes für kleine Tabellen möglicherweise niemals verwendet, müssen jedoch trotzdem verwaltet werden, wenn sich Daten in der Tabelle ändern.  
  
-   Indizes für Sichten können zu erheblichen Leistungsverbesserungen führen, wenn die Sicht Aggregationen, Tabellenjoins oder eine Kombination aus Aggregationen und Joins enthält. Es ist nicht erforderlich, dass in der Abfrage explizit auf die jeweilige Sicht verwiesen wird, damit der Abfrageoptimierer die Sicht verwendet.  
  
-   Verwenden Sie den Datenbankoptimierungsratgeber, um die Datenbank zu analysieren und Indexempfehlungen zu erhalten. Weitere Informationen finden Sie unter [Database Engine Tuning Advisor](../relational-databases/performance/database-engine-tuning-advisor.md).  
  
### <a name="query-considerations"></a>Überlegungen zu Abfragen  
 Beachten Sie beim Entwerfen eines Indexes die folgenden Abfragerichtlinien:  
  
-   Erstellen Sie nicht gruppierte Indizes für die Spalten, die häufig in Prädikaten und Joinbedingungen in Abfragen verwendet werden. Sie sollten jedoch keine unnötigen Spalten hinzufügen. Wenn Sie zu viele Indexspalten hinzufügen, kann sich dies negativ auf den Speicherplatz und die Indexverwaltungsleistung auswirken.  
  
-   Abdeckende Indizes können die Abfrageleistung steigern, weil alle Daten im Index selbst enthalten sind, die die Anforderungen der Abfrage erfüllen. Auf diese Weise muss nur auf die Indexseiten und nicht auf die Datenseiten der Tabelle oder des gruppierten Indexes verwiesen werden, um die abgefragten Daten abzurufen, wodurch der Umfang der E/A-Operationen des Datenträgers verringert wird. Eine Abfrage der Spalten **a** und **b** für eine Tabelle, die einen zusammengesetzten Index besitzt, der für die Spalten **a**, **b**und **c** erstellt wurde, kann die angegebenen Daten ausschließlich aus dem Index abrufen.  
  
-   Schreiben Sie Abfragen, die möglichst viele Zeilen in einer einzigen Anweisung einfügen oder ändern, anstatt mehrere Abfragen zum Aktualisieren der gleichen Zeilen zu verwenden. Wenn nur eine Anweisung verwendet wird, kann der Index optimal verwaltet werden.  
  
-   Werten Sie den Abfragetyp sowie die Art der Verwendung von Spalten in der Abfrage aus. Eine Spalte, die in einem Abfragetyp für genaue Übereinstimmung verwendet wird, ist z. B. ein guter Kandidat für einen nicht gruppierten oder gruppierten Index.
  
### <a name="column-considerations"></a>Überlegungen zu Spalten  
 Beachten Sie beim Entwerfen eines Indexes die folgenden Spaltenrichtlinien:  
  
-   Wählen Sie für gruppierte Indizes einen kurzen Indexschlüssel aus. Gruppierte Indizes bieten darüber hinaus den Vorteil, dass sie für eindeutige oder Nicht-NULL-Spalten erstellt werden.  
  
-   Die Datentypen **ntext**, **text**, **image**, **varchar(max)**, **nvarchar(max)**und **varbinary(max)** können nicht als Indexschlüsselspalten angegeben werden. **varchar(max)**, **nvarchar(max)**, **varbinary(max)**und **xml** -Datentypen können jedoch als Nichtschlüssel-Indexspalten in einen nicht gruppierten Index aufgenommen werden. Weitere Informationen finden Sie im Abschnitt [Index mit eingeschlossenen Spalten](#Included_Columns)in diesem Handbuch.  
  
-   Ein **xml** -Datentyp kann nur in einem XML-Index eine Schlüsselspalte sein. Weitere Informationen finden Sie unter [XML-Indizes &#40;SQL Server&#41;](../relational-databases/xml/xml-indexes-sql-server.md). Mit SQL Server 2012 SP1 wird ein neuer XML-Indextyp eingeführt, der als selektiver XML-Index bezeichnet wird. Durch diesen neuen Index kann die Abfrageleistung bei Daten verbessert werden, die als XML in SQL Server gespeichert sind. Das sorgt für eine schnellere Indizierung großer XML-Datenmengen und für höhere Skalierbarkeit, indem die Speicherkosten des Indexes gesenkt werden. Weitere Informationen finden Sie unter [Selektive XML-Indizes &#40;SXI&#41;](../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
-   Überprüfen Sie die Eindeutigkeit der Spalten. Ein eindeutiger Index anstelle eines nicht eindeutigen Indexes für dieselbe Kombination von Spalten stellt zusätzliche Informationen für den Abfrageoptimierer bereit, die den Index wertvoller machen. Weitere Informationen finden Sie unter [Richtlinien zum Entwerfen eindeutiger Indizes](#Unique) in diesem Handbuch.  
  
-   Überprüfen Sie die Datenverteilung in der Spalte. Häufig dauert eine Abfrage deshalb sehr lange, weil eine indizierte Spalte mit wenigen eindeutigen Werten verwendet wird oder weil sie einen Join mit einer solchen Spalte durchführt. Hierbei handelt es sich um ein grundlegendes Problem von Daten und Abfragen, das in der Regel nicht gelöst werden kann, ohne die betreffende Situation zu identifizieren. Beispielsweise wird ein physisches Telefonbuch, das alphabetisch nach dem Nachnamen sortiert ist, das Suchen eines Teilnehmers nicht vereinfachen, wenn alle Teilnehmer des Ortsnetzes Smith oder Jones heißen. Weitere Informationen zur Datenverteilung finden Sie unter [Statistics](../relational-databases/statistics/statistics.md).  
  
-   Verwenden Sie für Spalten mit fest definierten Teilmengen, z. B. Spalten mit geringer Dichte, Spalten, die größtenteils NULL-Werte enthalten, Spalten mit Wertekategorien und Spalten mit verschiedenen Wertebereichen, gefilterte Indizes. Ein gut entworfener gefilterter Index kann die Abfrageleistung verbessern, die Indexwartungskosten reduzieren und den Speicheraufwand verringern.  
  
-   Berücksichtigen Sie die Reihenfolge der Spalten, wenn der Index mehrere Spalten enthalten soll. Die Spalte, die in der WHERE-Klausel in einer Gleich- (=), Größer als- (>), Kleiner als- (<) oder BETWEEN-Suchbedingung verwendet oder in einen Join eingeschlossen wird, sollte an erster Stelle stehen. Die Reihenfolge zusätzlicher Spalten sollte basierend auf dem Grad ihrer Eindeutigkeit, d. h. von der eindeutigsten Spalte absteigend zu der am wenigsten eindeutigen Spalte, ausgewählt werden.  
  
     Wenn der Index z. B. als `LastName`, `FirstName` definiert ist, ist der Index hilfreich, wenn das Suchkriterium `WHERE LastName = 'Smith'` oder `WHERE LastName = Smith AND FirstName LIKE 'J%'`lautet. Der Abfrageoptimierer verwendet den Index jedoch nicht für eine Abfrage, die nur nach `FirstName (WHERE FirstName = 'Jane')`sucht.  
  
-   Ziehen Sie das Indizieren berechneter Spalten in Betracht. Weitere Informationen finden Sie unter [Indexes on Computed Columns](../relational-databases/indexes/indexes-on-computed-columns.md).  
  
### <a name="index-characteristics"></a>Indexmerkmale  
 Wenn sich herausgestellt hat, dass ein Index für eine Abfrage geeignet ist, können Sie den Indextyp auswählen, der für die jeweilige Situation am besten geeignet ist. Die Indexmerkmale beziehen sich z. B. auf Folgendes:  
  
-   Gruppiert im Vergleich zu nicht gruppiert  
  
-   Eindeutig im Vergleich zu nicht eindeutig  
  
-   Einspaltig im Vergleich zu mehrspaltig  
  
-   Aufsteigende oder absteigende Reihenfolge in den Spalten des Indexes  
  
-   Tabellenindizes im Vergleich zu gefilterten für nicht gruppierte Indizes  
  
 Um die Indexleistung- oder -wartung zu optimieren, können Sie durch das Festlegen einer Option wie z. B. FILLFACTOR auch die Ausgangsspeichermerkmale des Indexes anpassen. Zudem können Sie den Speicherort des Indexes mithilfe von Dateigruppen oder Partitionsschemas festlegen, um die Leistung zu optimieren.  
  
###  <a name="Index_placement"></a> Indexplatzierung in Dateigruppen oder Partitionsschemas  
 Bei der Entwicklung einer Indexentwurfsstrategie sollten Sie die Platzierung der Indizes in den Dateigruppen berücksichtigen, die der Datenbank zugeordnet sind. Das sorgfältige Auswählen der Dateigruppe oder des Partitionsschemas kann die Abfrageleistung verbessern.  
  
 Standardmäßig werden Indizes in derselben Dateigruppe wie die Basistabelle gespeichert, für die der Index erstellt wird. Ein nicht partitionierter, gruppierter Index und die Basistabelle befinden sich immer in der gleichen Dateigruppe. Sie können jedoch folgende Aktionen ausführen:  
  
-   Erstellen nicht gruppierter Indizes in einer anderen Dateigruppe als der Dateigruppe der Basistabelle oder des gruppierten Indexes.  
  
-   Partitionieren von gruppierten und nicht gruppierten Indizes, damit diese mehrere Dateigruppen umfassen.  
  
-   Verschieben einer Tabelle aus einer Dateigruppe in eine andere durch Löschen des gruppierten Index und Angeben einer neuen Dateigruppe oder eines Partitionsschemas in der MOVE TO-Klausel der DROP INDEX-Anweisung oder durch Verwenden der CREATE INDEX-Anweisung mit der DROP_EXISTIN-Klausel.  
  
 Wird der nicht gruppierte Index in einer anderen Dateigruppe erstellt, können Leistungsvorteile erzielt werden, wenn die Dateigruppen verschiedene physische Laufwerke mit eigenen Controllern verwenden. Daten und Indexinformationen können dann parallel von mehreren Leseköpfen gelesen werden. Werden beispielsweise `Table_A` in Dateigruppe `f1` und `Index_A` in Dateigruppe `f2` von derselben Abfrage verwendet, können Leistungsvorteile erzielt werden, da beide Dateigruppen konfliktfrei vollständig verwendet werden können. Wenn `Table_A` von der Abfrage durchsucht wird, ohne dass auf `Index_A` verwiesen wird, wird jedoch nur Dateigruppe `f1` verwendet. In diesem Fall ist kein Leistungsgewinn zu verzeichnen.  
  
 Da jedoch nicht vorhersehbar ist, welche Zugriffsart wann erfolgt, ist die Entscheidung für das Verteilen der Tabellen und Indizes auf alle Dateigruppen häufig die bessere Lösung. So ist sichergestellt, dass unabhängig von der Art des Datenzugriffs auf alle Datenträger zugegriffen wird, da alle Daten und Indizes gleichmäßig auf alle Datenträger verteilt sind. Diese Lösung ist auch aus Systemadministratorensicht einfacher.  
  
#### <a name="partitions-across-multiple-filegroups"></a>Partitionen über mehrere Dateigruppen  
 Sie können auch das Partitionieren von gruppierten und nicht gruppierten Indizes über mehrere Dateigruppen hinweg in Betracht ziehen. Partitionierte Indizes werden horizontal oder nach Zeile basierend auf einer Partitionsfunktion partitioniert. Die Partitionsfunktion definiert, wie jede einzelne Zeile einer Gruppe von Partitionen auf der Grundlage der Werte bestimmter Spalten zugeordnet wird, die als Partitionierungsspalten bezeichnet werden. Ein Partitionsschema gibt die Zuordnung dieser Partitionen zu einer Sammlung von Dateigruppen an.  
  
 Das Partitionieren eines Indexes kann die folgenden Vorteile bieten:  
  
-   Bereitstellen skalierbarer Systeme, die die Verwaltbarkeit großer Indizes vereinfachen. OLTP-Systeme können z. B. partitionsabhängige Anwendungen implementieren, die große Indizes verwalten können.  
  
-   Schnellere und effizientere Ausführung von Abfragen. Wenn Abfragen auf mehrere Partitionen eines Indexes zugreifen, kann der Abfrageoptimierer einzelne Partitionen gleichzeitig verarbeiten und Partitionen ausschließen, die nicht von der Abfrage betroffen sind.  
  
 Weitere Informationen finden Sie unter [Partitioned Tables and Indexes](../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
###  <a name="Sort_Order"></a> Entwurfsrichtlinien zur Sortierreihenfolge von Indizes  
 Beim Definieren von Indizes sollten Sie berücksichtigen, ob die Daten für die Indexschlüsselspalte in aufsteigender oder absteigender Reihenfolge gespeichert werden sollen. Die Standardreihenfolge ist aufsteigend. Hierbei wird auch die Kompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]beibehalten. Die Syntax der CREATE INDEX-, CREATE TABLE- und ALTER TABLE-Anweisungen unterstützt die Schüsselwörter ASC (aufsteigend) und DESC (absteigend) für einzelne Spalten in Indizes und Einschränkungen:  
  
 Das Angeben der Reihenfolge, in der die Schlüsselwerte in einem Index gespeichert werden, ist sinnvoll, wenn Abfragen, die auf die Tabelle verweisen, über ORDER BY-Klauseln verfügen, die verschiedene Richtungen für die Schlüsselspalten in dem entsprechenden Index angeben. In diesen Fällen kann der Index dafür sorgen, dass kein SORT-Operator mehr im Abfrageplan benötigt wird, wodurch die Abfrage effizienter wird. Die Mitarbeiter der Einkaufsabteilung von [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] müssen beispielsweise die Qualität der Produkte, die sie von den Anbietern kaufen, bewerten. Die Einkäufer sind vor allem interessiert daran, Produkte zu finden, die von diesen Anbietern gesendet wurden und die eine hohe Ablehnungsrate aufweisen. Wie in der folgenden Abfrage gezeigt, muss zum Abrufen der Daten, die diese Anforderung erfüllen, die `RejectedQty` -Spalte in der `Purchasing.PurchaseOrderDetail` -Tabelle in absteigender Reihenfolge (von groß nach klein) sortiert werden, und die `ProductID` -Spalte muss in aufsteigender Reihenfolge (von klein nach groß) sortiert werden.  
  
```  
SELECT RejectedQty, ((RejectedQty/OrderQty)*100) AS RejectionRate,  
    ProductID, DueDate  
FROM Purchasing.PurchaseOrderDetail  
ORDER BY RejectedQty DESC, ProductID ASC;  
```  
  
 Der folgende Ausführungsplan für diese Abfrage zeigt, dass der Abfrageoptimierer einen SORT-Operator verwendet hat, um das Resultset in der durch die ORDER BY-Klausel angegebenen Reihenfolge zurückzugeben.  
  
 ![IndexSort1](../relational-databases/media/indexsort1.gif)
  
  
 Falls ein Index mit Schlüsselspalten erstellt wird, die mit jenen in der ORDER BY-Klausel in der Abfrage übereinstimmen, kann der SORT-Operator im Abfrageplan gelöscht werden, wodurch der Abfrageplan effizienter wird.  
  
```  
CREATE NONCLUSTERED INDEX IX_PurchaseOrderDetail_RejectedQty  
ON Purchasing.PurchaseOrderDetail  
    (RejectedQty DESC, ProductID ASC, DueDate, OrderQty);  
```  
  
 Nachdem die Abfrage erneut ausgeführt wurde, zeigt folgender Ausführungsplan, dass der SORT-Operator gelöscht wurde und der neu erstellte nicht gruppierte Index verwendet wird.  
  
 ![InsertSort2](../relational-databases/media/insertsort2.gif)
  
  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] bewegt sich in beide Richtungen gleichermaßen effizient. Ein als `(RejectedQty DESC, ProductID ASC)` definierter Index kann nach wie vor für eine Abfrage verwendet werden, in der die Sortierreihenfolge der Spalten in der ORDER BY-Klausel reserviert sind. Eine Abfrage mit der ORDER BY-Klausel `ORDER BY RejectedQty ASC, ProductID DESC` kann den Index beispielsweise verwenden.  
  
 Die Sortierreihenfolge kann nur für Schlüsselspalten angegeben werden. Die Katalogsicht [sys.index_columns](../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md) und die INDEXKEY_PROPERTY-Funktion melden, ob eine Indexspalte in aufsteigender oder absteigender Reihenfolge gespeichert wird.  
  
  
##  <a name="Clustered"></a> Richtlinien für den Entwurf gruppierter Indizes  
 Gruppierte Indizes sortieren und speichern die Datenzeilen in den Tabellen basierend auf ihren Schlüsselwerten. Pro Tabelle kann nur ein gruppierter Index vorhanden sein, da die Datenzeilen nur in einer Reihenfolge sortiert werden können. Mit wenigen Ausnahmen sollte für jede Tabelle ein gruppierter Index für die Spalte(n) definiert werden, auf die Folgendes zutrifft:  
  
-   Sie kann für häufig verwendete Abfragen verwendet werden.  
  
-   Sie stellt einen hohen Grad an Eindeutigkeit bereit.  
  
    > [!NOTE]  
    >  Wenn Sie eine PRIMARY KEY-Einschränkung erstellen, wird automatisch ein eindeutiger Index für die Spalte(n) erstellt. Standardmäßig ist dieser Index gruppiert; Sie können jedoch auch einen nicht gruppierten Index angeben, wenn Sie die Einschränkung erstellen.  
  
-   Sie kann in Bereichsabfragen verwendet werden.  
  
 Wenn der gruppierte Index nicht mit der UNIQUE-Eigenschaft erstellt wird, fügt das [!INCLUDE[ssDE](../includes/ssde-md.md)] der Tabelle automatisch eine 4 Byte große uniqueifier-Spalte hinzu. Falls erforderlich, fügt das [!INCLUDE[ssDE](../includes/ssde-md.md)] einer Zeile automatisch einen uniqueifier-Wert hinzu, um jeden Schlüssel eindeutig zu machen. Diese Spalte und ihre Werte werden intern verwendet und können durch Benutzer nicht angezeigt werden. Der Zugriff durch Benutzer auf diese ist ebenfalls nicht möglich.  
  
### <a name="clustered-index-architecture"></a>Architektur gruppierter Indizes  
 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]sind Indizes in Form von B-Strukturen aufgebaut. Jede Seite in der B-Struktur eines Indexes wird als Indexknoten bezeichnet. Der oberste Knoten der B-Struktur wird als Stammknoten bezeichnet. Die unteren Knoten im Index werden als Blattknoten bezeichnet. Alle anderen Indexebenen zwischen dem Stamm- und den Blattknoten werden zusammenfassend als Zwischenebenen bezeichnet. In einem gruppierten Index enthalten die Blattknoten die Datenseiten der zugrunde liegenden Tabelle. Die Stamm- und Zwischenebenenknoten enthalten Indexseiten, in denen Indexzeilen enthalten sind. Jede Indexzeile enthält einen Schlüsselwert und einen Zeiger auf eine Seite einer Zwischenebene in der B-Struktur oder auf eine Datenzeile in der Blattebene des Indexes. Die Seiten auf jeder Ebene des Indexes sind durch eine doppelt verknüpfte Liste miteinander verknüpft.  
  
 Gruppierte Indizes besitzen eine Zeile in [sys.partitions](../relational-databases/system-catalog-views/sys-partitions-transact-sql.md), wobei **index_id** = 1 für jede Partition, die vom Index verwendet wird. Standardmäßig besitzt ein gruppierter Index eine Partition. Wenn ein gruppierter Index über mehrere Partitionen verfügt, besitzt jede Partition eine B-Struktur, die die Daten für diese bestimmte Partition enthält. Wenn ein gruppierter Index z. B. vier Partitionen besitzt, sind vier B-Strukturen vorhanden, eine in jeder Partition.  
  
 Abhängig von den Datentypen im gruppierten Index weist jede gruppierte Indexstruktur eine oder mehrere Zuordnungseinheiten auf, in denen die Daten für eine bestimmte Partition gespeichert und verwaltet werden. Jeder gruppierte Index weist mindestens eine IN_ROW_DATA-Zuordnungseinheit pro Partition auf. Der gruppierte Index besitzt außerdem eine LOB_DATA-Zuordnungseinheit pro Partition, wenn LOB-Spalten (Large Object) vorhanden sind. Außerdem ist eine ROW_OVERFLOW_DATA-Zuordnungseinheit pro Partition vorhanden, wenn der Index Spalten variabler Länge aufweist, die die Zeilengrößenbegrenzung von 8.060 Byte übersteigen.  
  
 Die Seiten in der Datenkette und die darin enthaltenen Zeilen werden anhand des Werts des Schlüssels des gruppierten Indexes angeordnet. Jede Einfügung wird an der Position vorgenommen, die der Schlüsselwert der eingefügten Zeile in der Reihenfolge vorhandener Zeilen einnimmt.  
  
 Die folgende Abbildung veranschaulicht die Struktur eines gruppierten Indexes in einer einzelnen Partition.  
 
 ![bokind2](../relational-databases/media/bokind2.gif)  
  
### <a name="query-considerations"></a>Überlegungen zu Abfragen  
 Bevor Sie gruppierte Indizes erstellen, sollten Sie sich überlegen, wie der Zugriff auf die Daten erfolgt. Einen gruppierten Index können Sie für Abfragen verwenden, die die folgenden Aktionen durchführen:  
  
-   Zurückgeben eines Wertebereichs, indem z. B. folgende Operatoren verwendet werden: BETWEEN, >, >=, < und <=.  
  
     Sobald mithilfe des gruppierten Indexes die Zeile mit dem ersten Wert gefunden wird, ist sichergestellt, dass Zeilen mit nachfolgenden Indexwerten physisch benachbart sind. Wenn mit einer Abfrage z. B. Datensätze aus einem Bereich von Verkaufsauftragsnummern abgerufen werden, bietet ein gruppierter Index für die `SalesOrderNumber` -Spalte die Möglichkeit, schnell die Zeile zu finden, die die Start-Verkaufsauftragsnummer enthält, und dann alle nachfolgenden Zeilen in der Tabelle abzurufen, bis die letzte Verkaufsauftragsnummer erreicht ist.  
  
-   Zurückgeben umfangreicher Resultsets.  
  
-   Verwenden von JOIN-Klauseln; in der Regel handelt es sich dabei um Fremdschlüsselspalten.  
  
-   Verwenden von ORDER BY- oder GROUP BY-Klauseln.  
  
     Durch einen Index für Spalten, die in der ORDER BY- oder GROUP BY-Klausel angegeben werden, entfällt ggf. die Notwendigkeit für [!INCLUDE[ssDE](../includes/ssde-md.md)] , die Daten zu sortieren, da die Zeilen bereits sortiert sind. Die Abfrageleistung wird somit verbessert.  
  
### <a name="column-considerations"></a>Überlegungen zu Spalten  
 Die Definition des gruppierten Indexschlüssels sollte im Allgemeinen so wenig Spalten wie möglich umfassen. Ziehen Sie Spalten in Betracht, auf die ein oder mehrere der folgenden Merkmale zutreffen:  
  
-   Sie sind eindeutig oder enthalten zahlreiche unterschiedliche Werte.  
  
     Eine Mitarbeiter-ID identifiziert einen Mitarbeiter z. B. eindeutig. Ein gruppierter Index oder eine PRIMARY KEY-Einschränkung für die `EmployeeID` -Spalte verbessert die Leistung von Abfragen, durch die Mitarbeiterinformationen anhand der Mitarbeiter-ID gesucht werden. Alternativ kann ein gruppierter Index für `LastName`, `FirstName`und `MiddleName` erstellt werden, weil Mitarbeiterdatensätze häufig auf diese Weise gruppiert und abgefragt werden und die Kombination dieser Spalten jedoch trotzdem einen hohen Differenzierungsgrad bietet.  
  
-   Der Zugriff auf sie erfolgt sequenziell.  
  
     Durch eine Produkt-ID werden Produkte in der `Production.Product` -Tabelle der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Datenbank beispielsweise eindeutig identifiziert. Abfragen, in denen eine sequenzielle Suche angegeben wird, z. B. `WHERE ProductID BETWEEN 980 and 999`, profitieren von einem gruppierten Index für `ProductID`. Die Ursache liegt darin, dass die Zeilen für diese Schlüsselspalte in sortierter Reihenfolge gespeichert werden.  
  
-   Definiert als IDENTITY.  
  
-   Sie wird häufig verwendet, um die aus einer Tabelle abgerufenen Daten zu sortieren.  
  
     Es kann sinnvoll sein, die Tabelle für die betreffende Spalte zu gruppieren (d. h., physisch zu sortieren), damit nicht bei jeder Abfrage der Spalte Kosten für einen Sortiervorgang entstehen.  
  
 Die Verwendung eines gruppierten Indexes ist nicht empfehlenswert, wenn die Spalten die folgenden Merkmale aufweisen:  
  
-   Spalten, die häufig geändert werden.  
  
     In diesem Fall würde die gesamte Zeile verschoben, weil [!INCLUDE[ssDE](../includes/ssde-md.md)] die physische Reihenfolge der Datenwerte der Zeile aufrechterhalten muss. Dieser Aspekt sollte insbesondere bei Systemen berücksichtigt werden, in denen Transaktionsverarbeitung in großem Umfang erfolgt und Daten nur selten von Dauer sind.  
  
-   Ausführliche Schlüssel.  
  
     Ausführliche Schlüssel sind aus mehreren Spalten oder mehreren großen Spalten zusammengesetzt. Die Schlüsselwerte aus dem gruppierten Index werden von allen nicht gruppierten Indizes als Suchschlüssel verwendet. Alle nicht gruppierten Indizes, die für dieselbe Tabelle definiert werden, sind erheblich größer, da die Einträge des nicht gruppierten Indexes den Gruppierungsschlüssel sowie die Schlüsselspalten enthalten, die für diesen nicht gruppierten Index definiert wurden.  
  
  
##  <a name="Nonclustered"></a> Entwurfsrichtlinien für einen nicht gruppierten Index  
 Ein nicht gruppierter Index enthält Indexschlüsselwerte sowie Zeilenlokatoren, die auf den Speicherort der Tabellendaten verweisen. Sie können mehrere nicht gruppierte Indizes für eine Tabelle oder eine indizierte Sicht erstellen. Im Allgemeinen sollten nicht gruppierte Indizes so entworfen werden, dass sich die Leistung häufig verwendeter Abfragen verbessert, die nicht vom gruppierten Index abgedeckt werden.  
  
 Vergleichbar mit der Art und Weise wie Sie einen Index in einem Buch verwenden, sucht der Abfrageoptimierer nach einem Datenwert, indem er den nicht gruppierten Index durchsucht, um so den Speicherort des Datenwerts in der Tabelle zu ermitteln. Anschließend werden die Daten direkt von diesem Speicherort abgerufen. Aus diesem Grund sind nicht gruppierte Indizes optimal für Abfragen geeignet, die nach genauen Übereinstimmungen suchen, da der Index Einträge enthält, die in der Tabelle den genauen Speicherort der Datenwerte beschreiben, die in den Abfragen gesucht werden. Wenn beispielsweise die `HumanResources. Employee` -Tabelle nach sämtlichen Mitarbeitern abgefragt werden soll, die einem bestimmten Abteilungsleiter unterstehen, verwendet der Abfrageoptimierer möglicherweise den nicht gruppierten Index `IX_Employee_ManagerID`; hier ist `ManagerID` die Schlüsselspalte. Der Abfrageoptimierer kann schnell alle Einträge im Index finden, die mit der angegebenen `ManagerID`übereinstimmen. Jeder Indexeinträg verweist auf die genaue Seite und Zeile in der Tabelle bzw. im gruppierten Index, in der die entsprechenden Daten zu finden sind. Nachdem der Abfrageoptimierer sämtliche Einträge im Index gefunden hat, kann er sich direkt zu der genauen Seite und Zeile begeben, um die Daten abzurufen.  
  
### <a name="nonclustered-index-architecture"></a>Architektur nicht gruppierter Indizes  
 Nicht gruppierte Indizes weisen dieselbe B-Baumstruktur auf wie gruppierte Indizes, mit Ausnahme der beiden folgenden signifikanten Unterschiede:  
  
-   Die Datenzeilen der zugrunde liegenden Tabelle werden nicht auf der Grundlage ihrer nicht gruppierten Schlüssel sortiert und gespeichert.  
  
-   Die Blattebene eines nicht gruppierten Indexes besteht aus Indexseiten, nicht aus Datenseiten.  
  
 Zeilenlokatoren in nicht gruppierten Indexzeilen bestehen entweder aus Zeigern, die auf jeweils eine Zeile zeigen, oder aus einem Schlüssel eines gruppierten Indexes für eine Zeile, wie im Folgenden erläutert:  
  
-   Wenn es sich bei der Tabelle um einen Heap handelt (d. h. sie hat keinen gruppierten Index), entspricht der Zeilenlokator einem Zeiger auf die Zeile. Der Zeiger setzt sich aus dem Dateibezeichner (ID), der Seitennummer und der Nummer der Zeile auf der Seite zusammen. Der ganze Zeiger wird als Zeilen-ID (RID) bezeichnet.  
  
-   Wenn die Tabelle einen gruppierten Index besitzt oder der Index für eine indizierte Sicht erstellt wurde, ist der Zeilenlokator der Schlüssel des gruppierten Indexes für die Zeile.  
  
 Nicht gruppierte Indizes verfügen in [sys.partitions](../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) für jede vom Index verwendete Partition über eine Zeile, deren **index_id** >1 ist. Standardmäßig besitzen nicht gruppierte Indizes nur eine Partition. Wenn ein nicht gruppierter Index mehrere Partitionen besitzt, weist jede Partition eine B-Baumstruktur auf, die die Indexzeilen der entsprechenden Partition enthält. Wenn ein nicht gruppierter Index beispielsweise vier Partitionen besitzt, gibt es vier B-Baumstrukturen – jeweils eine in jeder Partition.  
  
 Abhängig von den Datentypen des nicht gruppierten Indexes erhält jede Struktur mindestens eine Zuordnungseinheit, in der die Daten einer bestimmten Partition gespeichert und verwaltet werden. Jeder nicht gruppierte Index besitzt also eine IN_ROW_DATA-Zuordnungseinheit pro Partition, die die B-Baumstrukturseiten des Indexes speichert. Außerdem besitzt der nicht gruppierte Index eine LOB_DATA-Zuordnungseinheit, wenn er LOB-Spalten (Large Object) enthält. Endlich besitzt er eine ROW_OVERFLOW_DATA-Zuordnungseinheit pro Partition, wenn er Spalten variabler Länge enthält, die das Zeilengrößenlimit von 8.060 Byte überschreiten.  
  
 Die folgende Abbildung veranschaulicht die Struktur eines gruppierten Indexes einer einzigen Partition.  

![bokind1a](../relational-databases/media/bokind1a.gif)  
  
  
### <a name="database-considerations"></a>Überlegungen zu Datenbanken  
 Berücksichtigen Sie beim Entwerfen nicht gruppierter Indizes die Merkmale der jeweiligen Datenbank.  
  
-   Datenbanken oder Tabellen mit geringen Updateanforderungen, aber großem Datenvolumen, können von zahlreichen nicht gruppierten Indizes zur Verbesserung der Abfrageleistung profitieren. Mit gefilterten Indizes mit klar definierten Teilmengen von Daten können Sie im Vergleich zu nicht gruppierten Tabellenindizes die Abfrageleistung verbessern und den Aufwand für die Indexverwaltung und die Indexspeicherung reduzieren.  
  
     Entscheidungsunterstützungssystem-Anwendungen und -Datenbanken, die hauptsächlich schreibgeschützte Daten enthalten, können von zahlreichen nicht gruppierten Indizes profitieren. Der Abfrageoptimierer hat hinsichtlich des Ermittelns der schnellsten Zugriffsmethode eine größere Auswahl an Indizes, und da die Datenbankmerkmale auf einen geringen Updateaufwand schließen lassen, wird die Leistung durch die Indexwartung nicht beeinträchtigt.  
  
-   Bei Anwendungen und Datenbanken zur Onlinetransaktionsverarbeitung mit Tabellen, die umfassend aktualisiert werden, sollte ein Übermaß an Indizierung vermieden werden. Zusätzlich sollten die Indizes schmal sein, also so wenig Spalten wie möglich enthalten.  
  
     Eine große Anzahl an Indizes für eine Tabelle beeinträchtigt die Leistung von INSERT-, UPDATE-, DELETE- und MERGE-Anweisungen, da alle Indizes entsprechend angepasst werden müssen, sobald Daten in der Tabelle geändert werden.  
  
### <a name="query-considerations"></a>Überlegungen zu Abfragen  
 Bevor Sie nicht gruppierte Indizes erstellen, sollten Sie sich darüber im Klaren sein, wie der Zugriff auf Ihre Daten erfolgt. Erwägen Sie das Verwenden eines nicht gruppierten Indexes für Abfragen mit folgenden Attributen:  
  
-   Verwenden von JOIN- oder GROUP BY-Klauseln.  
  
     Erstellen Sie mehrere nicht gruppierte Indizes für Spalten, die an Join- und Gruppierungsvorgängen beteiligt sind, sowie einen gruppierten Index für eine beliebige Fremdschlüsselspalte.  
  
-   Kein Zurückgeben großer Resultsets.  
  
     Erstellen Sie gefilterte Indizes für Abfragen, die eine klar definierte Zeilenteilmenge aus einer großen Tabelle zurückgeben.  
  
-   Enthalten von Spalten, die häufig an Suchbedingungen einer Abfrage beteiligt sind (z. B. WHERE-Klausel), die genaue Übereinstimmungen zurückgeben.  
  
### <a name="column-considerations"></a>Überlegungen zu Spalten  
 Ziehen Sie Spalten mit einem oder mehrerer dieser Attribute in Betracht:  
  
-   Abdecken der Abfrage.  
  
     Leistungsgewinne werden erzielt, wenn der Index alle Spalten in der Abfrage enthält. Der Abfrageoptimierer kann alle Spaltenwerte im Index finden; da auf Daten der Tabelle oder des gruppierten Indexes nicht zugegriffen wird, kommt es zu weniger Datenträger-E/A-Vorgängen. Verwenden Sie einen Index mit eingeschlossenen Spalten, um mehrere Spalten abzudecken, anstatt einen breiten Indexschlüssel zu erstellen.  
  
     Wenn die Tabelle einen gruppierten Index aufweist, werden die im gruppierten Index definierten Spalten automatisch an das Ende sämtlicher nicht gruppierter Indizes für die Tabelle angefügt. Auf diese Weise kann eine abgedeckte Abfrage erstellt werden, ohne dass die Spalten des gruppierten Indexes in der Definition des nicht gruppierten Indexes angegeben werden. Wenn eine Tabelle beispielsweise einen gruppierten Index für Spalte `C`besitzt, weist ein nicht gruppierter Index für die Spalten `B` und `A` die Schlüsselwertspalten `B`, `A`und `C`auf.  
  
-   Große Anzahl unterschiedlicher Werte, beispielsweise eine Kombination aus Nachname und Vorname, wenn für andere Spalten ein gruppierter Index verwendet wird.  
  
     Wenn nur sehr wenige unterschiedliche Werte vorhanden sind, beispielsweise nur 1 und 0, verwenden die meisten Abfragen den Index nicht, da ein Tabellenscan im Allgemeinen effizienter ist. Für diesen Datentyp sollten Sie einen gefilterten Index anhand eines anderen Werts erstellen, der in weniger Zeilen vorkommt. Beispiel: Wenn die meisten Werte 0 sind, kann der Abfrageoptimierer einen gefilterten Index für die Zeilen verwenden, die den Wert 1 enthalten.  
  
####  <a name="Included_Columns"></a> Verwenden eingeschlossener Spalten, um nicht gruppierte Indizes zu erweitern  
 Sie können die Funktionen nicht gruppierter Indizes erweitern, indem Sie der Blattebene des nicht gruppierten Indexes Nichtschlüsselspalten hinzufügen. Indem Sie Nichtschlüsselspalten einschließen, erstellen Sie nicht gruppierte Indizes, die eine größere Anzahl von Abfragen abdecken. Dies ist der Fall, weil Nichtschlüsselspalten die folgenden Vorteile aufweisen:  
  
-   Es kann sich um Datentypen handeln, die als Indexschlüsselspalten nicht zulässig sind.  
  
-   Sie werden von [!INCLUDE[ssDE](../includes/ssde-md.md)] beim Berechnen der Indexschlüsselspalten oder Indexschlüsselgröße nicht berücksichtigt.  
  
 Ein Index mit eingeschlossenen Nichtschlüsselspalten kann die Abfrageleistung erheblich steigern, wenn alle Spalten in der Abfrage in den Index als Schlüssel- oder Nichtschlüsselspalten eingeschlossen werden. Leistungsvorteile werden erzielt, weil der Abfrageoptimierer alle Spaltenwerte im Index finden kann; auf Daten der Tabelle oder des gruppierten Indexes wird nicht zugegriffen, sodass als Ergebnis weniger Datenträger-E/A-Vorgänge auftreten.  
  
> [!NOTE]  
>  Wenn ein Index alle Spalten enthält, auf die die Abfrage verweist, wird dies normalerweise als Abdecken der Abfrage bezeichnet.  
  
 Die Schlüsselspalten werden auf allen Ebenen des Indexes gespeichert, die Nichtschlüsselspalten nur auf der Blattebene.  
  
##### <a name="using-included-columns-to-avoid-size-limits"></a>Verwenden eingeschlossener Spalten, um Größenbeschränkungen zu umgehen  
 Sie können Nichtschlüsselspalten in einen nicht gruppierten Index einschließen, damit die Größenbegrenzungen des aktuellen Indexes von maximal 16 Schlüsselspalten und einer maximalen Größe des Indexschlüssels von 900 Byte nicht überschritten werden. Nichtschlüsselspalten werden von [!INCLUDE[ssDE](../includes/ssde-md.md)] beim Berechnen der Indexschlüsselspalten oder Indexschlüsselgröße nicht berücksichtigt.  
  
 Angenommen, Sie möchten die folgenden Spalten in der `Document` -Tabelle indizieren:  
  
 `Title nvarchar(50)`  
  
 `Revision nchar(5)`  
  
 `FileName nvarchar(400)`  
  
 Da für die Datentypen **nchar** und **nvarchar** 2 Bytes für jedes Zeichen erforderlich sind, überschreitet ein Index, der diese drei Spalten enthält, die Größenbeschränkung von 900 Bytes um 10 Bytes (455 * 2). Indem die `INCLUDE` -Klausel der `CREATE INDEX` -Anweisung verwendet wird, kann der Indexschlüssel als (`Title, Revision`) und `FileName` als Nichtschlüsselspalte definiert werden. Auf diese Weise beträgt die Größe des Indexschlüssels 110 Byte (55 \* 2), und der Index enthält dennoch alle erforderlichen Spalten. Die folgende Anweisung erstellt einen solchen Index:  
  
```  
CREATE INDEX IX_Document_Title   
ON Production.Document (Title, Revision)   
INCLUDE (FileName);   
```  
  
##### <a name="index-with-included-columns-guidelines"></a>Richtlinien für Indizes mit eingeschlossenen Spalten  
 Wenn Sie nicht gruppierte Indizes mit eingeschlossenen Spalten entwerfen, sollten Sie die folgenden Richtlinien beachten:  
  
-   Nichtschlüsselspalten werden in der INCLUDE-Klausel der CREATE INDEX-Anweisung definiert.  
  
-   Nichtschlüsselspalten können nur für nicht gruppierte Indizes für Tabellen oder indizierte Sichten definiert werden.  
  
-   Mit Ausnahme von **text**, **ntext**und **image**sind alle Datentypen zulässig.  
  
-   Bei berechneten Spalten, die deterministisch und präzise oder unpräzise sind, kann es sich um eingeschlossene Spalten handeln. Weitere Informationen finden Sie unter [Indexes on Computed Columns](../relational-databases/indexes/indexes-on-computed-columns.md).  
  
-   Ebenso wie Schlüsselspalten können berechnete Spalten, die aus **image**, **ntext**und **text** -Datentypen abgeleitet werden, Nichtschlüsselspalten (eingeschlossene Spalten) sein, wenn der Datentyp der berechneten Spalte als Nichtschlüssel-Indexspalte zulässig ist.  
  
-   Spaltennamen dürfen nicht sowohl in der INCLUDE-Liste als auch in der Schlüsselspaltenliste angegeben werden.  
  
-   Spaltennamen können nicht in der INCLUDE-Liste wiederholt werden.  
  
##### <a name="column-size-guidelines"></a>Richtlinien für die Spaltengröße  
  
-   Es muss mindestens eine Schlüsselspalte definiert werden. Die maximal zulässige Anzahl der Nichtschlüsselspalten beträgt 1023 Spalten. Dies ist die maximale Anzahl der Tabellenspalten minus 1.  
  
-   Indexschlüsselspalten (ausschließlich der Nichtschlüsselspalten) unterliegen der Begrenzung der Indexgröße auf maximal 16 Schlüsselspalten und der Gesamtgröße des Indexschlüssels von 900 Byte.  
  
-   Die Gesamtgröße aller Nichtschlüsselspalten wird nur durch die in der INCLUDE-Klausel angegebene Größe der Spalten beschränkt; **varchar(max)** -Spalten sind z. B. auf 2 GB beschränkt.  
  
##### <a name="column-modification-guidelines"></a>Richtlinien für die Spaltenänderung  
 Wenn Sie eine Tabellenspalte ändern, die als eingeschlossene Spalte definiert wurde, gelten die folgenden Einschränkungen:  
  
-   Nichtschlüsselspalten können nur aus der Tabelle gelöscht werden, wenn der Index zuvor gelöscht wird.  
  
-   Nichtschlüsselspalten können nur zum Ausführen der folgenden Aufgaben geändert werden:  
  
    -   Ändern der NULL-Zulässigkeit der Spalte von NOT NULL in NULL.  
  
    -   Vergrößern der Länge von **varchar**-, **nvarchar**- oder **varbinary** -Spalten.  
  
        > [!NOTE]  
        >  Diese Einschränkungen hinsichtlich der Spaltenänderung gelten für Indexschlüsselspalten.  
  
##### <a name="design-recommendations"></a>Entwurfsempfehlungen  
 Überarbeiten Sie nicht gruppierte Indizes mit großen Indexschlüsseln so, dass nur Spalten, die für Suchen und Suchvorgänge verwendet werden, Schlüsselspalten sind. Erklären Sie alle anderen Spalten, die die Abfrage abdecken, zu eingeschlossenen Nichtschlüsselspalten. Auf diese Weise sind alle Spalten vorhanden, die zum Abdecken der Abfrage erforderlich sind, der Indexschlüssel selbst ist jedoch klein und effizient.  
  
 Angenommen, Sie möchten z. B. einen Index entwerfen, der die folgende Abfrage abdeckt:  
  
```  
SELECT AddressLine1, AddressLine2, City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE PostalCode BETWEEN N'98000' and N'99999';  
```  
  
 Damit die Abfrage abgedeckt wird, muss jede Spalte im Index definiert werden. Sie könnten zwar alle Spalten als Schlüsselspalten definieren, die Schlüsselgröße würde dann aber 334 Byte betragen. Da die einzige Spalte, die tatsächlich als Suchkriterium verwendet wird, die `PostalCode` -Spalte mit einer Länge von 30 Byte ist, definiert der bessere Indexentwurf `PostalCode` als Schlüsselspalte und schließt alle anderen Spalten als Nichtschlüsselspalten ein.  
  
 Die folgende Anweisung erstellt einen Index mit eingeschlossenen Spalten, um die Abfrage abzudecken:  
  
```  
CREATE INDEX IX_Address_PostalCode  
ON Person.Address (PostalCode)  
INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
```  
  
##### <a name="performance-considerations"></a>Überlegungen zur Leistung  
 Vermeiden Sie es, nicht erforderliche Spalten hinzuzufügen. Das Hinzufügen einer zu großen Anzahl von Schlüssel- oder Nichtschlüssel-Indexspalten kann zu folgenden Auswirkungen auf die Leistung führen:  
  
-   Es passen weniger Indexzeilen auf eine Seite. Dies kann zu einer Zunahme der E/A und verringerter Cacheeffizienz führen.  
  
-   Zum Speichern des Indexes ist eine größere Menge an Speicherplatz erforderlich. Insbesondere das Hinzufügen von **varchar(max)**, **nvarchar(max)**, **varbinary(max)**oder **xml** -Datentypen als Nichtschlüssel-Indexspalten kann die Anforderungen an den Speicherplatz erheblich erhöhen. Der Grund liegt darin, dass die Spaltenwerte in die Blattebene des Indexes kopiert werden. Daher werden sie sowohl im Index als auch in der Basistabelle gespeichert.  
  
-   Die Indexwartung kann zu einem größeren Zeitaufwand für das Ausführen von Änderungen, Einfügungen, Updates oder Löschvorgängen an der zugrunde liegenden Tabelle oder indizierten Sicht führen.  
  
 Sie müssen überprüfen, ob die Steigerungen der Abfrageleistung die negativen Auswirkungen auf die Leistung während der Datenänderung sowie hinsichtlich zusätzlicher Speicherplatzanforderungen aufwiegen.  
  
  
##  <a name="Unique"></a> Richtlinien zum Entwerfen eindeutiger Indizes  
 Ein eindeutiger Index garantiert, dass der Indexschlüssel keine doppelten Werte enthält und dass deshalb jede Zeile in der Tabelle in gewisser Weise eindeutig ist. Das Angeben eines eindeutigen Indexes ist nur dann sinnvoll, wenn die Eindeutigkeit ein Merkmal der Daten ist. Wenn Sie z. B. sicherstellen möchten, dass die Werte in der `NationalIDNumber` -Spalte der `HumanResources.Employee` -Tabelle eindeutig sind, wenn der Primärschlüssel `EmployeeID`entspricht, erstellen Sie eine UNIQUE-Einschränkung für die `NationalIDNumber` -Spalte. Wenn der Benutzer versucht, denselben Wert für mehrere Mitarbeiter in diese Spalte einzugeben, wird eine Fehlermeldung angezeigt, und der doppelte Wert wird nicht eingegeben.  
  
 Durch eindeutige Indizes für mehrere Spalten stellt der Index sicher, dass jede Kombination der Werte in der indizierten Spalte eindeutig ist. Wenn z. B. ein eindeutiger Index für eine Kombination der Spalten `LastName`, `FirstName`und `MiddleName` erstellt wird, können zwei Zeilen in der Tabelle nicht über dieselbe Wertekombination für diese Spalten verfügen.  
  
 Sowohl gruppierte als auch nicht gruppierte Indizes können eindeutig sein. Unter der Voraussetzung, dass die Daten in der Spalte eindeutig sind, können Sie einen eindeutigen gruppierten Index und mehrere eindeutige nicht gruppierte Indizes für dieselbe Tabelle erstellen.  
  
 Eindeutige Indizes haben folgende Vorteile:  
  
-   Die Datenintegrität der definierten Spalten ist sichergestellt.  
  
-   Es werden zusätzliche, für den Abfrageoptimierer hilfreiche Informationen bereitgestellt.  
  
 Durch das Erstellen einer PRIMARY KEY- oder einer UNIQUE-Einschränkung wird automatisch ein eindeutiger Index für die angegebenen Spalten erstellt. Es gibt keine deutlichen Unterschiede zwischen dem Erstellen einer UNIQUE-Einschränkung und dem Erstellen eines eindeutigen Indexes unabhängig von einer Einschränkung. Die Datenüberprüfung erfolgt auf dieselbe Weise, und der Abfrageoptimierer macht keinen Unterschied zwischen einem durch eine Einschränkung erstellten eindeutigen Index und einem manuell erstellten Index. Allerdings sollten sie eine UNIQUE- oder PRIMARY KEY-Einschränkung für die Spalte erstellen, wenn Datenintegrität das Ziel ist. Dadurch wird das Ziel des Indexes klar.  
  
### <a name="considerations"></a>Weitere Überlegungen  
  
-   Ein eindeutiger Index, die UNIQUE-Einschränkung oder die PRIMARY KEY-Einschränkung kann nicht erstellt werden, wenn in den Daten doppelte Schlüsselwerte vorhanden sind.  
  
-   Wenn die Daten eindeutig sind und Sie die Eindeutigkeit erzwingen wollen, werden durch das Erstellen eines eindeutigen Indexes anstelle eines nicht eindeutigen Indexes für dieselbe Spaltenkombination zusätzliche Informationen für den Abfrageoptimierer bereitgestellt, mit deren Hilfe effizientere Ausführungspläne erstellt werden können. Das Erstellen eines eindeutigen Indexes (vorzugsweise durch Erstellen einer UNIQUE-Einschränkung) ist in diesem Fall empfohlen.  
  
-   Ein eindeutiger, nicht gruppierter Index kann eingeschlossene Nichtschlüsselspalten enthalten. Weitere Informationen finden Sie unter [Index mit eingeschlossenen Spalten](#Included_Columns).  
  
  
##  <a name="Filtered"></a> Richtlinien für den Entwurf gefilterter Indizes  
 Ein gefilterter Index ist ein optimierter nicht gruppierter Index, der sich besonders für Abfragen eignet, bei denen aus einer fest definierten Teilmenge von Daten ausgewählt wird. Dieser verwendet ein Filterprädikat, um einen Teil der Zeilen in der Tabelle zu indizieren. Mit einem sorgfältig entworfenen gefilterten Index können im Gegensatz zu Tabellenindizes die Abfrageleistung verbessert und der Aufwand für die Indexverwaltung und -speicherung reduziert werden.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|  
  
 Gefilterte Indizes können gegenüber Tabellenindizes folgende Vorteile bieten:  
  
-   **Verbesserte Abfrageleistung und Planqualität**  
  
     Mit einem sorgfältig entworfenen gefilterten Index wird die Abfrageleistung und die Ausführungsplanqualität verbessert, da dieser kleiner ist als ein nicht gruppierter Tabellenindex und mit gefilterten Statistiken arbeitet. Die gefilterten Statistiken sind genauer als Tabellenstatistiken, da diese nur die Zeilen im gefilterten Index umfassen.  
  
-   **Reduzierter Aufwand bei der Indexverwaltung**  
  
     Ein Index wird nur beibehalten, wenn DML-Anweisungen (Data Manipulation Language) die Daten im Index beeinflussen. Ein gefilterter Index reduziert im Vergleich zu einem nicht gruppierten Tabellenindex den Aufwand für die Indexverwaltung, da dieser kleiner ist und nur beibehalten wird, wenn die Daten im Index beeinflusst werden. Eine große Anzahl von gefilterten Indizes ist insbesondere dann von Vorteil, wenn diese Daten enthalten, die nur selten beeinflusst werden. Ebenso reduziert die geringere Indexgröße den Aufwand für die Aktualisierung der Statistiken, wenn ein gefilterter Index nur die häufig beeinflussten Daten enthält.  
  
-   **Reduzierter Aufwand bei der Indexspeicherung**  
  
     Ein gefilterter Index kann den Speicherplatzbedarf von nicht gruppierten Indizes reduzieren, wenn ein Tabellenindex nicht erforderlich ist. Sie können einen nicht gruppierten Tabellenindex durch mehrere gefilterte Indizes ersetzen, ohne damit die Speicherplatzanforderungen wesentlich zu erhöhen.  
  
 Gefilterte Indizes sind nützlich, wenn Spalten klar definierte Teilmengen von Daten enthalten, auf die Abfragen in SELECT-Anweisungen verweisen. Beispiele:  
  
-   Spalten mit geringer Dichte, die nur wenige Werte ungleich NULL enthalten.  
  
-   Heterogene Spalten, die Datenkategorien enthalten.  
  
-   Spalten, die Wertebereiche enthalten, z.&nbsp;B. Dollarmengen, Zeit- und Datumsangaben.  
  
-   Tabellenpartitionen, die durch einfache Vergleichslogik für Spaltenwerte definiert werden.  
  
 Der reduzierte Verwaltungsaufwand für gefilterte Indizes ist am deutlichsten, wenn die Zeilenanzahl im Index verglichen mit der eines Tabellenindex klein ist. Wenn der gefilterte Index die meisten Zeilen in der Tabelle einschließt, ist der Verwaltungsaufwand möglicherweise größer als bei einem Tabellenindex. In diesem Fall sollten Sie anstelle eines gefilterten Index einen Tabellenindex verwenden.  
  
 Gefilterte Indizes werden für eine Tabelle definiert und unterstützen nur einfache Vergleichsoperatoren. Wenn Sie einen Filterausdruck benötigen, der auf mehrere Tabellen verweist oder eine komplexe Logik aufweist, sollten Sie eine Sicht erstellen.  
  
### <a name="design-considerations"></a>Entwurfsaspekte  
 Wenn Sie effektive gefilterte Indizes entwerfen möchten, müssen Sie wissen, welche Abfragen von Ihrer Anwendung verwendet werden und wie diese mit Teilmengen Ihrer Daten in Beziehung stehen. Einige Beispiele für Daten mit fest definierten Teilmengen sind Spalten, die größtenteils nur NULL-Werte enthalten, Spalten mit heterogenen Wertekategorien und Spalten mit verschiedenen Wertebereichen. Die folgenden Entwurfsüberlegungen zeigen, wann ein gefilterter Index Vorteile gegenüber Tabellenindizes hat.  
  
#### <a name="filtered-indexes-for-subsets-of-data"></a>Gefilterte Indizes für Datenteilmengen  
 Wenn eine Spalte nur wenig relevante Werte für Abfragen aufweist, können Sie für die Teilmenge der Werte einen gefilterten Index erstellen. Wenn beispielsweise die Werte in einer Spalte größtenteils NULL sind und die Abfrage nur die Werte ungleich NULL berücksichtigt, können Sie für die Datenzeilen mit den Werten ungleich NULL einen gefilterten Index erstellen. Der resultierende Index ist kleiner und verursacht weniger Verwaltungsaufwand als ein nicht gruppierter Tabellenindex, der für dieselben Schlüsselspalten festgelegt wird.  
  
 Die Datenbank `AdventureWorks2012` enthält z. B. eine `Production.BillOfMaterials` -Tabelle mit 2679 Zeilen. Die `EndDate` -Spalte hat nur 199 Zeilen mit einem Wert ungleich NULL. Die anderen 2.480 Zeilen enthalten einen NULL-Wert. Der folgende gefilterte Index würde Abfragen abdecken, die die im Index definierten Spalten zurückgeben und die für `EndDate`nur Zeilen mit einem Wert ungleich NULL auswählen.  
  
```  
CREATE NONCLUSTERED INDEX FIBillOfMaterialsWithEndDate  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL ;  
GO  
```  
  
 Der gefilterte Index `FIBillOfMaterialsWithEndDate` ist für die folgende Abfrage gültig. Sie können den Abfrageausführungsplan anzeigen, um zu bestimmen, ob der Abfrageoptimierer den gefilterten Index verwendet hat.  
  
```  
SELECT ProductAssemblyID, ComponentID, StartDate   
FROM Production.BillOfMaterials  
WHERE EndDate IS NOT NULL   
    AND ComponentID = 5   
    AND StartDate > '20080101' ;  
```  
  
 Weitere Informationen zum Erstellen von gefilterten Indizes und zum Definieren des Prädikatausdrucks für gefilterte Indizes finden Sie unter [Create Filtered Indexes](../relational-databases/indexes/create-filtered-indexes.md).  
  
#### <a name="filtered-indexes-for-heterogeneous-data"></a>Gefilterte Indizes für heterogene Daten  
 Wenn eine Tabelle heterogene Datenzeilen enthält, können Sie einen gefilterten Index für eine oder mehrere Datenkategorien erstellen.  
  
 Zum Beispiel wird jedes Produkt, das in der `Production.Product` -Tabelle aufgelistet ist, einer `ProductSubcategoryID`zugewiesen, die wiederum den Produktkategorien Fahrräder, Bauteile, Bekleidung oder Zubehör zugeordnet wird. Diese Kategorien sind heterogen, da ihre Spaltenwerte in der `Production.Product` -Tabelle nicht eng zueinander in Beziehung stehen. Beispielsweise besitzen die Spalten `Color`, `ReorderPoint`, `ListPrice`, `Weight`, `Class`und `Style` eindeutige Merkmale für jede Produktkategorie. Angenommen, es werden häufig Abfragen für Zubehör mit Unterkategorien zwischen 27 und 36 einschließlich ausgeführt. Sie können die Abfrageleistung für Zubehör verbessern, indem Sie einen gefilterten Index für die Unterkategorien von Zubehör erstellen, wie im folgenden Beispiel veranschaulicht.  
  
```  
CREATE NONCLUSTERED INDEX FIProductAccessories  
    ON Production.Product (ProductSubcategoryID, ListPrice)   
        Include (Name)  
WHERE ProductSubcategoryID >= 27 AND ProductSubcategoryID <= 36;  
  
```  
  
 Der gefilterte Index `FIProductAccessories` deckt die folgende Abfrage ab, da die Abfrageergebnisse  
  
 im Index enthalten sind und der Abfrageplan keine Basistabellensuche einschließt. Der Abfrageprädikatausdruck `ProductSubcategoryID = 33` ist z. B. eine Teilmenge der gefilterten Indexprädikate `ProductSubcategoryID >= 27` und `ProductSubcategoryID <= 36`, die Spalten `ProductSubcategoryID` und `ListPrice` im Abfrageprädikat sind beides Schlüsselspalten im Index, und der Name wird in der Blattebene des Indexes als einbezogene Spalte gespeichert.  
  
```  
SELECT Name, ProductSubcategoryID, ListPrice  
FROM Production.Product  
WHERE ProductSubcategoryID = 33 AND ListPrice > 25.00 ;  
  
```  
  
#### <a name="key-columns"></a>Schlüsselspalten  
 Die bewährte Methode besteht darin, eine geringe Anzahl von Schlüsselspalten oder eingeschlossenen Spalten in eine Definition des gefilterten Indexes einzuschließen und nur die Spalten einzubeziehen, die der Abfrageoptimierer benötigt, um den gefilterten Index für den Abfrageausführungsplan auszuwählen. Der Abfrageoptimierer kann einen gefilterten Index für die Abfrage auswählen, unabhängig davon, ob dieser die Abfrage abdeckt oder nicht. Der Abfrageoptimierer wählt jedoch eher einen gefilterten Index aus, der die Abfrage abdeckt.  
  
 In einigen Fällen deckt ein gefilterter Index die Abfrage ab, ohne die Spalten im gefilterten Indexausdruck als Schlüsselspalten oder eingeschlossene Spalten in der Definition des gefilterten Indexes einzuschließen. Die folgenden Richtlinien erläutern, wann eine Spalte im gefilterten Indexausdruck eine Schlüsselspalte oder eingeschlossene Spalte in der Definition des gefilterten Indexes sein sollte. Die Beispiele beziehen sich auf den gefilterten Index `FIBillOfMaterialsWithEndDate` , der zuvor erstellt wurde.  
  
 Eine Spalte im gefilterten Indexausdruck muss in der gefilterten Indexdefinition keine Schlüsselspalte oder eingeschlossene Spalte sein, wenn der gefilterte Indexausdruck dem Abfrageprädikat entspricht und die Abfrage die Spalte im gefilterten Indexausdruck mit den Abfrageergebnissen nicht zurückgibt. Zum Beispiel deckt `FIBillOfMaterialsWithEndDate` die folgende Abfrage ab, da das Abfrageprädikat dem Filterausdruck entspricht und `EndDate` nicht mit den Abfrageergebnissen zurückgegeben wird. `FIBillOfMaterialsWithEndDate` erfordert nicht, dass `EndDate` eine Schlüsselspalte oder eingeschlossene Spalte in der Definition des gefilterten Indexes ist.  
  
```  
SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
WHERE EndDate IS NOT NULL;   
```  
  
 Eine Spalte im gefilterten Indexausdruck sollte in der gefilterten Indexdefinition eine Schlüsselspalte oder eingeschlossene Spalte sein, wenn das Abfrageprädikat die Spalte in einem Vergleich verwendet, der nicht dem gefilterten Indexausdruck entspricht. Zum Beispiel ist `FIBillOfMaterialsWithEndDate` für die folgende Abfrage gültig, da damit aus dem gefilterten Index eine Teilmenge von Zeilen ausgewählt wird. Damit wird jedoch nicht die folgende Abfrage abgedeckt, da `EndDate` im Vergleich `EndDate > '20040101'`verwendet wird, der nicht dem gefilterten Indexausdruck entspricht. Der Abfrageprozessor kann diese Abfrage nicht ausführen, ohne die Werte von `EndDate`abzurufen. Deshalb sollte `EndDate` eine Schlüsselspalte oder eingeschlossene Spalte in der Definition des gefilterten Indexes darstellen.  
  
```  
SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
WHERE EndDate > '20040101';   
```  
  
 Eine Spalte im gefilterten Indexausdruck sollte in der Definition des gefilterten Indexes eine Schlüsselspalte oder eingeschlossene Spalte sein, wenn die Spalte im Abfrageresultset enthalten ist. Zum Beispiel deckt `FIBillOfMaterialsWithEndDate` die folgende Abfrage nicht ab, da damit die `EndDate` -Spalte in den Abfrageergebnissen zurückgegeben wird. Deshalb sollte `EndDate` eine Schlüsselspalte oder eingeschlossene Spalte in der Definition des gefilterten Indexes darstellen.  
  
```  
SELECT ComponentID, StartDate, EndDate FROM Production.BillOfMaterials  
WHERE EndDate IS NOT NULL;  
```  
  
 Der Schlüssel des gruppierten Indexes für die Tabelle muss in der gefilterten Indexdefinition keine Schlüsselspalte oder eingeschlossene Spalte sein. Der Schlüssel des gruppierten Indexes ist automatisch in allen nicht gruppierten Indizes enthalten, dazu zählen auch gefilterte Indizes.  
  
#### <a name="data-conversion-operators-in-the-filter-predicate"></a>Datenkonvertierungsoperatoren im Filterprädikat  
 Wenn der im gefilterten Indexausdruck der gefilterten Indexergebnisse angegebene Vergleichsoperator eine implizite oder explizite Datenkonvertierung ergibt, kommt es zu einem Fehler, wenn die Konvertierung auf der linken Seite eines Vergleichsoperators auftritt. Eine mögliche Lösung besteht darin, den gefilterten Indexausdruck mit dem Datenkonvertierungsoperator (CAST oder CONVERT) auf die rechte Seite des Vergleichsoperators zu schreiben.  
  
 Im folgenden Beispiel wird eine Tabelle mit einer Vielzahl von Datentypen erstellt.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.TestTable (a int, b varbinary(4));  
  
```  
  
 In der folgenden Definition des gefilterten Indexes wird die Spalte `b` implizit in einen ganzzahligen Datentyp konvertiert, um sie mit der Konstante 1 vergleichen zu können. Dadurch wird die Fehlermeldung 10611 erzeugt, da die Konvertierung auf der linken Seite des Operators im gefilterten Prädikat auftritt.  
  
```  
CREATE NONCLUSTERED INDEX TestTabIndex ON dbo.TestTable(a,b)  
WHERE b = 1;  
```  
  
 Die Lösung besteht darin, die Konstante auf der rechten Seite zu konvertieren, damit diese vom gleichen Typ ist wie Spalte `b`, wie aus dem folgenden Beispiel hervorgeht:  
  
```  
CREATE INDEX TestTabIndex ON dbo.TestTable(a,b)  
WHERE b = CONVERT(Varbinary(4), 1);  
```  
  
 Durch das Verschieben der Datenkonvertierung von der linken Seite auf die rechte Seite eines Vergleichsoperators wird möglicherweise die Bedeutung der Konvertierung geändert. Im obigen Beispiel wurde aus einem Integer-Vergleich ein **varbinary** -Vergleich, als der CONVERT-Operator der rechten Seite hinzugefügt wurde.  
  
  
##  <a name="Additional_Reading"></a> Zusätzliches Lesematerial  
[Verbessern der Leistung mit indizierten Sichten in SQL Server 2008](http://msdn.microsoft.com/library/dd171921(v=sql.100).aspx)  
[Partitioned Tables and Indexes](../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  


