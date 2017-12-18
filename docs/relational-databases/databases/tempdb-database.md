---
title: tempdb-Datenbank | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
caps.latest.revision: "66"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.openlocfilehash: 6d71dcbda413d604c2c6ac2e4d85a815a4aa3719
ms.sourcegitcommit: ef1fa818beea435f58986af3379853dc28f5efd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="tempdb-database"></a>tempdb-Datenbank
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die **tempdb**-Systemdatenbank ist eine globale Ressource, die für alle Benutzer verfügbar ist, die mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbunden sind. In dieser Datenbank sind die folgenden Elemente enthalten:  
  
- Temporäre **Benutzerobjekte**, die explizit erstellt werden, z.B. globale oder lokale temporäre Tabellen und Indizes, temporäre gespeicherte Prozeduren, Tabellenvariablen, in Tabellenwertfunktionen zurückgegebene Tabellen oder Cursor.  
- **Interne Objekte**, die von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] erstellt werden. Dazu gehören:
  - Arbeitstabellen, in denen direkte Ergebnisse für Spools, Cursor, Sortierungen und temporäre große Objektspeicher (LOB) gespeichert werden.
  - Arbeitsdateien für Hashjoin- oder Hashaggregatvorgänge.
  - Zwischenergebnisse von Sortierungen für Vorgänge, wie z. B. das Erstellen oder Neuerstellen von Indizes (wenn SORT_IN_TEMPDB angegeben ist) oder bestimmte GROUP BY-, ORDER BY- oder UNION-Abfragen.

  > [!NOTE]
  > Jedes interne Objekt verwendet mindestens neun Seiten: eine IAM-Seite (Index Allocation Map) und einen achtseitigen Block. Weitere Informationen zu Seiten und Blöcken finden Sie unter [Seiten und Blöcke](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents).

- **Versionsspeicher**, die aus einer Auflistung von Datenseiten bestehen, in denen die Datenzeilen enthalten sind, die zur Unterstützung der Funktionen, die die Zeilenversionsverwaltung verwenden, erforderlich ist. Es gibt zwei Versionsspeicher: ein allgemeiner Versionsspeicher und ein Onlineindexerstellungs-Versionsspeicher. Der Versionsspeicher kann Folgendes beinhalten:
  - Zeilenversionen, die von Datenänderungstransaktionen in einer Datenbank generiert werden, die READ COMMITTED mit Zeilenversionsverwaltung oder Transaktionen der Momentaufnahmeisolation verwendet.  
  - Zeilenversionen, die von Datenänderungstransaktionen für Funktionen, wie z. B. Onlineindexvorgänge, Multiple Active Result Sets (MARS) und AFTER-Trigger, generiert wurden.  
  
Die Operationen in **tempdb** werden minimal protokolliert. Hierdurch kann für die Transaktion ein Rollback ausgeführt werden. **tempdb** wird bei jedem Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu erstellt, sodass das System immer mit einer bereinigten Kopie der Datenbank startet. Temporäre Tabellen und gespeicherte Prozeduren werden beim Trennen der Verbindung automatisch gelöscht; es sind keine Verbindungen aktiv, wenn das System heruntergefahren wird. Daher wird zwischen den einzelnen Sitzungen von **nichts in** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert. Sicherungs- und Wiederherstellungsvorgänge sind in **tempdb**nicht zulässig.  
  
## <a name="physical-properties-of-tempdb"></a>physische Eigenschaften von tempdb  
 In der folgenden Tabelle werden die anfänglichen Konfigurationswerte der **tempdb**-Daten- und Protokolldateien aufgeführt, die auf den Standardeinstellungen der Modelldatenbank basieren. Die Größe dieser Dateien kann sich in den verschiedenen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]geringfügig unterscheiden.  
  
|File|Logischer Name (logical name)|Physischer Name (physical name)|Anfangsgröße|Dateivergrößerung (file growth)|  
|----------|------------------|-------------------|------------------|-----------------|  
|Primäre Daten|tempdev|tempdb.mdf|8 Megabytes|Automatische Vergrößerung um 64 MB, bis der Speicherplatz auf dem Datenträger erschöpft ist|  
|Sekundäre Datendateien*|temp#|tempdb_mssql_#.ndf|8 Megabytes|Automatische Vergrößerung um 64 MB, bis der Speicherplatz auf dem Datenträger erschöpft ist|  
|Log|templog|templog.ldf|8 Megabytes|Automatische Vergrößerung um 64 MB, bis der Maximalwert von 2 TB erreicht wird|  
  
 \* Die Anzahl der Dateien hängt von der Anzahl der (logischen) Prozessoren auf dem Computer ab. Als allgemeine Regel gilt: Verwenden Sie die gleiche Anzahl an Datendateien wie logischen Prozessoren, falls die Anzahl von logischen Prozessoren acht oder weniger beträgt. Verwenden Sie acht Datendateien, wenn die Anzahl von logischen Prozessoren größer ist als acht. Falls daraufhin weiterhin ein Konflikt besteht, erhöhen Sie die Anzahl von Datendateien um ein Vielfaches von vier, bis der Konflikt auf ein akzeptables Ausmaß reduziert ist, oder ändern Sie die Arbeitsauslastung bzw. den Code.

> [!NOTE]
> Der Standardwert für die Anzahl der Datendateien basiert auf den allgemeinen Richtlinien in [KB 2154845](http://support.microsoft.com/kb/2154845/).  
  
### <a name="moving-the-tempdb-data-and-log-files"></a>Verschieben der tempdb-Daten- und -Protokolldateien  
 Weitere Informationen zum Verschieben der **tempdb** -Daten- und -Protokolldateien finden Sie unter [Verschieben von Systemdatenbanken](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options"></a>Datenbankoptionen  
 Die folgende Tabelle nennt die Standardwerte für die einzelnen Datenbankoptionen in der **tempdb** -Datenbank und gibt an, ob die entsprechende Option geändert werden kann. Zum Anzeigen der aktuellen Einstellungen dieser Optionen verwenden Sie die Katalogsicht [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Datenbankoption|Standardwert|Kann geändert werden.|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|ja|  
|ANSI_NULL_DEFAULT|OFF|ja|  
|ANSI_NULLS|OFF|ja|  
|ANSI_PADDING|OFF|ja|  
|ANSI_WARNINGS|OFF|ja|  
|ARITHABORT|OFF|ja|  
|AUTO_CLOSE|OFF|Nein|  
|AUTO_CREATE_STATISTICS|ON|ja|  
|AUTO_SHRINK|OFF|Nein|  
|AUTO_UPDATE_STATISTICS|ON|ja|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|ja|  
|CHANGE_TRACKING|OFF|Nein|  
|CONCAT_NULL_YIELDS_NULL|OFF|ja|  
|CURSOR_CLOSE_ON_COMMIT|OFF|ja|  
|CURSOR_DEFAULT|GLOBAL|ja|  
|Datenbankverfügbarkeitsoptionen|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|Nein<br /><br /> Nein<br /><br /> Nein|  
|DATE_CORRELATION_OPTIMIZATION|OFF|ja|  
|DB_CHAINING|ON|Nein|  
|ENCRYPTION|OFF|Nein|  
|MIXED_PAGE_ALLOCATION|OFF|Nein|  
|NUMERIC_ROUNDABORT|OFF|ja|  
|PAGE_VERIFY|CHECKSUM für neue Installationen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE für Upgrades von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|ja|  
|PARAMETERIZATION|SIMPLE|ja|  
|QUOTED_IDENTIFIER|OFF|ja|  
|READ_COMMITTED_SNAPSHOT|OFF|Nein|  
|RECOVERY|SIMPLE|Nein|  
|RECURSIVE_TRIGGERS|OFF|ja|  
|Service Broker-Optionen|ENABLE_BROKER|ja|  
|TRUSTWORTHY|OFF|Nein|  
  
 Eine Beschreibung dieser Datenbankoptionen finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="restrictions"></a>Einschränkungen  
 Die folgenden Operationen können mit der **tempdb** -Datenbank nicht ausgeführt werden:  
  
- Hinzufügen von Dateigruppen.  
- Sichern und Wiederherstellen der Datenbank.  
- Ändern der Sortierung. Die Standardsortierung entspricht der Serversortierung.  
- Ändern des Datenbankbesitzers Der Besitzer von**tempdb** ist **sa**.  
- Erstellen einer Datenbankmomentaufnahme.  
- Löschen der Datenbank.  
- Löschen des **guest** -Benutzers aus der Datenbank.  
- Aktivieren von Change Data Capture  
- Teilnehmen an der Datenbankspiegelung.  
- Entfernen der primären Dateigruppe, der primären Datendatei oder der Protokolldatei.  
- Umbenennen der Datenbank oder der primären Dateigruppe.  
- Ausführen von DBCC CHECKALLOC.  
- Ausführen von DBCC CHECKCATALOG.  
- Versetzen der Datenbank in den OFFLINE-Modus.  
- Versetzen der Datenbank oder der primären Dateigruppe in den READ_ONLY-Modus.  
  
## <a name="permissions"></a>Berechtigungen  
 Jeder Benutzer ist berechtigt, temporäre Objekte in tempdb zu erstellen. Benutzer haben nur Zugriff auf ihre eigenen Objekte, es sei denn, ihnen wurden zusätzliche Berechtigungen zugewiesen. Die CONNECT-Berechtigung für tempdb kann widerrufen werden, um Benutzer daran zu hindern, die tempdb-Datenbank zu verwenden. Von diesem Schritt wird jedoch abgeraten, da einige Routinevorgänge auf die Verwendung von tempdb angewiesen sind.  

## <a name="optimizing-tempdb-performance"></a>Optimieren der Leistung von tempdb
 Die Größe und die physische Platzierung der tempdb-Datenbank kann sich auf die Leistung eines Systems auswirken. Wurde für tempdb beispielsweise eine zu kleine Größe definiert, muss bei jedem Neustart der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz möglicherweise ein Teil der Verarbeitungslast des Systems dafür aufgewendet werden, die tempdb-Datenbank automatisch auf den Umfang zu vergrößern, der zum Unterstützen der anfallenden Arbeitsauslastung erforderlich ist.

 Verwenden Sie nach Möglichkeit die [schnelle Dateiinitialisierung für Datenbank](../../relational-databases/databases/database-instant-file-initialization.md), um die Leistung von Datendateivergrößerungen zu verbessern.
 
 Weisen Sie allen tempdb-Dateien im Voraus Speicherplatz zu, indem Sie die Dateigröße auf einen Wert festlegen, der hoch genug ist, um der typischen Arbeitsauslastung in der Umgebung gerecht zu werden. Dadurch verhindern Sie, dass die tempdb-Datenbank zu häufig vergrößert wird, was zu Leistungseinbußen führen kann. Für die tempdb-Datenbank sollte die automatische Vergrößerung festgelegt werden, jedoch nur für den Fall eines zusätzlichen Speicherplatzbedarfs für nicht geplante Ausnahmen. 

 Datendateien sollten in jeder [Dateigruppe](../../relational-databases/databases/database-files-and-filegroups.md#filegroups) die gleiche Größe haben, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Algorithmus zum proportionalen Auffüllen verwendet, in dem Zuteilungen in Dateien mit mehr freiem Platz bevorzugt werden. Ein Aufteilen von tempdb in mehrere Datendateien gleicher Größe bietet einen hohen Grad an paralleler Effizienz in Vorgängen, in denen tempdb verwendet wird. 
 
 Legen Sie das Inkrement für die Dateivergrößerung auf eine sinnvolle Größe fest, sodass der Zuwachs der tempdb-Datenbank nicht zu gering ausfällt. Wenn der Dateizuwachs im Vergleich zur Anzahl der Daten, die in die tempdb-Datenbank geschrieben werden, zu gering ist, muss tempdb möglicherweise ständig vergrößert werden. Dies beeinträchtigt die Leistung.
 
 Führen Sie die folgende Abfrage aus, um die aktuelle Größe von tempdb und die aktuellen Größenzuwachsparameter zu überprüfen:
 ```t-sql
 SELECT name AS FileName, 
    size*1.0/128 AS FileSizeinMB,
    CASE max_size 
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file will grow to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' = 
        CASE
            WHEN growth = 0 THEN 'Size is fixed and will not grow.'
            WHEN growth > 0 AND is_percent_growth = 0 
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```
 
 Platzieren Sie die tempdb-Datenbank auf einem schnellen E/A-Subsystem. Verwenden Sie Datenträgerstriping, wenn viele Datenträger direkt angeschlossen sind. Einzelne oder Gruppen von tempdb-Datendateien müssen nicht unbedingt auf verschiedenen Datenträgern oder Spindeln gespeichert sein – es sei denn, Sie stoßen auf E/A-Engpässe.
 
 Legen Sie die tempdb-Datenbank auf anderen Datenträgeren ab als denen, die von den Benutzerdatenbanken verwendet werden.

## <a name="performance-improvements-in-tempdb"></a>Leistungsverbesserungen in tempdb  
 Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] wird die **tempdb**-Leistung auf folgende Weise weiter optimiert:  
  
- Temporäre Tabellen und Tabellenvariablen werden zwischengespeichert. Das Zwischenspeichern ermöglicht das sehr schnelle Ausführen von Vorgängen zum Löschen und Erstellen der temporären Objekte und reduziert das Auftreten von Seitenzuordnungskonflikten.  
- Das Latchprotokoll für Seitenzuordnungen wurde verbessert. Dadurch wird die Anzahl der verwendeten UP-Latches (Update) reduziert.  
- Der Protokollierungsaufwand für **tempdb** wurde reduziert. Dadurch wird die für die **tempdb** -Protokolldatei verwendete Datenträger-E/A-Bandbreite reduziert.  
- Das Setup fügt während der Installation einer neuen Instanz mehrere tempdb-Datendateien hinzu. Diese Aufgabe kann mit der neuen Eingabesteuerung der Benutzeroberfläche im Bereich **Datenbankmodulkonfiguration** und einem Befehlszeilenparameter /SQLTEMPDBFILECOUNT durchgeführt werden. Standardmäßig fügt das Setup genau so viele tempdb-Dateien hinzu, wie es logische Prozessoren gibt. Es werden dabei allerdings höchstens acht Dateien hinzugefügt.  
- Wenn mehrere **tempdb** -Datenbankdateien vorhanden sind, werden alle Dateien gleichzeitig und im selben Umfang je nach Wachstumseinstellungen automatisch vergrößert. Ablaufverfolgungsflag 1117 ist nicht mehr erforderlich.  
- Alle Zuordnungen in **tempdb** verwenden gleichartige Blöcke. [Ablaufverfolgungsflag 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) ist nicht mehr erforderlich.  
- Für die primäre Dateigruppe ist die AUTOGROW_ALL_FILES-Eigenschaft aktiviert und kann nicht geändert werden. 

## <a name="capacity-planning-for-tempdb"></a>Kapazitätsplanung für tempdb
 Das Festlegen der angemessenen Größe von tempdb in einer Produktionsumgebung hängt von vielen Faktoren ab. Wie bereits zuvor in diesem Thema beschrieben, schließen diese Faktoren die vorhandene Arbeitsauslastung und die verwendeten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen ein. Es wird empfohlen, die vorhandene Workload durch Ausführen folgender Aufgaben in einer SQL Server-Testumgebung zu analysieren:
- Festlegen der automatischen Vergrößerung für tempdb
- Ausführen einzelner Abfragen oder Ablaufverfolgungsdateien der Workload sowie Überwachen der Speicherplatzverwendung in tempdb
- Ausführen von Indexverwaltungsvorgängen wie das Neuerstellen von Indizes, und die Überwachung des Speicherplatzes in tempdb 
- Verwenden der Werte zur Speicherplatzverwendung aus den vorigen Schritten, um den Gesamtverbrauch der Workload vorherzusagen; Anpassen dieses Werts für prognostizierte gleichzeitige Aktivitäten und anschließend Festlegen der entsprechenden Größe von tempdb.

## <a name="how-to-monitor-tempdb-use"></a>Überwachen der Speicherplatzverwendung in tempdb
  Wenn nicht mehr genügend Speicherplatz in tempdb vorhanden ist, kann das erhebliche Störungen in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Produktionsumgebung verursachen und dazu führen, dass ausgeführte Anwendungen Vorgänge nicht abschließen können. Sie können mit der dynamischen Verwaltungssicht [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) den in den tempdb-Dateien verwendeten Speicherplatz überwachen:
  
 ```t-sql
 -- Determining the Amount of Free Space in tempdb
 SELECT SUM(unallocated_extent_page_count) AS [free pages], 
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
 
 ```t-sql
 -- Determining the Amount Space Used by the Version Store
 SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
 
 ```t-sql
 -- Determining the Amount of Space Used by Internal Objects
 SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
 
 ```t-sql
 -- Determining the Amount of Space Used by User Objects
 SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
  
  Um außerdem die Aktivität für die Seitenzuordnung und die Zuordnungsaufhebung in tempdb auf der Sitzungs- oder Aufgabenebene zu überwachen, können Sie die dynamischen Verwaltungssichten [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) und [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md) verwenden. Mithilfe dieser Sichten können große Abfragen, temporäre Tabellen oder Tabellenvariablen identifiziert werden, die große Mengen von Speicherplatz in tempdb belegen. Es gibt ebenfalls mehrere Leistungsindikatoren, die zum Überwachen des in tempdb verfügbaren freien Speicherplatzes verwendet werden können. Diese können auch verwendet werden, um die Ressourcen, die tempdb verwenden, zu überwachen. Weitere Informationen finden Sie im nächsten Abschnitt.

 ```t-sql
 -- Obtaining the space consumed by internal objects in all currently running tasks in each session
 SELECT session_id, 
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count 
 FROM sys.dm_db_task_space_usage 
 GROUP BY session_id;
 ```
 
 ```t-sql
 -- Obtaining the space consumed by internal objects in the current session for both running and completed tasks
 SELECT R2.session_id,
  R1.internal_objects_alloc_page_count 
  + SUM(R2.internal_objects_alloc_page_count) AS session_internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count 
  + SUM(R2.internal_objects_dealloc_page_count) AS session_internal_objects_dealloc_page_count
 FROM sys.dm_db_session_space_usage AS R1 
 INNER JOIN sys.dm_db_task_space_usage AS R2 ON R1.session_id = R2.session_id
 GROUP BY R2.session_id, R1.internal_objects_alloc_page_count, 
  R1.internal_objects_dealloc_page_count;;
 ```

## <a name="related-content"></a>Verwandte Inhalte  
 [SORT_IN_TEMPDB-Option für Indizes](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
 [Systemdatenbanken](../../relational-databases/databases/system-databases.md)  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
 [Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von tempdb in SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81216)  
 [Problembehandlung bei unzureichendem Speicherplatz in tempdb](http://msdn.microsoft.com/library/ms176029.aspx) 
