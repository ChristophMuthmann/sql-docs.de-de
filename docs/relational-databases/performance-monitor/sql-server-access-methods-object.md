---
title: SQL Server, Zugriffsmethoden-Objekt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access Methods object
- SQLServer:Access Methods
ms.assetid: 27558585-e780-48bb-a042-30d664662ebc
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfbbfd6ac0e746fc8165186745006a1834f5aebe
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-access-methods-object"></a>SQL Server, Zugriffsmethoden-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Das **Zugriffsmethoden**-Objekt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt Leistungsindikatoren zum Überwachen des Zugriffs auf die logischen Daten in der Datenbank bereit. Der physische Zugriff auf die Datenbankseiten auf dem Datenträger wird mithilfe der **Puffer-Manager** -Leistungsindikatoren überwacht. Durch die Überwachung der Methoden, die für den Zugriff auf in der Datenbank gespeicherte Daten verwendet werden, können Sie leichter bestimmen, ob die Abfrageleistung verbessert werden kann, indem Sie Indizes hinzufügen oder ändern, Partitionen hinzufügen oder verschieben, Dateien oder Dateigruppen hinzufügen, Indizes defragmentieren oder Abfragen neu schreiben. Die **Zugriffsmethoden** -Leistungsindikatoren können auch zum Überwachen des Umfangs der Daten, Indizes und des freien Speicherplatzes in der Datenbank verwendet werden und dadurch einen Hinweis auf das Datenvolumen und die Fragmentierung der einzelnen Serverinstanzen geben. Eine zu starke Fragmentierung kann die Leistung beeinträchtigen.  
  
 Einzelheiten über Datenmengen, Fragmentierung und Auslastung finden Sie in den folgenden dynamischen Verwaltungssichten:  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)  
  
-   [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)  
  
 Verwenden Sie für den Speicherplatzverbrauch in **tempdb** auf der Dateiebene, der Aufgabenebene und der Sitzungsebene die folgenden dynamischen Verwaltungssichten:  
  
-   [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
-   [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)  
  
-   [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
  
 Diese Tabelle enthält eine Beschreibung der Indikatoren für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Zugriffsmethoden** -Leistungsindikatoren überwacht.  
  
|Zugriffsmethoden-Leistungsindikatoren von SQL Server|Description|  
|----------------------------------------|-----------------|  
|**Cleanupbatches für AUs/Sekunde**|Anzahl der Batches pro Sekunde, die durch den Hintergrundtask für den Cleanup von zurückgestellten gelöschten Zuordnungseinheiten erfolgreich ausgeführt wurden.|  
|**Cleanups für AUs/Sekunde**|Anzahl der Zuordnungseinheiten pro Sekunde, die durch den Hintergrundtask für den Cleanup zurückgestellter gelöschter Zuordnungseinheiten erfolgreich gelöscht wurden. Für jeden Einheitenlöschvorgang sind mehrere Batches erforderlich.|  
|**Anzahl der als Verweis erstellten LOB-Werte**|Anzahl der LOB-Werte, die als Verweis ausgegeben wurden. Als Verweis erstellte LOB-Werte werden in bestimmten Massenvorgängen verwendet, um die Kosten einer Übergabe nach Wert zu vermeiden.|  
|**Anzahl der als Verweis verwendeten LOB-Werte**|Anzahl der LOB-Werte, die als Verweis verwendet wurden. Als Verweis erstellte LOB-Werte werden in bestimmten Massenvorgängen verwendet, um die Kosten einer Übergabe nach Wert zu vermeiden.|  
|**Anzahl der LOB-Read-Aheads**|Anzahl der LOB-Seiten, für die ein Read-Ahead ausgegeben wurde.|  
|**Anzahl für Pull in Zeile**|Anzahl der Werte, die durch Ausführen eines Pulls aus Außerhalb Zeile in Innerhalb Zeile verschoben wurden.|  
|**Anzahl für Push aus Zeile**|Anzahl der Werte, die durch Ausführen eines Pushs von innerhalb einer Zeile außerhalb von Zeilen verschoben wurden.|  
|**Zurückgestellte gelöschte AUs**|Anzahl der Zuordnungseinheiten, die durch den Hintergrundtask für den Cleanup zurückgestellter gelöschter Zuordnungen gelöscht werden sollen.|  
|**Zurückgestellte gelöschte Rowsets**|Anzahl der erstellten Rowsets im Ergebnis abgebrochener Vorgänge zur Onlineindexerstellung, die durch den Hintergrundtask für den Cleanup von zurückgestellten gelöschten Rowsets gelöscht werden sollen.|  
|**Cleanup für gelöschte Rowsets/Sekunde**|Anzahl der erstellten Rowsets im Ergebnis abgebrochener Vorgänge zur Onlineindexerstellung, die durch den Hintergrundtask für den Cleanup von zurückgestellten gelöschten Rowsets pro Sekunde erfolgreich gelöscht wurden.|  
|**Gelöschte Rowsets ausgelassen/Sekunde**|Anzahl der Rowsets im Ergebnis abgebrochener Vorgänge zur Onlineindexerstellung, die durch den Hintergrundtask für den Cleanup von zurückgestellten gelöschten Rowsets ausgelassen wurden.|  
|**Aufgehobene Blockzuordnungen/Sekunde**|Anzahl der Blöcke, deren Zuordnung in allen Datenbanken pro Sekunde in dieser Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aufgehoben wurde.|  
|**Zugeordnete Blöcke/Sekunde**|Anzahl der Blöcke, die in allen Datenbanken pro Sekunde in dieser Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zugeordnet wurden.|  
|**Fehler in Cleanupbatches von AUs/Sekunde**|Anzahl der Batches pro Sekunde, die fehlgeschlagen sind und für die ein erneuter Versuch durch den Hintergrundtask für den Cleanup von zurückgestellten gelöschten Zuordnungseinheiten erforderlich war. Der Fehler kann auf nicht genügend Arbeits- oder Datenträgerspeicher zurückzuführen sein, aber auch auf Hardwarefehler und andere Gründe.|  
|**Fehler beim Verwenden des Blattseitencookies**|Häufigkeit, mit der ein Blattseitencookie während einer Indexsuche nicht verwendet werden konnte, da Änderungen auf der Blattseite vorgenommen wurden. Der Cookie wird verwendet, um die Indexsuche zu beschleunigen.|  
|**Fehler beim Verwenden von Strukturseitencookie**|Häufigkeit, mit der ein Strukturseitencookie während einer Indexsuche nicht verwendet werden konnte, da Änderungen auf den übergeordneten Seiten dieser Strukturseiten vorgenommen wurden. Der Cookie wird verwendet, um die Indexsuche zu beschleunigen.|  
|**Weitergeleitete Datensätze/Sekunde**|Anzahl der Datensätze pro Sekunde, die über Zeiger auf weitergeleitete Datensätze abgerufen wurden.|  
|**Seitenabrufvorgänge für freien Speicher/Sekunde**|Anzahl der Seiten, die pro Sekunde von Scans nach freiem Speicherplatz abgerufen werden. Diese Scans suchen nach freiem Speicherplatz in Seiten, die bereits einer Zuordnungseinheit zugeordnet wurden, um Anforderungen zum Einfügen oder Bearbeiten von Datensatzfragmenten zu erfüllen.|  
|**Scans für freien Speicherplatz/Sekunde**|Anzahl der Scans pro Sekunde, die gestartet werden, um in bereits einer Zuordnungseinheit zugeordneten Seiten freien Speicherplatz zum Einfügen oder Bearbeiten eines Datensatzfragments zu suchen. Pro Scan können mehrere Seiten gefunden werden.|  
|**Vollständige Scans/Sekunde**|Anzahl der unbeschränkten, vollständigen Scans pro Sekunde. Hierbei kann es sich entweder um Scans der Basistabelle oder um vollständige Indexscans handeln.|  
|**Indexsuchen/Sekunde**|Anzahl der Indexsuchen pro Sekunde. Diese werden verwendet, um einen Bereichsscan zu starten, die Position eines Bereichsscans neu festzulegen, einzelne Indexdatensätze abzurufen sowie um den Index nach einer Einfügeposition für eine neue Zeile zu durchsuchen.|  
|**InSysXact-Wartevorgänge/Sekunde**|Die Anzahl der Versuche, die ein Reader auf eine Seite warten muss, weil das InSysXact-Bit festgelegt ist.|  
|**Anzahl der erstellten LobHandle-Elemente**|Anzahl der temporären LOBs, die erstellt wurden.|  
|**Anzahl der gelöschten LobHandle-Elemente**|Anzahl der temporären LOBs, die gelöscht wurden.|  
|**Anzahl der erstellten LobSS-Anbieter**|Anzahl der LOB-Speicherdienstanbieter (LobSSP), die erstellt wurden. Pro LobSSP wird eine Arbeitstabelle erstellt.|  
|**Anzahl der gelöschten LobSS-Anbieter**|Anzahl der LobSS-Anbieter, die gelöscht wurden.|  
|**Anzahl der abgeschnittenen LobSS-Anbieter**|Anzahl der LobSS-Anbieter, die abgeschnitten wurden.|  
|**Zuordnungen gemischter Seiten/Sekunde**|Anzahl der Seiten, die in gemischten Blöcken pro Sekunde zugeordnet wurden. Diese können verwendet werden, um die IAM-Seiten und die ersten acht einer Zuordnungseinheit zugeordneten Seiten zu speichern.|  
|**Seitenkomprimierungsversuche/Sekunde**|Anzahl an Seiten, die zur Komprimierung auf Seitenebene ausgewertet werden. Dies schließt Seiten ein, die nicht komprimiert wurden, da beträchtliche Einsparungen erreicht werden konnten. Enthält alle Objekte in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz. Informationen zu bestimmten Objekten finden Sie unter [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)aufgehoben wurde.|  
|**Aufgehobene Seitenzuordnungen/Sekunde**|Anzahl der Seiten, deren Zuordnung pro Sekunde in allen Datenbanken in dieser Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aufgehoben wurde. Darin enthalten sind Seiten aus sowohl gemischten als auch gleichartigen Blöcken.|  
|**Seitenteilungen/Sekunde**|Anzahl der Seitenteilungen pro Sekunde, die das Ergebnis eines Überlaufs von Indexseiten sind.|  
|**Zugeordnete Seiten/Sekunde**|Anzahl der Seiten, die in allen Datenbanken pro Sekunde in dieser Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zugeordnet wurden. Hierzu zählen auch Seitenzuordnungen aus gemischten sowie aus einheitlichen Blöcken.|  
|**Komprimierte Seiten/Sekunde**|Anzahl an Datenseiten, die mit PAGE-Komprimierung komprimiert werden. Enthält alle Objekte in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz. Informationen zu bestimmten Objekten finden Sie unter [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)aufgehoben wurde.|  
|**Untersuchungsscans/Sekunde**|Anzahl der Untersuchungsscans pro Sekunde, mit denen höchstens eine einzelne gekennzeichnete Zeile in einem Index oder einer Basistabelle gesucht wird.|  
|**Bereichsscans/Sekunde**|Anzahl der eingeschränkten Bereichsscans mithilfe von Indizes pro Sekunde.|  
|**Scanpunktüberprüfungen/Sekunde**|Häufigkeit pro Sekunde, mit der der Scanpunkt erneut überprüft werden musste, um den Scan fortsetzen zu können.|  
|**Ausgelassene inaktive Datensätze/Sekunde**|Anzahl der inaktiv gesetzten Datensätze pro Sekunde, die im Laufe von Scans ausgelassen wurden.|  
|**Ausweitungen von Tabellensperren/Sekunde**|Häufigkeit, mit der Sperren in einer Tabelle auf die TABLE- bzw. HoBT-Granularität ausgeweitet wurden.|  
|**Blattseitencookie verwendet**|Häufigkeit, mit der ein Blattseitencookie während einer Indexsuche erfolgreich verwendet wurde, da keine Änderungen am Blatt aufgetreten sind. Der Cookie wird verwendet, um die Indexsuche zu beschleunigen.|  
|**Strukturseitencookie verwendet**|Häufigkeit, mit der ein Strukturseitencookie während einer Indexsuche erfolgreich verwendet wurde, da keine Änderungen an der übergeordneten Seite der Strukturseite aufgetreten sind. Der Cookie wird verwendet, um die Indexsuche zu beschleunigen.|  
|**Erstellte Arbeitsdateien/Sekunde**|Anzahl der pro Sekunde erstellten Arbeitsdateien. Arbeitsdateien können beispielsweise verwendet werden, um temporäre Ergebnisse für Hashjoins und Hashaggregate zu speichern.|  
|**Erstellte Arbeitstabellen/Sekunde**|Anzahl der pro Sekunde erstellten Arbeitstabellen. Arbeitstabellen können beispielsweise verwendet werden, um temporäre Ergebnisse von Spoolvorgängen für Abfragen, von LOB-Variablen, XML-Variablen und vom Cursor zu speichern.|  
|**Basis für Arbeitstabellen aus Cache**|Nur zur internen Verwendung.|  
|**Quote der Arbeitstabellen aus Cache**|Prozentsatz der erstellten Arbeitstabellen, bei denen die ersten zwei Seiten der Arbeitstabelle nicht zugeordnet wurden, sondern im Arbeitstabellencache verfügbar waren. (Wenn eine Arbeitstabelle gelöscht wird, kann die Zuordnung von zwei Seiten beibehalten werden, die an den Arbeitstabellencache zurückgegeben werden. Hierdurch wird die Leistung erhöht.)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
