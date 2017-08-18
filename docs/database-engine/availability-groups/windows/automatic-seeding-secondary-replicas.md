---
title: "Automatisches Seeding für sekundäre Replikate (SQL Server) | Microsoft-Dokumentation"
description: "Verwenden Sie das automatische Seeding zum Initialisieren sekundärer Replikate."
services: data-lake-analytics
ms.custom: 
ms.date: 06/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Automatic seeding [SQL Server], secondary replica
ms.assetid: 
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1b72f9f5bf58f72bb4284b1a6cc8d0af7a722aed
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="automatic-seeding-for-secondary-replicas"></a>Automatisches Seeding für sekundäre Replikate

[!INCLUDE [tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Bei SQL Server 2012 und 2014 ist die einzige Möglichkeit, ein sekundäres Replikat in einer Verfügbarkeitsgruppe zu initialisieren, die Verwendung von Sicherung, Kopieren und Wiederherstellung. SQL Server 2016 führt eine neue Funktion zum Initialisieren eines sekundären Replikats ein – das *automatische Seeding*. Das automatische Seeding verwendet die Übermittlung durch Protokollstream, um die Sicherung mit VDI für jede Datenbank der Verfügbarkeitsgruppe mit konfigurierten Endpunkten an das sekundäre Replikat zu streamen. Diese neue Funktion kann verwendet werden, wenn eine Verfügbarkeitsgruppe erstellt wird oder wenn ihr eine Datenbank hinzugefügt wird. Das automatische Seeding ist in allen Versionen von SQL Server verfügbar, die Always On-Verfügbarkeitsgruppen unterstützen, und kann sowohl mit herkömmlichen als auch mit [verteilten Verfügbarkeitsgruppen](distributed-availability-groups.md) verwendet werden.

## <a name="considerations"></a>Weitere Überlegungen

Überlegungen zur Verwendung des automatischen Seedings beinhalten:

* [Auswirkungen von Leistung und Transaktionsprotokoll auf das primäre Replikat](#performance-and-transaction-log-impact-on-the-primary-replica)
* [Datenträgerlayout](#disk-layout)
* [Sicherheit](#security)


### <a name="performance-and-transaction-log-impact-on-the-primary-replica"></a>Auswirkungen von Leistung und Transaktionsprotokoll auf das primäre Replikat

Ob das automatische Seeding beim Initialisieren eines sekundären Replikats hilfreich ist, hängt von der Größe der Datenbank, der Netzwerkgeschwindigkeit und der Entfernung zwischen dem primären und dem sekundären Replikat ab. Zum Beispiel kann Folgendes gegeben sein:

* Die Datenbankgröße beträgt 5 TB
* Die Netzwerkgeschwindigkeit beträgt 1GB/s
* Die Entfernung zwischen den beiden Standorten beträgt über 1.600 Kilometer

Ein Netzwerk mit 1GB/s kann einen dauerhaften Durchsatz von 125 MB/s bieten, wenn die volle Bandbreite verfügbar ist. In diesem Beispiel würde das automatische Seeding knapp über 11 Stunden dauern. In der Praxis ist das automatische Seeding etwas langsamer, da Netzwerksignale auf langen Entfernungen schwächer werden und der Link normalerweise mit anderen Ressourcen im Netzwerk geteilt wird. Während des Seedings wird das Transaktionsprotokoll für die Datenbank im primären Replikat noch länger und kann erst abgeschnitten werden, wenn das automatische Seeding für diese Datenbank abgeschlossen ist.  Das Transaktionsprotokoll kann dann mit einer Sicherung des Transaktionsprotokolls abgeschnitten werden.

Das automatische Seeding ist ein Singlethreadprozess, der bis zu fünf Datenbanken verarbeiten kann. Dies kann die Leistung beeinträchtigen, vor allem wenn die Verfügbarkeitsgruppe über mehrere Datenbanken verfügt.

Die Komprimierung kann für das automatische Seeding verwendet werden, ist aber in der Standardeinstellung deaktiviert. Das Aktivieren der Komprimierung reduziert die Netzwerkbandbreite und beschleunigt möglicherweise den Prozess, führt jedoch zu zusätzlichem Prozessoroverhead. Aktivieren Sie das Ablaufverfolgungsflag 9567, um die Komprimierung während des automatischen Seedings zu verwenden. Siehe dazu [Optimieren der Komprimierung für die Verfügbarkeitsgruppe](tune-compression-for-availability-group.md).

### <a name="disk-layout"></a>Datenträgerlayout

Der Ordner, in dem die Datenbank durch das automatische Seeding erstellt wird, muss bereits vorhanden und mit dem Pfad auf dem primären Replikat identisch sein.

### <a name="security"></a>Sicherheit

Die Sicherheitsberechtigungen variieren je nach Art des Replikats, das initialisiert wird:

* Bei einer herkömmlichen Verfügbarkeitsgruppe müssen der Verfügbarkeitsgruppe auf dem sekundären Replikat Berechtigungen gewährt werden, wenn dieses mit der Verfügbarkeitsgruppe verknüpft wird. Verwenden Sie in Transact-SQL den Befehl „ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE“.
* Bei einer verteilten Verfügbarkeitsgruppe, bei der sich die erstellten Datenbanken des Replikats auf dem primären Replikat der sekundären Verfügbarkeitsgruppe befinden, sind keine zusätzlichen Berechtigungen erforderlich, da es sich bereits um ein primäres Replikat handelt.
* Bei einem sekundären Replikat auf der sekundären Verfügbarkeitsgruppe einer verteilten Verfügbarkeitsgruppe müssen Sie den Befehl „ALTER AVAILABILITY GROUP [2ndAGName] GRANT CREATE ANY DATABASE“ verwenden. Für dieses sekundäre Replikat wird ein Seeding vom primären Replikat der sekundären Verfügbarkeitsgruppe durchgeführt.

## <a name="create-an-availability-group-with-automatic-seeding"></a>Erstellen einer Verfügbarkeitsgruppe mit automatischem Seeding

Sie erstellen eine Verfügbarkeitsgruppe mit automatischem Seeding mit Transact-SQL oder SQL Server Management Studio (SSMS, Version 17 oder höher). Befolgen Sie [diese Anweisungen](use-the-availability-group-wizard-sql-server-management-studio.md), um den Assistenten für Verfügbarkeitsgruppen in SSMS zu verwenden. Bei Schritt 9 wird das automatische Seeding als erste und standardmäßige Option angezeigt.

![Auswählen der anfänglichen Datensynchronisierung][1]

Im folgenden Beispiel wird eine Verfügbarkeitsgruppe mit Transact-SQL erstellt. Siehe auch [Erstellen einer Verfügbarkeitsgruppe (Transact-SQL)](create-an-availability-group-transact-sql.md). Das Seeding wird auf einem sekundären Replikat aktiviert, indem Sie die Option „SEEDING_MODE“ auf „AUTOMATIC“ (AUTOMATISCH) festlegen. Das Standardverhalten ist „MANUAL“ (MANUELL) und somit das Verhalten von Vorgängerversionen von SQL Server 2016 und erfordert eine Sicherung der Datenbank auf dem primären Replikat, eine Kopie der Sicherungsdatei auf das sekundäre Replikat und eine Wiederherstellung der Sicherung mit „NORECOVERY“.

```
CREATE AVAILABILITY GROUP [AGName]
  FOR DATABASE db1
  REPLICA ON N'Primary_Replica'
WITH (
  ENDPOINT_URL = N'TCP://Primary_Replica.Contoso.com:5022', 
  FAILOVER_MODE = AUTOMATIC, 
  AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
),
  N'Secondary_Replica' WITH (
    ENDPOINT_URL = N'TCP://Secondary_Replica.Contoso.com :5022', 
    FAILOVER_MODE = AUTOMATIC, 
    SEEDING_MODE = AUTOMATIC);
 GO
```

Das Festlegen von „SEEDING_MODE“ auf einem primären Replikat während einer „CREATE AVAILABILITY GROUP“-Anweisung hat keine Auswirkung, da das primäre Replikat bereits die hauptsächliche Lese-/Schreibkopie der Datenbank enthält. „SEEDING_MODE“ würde nur angewendet werden, wenn ein anderes Replikat zum primären würde und eine Datenbank hinzugefügt würde. Der Seedingmodus kann später geändert werden. Siehe dazu [Ändern des Seedingmodus eines Replikats](#change-the-seeding-mode-of-a-replica).

Sobald auf einer Instanz, die zum sekundären Replikat wird, die Verknüpfung erfolgt, wird folgende Meldung zum SQL Server-Protokoll hinzugefügt:

„Local availability replica for availability group 'AGName' has not been granted permission to create databases, but has a SEEDING_MODE of AUTOMATIC. Use the ALTER AVAILABILITY GROUP … GRANT CREATE ANY DATABASE command to allow the creation of databases seeded by the primary availability replica.“ (Dem lokalen Verfügbarkeitsreplikat für die Verfügbarkeitsgruppe „Verfügbarkeitsgruppenname“ kann keine Berechtigung zum Erstellen von Datenbanken erteilt werden, aber „SEEDING_MODE“ ist auf „AUTOMATISCH“ festgelegt. Verwenden Sie den Befehl „ALTER AVAILABILITY GROUP … GRANT CREATE ANY DATABASE“, um das Erstellen von Datenbanken zuzulassen, für die vom primären Verfügbarkeitsreplikat ein Seeding ausgeführt wird.)

Führen Sie nach der Verknüpfung die folgende Anweisung aus:

```
ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE
 GO
````

> [!NOTE] 
> Es gibt zurzeit ein bekanntes Problem ab SQL Server 2016 SP1 CU2, bei dem ein sekundäres Replikat drei Minuten warten muss, bis der Verfügbarkeitsgruppe erlaubt wird, für die Datenbank ein Seeding auszuführen, bevor eine „ALTER AVAILABILITY GROUP...“-Anweisung ausgeführt wird. Vor Ablauf dieser Zeit gibt die Anweisung keinen Fehler zurück, sondern vermeldet stattdessen einen Erfolg. Dies ist auch ein bekanntes Problem. Diese Probleme werden in einem zukünftigen Update von SQL Server behoben. Fügen Sie zur Umgehung des Problems eine „WAITFOR“-Anweisung ein:

```
WAITFOR DELAY '00:03:15';
ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE;
GO
```

Bei erfolgreicher Ausführung wird die Datenbank/werden die Datenbanken auf dem sekundären Replikat automatisch erstellt und weist/weisen einen der folgenden beiden Status auf:

* SYNCHRONIZED (SYNCHRONISIERT), wenn das sekundäre Replikat so konfiguriert ist, dass es synchron ist, und die Daten vollständig synchronisiert werden.
* SYNCHRONIZING (WIRD SYNCHRONISIERT), wenn das sekundäre Replikat mit asynchroner Datenverschiebung konfiguriert wird oder wenn es mit synchroner Datenverschiebung synchronisiert wird, aber noch nicht mit dem primären Replikat synchronisiert wurde.

<a name="sql-server-log"></a> Zusätzlich zur unten beschriebenen [dynamischen Verwaltungssicht](#dynamic-management-views) werden Beginn und Abschluss des automatischen Seedings im SQL Server-Protokoll angezeigt:

![SQL Server-Protokoll][2]

## <a name="combine-backup-and-restore-with-automatic-seeding"></a>Kombinieren von Sicherung und Wiederherstellung mit automatischem Seeding

Es ist möglich, das herkömmliche Sichern, Kopieren und Wiederherstellen mit automatischem Seeding zu kombinieren. Stellen Sie in diesem Fall zuerst die Datenbank auf einem sekundären Replikat wieder her, einschließlich aller verfügbaren Transaktionsprotokolle. Aktivieren Sie beim Erstellen der Verfügbarkeitsgruppe als Nächstes das automatische Seeding, um die Datenbank des sekundären Replikats „einzuholen“, als ob eine Sicherung des Protokollfragments wiederhergestellt würde (siehe [Protokollfragmentsicherungen (SQL Server)](../../../relational-databases/backup-restore/tail-log-backups-sql-server.md)).

## <a name="add-a-database-to-an-availability-group-with-automatic-seeding"></a>Hinzufügen einer Datenbank zu einer Verfügbarkeitsgruppe mit automatischem Seeding

Sie können mit automatischem Seeding mit Transact-SQL oder SQL Server Management Studio (SSMS, Version 17 oder höher) eine Datenbank zu einer Verfügbarkeitsgruppe hinzufügen.
Wenn das sekundäre Replikat das automatische Seeding verwendet hat, als es zur Verfügbarkeitsgruppe hinzugefügt wurde, muss weiter nichts unternommen werden. Wenn Sichern, Kopieren und Wiederherstellen verwendet wurden, ändern Sie zuerst den Seedingmodus (siehe nächster Abschnitt). Verwenden Sie beim Hinzufügen der Datenbank dann die „GRANT“-Anweisung. Siehe dazu [Verfügbarkeitsgruppe – Hinzufügen einer Datenbank](availability-group-add-a-database.md).

## <a name="change-the-seeding-mode-of-a-replica"></a>Ändern des Seedingmodus eines Replikats

Der Seedingmodus eines Replikats kann geändert werden, nachdem die Verfügbarkeitsgruppe erstellt wurde, und das automatische Seeding kann so aktiviert oder deaktiviert werden. Das Aktivieren des automatischen Seedings nach dem Erstellen ermöglicht, dass eine Datenbank zur Verfügbarkeitsgruppe hinzugefügt werden kann, die automatisches Seeding verwendet, wenn Sie mit Sichern, Kopieren und Wiederherstellen erstellt wurde. Beispiel:

```
ALTER AVAILABILITY GROUP [AGName]
  MODIFY REPLICA ON 'Replica_Name'
  WITH (SEEDING_MODE = AUTOMATIC)
```

Verwenden Sie zum Deaktivieren des automatischen Seedings den Wert „MANUAL“ (MANUELL).

## <a name="prevent-automatic-seeding-after-an-availability-group-is-created"></a>Verhindern des automatischen Seedings, nachdem eine Verfügbarkeitsgruppe erstellt wurde

Wenn Sie das automatische Seeding für ein sekundäres Replikat nicht vollständig deaktivieren, aber vorübergehend vermeiden möchten, dass das sekundäre Replikat automatisch Datenbanken erstellen kann, müssen Sie der Verfügbarkeitsgruppe die „CREATE“-Berechtigung verweigern. Dies ist der Fall, wenn eine neue Datenbank der Verfügbarkeitsgruppe hinzugefügt wird, aber die Verfügbarkeitsgruppe die Datenbank nicht auf einem sekundären Replikat erstellen können soll.

```
ALTER AVAILABILITY GROUP [AGName] DENY CREATE ANY DATABASE
GO
```

## <a name="monitor-automatic-seeding"></a>Überwachen des automatischen Seedings

Es gibt vier Arten der Überwachung und Problembehandlung des automatischen Seedings:

* [SQL Server-Protokoll](#sql-server-log) wie bereits beschrieben
* [Dynamische Verwaltungssichten](#dynamic-management-views)
* [Tabellen mit Sicherungsverläufen](#backup-history-tables)
* [Erweiterte Ereignisse](#extended-events)

### <a name="dynamic-management-views"></a>Dynamische Verwaltungssichten

Es gibt zwei dynamische Verwaltungssichten (Dynamic Management Views, DMVs) zur Überwachung des Seedings: „sys.dm_hadr_automatic_seeding“ und „sys.dm_hadr_physical_seeding_stats“.

* „sys.dm_hadr_automatic_seeding“ enthält den allgemeinen Status des automatischen Seedings und speichert den Verlauf bei jeder Ausführung (ob erfolgreich oder nicht). Die Spalte „current_state“ weist entweder den Wert „COMPLETED“ (ABGESCHLOSSEN) oder „FAILED“ (FEHLGESCHLAGEN) auf. Verwenden Sie bei dem Wert „FAILED“ (FEHLGESCHLAGEN) den Wert in „failure_state_desc“ zur Diagnose des Problems. Möglicherweise müssen Sie dies mit dem Inhalt des [SQL Server-Protokolls](#sql-server-log) kombinieren, um den Fehler zu finden. Diese DMV wird auf dem primären Replikat und allen sekundären Replikaten aufgefüllt.

* „sys.dm_hadr_physical_seeding_stats“ zeigt den Status des automatischen Seedings bei der Ausführung an. Wie bei „sys.dm_hadr_automatic_seeding“ werden Werte auf dem primären und sekundären Replikat angezeigt, aber dieser Verlauf wird nicht gespeichert. Die Werte gelten nur für die aktuelle Ausführung und werden nicht gespeichert. Zu den wichtigen Spalten zählen „start_time_utc, end_time_utc“, „estimate_time_complete_utc“, „total_disk_io_wait_time_ms“, „total_network_wait_time_ms“ und wenn das Seeding fehlschlägt auch „failure_message“.

### <a name="backup-history-tables"></a>Tabellen mit Sicherungsverläufen

Das automatische Seeding erstellt auch Einträge in den `msdb`-Tabellen, die den Verlauf für Sicherungen und Wiederherstellungen speichern. Auf dem sekundären Replikat, das das automatische Seeding empfängt, verfügt die Spalte „physical_device_name“ der `backupmediafamily`-Tabelle über eine GUID für ihren Wert, und der entsprechende Eintrag in `backupset` enthält den Namen des primären Replikats für „server_name“ und „machine_name“.

### <a name="extended-events"></a>Erweiterte Ereignisse

Das automatische Seeding fügt neue erweiterte Ereignisse zum Nachverfolgen von Statistiken zu Statusänderungen, Fehlern und Leistung während der Initialisierung hinzu.
Das folgende Skript erstellt z.B. eine Sitzung für erweiterte Ereignisse, die Ereignisse im Zusammenhang mit automatischem Seeding erfasst.

```
CREATE EVENT SESSION [AG_autoseed] ON SERVER 
    ADD EVENT sqlserver.hadr_automatic_seeding_state_transition,
    ADD EVENT sqlserver.hadr_automatic_seeding_timeout,
    ADD EVENT sqlserver.hadr_db_manager_seeding_request_msg,
    ADD EVENT sqlserver.hadr_physical_seeding_backup_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_failure,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_target_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_progress,
    ADD EVENT sqlserver.hadr_physical_seeding_restore_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_submit_callback
    ADD TARGET package0.event_file(SET filename=N’autoseed.xel’,max_file_size=(5),max_rollover_files=(4))
  WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)
GO

ALTER EVENT SESSION AlwaysOn_autoseed ON SERVER STATE=START
GO
```

Die folgende Tabelle enthält erweiterte Ereignisse, die sich auf automatisches Seeding beziehen.

|Name|Beschreibung|
|----|-----------|
|hadr_db_manager_seeding_request_msg|Seedinganforderungsnachricht.|
|hadr_physical_seeding_backup_state_change|Statusänderung auf der Sicherungsseite für das physische Seeding.|
|hadr_physical_seeding_restore_state_change|Statusänderung auf der Wiederherstellungsseite für das physische Seeding.|
|hadr_physical_seeding_forwarder_state_change|Statusänderung auf der Weiterleitungsseite für das physische Seeding.|
|hadr_physical_seeding_forwarder_target_state_change|Statusänderung auf der Zielseite der Weiterleitung für das physische Seeding.|
|hadr_physical_seeding_submit_callback|Senderückrufereignis für das physische Seeding.|
|hadr_physical_seeding_failure|Fehlerereignis für das physische Seeding.|
|hadr_physical_seeding_progress|Statusereignis für das physische Seeding.|
|hadr_physical_seeding_schedule_long_task_failure|Fehlerereignis für langen Task im Zeitplan für das physische Seeding.|
|hadr_automatic_seeding_start|Tritt beim Senden eines automatischen Seedingvorgangs auf.|
|hadr_automatic_seeding_state_transition|Tritt beim Statuswechsel eines automatischen Seedingvorgangs auf.|
|hadr_automatic_seeding_success|Tritt beim Erfolg eines automatischen Seedingvorgangs auf.|
|hadr_automatic_seeding_failure|Tritt bei einem Fehler eines automatischen Seedingvorgangs auf.|
|hadr_automatic_seeding_timeout|Tritt beim Timeout eines automatischen Seedingvorgangs auf.|

## <a name="see-also"></a>Siehe auch

[ALTER AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/alter-availability-group-transact-sql)

[CREATE AVAILABILITY GROUP (Transact-SQL)](https://msdn.microsoft.com/library/ff878399.aspx)

[Handbuch zur Problembehandlung und Überwachung von Always On-Verfügbarkeitsgruppen](http://technet.microsoft.com/library/dn135328.aspx)

> Dieser Inhalt wurde von [Allan Hirt](http://mvp.microsoft.com/en-us/PublicProfile/4025254?fullName=Allan%20Hirt), einem Microsoft Most Valued Professional, verfasst.

<!--Image references-->
[1]: ./media/auto-seed-new-availability-group.png
[2]: ./media/auto-seed-sql-server-log.png

