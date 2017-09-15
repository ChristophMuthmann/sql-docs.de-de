---
title: "Aktualisiert – SQL Server on Linux Docs | Microsoft Docs"
description: "Aktualisierter Inhalt in zuletzt geänderten Dokumentation für Microsoft SQL Server on Linux Codeausschnitte anzeigen"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 9e6b139e45ccb5184255eabedfb0f809ff64fd2b
ms.contentlocale: de-de
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Neue und zuletzt aktualisiert: SQL Server on Linux Docs



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-07-18** &nbsp; - zu - &nbsp; **2017-09-11**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Microsoft SQL Server on Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links führen zu neue Artikel, die vor kurzem hinzugefügt wurden.


1. [DB-E-Mails und e-Mail-Benachrichtigungen mit SQL-Agent für Linux](sql-server-linux-db-mail-sql-agent.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

Dieser Abschnitt zeigt die Auszüge von Updates, die vom Artikel, die vor kurzem eine große Aktualisierung aufgetreten sind.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese compact Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Betreiben Sie HA-verfügbarkeitsgruppe für SQL Server on Linux](#TitleNum_1)
2. [Konfigurieren von SQL Server-2017 Container Bilder auf Docker](#TitleNum_2)
3. [Konfigurieren von SQL Server unter Linux mit dem Mssql-Conf-tool](#TitleNum_3)
4. [Feedback von Kunden für SQLServer on Linux](#TitleNum_4)
5. [Migration von einer SQL Server-Datenbank von Windows, Linux mit Sicherung und Wiederherstellung](#TitleNum_5)
6. [Versionshinweise für SQL Server-2017 unter Linux](#TitleNum_6)
7. [-Installationsleitfaden für SQL Server on Linux](#TitleNum_7)
8. [Installieren von SQL Server Integration Services (SSIS) unter Linux](#TitleNum_8)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-operate-ha-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-failover-hamd"></a>1. &nbsp;[Ausgeführt werden virtuelle Maschinen mit hoher Verfügbarkeit-Gruppe für SQL Server on Linux](sql-server-linux-availability-group-failover-ha.md)

*Aktualisiert: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 167.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1bef3ece125721b041aa2b9d836329736377df8d 669d2b9a614d680b98280d5b522ba82cf466536c  (PR=2948  ,  Filename=sql-server-linux-availability-group-failover-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



**Aktualisieren der verfügbarkeitsgruppe.**


Überprüfen Sie die bewährten Methoden an [Upgrade Availability Group Replikat Instanzen--.., vor dem upgrade von einer verfügbarkeitsgruppe / database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

In den folgenden Abschnitten wird erläutert, wie ein paralleles Upgrade mit SQL Server-Instanzen unter Linux mit Verfügbarkeitsgruppen ausführen.

**Aktualisieren Sie die Schritte unter Linux**


Wenn Replikate der verfügbarkeitsgruppe für Instanzen von SQL Server unter Linux sind, ist der Clustertyp der verfügbarkeitsgruppe entweder `EXTERNAL` oder `NONE`. Eine verfügbarkeitsgruppe, die von einem Cluster-Manager verwaltet wird, neben Windows Server-Failovercluster (WSFC ist) `EXTERNAL`. Schrittmacher mit Corosync ist ein Beispiel für einen externen Cluster-Manager. Eine verfügbarkeitsgruppe mit keine Cluster-Manager verfügt Clustertyp `NONE` die Aktualisierung hier beschriebenen Schritte sind spezifisch für Verfügbarkeitsgruppen von Clustertyp `EXTERNAL` oder `NONE`.

1. Bevor Sie beginnen, Sichern Sie jede Datenbank.
2. Aktualisieren von SQL Server-Instanzen, sekundäre Replikate gehostet.

    a. Aktualisieren Sie zuerst die asynchronen sekundären Replikate.

    b. Aktualisieren Sie die synchrone sekundäre Replikate.

   >[!NOTE]
   >Wenn eine verfügbarkeitsgruppe nur asynchrone verfügt wird Replikate - um Datenverluste zu vermeiden. ändern ein Replikat, synchrone und warten, bis er synchronisiert wird. Aktualisieren Sie dann dieses Replikat aus.

   b. 1. Beenden Sie die Ressource auf dem Knoten, der das sekundäre Replikat als Ziel für Upgrade hostet

   Beenden Sie vor dem Ausführen von Upgrade-Befehls, die Ressource, damit der Cluster nicht werden überwacht und sie unnötig fehl. Im folgenden Beispiel wird eine standorteinschränkung für den Knoten, der sich ergeben, wird für die Ressource beendet werden soll. Update `ag_cluster-master` mit dem Ressourcennamen und `nodeName1` mit dem Knoten, der das Ziel für das Upgrade Replikat hostet.

```
   pcs constraint location ag_cluster-master avoids nodeName1
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>2. &nbsp;[Konfigurieren von SQL Server-2017 Container Bilder auf Docker](sql-server-linux-configure-docker.md)

*Aktualisiert: 2017-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 257.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0239ed55a23721eedcc0407a0886d08da47c975b 108fe230151cff7dc91fcdc22218f232394746ec  (PR=3050  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=60272ce672c0a32738b0084ea86f8907ec7fc0a5) -->



1. Identifizieren Sie die Docker **Tag** für die Version, die Sie verwenden möchten. Um die verfügbaren Tags anzuzeigen, finden Sie unter [der Mssql-Server-Linux-Docker Hub-Seite](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Ziehen Sie das SQL Server-Container-Bild mit dem Tag. Um das Bild RC1 per Pull abzurufen, ersetzen Sie z. B. `<image_tag>` in den folgenden Befehl mit `rc1`.

```
   docker pull microsoft/mssql-server-linux:<image_tag>
```

1. Um einen neuen Container mit dem sich das Bild auszuführen, geben Sie den Tagnamen in der `docker run` Befehl. Ersetzen Sie in den folgenden Befehl `<image_tag>` mit der Version, die Sie ausführen möchten.

```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

Diese Schritte können auch einen vorhandenen Container herabgestuft werden, verwendet werden. Sie können z. B. zurücksetzen möchten oder downgrade einen aktiven Container für die Problembehandlung oder testen. Um einen aktiven Container ein Downgrade auszuführen, müssen Sie eine Technik für die Persistenz für den Datenordner verwenden. Befolgen Sie die gleichen Schritte der [upgrade Abschnitt--#upgrade), aber der Tagname der älteren Version angeben, wenn Sie den neuen Container ausführen.

> [!IMPORTANT]



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-configure-sql-server-on-linux-with-the-mssql-conf-toolsql-server-linux-configure-mssql-confmd"></a>3. &nbsp;[Konfigurieren Sie SQL Server unter Linux mit dem Mssql-Conf-Tool](sql-server-linux-configure-mssql-conf.md)

*Aktualisiert: 2017-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_2) | [Weiter](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= lbosq.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6117f03e9617b70077488d86f94b32537c4cb9e8 4247a749c056037dd71a27121525be04be6a4f21  (PR=3042  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=46b16dcf147dbd863eec0330e87511b4ced6c4ce) -->



**<a id="localaudit"></a>Die lokale Überwachung Verzeichnis festlegen**


Die **telemetry.userrequestedlocalauditdirectory** Einstellung ermöglicht das lokale Überwachung und ermöglicht Ihnen das Verzeichnis festlegen, in dem die lokale Überwachung protokolliert werden erstellt.

1. Erstellen Sie ein Zielverzeichnis für neue lokale Überwachungsprotokolle ein. Das folgende Beispiel erstellt ein neues **/Tmp/Audit** Verzeichnis:

```
   sudo mkdir /tmp/audit
```

1. Ändern Sie den Besitzer und die Gruppe des Verzeichnisses, das die **Mssql** Benutzer:

```
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
```

1. Führen Sie das Skript Mssql-Conf als Root mit der **festgelegt** -Befehl für **telemetry.userrequestedlocalauditdirectory**:

```
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
```

1. Starten Sie SQL Server-Dienst neu:

```
   sudo systemctl restart mssql-server
```

Weitere Informationen finden Sie unter [Kundenfeedback für SQL Server auf Linux--sql-server-linux-customer-feedback.md).

**<a id="lcid"></a>Ändern Sie das SQL Server-Gebietsschema**


Die **language.lcid** ändert sich das SQL Server-Gebietsschema auf alle unterstützten Sprachen-ID (LCID) festlegen.

1. Im folgende Beispiel ändert das Gebietsschema auf Französisch (1036):

```
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
```

1. Starten Sie den SQL Server-Dienst, um die Änderungen zu übernehmen:

```
   sudo systemctl restart mssql-server
```

**<a id="memorylimit"></a>Das Arbeitsspeicherlimit festgelegt**


Die **memory.memorylimitmb** Steuerelemente Größe des physischen Arbeitsspeichers (in MB) verfügbar auf SQL Server festlegen. Der Standardwert ist 80 % des physischen Arbeitsspeichers.

1. Führen Sie das Skript Mssql-Conf als Root mit der **festgelegt** -Befehl für **memory.memorylimitmb**. Im folgenden Beispiel wird den verfügbare Speicher mit SQL Server zum 3,25 GB (3328 MB) an.

```
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
```

1. Starten Sie den SQL Server-Dienst, um die Änderungen zu übernehmen:



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-customer-feedback-for-sql-server-on-linuxsql-server-linux-customer-feedbackmd"></a>4. &nbsp;[Feedback von Kunden für SQLServer on Linux](sql-server-linux-customer-feedback.md)

*Aktualisiert: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_3) | [Weiter](#TitleNum_5))

<!-- Source markdown line 104.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9d8122e864804004d91f6b7c5c3d24c4a4114d34 7316ef831c390a854c324f23a02c3fb6005e2fea  (PR=2948  ,  Filename=sql-server-linux-customer-feedback.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->




**Für Docker**

Zum Aktivieren der lokalen Überwachung auf Docker benötigen Sie Docker [behalten Ihre Data--sql-server-linux-configure-docker.md).

1. Das Zielverzeichnis für neue lokale Überwachungsprotokolle werden im Container. Erstellen Sie ein Zielverzeichnis für neue lokale Überwachungsprotokolle im Hostverzeichnis auf Ihrem Computer. Das folgende Beispiel erstellt ein neues **/audit** Verzeichnis:

```
   sudo mkdir <host directory>/audit
```


1. Hinzufügen einer `mssql.conf` Datei mit den Zeilen `[telemetry]` und `userrequestedlocalauditdirectory = <host directory>/audit` im Hostverzeichnis:

```
   echo '[telemetry]' >> <host directory>/mssql.conf
```

```
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
```
2. Führen Sie das Container-Bild
```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

**Nächste Schritte**





&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restoresql-server-linux-migrate-restore-databasemd"></a>5. &nbsp;[Migration eine SQL Server-Datenbank von Windows, Linux mit Sicherung und Wiederherstellung](sql-server-linux-migrate-restore-database.md)

*Aktualisiert: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_4) | [Weiter](#TitleNum_6))

<!-- Source markdown line 30.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e78f5516a46eab834f644979d3e1c0ca415fabcd 6b03a01385078290b9f451ac013b628f53e0e8b4  (PR=2948  ,  Filename=sql-server-linux-migrate-restore-database.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



* Windows-Computer mit den folgenden:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) installiert.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) installiert.
  * Die Zieldatenbank zu migrieren.

* Linux-Computer mit Folgendes installiert:
  * SQL Server 2017 RC2. Finden Sie unter der Schnellstarts Installation für [RHEL--quickstart-install-connect-red-hat.md) [SLES – Schnellstart-Installation herstellen suse.md), oder [Ubuntu – Schnellstart-Installation herstellen ubuntu.md).
  * SQL Server 2017 RC2 [Befehlszeilen Tools--sql-server-linux-setup-tools.md).

**Erstellen Sie eine Sicherung in Windows**


Es gibt mehrere Möglichkeiten, erstellen eine Sicherungsdatei mit einer Datenbank auf Windows aus. Verwenden Sie SQL Server Management Studio (SSMS) die folgenden Schritte aus.

1. Starten Sie **SQL Server Management Studio** auf dem Windows-Computer.

1. Geben Sie im Verbindungsdialogfeld **"localhost"**.

1. Erweitern Sie im Objekt-Explorer **Datenbanken**.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>6. &nbsp;[Versionshinweise für SQL Server-2017 unter Linux](sql-server-linux-release-notes.md)

*Aktualisiert: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_5) | [Weiter](#TitleNum_7))

<!-- Source markdown line 31.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4c8b9876f4792782314ba2f9b246405fb8036f84 acb97cf0a2e0bdd039575eaab9c41003316cbb02  (PR=2939  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



**<a id="RC2"></a>RC2 (August 2017)**


Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.900.75.

**Unterstützte Plattformen**


| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installation Guide--quickstart-install-connect-red-hat.md) |
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Installationshandbuch – Schnellstart-Installation herstellen suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Installationshandbuch – Schnellstart-Installation herstellen ubuntu.md) |
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch – Schnellstart-Installation herstellen docker.md) |

> [!NOTE]
> Sie benötigen mindestens 3,25 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
> SQL Server-Datenbankmodul wurde bis zu 1,5 TB Arbeitsspeicher zu diesem Zeitpunkt getestet.

**Details zum Paket**


Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Beachten Sie, dass Sie nicht benötigen, um diese Pakete direkt herunterzuladen, wenn Sie die Schritte in den folgenden Handbüchern zur Installation verwenden:

- [Installieren Sie SQL Server-Paket – Sql-Server-Linux-setup.md)
- [Installieren Sie Volltextsuche Package--sql-server-linux-setup-full-text-search.md)
- [Installieren Sie SQL Server-Agent package--sql-server-linux-setup-sql-agent.md)

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.900.75-1 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) |



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7. &nbsp;[-Installationsleitfaden für SQL Server on Linux](sql-server-linux-setup.md)

*Aktualisiert: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_6) | [Weiter](#TitleNum_8))

<!-- Source markdown line 70.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00394e1733568a55243788d828968ff9b58a3c99 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880  (PR=2971  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=303d3b74da3fe370d19b7602c0e11e67b63191e7) -->



**<a id="rollback"></a>Rollback SQLServer**


Verwenden Sie Rollback oder Downgrade für die SQL Server auf einer früheren Version die folgenden Schritte aus:

1. Identifizieren Sie die Versionsnummer für das SQL Server-Paket beim downgrade auf den gewünschten. Eine Liste der Paket-Zahlen finden Sie unter [Version Notes--sql-server-linux-release-notes.md.)

1. Ein Downgrade auf eine frühere Version von SQL Server. Ersetzen Sie in den folgenden Befehlen `<version_number>` mit der SQL Server-Versionsnummer, die Sie in Schritt 1 identifiziert.

   | Platform | Paket-Update-Befehle |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> Es wird nur unterstützt, um ein Downgrade auf eine Version, innerhalb der gleichen Hauptversion, z. B. SQL Server-2017 auszuführen.

> [!IMPORTANT]
> Downgrade für die wird zu diesem Zeitpunkt nur zwischen RC2 und RC1 unterstützt.




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-install-sql-server-integration-services-ssis-on-linuxsql-server-linux-setup-ssismd"></a>8. &nbsp;[Installieren von SQL Server Integration Services (SSIS) unter Linux](sql-server-linux-setup-ssis.md)

*Aktualisiert: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_7))

<!-- Source markdown line 66.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a3fecd2553d1b25406445b8a26b22c9015dd98fe f836d560513fef1217e7dbce0ab85f78eec6f937  (PR=2948  ,  Filename=sql-server-linux-setup-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



Falls Sie noch `mssql-server-is` installiert haben, können Sie auf die neueste Version mit dem folgenden Befehl aktualisieren:

```
sudo apt-get install mssql-server-is
```


So entfernen Sie `mssql-server-is`, können Sie folgenden Befehl ausführen:
```
sudo apt-get remove msssql-server-is
```



**<a name="RHEL"></a>Installieren Sie SSIS auf RHEL**

So installieren Sie die `mssql-server-is` Paket auf RHEL, gehen Sie folgendermaßen vor:


1.  Geben Sie ein Superuser-Modus.

```
    sudo su
```


2.  Herunterladen der Konfigurationsdatei für Microsoft SQL Server-Red Hat-Repository.

```
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
```


3.  Exit-Superuser-Modus.

```
    exit
```


4.  Führen Sie die folgenden Befehle zum Installieren von SQL Server Integration Services.

```
    sudo yum install -y mssql-server-is
```


5.  Führen Sie nach der Installation `ssis-conf`.







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Dieser Abschnitt enthält sehr ähnlich Artikel für die zuletzt aktualisierten Artikel in anderen Bereichen in unserer öffentlichen Repositorys für "github.com" Betreff: [MicrosoftDocs/Sql-Docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [Neue und aktualisierte (3 + 12): **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (5 + 0): **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [Neue und aktualisierte (5 + 1): **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (19 + 82): **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (1 + 8): **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (12 + 1): **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (0 + 1): **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (7 + 1): **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (1 + 1): **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neue und aktualisierte (0 + 2): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neue und aktualisierte (1 + 4): **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (4 + 1): **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)
- [Neue und aktualisierte (0 + 1): **-Tools für SQL** Docs](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [Neue und aktualisierte (0 + 0): **Analysis Services für SQL** Docs](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [Neue und aktualisierte (0 + 0): **Master Data Services (MDS) für SQL** Docs](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)



