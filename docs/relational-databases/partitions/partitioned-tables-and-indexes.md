---
title: Partitionierte Tabellen und Indizes | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/20/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-partition
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitioned tables [SQL Server], about partitioned tables
- partitioned indexes [SQL Server], architecture
- partitioned tables [SQL Server], architecture
- partitioned indexes [SQL Server], about partitioned indexes
ms.assetid: cc5bf181-18a0-44d5-8bd7-8060d227c927
caps.latest.revision: "48"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 85ad3feb00088d3a0d8fa6095b241cc9f07c1c13
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="partitioned-tables-and-indexes"></a>Partitionierte Tabellen und Indizes
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die Tabellen- und Indexpartitionierung. Die Daten partitionierter Tabellen und Indizes werden in Einheiten aufgeteilt, die über mehrere Dateigruppen in einer Datenbank verteilt sein können. Die Daten werden horizontal partitioniert, sodass Gruppen von Zeilen einzelnen Partitionen zugeordnet werden. Alle Partitionen eines einzelnen Indexes oder einer Tabelle müssen sich in der gleichen Datenbank befinden. Die Tabelle oder der Index wird als einzelne logische Entität behandelt, wenn Abfragen oder Aktualisierungen für die Daten ausgeführt werden. Vor [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 waren partitionierte Tabellen und Indizes nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen für den SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützt standardmäßig bis zu 15.000 Partitionen. In Versionen vor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]war die Anzahl der Partitionen standardmäßig auf 1.000 beschränkt. Auf x86-basierten Systemen ist das Erstellen einer Tabelle oder eines Index mit mehr als 1000 möglich, wird jedoch nicht unterstützt.  
  
## <a name="benefits-of-partitioning"></a>Vorteile der Partitionierung  
 Das Partitionieren großer Tabellen oder Indizes kann die folgenden Vorteile bei der Verwaltung und Leistung haben.  
  
-   Sie können Teilmengen von Daten schnell und effizient übertragen und darauf zugreifen, während die Integrität der Datensammlung erhalten bleibt. So dauert beispielsweise ein Vorgang wie das Laden von Daten von einem OLTP-System in ein OLAP-System nur Sekunden, statt Minuten und Stunden, wenn die Daten nicht partitioniert sind.  
  
-   Sie können Wartungsvorgänge für eine oder mehrere Partitionen schneller ausführen. Die Vorgänge sind effizienter, da sie auf nur diese Datenteilmengen abzielen, statt auf die ganze Tabelle. Sie können z. B. wählen, Daten in einer oder mehreren Partitionen zu komprimieren oder eine oder mehrere Partitionen eines Indexes neu zu erstellen.  
  
-   Die Abfrageleistung lässt sich, abhängig von den am häufigsten ausgeführten Abfragetypen sowie der Hardwarekonfiguration, möglicherweise verbessern. So kann der Abfrageoptimierer zum Beispiel Gleichheitsjoin-Abfragen zwischen zwei oder mehr partitionierten Tabellen schneller verarbeiten, wenn die Partitionierungsspalten in den Tabellen identisch sind, da die Partitionen selbst verbunden sein können.  
  
     Beim Sortieren von Daten nach E-A-Operationen geht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zunächst nach Partitionen vor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] greift jeweils auf ein Laufwerk zu, wodurch sich die Leistung möglicherweise verringert. Um die Leistung beim Sortieren von Daten zu verbessern, verteilen Sie die Datendateien der Partitionen über mehrere Datenträger, d. h. durch das Einrichten eines RAID (Redundant Array of Independent Disks). Auf diese Weise kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , obwohl die Daten dabei weiterhin nach Partitionen sortiert werden, auf alle Laufwerke der einzelnen Partitionen gleichzeitig zugreifen.  
  
     Darüber hinaus kann die Leistung verbessert werden, indem eine Sperrenausweitung auf Partitionsebene statt auf die gesamte Tabelle angewendet wird. Dies kann Sperrenkonflikte für die Tabelle reduzieren.  
  
## <a name="components-and-concepts"></a>Komponenten und Konzepte  
 Die folgenden Begriffe beziehen sich auf die Tabellen- und Indexpartitionierung.  
  
 Partitionsfunktion  
 Ein Datenbankobjekt, das definiert, wie die Zeilen einer Tabelle oder eines Index basierend auf den Werten bestimmter Spalten, den sogenannten Partitionierungsspalten, einem Satz von Partitionen zugeordnet werden. Das heißt, die Partitionsfunktion definiert die Anzahl von Partitionen, über die die Tabelle verfügt, und wie die Begrenzungen der Partitionen definiert werden. Angenommen, Sie verfügen über eine Tabelle, die Verkaufsauftragsdaten enthält, und möchten die Tabelle möglicherweise in zwölf (monatliche) Partitionen auf Grundlage einer **datetime** -Spalte (z.B. Verkaufsdatum) partitionieren.  
  
 Partitionsschema  
 Ein Datenbankobjekt, das die Partitionen einer Partitionsfunktion Dateigruppen zuordnet. Der wichtigste Grund dafür, dass Partitionen in separaten Dateigruppen platziert werden, besteht darin, sicherzustellen, dass Sie Sicherungsvorgänge unabhängig für Partitionen ausführen können. Dies liegt daran, dass Sie Sicherungen für einzelne Dateigruppen ausführen können.  
  
 Partitionierungsspalte  
 Die Spalte einer Tabelle oder eines Indexes, die von einer Partitionsfunktion zum Partitionieren der Tabelle oder des Indexes verwendet wird. Berechnete Spalten, die in eine Partitionsfunktion einbezogen werden, müssen explizit als PERSISTED gekennzeichnet sein. Alle Datentypen, die zum Verwenden als Indexspalten zulässig sind, können als Partitionsspalte verwenden werden, mit Ausnahme des Datentyps **timestamp**. Die Datentypen **ntext**-, **text**-, **image**-, **xml**-, **varchar(max)**-, **nvarchar(max)**oder **varbinary(max)** können nicht angegeben werden. Zudem können der benutzerdefinierte CLR-Typ (Common Language Runtime) von Microsoft .NET Framework und die Spalten mit dem Aliasdatentyp nicht angegeben werden.  
  
 Ausgerichteter Index  
 Ein Index, der auf dem gleichen Partitionsschema wie die zugehörige Tabelle aufbaut. Wenn eine Tabelle und ihre Indizes aneinander ausgerichtet sind, kann SQL Server schnell zwischen Partitionen wechseln und gleichzeitig die Partitionsstruktur sowohl der Tabelle als auch ihrer Indizes beibehalten. Ein Index muss nicht an derselben benannten Partitionsfunktion beteiligt sein, um an ihrer Basistabelle ausgerichtet zu sein. Allerdings muss die Partitionsfunktion des Indexes und der Basistabelle im Wesentlichen übereinstimmen, und zwar dahingehend, dass 1) die Argumente der Partitionsfunktionen denselben Datentyp haben, dass sie 2) dieselbe Anzahl von Partitionen definieren und dass sie 3) dieselben Begrenzungswerte für Partitionen definieren.  
  
 Nicht ausgerichteter Index  
 Ein Index, der unabhängig von der zugehörigen Tabelle partitioniert ist. Das heißt, der Index hat ein anderes Partitionsschema oder wird in einer anderen Dateigruppe als die Basistabelle platziert. Das Entwerfen eines nicht ausgerichteten partitionierten Index kann in den folgenden Fällen nützlich sein:  
  
-   Die Basistabelle ist nicht partitioniert.  
  
-   Der Indexschlüssel ist eindeutig und enthält nicht die Partitionierungsspalte der Tabelle.  
  
-   Sie möchten die Basistabelle an angeordneten Joins mit weiteren Tabellen beteiligen, die unterschiedliche Joinspalten verwenden.  

 Partitionsentfernung: Der Prozess, durch den der Abfrageoptimierer nur auf relevante Partitionen zugreift, um die Filterkriterien der Abfrage zu erfüllen.  
  
## <a name="performance-guidelines"></a>Leistungsrichtlinien  
 Die neue, höhere Grenze von 15.000 Partitionen wirkt sich auf den Arbeitsspeicher, Vorgänge mit partitionierten Indizes, DBCC-Befehle und Abfragen aus. In diesem Abschnitt werden die Auswirkungen auf die Leistung beschrieben, wenn die Anzahl der Partitionen mehr als 1.000 beträgt, und es werden mögliche Problemumgehungen bereitgestellt. Dadurch, dass die maximale Anzahl von Partitionen auf 15.000 erhöht wurde, können Sie Daten über einen längeren Zeitraum speichern. Sie sollten Daten jedoch nur so lange beibehalten, wie sie benötigt werden, und darauf achten, dass die Leistung und die Anzahl der Partitionen ausgewogen ist.  
  
### <a name="processor-cores-and-number-of-partitions-guidelines"></a>Richtlinien für Prozessorkerne und die Anzahl der Partitionen  
 Zur Maximierung der Leistung paralleler Vorgänge wird empfohlen, die gleiche Anzahl von Partitionen und Prozessorkernen und bis zu einem Maximum von 64 zu verwenden (was die maximal zulässige Anzahl paralleler Prozessoren ist, die SQL Server nutzen kann).  
  
### <a name="memory-usage-and-guidelines"></a>Speicherauslastung und Richtlinien  
 Es empfiehlt sich, mindestens 16 GB Arbeitsspeicher zu verwenden, wenn eine große Anzahl von Partitionen verwendet wird. Wenn das System nicht über ausreichend Arbeitsspeicher verfügt, kann es bei DML-Anweisungen (Datenbearbeitungssprache), DDL-Anweisungen (Datendefinitionssprache) und anderen Vorgängen aufgrund ungenügenden Arbeitsspeichers zu Fehlern kommen. Bei Systemen mit 16 GB Arbeitsspeicher, die zahlreiche speicherintensive Prozesse ausführen, kann es bei Vorgängen, die für eine große Anzahl von Partitionen ausgeführt werden, zu Fehlern aufgrund von Speicherauslastung kommen. Je mehr Arbeitsspeicher Sie über die empfohlenen 16 GB hinaus verwenden, desto geringer ist die Wahrscheinlichkeit, dass Probleme mit der Leistung und Speicherauslastung auftreten.  
  
 Einschränkungen beim Arbeitsspeicher können sich negativ auf die Leistung oder auf die Möglichkeit von SQL Server zum Erstellen eines partitionierten Index auswirken. Das gilt insbesondere für den Fall, wenn der Index nicht an seiner Basistabelle oder an deren gruppierten Index ausgerichtet ist, sofern für die Tabelle bereits ein gruppierter Index erstellt wurde.  
  
### <a name="partitioned-index-operations"></a>Vorgänge für partitionierte Indizes  
 Einschränkungen beim Arbeitsspeicher können sich negativ auf die Leistung oder auf die Möglichkeit von SQL Server zum Erstellen eines partitionierten Index auswirken. Dies ist insbesondere bei nicht ausgerichteten Indizes der Fall. Das Erstellen bzw. Neuerstellen von nicht ausgerichteten Indizes für eine Tabelle mit mehr als 1.000 Partitionen ist möglich, wird aber nicht unterstützt. Dies hätte Leistungseinbußen oder eine zu hohe Speicherauslastung während der Vorgänge zur Folge.  
  
 Das Erstellen und Neuerstellen von ausgrichteten Indizes kann um so länger dauern, je mehr Partitionen hinzugefügt werden. Es empfiehlt sich, nicht mehrere Befehle zum Erstellen und Neuerstellen von Befehlen gleichzeitig auszuführen, da es zu Leistungs- und Arbeitsspeicherproblemen kommen kann.  
  
 Wenn SQL Server Sortiervorgänge zum Erstellen partitionierter Indizes durchführt, wird zuerst eine Sortiertabelle für jede Partition erstellt. Anschließend erstellt es die Sortiertabellen entweder in der jeweiligen Dateigruppe jeder Partition oder in **tempdb**, wenn die SORT_IN_TEMPDB-Indexoption angegeben wurde. Jede Sortiertabelle setzt für ihre Erstellung eine Mindestmenge an Arbeitsspeicher voraus. Wenn Sie einen partitionierten Index erstellen, der an seiner Basistabelle ausgerichtet ist, werden alle Sortiertabellen nacheinander erstellt, was weniger Arbeitsspeicher in Anspruch nimmt. Wenn Sie allerdings einen nicht gruppierten partitionierten Index erstellen, werden alle Sortiertabellen gleichzeitig erstellt. Das heißt, es muss ausreichend Arbeitsspeicher verfügbar sein, um diese gleichzeitigen Sortiervorgänge zu verarbeiten. Je größer die Anzahl der Partitionen, desto mehr Arbeitsspeicher wird benötigt. Die Mindestgröße für jede Sortiertabelle beträgt 40 Seiten für jede Partition mit 8 Kilobyte pro Seite. So beansprucht z.&nbsp;B. ein nicht ausgerichteter partitionierter Index mit 100 Partitionen ausreichend Arbeitsspeicher, um 4.000 (40 * 100) Seiten gleichzeitig seriell sortieren zu können. Wenn dieser Arbeitsspeicher verfügbar ist, ist die Erstellung zwar erfolgreich, jedoch kann die Leistung darunter leiden. Wenn dieser Arbeitsspeicher nicht verfügbar ist, schlägt die Erstellung fehl. Alternativ erfordert ein ausgerichteter partitionierter Index mit 100 Partitionen nur ausreichend Arbeitsspeicher, um 40 Seiten zu sortieren, da die Sortiervorgänge nicht gleichzeitig durchgeführt werden.  
  
 Sowohl bei ausgerichteten als auch bei nicht ausgerichteten Indizes kann der Arbeitsspeicherbedarf noch höher sein, wenn SQL Server bei einem Computer mit mehreren Prozessoren Grade der Parallelität beim Erstellungsvorgang verwendet. Denn je höher die Grade der Parallelität sind, desto größer ist auch der Arbeitsspeicherbedarf. Wenn SQL Server z. B. die Grade der Parallelität auf 4 festlegt, benötigt ein nicht ausgerichteter partitionierter Index mit 100 Partitionen ausreichend Arbeitsspeicher, damit vier Prozessoren gleichzeitig jeweils 4.000 Seiten sortieren können – also 16.000 Seiten gleichzeitig. Wenn der partitionierte Index ausgerichtet ist, verringert sich der Arbeitsspeicherbedarf auf vier Prozessoren, die jeweils 40 Seiten sortieren – also 160 (4 * 40) Seiten. Sie können die MAXDOP-Indexoption verwenden, um die Grade der Parallelität manuell zu reduzieren.  
  
### <a name="dbcc-commands"></a>DBCC-Befehle  
 Bei einer größeren Anzahl von Partitionen können DBCC-Befehle mehr Zeit für die Ausführung in Anspruch nehmen, während sich die Anzahl von Partitionen erhöht.  
  
### <a name="queries"></a>Abfragen  
 Abfragen, die Partitionsentfernung verwenden, weisen eine vergleichbare oder verbesserte Leistung bei einer größeren Anzahl von Partitionen auf. Abfragen, die keine Partitionsentfernung verwenden, nehmen mehr Zeit für die Ausführung in Anspruch, wenn sich die Anzahl der Partitionen erhöht.  
  
 Nehmen Sie beispielsweise an, eine Tabelle hat 100 Millionen Zeilen und Spalten `A`, `B`und `C`. In Szenario 1 ist die Tabelle in 1000 Partitionen der Spalte `A`unterteilt. In Szenario 2 ist die Tabelle in 10.000 Partitionen der Spalte `A`unterteilt. Eine Abfrage der Tabelle, die über eine WHERE-Klausel verfügt, die nach Spalte `A` filtert, führt die Partitionsentfernung aus und scannt eine Partition. Die gleiche Abfrage wird in Szenario 2 möglicherweise schneller ausgeführt, da es weniger zu scannende Zeilen in einer Partition gibt. Eine Abfrage, die über eine WHERE-Klausel verfügt, die nach Spalte B filtert, scannt alle Partitionen. Die Abfrage wird möglicherweise in Szenario 1 schneller als in Szenario 2 ausgeführt, da weniger Partitionen gescannt werden müssen.  
  
 Abfragen, die Operatoren wie TOP oder MAX/MIN für andere Spalten als die Partitionierungsspalte verwenden, erzielen aufgrund der Partitionierung möglicherweise eine geringere Leistung, da alle Partitionen ausgewertet werden müssen.  
  
## <a name="behavior-changes-in-statistics-computation-during-partitioned-index-operations"></a>Das Verhalten ändert sich beim Berechnen von Statistiken, während Vorgänge für partitionierte Indizes durchgeführt werden  
 Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]werden Statistiken nicht durch das Scannen aller Zeilen in der Tabelle erstellt, wenn ein partitionierter Index erstellt oder neu erstellt wird. Der Abfrageoptimierer generiert stattdessen Statistiken mithilfe des Standardalgorithmus zur Stichprobenentnahme. Nachdem eine Datenbank mit partitionierten Indizes aktualisiert wurde, bemerken Sie möglicherweise einen Unterschied in den Histogrammdaten für diese Indizes. Diese Änderung des Verhaltens beeinträchtigt die Abfrageleistung möglicherweise nicht. Um Statistiken zu partitionierten Indizes durch das Scannen aller Zeilen in der Tabelle abzurufen, verwenden Sie CREATE STATISTICS oder UPDATE STATISTICS mit der FULLSCAN-Klausel.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|||  
|-|-|  
|**Aufgaben**|**Thema**|  
|Beschreibt das Erstellen von Partitionsfunktionen und Partitionsschemas sowie deren Anwendung auf eine Tabelle und einen Index.|[Erstellen partitionierter Tabellen und Indizes](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)|  
|||  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Die folgenden Whitepaper zu partitionierten Tabellen und Indexstrategien sowie Implementierungen sind möglicherweise für Sie interessant.  
  
-   [Partitionierte Tabellen- und Indexstrategien für SQL Server 2008](http://msdn.microsoft.com/library/dd578580\(SQL.100\).aspx)  
  
-   [So implementieren Sie ein automatisch gleitendes Fenster](http://msdn.microsoft.com/library/aa964122\(SQL.90\).aspx)  
  
-   [Massenladen in eine partitionierte Tabelle](http://msdn.microsoft.com/library/cc966380.aspx)  
  
-   [Project REAL: Data Lifecycle -- Partitionierung](https://technet.microsoft.com/library/cc966424.aspx)  
  
-   [Verbesserte Abfrageverarbeitung bei partitionierten Tabellen und Indizes](http://msdn.microsoft.com/library/ms345599.aspx)  
  
-   [Top 10 Best Practices zum Erstellen von einem umfassenden relationalen Data Warehouse](http://sqlcat.com/top10lists/archive/2008/02/06/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse.aspx)  
  
  
