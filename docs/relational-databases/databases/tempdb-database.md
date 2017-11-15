---
title: tempdb-Datenbank | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
ms.openlocfilehash: 003196d8c30ca45c54750587c03c8d7d6e5a358d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="tempdb-database"></a>tempdb-Datenbank
  Die **tempdb** -Systemdatenbank ist eine globale Ressource, die für alle Benutzer verfügbar ist, die mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbunden sind. In der Datenbank sind die folgenden Elemente enthalten:  
  
-   Temporäre Benutzerobjekte, die explizit erstellt werden, z. B. globale oder lokale temporäre Tabellen, temporäre gespeicherte Prozeduren, Tabellenvariablen oder Cursor.  
  
-   Interne Objekte, die von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]erstellt werden, z. B. Arbeitstabellen zum Speichern von Zwischenergebnissen für Spool- und Sortiervorgänge.  
  
-   Zeilenversionen, die von Datenänderungstransaktionen in einer Datenbank generiert werden, die READ COMMITTED mit Zeilenversionsverwaltung oder Transaktionen der Momentaufnahmeisolation verwendet.  
  
-   Zeilenversionen, die von Datenänderungstransaktionen für Funktionen, wie z. B. Onlineindexvorgänge, Multiple Active Result Sets (MARS) und AFTER-Trigger, generiert wurden.  
  
 Die Operationen in **tempdb** werden minimal protokolliert. Hierdurch kann für die Transaktion ein Rollback ausgeführt werden. **tempdb** wird bei jedem Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu erstellt, sodass das System immer mit einer bereinigten Kopie der Datenbank startet. Temporäre Tabellen und gespeicherte Prozeduren werden beim Trennen der Verbindung automatisch gelöscht; es sind keine Verbindungen aktiv, wenn das System heruntergefahren wird. Daher wird zwischen den einzelnen Sitzungen von **nichts in** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert. Sicherungs- und Wiederherstellungsvorgänge sind in **tempdb**nicht zulässig.  
  
## <a name="physical-properties-of-tempdb"></a>physische Eigenschaften von tempdb  
 Die folgende Tabelle listet die anfänglichen Konfigurationswerte der **tempdb** -Daten- und Protokolldateien auf. Die Größe dieser Dateien kann sich in den verschiedenen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]geringfügig unterscheiden.  
  
|File|Logischer Name (logical name)|Physischer Name (physical name)|Anfangsgröße|Dateivergrößerung (file growth)|  
|----------|------------------|-------------------|------------------|-----------------|  
|Primäre Daten|tempdev|tempdb.mdf|8 Megabytes|Automatische Vergrößerung um 64 MB, bis der Speicherplatz auf dem Datenträger erschöpft ist|  
|Sekundäre Datendateien*|temp#|tempdb_mssql_#.ndf|8 Megabytes|Automatische Vergrößerung um 64 MB, bis der Speicherplatz auf dem Datenträger erschöpft ist|  
|Log|templog|templog.ldf|8 Megabytes|Automatische Vergrößerung um 64 MB, bis der Maximalwert von 2 TB erreicht wird|  
  
 \* Die Anzahl der Dateien hängt von der Anzahl der (logischen) Kerne auf dem Computer ab. Der Wert ist die Anzahl der Kerne oder 8, je nachdem, welcher Wert niedriger ist.   
Der Standardwert für die Anzahl der Datendateien basiert auf den allgemeinen Richtlinien in [KB 2154845](https://support.microsoft.com/en-us/kb/2154845/).  
  
## <a name="performance-improvements-in-tempdb"></a>Leistungsverbesserungen in tempdb  
 Die Leistung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tempdb **wurde in** folgendermaßen verbessert:  
  
-   Temporäre Tabellen und Tabellenvariablen können zwischengespeichert werden. Das Zwischenspeichern ermöglicht das sehr schnelle Ausführen von Vorgängen zum Löschen und Erstellen der temporären Objekte und reduziert das Auftreten von Seitenzuordnungskonflikten.  
  
-   Das Latchprotokoll für Seitenzuordnungen wurde verbessert. Dadurch wird die Anzahl der verwendeten UP-Latches (Update) reduziert.  
  
-   Der Protokollierungsaufwand für **tempdb** wurde reduziert. Dadurch wird die für die **tempdb** -Protokolldatei verwendete Datenträger-E/A-Bandbreite reduziert.  
  
-   Das Setup fügt während der Installation einer neuen Instanz mehrere tempdb-Datendateien hinzu. Diese Aufgabe kann mit der neuen Eingabesteuerung der Benutzeroberfläche im Bereich **Datenbankmodulkonfiguration** und einem Befehlszeilenparameter /SQLTEMPDBFILECOUNT durchgeführt werden. Standardmäßig fügt das Setup genau so viele tempdb-Dateien hinzu wie die CPU-Anzahl oder 8, je nachdem, welcher Wert niedriger ist.  
  
-   Wenn mehrere **tempdb** -Datenbankdateien vorhanden sind, werden alle Dateien gleichzeitig und im selben Umfang je nach Wachstumseinstellungen automatisch vergrößert.  Ablaufverfolgungsflag 1117 ist nicht mehr erforderlich.  
  
-   Alle Zuordnungen in **tempdb** verwenden gleichartige Blöcke. Ablaufverfolgungsflag 1118 ist nicht mehr erforderlich.  
  
-   Für die primäre Dateigruppe ist die AUTOGROW_ALL_FILES-Eigenschaft aktiviert und kann nicht geändert werden.  
  
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
  
-   Hinzufügen von Dateigruppen.  
  
-   Sichern und Wiederherstellen der Datenbank.  
  
-   Ändern der Sortierung. Die Standardsortierung entspricht der Serversortierung.  
  
-   Ändern des Datenbankbesitzers Der Besitzer von**tempdb** ist **sa**.  
  
-   Erstellen einer Datenbankmomentaufnahme.  
  
-   Löschen der Datenbank.  
  
-   Löschen des **guest** -Benutzers aus der Datenbank.  
  
-   Aktivieren von Change Data Capture  
  
-   Teilnehmen an der Datenbankspiegelung.  
  
-   Entfernen der primären Dateigruppe, der primären Datendatei oder der Protokolldatei.  
  
-   Umbenennen der Datenbank oder der primären Dateigruppe.  
  
-   Ausführen von DBCC CHECKALLOC.  
  
-   Ausführen von DBCC CHECKCATALOG.  
  
-   Versetzen der Datenbank in den OFFLINE-Modus.  
  
-   Versetzen der Datenbank oder der primären Dateigruppe in den READ_ONLY-Modus.  
  
## <a name="permissions"></a>Berechtigungen  
 Jeder Benutzer ist berechtigt, temporäre Objekte in tempdb zu erstellen. Benutzer haben nur Zugriff auf ihre eigenen Objekte, es sei denn, ihnen wurden zusätzliche Berechtigungen zugewiesen. Die CONNECT-Berechtigung für tempdb kann widerrufen werden, um Benutzer daran zu hindern, die tempdb-Datenbank zu verwenden. Von diesem Schritt wird jedoch abgeraten, da einige Routinevorgänge auf die Verwendung von tempdb angewiesen sind.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [SORT_IN_TEMPDB-Option für Indizes](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
  
 [Systemdatenbanken](../../relational-databases/databases/system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
 [Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von tempdb in SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81216)  
  
  
