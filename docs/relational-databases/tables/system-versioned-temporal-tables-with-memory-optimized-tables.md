---
title: Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 07/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 23274522-e5cf-4095-bed8-bf986d6342e0
caps.latest.revision: 16
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82ca8698bdefad9764b03b19a885b098c8421400
ms.lasthandoff: 04/11/2017

---
# <a name="system-versioned-temporal-tables-with-memory-optimized-tables"></a>Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Temporale Tabellen mit Systemversionsverwaltung für [speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) bieten eine kostengünstige Lösung für Szenarien, in denen zusätzlich zur Datensammlung mit In-Memory-OLTP-Arbeitsauslastungen [Datenüberwachung und Zeitpunktanalyse](http://msdn.microsoft.com/library/mt631669.aspx) erforderlich sind. Sie bieten hohen Transaktionsdurchsatz, sperrenfreie Parallelität und gleichzeitig die Möglichkeit, große Mengen von Verlaufsdaten zu speichern, die leicht abgefragt werden können.  
  
## <a name="overview"></a>Übersicht  
 Temporale Tabellen mit Systemversionsverwaltung speichern automatisch einen vollständigen Verlauf der Datenänderungen und stellen praktische Transact-SQL-Erweiterungen für die Zeitpunktanalyse zur Verfügung. Normalerweise wird der Datenverlauf für eine sehr lange Zeit beibehalten (mehrere Monate sogar Jahre), auch wenn er nicht regelmäßig abgefragt wird.  
  
 Datenüberwachung und zeitbasierte Analyse können in verschiedenen Umgebungen erforderlich sein, vor allem bei OLTP-Systemen, die eine sehr große Anzahl von Anforderungen verarbeiten und bei denen In-Memory-OLTP-Technologie verwendet wird. Die Verwendung speicheroptimierter Tabellen in temporalen Szenarien ist jedoch schwierig, da die riesige Menge an generierten historischen Daten häufig die Grenzen des verfügbaren RAM-Speichers überschreitet. Gleichzeitig ist es keine optimale Lösung, schreibgeschützte historische Daten, auf die mit zunehmendem Alter immer seltener zugegriffen wird, im RAM zu speichern.  
  
 Temporale Tabellen mit Systemversionsverwaltung für speicheroptimierte Tabellen ermöglichen einen hohen Transaktionsdurchsatz, sperrenfreie Parallelität und gleichzeitig die Möglichkeit, große Mengen von Verlaufsdaten zu speichern, da sie In-Memory-Tabellen zum Speichern von aktuellen Daten (die temporale Tabelle) und datenträgerbasierte Tabellen für historische Daten verwenden. Die Auswirkung auf DML-Vorgänge wird durch die Verwendung einer internen, automatisch generierten speicheroptimierten Stagingtabelle minimiert, die den aktuellen Verlauf speichert und ermöglicht, dass DMLs auf systemintern kompiliertem Code heraus ausgeführt werden können.  
  
 Das folgende Diagramm veranschaulicht diese Architektur. ![Temporale speicherinterne Architektur](../../relational-databases/tables/media/temporal-in-memory-architecture.png "Temporale speicherinterne Architektur")  
  
## <a name="implementation-details"></a>Implementierungsdetails  
 Die folgenden Fakten über temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen sind Aspekte, die Sie berücksichtigen sollten, wenn Sie eine speicheroptimierte Tabelle mit Systemversionsverwaltung erstellen. Syntaxoptionen und ein Beispiel finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
-   Nur dauerhafte speicheroptimierte Tabellen können der Systemversionsverwaltung unterliegen (**DURABILITY = SCHEMA_AND_DATA**).  
  
-   Die Verlaufstabelle für speicheroptimierte Tabellen mit Systemversionsverwaltung muss datenträgerbasiert sein, unabhängig davon, ob sie vom Endbenutzer oder vom System erstellt wurde.  
  
-   Abfragen, die nur die aktuelle (speicherinterne) Tabelle betreffen, können in [nativ kompilierten T-SQL-Modulen](https://msdnstage.redmond.corp.microsoft.com/en-us/library/dn133184.aspx)verwendet werden. Temporale Abfragen mit der Klausel FOR SYSTEM TIME werden in nativ kompilierten Modulen nicht unterstützt. In Ad-hoc-Abfragen und nicht nativen Modulen wird die Verwendung der Klausel FOR SYSTEM TIME mit speicheroptimierten Tabellen unterstützt.  
  
-   Wenn **SYSTEM_VERSIONING = ON**, wird automatisch eine interne speicheroptimierte Stagingtabelle erstellt, um die neuesten mit der Systemversionsverwaltung erfassten Änderungen, zu übernehmen, die das Ergebnis von Aktualisierungs- und Löschvorgängen in der aktuellen speicheroptimierten Tabelle sind.  
  
-   Daten aus der internen speicheroptimierten Stagingtabelle werden vom asynchronen Datenleerungstask regelmäßig in die datenträgerbasierte Verlaufstabelle verschoben. Dieser Datenleerungsmechanismus hat zum Ziel, die internen Speicherpuffer bei unter 10 % der Arbeitsspeichernutzung der übergeordneten Objekte zu halten. Sie können die gesamte Arbeitsspeichernutzung der speicheroptimierten temporalen Tabelle mit Systemversionsverwaltung nachhalten, indem Sie [sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md) abfragen und die Daten für die interne speicheroptimierte Stagingtabelle sowie die aktuelle temporale Tabelle zusammenfassen.  
  
-   Sie können eine Datenleerung erzwingen, indem Sie [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md) aufrufen.  
  
-   Wenn **SYSTEM_VERSIONING = OFF** oder wenn das Schema einer Tabelle mit Systemversionsverwaltung durch Hinzufügen, Löschen oder Ändern von Spalten geändert wurde, wird der gesamte Inhalt des internen Stagingpuffers in die datenträgerbasierte Verlaufstabelle verschoben.  
  
-   Das Abfragen von historischen Daten ist unter der SNAPSHOT-Isolationsstufe effektiv und gibt stets eine Vereinigung des In-Memory-Stagingpuffers und der datenträgerbasierten Tabelle ohne Duplikate zurück.   
  
-   **ALTER TABLE** -Vorgänge, die das Tabellenschema intern ändern, müssen eine Datenleerung ausführen, wodurch sich die Dauer des Vorgangs möglicherweise verlängert.  
  
## <a name="the-internal-memory-optimized-staging-table"></a>Die interne speicheroptimierte Stagingtabelle  
 Die interne speicheroptimierte Stagingtabelle ist ein internes Objekt, das vom System erstellt wird, um DML-Vorgänge zu optimieren.  
  
-   Der Tabellenname wird im folgenden Format generiert: **Memory_Optimized_History_Table_<object_id>**, wobei *<object_id>* der Bezeichner der aktuellen temporalen Tabelle ist.  
  
-   Die Tabelle repliziert das Schema der aktuellen temporalen Tabelle inklusive einer BIGINT-Spalte. Diese zusätzliche Spalte gewährleistet die Eindeutigkeit der in den internen Verlaufspuffer verschobenen Zeilen.  
  
-   Die zusätzliche Spalte weist das folgende Namensformat auf: **Change_ID[_<suffix>]**, wobei *_\<suffix>* optional hinzugefügt wird, falls die Tabelle bereits über eine *Change_ID*-Spalte verfügt.  
  
-   Die maximale Zeilengröße für eine speicheroptimierte Tabelle mit Systemversionsverwaltung wird aufgrund der zusätzlichen BIGINT-Spalte in der Stagingtabelle um 8 Bytes reduziert. Der neue Höchstwert ist jetzt 8052 Bytes.  
  
-   Die interne speicheroptimierte Stagingtabelle wird im Objekt-Explorer von SQL Server Management Studio nicht dargestellt.  
  
-   Metadaten für diese Tabelle sowie für die Verbindung mit der aktuellen temporalen Tabelle finden Sie unter [sys.internal_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md).  
  
## <a name="the-data-flush-task"></a>Der Datenleerungstask  
 Die Datenleerung ist ein regelmäßig aktivierter Tasks, der überprüft, ob eine speicheroptimierte Tabelle eine größenbasierte Arbeitsspeicherbedingung für das Verschieben von Daten erfüllt. Das Verschieben der Daten beginnt, wenn die Arbeitsspeichernutzung der internen Stagingtabelle 8 % der Arbeitsspeichernutzung der aktuellen temporalen Tabelle erreicht.  
  
 Der Datenleerungstask wird regelmäßig nach einem Zeitplan aktiviert, der basierend auf der vorhandenen Arbeitsauslastung variiert. Bei hoher Arbeitsauslastung bis zu alle 5 Sekunden und bei geringer Arbeitsauslastung nur jede Minute. Für jede interne speicheroptimierte Stagingtabelle, für die eine Bereinigung erforderlich ist, wird ein Thread erzeugt.  
  
 Bei der Datenleerung werden alle Datensätze aus dem In-Memory-Puffer gelöscht, die älter als die älteste, aktuell ausgeführte Transaktion sind, um diese Datensätze in die datenträgerbasierte Verlaufstabelle zu verschieben.  
  
 Sie können eine Datenleerung erzwingen, indem Sie [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md) aufrufen und das Schema sowie den Tabellennamen angeben:   
**sys.sp_xtp_flush_temporal_history  @schema_name, @object_name**. Mit diesem vom Benutzer ausgeführten Befehl wird derselbe Datenverschiebungsvorgang aufgerufen wie durch das Aufrufen des Datenleerungstasks durch das System gemäß internem Zeitplan.  
  
## <a name="did-this-article-help-you-were-listening"></a>Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20System-Versioned%20Temporal%20Tables%20with%20Memory-Optimized%20Tables%20page)  
  
## <a name="see-also"></a>Siehe auch  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Verwendungsszenarien für temporale Tabellen](../../relational-databases/tables/temporal-table-usage-scenarios.md)   
 [Systemkonsistenzprüfungen von temporalen Tabellen](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Überlegungen und Einschränkungen zu temporalen Tabellen](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Sicherheit bei temporale Tabellen](../../relational-databases/tables/temporal-table-security.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

