---
title: "Einführung in speicheroptimierte Tabellen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 12/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ef1cc7de-63be-4fa3-a622-6d93b440e3ac
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0b3da20931446202987e7dde901f01f8d4902a79
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="introduction-to-memory-optimized-tables"></a>Einführung in speicheroptimierte Tabellen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Speicheroptimierte Tabellen werden mit [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) erstellt.  
  
 Speicheroptimierte Tabellen sind standardmäßig vollständig dauerhaft und bieten, wie Transaktionen in (herkömmlichen) datenträgerbasierten Tabellen, vollständige ACID-Eigenschaften (Atomarität, Konsistenz, Isolation, Dauerhaftigkeit). Speicheroptimierte Tabellen und nativ kompilierte gespeicherte Prozeduren unterstützen nur einen Teil der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Features.
 
Ab SQL Server 2016 und in der Azure SQL-Datenbank gibt es keine Einschränkungen für [Sortierungen oder Codepages](../../relational-databases/collations/collation-and-unicode-support.md) , die spezifisch für In-Memory OLTP sind.
  
 Beim Primärspeicher für speicheroptimierte Tabellen handelt es sich um den Hauptspeicher. Zeilen in der Tabelle werden aus dem Arbeitsspeicher gelesen und in diesen geschrieben. Eine zweite Kopie der Tabellendaten wird auf Festplatte gespeichert, aber nur zu Dauerhaftigkeitszwecken. Weitere Informationen zu dauerhaften Tabellen finden Sie unter [Erstellen und Verwalten von Speicher für arbeitsspeicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md) . Daten in speicheroptimierten Tabellen werden nur während der Datenbankwiederherstellung vom Datenträger gelesen (z.B. nach einem Serverneustart).  
  
 Noch deutlichere Leistungsverbesserungen werden bei In-Memory OLTP durch die Unterstützung von dauerhaften Tabellen mit verzögerter Transaktionsdauerhaftigkeit erzielt. Verzögerte dauerhafte Transaktionen werden kurz nach dem Commit der Transaktion und nach der Rückgabe der Steuerung an den Client auf dem Datenträger gespeichert. Im Austausch für die höhere Leistung besteht die Gefahr, dass Transaktionen, die noch nicht auf dem Datenträger gespeichert wurden, bei einem Absturz oder Failover des Servers verloren gehen.  
  
 Neben den standardmäßig dauerhaften speicheroptimierten Tabellen unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auch nicht dauerhafte speicheroptimierte Tabellen, die nicht protokolliert und deren Daten nicht auf dem Datenträger beibehalten werden. Das bedeutet, dass Transaktionen in diesen Tabellen keine Datenträger-E/A-Vorgänge erfordern, die Daten aber bei einem Serverabsturz oder einem Failover nicht wiederhergestellt werden können.  
  
 In-Memory OLTP ist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integriert, um in allen Bereichen wie Entwicklung, Bereitstellung, Verwaltbarkeit und Unterstützbarkeit eine reibungslose Benutzererfahrung zu ermöglichen. Eine Datenbank kann speicherinterne wie auch datenträgerbasierte Objekte enthalten.  
  
 Für Zeilen in speicheroptimierten Tabellen wird die Versionsverwaltung verwendet. Dies bedeutet, dass für jede Zeile in der Tabelle möglicherweise mehrere Versionen vorliegen. Alle Zeilenversionen werden in derselben Tabellendatenstruktur verwaltet. Die Zeilenversionsverwaltung wird verwendet, um gleichzeitige Lese- und Schreibvorgänge für dieselbe Zeile zuzulassen. Weitere Informationen zu gleichzeitigen Lese- und Schreibvorgängen für die gleiche Zeile finden Sie unter [Transactions with Memory-Optimized Tables](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)(Transaktionen mit speicheroptimierten Tabellen).  
  
 Die folgende Abbildung veranschaulicht die Multiversionsverwaltung. Die Abbildung zeigt eine Tabelle mit drei Zeilen, und jede Zeile weist unterschiedliche Versionen auf.  
  
![Multiversionsverwaltung.](../../relational-databases/in-memory-oltp/media/hekaton-tables-1.gif "Multi-versioning.")  
  
 Die Tabelle enthält drei Zeilen: r1, r2 und r3. r1 verfügt über drei Versionen, r2 über zwei Versionen und r3 über vier Versionen. Beachten Sie, dass unterschiedliche Versionen derselben Zeile nicht unbedingt aufeinander folgende Speicheradressen belegen. Die unterschiedlichen Zielversionen können über die Tabellendatenstruktur verteilt sein.  
  
 Die speicheroptimierte Tabellendatenstruktur kann als Auflistung von Zeilenversionen gesehen werden. Während Zeilen in datenträgerbasierten Tabellen in Seiten und Blöcken angeordnet sind und einzelne Zeilen mithilfe der Seitenzahl und des Seitenoffsets adressiert werden, werden Zeilenversionen in speicheroptimierten Tabellen mithilfe von 8-Byte-Speicherzeigern adressiert.  
  
 Der Datenzugriff in speicheroptimierten Tabellen erfolgt auf zwei Arten:  
  
-   Durch systemintern kompilierte gespeicherte Prozeduren  
  
-   Durch interpretiertes [!INCLUDE[tsql](../../includes/tsql-md.md)], außerhalb einer systemintern kompilierten gespeicherten Prozedur. Diese [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen können sich entweder in interpretierten gespeicherten Prozeduren befinden oder als Ad-hoc- [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen vorliegen.  
  
## <a name="accessing-data-in-memory-optimized-tables"></a>Zugriff auf Daten in speicheroptimierten Tabellen  

Auf speicheroptimierte Tabellen kann am effizientesten mit systemintern kompilierten gespeicherten Prozeduren ([Systemintern kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)) zugegriffen werden. Auf speicheroptimierte Tabellen kann außerdem mit (herkömmlichem) interpretiertem [!INCLUDE[tsql](../../includes/tsql-md.md)]zugegriffen werden. "Interpretiertes [!INCLUDE[tsql](../../includes/tsql-md.md)] " bezieht sich auf den Zugriff auf speicheroptimierte Tabellen ohne eine systemintern kompilierte gespeicherte Prozedur. Beispiele für den Zugriff auf interpretiertes [!INCLUDE[tsql](../../includes/tsql-md.md)] sind der Zugriff auf eine speicheroptimierte Tabelle über einen DML-Trigger, einen Ad-Hoc- [!INCLUDE[tsql](../../includes/tsql-md.md)] -Batch, eine Sicht und eine Tabellenwertfunktion.  
  
 In der folgenden Tabelle wird der systemeigene und interpretierte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff für verschiedene Objekte zusammengefasst.  
  
|Funktion|Zugriff mithilfe einer systemintern kompilierten gespeicherten Prozedur|Interpretierter [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff|CLR-Zugriff|  
|-------------|-------------------------------------------------------|-------------------------------------------|----------------|  
|Speicheroptimierte Tabelle|ja|ja|Nein*|  
|Speicheroptimierter Tabellentyp|ja|ja|Nein|  
|Systemintern kompilierte gespeicherte Prozedur|Das Schachteln von systemintern kompilierten gespeicherten Prozeduren wird jetzt unterstützt. Sie können in gespeicherten Prozeduren die EXECUTE-Syntax verwenden, solange die Prozedur, auf die verwiesen wird, ebenfalls systemintern kompiliert wird.|ja|Nein*|  
  
 *Sie können auf eine speicheroptimierte Tabelle oder eine systemintern kompilierte gespeicherte Prozedur nicht über die Kontextverbindung (die Verbindung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , wenn ein CLR-Modul ausgeführt wird) zugreifen. Sie können jedoch eine andere Verbindung erstellen und öffnen, über die Sie auf speicheroptimierte Tabellen und systemintern kompilierte gespeicherte Prozeduren zugreifen können.  
  
## <a name="performance-and-scalability"></a>Leistung und Skalierbarkeit  

Die folgenden Faktoren beeinflussen die Leistungsvorteile, die mit In-Memory OLTP erreicht werden können:  
  
*Kommunikation:* Eine Anwendung mit vielen Aufrufen kurzer gespeicherter Prozeduren erzielt möglicherweise einen kleineren Leistungszuwachs als eine Anwendung, bei der weniger Aufrufe und zusätzliche Funktionen in jeder gespeicherten Prozedur implementiert sind.  
  
*[!INCLUDE[tsql](../../includes/tsql-md.md)] -Ausführung:* In-Memory OLTP gewährleistet die beste Leistung bei systemintern kompilierten gespeicherten Prozeduren im Gegensatz zu interpretierten gespeicherten Prozeduren oder Abfrageausführungen. Dies kann einen Vorteil gegenüber dem Zugriff auf speicheroptimierte Tabellen aus solchen gespeicherten Prozeduren bieten.  
  
*Bereichsscan im Vergleich zu Punktsuche:* Speicheroptimierte, nicht gruppierte Indizes unterstützen Bereichsscans und sortierte Scans. Bei Punktsuchen erzielen Sie mit speicheroptimierten Hashindizes eine bessere Leistung als mit speicheroptimierten, nicht gruppierten Indizes. Speicheroptimierte, nicht gruppierte Indizes weisen eine bessere Leistung auf als datenträgerbasierte Indizes.

- Ab SQL Server 2016 kann der Abfrageplan für eine speicheroptimierte Tabelle die Tabelle parallel scannen. Dies verbessert die Leistung von Analyseabfragen.
  - Hashindizes können seit SQL Server 2016 auch parallel gescannt werden.
  - Nicht gruppierte Indizes können seit SQL Server 2016 auch parallel gescannt werden.
  - Columnstore-Indizes können seit ihrer Einführung in SQL Server 2014 parallel gescannt werden.
  
*Indexvorgänge:* Indexvorgänge werden nicht protokolliert und sind nur im Arbeitsspeicher vorhanden.  
  
*Parallelität:* Anwendungen, deren Leistung durch Parallelität auf Modulebene wie Latchkonflikte oder Blockierungen beeinträchtigt wird, verzeichnen eine erhebliche Leistungssteigerung, wenn die Anwendung auf In-Memory OLTP umgestellt wird.  
  
In der folgenden Tabelle werden die Leistungs- und Skalierbarkeitsprobleme, die häufig in relationalen Datenbanken auftreten, zusammen mit einer möglichen Leistungssteigerung durch In-Memory OLTP aufgeführt.  
  
|Problem|Einfluss durch In-Memory OLTP|  
|-----------|----------------------------|  
|Leistung<br /><br /> Intensive Ressourcennutzung (CPU, E/A, Netzwerk oder Arbeitsspeicher)|CPU<br /> Durch systemintern kompilierte gespeicherte Prozeduren kann die CPU-Nutzung erheblich gesenkt werden, da sie deutlich weniger Anweisungen als interpretierte gespeicherte Prozeduren benötigen, um eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung auszuführen.<br /><br /> In-Memory OLTP kann die erforderlichen Hardwareinvestitionen bei horizontal skalierten Arbeitsauslastungen reduzieren, da ein Server so potenziell den Durchsatz von fünf bis 10 Servern erzielen kann.<br /><br /> E/A<br /> Wenn bei der Verarbeitung ein E/A-Engpass aufgrund der Verarbeitung von Daten oder Indexseiten auftritt, lässt sich dieser durch In-Memory OLTP u. U. reduzieren. Zudem wird der Prüfpunktalgorithmus von In-Memory OLTP-Objekten kontinuierlich durchgeführt und führt nicht zu einem plötzlichen Anstieg von E/A-Vorgängen. Wenn jedoch das Workingset der leistungskritischen Tabellen zu groß für den Arbeitsspeicher ist, steigert In-Memory OLTP nicht die Leistung, da dieser Datenbanktyp speicherresidente Daten benötigt. Wenn bei der Protokollierung ein E/A-Engpass auftritt, kann In-Memory OLTP diesen Engpass verringern, da weniger Protokollierungsaktivität durchgeführt wird. Wenn eine oder mehrere speicheroptimierte Tabellen als nicht dauerhafte Tabellen konfiguriert sind, können Sie dadurch die Protokollierung für Daten eliminieren.<br /><br /> Speicher<br /> In-Memory OLTP bietet keine Leistungssteigerung. In-Memory OLTP kann den Arbeitsspeicher zusätzlich belasten, da die Objekte speicherresident sein müssen.<br /><br /> Netzwerk<br /> In-Memory OLTP bietet keine Leistungssteigerung. Die Daten müssen von der Datenebene an die Anwendungsebene übertragen werden.|  
|Skalierbarkeit<br /><br /> Die meisten Skalierungsprobleme bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anwendungen werden durch Parallelitätsprobleme wie Konflikten bei Sperren, Latches und Spinlocks verursacht.|Latchkonflikte<br /> Ein typisches Szenario ist ein Konflikt auf der letzten Seite eines Indexes, wenn Zeilen gleichzeitig in Schlüsselreihenfolge einfügt werden. Da In-Memory OLTP beim Datenzugriff keine Latches verwendet, werden Skalierbarkeitsprobleme aufgrund von Latchkonflikten vollständig eliminiert.<br /><br /> Spinlock-Konflikt<br /> Da In-Memory OLTP beim Datenzugriff keine Latches verwendet, werden Skalierbarkeitsprobleme aufgrund von Spinlock-Konflikten vollständig eliminiert.<br /><br /> Konflikte aufgrund von Sperren<br /> Wenn in der Datenbankanwendung Blockierungen zwischen Lese- und Schreibvorgängen auftreten, werden diese Blockierungsprobleme durch In-Memory OLTP beseitigt, da es eine neue Art der optimistischen Nebenläufigkeitssteuerung für die Implementierung der Transaktionsisolationsstufen verwendet. In-Memory OLTP verwendet nicht TempDB, um Zeilenversionen zu speichern.<br /><br /> Wenn das Skalierungsproblem durch einen Konflikt zwischen zwei Schreibvorgängen verursacht wird, etwa zwei Transaktionen, die gleichzeitig dieselbe Zeile zu aktualisieren versuchen, führt In-Memory OLTP eine Transaktion erfolgreich durch und beendet die andere. Die fehlgeschlagene Transaktion muss zur Wiederholung explizit oder implizit erneut gesendet werden. In beiden Fällen müssen Sie Änderungen an der Anwendung vornehmen.<br /><br /> Wenn in der Anwendung häufig Konflikte zwischen zwei Schreibvorgängen auftreten, wird der Wert der optimistischen Sperre verringert. Die Anwendung ist für In-Memory OLTP nicht geeignet. Die meisten OLTP-Anwendungen weisen keine Schreibkonflikte auf, sofern diese nicht durch Sperrenausweitung verursacht werden.|  
  
##  <a name="rls"></a> Sicherheit auf Zeilenebene in speicheroptimierten Tabellen  

[Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md) wird für speicheroptimierte Tabellen unterstützt. Richtlinien für die Sicherheit auf Zeilenebene werden auf speicheroptimierte Tabellen im Wesentlichen auf die gleiche Weise wie auf datenträgerbasierte Tabellen angewendet. Der einzige Unterschied ist, dass die als Sicherheitsprädikate verwendeten Inline-Tabellenwertfunktionen systemintern kompiliert (mit der Option WITH NATIVE_COMPILATION erstellt) werden müssen. Weitere Informationen finden Sie unter [Row-Level Security](../../relational-databases/security/row-level-security.md#Limitations) (Sicherheit auf Zeilenebene) im Abschnitt [Cross-Feature Compatibility](../../relational-databases/security/row-level-security.md) (Funktionsübergreifende Kompatibilität).  
  
 Für speicherinterne Tabellen wurden verschiedene integrierte Sicherheitsfunktionen aktiviert, die für Sicherheit auf Zeilenebene wesentlich sind. Weitere Informationen finden Sie unter [Integrierte Funktionen in nativ kompilierten Modulen](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#bfncsp).  
  
 **EXECUTE AS CALLER:** Alle nativen Module unterstützen und verwenden jetzt standardmäßig EXECUTE AS CALLER, auch ohne entsprechenden Hinweis. Der Grund dafür ist, dass von allen Sicherheitsprädikatfunktionen auf Zeilenebene die Verwendung von EXECUTE AS CALLER erwartet wird, sodass die Funktion (und alle integrierten Funktionen, die in ihr verwendet werden) im Kontext des aufrufenden Benutzers ausgewertet wird.   
EXECUTE AS CALLER ist mit einer geringen Leistungseinbuße (ungefähr 10 %) verbunden, die durch das Überprüfen der Berechtigung des Aufrufers verursacht wird. Wenn das Modul explizit EXECUTE AS OWNER oder EXECUTE AS SELF angibt, werden diese Berechtigungsüberprüfungen und die entsprechenden Leistungseinbußen vermieden. Wenn jedoch eine dieser Optionen zusammen mit den oben beschriebenen integrierten Funktionen verwendet wird, kommt es aufgrund des erforderlichen Kontextwechsels zu einer erheblich höheren Leistungseinbuße.  
  
## <a name="scenarios"></a>Szenarien

Eine kurze Erläuterung typischer Szenarien, in denen die Leistung mit [!INCLUDE[hek_1](../../includes/hek-1-md.md)] verbessert werden kann, finden Sie unter [In-Memory OLTP](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Siehe auch

[In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
