---
title: SQL Server-Einstellungen unter Linux konfigurieren | Microsoft Docs
description: "Dieser Artikel beschreibt, wie der Mssql-Conf-Tool verwenden, um die Einstellungen für SQL Server-2017 unter Linux konfigurieren."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.workload: On Demand
ms.openlocfilehash: 7b921f563b769a1a4c6a3edb5089a04050d0df74
ms.sourcegitcommit: 57f45ee008141ddf009b1c1195442529e0ea1508
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>Konfigurieren von SQL Server unter Linux mit dem Mssql-Conf-tool

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

**MSSQL-Conf** ein Konfigurationsskript, der mit SQL Server-2017 für Red Hat Enterprise Linux, SUSE Linux Enterprise Server und Ubuntu installiert ist. Sie können dieses Hilfsprogramm verwenden, um die folgenden Parameter festzulegen:

|||
|---|---|
| [Agent](#agent) | Aktivieren Sie SQL Server-Agent |
| [Sortierung](#collation) | Legen Sie eine neue Sortierung für SQL Server unter Linux. |
| [Kundenfeedback](#customerfeedback) | Wählen Sie aus, und zwar unabhängig davon, ob SQL Server Feedback an Microsoft sendet. |
| [Datenbank-E-Mail-Profil](#dbmail) | Legen Sie das standardmäßige Datenbank-Mailprofil für SQL Server on Linux |
| [Standarddatenverzeichnis](#datadir) | Ändern Sie das Standardverzeichnis für neue SQL Server-Datenbank-Datendateien (MDF). |
| [Standard-Protokollverzeichnis](#datadir) | Ändert das Standardverzeichnis für neue SQL Server-Protokolldateien (LDF) Datenbankdateien an. |
| [Standardverzeichnis für master-Datenbank-Datei](#masterdatabasedir) | Ändert das Standardverzeichnis für die master-Datenbank-Dateien auf vorhandenen SQL-Installation.|
| [Standarddateiname für die master-Datenbank](#masterdatabasename) | Ändert den Namen der master-Datenbank-Dateien. |
| [Dump Standardverzeichnis](#dumpdir) | Ändern Sie das Standardverzeichnis für neue Speicherabbilder und andere Dateien zur Problembehandlung. |
| [Fehler-Standardprotokollverzeichnis](#errorlogdir) | Ändert das Standardverzeichnis für neue SQL Server-Fehlerprotokoll, Standard-Profiler-Ablaufverfolgung System Health Sitzung XE und Hekaton Sitzung XE-Dateien. |
| [Standardsicherungsverzeichnis](#backupdir) | Ändern Sie das Standardverzeichnis für neue Sicherungsdateien an. |
| [Dumptyp](#coredump) | Wählen Sie den Typ der Dump Speicherabbild sammeln. |
| [High Availability (Hohe Verfügbarkeit)](#hadr) | Aktivieren von Verfügbarkeitsgruppen. |
| [Lokales Verzeichnis für Überwachung](#localaudit) | Legen Sie ein hinzuzufügende Überwachungsdateien lokalen Verzeichnis. |
| [Gebietsschema](#lcid) | Legen Sie das Gebietsschema für SQL Server verwenden. |
| [Arbeitsspeichergrenze](#memorylimit) | Legen Sie den Höchstwert des Arbeitsspeichers für SQL Server. |
| [TCP-port](#tcpport) | Ändern Sie den Port, auf dem SQL Server für Verbindungen lauscht. |
| [TLS](#tls) | Konfigurieren Sie die Sicherheit auf Transportebene. |
| [Ablaufverfolgungsflags](#traceflags) | Legen Sie die Ablaufverfolgungsflags, die der Dienst verwenden soll. |

> [!TIP]
> Einige dieser Einstellungen können auch mit Umgebungsvariablen konfiguriert werden. Weitere Informationen finden Sie unter [konfigurieren Sie SQL Server-Einstellungen mit Umgebungsvariablen](sql-server-linux-configure-environment-variables.md).

## <a name="usage-tips"></a>Tipps zur Verwendung

* Stellen Sie für AlwaysOn-Verfügbarkeitsgruppen und freigegebene Datenträgercluster immer die gleichen Änderungen an der Konfiguration auf jedem Knoten ein.

* Für die freigegebenen Datenträger Clusterszenario: versuchen Sie nicht, starten die **Mssql Server** Dienst, um Änderungen zu übernehmen. SQL Server wird als Anwendung ausgeführt. Nehmen Sie stattdessen die Ressource offline und anschließend wieder online.

* Diese Beispiele ausführen Mssql-Conf, indem Sie den vollständigen Pfad angeben: **/opt/mssql/bin/mssql-conf**. Falls gewünscht, um stattdessen an, dass der Pfad zu navigieren, Mssql-Conf im Kontext des aktuellen Verzeichnisses ausgeführt: **. / Mssql-Conf**.

## <a id="agent"></a> Aktivieren Sie SQL Server-Agent

Die **sqlagent.enabled** kann festgelegt werden, [SQL Server-Agent](sql-server-linux-run-sql-server-agent-job.md). Standardmäßig ist SQL Server-Agent deaktiviert.

Um diese Einstellungen zu ändern, verwenden Sie die folgenden Schritte aus:

1. Aktivieren Sie die SQL Server-Agent:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

1. Starten Sie SQL Server-Dienst neu:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="collation"></a> Ändern Sie die SQL Server-Sortierung

Die **Satz Sortierung** Option ändert den Sortierungswert auf eines der unterstützten Sortierungen.

1. Erste [Sichern einer beliebigen Benutzerdatenbank](sql-server-linux-backup-and-restore-database.md) auf dem Server.

1. Verwenden Sie dann die [Sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) gespeicherte Prozedur, um die Benutzerdatenbanken zu trennen.

1. Führen Sie die **Satz Sortierung** aus, und befolgen Sie die Anweisungen:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. Das Hilfsprogramm Mssql-Conf versucht, auf den Wert der angegebenen Sortierung ändern und den Dienst neu. Wenn Fehler vorliegen, setzt er die Sortierung auf den vorherigen Wert zurück.

1. Werden Ihre Benutzer-datenbanksicherungen.

Führen Sie eine Liste der unterstützten Sortierungen, die [Sys. fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) Funktion: `SELECT Name from sys.fn_helpcollations()`.

## <a id="customerfeedback"></a> Konfigurieren von Kundenfeedback

Die **telemetry.customerfeedback** Änderungen festlegen, ob SQL Server Feedback an Microsoft oder nicht sendet. Standardmäßig ist dieser Wert festgelegt, um **"true"**. Um den Wert zu ändern, führen Sie die folgenden Befehle ein:

1. Führen Sie das Skript Mssql-Conf als Root mit der **festgelegt** -Befehl für **telemetry.customerfeedback**. Im folgende Beispiel wird deaktiviert Kundenfeedback durch Angabe **"false"**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Starten Sie SQL Server-Dienst neu:

   ```bash
   sudo systemctl restart mssql-server
   ```

Weitere Informationen finden Sie unter [Feedback von Kunden für SQL Server on Linux](sql-server-linux-customer-feedback.md).

## <a id="datadir"></a> Ändern Sie das Standardverzeichnis Daten- oder Protokolldatei

Die **filelocation.defaultdatadir** und **filelocation.defaultlogdir** Einstellungen ändern Sie den Speicherort, an dem die neue Datenbank und-Protokolldateien erstellt werden. Dieser Speicherort ist standardmäßig /var/opt/mssql/data. Um diese Einstellungen zu ändern, verwenden Sie die folgenden Schritte aus:

1. Erstellen Sie das Zielverzeichnis für die neue Datenbank Daten-und Protokolldateien. Das folgende Beispiel erstellt ein neues **/Tmp/Daten** Verzeichnis:

   ```bash
   sudo mkdir /tmp/data
   ```

1. Ändern Sie den Besitzer und die Gruppe des Verzeichnisses, das die **Mssql** Benutzer:

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. Verwenden der Mssql-Conf so ändern Sie das Standardverzeichnis für die Daten mit der **festgelegt** Befehl:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. Starten Sie SQL Server-Dienst neu:

   ```bash
   sudo systemctl restart mssql-server
   ```

1. Jetzt werden die Datenbankdateien für die neuen erstellten Datenbanken in den neuen Speicherort gespeichert werden. Wenn Sie den Speicherort der Protokolldateien (LDF) der neuen Datenbanken ändern möchten, können Sie den folgenden "Set"-Befehl verwenden:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. Mit diesem Befehl auch davon ausgegangen, dass ein Protokollverzeichnis/Tmp/vorhanden ist, wird unter dem Benutzer und Gruppe **Mssql**.


## <a id="masterdatabasedir"></a> Ändern Sie das Standard-master-Datenbank-Dateiverzeichnis

Die **filelocation.masterdatafile** und **filelocation.masterlogfile** Einstellung ändert sich den Speicherort, in dem die SQL Server-Datenbankmodul, für die master-Datenbank-Dateien sucht. Dieser Speicherort ist standardmäßig /var/opt/mssql/data. 

Um diese Einstellungen zu ändern, verwenden Sie die folgenden Schritte aus:

1. Erstellen Sie das Zielverzeichnis für neue Fehlerprotokolldateien. Das folgende Beispiel erstellt ein neues **/Tmp/Masterdatabasedir** Verzeichnis:

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. Ändern Sie den Besitzer und die Gruppe des Verzeichnisses, das die **Mssql** Benutzer:

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. Verwenden der Mssql-Conf so ändern Sie das Standardverzeichnis für die master-Datenbank für die master Daten und Protokolldateien mit den **festgelegt** Befehl:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

1. Beenden Sie den SQL Server-Dienst:

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Verschieben Sie die Dateien master.mdf und masterlog.ldf: 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. Starten Sie den SQL Server-Dienst:

   ```bash
   sudo systemctl start mssql-server
   ```
   
> [!NOTE]
> Wenn SQL Server im angegebenen Verzeichnis die Dateien master.mdf und mastlog.ldf finden kann, eine Kopie vorlagenbasierte Systemdatenbanken werden automatisch im angegebenen Verzeichnis erstellt, und SQL Server wird erfolgreich gestartet. Metadaten wie etwa von Benutzerdatenbanken, Server-Anmeldungen, Serverzertifikate, Verschlüsselungsschlüssel, SQL Agent-Aufträge oder Kennwort für SA-Anmeldung wird jedoch nicht in die neue master-Datenbank aktualisiert werden. Sie müssen zum Beenden von SQL Server und verschieben Ihre alte Dateien master.mdf und mastlog.ldf an den neuen angegebenen Speicherort aus, und starten Sie SQL Server, um den Vorgang fortzusetzen, verwenden die vorhandene Metadaten. 


## <a id="masterdatabasename"></a> Ändern Sie den Namen der master-Datenbank.

Die **filelocation.masterdatafile** und **filelocation.masterlogfile** Einstellung ändert sich den Speicherort, in dem die SQL Server-Datenbankmodul, für die master-Datenbank-Dateien sucht. Dieser Speicherort ist standardmäßig /var/opt/mssql/data. Um diese Einstellungen zu ändern, verwenden Sie die folgenden Schritte aus:

1. Beenden Sie den SQL Server-Dienst:

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Verwenden der Mssql-Conf so ändern Sie die Namen der erwarteten master-Datenbank für die master Daten und Protokolldateien mit den **festgelegt** Befehl:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data /mastlognew.ldf
   ```

1. Ändern Sie den Namen der der master-Datenbank Daten und Protokolldateien 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. Starten Sie den SQL Server-Dienst:

   ```bash
   sudo systemctl start mssql-server
   ```



## <a id="dumpdir"></a> Ändern Sie den Speicherort des Standardverzeichnisses dump

Die **filelocation.defaultdumpdir** Einstellung ändert sich den Standardspeicherort, in dem für den Speicher und SQL-Dumps generiert werden, wenn ein Absturz (Crash) vorhanden ist. Standardmäßig werden diese Dateien in /var/opt/mssql/log generiert.

Um den neuen Speicherort einzurichten, verwenden Sie die folgenden Befehle ein:

1. Erstellen Sie das Zielverzeichnis für neue debugdumpdateien. Das folgende Beispiel erstellt ein neues **/Tmp/Dump** Verzeichnis:

   ```bash
   sudo mkdir /tmp/dump
   ```

1. Ändern Sie den Besitzer und die Gruppe des Verzeichnisses, das die **Mssql** Benutzer:

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. Verwenden der Mssql-Conf so ändern Sie das Standardverzeichnis für die Daten mit der **festgelegt** Befehl:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. Starten Sie SQL Server-Dienst neu:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="errorlogdir"></a> Ändern Sie die Fehler Directory Standardspeicherort der Protokolldatei

Die **filelocation.errorlogfile** Einstellung ändert sich die Position, in dem das neue Fehlerprotokoll, Standard-Profiler-Ablaufverfolgung systemintegritätssitzung XE und Hekaton-Sitzungsdateien XE erstellt werden. Dieser Speicherort ist standardmäßig /var/opt/mssql/log. Das Verzeichnis, in dem SQL-Fehlerprotokoll-Datei festgelegt ist, wird das Standardprotokollverzeichnis für andere Protokolle.

Um diese Einstellungen zu ändern:

1. Erstellen Sie das Zielverzeichnis für neue Fehlerprotokolldateien. Das folgende Beispiel erstellt ein neues **/Tmp/Logs** Verzeichnis:

   ```bash
   sudo mkdir /tmp/logs
   ```

1. Ändern Sie den Besitzer und die Gruppe des Verzeichnisses, das die **Mssql** Benutzer:

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. Verwenden der Mssql-Conf so ändern Sie den standardmäßigen Errorlog-Dateinamen mit der **festgelegt** Befehl:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. Starten Sie SQL Server-Dienst neu:

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a id="backupdir"></a> Ändern des Standardspeicherorts für das Sicherungsverzeichnis

Die **filelocation.defaultbackupdir** Einstellung ändert sich den Standardspeicherort, an dem die Sicherungsdateien generiert werden. Standardmäßig werden diese Dateien in /var/opt/mssql/data generiert.

Um den neuen Speicherort einzurichten, verwenden Sie die folgenden Befehle ein:

1. Erstellen Sie das Zielverzeichnis für neue Sicherungsdateien an. Das folgende Beispiel erstellt ein neues **/Tmp/Sicherung** Verzeichnis:

   ```bash
   sudo mkdir /tmp/backup
   ```

1. Ändern Sie den Besitzer und die Gruppe des Verzeichnisses, das die **Mssql** Benutzer:

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. Verwenden Sie Mssql-Conf, um das Standardsicherungsverzeichnis mit dem Befehl "Set" zu ändern:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. Starten Sie SQL Server-Dienst neu:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a> Core Dump Einstellungen angeben

Tritt eine Ausnahme in einem SQL Server-Prozesse auf, wird SQL Server ein Speicherabbild erstellt.

Es gibt zwei Optionen für die Steuerung des Typs der Speicher ein Abbild sichert, dass SQL Server erfasst: **coredump.coredumptype** und **coredump.captureminiandfull**. Diese beziehen sich auf die beiden Phasen der Erfassung des Core Dump. 

Die erste Phase Erfassung wird gesteuert, indem die **coredump.coredumptype** Einstellung, die festlegt, den Typ der Dumpdatei, während eine Ausnahme generiert. Die zweite Phase ist aktiviert, wenn die **coredump.captureminiandfull** Einstellung. Wenn **coredump.captureminiandfull** festgelegt ist, auf "true", das Speicherabbild durch die angegebene Datei **coredump.coredumptype** wird generiert, und eine zweite Miniabbild wird ebenfalls generiert. Festlegen von **coredump.captureminiandfull** auf "false" verhindert die zweite Erfassung versuchen.

1. Entscheiden Sie, ob sowohl vollständige als auch Mini-Dumpdateien mit Erfassen der **coredump.captureminiandfull** Einstellung.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    Standard: **"false"**

1. Geben Sie die Dumpdatei mit der **coredump.coredumptype** Einstellung.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    Standard: **Miniplus**

    Die folgende Tabelle enthält die möglichen **coredump.coredumptype** Werte.

    | Typ | Description |
    |-----|-----|
    | **mini** | Mini lautet der kleinste Dump-Dateityp. Verwendet er die Linux-System-Informationen, um zu bestimmen, Threads und Module im Prozess. Das Speicherabbild enthält nur die Host-Umgebung Threadstapel und Modulen. Es enthält keine indirekte Speicherreferenzen oder Globals. |
    | **miniplus** | MiniPlus Mini ähnelt, aber sie zusätzlichen Arbeitsspeicher enthält. Er versteht im Rahmen der SQLPAL und der hostumgebung die folgenden Speicherbereiche das Speicherabbild hinzufügen:</br></br> -Globals verschiedene</br> -Alle Arbeitsspeicher über 64TB</br> -Alle Regionen in gefunden benannte **/proc/$ pid/Zuordnungen**</br> -Indirekte Arbeitsspeicher von Threads und Stapel</br> -Thread Informationen</br> -Der Teb und den Peb des verknüpften</br> -Modulinformationen</br> -Struktur VMM und VAD |
    | **filtered** | Gefilterte mithilfe einer Subtraktion basierende entwerfen, in dem alle Arbeitsspeicher des Prozesses enthalten ist, sofern nicht ausdrücklich ausgeschlossen. Der Entwurf versteht im Rahmen der SQLPAL und der hostumgebung, Ausschließen von bestimmten Regionen von das Speicherabbild.
    | **full** | Vollständige befindet, die alle Regionen enthält vollständige prozessdump **/proc/$ pid/Zuordnungen**. Dies wird nicht gesteuert, indem **coredump.captureminiandfull** Einstellung. |

## <a id="dbmail"></a> Legen Sie das standardmäßige Datenbank-Mailprofil für SQL Server on Linux

Die **sqlpagent.databasemailprofile** können Sie das Standardprofil für die DB-Mail für e-Mail-Benachrichtigungen festlegen.

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> Hohe Verfügbarkeit

Die **hadr.hadrenabled** Option Verfügbarkeitsgruppen auf SQL Server-Instanz aktiviert. Der folgende Befehl aktiviert die Verfügbarkeitsgruppen durch Festlegen von **hadr.hadrenabled** auf 1. Sie müssen neu starten, SQL Server für die Einstellung wirksam wird.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

Informationen, wie dies mit Verfügbarkeitsgruppen verwendet wird, finden Sie unter den folgenden zwei Themen.

- [Konfigurieren Sie Always On-Verfügbarkeitsgruppe für SQLServer on Linux](sql-server-linux-availability-group-configure-ha.md)
- [Konfigurieren Sie Skalieren von Lesevorgängen verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-rs.md)

## <a id="localaudit"></a> Die lokale Überwachung Verzeichnis festlegen

Die **telemetry.userrequestedlocalauditdirectory** Einstellung ermöglicht das lokale Überwachung und ermöglicht Ihnen das Verzeichnis festlegen, in dem die lokale Überwachung protokolliert werden erstellt.

1. Erstellen Sie ein Zielverzeichnis für neue lokale Überwachungsprotokolle ein. Das folgende Beispiel erstellt ein neues **/Tmp/Audit** Verzeichnis:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. Ändern Sie den Besitzer und die Gruppe des Verzeichnisses, das die **Mssql** Benutzer:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. Führen Sie das Skript Mssql-Conf als Root mit der **festgelegt** -Befehl für **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. Starten Sie SQL Server-Dienst neu:

   ```bash
   sudo systemctl restart mssql-server
   ```

Weitere Informationen finden Sie unter [Feedback von Kunden für SQL Server on Linux](sql-server-linux-customer-feedback.md).

## <a id="lcid"></a> Ändern Sie das SQL Server-Gebietsschema

Die **language.lcid** ändert sich das SQL Server-Gebietsschema auf alle unterstützten Sprachen-ID (LCID) festlegen. 

1. Im folgende Beispiel ändert das Gebietsschema auf Französisch (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. Starten Sie den SQL Server-Dienst, um die Änderungen zu übernehmen:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> Das Arbeitsspeicherlimit festgelegt

Die **memory.memorylimitmb** Steuerelemente Größe des physischen Arbeitsspeichers (in MB) verfügbar auf SQL Server festlegen. Der Standardwert ist 80 % des physischen Arbeitsspeichers.

1. Führen Sie das Skript Mssql-Conf als Root mit der **festgelegt** -Befehl für **memory.memorylimitmb**. Im folgenden Beispiel wird den verfügbare Speicher mit SQL Server zum 3,25 GB (3328 MB) an.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. Starten Sie den SQL Server-Dienst, um die Änderungen zu übernehmen:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="tcpport"></a> Ändern Sie den TCP-port

Die **network.tcpport** Einstellung ändert sich des TCP-Ports, auf dem SQL Server Verbindungen überwacht. Standardmäßig wird dieser Port auf 1433 festgelegt. Um den Port zu ändern, führen Sie die folgenden Befehle ein:

1. Führen Sie das Skript Mssql-Conf als Stamm mit dem Befehl "set" für "network.tcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

1. Starten Sie SQL Server-Dienst neu:

   ```bash
   sudo systemctl restart mssql-server
   ```

1. Wenn nun eine Verbindung mit SQL Server herstellen, müssen Sie den benutzerdefinierten Port durch ein Komma (,) nach der Hostname oder IP-Adresse angeben. Um mit SQLCMD eine Verbindung herzustellen, würden Sie z. B. den folgenden Befehl verwenden:

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> TLS-Einstellungen angeben

Die folgenden Optionen konfigurieren TLS für eine Instanz von SQL Server auf dem Linux ausgeführt wird.

|Option |Description |
|--- |--- |
|**network.forceencryption** |Wenn der Wert 1, dann [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] erzwingt, dass alle Verbindungen verschlüsselt werden. Standardmäßig ist diese Option 0. |
|**network.tlscert** |Der absolute Pfad zu dem Zertifikat-Datei mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für TLS-Verbindungen verwendet. Beispiel: `/etc/ssl/certs/mssql.pem` der Zertifikatsdatei muss der Mssql-Konto zugänglich sein. Microsoft empfiehlt, Einschränken des Zugriffs auf die Datei mit `chown mssql:mssql <file>; chmod 400 <file>`. |
|**network.tlskey** |Der absolute Pfad zum privaten Schlüssel Datei, die mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für TLS-Verbindungen verwendet. Beispiel: `/etc/ssl/private/mssql.key` der Zertifikatsdatei muss der Mssql-Konto zugänglich sein. Microsoft empfiehlt, Einschränken des Zugriffs auf die Datei mit `chown mssql:mssql <file>; chmod 400 <file>`. |
|**network.tlsprotocols** |Eine durch Trennzeichen getrennte Liste der TLS-Protokolle von SQL Server zulässig sind. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] immer versucht, die stärkste zulässige Protokoll ausgehandelt. Wenn ein Client ein zulässige Protokoll nicht unterstützt [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] lehnt der Verbindungsversuch fehl.  Aus Kompatibilitätsgründen sind alle unterstützten Protokolle (1,2, 1.1, 1.0) standardmäßig zulässig.  Wenn Ihre Clients TLS 1.2 unterstützt, empfiehlt Microsoft, sodass nur TLS 1.2. |
|**network.tlsciphers** |Gibt an, welche Chiffren zulässig sind [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für TLS. Diese Zeichenfolge muss formatiert werden, pro [OpenSSLs-Chiffre Listenformat](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). Im Allgemeinen müssen Sie nicht diese Option zu ändern. <br /> Standardmäßig sind die folgenden Chiffren zulässig: <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Pfad zu der Kerberos-Keytab-Datei |

Ein Beispiel der Verwendung von TLS-Einstellungen finden Sie unter [Verschlüsseln von Verbindungen zu SQL Server on Linux](sql-server-linux-encrypted-connections.md).

## <a id="traceflags"></a> Aktivieren/Deaktivieren von Ablaufverfolgungsflags

Dies **Ablaufverfolgungsflag** Option aktiviert oder deaktiviert die Traceflags für den Start des SQL Server-Diensts. Zum Aktivieren/Deaktivieren des ein Ablaufverfolgungsflag, verwenden Sie die folgenden Befehle:

1. Aktivieren Sie ein Ablaufverfolgungsflag mit dem folgenden Befehl ein. Z. B. für Ablaufverfolgungsflag 1234:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. Sie können mehrere Traceflags aktivieren, indem Sie diese separat angeben:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. Auf ähnliche Weise, können Sie eine oder mehrere aktivierte Traceflags deaktivieren, indem sie angeben und das Hinzufügen der **deaktiviert** Parameter:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. Starten Sie den SQL Server-Dienst, um die Änderungen zu übernehmen:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>Entfernen einer Einstellung

Festlegung eine Einstellung vorgenommen mit `mssql-conf set`, rufen Sie **Mssql-Conf** mit der `unset` Option und der Name der Einstellung. Dies löscht die Einstellung, die effektiv auf den Standardwert zurückgeben.

1. Das folgende Beispiel löscht die **network.tcpport** Option.

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. Starten Sie SQL Server-Dienst neu.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>Anzeigen der aktuellen Einstellungen

So konfiguriert, alle Einstellungen, führen Sie den folgenden Befehl aus, um den Inhalt der Ausgabe der **mssql.conf** Datei:

```bash
sudo cat /var/opt/mssql/mssql.conf
```

Beachten Sie, dass alle Einstellungen in dieser Datei nicht angezeigt. die Standardwerte verwenden. Der nächste Abschnitt enthält ein Beispiel für **mssql.conf** Datei.

## <a name="mssqlconf-format"></a>mssql.conf format

Die folgenden **/var/opt/mssql/mssql.conf** Datei bietet ein Beispiel für jede Einstellung. Verwenden Sie dieses Format manuell vornehmen von Änderungen an der **mssql.conf** Datei nach Bedarf. Wenn Sie die Datei manuell ändern, müssen Sie SQL Server neu starten, bevor die Änderungen angewendet werden. Verwenden der **mssql.conf** Datei mit Docker, benötigen Sie Docker [behält Ihre Daten](sql-server-linux-configure-docker.md). Fügen Sie zuerst eine vollständige **mssql.conf** Datei auf Ihrem Hostverzeichnis, und führen Sie den Container. Es ist ein Beispiel hierzu finden Sie unter [Kundenfeedback](sql-server-linux-customer-feedback.md).

```ini
[EULA]
accepteula = Y

[coredump]
captureminiandfull = true
coredumptype = full

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

## <a name="next-steps"></a>Nächste Schritte

Um stattdessen Umgebungsvariablen verwenden, um einige dieser konfigurationsänderungen vornehmen, finden Sie unter [konfigurieren Sie SQL Server-Einstellungen mit Umgebungsvariablen](sql-server-linux-configure-environment-variables.md).

Andere Verwaltungstools und Szenarien finden Sie unter [Verwalten von SQL Server on Linux](sql-server-linux-management-overview.md).
