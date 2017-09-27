---
title: "Versionshinweise für SQL Server-2017 unter Linux | Microsoft Docs"
description: "Dieses Thema enthält die Versionshinweise und Funktionen für SQL Server-2017 unter Linux unterstützt. Anmerkungen zu dieser Version sind aus Gründen der RC2 und frühere Versionen."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/07/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.translationtype: MT
ms.sourcegitcommit: dbe6f832d4af55ddd15e12fba17a4da490fe19ae
ms.openlocfilehash: 14277304baaaf6aa40fe279af407c7ce915eaa60
ms.contentlocale: de-de
ms.lasthandoff: 09/25/2017

---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Versionshinweise für SQL Server-2017 unter Linux

Die folgenden Anmerkungen gelten für SQL Server-2017 auf Linux ausgeführt wird. Diese Version unterstützt viele der Funktionen des Datenbankmoduls der SQL Server für Linux. Im folgenden Thema wird für jede Version, ab der neuesten Version ist, RC2 in Abschnitte aufgeteilt. Konsultieren Sie die Informationen in den einzelnen Abschnitten für unterstützte Plattformen, Tools, Funktionen und bekannte Probleme.

Die folgende Tabelle enthält die Versionen von SQL Server-2017 in diesem Thema behandelt.

| Release | Version | Veröffentlichungsdatum |
|-----|-----|-----|
| [RC2](#RC2) | 14.0.900.75 | 8-2017 |
| [RC1](#RC1) | 14.0.800.90 | 7-2017 |
| [CTP-VERSION 2.1](#ctp21) | 14.0.600.250 | 5-2017 |
| [CTP 2.0](#ctp20) | 14.0.500.272 | 4-2017 |
| [CTP 1.4](#ctp14) | 14.0.405.198 | 3-2017 |
| [CTP-VERSION 1.3](#ctp13) | 14.0.304.138 | 2-2017 |
| [CTP-VERSION 1.2](#ctp12) | 14.0.200.24 | 1-2017 |
| [CTP-VERSION 1.1](#ctp11) | 14.0.100.187 | 12-2016 |
| [CTP 1.0](#ctp10) | 14.0.1.246 | 11-2016 |

## <a id="RC2"></a>RC2 (August 2017)

Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.900.75.

### <a name="supported-platforms"></a>Unterstützte Plattformen

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Installationshandbuch](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!NOTE]
> Sie benötigen mindestens 3,25 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
> SQL Server-Datenbankmodul wurde bis zu 1,5 TB Arbeitsspeicher zu diesem Zeitpunkt getestet.

### <a name="package-details"></a>Details zum Paket

Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Beachten Sie, dass Sie nicht benötigen, um diese Pakete direkt herunterzuladen, wenn Sie die Schritte in den folgenden Handbüchern zur Installation verwenden:

- [Installieren Sie SQL Server-Paket](sql-server-linux-setup.md)
- [Volltext-Suchdienst-Paket installieren](sql-server-linux-setup-full-text-search.md)
- [Installieren von SQL Server-Agent-Paket](sql-server-linux-setup-sql-agent.md)

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.900.75-1 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.900.75-1 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.900.75-1 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.900.75-1_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.900.75-1_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.900.75-1_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.900.75-1_amd64.deb) |

### <a name="supported-client-tools"></a>Unterstützte-Clienttools

| Tool | Mindestversion |
|-----|-----|
| [SQL Server Management Studio (SSMS) für Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools für Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio-Code](https://code.visualstudio.com) mit der [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) | neueste |

### <a name="Unsupported"></a>Nicht unterstützte Funktionen und Dienste

Die folgenden Features und Dienste sind zu diesem Zeitpunkt nicht verfügbar unter Linux. Die Unterstützung dieser Funktionen wird immer während der monatlichen Updates Rhythmus der Preview-Programm aktiviert werden.

| Bereich | Nicht unterstützte Funktion oder ein Dienst |
|-----|-----|
| **Datenbankmodul** | Transaktionsreplikation |
| &nbsp; | Mergereplikation |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Verteilte Abfragen mit 3rd Party Verbindungen |
| &nbsp; | Erweiterte gespeicherte Systemprozeduren (XP_CMDSHELL, usw.). |
| &nbsp; | Filetable |
| &nbsp; | Legen Sie die CLR-Assemblys mit der EXTERNAL_ACCESS oder UNSAFE-Berechtigung |
| &nbsp; | Pufferpoolerweiterung |
| **SQL Server-Agent** |  Subsysteme: CmdExec, PowerShell, Warteschlangenleser, SSIS, SSAS, SSRS |
| &nbsp; | Warnungen |
| &nbsp; | Protokolllese-Agent |
| &nbsp; | Change Data Capture |
| &nbsp; | Verwaltete Sicherung |
| **High Availability (Hohe Verfügbarkeit)** | Datenbankspiegelung  |
| **Sicherheit** | Erweiterbare Schlüsselverwaltung |
| **Dienste** | SQL Server-Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Bekannte Probleme

In den folgenden Abschnitten werden bekannte Probleme in dieser Version von SQL Server 2017 RC2 unter Linux beschrieben.

#### <a name="general"></a>Allgemein

- Die Länge des Hostnamens, auf dem SQL Server muss installiert sein, mit 15 Zeichen oder weniger ist. 

    - **Auflösung**: Ändern Sie den Namen in/Etc/Hostname um etwa 15 Zeichen enthalten.

- Die Systemzeit manuell Abwärtskompatibilität zeitlich festlegen führt dazu, dass SQL Server nicht mehr aktualisiert die interne Systemzeit innerhalb von SQL Server.

    - **Auflösung**: SQLServer neu starten.

- Nur die Einzelinstanz-Installationen werden unterstützt.

    - **Auflösung**: Wenn Sie mehrere Instanzen auf einem angegebenen Host verwenden möchten, erwägen Sie VMs oder Docker-Containern. 

- SQL Server-Konfigurations-Manager Verbindung keine mit SQL Server on Linux.

- Die Standardsprache der **sa** Anmeldung ist Englisch.

    - **Auflösung**: Ändern der Sprache des der **sa** melden Sie sich mit den **ALTER LOGIN** Anweisung.

#### <a name="databases"></a>Datenbanken

- Der master-Datenbank kann nicht mit dem Hilfsprogramm Mssql-Conf verschoben werden. Anderen Systemdatenbanken können mit Mssql-conf verschoben werden

- Beim Wiederherstellen einer Datenbank, die auf SQL Server on Windows gesichert wurde, müssen Sie verwenden die **WITH MOVE** -Klausel in Transact-SQL-Anweisung.

- Heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht auf SQL Server unter Linux unterstützt. SQL Server mit SQL Server, die verteilte Transaktionen unterstützt werden.

- Bestimmte Algorithmen (Verschlüsselungssammlungen) for Transport Layer Security (TLS) funktionieren nicht ordnungsgemäß mit SQL Server on Linux. Dies führt zu Verbindungsfehlern, beim Versuch, eine Verbindung mit SQL Server als auch Probleme herstellen von Verbindungen zwischen den Replikaten in Gruppen mit hoher Verfügbarkeit.

   - **Auflösung**: Ändern der **mssql.conf** Konfigurationsskript für SQL Server on Linux problematisch Verschlüsselungssuites zu deaktivieren, indem Sie folgende Aktionen ausgeführt:

      1. Fügen Sie Folgendes hinzu /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers=ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

      1. Starten Sie SQL Server mit dem folgenden Befehl neu.
   
      ```
      sudo systemctl restart mssql-server
      ```

- SQL Server 2014-Datenbanken unter Windows, die In-Memory OLTP verwenden, können nicht auf SQL Server-2017 unter Linux wiederhergestellt werden. Zum Wiederherstellen einer SQL Server 2014-Datenbank, die in-Memory OLTP verwendet, zunächst ein upgrade der Datenbanken auf SQL Server 2016 oder 2017 von SQL Server unter Windows bevor sie in SQL Server on Linux verschoben, über sichern/wiederherstellen oder trennen/anfügen.

#### <a name="remote-database-files"></a>Remote-Datenbankdateien

- Hosten der Datenbankdateien auf einer NFS-Server wird in dieser Version nicht unterstützt. Dazu gehören, verwenden Sie stattdessen NFS für freigegebene Datenträger Failoverclustering sowie Datenbanken für nicht gruppierte Instanzen. Wir arbeiten zur Aktivierung von NFS-Server-Unterstützung in zukünftigen Releases.

#### <a name="localization"></a>Lokalisierung

- Wenn das Gebietsschema Englisch (En_us) nicht während des Setups ist, müssen Sie die UTF-8-Codierung in der Bash-Sitzung/Terminaldienste verwenden. Wenn Sie die ASCII-Codierung verwenden, wird möglicherweise eine Fehlermeldung ähnlich der folgenden angezeigt:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Wenn Sie UTF-8-Codierung verwenden können, führen Sie Setup mithilfe der Umgebungsvariable MSSQL_LCID Ihrer Wahl der Sprache angeben.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

#### <a name="full-text-search"></a>Volltextsuche
- Nicht alle Filter sind in dieser Version, z. B. Filter für Office-Dokumente verfügbar. Eine Liste der unterstützten Filter, finden Sie unter [installieren Sie SQL Server-Volltextsuche unter Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
Sie können SSIS-Pakete auf Linux ausführen. Weitere Informationen finden Sie unter den folgenden Artikeln:
-   [Blog Post Ankündigung SSIS-Unterstützung für Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Installieren von SQL Server Integration Services (SSIS) unter Linux](sql-server-linux-setup-ssis.md)
-   [Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS](sql-server-linux-migrate-ssis.md)

Bitte beachten Sie die folgenden bekannten Probleme mit dieser Version.

- Die **Mssql Server ist** Paket wird in dieser Version für Ubuntu und Red Hat Enterprise Linux (RHEL) unterstützt.

- Mit SSIS unter Linux CTP-Version 2.1 aktualisiert und höher können SSIS-Pakete auf Linux ODBC-Verbindungen. Diese Funktion wurde mit SQL Server und die MySQL-ODBC-Treiber getestet, aber auch mit jeder Unicode-ODBC-Treiber arbeiten, die die ODBC-Spezifikation berücksichtigt werden sollen. Zur Entwurfszeit können Sie entweder einen DSN oder eine Verbindungszeichenfolge in die ODBC-Verbindung angeben; Sie können auch Windows-Authentifizierung verwenden. Weitere Informationen finden Sie unter der [Blogbeitrag Ankündigung ODBC-Unterstützung unter Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Die folgenden Funktionen werden in dieser Version nicht unterstützt, beim Ausführen von SSIS-Pakete auf Linux:
  - SSIS-Katalogdatenbank
  - Geplante paketausführung vom SQL-Agent
  - Windows-Authentifizierung
  - Drittanbieter-Komponenten
  - Change Data Capture (CDC)
  - SSIS für horizontales Skalieren
  - Azure FeaturePack für SSIS
  - Unterstützung für Hadoop und HDFS
  - Microsoft Connector for SAP BW

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Die folgenden Einschränkungen gelten für SSMS unter Windows, die mit SQL Server on Linux verbunden.

- Ausführen von Wartungsplänen werden nicht unterstützt.

- Management Data Warehouse (MDW) und der Datensammler in SSMS werden nicht unterstützt. 

- SSMS-UI-Komponenten, die Windows-Authentifizierung oder Windows-Ereignisprotokoll-Optionen verfügen funktionieren nicht mit Linux. Sie können diese Funktionen weiterhin mit anderen Optionen, z. B. SQL-Anmeldenamen verwenden. 

- Anzahl der Protokolldateien beibehalten werden sollen, nicht geändert werden.

### <a name="next-steps"></a>Nächste Schritte

Um zu beginnen, finden Sie unter den folgenden Schnellstart-Lernprogrammen:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Trennung Leiste-Grafik](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="RC1"></a>RC1 (Juli 2017)
Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.800.90.

### <a name="supported-platforms"></a>Unterstützte Plattformen 

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Installationshandbuch](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!NOTE]
> Sie benötigen mindestens 3,25 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
> SQL Server-Datenbankmodul wurde bis zu 1 TB Arbeitsspeicher zu diesem Zeitpunkt getestet.

### <a name="package-details"></a>Details zum Paket
Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Beachten Sie, dass Sie nicht benötigen, um diese Pakete direkt herunterzuladen, wenn Sie die Schritte in den folgenden Handbüchern zur Installation verwenden:

- [Installieren Sie SQL Server-Paket](sql-server-linux-setup.md)
- [Volltext-Suchdienst-Paket installieren](sql-server-linux-setup-full-text-search.md)
- [Installieren von SQL Server-Agent-Paket](sql-server-linux-setup-sql-agent.md)

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.800.90-2 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.800.90-2.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.800.90-2.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.800.90-2.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.800.90-2.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.800.90-2 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.800.90-2.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.800.90-2.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.800.90-2.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.800.90-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.800.90-2 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.800.90-2_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.800.90-2_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.800.90-2_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.800.90-2_amd64.deb) |

### <a name="supported-client-tools"></a>Unterstützte-Clienttools

| Tool | Mindestversion |
|-----|-----|
| [SQL Server Management Studio (SSMS) für Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools für Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio-Code](https://code.visualstudio.com) mit der [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) | neueste |

### <a name="unsupported-features-and-services"></a>Nicht unterstützte Funktionen und Dienste
Die folgenden Features und Dienste sind zu diesem Zeitpunkt nicht verfügbar unter Linux. Die Unterstützung dieser Funktionen wird immer während der monatlichen Updates Rhythmus der Preview-Programm aktiviert werden.

| Bereich | Nicht unterstützte Funktion oder ein Dienst |
|-----|-----|
| **Datenbankmodul** | Transaktionsreplikation |
| &nbsp; | Mergereplikation |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Verteilte Abfrage |
| &nbsp; | Machine Learning-Dienste |
| &nbsp; | Erweiterte gespeicherte Systemprozeduren (XP_CMDSHELL, usw.). |
| &nbsp; | Filetable |
| &nbsp; | Legen Sie die CLR-Assemblys mit der EXTERNAL_ACCESS oder UNSAFE-Berechtigung |
| **SQL Server-Agent** |  Subsysteme: CmdExec, PowerShell, Warteschlangenleser, SSIS, SSAS, SSRS |
| &nbsp; | Warnungen |
| &nbsp; | Protokolllese-Agent |
| &nbsp; | Change Data Capture |
| &nbsp; | Verwaltete Sicherung |
| **High Availability (Hohe Verfügbarkeit)** | Datenbankspiegelung  |
| &nbsp; | Verfügbarkeit Gruppe paralleles upgrade |
| **Sicherheit** | Erweiterbare Schlüsselverwaltung |
| **Dienste** | SQL Server-Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Bekannte Probleme
In den folgenden Abschnitten werden bekannte Probleme in dieser Version von SQL Server 2017 RC1 unter Linux beschrieben.

#### <a name="general"></a>Allgemein
- Die Länge des Hostnamens, auf dem SQL Server muss installiert sein, mit 15 Zeichen oder weniger ist. 

    - **Auflösung**: Ändern Sie den Namen in/Etc/Hostname um etwa 15 Zeichen enthalten.

- Die Systemzeit manuell Abwärtskompatibilität zeitlich festlegen führt dazu, dass SQL Server nicht mehr aktualisiert die interne Systemzeit innerhalb von SQL Server.

    - **Auflösung**: SQLServer neu starten.

- Nur die Einzelinstanz-Installationen werden unterstützt.

    - **Auflösung**: Wenn Sie mehrere Instanzen auf einem angegebenen Host verwenden möchten, erwägen Sie VMs oder Docker-Containern. 

- SQL Server-Konfigurations-Manager Verbindung keine mit SQL Server on Linux.

- Die Standardsprache der **sa** Anmeldung ist Englisch.

    - **Auflösung**: Ändern der Sprache des der **sa** melden Sie sich mit den **ALTER LOGIN** Anweisung.

#### <a name="databases"></a>Datenbanken

- Systemdatenbanken können nicht mit dem Hilfsprogramm Mssql-Conf verschoben werden.

- Beim Wiederherstellen einer Datenbank, die auf SQL Server on Windows gesichert wurde, müssen Sie verwenden die **WITH MOVE** -Klausel in Transact-SQL-Anweisung.

- Heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht auf SQL Server unter Linux unterstützt. SQL Server mit SQL Server, die verteilte Transaktionen unterstützt werden.

#### <a name="remote-database-files"></a>Remote-Datenbankdateien

- Hosten der Datenbankdateien auf einer NFS-Server wird in dieser Version nicht unterstützt. Dazu gehören, verwenden Sie stattdessen NFS für freigegebene Datenträger Failoverclustering sowie Datenbanken für nicht gruppierte Instanzen. Wir arbeiten zur Aktivierung von NFS-Server-Unterstützung in zukünftigen Releases.

#### <a name="cross-platform-availability-groups-and-distributed-availability-groups"></a>Plattformübergreifende Verfügbarkeitsgruppen und verteilte Verfügbarkeitsgruppen

- Aufgrund eines bekannten Problems ist das Erstellen von Verfügbarkeitsgruppen mit Replikaten auf gehosteten auf Windows- und Linux-Instanzen in dieser Version nicht funktionsfähig. Dies schließt verteilte Verfügbarkeitsgruppen ein. Das Update wird in der zukünftigen Release Candidate-Build verfügbar sein. 

#### <a name="server-collation"></a>Serversortierung

- Wenn mithilfe der MSSQL_COLLATION überschreiben oder bei der Installation ein lokalisiertes (nicht englische) ausführen, es ist möglich SQL Server wird einen Deadlock erreicht, wenn Sie möchten, legen Sie die serversortierung, der ein Speicherabbild erstellt. Setup wird erfolgreich abgeschlossen werden jedoch Sortierung des Servers wurde nicht festgelegt werden. Die problemumgehung besteht darin, führen Sie Folgendes aus. / Mssql-Conf Set-Sortierung, und geben Sie den Namen der Sortierung gewünscht wird, wenn Sie aufgefordert werden (der Sortierungsnamen finden Sie in das Fehlerprotokoll in der Befehlszeile: "Es wurde versucht, die standardsortierung auf ändern..."). 
 
#### <a name="localization"></a>Lokalisierung

- Wenn das Gebietsschema Englisch (En_us) nicht während des Setups ist, müssen Sie die UTF-8-Codierung in der Bash-Sitzung/Terminaldienste verwenden. Wenn Sie die ASCII-Codierung verwenden, wird möglicherweise eine Fehlermeldung ähnlich der folgenden angezeigt:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Wenn Sie UTF-8-Codierung verwenden können, führen Sie Setup mithilfe der Umgebungsvariable MSSQL_LCID Ihrer Wahl der Sprache angeben.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

#### <a name = "fci"></a>Freigegebene Datenträger Instanz clusterupgrade

Der Cluster-Ressourcen-Agent legt den Namen des virtuellen Servers in RC1 wie es in einer Failoverclusterinstanz auf Windows fest. Bevor Sie RC1 `@@servername` auf einem freigegebenen Datenträger Cluster den bestimmten Knoten zurückgegeben nennen dies nach einem Failover `@@servername` einen anderen Wert zurückgegeben. In RC1 wird der ServerName der freigegebenen Datenträger gruppierten Instanz mit dem Ressourcennamen aktualisiert, wenn die Ressource zum Cluster hinzugefügt wird. Aus diesem Grund müssen der Cluster nach dem manuellen Failover der SQL Server neu starten, während des Upgrades – wie in der folgenden Schritte aus:

1. Aktualisieren Sie zuerst die sekundären (passiven) Knoten.
   - Upgrade **Mssql Server** Paket.
   - Upgrade **Mssql-Server-ha** Paket.
1. Ein manuelles Failover zu aktualisierten Knoten.
   `pcs resource move <resourceName>`
   - Bei einem Ausfall anfänglich daran, dass der Agent für die Ressource der tatsächlichen und der erwarteten ServerName überprüft. Der erwartete ServerName ist unterschiedlich sein.
   - Cluster wird SQL Server-Ressource auf demselben Knoten neu gestartet. Den Namen des Servers werden aktualisiert.
1. Aktualisieren Sie den anderen Knoten. 
   - Upgrade **Mssql Server** Paket.
   - Upgrade **Mssql-Server-ha** Paket.
1. Entfernen Sie die Einschränkung, die durch die manuelle ressourcenverschiebung hinzugefügt. Finden Sie unter [Failovercluster manuell](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md#failManual).
2. Falls gewünscht, Failback auf den ursprünglichen Primärknoten. 

#### <a name="availability-group"></a>Verfügbarkeitsgruppe

Unter Linux wird die paralleles Upgrade von SQL Server 2017 CTP-Version 2.1 auf RC1 nicht unterstützt. Nach dem upgrade des sekundären Replikats, wird diese vom primären Replikat getrennt, bis das primäre Replikat aktualisiert wird. Microsoft ist zum Beheben dieses Problems für eine künftige Version planen.

#### <a name="full-text-search"></a>Volltextsuche
- Nicht alle Filter sind in dieser Version, z. B. Filter für Office-Dokumente verfügbar. Eine Liste der unterstützten Filter, finden Sie unter [installieren Sie SQL Server-Volltextsuche unter Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- Die **Mssql Server ist** Paket SUSE in dieser Version nicht unterstützt wird. Es wird zurzeit auf Ubuntu und auf Red Hat Enterprise Linux (RHEL) unterstützt.

- Die folgenden Funktionen werden in dieser Version nicht unterstützt, beim Ausführen von SSIS-Pakete auf Linux:
  - SSIS-Katalogdatenbank
  - Geplante paketausführung vom SQL-Agent
  - Windows-Authentifizierung
  - Drittanbieter-Komponenten
  - Change Data Capture (CDC)
  - SSIS für horizontales Skalieren
  - Azure FeaturePack für SSIS
  - Unterstützung für Hadoop und HDFS
  - Microsoft Connector for SAP BW

Weitere Informationen zu SSIS unter Linux finden Sie unter den folgenden Artikeln:
-   [Installieren von SQL Server Integration Services (SSIS) unter Linux](sql-server-linux-setup-ssis.md)
-   [Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Die folgenden Einschränkungen gelten für SSMS unter Windows, die mit SQL Server on Linux verbunden.

- Ausführen von Wartungsplänen werden nicht unterstützt.

- Management Data Warehouse (MDW) und der Datensammler in SSMS werden nicht unterstützt. 

- SSMS-UI-Komponenten, die Windows-Authentifizierung oder Windows-Ereignisprotokoll-Optionen verfügen funktionieren nicht mit Linux. Sie können diese Funktionen weiterhin mit anderen Optionen, z. B. SQL-Anmeldenamen verwenden. 

- Anzahl der Protokolldateien beibehalten werden sollen, nicht geändert werden.

### <a name="next-steps"></a>Nächste Schritte

Um zu beginnen, finden Sie unter den folgenden Schnellstart-Lernprogrammen:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Trennung Leiste-Grafik](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp21"></a>CTP-Version 2.1 (Mai 2017)
Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.600.250.

### <a name="supported-platforms"></a>Unterstützte Plattformen 

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Installationshandbuch](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!NOTE]
> Sie benötigen mindestens 3,25 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
> SQL Server-Datenbankmodul wurde bis zu 1 TB Arbeitsspeicher zu diesem Zeitpunkt getestet.

### <a name="package-details"></a>Details zum Paket
Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Sie brauchen diese Pakete direkt herunterladen, wenn Sie die Schritte in den folgenden Handbüchern zur Installation verwenden:

- [Installieren Sie SQL Server-Paket](sql-server-linux-setup.md)
- [Volltext-Suchdienst-Paket installieren](sql-server-linux-setup-full-text-search.md)
- [Installieren von SQL Server-Agent-Paket](sql-server-linux-setup-sql-agent.md)

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.600.250-2 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.600.250-2.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.600.250-2.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.600.250-2.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.600.250-2.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.600.250-2 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.600.250-2.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.600.250-2.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.600.250-2.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.600.250-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.600.250-2 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.600.250-2_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.600.250-2_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.600.250-2_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.600.250-2_amd64.deb) |

### <a name="supported-client-tools"></a>Unterstützte-Clienttools

| Tool | Mindestversion |
|-----|-----|
| [SQL Server Management Studio (SSMS) für Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools für Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio-Code](https://code.visualstudio.com) mit der [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) | Neueste (1.12) |

### <a name="unsupported-features-and-services"></a>Nicht unterstützte Funktionen und Dienste
Die folgenden Features und Dienste sind zu diesem Zeitpunkt nicht verfügbar unter Linux. Die Unterstützung dieser Funktionen wird immer während der monatlichen Updates Rhythmus der Preview-Programm aktiviert werden.

| Bereich | Nicht unterstützte Funktion oder ein Dienst |
|-----|-----|
| **Datenbankmodul** | Replikation |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Verteilte Abfrage |
| &nbsp; | Erweiterte gespeicherte Systemprozeduren (XP_CMDSHELL, usw.). |
| &nbsp; | Filetable |
| &nbsp; | Legen Sie die CLR-Assemblys mit der EXTERNAL_ACCESS oder UNSAFE-Berechtigung |
| **High Availability (Hohe Verfügbarkeit)** | Datenbankspiegelung  |
| **Sicherheit** | Active Directory-Authentifizierung |
| &nbsp; | Windows-Authentifizierung |
| &nbsp; | Erweiterbare Schlüsselverwaltung |
| &nbsp; | Verwendung von vom Benutzer bereitgestellte Zertifikat für SSL oder TLS |
| **Dienste** | SQL Server-Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Bekannte Probleme
In den folgenden Abschnitten werden bekannte Probleme in dieser Version von SQL Server 2017 CTP-Version 2.1 unter Linux beschrieben.

#### <a name="general"></a>Allgemein
- Die Länge des Hostnamens, auf dem SQL Server muss installiert sein, mit 15 Zeichen oder weniger ist. 

    - **Auflösung**: Ändern Sie den Namen in/Etc/Hostname um etwa 15 Zeichen enthalten.

- Die Systemzeit manuell Abwärtskompatibilität zeitlich festlegen führt dazu, dass SQL Server nicht mehr aktualisiert die interne Systemzeit innerhalb von SQL Server.

    - **Auflösung**: SQLServer neu starten.

- Nur die Einzelinstanz-Installationen werden unterstützt.

    - **Auflösung**: Wenn Sie mehrere Instanzen auf einem angegebenen Host verwenden möchten, erwägen Sie VMs oder Docker-Containern. 

- SQL Server-Konfigurations-Manager Verbindung keine mit SQL Server on Linux.

- Die Standardsprache der **sa** Anmeldung ist Englisch.

    - **Auflösung**: Ändern der Sprache des der **sa** melden Sie sich mit den **ALTER LOGIN** Anweisung.

#### <a name="databases"></a>Datenbanken
- Systemdatenbanken können nicht mit dem Hilfsprogramm Mssql-Conf verschoben werden.

- Beim Wiederherstellen einer Datenbank, die auf SQL Server on Windows gesichert wurde, müssen Sie verwenden die **WITH MOVE** -Klausel in Transact-SQL-Anweisung.

- Heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht auf SQL Server unter Linux unterstützt. SQL Server mit SQL Server, die verteilte Transaktionen unterstützt werden.

#### <a name="always-on-availability-group"></a>Always On-Verfügbarkeitsgruppe.
- `sys.fn_hadr_backup_is_preffered_replica`funktioniert nicht für `CLUSTER_TYPE=NONE` oder `CLUSTER_TYPE=EXTERNAL` daran, dass sie die WSFC-repliziert Clusterregistrierung benötigt Schlüssel dem nicht verfügbar. Wir arbeiten über eine andere Funktion eine ähnliche Funktionalität bereitstellen. 

#### <a name="full-text-search"></a>Volltextsuche
- Nicht alle Filter sind in dieser Version, z. B. Filter für Office-Dokumente verfügbar. Eine Liste der unterstützten Filter, finden Sie unter [installieren Sie SQL Server-Volltextsuche unter Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a name="sql-agent"></a>SQL-Agent
- Die folgenden Komponenten und Subsysteme des SQL Agent-Aufträge werden unter Linux derzeit nicht unterstützt:

    - Subsysteme: CmdExec, PowerShell, Replikationsverteiler, Momentaufnahme, Merge, Warteschlangenleser, SSIS, SSAS, SSRS
    - Warnungen
    - DB-Mail
    - Protokolllese-Agent 
    - Change Data Capture

#### <a name="sqlpackage"></a>SqlPackage
- Mithilfe des SqlPackage muss einen absoluten Pfad für Dateien angegeben werden. Verwenden relative Pfade werden Dateien unter "/ Tmp /-Sqlpackage. zugeordnet. \<Code \> /System/system32 "Ordner. 

  - **Auflösung**: absolute Pfade verwenden.

- SqlPackage zeigt den Speicherort der Dateien mit einer "" c: "\\" Präfix.

#### <a name="ssis"></a> SQL Server Integration Services (SSIS)
Sie können SSIS-Pakete auf Linux ausführen. Weitere Informationen finden Sie unter der [Blog Post Ankündigung SSIS-Unterstützung für Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). Bitte beachten Sie die folgenden bekannten Probleme mit dieser Version.

- Die **Mssql Server ist** Paket wird nur auf Ubuntu zu diesem Zeitpunkt unterstützt.

- Die folgenden Funktionen werden nicht unterstützt, wenn SSIS-Pakete auf Linux ausgeführt wird:
  - SSIS-Katalog DB
  - Planen der Ausführung von Paketen vom SQL-Agent
  - Windows-Authentifizierung
  - Drittanbieter-Komponenten
  - ODBC-Treiber von Drittanbietern
  - ODBC-Verbindungs-Manager, Quelle und Ziel (mit SSIS auf Linux CTP-Version 2.1 aktualisieren unterstützt)
  - Change Data Capture (CDC)
  - Horizontale Hochskalierung
  - Azure Feature Pack
  - Hadoop und HDFS-Unterstützung
  - Microsoft Connector for SAP BW

Mit SSIS auf Linux CTP-Version 2.1 aktualisiert können SSIS-Pakete auf Linux ODBC-Verbindungen. Weitere Informationen finden Sie unter der [Blogbeitrag Ankündigung ODBC-Unterstützung unter Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Die folgenden Einschränkungen gelten für SSMS unter Windows, die mit SQL Server on Linux verbunden.

- Ausführen von Wartungsplänen werden nicht unterstützt.

- Management Data Warehouse (MDW) und der Datensammler in SSMS werden nicht unterstützt. 

- SSMS-UI-Komponenten, die Windows-Authentifizierung oder Windows-Ereignisprotokoll-Optionen verfügen funktionieren nicht mit Linux. Sie können diese Funktionen weiterhin mit anderen Optionen, z. B. SQL-Anmeldenamen verwenden. 

- Anzahl der Protokolldateien beibehalten werden sollen, nicht geändert werden.

### <a name="next-steps"></a>Nächste Schritte

Um zu beginnen, finden Sie unter den folgenden Schnellstart-Lernprogrammen:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Trennung Leiste-Grafik](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp20"></a>CTP 2.0 (April 2017)
Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.500.272.

### <a name="supported-platforms"></a>Unterstützte Plattformen 

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Installationshandbuch](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS und 16.10 | EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Sie benötigen mindestens 3,25 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
> SQL Server-Datenbankmodul wurde bis zu 1 TB Arbeitsspeicher zu diesem Zeitpunkt getestet.

### <a name="package-details"></a>Details zum Paket
Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Beachten Sie, dass Sie nicht benötigen, um diese Pakete direkt herunterzuladen, wenn Sie die Schritte in den folgenden Handbüchern zur Installation verwenden:

- [Installieren Sie SQL Server-Paket](sql-server-linux-setup.md)
- [Volltext-Suchdienst-Paket installieren](sql-server-linux-setup-full-text-search.md)
- [Installieren von SQL Server-Agent-Paket](sql-server-linux-setup-sql-agent.md)

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.500.272-2 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.500.272-2.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.500.272-2.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.500.272-2.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.500.272-2.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.500.272-2 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.500.272-2.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.500.272-2.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.500.272-2.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.500.272-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.500.272-2 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.500.272-2_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.500.272-2_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.500.272-2_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.500.272-2_amd64.deb) |
| Ubuntu 16.10 Debian-Paket | 14.0.500.272-2 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.500.272-2_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.500.272-2_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.500.272-2_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.500.272-2_amd64.deb) |

### <a name="supported-client-tools"></a>Unterstützte-Clienttools

| Tool | Mindestversion |
|-----|-----|
| [SQL Server Management Studio (SSMS) für Windows - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools für Visual Studio - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Visual Studio-Code](https://code.visualstudio.com) mit der [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) | Neueste (0.2.1) |

> [!NOTE] 
> Die angegebenen Versionen von SQL Server Management Studio und SQL Server Data Tools sind höher Release Candidates, daher für die Verwendung in der Produktion nicht empfohlen.

### <a name="unsupported-features-and-services"></a>Nicht unterstützte Funktionen und Dienste
Die folgenden Features und Dienste sind zu diesem Zeitpunkt nicht verfügbar unter Linux. Die Unterstützung dieser Funktionen wird immer während der monatlichen Updates Rhythmus der Preview-Programm aktiviert werden.

| Bereich | Nicht unterstützte Funktion oder ein Dienst |
|-----|-----|
| **Datenbankmodul** | Replikation |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Verteilte Abfrage |
| &nbsp; | Erweiterte gespeicherte Systemprozeduren (XP_CMDSHELL, usw.). |
| &nbsp; | Filetable |
| &nbsp; | Legen Sie die CLR-Assemblys mit der EXTERNAL_ACCESS oder UNSAFE-Berechtigung |
| **High Availability (Hohe Verfügbarkeit)** | Datenbankspiegelung  |
| **Sicherheit** | Active Directory-Authentifizierung |
| &nbsp; | Windows-Authentifizierung |
| &nbsp; | Erweiterbare Schlüsselverwaltung |
| &nbsp; | Verwendung von vom Benutzer bereitgestellte Zertifikat für SSL oder TLS |
| **Dienste** | SQL Server-Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Bekannte Probleme
In den folgenden Abschnitten werden bekannte Probleme in dieser Version von SQL Server 2017 CTP 2.0 unter Linux beschrieben.

#### <a name="general"></a>Allgemein
- Die Länge des Hostnamens, auf dem SQL Server muss installiert sein, mit 15 Zeichen oder weniger ist. 

    - **Auflösung**: Ändern Sie den Namen in/Etc/Hostname um etwa 15 Zeichen enthalten.

- Die Systemzeit manuell Abwärtskompatibilität zeitlich festlegen führt dazu, dass SQL Server nicht mehr aktualisiert die interne Systemzeit innerhalb von SQL Server.

    - **Auflösung**: SQLServer neu starten.

- Nur die Einzelinstanz-Installationen werden unterstützt.

    - **Auflösung**: Wenn Sie mehrere Instanzen auf einem angegebenen Host verwenden möchten, erwägen Sie VMs oder Docker-Containern. 

- SQL Server-Konfigurations-Manager Verbindung keine mit SQL Server on Linux.

- Die Standardsprache der **sa** Anmeldung ist Englisch.

    - **Auflösung**: Ändern der Sprache des der **sa** melden Sie sich mit den **ALTER LOGIN** Anweisung.

#### <a name="databases"></a>Datenbanken
- Systemdatenbanken können nicht mit dem Hilfsprogramm Mssql-Conf verschoben werden.

- Beim Wiederherstellen einer Datenbank, die auf SQL Server on Windows gesichert wurde, müssen Sie verwenden die **WITH MOVE** -Klausel in Transact-SQL-Anweisung.

- Heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht auf SQL Server unter Linux unterstützt. SQL Server mit SQL Server, die verteilte Transaktionen unterstützt werden.

#### <a name="always-on-availability-group"></a>Always On-Verfügbarkeitsgruppe.
- Alle HA-Konfigurationen - was bedeutet, dass die verfügbarkeitsgruppe als Ressource eine Schrittmacher Cluster - mit vor CTP2. 0-Pakete erstellt hinzugefügt wird, sind nicht abwärtskompatibel mit der neuen Paket. Löschen Sie alle zuvor konfigurierte Clusterressourcen und erstellen Sie neue Verfügbarkeitsgruppen mit `CLUSTER_TYPE=EXTERNAL`. Finden Sie unter [konfigurieren Always On-Verfügbarkeitsgruppe für SQLServer on Linux](sql-server-linux-availability-group-configure-ha.md).
- Erstellt mit Verfügbarkeitsgruppen `CLUSTER_TYPE=NONE` und können nicht hinzugefügt werden, wie Ressourcen im Cluster nach dem Upgrade weiterarbeiten können. Skalieren von Lesevorgängen Szenarien zur Verwendung. Finden Sie unter [konfigurieren Skalieren von Lesevorgängen verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-rs.md).
- `sys.fn_hadr_backup_is_preffered_replica`funktioniert nicht für `CLUSTER_TYPE=NONE` oder `CLUSTER_TYPE=EXTERNAL` daran, dass sie die WSFC-repliziert Clusterregistrierung benötigt Schlüssel dem nicht verfügbar. Wir arbeiten über eine andere Funktion eine ähnliche Funktionalität bereitstellen. 

#### <a name="full-text-search"></a>Volltextsuche
- Nicht alle Filter sind in dieser Version, z. B. Filter für Office-Dokumente verfügbar. Eine Liste der unterstützten Filter, finden Sie unter [installieren Sie SQL Server-Volltextsuche unter Linux](sql-server-linux-setup-full-text-search.md#filters).

- Die koreanische wörtertrennung benötigt einige Sekunden zum Laden und generiert einen Fehler bei der erstmaligen Verwendung. Nach diesem ersten Fehler sollte es ordnungsgemäß funktionieren.

#### <a name="sql-agent"></a>SQL-Agent
- Die folgenden Komponenten und Subsysteme des SQL Agent-Aufträge werden unter Linux derzeit nicht unterstützt:

    - Subsysteme: CmdExec, PowerShell, Replikationsverteiler, Momentaufnahme, Merge, Warteschlangenleser, SSIS, SSAS, SSRS
    - Warnungen
    - DB-Mail
    - Protokolllese-Agent 
    - Change Data Capture

#### <a name="sqlpackage"></a>SqlPackage
- Mithilfe des SqlPackage muss einen absoluten Pfad für Dateien angegeben werden. Verwenden relative Pfade werden Dateien unter "/ Tmp /-Sqlpackage. zugeordnet. \<Code \> /System/system32 "Ordner. 

    - **Auflösung**: absolute Pfade verwenden.

- SqlPackage zeigt den Speicherort der Dateien mit einer "" c: "\\" Präfix.

    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Die folgenden Einschränkungen gelten für SSMS unter Windows, die mit SQL Server on Linux verbunden.

- Ausführen von Wartungsplänen werden nicht unterstützt.

- Management Data Warehouse (MDW) und der Datensammler in SSMS werden nicht unterstützt. 

- SSMS-UI-Komponenten, die Windows-Authentifizierung oder Windows-Ereignisprotokoll-Optionen verfügen funktionieren nicht mit Linux. Sie können diese Funktionen weiterhin mit anderen Optionen, z. B. SQL-Anmeldenamen verwenden. 

- Anzahl der Protokolldateien beibehalten werden sollen, nicht geändert werden.

### <a name="next-steps"></a>Nächste Schritte

Um zu beginnen, finden Sie unter den folgenden Schnellstart-Lernprogrammen:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Trennung Leiste-Grafik](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp14"></a>CTP-Version 1.4 (März 2017)
Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.405.198.

### <a name="supported-platforms"></a>Unterstützte Plattformen 

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Installationshandbuch](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS und 16.10 | EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Sie benötigen mindestens 3,25 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
> SQL Server-Datenbankmodul wurde bis zu 1 TB Arbeitsspeicher zu diesem Zeitpunkt getestet.

### <a name="package-details"></a>Details zum Paket
Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Beachten Sie, dass Sie nicht benötigen, um diese Pakete direkt herunterladen, wenn Sie die Schritte in den folgenden Handbüchern zur Installation verwenden
-   [Installieren Sie SQL Server-Paket](sql-server-linux-setup.md)
-   [Volltext-Suchdienst-Paket installieren](sql-server-linux-setup-full-text-search.md)
-   [Installieren von SQL Server-Agent-Paket](sql-server-linux-setup-sql-agent.md)

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.405.200-1 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.405.200-1.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.405.200-1.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.405.200-1.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.405.200-1.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.405.200-1 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.405.200-1.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.405.200-1.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.405.200-1.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.405.200-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.405.200-1 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.405.200-1_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.405.200-1_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.405.200-1_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.405.200-1_amd64.deb) |
| Ubuntu 16.10 Debian-Paket | 14.0.405.200-1 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.405.200-1_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.405.200-1_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.405.200-1_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.405.200-1_amd64.deb) |

### <a name="supported-client-tools"></a>Unterstützte-Clienttools

| Tool | Mindestversion |
|-----|-----|
| [SQL Server Management Studio (SSMS) für Windows - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools für Visual Studio - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Visual Studio-Code](https://code.visualstudio.com) mit der [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) | Neueste (0.2.1) |

> [!NOTE] 
> Die angegebenen Versionen von SQL Server Management Studio und SQL Server Data Tools sind höher Release Candidates, daher für die Verwendung in der Produktion nicht empfohlen.

### <a name="unsupported-features-and-services"></a>Nicht unterstützte Funktionen und Dienste
Die folgenden Features und Dienste sind zu diesem Zeitpunkt nicht verfügbar unter Linux. Die Unterstützung dieser Funktionen wird immer während der monatlichen Updates Rhythmus der Preview-Programm aktiviert werden.

| Bereich | Nicht unterstützte Funktion oder ein Dienst |
|-----|-----|
| **Datenbankmodul** | Replikation |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Verteilte Abfrage |
| &nbsp; | Erweiterte gespeicherte Systemprozeduren (XP_CMDSHELL, usw.). |
| &nbsp; | Filetable |
| &nbsp; | Legen Sie die CLR-Assemblys mit der EXTERNAL_ACCESS oder UNSAFE-Berechtigung |
| **High Availability (Hohe Verfügbarkeit)** | Datenbankspiegelung  |
| **Sicherheit** | Active Directory-Authentifizierung |
| &nbsp; | Windows-Authentifizierung |
| &nbsp; | Erweiterbare Schlüsselverwaltung |
| &nbsp; | Verwendung von vom Benutzer bereitgestellte Zertifikat für SSL oder TLS |
| **Dienste** | SQL Server-Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Bekannte Probleme
In den folgenden Abschnitten werden bekannte Probleme mit dieser Version von SQL Server 2017 CTP 1.4 auf Linux beschrieben.

#### <a name="general"></a>Allgemein
- Die Länge des Hostnamens, auf dem SQL Server muss installiert sein, mit 15 Zeichen oder weniger ist. 

    - **Auflösung**: Ändern Sie den Namen in/Etc/Hostname um etwa 15 Zeichen enthalten.

- Führen Sie den Befehl nicht `ALTER SERVICE MASTER KEY REGENERATE`. Es ist ein bekanntes Problem, das SQL Server instabil bewirkt. Wenn Sie mit dem Diensthauptschlüssel neu generieren müssen, sollten Sie sichern Sie die Datenbankdateien deinstallieren und erneut installieren von SQL Server, und stellen Sie die Datenbankdateien wieder her.

- Die Systemzeit manuell Abwärtskompatibilität zeitlich festlegen führt dazu, dass SQL Server nicht mehr aktualisiert die interne Systemzeit innerhalb von SQL Server.

    - **Auflösung**: SQLServer neu starten.

- Einige Namen Zeitzone in Linux zuordnen nicht genau die Namen der Windows-Zeitzonen.

    - **Auflösung**: Verwenden Sie die Zeitzone Namen aus TZID-Spalte in der ' Zuordnung für: 'Windows-Section-Tabelle auf die [Unicode.org Dokumentationsseite](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- SQL Server-Datenbankmodul erwartet, dass Zeilen in Textdateien mit CR-LF (Windows-Stil Zeile Formatierung) beendet werden soll.

- Nur die Einzelinstanz-Installationen werden unterstützt.

    - **Auflösung**: Wenn Sie mehrere Instanzen auf einem angegebenen Host verwenden möchten, erwägen Sie VMs oder Docker-Containern. 

- Alle Protokolldateien und Fehlerprotokolle in UTF-16 codiert sind.

- SQL Server-Konfigurations-Manager Verbindung keine mit SQL Server on Linux.

- **CREATE ASSEMBLY** funktioniert nicht bei dem Versuch, eine Datei zu verwenden. Verwenden der **FROM \<Bits\> ** Methode stattdessen vorläufig. 

#### <a name="databases"></a>Datenbanken
- Systemdatenbanken können nicht mit dem Hilfsprogramm Mssql-Conf verschoben werden.

- Beim Wiederherstellen einer Datenbank, die auf SQL Server on Windows gesichert wurde, müssen Sie verwenden die **WITH MOVE** -Klausel in Transact-SQL-Anweisung.

- Heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht auf SQL Server unter Linux unterstützt. SQL Server mit SQL Server, die verteilte Transaktionen unterstützt werden.

#### <a name="always-on-availability-group"></a>Always On-Verfügbarkeitsgruppe.
- AlwaysOn-Verfügbarkeitsgruppe, die Clusterressourcen unter Linux, die mit der CTP-Version 1.3 erstellt wurden nach dem upgrade der HA-Paket (Mssql-Server-ha) fehl. 

   - **Auflösung**: vor dem upgrade der HA-Paket, legen Sie den Cluster-Ressourcen-Parameter `notify=true`. 
   
      - Im folgenden Beispiel wird den Cluster-Ressourcen-Parameter für eine Ressource mit dem Namen **ag1** für RHEL oder Ubuntu: 

      ```bash
      sudo pcs resource update ag1-master notify=true
      ```

      - Aktualisieren Sie die Konfiguration von Verfügbarkeitsgruppen Ressource hinzufügen für SLES `notify=true`.  

      ```bash
      crm configure edit ms-ag_cluster 
      ```

      Hinzufügen `notify=true` und die Konfiguration zu speichern.

- AlwaysOn-Verfügbarkeitsgruppen unter Linux müssen gelegentlich Datenverlust werden, wenn Replikate befinden sich im synchronen Commit-Modus. Finden Sie Details nach Bedarf für Ihre Linux-Distributionen. 

   - [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   - [SLES](sql-server-linux-availability-group-cluster-sles.md)
   - [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

#### <a name="full-text-search"></a>Volltextsuche
- Nicht alle Filter sind in dieser Version, z. B. Filter für Office-Dokumente verfügbar. Eine Liste der unterstützten Filter, finden Sie unter [installieren Sie SQL Server-Volltextsuche unter Linux](sql-server-linux-setup-full-text-search.md#filters).

- Die koreanische wörtertrennung benötigt einige Sekunden zum Laden und generiert einen Fehler bei der erstmaligen Verwendung. Nach diesem ersten Fehler sollte es ordnungsgemäß funktionieren.

#### <a name="sql-agent"></a>SQL-Agent
- Die folgenden Komponenten und Subsysteme des SQL Agent-Aufträge werden unter Linux derzeit nicht unterstützt:
    - Subsysteme: CmdExec, PowerShell, Replikationsverteiler, Momentaufnahme, Merge, Warteschlangenleser, SSIS, SSAS, SSRS
    - Warnungen
    - DB-Mail
    - Protokollversand
    - Protokolllese-Agent 
    - Change Data Capture

#### <a name="in-memory-oltp"></a>In-Memory OLTP
- In-Memory OLTP-Datenbanken können nur im Verzeichnis /var/opt/mssql erstellt werden. Weitere Informationen finden Sie auf der [In-Memory-OLTP-Thema](sql-server-linux-performance-get-started.md#use-in-memory-oltp).

#### <a name="sqlpackage"></a>SqlPackage
- Mithilfe des SqlPackage muss einen absoluten Pfad für Dateien angegeben werden. Verwenden relative Pfade werden Dateien unter "/ Tmp /-Sqlpackage. zugeordnet. \<Code \> /System/system32 "Ordner. 

    - **Auflösung**: absolute Pfade verwenden.

- SqlPackage zeigt den Speicherort der Dateien mit einer "" c: "\\" Präfix.

    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Die folgenden Einschränkungen gelten für SSMS unter Windows, die mit SQL Server on Linux verbunden.

- Ausführen von Wartungsplänen werden nicht unterstützt.

- Management Data Warehouse (MDW) und der Datensammler in SSMS wird nicht unterstützt. 

- SSMS-UI-Komponenten, die Windows-Authentifizierung oder Windows-Ereignisprotokoll-Optionen verfügen funktionieren nicht mit Linux. Sie können diese Funktionen weiterhin mit anderen Optionen, z. B. SQL-Anmeldenamen verwenden. 

- Die Dateibrowser ist beschränkt auf die "" c: "\\" Gültigkeitsbereich auflöst/Var/opt/Mssql/unter Linux. Um andere Pfade verwenden zu können, Generieren von Skripts, der den UI-Vorgang aus, und Ersetzen Sie die "c:"\\ Pfade mit Linux-Pfaden. Führen Sie das Skript dann manuell in SSMS.

- Anzahl der Protokolldateien beibehalten werden sollen, nicht geändert werden.

### <a name="next-steps"></a>Nächste Schritte

Um zu beginnen, finden Sie unter den folgenden Schnellstart-Lernprogrammen:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Trennung Leiste-Grafik](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp13"></a>CTP-Version 1.3 (Version von Februar 2017)
Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.304.138.

### <a name="supported-platforms"></a>Unterstützte Plattformen 

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Installationshandbuch](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS und 16.10 | EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Sie benötigen mindestens 3,25 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
> SQL Server-Datenbankmodul wurde bis zu 1 TB Arbeitsspeicher zu diesem Zeitpunkt getestet.

### <a name="package-details"></a>Details zum Paket
Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Beachten Sie, dass Sie nicht benötigen, um diese herunterzuladen Pakete direkt auf, wenn Sie die Schritte im Verwenden der [Installationshandbüchern](sql-server-linux-setup.md).

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.304.138-1 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.304.138-1.x86_64.rpm)</br>[MSSQL-Server-ha hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.304.138-1.x86_64.rpm)</br>[MSSQL-Server-Fts Full-Text Search RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.304.138-1.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.304.138-1 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.304.138-1.x86_64.rpm)</br>[MSSQL-Server-ha hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.304.138-1.x86_64.rpm)</br>[MSSQL-Server-Fts Full-Text Search RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.304.138-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.304.138-1 | [MSSQL-Server-Datenbankmodul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.304.138-1_amd64.deb)</br>[MSSQL-Server-ha hohe Verfügbarkeit Debian Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.304.138-1_amd64.deb)</br>[MSSQL-Server-Fts Volltextsuche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.304.138-1_amd64.deb) |
| Ubuntu 16.10 Debian-Paket | 14.0.304.138-1 | [MSSQL-Server-Datenbankmodul Debian-Paket](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.304.138-1_amd64.deb)</br>[MSSQL-Server-ha hohe Verfügbarkeit Debian Paket](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.304.138-1_amd64.deb)</br>[MSSQL-Server-Fts Volltextsuche Debian-Paket](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.304.138-1_amd64.deb) |

### <a name="supported-client-tools"></a>Unterstützte-Clienttools

| Tool | Mindestversion |
|-----|-----|
| [SQL Server Management Studio (SSMS) für Windows - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools für Visual Studio - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Visual Studio-Code](https://code.visualstudio.com) mit der [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) | Neueste (0.2.1) |

> [!NOTE] 
> Die angegebenen Versionen von SQL Server Management Studio und SQL Server Data Tools sind höher Release Candidates, daher für die Verwendung in der Produktion nicht empfohlen.

### <a name="unsupported-features-and-services"></a>Nicht unterstützte Funktionen und Dienste
Die folgenden Features und Dienste sind zu diesem Zeitpunkt nicht verfügbar unter Linux. Die Unterstützung dieser Funktionen wird immer während der monatlichen Updates Rhythmus der Preview-Programm aktiviert werden.

| Bereich | Nicht unterstützte Funktion oder ein Dienst |
|-----|-----|
| **Datenbankmodul** | Replikation |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Verteilte Abfrage |
| &nbsp; | Erweiterte gespeicherte Systemprozeduren (XP_CMDSHELL, usw.). |
| &nbsp; | Filetable |
| &nbsp; | Legen Sie die CLR-Assemblys mit der EXTERNAL_ACCESS oder UNSAFE-Berechtigung |
| **High Availability (Hohe Verfügbarkeit)** | Datenbankspiegelung  |
| **Sicherheit** | Active Directory-Authentifizierung |
| &nbsp; | Windows-Authentifizierung |
| &nbsp; | Erweiterbare Schlüsselverwaltung |
| &nbsp; | Verwendung von vom Benutzer bereitgestellte Zertifikat für SSL oder TLS |
| **Dienste** | SQL Server-Agent |
| &nbsp; | SQL Server-Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Bekannte Probleme
In den folgenden Abschnitten werden bekannte Probleme mit dieser Version von SQL Server 2017 CTP-Version 1.3 auf Linux beschrieben.

#### <a name="general"></a>Allgemein
- Die Länge des Hostnamens, auf dem SQL Server muss installiert sein, mit 15 Zeichen oder weniger ist. 

    - **Auflösung**: Ändern Sie den Namen in/Etc/Hostname um etwa 15 Zeichen enthalten.

- Führen Sie den Befehl nicht `ALTER SERVICE MASTER KEY REGENERATE`. Es ist ein bekanntes Problem, das SQL Server instabil bewirkt. Wenn Sie mit dem Diensthauptschlüssel neu generieren müssen, sollten Sie sichern Sie die Datenbankdateien deinstallieren und erneut installieren von SQL Server, und stellen Sie die Datenbankdateien wieder her.

- Die Systemzeit manuell Abwärtskompatibilität zeitlich festlegen führt dazu, dass SQL Server nicht mehr aktualisiert die interne Systemzeit innerhalb von SQL Server.

    - **Auflösung**: SQLServer neu starten.

- Einige Namen Zeitzone in Linux zuordnen nicht genau die Namen der Windows-Zeitzonen.

    - **Auflösung**: Verwenden Sie die Zeitzone Namen aus TZID-Spalte in der ' Zuordnung für: 'Windows-Section-Tabelle auf die [Unicode.org Dokumentationsseite](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- SQL Server-Datenbankmodul erwartet, dass Zeilen in Textdateien mit CR-LF (Windows-Stil Zeile Formatierung) beendet werden soll.

- Nur die Einzelinstanz-Installationen werden unterstützt.

    - **Auflösung**: Wenn Sie mehrere Instanzen auf einem angegebenen Host verwenden möchten, erwägen Sie VMs oder Docker-Containern. 

- Alle Protokolldateien und Fehlerprotokolle in UTF-16 codiert sind.

- SQL Server-Konfigurations-Manager Verbindung keine mit SQL Server on Linux.

- **CREATE ASSEMBLY** funktioniert nicht bei dem Versuch, eine Datei zu verwenden. Verwenden der **FROM \<Bits\> ** Methode stattdessen vorläufig. 

#### <a name="databases"></a>Datenbanken
- Ändern die Speicherorte der Daten- und Protokolldateien TempDB-Dateien wird nicht unterstützt.

- Systemdatenbanken können nicht mit dem Hilfsprogramm Mssql-Conf verschoben werden.

- Beim Wiederherstellen einer Datenbank, die auf SQL Server on Windows gesichert wurde, müssen Sie verwenden die **WITH MOVE** -Klausel in Transact-SQL-Anweisung.

- Heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht auf SQL Server unter Linux unterstützt. SQL Server mit SQL Server, die verteilte Transaktionen unterstützt werden.

- AlwaysOn-Verfügbarkeitsgruppen unter Linux müssen gelegentlich Datenverlust werden, wenn Replikate befinden sich im synchronen Commit-Modus. Finden Sie unter 
 
   - [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   - [SLES](sql-server-linux-availability-group-cluster-sles.md)
   - [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   
#### <a name="full-text-search"></a>Volltextsuche
- Nicht alle Filter sind in dieser Version, z. B. Filter für Office-Dokumente verfügbar. Eine Liste der unterstützten Filter, finden Sie unter [installieren Sie SQL Server-Volltextsuche unter Linux](sql-server-linux-setup-full-text-search.md#filters).

- Die koreanische wörtertrennung benötigt einige Sekunden zum Laden und generiert einen Fehler bei der erstmaligen Verwendung. Nach diesem ersten Fehler sollte es ordnungsgemäß funktionieren.

#### <a name="in-memory-oltp"></a>In-Memory OLTP
- In-Memory OLTP-Datenbanken können nur im Verzeichnis /var/opt/mssql erstellt werden. Weitere Informationen finden Sie auf der [In-Memory-OLTP-Thema](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Mithilfe des SqlPackage muss einen absoluten Pfad für Dateien angegeben werden. Verwenden relative Pfade ordnet die Dateien unter der "/tmp/sqlpackage./ <code/> /System/system32" Ordner. 

    - **Auflösung**: absolute Pfade verwenden.

- SqlPackage zeigt den Speicherort der Dateien mit einer "" c: "\\" Präfix.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP & ODBC 
- SQL Server-Befehlszeile tools (Mssql-Tools), und der ODBC-Treiber (Msodbcsql) hängt von einer benutzerdefinierten UnixODBC-Treiber-Manager. Dies bewirkt, dass Konflikte, wenn Sie einen zuvor installierten UnixODBC Treiber-Manager haben. 

    - **Auflösung**: auf Ubuntu, der Konflikt wird automatisch aufgelöst. Bei der Frage, ob Sie den vorhandenen UnixODBC-Treiber-Manager deinstallieren möchten, geben Sie "y", und setzen Sie die Installation fort. Auf RedHat, müssen Sie zum manuellen Entfernen der vorhandenen UnixODBC Treiber-Manager mit `yum remove unixODBC`. Wir muss arbeiten Korrektur dieser Beschränkung für RHEL und SUSE und ein Update für Sie bald.  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Die folgenden Einschränkungen gelten für SSMS unter Windows, die mit SQL Server on Linux verbunden.

- Ausführen von Wartungsplänen werden nicht unterstützt.

- Management Data Warehouse (MDW) und der Datensammler in SSMS wird nicht unterstützt. 

- SSMS-UI-Komponenten, die Windows-Authentifizierung oder Windows-Ereignisprotokoll-Optionen verfügen funktionieren nicht mit Linux. Sie können diese Funktionen weiterhin mit anderen Optionen, z. B. SQL-Anmeldenamen verwenden. 

- Der SQL Server-Agent ist noch nicht unterstützt. Aus diesem Grund funktioniert SQL Server-Agent-Funktionalität in SSMS unter Linux im Moment nicht.

- Die Dateibrowser ist beschränkt auf die "" c: "\\" Gültigkeitsbereich auflöst/Var/opt/Mssql/unter Linux. Um andere Pfade verwenden zu können, Generieren von Skripts, der den UI-Vorgang aus, und Ersetzen Sie die "c:"\\ Pfade mit Linux-Pfaden. Führen Sie das Skript dann manuell in SSMS.

- Anzahl der Protokolldateien beibehalten werden sollen, nicht geändert werden.

### <a name="next-steps"></a>Nächste Schritte

Um zu beginnen, finden Sie unter den folgenden Schnellstart-Lernprogrammen:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Trennung Leiste-Grafik](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp12-ctp-12-january-2017"></a><a id="ctp12">CTP-Version 1.2 (Januar 2017)
Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.200.24.

### <a name="supported-platforms"></a>Unterstützte Plattformen 

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Installationshandbuch](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS und 16.10 | EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Sie benötigen mindestens 3,25 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
> SQL Server-Datenbankmodul wurde nur bis zu 256GB Arbeitsspeicher zu diesem Zeitpunkt getestet.

### <a name="package-details"></a>Details zum Paket
Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Beachten Sie, dass Sie nicht benötigen, um diese herunterzuladen Pakete direkt auf, wenn Sie die Schritte im Verwenden der [Installationshandbüchern](sql-server-linux-setup.md).

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| RPM-Paket | 14.0.200.24-2 | [MSSQL Server 14.0.200.24-2-Engine-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.200.24-2.x86_64.rpm)</br>[MSSQL Server 14.0.200.24-2 hohe Verfügbarkeit-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.200.24-2.x86_64.rpm) | 
| Debian-Paket | 14.0.200.24-2 | [MSSQL Server 14.0.200.24-2 Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.200.24-2_amd64.deb) |

### <a name="supported-client-tools"></a>Unterstützte-Clienttools

| Tool | Mindestversion |
|-----|-----|
| [SQL Server Management Studio (SSMS) für Windows - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools für Visual Studio - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Visual Studio-Code](https://code.visualstudio.com) mit der [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) | Neueste (0,2) |

> [!NOTE] 
> Die angegebenen Versionen von SQL Server Management Studio und SQL Server Data Tools sind höher Release Candidates, daher für die Verwendung in der Produktion nicht empfohlen.

### <a name="unsupported-features-and-services"></a>Nicht unterstützte Funktionen und Dienste
Die folgenden Features und Dienste sind zu diesem Zeitpunkt nicht verfügbar unter Linux. Die Unterstützung dieser Funktionen wird immer während der monatlichen Updates Rhythmus der Preview-Programm aktiviert werden.

| Bereich | Nicht unterstützte Funktion oder ein Dienst |
|-----|-----|
| **Datenbankmodul** | Volltextsuche |
| &nbsp; | Replikation |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Verteilte Abfrage |
| &nbsp; | Erweiterte gespeicherte Systemprozeduren (XP_CMDSHELL, usw.). |
| &nbsp; | Filetable |
| &nbsp; | Legen Sie die CLR-Assemblys mit der EXTERNAL_ACCESS oder UNSAFE-Berechtigung |
| **High Availability (Hohe Verfügbarkeit)** | AlwaysOn-Verfügbarkeitsgruppen |
| &nbsp; | Datenbankspiegelung  |
| **Sicherheit** | Active Directory-Authentifizierung |
| &nbsp; | Windows-Authentifizierung |
| &nbsp; | Erweiterbare Schlüsselverwaltung |
| &nbsp; | Verwendung von vom Benutzer bereitgestellte Zertifikat für SSL oder TLS |
| **Dienste** | SQL Server-Agent |
| &nbsp; | SQL Server-Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Bekannte Probleme
In den folgenden Abschnitten werden bekannte Probleme mit dieser Version von SQL Server 2017 CTP-Version 1.2 auf Linux beschrieben.

#### <a name="general"></a>Allgemein
- Die Länge des Hostnamens, auf dem SQL Server muss installiert sein, mit 15 Zeichen oder weniger ist. 

    - **Auflösung**: Ändern Sie den Namen in/Etc/Hostname um etwa 15 Zeichen enthalten.

- Führen Sie den Befehl nicht `ALTER SERVICE MASTER KEY REGENERATE`. Es ist ein bekanntes Problem, das SQL Server instabil bewirkt. Wenn Sie mit dem Diensthauptschlüssel neu generieren müssen, sollten Sie sichern Sie die Datenbankdateien deinstallieren und erneut installieren von SQL Server, und stellen Sie die Datenbankdateien wieder her.

- Der Ressourcenname für SQL-Ressource von Ocf:sql:fci in Ocf:mssql:fci geändert. Weitere Informationen zur Konfiguration eines Failoverclusters in einem freigegebenen Datenträger Sie finden [hier](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-shared-disk-cluster-red-hat-7-configure).

- Die Systemzeit manuell Abwärtskompatibilität zeitlich festlegen führt dazu, dass SQL Server nicht mehr aktualisiert die interne Systemzeit innerhalb von SQL Server.

    - **Auflösung**: SQLServer neu starten.

- Einige Namen Zeitzone in Linux zuordnen nicht genau die Namen der Windows-Zeitzonen.

    - **Auflösung**: Verwenden Sie die Zeitzone Namen aus TZID-Spalte in der ' Zuordnung für: 'Windows-Section-Tabelle auf die [Unicode.org Dokumentationsseite](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- SQL Server-Datenbankmodul erwartet, dass Zeilen in Textdateien mit CR-LF (Windows-Stil Zeile Formatierung) beendet werden soll.

- Nur die Einzelinstanz-Installationen werden unterstützt.

    - **Auflösung**: Wenn Sie mehrere Instanzen auf einem angegebenen Host verwenden möchten, erwägen Sie VMs oder Docker-Containern. 

- Alle Protokolldateien und Fehlerprotokolle in UTF-16 codiert sind.

- SQL Server-Konfigurations-Manager Verbindung keine mit SQL Server on Linux.

- **CREATE ASSEMBLY** funktioniert nicht bei dem Versuch, eine Datei zu verwenden. Verwenden der **FROM \<Bits\> ** Methode stattdessen vorläufig. 

#### <a name="databases"></a>Datenbanken
- Ändern die Speicherorte der Daten- und Protokolldateien TempDB-Dateien wird nicht unterstützt.

- Systemdatenbanken können nicht mit dem Hilfsprogramm Mssql-Conf verschoben werden.

- Beim Wiederherstellen einer Datenbank, die auf SQL Server on Windows gesichert wurde, müssen Sie verwenden die **WITH MOVE** -Klausel in Transact-SQL-Anweisung.

- Heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht auf SQL Server unter Linux unterstützt. SQL Server mit SQL Server, die verteilte Transaktionen unterstützt werden.

#### <a name="in-memory-oltp"></a>In-Memory OLTP
- In-Memory OLTP-Datenbanken können nur im Verzeichnis /var/opt/mssql erstellt werden. Diese Datenbanken benötigen auch die "" c: "\\" Notation beim bezeichnet. Weitere Informationen finden Sie auf der [In-Memory-OLTP-Thema](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Mithilfe des SqlPackage muss einen absoluten Pfad für Dateien angegeben werden. Verwenden relative Pfade werden Dateien unter "/ Tmp /-Sqlpackage. zugeordnet. \<Code \> /System/system32 "Ordner. 

    - **Auflösung**: absolute Pfade verwenden.

- SqlPackage zeigt den Speicherort der Dateien mit einer "" c: "\\" Präfix.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP & ODBC 
- Wenn Sie eine ältere Version von SQL Server-Befehlszeilentools (Mssql-Tools) und der ODBC-Treiber (Msodbcsql) haben, können Sie eine benutzerdefinierte UnixODBC Treiber-Manager (UnixODBC-UTF16-Format) installiert haben. Dies kann möglicherweise Konflikte verursachen, wie wir einen benutzerdefiniertes Treiber-Manager nicht mehr verwenden. 

    - **Auflösung**: auf Ubuntu und SLES der Konflikt wird automatisch aufgelöst. Bei der Frage, ob Sie den vorhandenen UnixODBC-Treiber-Manager deinstallieren möchten, geben Sie "y", und setzen Sie die Installation fort. Auf RedHat, müssen Sie zum manuellen Entfernen der vorhandenen UnixODBC Treiber-Manager mit `yum remove unixODBC-utf16 unixODBC-utf16-devel` , und wiederholen Sie die Installation.
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Die folgenden Einschränkungen gelten für SSMS unter Windows, die mit SQL Server on Linux verbunden.

- Ausführen von Wartungsplänen werden nicht unterstützt.

- Management Data Warehouse (MDW) und der Datensammler in SSMS wird nicht unterstützt. 

- SSMS-UI-Komponenten, die Windows-Authentifizierung oder Windows-Ereignisprotokoll-Optionen verfügen funktionieren nicht mit Linux. Sie können diese Funktionen weiterhin mit anderen Optionen, z. B. SQL-Anmeldenamen verwenden. 

- Der SQL Server-Agent ist noch nicht unterstützt. Aus diesem Grund funktioniert SQL Server-Agent-Funktionalität in SSMS unter Linux im Moment nicht.

- Die Dateibrowser ist beschränkt auf die "" c: "\\" Gültigkeitsbereich auflöst/Var/opt/Mssql/unter Linux. Um andere Pfade verwenden zu können, Generieren von Skripts, der den UI-Vorgang aus, und Ersetzen Sie die "c:"\\ Pfade mit Linux-Pfaden. Führen Sie das Skript dann manuell in SSMS.

### <a name="next-steps"></a>Nächste Schritte

Um zu beginnen, finden Sie unter den folgenden Schnellstart-Lernprogrammen:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Trennung Leiste-Grafik](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp11-ctp-11-december-2016"></a><a id="ctp11">CTP-Version 1.1 (Dezember 2016)
Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.100.187.

### <a name="supported-platforms"></a>Unterstützte Plattformen 

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux-Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| Ubuntu 16.04LTS und 16.10 | EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Sie benötigen mindestens 3,25 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
> SQL Server-Datenbankmodul wurde nur bis zu 256GB Arbeitsspeicher zu diesem Zeitpunkt getestet.

### <a name="package-details"></a>Details zum Paket
Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Beachten Sie, dass Sie nicht benötigen, um diese herunterzuladen Pakete direkt auf, wenn Sie die Schritte im Verwenden der [Installationshandbüchern](sql-server-linux-setup.md).

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| RPM-Paket | 14.0.100.187-1 | [MSSQL Server 14.0.100.187-1-Engine-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.100.187-1.x86_64.rpm)</br>[MSSQL Server 14.0.100.187-1 hohe Verfügbarkeit-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.100.187-1.x86_64.rpm) | 
| Debian-Paket | 14.0.100.187-1 | [MSSQL Server 14.0.100.187-1 Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.100.187-1_amd64.deb) |

### <a name="supported-client-tools"></a>Unterstützte-Clienttools

| Tool | Mindestversion |
|-----|-----|
| [SQL Server Management Studio (SSMS) für Windows - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools für Visual Studio - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Visual Studio-Code](https://code.visualstudio.com) mit der [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) | Neueste (0,2) |

> [!NOTE] 
> Die angegebenen Versionen von SQL Server Management Studio und SQL Server Data Tools sind höher Release Candidates, daher für die Verwendung in der Produktion nicht empfohlen.

### <a name="unsupported-features-and-services"></a>Nicht unterstützte Funktionen und Dienste
Die folgenden Features und Dienste sind zu diesem Zeitpunkt nicht verfügbar unter Linux. Die Unterstützung dieser Funktionen wird immer während der monatlichen Updates Rhythmus der Preview-Programm aktiviert werden.

| Bereich | Nicht unterstützte Funktion oder ein Dienst |
|-----|-----|
| **Datenbankmodul** | Volltextsuche |
| &nbsp; | Replikation |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Verteilte Abfrage |
| &nbsp; | Erweiterte gespeicherte Systemprozeduren (XP_CMDSHELL, usw.). |
| &nbsp; | Filetable |
| &nbsp; | Legen Sie die CLR-Assemblys mit der EXTERNAL_ACCESS oder UNSAFE-Berechtigung |
| **High Availability (Hohe Verfügbarkeit)** | AlwaysOn-Verfügbarkeitsgruppen |
| &nbsp; | Datenbankspiegelung  |
| **Sicherheit** | Active Directory-Authentifizierung |
| &nbsp; | Windows-Authentifizierung |
| &nbsp; | Erweiterbare Schlüsselverwaltung |
| &nbsp; | Verwendung von vom Benutzer bereitgestellte Zertifikat für SSL oder TLS |
| **Dienste** | SQL Server-Agent |
| &nbsp; | SQL Server-Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Bekannte Probleme
In den folgenden Abschnitten werden bekannte Probleme mit dieser Version von SQL Server 2017 CTP-Version 1.1 auf Linux beschrieben.

#### <a name="general"></a>Allgemein
- Die Länge des Hostnamens, auf dem SQL Server muss installiert sein, mit 15 Zeichen oder weniger ist. 

    - **Auflösung**: Ändern Sie den Namen in/Etc/Hostname um etwa 15 Zeichen enthalten.

- Führen Sie den Befehl nicht `ALTER SERVICE MASTER KEY REGENERATE`. Es ist ein bekanntes Problem, das SQL Server instabil bewirkt. Wenn Sie mit dem Diensthauptschlüssel neu generieren müssen, sollten Sie sichern Sie die Datenbankdateien deinstallieren und erneut installieren von SQL Server, und stellen Sie die Datenbankdateien wieder her.

- Der Ressourcenname für SQL-Ressource von Ocf:sql:fci in Ocf:mssql:fci geändert. Weitere Informationen zur Konfiguration eines Failoverclusters in einem freigegebenen Datenträger Sie finden [hier](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-shared-disk-cluster-red-hat-7-configure).

- Die Systemzeit manuell Abwärtskompatibilität zeitlich festlegen führt dazu, dass SQL Server nicht mehr aktualisiert die interne Systemzeit innerhalb von SQL Server.

    - **Auflösung**: SQLServer neu starten.

- Einige Namen Zeitzone in Linux zuordnen nicht genau die Namen der Windows-Zeitzonen.

    - **Auflösung**: Verwenden Sie die Zeitzone Namen aus TZID-Spalte in der ' Zuordnung für: 'Windows-Section-Tabelle auf die [Unicode.org Dokumentationsseite](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- SQL Server-Datenbankmodul erwartet, dass Zeilen in Textdateien mit CR-LF (Windows-Stil Zeile Formatierung) beendet werden soll.

- Nur die Einzelinstanz-Installationen werden unterstützt.

    - **Auflösung**: Wenn Sie mehrere Instanzen auf einem angegebenen Host verwenden möchten, erwägen Sie VMs oder Docker-Containern. 

- Alle Protokolldateien und Fehlerprotokolle in UTF-16 codiert sind.

- SQL Server-Konfigurations-Manager Verbindung keine mit SQL Server on Linux.

- **CREATE ASSEMBLY** funktioniert nicht bei dem Versuch, eine Datei zu verwenden. Verwenden der **FROM \<Bits\> ** Methode stattdessen vorläufig. 

#### <a name="databases"></a>Datenbanken
- Ändern die Speicherorte der Daten- und Protokolldateien TempDB-Dateien wird nicht unterstützt.

- Systemdatenbanken können nicht mit dem Hilfsprogramm Mssql-Conf verschoben werden.

- Beim Wiederherstellen einer Datenbank, die auf SQL Server on Windows gesichert wurde, müssen Sie verwenden die **WITH MOVE** -Klausel in Transact-SQL-Anweisung.

- Heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht auf SQL Server unter Linux unterstützt. SQL Server mit SQL Server, die verteilte Transaktionen unterstützt werden.

#### <a name="in-memory-oltp"></a>In-Memory OLTP
- In-Memory OLTP-Datenbanken können nur im Verzeichnis /var/opt/mssql erstellt werden. Diese Datenbanken benötigen auch die "" c: "\" Notation beim bezeichnet. Weitere Informationen finden Sie auf der [In-Memory-OLTP-Thema](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Mithilfe des SqlPackage muss einen absoluten Pfad für Dateien angegeben werden. Verwenden relative Pfade werden Dateien unter "/ Tmp /-Sqlpackage. zugeordnet. \<Code \> /System/system32 "Ordner. 

    - **Auflösung**: absolute Pfade verwenden.

- SqlPackage zeigt den Speicherort der Dateien mit einer "" c: "\\" Präfix.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP & ODBC 
- SQL Server-Befehlszeile tools (Mssql-Tools), und der ODBC-Treiber (Msodbcsql) hängt von einer benutzerdefinierten UnixODBC-Treiber-Manager. Dies bewirkt, dass Konflikte, wenn Sie einen zuvor installierten UnixODBC Treiber-Manager haben. 

    - **Auflösung**: auf Ubuntu, der Konflikt wird automatisch aufgelöst. Bei der Frage, ob Sie den vorhandenen UnixODBC-Treiber-Manager deinstallieren möchten, geben Sie "y", und setzen Sie die Installation fort. Auf RedHat, müssen Sie zum manuellen Entfernen der vorhandenen UnixODBC Treiber-Manager mit `yum remove unixODBC`. Wir muss arbeiten Korrektur dieser Beschränkung für RHEL und SUSE und ein Update für Sie bald.  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Die folgenden Einschränkungen gelten für SSMS unter Windows, die mit SQL Server on Linux verbunden.

- Ausführen von Wartungsplänen werden nicht unterstützt.

- Management Data Warehouse (MDW) und der Datensammler in SSMS wird nicht unterstützt. 

- SSMS-UI-Komponenten, die Windows-Authentifizierung oder Windows-Ereignisprotokoll-Optionen verfügen funktionieren nicht mit Linux. Sie können diese Funktionen weiterhin mit anderen Optionen, z. B. SQL-Anmeldenamen verwenden. 

- Der SQL Server-Agent ist noch nicht unterstützt. Aus diesem Grund funktioniert SQL Server-Agent-Funktionalität in SSMS unter Linux im Moment nicht.

- Die Dateibrowser ist beschränkt auf die "" c: "\\" Gültigkeitsbereich auflöst/Var/opt/Mssql/unter Linux. Um andere Pfade verwenden zu können, Generieren von Skripts, der den UI-Vorgang aus, und Ersetzen Sie die "c:"\\ Pfade mit Linux-Pfaden. Führen Sie das Skript dann manuell in SSMS.

v

![Trennung Leiste-Grafik](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp10-ctp-10-november-2016"></a><a id="ctp10">CTP 1.0 (November 2016)
Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.1.246.

### <a name="supported-platforms"></a>Unterstützte Plattformen 

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.2 Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| Ubuntu 16.04LTS | EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Sie benötigen mindestens 3,25 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
> SQL Server-Datenbankmodul wurde nur bis zu 256GB Arbeitsspeicher zu diesem Zeitpunkt getestet.

### <a name="package-details"></a>Details zum Paket
Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Beachten Sie, dass Sie nicht benötigen, um diese herunterzuladen Pakete direkt auf, wenn Sie die Schritte im Verwenden der [Installationshandbüchern](sql-server-linux-setup.md).

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| RPM-Paket | 14.0.1.246-6 | [MSSQL Server 14.0.1.246-6-Engine-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.1.246-6.x86_64.rpm)</br>[MSSQL Server 14.0.1.246-6 hohe Verfügbarkeit-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.1.246-6.x86_64.rpm) | 
| Debian-Paket | 14.0.1.246-6 | [MSSQL Server 14.0.1.246-6 Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.1.246-6_amd64.deb) |

### <a name="supported-client-tools"></a>Unterstützte-Clienttools

| Tool | Mindestversion |
|-----|-----|
| [SQL Server Management Studio (SSMS) für Windows - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools für Visual Studio - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Visual Studio-Code](https://code.visualstudio.com) mit der [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) | Neueste (0.1.5) |

> [!NOTE] 
> Die angegebenen Versionen von SQL Server Management Studio und SQL Server Data Tools sind höher Release Candidates, daher für die Verwendung in der Produktion nicht empfohlen.

### <a name="unsupported-features-and-services"></a>Nicht unterstützte Funktionen und Dienste
Die folgenden Features und Dienste sind zu diesem Zeitpunkt nicht verfügbar unter Linux. Die Unterstützung dieser Funktionen wird immer während der monatlichen Updates Rhythmus der Preview-Programm aktiviert werden.

| Bereich | Nicht unterstützte Funktion oder ein Dienst |
|-----|-----|
| **Datenbankmodul** | Volltextsuche |
| &nbsp; | Replikation |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Verteilte Abfrage |
| &nbsp; | Erweiterte gespeicherte Systemprozeduren (XP_CMDSHELL, usw.). |
| &nbsp; | Filetable |
| &nbsp; | Legen Sie die CLR-Assemblys mit der EXTERNAL_ACCESS oder UNSAFE-Berechtigung |
| **High Availability (Hohe Verfügbarkeit)** | AlwaysOn-Verfügbarkeitsgruppen |
| &nbsp; | Datenbankspiegelung  |
| **Sicherheit** | Active Directory-Authentifizierung |
| &nbsp; | Windows-Authentifizierung |
| &nbsp; | Erweiterbare Schlüsselverwaltung |
| &nbsp; | Verwendung von vom Benutzer bereitgestellte Zertifikat für SSL oder TLS |
| **Dienste** | SQL Server-Agent |
| &nbsp; | SQL Server-Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Bekannte Probleme
In den folgenden Abschnitten werden bekannte Probleme mit dieser Version von SQL Server 2017 CTP1 unter Linux beschrieben.

#### <a name="general"></a>Allgemein
- Die Länge des Hostnamens, auf dem SQL Server muss installiert sein, mit 15 Zeichen oder weniger ist. 

    - **Auflösung**: Ändern Sie den Namen in/Etc/Hostname um etwa 15 Zeichen enthalten.

- Die Systemzeit manuell Abwärtskompatibilität zeitlich festlegen führt dazu, dass SQL Server nicht mehr aktualisiert die interne Systemzeit innerhalb von SQL Server.

    - **Auflösung**: SQLServer neu starten.

- Einige Namen Zeitzone in Linux zuordnen nicht genau die Namen der Windows-Zeitzonen.

    - **Auflösung**: Verwenden Sie die Zeitzone Namen aus TZID-Spalte in der ' Zuordnung für: 'Windows-Section-Tabelle auf die [Unicode.org Dokumentationsseite](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- SQL Server-Datenbankmodul erwartet, dass Zeilen in Textdateien mit CR-LF (Windows-Stil Zeile Formatierung) beendet werden soll.

- Nur die Einzelinstanz-Installationen werden unterstützt.

    - **Auflösung**: Wenn Sie mehrere Instanzen auf einem angegebenen Host verwenden möchten, erwägen Sie VMs oder Docker-Containern. 

- Alle Protokolldateien und Fehlerprotokolle in UTF-16 codiert sind.

- SQL Server-Konfigurations-Manager Verbindung keine mit SQL Server on Linux.

- **CREATE ASSEMBLY** funktioniert nicht bei dem Versuch, eine Datei zu verwenden. Verwenden der **FROM \<Bits\> ** Methode stattdessen vorläufig.

#### <a name="databases"></a>Datenbanken
- Ändern die Speicherorte der Daten- und Protokolldateien TempDB-Dateien wird nicht unterstützt.

- Systemdatenbanken können nicht mit dem Hilfsprogramm Mssql-Conf verschoben werden.

- Beim Wiederherstellen einer Datenbank, die auf SQL Server on Windows gesichert wurde, müssen Sie verwenden die **WITH MOVE** -Klausel in Transact-SQL-Anweisung.

- Heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht auf SQL Server unter Linux unterstützt. SQL Server mit SQL Server, die verteilte Transaktionen unterstützt werden.

#### <a name="in-memory-oltp"></a>In-Memory OLTP
- In-Memory OLTP-Datenbanken können nur im Verzeichnis /var/opt/mssql erstellt werden. Diese Datenbanken benötigen auch die "" c: "\\" Notation beim bezeichnet. Weitere Informationen finden Sie auf der [In-Memory-OLTP-Thema](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Mithilfe des SqlPackage erfordert, um einen absoluten Pfad für die Dateien anzugeben. Verwenden relative Pfade werden Dateien unter "/ Tmp /-Sqlpackage. zugeordnet. \<Code \> /System/system32 "Ordner. 

    - **Auflösung**: absolute Pfade verwenden.

- SqlPackage zeigt den Speicherort der Dateien mit einer "" c: "\\" Präfix.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP & ODBC 
- SQL Server-Befehlszeile tools (Mssql-Tools), und der ODBC-Treiber (Msodbcsql) hängt von einer benutzerdefinierten UnixODBC-Treiber-Manager. Dies bewirkt, dass Konflikte, wenn Sie einen zuvor installierten UnixODBC Treiber-Manager haben. 

    - **Auflösung**: auf Ubuntu, der Konflikt wird automatisch aufgelöst. Bei der Frage, ob Sie den vorhandenen UnixODBC-Treiber-Manager deinstallieren möchten, geben Sie "y", und setzen Sie die Installation fort. Auf RedHat, müssen Sie zum manuellen Entfernen der vorhandenen UnixODBC Treiber-Manager mit `yum remove unixODBC`. Wir muss arbeiten Korrektur dieser Beschränkung für RHEL und SUSE und ein Update für Sie bald.  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Die folgenden Einschränkungen gelten für SSMS unter Windows, die mit SQL Server on Linux verbunden.

- Ausführen von Wartungsplänen werden nicht unterstützt.

- Management Data Warehouse (MDW) und der Datensammler in SSMS wird nicht unterstützt. 

- SSMS-UI-Komponenten, die Windows-Authentifizierung oder Windows-Ereignisprotokoll-Optionen verfügen funktionieren nicht mit Linux. Sie können diese Funktionen weiterhin mit anderen Optionen, z. B. SQL-Anmeldenamen verwenden. 

- Der SQL Server-Agent ist noch nicht unterstützt. Aus diesem Grund funktioniert SQL Server-Agent-Funktionalität in SSMS unter Linux im Moment nicht.

- Die Dateibrowser ist beschränkt auf die "" c: "\\" Gültigkeitsbereich auflöst/Var/opt/Mssql/unter Linux. Um andere Pfade verwenden zu können, Generieren von Skripts, der den UI-Vorgang aus, und Ersetzen Sie die "c:"\\ Pfade mit Linux-Pfaden. Führen Sie das Skript dann manuell in SSMS.

### <a name="next-steps"></a>Nächste Schritte

Um zu beginnen, finden Sie unter den folgenden Schnellstart-Lernprogrammen:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

