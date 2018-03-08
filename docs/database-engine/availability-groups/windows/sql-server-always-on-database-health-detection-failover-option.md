---
title: "Failoveroption zur Datenbank-Integritätserkennung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- AlwaysOn
- DB_FAILOVER
- Always On
- High Availability
- SQL Server
ms.assetid: d74afd28-25c3-48a1-bc3f-e353bee615c2
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ce5cf8ff6cbbddd0e4a65d702494d80cf7537490
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="availability-group-database-level-health-detection-failover-option"></a>Failoveroption für die Integritätserkennung auf Datenbankebene in einer Verfügbarkeitsgruppe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Ab SQL Server 2016 ist die Option „Integritätserkennung auf Datenbankebene“ (DB_FAILOVER) verfügbar, wenn eine Always On-Verfügbarkeitsgruppe konfiguriert wird. Die Integritätserkennung auf Datenbankebene erkennt, wenn eine Datenbank sich nicht mehr im Onlinestatus befindet oder ein Fehler auftritt und löst ein automatisches Failover der Verfügbarkeitsgruppe aus.

Die Integritätserkennung auf Datenbankebene ist für die gesamte Verfügbarkeitsgruppe aktiviert, wodurch die Datenbank-Integritätserkennung jede Datenbank in der Verfügbarkeitsgruppe überwacht. Sie kann nicht selektiv für bestimmte Datenbanken in der Verfügbarkeitsgruppe aktiviert werden.

## <a name="benefits-of-database-level-health-detection-option"></a>Vorteile der Option „Integritätserkennung auf Datenbankebene“
---
Die Option „Integritätserkennung auf Datenbankebene“ für Verfügbarkeitsgruppen wird weitgehend als eine gute Möglichkeit empfohlen, um die Hochverfügbarkeit Ihrer Datenbanken zu gewährleisten. Sie sollten erwägen, diese für alle Verfügbarkeitsgruppen festzulegen. Wenn Ihre Anwendung von mehreren Datenbanken abhängig ist, um hoch verfügbar zu sein, gruppieren Sie diese in einer Verfügbarkeitsgruppe mit der aktivierten Option für die Datenbank-Integritätserkennung.

Wenn die Option „Integritätserkennung auf Datenbankebene“ aktiviert ist und ein SQL Server beispielsweise für eine der Datenbanken nicht in die Transaktionsprotokolldatei schreiben kann, würde der Status dieser Datenbank einen Fehler anzeigen und die Verfügbarkeitsgruppe bald darauf ein Failover auslösen. Ihre Anwendung könnte die Verbindung wiederherstellen und ihre Arbeit mit minimalen Unterbrechungen fortsetzen, sobald die Datenbanken wieder online sind.

<a name="enabling-database-level-health-detection"></a>Aktivieren der Integritätserkennung auf Datenbankebene
----
Obwohl sie allgemein empfohlen wird, ist die Option für die Datenbank-Integritätserkennung **standardmäßig ausgeschaltet**, um die Abwärtskompatibilität mit den Standardeinstellungen von früheren Versionen zu gewährleisten.

Es gibt mehrere Möglichkeiten, um die Einstellung „Integritätserkennung auf Datenbankebene“ zu aktivieren:

1. Stellen Sie in SQL Server Management Studio eine Verbindung mit dem SQL Server-Datenbankmodul her. Wenn Sie das Fenster des Objekt-Explorers verwenden, klicken Sie mit der rechten Maustaste auf den Knoten „Hohe Verfügbarkeit mit Always On“, und führen Sie den **Assistenten für neue Verfügbarkeitsgruppen** aus. Aktivieren Sie das Kontrollkästchen **Integritätserkennung auf Datenbankebene** auf der Seite „Namen angeben“. Schließen Sie anschließend die restlichen Seiten des Assistenten ab.

   ![Always On-Kontrollkästchen zum Aktivieren der Datenbank-Integritätserkennung](../../../database-engine/availability-groups/windows/media/always-on-enable-database-health-checkbox.png)

2. Lassen Sie die **Eigenschaften** einer bestehenden Verfügbarkeitsgruppe in SQL Server Management Studio anzeigen. Stellen Sie eine Verbindung mit Ihrem SQL Server her. Wenn Sie das Fenster des Objekt-Explorers verwenden, erweitern Sie den Knoten „Hohe Verfügbarkeit mit Always On“. Erweitern Sie „Verfügbarkeitsgruppen“. Klicken Sie mit der rechten Maustaste auf die Verfügbarkeitsgruppe, und wählen Sie „Eigenschaften“ aus. Aktivieren Sie die Option **Integritätserkennung auf Datenbankebene**, und klicken Sie dann auf OK oder legen Sie die Änderung als Skript fest.

   ![Eigenschaften der Integritätserkennung auf Datenbankebene für Always On-Verfügbarkeitsgruppen](../../../database-engine/availability-groups/windows/media/always-on-ag-properties-database-level-health-detection.png)


3. Transact-SQL-Syntax für **CREATE AVAILABILITY GROUP**. Der Parameter „DB_FAILOVER“ akzeptiert die Werte „ON“ oder „OFF“.

   ```Transact-SQL
   CREATE AVAILABILITY GROUP [Contoso-ag]
   WITH (DB_FAILOVER=ON)
   FOR DATABASE [AutoHa-Sample]
   REPLICA ON
       N'SQLSERVER-0' WITH (ENDPOINT_URL = N'TCP://SQLSERVER-0.DOMAIN.COM:5022',
         FAILOVER_MODE = AUTOMATIC, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
       N'SQLSERVER-1' WITH (ENDPOINT_URL = N'TCP://SQLSERVER-1.DOMAIN.COM:5022',
        FAILOVER_MODE = AUTOMATIC, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
    ```

4. Transact-SQL-Syntax für **ALTER AVAILABILITY GROUP**. Der Parameter „DB_FAILOVER“ akzeptiert die Werte „ON“ oder „OFF“.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [Contoso-ag] SET (DB_FAILOVER = ON);

   ALTER AVAILABILITY GROUP [Contoso-ag] SET (DB_FAILOVER = OFF);
   ```

### <a name="caveats"></a>Vorbehalte

Bitte beachten Sie, dass die Option „Integritätserkennung auf Datenbankebene“ derzeit nicht bewirkt, dass SQL Server die Festplattenbetriebszeit und die Verfügbarkeit der Datenbankdateien direkt überwacht. Wenn bei einer Festplatte ein Fehler auftritt oder sie nicht verfügbar ist, wird nur dadurch nicht notwendigerweise ein automatisches Failover ausgelöst.

Wenn sich eine Datenbank beispielsweise im Leerlauf ohne aktive Transaktionen befindet und keine physischen Schreibvorgänge stattfinden, kann auf einige Datenbankdateien nicht mehr zugegriffen werden. SQL Server führt keine E/A-Lese- oder Schreibvorgänge für die Dateien aus und ändert den Status dieser Datenbank nicht sofort, sodass kein Failover ausgelöst werden würde. Wenn dann ein Datenbankprüfpunkt auftritt oder ein physischer Lese- oder Schreibvorgang ausgeführt wird, um eine Abfrage auszuführen, erkennt SQL Server das Dateiproblem und reagiert darauf mit einer Statusänderung der Datenbank. Anschließend würde die Verfügbarkeitsgruppe mit der aktivierten Integritätserkennung auf Datenbankebene wegen der Änderung des Datenbankzustands ein Failover auslösen.

Wenn das SQL-Server-Datenbankmodul beispielsweise eine Datenseite lesen muss, um eine Abfrage auszuführen und die Datenseite im Pufferpoolspeicher zwischengespeichert ist, ist keine Festplatte nötig, die über physischen Zugriff gelesen wird, um die Abfrageanforderung auszuführen. Deshalb löst eine fehlende oder nicht verfügbare Datendatei nicht sofort ein automatisches Failover aus, auch wenn die Option für die Datenbank-Integritätserkennung aktiviert ist, da der Datenbankstatus nicht sofort geändert wird.


## <a name="database-failover-is-separate-from-flexible-failover-policy"></a>Das Datenbank-Failover ist von der flexiblen Failoverrichtlinie getrennt
Durch die Integritätserkennung auf Datenbankebene wird eine flexible Failoverrichtlinie implementiert, die die Schwellenwerte des SQL Server-Prozesszustands für die Failoverrichtlinie konfiguriert. Die Integritätserkennung auf Datenbankebene wird mithilfe des Parameters „DB_FAILOVER“ konfiguriert, während die Option „FAILURE_CONDITION_LEVEL“ der Verfügbarkeitsgruppe separat vorhanden ist, um die Erkennung des SQL Server-Prozesszustands zu konfigurieren. Die beiden Optionen sind unabhängig voneinander.

## <a name="managing-and-monitoring-database-level-health-detection"></a>Verwalten und Überwachen der Integritätserkennung auf Datenbankebene

### <a name="dynamic-management-views"></a>Dynamische Verwaltungssichten

Das DMV-System „sys.availability_groups“ zeigt die Spalte „db_failover“ an, die angibt, ob die Option „Integritätserkennung auf Datenbankebene“ deaktiviert (0) oder aktiviert (1) ist.

```Transact-SQL
select name, db_failover from sys.availability_groups
```


Beispielausgabe für DMV:

NAME  |  db_failover
---------|---------
| Contoso-ag |  1  |

### <a name="errorlog"></a>ErrorLog
Das SQL Server-Fehlerprotokoll (oder der Text aus „sp_readerrorlog“) zeigt wegen der Integritätserkennung auf Datenbankebene die Fehlermeldung 41653 an, wenn eine Verfügbarkeitsgruppe ein Failover ausgelöst hat.

Dieser Auszug aus dem Fehlerprotokoll zeigt beispielsweise, dass das Schreiben eines Transaktionsprotokolls wegen eines Laufwerkproblems fehlgeschlagen ist und daraufhin die Datenbank namens „AutoHa-Sample“ heruntergefahren wurde, wodurch die Integritätserkennung auf Datenbankebene ein Failover der Verfügbarkeitsgruppe ausgelöst hat.

>2016-04-25 12:20:21.08 spid1s      Fehler: 17053, Schweregrad: 16, Status: 1.
>
>2016-04-25 12:20:21.08 spid1s      SQLServerLogMgr::LogWriter: Ein Betriebssystemfehler 21(Das Gerät ist nicht bereit) ist aufgetreten.
>2016-04-25 12:20:21.08 spid1s      Schreibfehler während der Protokollleerung.
>
>2016-04-25 12:20:21.08 spid79      Fehler: 9001, Schweregrad: 21, Status: 4.
>
>2016-04-25 12:20:21.08 spid79      Das Protokoll für die Datenbank „AutoHa-Sample“ ist nicht verfügbar. Überprüfen Sie das Ereignisprotokoll auf verwandte Fehlermeldungen. Beheben Sie ggf. alle Fehler, und starten Sie die Datenbank neu.
>
>**2016-04-25 12:20:21.15 spid79      Fehler: 41653, Schweregrad: 21, Status: 1.**
>
>**2016-04-25 12:20:21.15 spid79      Fehler in der Datenbank „AutoHa-Sample“ (Fehlertyp: 2 „DB_SHUTDOWN“). Dieser verursacht einen Fehler der Verfügbarkeitsgruppe „Contoso-ag“.  Informationen zu den aufgetretenen Fehlern finden Sie im SQL Server-Fehlerprotokoll.  Falls das Problem weiterhin besteht, wenden Sie sich an den Systemadministrator.**
>
>2016-04-25 12:20:21.17 spid79      Zustandsinformationen der Datenbank „AutoHa-Sample“ - Festgeschriebene LSN: „(34:664:1)“    Commit-LSN: „(34:656:1)“    Commitzeit: „Apr 25 2016 12:19PM“
>
>2016-04-25 12:20:21.19 spid15s     Die Verbindung der Always On-Verfügbarkeitsgruppen mit der sekundären Datenbank wurde für die primäre Datenbank „AutoHa-Sample“ auf dem Verfügbarkeitsreplikat „SQLServer-0“ mit der Replikat-ID {c4ad5ea4-8a99-41fa-893e-189154c24b49} beendet. Diese Meldung dient nur zu Informationszwecken. Es ist keine Benutzeraktion erforderlich.
>
>2016-04-25 12:20:21.21 spid75      Always On: Das lokale Replikat der Verfügbarkeitsgruppe „Contoso-ag“  wird in Reaktion auf eine Anforderung vom WSFC (Windows Server Failover Clustering)-Cluster für den Wechsel zur primären Rolle vorbereitet. Diese Meldung dient nur zu Informationszwecken. Es ist keine Benutzeraktion erforderlich.
>
>2016-04-25 12:20:21.21 spid75      Der Status des lokalen Verfügbarkeitsreplikats in der Verfügbarkeitsgruppe „ag“ wurde von „PRIMARY_NORMAL“ in „RESOLVING_NORMAL“ geändert.  Der Status hat sich geändert, weil die Verfügbarkeitsgruppe offline geschaltet wird.  Das Replikat wird offline geschaltet, weil die zugeordnete Verfügbarkeitsgruppe gelöscht wurde, der Benutzer die zugeordnete Verfügbarkeitsgruppe in der WSFC (Windows Server Failover Clustering)-Verwaltungskonsole offline geschaltet hat, oder die Verfügbarkeitsgruppe einen Failover auf eine andere Instanz von SQL Server ausführt.  Weitere Informationen finden Sie im SQL Server-Fehlerprotokoll, in der WSFC-Verwaltungskonsole (Windows Server Failover Clustering) oder im WSFC-Protokoll.

### <a name="extended-event-sqlserveravailabilityreplicadatabasefaultreporting"></a>Erweiterte Ereignis sqlserver.availability_replica_database_fault_reporting

Ab SQL Server 2016 ist ein neues erweitertes Ereignis definiert, das von der Integritätserkennung auf Datenbankebene ausgelöst wird.  Der Ereignisname lautet **sqlserver.availability_replica_database_fault_reporting**

Dieses XEvent wird nur auf dem primären Replikat ausgelöst. Dieses XEvent wird ausgelöst, wenn ein Integritätsproblem auf Datenbankebene auf einer Datenbank erkannt wird, die in einer Verfügbarkeitsgruppe gehostet ist.

Hier finden Sie ein Beispiel zum Erstellen einer XEvent-Sitzung, das dieses Ereignis erfasst. Da kein Pfad angegeben ist, sollte die XEvent-Ausgabedatei im Standardpfad für SQL-Fehlerprotokolle gespeichert sein. Führen Sie folgendes Skript auf dem primären Replikat Ihrer Verfügbarkeitsgruppe aus:

Beispielskript für eine Sitzung für erweiterte Ereignisse
```
CREATE EVENT SESSION [AlwaysOn_dbfault] ON SERVER
ADD EVENT sqlserver.availability_replica_database_fault_reporting
ADD TARGET package0.event_file(SET filename=N'dbfault.xel',max_file_size=(5),max_rollover_files=(4))
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,
    MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)
GO
ALTER EVENT SESSION AlwaysOn_dbfault ON SERVER STATE=START
GO
```

#### <a name="extended-event-output"></a>Erweiterte Ereignisausgabe
Wenn Sie SQL Server Management Studio verwenden, stellen Sie eine Verbindung mit dem primären SQL Server her, erweitern Sie den Knoten „Verwaltung“ und dann „Erweiterte Ereignisse“. Suchen Sie die Sitzung (im obigen Beispiel „Always On_dbfault“ genannt) und erweitern Sie diese, um die Ausgabedateien anzuzeigen. Klicken Sie auf die Ausgabedatei, damit die Ereignisdatei in einer neuen Registerkarte geöffnet wird.

Eine Erläuterung der Felder finden Sie im Folgenden:

|Spaltendaten    | Description
|---------|---------
|availability_group_id  |Die ID der Verfügbarkeitsgruppe.
|availability_group_name    |Der Name der Verfügbarkeitsgruppe.
|availability_replica_id    |Die ID des Verfügbarkeitsreplikats.
|availability_replica_name  |Der Name des Verfügbarkeitsreplikats.
|database_name  |Der Name der Datenbank, die den Fehler meldet.
|database_replica_id    |Die ID der Verfügbarkeitsreplikatdatenbank.
|failover_ready_replicas    |Die Anzahl der sekundären Replikate mit automatischem Failover, die synchronisiert werden.
|fault_type     | Die angegebene Fehler-ID. Mögliche Werte:  <br/> 0: NONE <br/>1: Unknown<br/>2: Shutdown
|is_critical    | Dieser Wert sollte ab SQL Server 2016 immer TRUE für XEvent zurückgeben.


In dieser Beispielausgabe zeigt „fault_type“, dass ein kritisches Ereignis auf der Verfügbarkeitsgruppe „Contoso-ag“ stattgefunden hat, die sich auf dem Replikat „SQLSERVER-1“ befindet. Der Grund dafür ist die Datenbank namens „AutoHaSample2“ mit dem Fehlertyp 2 (Herunterfahren).

|Feld  | value
|---------|---------
|availability_group_id |    24E6FE58-5EE8-4C4E-9746-491CFBB208C1
|availability_group_name |  Contoso-ag
|availability_replica_id    | 3EAE74D1-A22F-4D9F-8E9A-DEFF99B1F4D1
|availability_replica_name |    SQLSERVER-1
|database_name |    AutoHa-Sample2
|database_replica_id | 39971379-8161-4607-82E7-098590E5AE00
|failover_ready_replicas |  1
|fault_type |   2
|is_critical    | Wahr


### <a name="related-references"></a>Verwandte Verweise

* [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)

* [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)

* [Flexible Failover Policy for Automatic Failover of an Availability Group (SQL Server) (Flexible Failoverrichtlinien für automatisches Failover in einer Verfügbarkeitsgruppe (SQL Server))](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)

* [Enhance Always On Failover Policy to Test SQL Server Database Data and Log Drives (Erweiterte Always On-Failoverrichtlinien zum Testen von SQL Server-Datenbankdaten und -Protokolllaufwerken)](https://blogs.msdn.microsoft.com/alwaysonpro/2016/01/14/enhance-alwayson-failover-policy-to-test-sql-server-database-data-and-log-drives/)

* [Erweiterte Ereignisse](../../../relational-databases/extended-events/extended-events.md)



