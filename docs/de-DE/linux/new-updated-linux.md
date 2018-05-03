---
title: Aktualisiert – SQL Server on Linux Docs | Microsoft Docs
description: Aktualisierter Inhalt in zuletzt geänderten Dokumentation für Microsoft SQL Server on Linux Codeausschnitte anzeigen
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: linux
ms.date: 04/28/2018
ms.openlocfilehash: adc9b9d4dec86f1b0e8807869aa0f20532837cea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Neue und zuletzt aktualisiert: SQL Server on Linux Docs



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2018-02-03** &nbsp; - zu - &nbsp; **2018-04-28**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Microsoft SQL Server on Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Active Directory-Authentifizierung für SQL Server on Linux](sql-server-linux-active-directory-auth-overview.md)
2. [Configure SQL Server AlwaysOn-Verfügbarkeitsgruppe unter Windows und Linux (Cross-Platform)](sql-server-linux-availability-group-cross-platform.md)
3. [Betreiben Sie Always On-Verfügbarkeitsgruppen unter Linux](sql-server-linux-availability-group-operate-ha.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Konfigurieren des Repositorys für die Installation und Upgrade von SQL Server on Linux](#TitleNum_1)
2. [Konfigurieren von SQL Server unter Linux mit dem Mssql-Conf-tool](#TitleNum_2)
3. [Versionshinweise für SQL Server-2017 unter Linux](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-repositories-for-installing-and-upgrading-sql-server-on-linuxsql-server-linux-change-repomd"></a>1. &nbsp; [Konfigurieren des Repositorys für die Installation und Upgrade von SQL Server on Linux](sql-server-linux-change-repo.md)

*Aktualisiert: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 72.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5ccaa0fcb8895f25c162e4e0494ad4872773de3 29a959be6ee7d58fe0c53e8f91bdd282fb2e6d29  (PR=5676  ,  Filename=sql-server-linux-change-repo.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- Druckt den Inhalt der Datei.

```
   sudo cat /etc/yum.repos.d/mssql-server.repo
```

- Die **Namen** Eigenschaft ist für die konfigurierten Repository. Sie können mit der Tabelle im Abschnitt [Repositorys] identifiziert werden.

**Entfernen Sie alte Repository (RHEL)**

Entfernen Sie ggf. das alte Repository mit dem folgenden Befehl.

```
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

Mit diesem Befehl wird davon ausgegangen, dass die Datei identifiziert, die im vorherigen Abschnitt benannt wurde **Mssql-server.repo**.

**Konfigurieren Sie neue Repository (RHEL)**

Konfigurieren Sie das neue Repository für SQL Server-Installationen und Upgrades verwenden. Verwenden Sie einen der folgenden Befehle aus, um das Repository Ihrer Wahl zu konfigurieren.

| Repository | Befehl |
|---|---|
| **CU** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

**<a id="sles"></a> SLES Repositorys konfigurieren**

Verwenden Sie die folgenden Schritte aus, um auf SLES Repositorys konfigurieren.

**Überprüfen Sie zuvor konfigurierten Repositorys (SLES)**

Überprüfen Sie zunächst, ob Sie bereits ein SQL Server-Repository registriert haben.

- Verwendung **Zypper Info** um Informationen über alle zuvor konfigurierten Repository abzurufen.

```
   sudo zypper info mssql-server
```

- Die **Repository** Eigenschaft ist für die konfigurierten Repository. Sie können mit der Tabelle im Abschnitt [Repositorys] identifiziert werden.

**Entfernen Sie alte Repository (SLES)**

Entfernen Sie ggf. das alte Repository. Verwenden Sie die folgenden Befehle, die basierend auf den zuvor konfigurierten Repository-Typ.

| Repository | Befehl zum Entfernen |
|---|---|
| **Vorschau** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-sql-server-on-linux-with-the-mssql-conf-toolsql-server-linux-configure-mssql-confmd"></a>2. &nbsp; [Konfigurieren von SQL Server unter Linux mit dem Mssql-Conf-tool](sql-server-linux-configure-mssql-conf.md)

*Aktualisiert: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 151.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3664c4d64ea4840dcbc718461ed04403cc486f30 89f708af45ce262057e967e9047f1328e19248ba  (PR=5676  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->




**<a id="masterdatabasedir"></a> Ändern Sie das Standard-master-Datenbank-Dateiverzeichnis**


Die **filelocation.masterdatafile** und **filelocation.masterlogfile** Einstellung ändert sich den Speicherort, in dem die SQL Server-Datenbankmodul, für die master-Datenbank-Dateien sucht. Dieser Speicherort ist standardmäßig /var/opt/mssql/data.

Um diese Einstellungen zu ändern, verwenden Sie die folgenden Schritte aus:

- Erstellen Sie das Zielverzeichnis für neue Fehlerprotokolldateien. Das folgende Beispiel erstellt ein neues **/Tmp/Masterdatabasedir** Verzeichnis:

```
   sudo mkdir /tmp/masterdatabasedir
```

- Ändern Sie den Besitzer und die Gruppe des Verzeichnisses, das die **Mssql** Benutzer:

```
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
```

- Verwenden der Mssql-Conf so ändern Sie das Standardverzeichnis für die master-Datenbank für die master Daten und Protokolldateien mit den **festgelegt** Befehl:

```
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
```

- Beenden Sie den SQL Server-Dienst:

```
   sudo systemctl stop mssql-server
```

- Verschieben Sie die Dateien master.mdf und masterlog.ldf:

```
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
```

- Starten Sie den SQL Server-Dienst:

```
   sudo systemctl start mssql-server
```

> [!NOTE]
> Wenn SQL Server im angegebenen Verzeichnis die Dateien master.mdf und mastlog.ldf finden kann, eine Kopie vorlagenbasierte Systemdatenbanken werden automatisch im angegebenen Verzeichnis erstellt, und SQL Server wird erfolgreich gestartet. Metadaten wie etwa von Benutzerdatenbanken, Server-Anmeldungen, Serverzertifikate, Verschlüsselungsschlüssel, SQL Agent-Aufträge oder Kennwort für SA-Anmeldung wird jedoch nicht in die neue master-Datenbank aktualisiert werden. Sie müssen zum Beenden von SQL Server und verschieben Ihre alte Dateien master.mdf und mastlog.ldf an den neuen angegebenen Speicherort aus, und starten Sie SQL Server, um den Vorgang fortzusetzen, verwenden die vorhandene Metadaten.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>3. &nbsp; [Versionshinweise für SQL Server-2017 unter Linux](sql-server-linux-release-notes.md)

*Aktualisiert: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_2))

<!-- Source markdown line 64.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 367d112a9427bbdd18e0e52cc82264dd169c91ae 63a67be08fa39ece778cf9ca0b9746dd28694574  (PR=5676  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- [Aktivieren Sie SQL Server-Agent]

**<a id="CU6"></a> CU6 (April 2018)**


Dies ist der kumulativen Update 6 (CU6)-Version von SQL Server-2017. Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.3025.34. Informationen zu den Korrekturen und Verbesserungen in dieser Version finden Sie unter [ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464).

**Details zum Paket**


Für Paketinstallationen der manuellen oder offline-können Sie die RPM und Debian Pakete mit den Informationen in der folgenden Tabelle herunterladen:

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.3025.34-3 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) |
| SLES RPM-Paket | 14.0.3025.34-3 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) |
| Ubuntu 16.04 Debian-Paket | 14.0.3025.34-3 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |







## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die *über* neue oder kürzlich aktualisierte Artikel verfügen

- [Neue und aktualisierte (11 + 6): &nbsp; &nbsp; **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (18 + 0): &nbsp; &nbsp; **Analysis Services für SQL** Docs](../analysis-services/new-updated-analysis-services.md)
- [Neue und aktualisierte (218 + 14): **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [Neue und aktualisierte (14 + 0): &nbsp; &nbsp; **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (3 + 2): &nbsp; &nbsp; **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (3 + 3): &nbsp; &nbsp; **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (7 + 10): &nbsp; &nbsp; **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (0 + 2): &nbsp; &nbsp; **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (1 + 3): &nbsp; &nbsp; **SQL Operations Studio** Docs](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neue und aktualisierte (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neue und aktualisierte (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (0 + 2): &nbsp; &nbsp; **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)
- [Neue und aktualisierte (1 + 1): &nbsp; &nbsp; **-Tools für SQL** Docs](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Themenbereiche, die *nicht* über neue oder kürzlich aktualisierte Artikel verfügen

- [Neue und aktualisierte (0 + 0): **Analyseplattformsystem für SQL** Docs](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neue und aktualisierte (0 + 0): **Data Quality Services für SQL** Docs](../data-quality-services/new-updated-data-quality-services.md)
- [Neue und aktualisierte (0 + 0): **Data Mining Extensions (DMX) für SQL** Docs](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [Neue und aktualisierte (0 + 0): **MDX (Multidimensional Expressions) für SQL** Docs](../mdx/new-updated-mdx.md)
- [Neue und aktualisierte (0 + 0): **ODBC (Open Database Connectivity) für SQL** Docs](../odbc/new-updated-odbc.md)
- [Neue und aktualisierte (0 + 0): **PowerShell für SQL** Docs](../powershell/new-updated-powershell.md)
- [Neue und aktualisierte (0 + 0): **Samples for SQL** Docs](../samples/new-updated-samples.md)
- [Neue und aktualisierte (0 + 0): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neue und aktualisierte (0 + 0): **XQuery für SQL** Docs](../xquery/new-updated-xquery.md)

