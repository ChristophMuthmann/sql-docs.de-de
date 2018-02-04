---
title: "Aktualisiert – SQL Server on Linux Docs | Microsoft Docs"
description: "Aktualisierter Inhalt in zuletzt geänderten Dokumentation für Microsoft SQL Server on Linux Codeausschnitte anzeigen"
services: na
documentationcenter: 
author: MightyPen
manager: craigg
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: d477af0c4c7027892d4ade8e586c9a9b908a05ea
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Neue und zuletzt aktualisiert: SQL Server on Linux Docs



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates*: &nbsp; **28.09.2017** &nbsp; – bis – &nbsp; **02.12.2017**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Microsoft SQL Server on Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Führen Sie die SQL Server-2017 in der cloud](quickstart-install-connect-clouds.md)
2. [Ändern Sie Repositorys aus dem Repository Vorschau in GA-repository](sql-server-linux-change-repo.md)
3. [Bewährte Methoden für Leistung und Konfigurationsrichtlinien für SQL Server-2017 unter Linux](sql-server-linux-performance-best-practices.md)
4. [Failoverclusterinstanzen - SQLServer on Linux](sql-server-linux-shared-disk-cluster-concepts.md)
5. [Konfigurieren der Failover-Clusterinstanz - iSCSI - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
6. [Konfigurieren Sie Failoverclusterinstanz – NFS - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
7. [Konfigurieren der Failover-Clusterinstanz - SMB - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
8. [Failoverclusterinstanz – SQL Server on Linux Betrieb](sql-server-linux-shared-disk-cluster-operate.md)
9. [Einschränkungen und bekannten Probleme für SSIS unter Linux](sql-server-linux-ssis-known-issues.md)
10. [Wiederherstellen einer SQL Server-Datenbank in einem Linux-Docker-container](tutorial-restore-backup-in-sql-server-container.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Führen Sie die 2017 von SQL Server-Container-Image mit Docker](#TitleNum_1)
2. [Konfigurieren von Always On-verfügbarkeitsgruppe für SQL Server on Linux](#TitleNum_2)
3. [Hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](#TitleNum_3)
4. [Konfigurieren von SQL Server-2017 Container Bilder auf Docker](#TitleNum_4)
5. [Verschlüsseln von Verbindungen zu SQLServer on Linux](#TitleNum_5)
6. [Erstellen und Ausführen von SQL Server-Agent-Aufträge unter Linux](#TitleNum_6)
7. [-Installationsleitfaden für SQL Server on Linux](#TitleNum_7)
8. [Konfigurieren Sie Failoverclusterinstanz – SQL Server für Linux (RHEL)](#TitleNum_8)
9. [Problembehandlung bei SQLServer on Linux](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-run-the-sql-server-2017-container-image-with-dockerquickstart-install-connect-dockermd"></a>1. &nbsp;[2017 von SQL Server-Container-Image mit Docker ausführen](quickstart-install-connect-docker.md)

*Aktualisiert: 30.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 261.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2aaf953c2f1fb675b1304186108fbef1eebf6f8f f7cd42bb320a8892a5ec63ce999186438097636a  (PR=4150  ,  Filename=quickstart-install-connect-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



**Entfernen Sie Ihres Containers**


Wenn Sie den SQL Server-Container, die in diesem Lernprogramm verwendete entfernen möchten, führen Sie die folgenden Befehle aus:

```
sudo docker stop sql1
sudo docker rm sql1
```

```
docker stop sql1
docker rm sql1
```

> [!WARNING]
> Beenden und Entfernen eines Containers dauerhaft löscht alle SQL Server-Daten im Container. Wenn Sie Ihre Daten zu erhalten müssen [erstellen, und kopieren Sie eine Sicherungsdatei aus dem Container--tutorial-restore-backup-in-sql-server-container.md), oder verwenden Sie eine [Container Datenpersistenz technique--sql-server-linux-configure-docker.md#persist).




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-always-on-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-configure-hamd"></a>2. &nbsp;[Konfigurieren von Always On-verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 129.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c7e6bc862e5b062a855918efbeee5fe748b7236 6900c9a30ce04ce54e7aaa270ef7d276c18f9afd  (PR=4150  ,  Filename=sql-server-linux-availability-group-configure-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



- Verfügbarkeitsgruppe mit zwei synchronen Replikaten und ein Replikat für die Konfiguration zu erstellen:

   >[!IMPORTANT]
   >Diese Architektur ermöglicht eine beliebige Edition von SQL Server das dritte Replikat hosten. Beispielsweise kann das dritte Replikat auf SQL Server Enterprise Edition gehostet werden. Enterprise Edition, ist der einzige gültige Endpunkttyp `WITNESS`.

```sql
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
       N'**<node1>**' WITH (
          ENDPOINT_URL = N'tcp://**<node1>**:**<5022>**',
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
          FAILOVER_MODE = EXTERNAL,
          SEEDING_MODE = AUTOMATIC
          ),
       N'**<node2>**' WITH (
          ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**',
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
          FAILOVER_MODE = EXTERNAL,
          SEEDING_MODE = AUTOMATIC
          ),
       N'**<node3>**' WITH (
          ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**',
          AVAILABILITY_MODE = CONFIGURATION_ONLY
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-high-availability-and-data-protection-for-availability-group-configurationssql-server-linux-availability-group-hamd"></a>3. &nbsp;[Hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](sql-server-linux-availability-group-ha.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_2) | [Weiter](#TitleNum_4))

<!-- Source markdown line 106.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e6bee794ce19f1ed62298b4a0cce7207550f1595 b64726cd6e91721850721786d26c170d59fc320a  (PR=4150  ,  Filename=sql-server-linux-availability-group-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



Der Standardwert für `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` ist 0. In der folgenden Tabelle wird die Verfügbarkeit Verhalten beschrieben.

| |Hohe Verfügbarkeit & </br> Datenschutz | Schutz von Daten
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|Ausfall des primären Replikats | Automatisches Failover. Neue primäre ist R / w. | Automatisches Failover. Neue primäre ist nicht verfügbar für Benutzertransaktionen.
|Ausfall des sekundären Replikats | Primäre ist R/W, läuft Sie ungeschützt zu Datenverlusten (falls der primäre schlägt fehl, und kann nicht wiederhergestellt werden). Kein automatisches Failover, wenn das primäre schlägt auch fehl. | Primäre ist nicht verfügbar für Benutzertransaktionen. Kein Replikat für ein Failover, wenn das primäre schlägt auch fehl.
|Konfiguration nur Replikat Ausfall | Ein Primärschlüssel ist R / w. Kein automatisches Failover, wenn das primäre schlägt auch fehl. | Ein Primärschlüssel ist R / w. Kein automatisches Failover, wenn das primäre schlägt auch fehl.
|Synchrone sekundäre + -Konfiguration nur Replikat Ausfall| Primäre ist nicht verfügbar für Benutzertransaktionen. Kein automatisches Failover. | Primäre ist nicht verfügbar für Benutzertransaktionen. Kein Replikat für ein Failover aus, wenn auch primäre ein Fehler auftritt.
<sup>*</sup>Standardwert

>[!NOTE]
>Die Instanz von SQL Server, die die Konfiguration nur Replikat hostet, kann auch andere Datenbanken hosten. Sie können auch als eine einzige Konfigurationsdatenbank für mehr als eine verfügbarkeitsgruppe teilnehmen.

**Anforderungen**


* Alle Replikate in einer verfügbarkeitsgruppe mit einem einzigen Configuration-Replikat müssen SQL Server 2017 CU 1 oder höher sein.
* Eine beliebige Edition von SQL Server kann eine einzige Replikat Konfiguration, einschließlich SQL Server Express hosten.
* Die verfügbarkeitsgruppe benötigt mindestens ein sekundäres Replikat – zusätzlich zu das primäre Replikat.
* Nur Replikate Konfiguration zählen nicht für die maximale Anzahl der Replikate pro Instanz von SQL Server. SQL Server standard Edition kann bis zu drei Replikate, SQL Server Enterprise Edition können bis zu 9.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>4. &nbsp;[Konfigurieren von SQL Server-2017 Container Bilder auf Docker](sql-server-linux-configure-docker.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_3) | [Weiter](#TitleNum_5))

<!-- Source markdown line 34.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c759fb88ae8d654414202f28c5fc58dfd02581bf fd270118f2f4608fceaf563fc143951b41097bdb  (PR=4150  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



Dieses Thema enthält Szenarien für die weitere Verwendung in den folgenden Abschnitten.

**<a id="production"></a>Führen Sie Produktion containerimages**


Quickstart im vorherigen Abschnitt führt die kostenlose Developer Edition von SQL Server von Docker Hub. Die meisten Informationen gilt weiterhin, wenn Produktion containerimages, z. B. Enterprise, Standard oder Web Edition ausgeführt werden soll. Es gibt jedoch einige Unterschiede, die im folgenden beschrieben werden.

- Sie können nur SQL Server in einer produktionsumgebung verwenden, wenn Sie eine gültige Lizenz verfügen. Sie erhalten eine kostenlose Lizenz für SQL Server Express Produktion [hier](https://go.microsoft.com/fwlink/?linkid=857693). Lizenzen für SQL Server Standard und Enterprise Edition stehen über [Microsoft Volume Licensing](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs.aspx).

- Produktion SQL Server-Container-Images müssen von abgerufen werden [Docker Store](https://store.docker.com). Wenn Sie einen noch nicht haben, erstellen Sie ein Konto im Docker-Speicher.

- Die Developer-Container-Abbild auf Docker-Speicher kann die Produktions-Editionen ausgeführt konfiguriert werden. Verwenden Sie die folgenden Schritte aus, um die Produktion-Editionen ausgeführt:

   1. Melden Sie sich zunächst auf die Docker-Id über die Befehlszeile.

```
      docker login
```

   1. Als Nächstes müssen Sie freien Entwickler containerimage in Docker-Informationsspeicher abzurufen. Wechseln Sie zu [https://store.docker.com/images/mssql-server-linux](https://store.docker.com/images/mssql-server-linux), klicken Sie auf **zur Kasse**, und befolgen Sie die Anweisungen.

   1. Überprüfen Sie die Anforderungen und führen Sie Prozeduren aus, in der [Schnellstart – Schnellstart-Installation herstellen docker.md). Es gibt jedoch zwei Unterschiede. Sie müssen das Image per Pull beziehen **Store/Microsoft/Mssql-Server – Linux:\<Tagname\>**  Docker Store. Außerdem müssen Sie angeben, die Produktion Edition mit der **MSSQL_PID** -Umgebungsvariablen angegeben. Im folgende Beispiel wird gezeigt, wie das neueste 2017 von SQL Server-Container-Bild für die Enterprise Edition ausgeführt wird:



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-encrypting-connections-to-sql-server-on-linuxsql-server-linux-encrypted-connectionsmd"></a>5. &nbsp;[Verschlüsseln von Verbindungen zu SQLServer on Linux](sql-server-linux-encrypted-connections.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_4) | [Weiter](#TitleNum_6))

<!-- Source markdown line 45.  ms.author= meetb;rickbyh.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7e3187866df060903e30000d60d673edad46d210 bcb1f2771e6c29b535a30b9f23ac296954509187  (PR=4150  ,  Filename=sql-server-linux-encrypted-connections.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



        sudo chown mssql:mssql mssql.pem mssql.key
        sudo chmod 600 mssql.pem mssql.key
        sudo mv mssql.pem /etc/ssl/certs/
        sudo mv mssql.key /etc/ssl/private/

- **Konfigurieren von SQLServer**

        systemctl stop mssql-server
        cat /var/opt/mssql/mssql.conf
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0

- **Registrieren des Zertifikats auf dem Clientcomputer (Windows, Linux oder MacOS)**

    -   Bei Verwendung von Zertifizierungsstelle signiertes Zertifikat müssen Sie das Zertifikat (Certificate Authority, CA), anstatt das Zertifikat auf den Clientcomputer kopiert.
    -   Wenn Sie das selbstsignierte Zertifikat nur verwenden, kopieren Sie die PEM-Datei in die folgenden Ordner je nach Verteilung, und führen Sie die Befehle aktivieren

        - **Windows**: importieren, die die PEM-Datei als ein Zertifikat unter "aktuelle Benutzer" -> vertrauenswürdiger Stammzertifizierungsstellen-Zertifikate >
        - **macOS**:

-   **Exemplarische Verbindungszeichenfolgen**

    - **..!NCLUDE-NotShown--ssmanstudiofull-md--../includes/ssmanstudiofull-md.md)]** ![SSMS connection dialog--media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS connection dialog")



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-create-and-run-sql-server-agent-jobs-on-linuxsql-server-linux-run-sql-server-agent-jobmd"></a>6. &nbsp;[Erstellen und Ausführen von SQL Server-Agentaufträge unter Linux](sql-server-linux-run-sql-server-agent-job.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_5) | [Weiter](#TitleNum_7))

<!-- Source markdown line 35.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1598129bb5f98434435d8ad02336a9adf76c7870 6fe3fe7df3a60dbac31f1df59aac9860d293421a  (PR=4150  ,  Filename=sql-server-linux-run-sql-server-agent-job.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



Die folgenden Voraussetzungen sind erforderlich, um dieses Lernprogramm abzuschließen:

* Linux-Computer mit den folgenden Voraussetzungen:
  * SQL Server-2017 ([RHEL--quickstart-install-connect-red-hat.md), [SLES – Schnellstart-Installation herstellen suse.md), oder [Ubuntu – Schnellstart-Installation herstellen ubuntu.md)) mit Befehlszeilentools.

Die folgenden erforderlichen Komponenten sind optional:

* Windows-Computer mit SSMS:
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) für optionale SSMS Schritte.

**Install SQL Server Agent (Installieren des SQL Server-Agents)**


Um SQL Server-Agent für Linux verwenden, installieren Sie zuerst die **Mssql-Server-Agent** Paket auf einem Computer, die bereits von SQL Server-2017 installiert.

1. Installieren Sie **Mssql-Server-Agent** mit den entsprechenden Befehl für Ihr Betriebssystem Linux.

   | Platform | Installation Befehle |
   |-----|-----|
   | RHEL | `sudo yum install mssql-server-agent` |
   | SLES | `sudo zypper refresh`<br/>`sudo zypper update mssql-server-agent` |
   | Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server-agent` |

1. Starten Sie SQL Server mit dem folgenden Befehl ein:

```
   sudo systemctl restart mssql-server
```

**Erstellen einer Beispieldatenbank**


Verwenden Sie die folgenden Schritte zum Erstellen einer Beispieldatenbank mit dem Namen **SampleDB**. Diese Datenbank ist für den täglichen Sicherungsauftrag verwendet.

1. Öffnen Sie eine terminal Bash-Sitzung, auf dem Linux-Computer.



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7. &nbsp;[-Installationsleitfaden für SQL Server on Linux](sql-server-linux-setup.md)

*Aktualisiert: 2017-12-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_6) | [Weiter](#TitleNum_8))

<!-- Source markdown line 125.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880 eedddcfb64c6432215f56b74dc91700d9804fce8  (PR=4160  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=085dd05d56afecbb454206ed8402cfbaa597cfbe) -->



**<a id="repositories"></a>Konfigurieren von quellrepositorys**


Beim Installieren oder Aktualisieren von SQL Server, erhalten Sie die neueste Version von SQL Server von Ihrem konfigurierten Microsoft-Repository.

**Repository-Optionen**


Es gibt zwei Haupttypen von Repositorys für jede Verteilung ein:

- **Kumulative Updates (CU)**: das kumulative Update (CU)-Repository enthält Pakete für die grundlegenden SQL Server-Version sowie alle Programmfehlerbehebungen und Verbesserungen seit diesem Release. Kumulative Updates sind spezifisch für die endgültige Produktversion, z. B. SQL Server-2017. Sie werden in einem regulären Rhythmus veröffentlicht.

- **GDR**: die GDR-Repository enthält Pakete für die grundlegenden SQL Server-Version und nur kritische Updates und Sicherheitsupdates seit diesem Release. Diese Updates werden auch auf die nächste CU-Version hinzugefügt.

Jeder CU und GDR-Version enthält die vollständige SQL Server-Paket und alle vorherigen Updates für das Repository. Aktualisieren von einer GDR-Version für eine CU-Version wird durch Ändern des konfigurierten Repositorys für SQL Server unterstützt. Sie können auch [downgrade--#rollback) auf eine beliebige Version innerhalb der Hauptversion (ex: 2017). Aktualisieren von ein CU-Version mit einer GDR-Version wird nicht unterstützt.

**Überprüfen Sie die konfigurierte repository**


Wenn Sie möchten überprüfen, welche Repository konfiguriert ist, verwenden Sie die folgenden plattformabhängige Techniken.

| Platform | Verfahren |
|-----|-----|
| RHEL | 1. Zeigen Sie die Dateien in den **/etc/yum.repos.d** Verzeichnis:`sudo ls /etc/yum.repos.d`<br/>2. Suchen Sie nach einer Datei, die das SQL Server-Verzeichnis, wie z. B. konfiguriert **Mssql-server.repo**.<br/>3. Drucken Sie den Inhalt der Datei ein:`sudo cat /etc/yum.repos.d/mssql-server.repo`<br/>4. Die **Namen** Eigenschaft ist für die konfigurierten Repository.|
| SLES | 1. Führen Sie den folgenden Befehl ein:`sudo zypper info mssql-server`<br/>2. Die **Repository** Eigenschaft ist für die konfigurierten Repository. |
| Ubuntu | 1. Führen Sie den folgenden Befehl ein:`sudo cat /etc/apt/sources.list`<br/>2. Überprüfen Sie die Paket-URL für Mssql-Server. |



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-configure-failover-cluster-instance---sql-server-on-linux-rhelsql-server-linux-shared-disk-cluster-configuremd"></a>8. &nbsp;[Konfigurieren Failoverclusterinstanz – SQL Server für Linux (RHEL)](sql-server-linux-shared-disk-cluster-configure.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_7) | [Weiter](#TitleNum_9))

<!-- Source markdown line 25.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 308fa1809c80a009f7f15b5ca6917f6b76588c3e 71f18baa320041ff10c94e8c7668e40dff45cac3  (PR=4150  ,  Filename=sql-server-linux-shared-disk-cluster-configure.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



> [!div class="checklist"]
> * Einrichten und Konfigurieren von Linux
> * Installieren und Konfigurieren von SQL Server
> * Konfigurieren Sie die Hosts-Datei
> * Konfigurieren von freigegebenen Speicher und Verschieben von Datenbankdateien
> * Installieren Sie und konfigurieren Sie auf jedem Clusterknoten Schrittmacher
> * Konfigurieren der Failoverclusterinstanz

In diesem Artikel erläutert, wie eine zwei-Knoten freigegebenen Datenträger-Failoverclusterinstanz (FCI) für SQL Server zu erstellen. Der Artikel enthält Anweisungen und Beispiele für Skripts für Red Hat Enterprise Linux (RHEL). Ubuntu-Distributionen sind ähnlich RHEL, damit Skriptbeispiele normalerweise werden auch auf Ubuntu arbeiten.

Konzeptionelle Informationen finden Sie unter [SQL Server Failoverclusterinstanz (FCI) auf Linux--sql-server-linux-shared-disk-cluster-concepts.md).

**Erforderliche Komponenten**


Zum Abschließen der End-to-End-Szenarios unten benötigen Sie zwei Computer, der zwei Knoten-Cluster und einem anderen Server für den Speicher bereitstellen. Unten aufgeführten Schritten dargestellt, wie diesen Servern konfiguriert werden kann.

**Einrichten und Konfigurieren von Linux**


Der erste Schritt ist so konfigurieren Sie das Betriebssystem auf den Clusterknoten. Konfigurieren Sie eine Linux-Distribution, auf den einzelnen Knoten im Cluster. Verwenden Sie den Verteilungspunkt und die Version auf beiden Knoten ein. Verwenden Sie eine oder das andere der folgenden Verteilungen:

* RHEL mit einem gültigen Abonnement für das Add-on für hohe Verfügbarkeit

**Installieren und Konfigurieren von SQL Server**


1. Installieren und Einrichten von SQL Server auf beiden Knoten.  Ausführliche Anweisungen finden Sie unter [Installieren von SQL Server on Linux – Sql-Server-Linux-setup.md).
1. Festlegen Sie ein Knoten als primärer und der andere als sekundärer, zum Zweck der Konfiguration. Verwenden Sie diese Begriffe für die folgenden dieses Handbuchs.
1. Beenden und Deaktivieren von SQL Server, auf dem sekundären Knoten.
    Im folgenden Beispiel wird beendet und deaktiviert SQL Server:
```
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
```

    > [!NOTE]
    > At set up time, a Server Master Key is generated for the SQL Server instance and placed at `var/opt/mssql/secrets/machine-key`. On Linux, SQL Server always runs as a local account called mssql. Because it's a local account, its identity isn't shared across nodes. Therefore, you need to copy the encryption key from primary node to each secondary node so each local mssql account can access it to decrypt the Server Master Key.



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-troubleshoot-sql-server-on-linuxsql-server-linux-troubleshooting-guidemd"></a>9. &nbsp;[Problembehandlung bei SQLServer on Linux](sql-server-linux-troubleshooting-guide.md)

*Aktualisiert: 30.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_8))

<!-- Source markdown line 125.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5f8557a34b38e028ff6e5ac370b6d2d6bf315091 196e56187b57bdd79cc5cdc5e6fce3d41e82af0c  (PR=4150  ,  Filename=sql-server-linux-troubleshooting-guide.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



**Starten Sie SQLServer in der Minimalkonfiguration oder im Einzelbenutzermodus**


**Starten Sie SQLServer im Modus der Minimalkonfiguration**

Dies ist hilfreich, wenn der Server aufgrund der Einstellung eines Konfigurationswerts (z. B. aufgrund von Arbeitsspeichermangel) nicht gestartet werden kann.

```
   sudo -u mssql /opt/mssql/bin/sqlservr -f
```

**Starten Sie SQLServer im Einzelbenutzermodus**

Unter bestimmten Umständen müssen Sie möglicherweise eine Instanz von SQL Server im Einzelbenutzermodus starten, mithilfe der Startoption-m. Dies ist z. B. der Fall, wenn Sie Serverkonfigurationsoptionen ändern oder eine beschädigte master-Datenbank oder andere Systemdatenbanken wiederherstellen möchten. Beispielsweise sollten Sie Serverkonfigurationsoptionen ändern oder eine beschädigte master-Datenbank oder andere Systemdatenbanken wiederherstellen

Starten Sie SQLServer im Einzelbenutzermodus
```
   sudo -u mssql /opt/mssql/bin/sqlservr -m
```

Starten Sie SQLServer im Einzelbenutzermodus mit SQLCMD
```
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
```

> [!WARNING]
>  Starten Sie SQL Server unter Linux mit dem Benutzer „MSSQL“, um zukünftige Startprobleme zu vermeiden. Beispiel „sudo-u mssql /opt/mssql/bin/sqlservr [STARTOPTIONEN]“

Wenn Sie versehentlich SQL Server mit einem anderen Benutzer gestartet haben, müssen Sie den Besitz von SQL Server-Datenbankdateien zurück an den Benutzer "Mssql" vor dem Starten von SQL Server mit Systemd zu ändern. Angenommen, um den Besitz aller Datenbankdateien unter /var/opt/mssql für den Benutzer "Mssql" zu ändern, führen Sie den folgenden Befehl

```
   chown -R mssql:mssql /var/opt/mssql/
```







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Die neue oder kürzlich aktualisierten Artikel haben Themenbereiche

- [Neu + Aktualisiert (3+14): Dokumente zu **Advanced Analytics für SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (1 + 0): **Analysis Services für SQL** Docs](../analysis-services/new-updated-analysis-services.md)
- [Neu + Aktualisiert (87+0): Dokumente zu **Analyseplattformsystem für SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neu + Aktualisiert (5+4): Dokumente zu **Herstellen einer Verbindung mit SQL**](../connect/new-updated-connect.md)
- [Neu + Aktualisiert (0+1): Dokumente zum **Datenbankmodul für SQL**](../database-engine/new-updated-database-engine.md)
- [Neu + Aktualisiert (2+2):Dokumente zu **Integration Services für SQL**](../integration-services/new-updated-integration-services.md)
- [Neu + Aktualisiert (10+9): Dokumente zu **Linux für SQL**](../linux/new-updated-linux.md)
- [Neu + Aktualisiert (2+4): Dokumente zu **Relationale Datenbanken für SQL**](../relational-databases/new-updated-relational-databases.md)
- [Neu + Aktualisiert (4+2): Dokumente zu **Reporting Services für SQL**](../reporting-services/new-updated-reporting-services.md)
- [Neu + Aktualisiert (0+1): Dokumente zu **Beispiele für SQL**](../sample/new-updated-sample.md)
- [Neu + Aktualisiert (21+0): Dokumente zu **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neu + Aktualisiert (5+1): Dokumente zu **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (0 + 1): **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neu + Aktualisiert (1+0): Dokumente zu **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Neue und aktualisierte (0 + 1): **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neu + Aktualisiert (0+2): Dokumente zu **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die keine Artikel neu oder vor kurzem aktualisiert haben.

- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [Neue und aktualisierte (0 + 0): **ActiveX Data Objects (ADO) für SQL** Docs](../ado/new-updated-ado.md)
- [Neue und aktualisierte (0 + 0): **Data Quality Services für SQL** Docs](../data-quality-services/new-updated-data-quality-services.md)
- [Neue und aktualisierte (0 + 0): **Data Mining Extensions (DMX) für SQL** Docs](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [Neue und aktualisierte (0 + 0): **MDX (Multidimensional Expressions) für SQL** Docs](../mdx/new-updated-mdx.md)
- [Neue und aktualisierte (0 + 0): **ODBC (Open Database Connectivity) für SQL** Docs](../odbc/new-updated-odbc.md)
- [Neue und aktualisierte (0 + 0): **PowerShell für SQL** Docs](../powershell/new-updated-powershell.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [Neue und aktualisierte (0 + 0): **XQuery für SQL** Docs](../xquery/new-updated-xquery.md)


