---
title: "Versionshinweise für SQL Server-2017 unter Linux | Microsoft Docs"
description: "Dieser Artikel enthält die Versionshinweise und Funktionen für SQL Server-2017 unter Linux unterstützt. Anmerkungen zu dieser Version sind für die aktuelle Version und früheren Releases enthalten."
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
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.workload: Active
ms.openlocfilehash: a661da062d65ca699627bc2b5bf0683e5fe08806
ms.sourcegitcommit: 7e9380e53341755df13fce130ab3287918a8e44c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Versionshinweise für SQL Server-2017 unter Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Die folgenden Anmerkungen gelten für SQL Server-2017 auf Linux ausgeführt wird. In diesem Artikel wird für jede Version in Abschnitte aufgeteilt. Die GA-Version wurde detaillierten hinsichtlich der unterstützbarkeit und bekannte Probleme aufgeführt werden. Jede Version des kumulativen Update (CU) ist ein Link zu einer Support-Artikel beschreiben die CU Änderungen sowie Links zu den Linux-Paket heruntergeladen.

## <a name="supported-platforms"></a>Unterstützte Plattformen

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 oder 7.4 Arbeitsstation, Server- und Desktopgeräte | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Modul 1.8 + unter Windows, Mac und Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!TIP]
> Weitere Informationen finden Sie in der [Systemanforderungen](sql-server-linux-setup.md#system) für SQL Server on Linux. Die neuesten Supportrichtlinie für SQL Server-2017, finden Sie unter der [technischen Support-Richtlinie für Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="supported-client-tools"></a>Unterstützte-Clienttools

| Tool | Mindestversion |
|-----|-----|
| [SQL Server Management Studio (SSMS) für Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools für Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio-Code](https://code.visualstudio.com) mit der [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) | neueste |

## <a name="release-history"></a>Revisionsverlauf

In der folgenden Tabelle werden die Revisionsverlauf für SQL Server-2017 aufgelistet.

| Release | Version | Veröffentlichungsdatum |
|-----|-----|-----|
| [CU4](#CU4) | 14.0.3022.28 | 2-2018 |
| [CU3](#CU3) | 14.0.3015.40 | 1-2018 |
| [CU2](#CU2) | 14.0.3008.27 | 11-2017 |
| [CU1](#CU1) | 14.0.3006.16 | 10-2017 |
| [GA](#GA) | 14.0.1000.169 | 10-2017 |

## <a id="cuinstall"></a> Installieren von kumulativen updates

Wenn Sie das kumulative Update Repository konfiguriert haben, erhalten Sie das neueste kumulative Update von SQL Server-Paketen beim Ausführen von Neuinstallationen. Das kumulative Update-Repository ist die Standardeinstellung für alle Artikel der Paket-Installation für SQL Server on Linux. Weitere Informationen zum Repository-Konfiguration finden Sie unter [konfigurieren Repositorys für SQL Server on Linux](sql-server-linux-change-repo.md).

Wenn Sie vorhandene SQL Server-Pakete aktualisieren, führen Sie das entsprechende Update-Befehl für jedes Paket, das neueste kumulative Update zu erhalten. Bestimmte Update-Anweisungen für jedes Paket finden Sie unter den folgenden Handbüchern zur Installation:

- [Installieren Sie SQL Server-Paket](sql-server-linux-setup.md#upgrade)
- [Volltext-Suchdienst-Paket installieren](sql-server-linux-setup-full-text-search.md)
- [Install SQL Server Integration Services (Installieren von SQL Server Integration Services)](sql-server-linux-setup-ssis.md)
- [Aktivieren Sie SQL Server-Agent](sql-server-linux-setup-sql-agent.md)

## <a id="CU4"></a> CU4 (Februar 2018)

Dies ist der kumulativen Update 4 (CU4)-Version von SQL Server-2017. Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.3022.28. Informationen zu den Korrekturen und Verbesserungen in dieser Version finden Sie unter [https://support.microsoft.com/en-us/help/4056498](https://support.microsoft.com/en-us/help/4056498).

### <a name="package-details"></a>Details zum Paket

Für Paketinstallationen der manuellen oder offline-können Sie die RPM und Debian Pakete mit den Informationen in der folgenden Tabelle herunterladen:

> [!NOTE]
> Zum Zeitpunkt der CU4 wird SQL Server-Agent nicht mehr als ein separates Paket installiert. Er ist mit dem Datenbankmodul-Paket installiert und muss aktiviert werden, um verwenden.

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.3022.28-2 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.3022.28-2 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.3022.28-2 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU3"></a> CU3 (Januar 2018)

Dies ist das kumulative Update 3 (CU3)-Version von SQL Server-2017. Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.3015.40. Informationen zu den Korrekturen und Verbesserungen in dieser Version finden Sie unter [https://support.microsoft.com/en-us/help/4052987](https://support.microsoft.com/en-us/help/4052987).

### <a name="package-details"></a>Details zum Paket

Für Paketinstallationen der manuellen oder offline-können Sie die RPM und Debian Pakete mit den Informationen in der folgenden Tabelle herunterladen:

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.3015.40-1 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.3015.40-1 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.3015.40-1 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (November 2017)

Dies ist das kumulative Update 2 (CU2)-Version von SQL Server-2017. Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.3008.27. Informationen zu den Korrekturen und Verbesserungen in dieser Version finden Sie unter [https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574).

### <a name="package-details"></a>Details zum Paket

Für Paketinstallationen der manuellen oder offline-können Sie die RPM und Debian Pakete mit den Informationen in der folgenden Tabelle herunterladen:

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.3008.27-1 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.3008.27-1 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.3008.27-1 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (Oktober 2017)

Dies ist das kumulative Update 1 (CU1)-Version von SQL Server-2017. Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.3006.16. Informationen zu den Korrekturen und Verbesserungen in dieser Version finden Sie unter [https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634).

### <a name="package-details"></a>Details zum Paket

Für Paketinstallationen der manuellen oder offline-können Sie die RPM und Debian Pakete mit den Informationen in der folgenden Tabelle herunterladen:

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.3006.16-3 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.3006.16-3 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.3006.16-3 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA (Oktober 2017)

Dies ist der allgemeinen Verfügbarkeit (GA)-Version von SQL Server-2017. Die Version des SQL Server-Datenbankmodul für diese Version ist 14.0.1000.169.

### <a name="package-details"></a>Details zum Paket

Details zum Paket und downloadpfaden für die RPM und Debian Pakete werden in der folgenden Tabelle aufgeführt. Beachten Sie, dass Sie nicht benötigen, um diese Pakete direkt herunterzuladen, wenn Sie die Schritte in den folgenden Handbüchern zur Installation verwenden:

- [Installieren Sie SQL Server-Paket](sql-server-linux-setup.md)
- [Volltext-Suchdienst-Paket installieren](sql-server-linux-setup-full-text-search.md)
- [Installieren von SQL Server-Agent-Paket](sql-server-linux-setup-sql-agent.md)
- [Install SQL Server Integration Services (Installieren von SQL Server Integration Services)](sql-server-linux-setup-ssis.md)

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat-RPM-Paket | 14.0.1000.169-2 | [Datenbankmodul-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM-Paket | 14.0.1000.169-2 | [MSSQL-Server-Datenbankmodul-RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Hohe Verfügbarkeit RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Volltext-Suche RPM-Paket](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server-Agent-RPM-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket | 14.0.1000.169-2 | [Modul Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Hohe Verfügbarkeit Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Volltext-Suche Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Debian-Paket für SQL Server-Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> Nicht unterstützte Funktionen und Dienstleistungen

Die folgenden Features und Dienste sind zum Zeitpunkt der GA-Version nicht verfügbar unter Linux. Die Unterstützung dieser Funktionen wird mit der Zeit immer aktiviert.

| Bereich | Nicht unterstützte Funktion oder ein Dienst |
|-----|-----|
| **Datenbankmodul** | Transaktionsreplikation |
| &nbsp; | Mergereplikation |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Verteilte Abfragen mit 3rd Party Verbindungen |
| &nbsp; | Erweiterte gespeicherte Systemprozeduren (XP_CMDSHELL, usw.). |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | Legen Sie die CLR-Assemblys mit der EXTERNAL_ACCESS oder UNSAFE-Berechtigung |
| &nbsp; | Pufferpoolerweiterung |
| **SQL Server-Agent** |  Subsysteme: CmdExec, PowerShell, Warteschlangenleser, SSIS, SSAS, SSRS |
| &nbsp; | Warnungen |
| &nbsp; | Protokolllese-Agent |
| &nbsp; | Change Data Capture |
| &nbsp; | Verwaltete Sicherung |
| **High Availability (Hohe Verfügbarkeit)** | Datenbankspiegelung  |
| **Sicherheit** | Erweiterbare Schlüsselverwaltung |
| &nbsp; | AD-Authentifizierung für Verbindungsserver | 
| &nbsp; | AD-Authentifizierung für Verfügbarkeitsgruppen (Testreihen) | 
| &nbsp; | 3rd Party AD-Tools (Centrify Vintela, Powerbroker) | 
| **Dienste** | SQL Server-Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

## <a name="known-issues"></a>Bekannte Probleme

In den folgenden Abschnitten werden bekannte Probleme mit der allgemeinen Verfügbarkeit (GA)-Version von SQL Server-2017 unter Linux beschrieben.

#### <a name="general"></a>Allgemein

- Upgrades für die GA-Version von SQL Server-2017 werden nur von der CTP-Version 2.1 oder höher unterstützt. 

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

- Heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht auf SQL Server unter Linux unterstützt. SQL Server mit SQL Server verknüpfte Server unterstützt werden, es sei denn, sie DTC beinhalten. Weitere Informationen finden Sie unter [heraufstufbare Transaktionen, dass der Microsoft Distributed Transaction Coordinator-Dienst werden nicht unterstützt, auf SQL Server auf Linux laufende](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/).

- Bestimmte Algorithmen (Verschlüsselungssammlungen) for Transport Layer Security (TLS) funktionieren nicht ordnungsgemäß mit SQL Server on Linux. Dies führt zu Verbindungsfehlern, beim Versuch, eine Verbindung mit SQL Server als auch Probleme herstellen von Verbindungen zwischen den Replikaten in Gruppen mit hoher Verfügbarkeit.

   - **Auflösung**: Ändern der **mssql.conf** Konfigurationsskript für SQL Server on Linux problematisch Verschlüsselungssuites zu deaktivieren, indem Sie folgende Aktionen ausgeführt:

      1. Fügen Sie Folgendes hinzu /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Starten Sie SQL Server mit dem folgenden Befehl neu.

      ```bash
      sudo systemctl restart mssql-server
      ```

- SQL Server 2014-Datenbanken unter Windows, die In-Memory OLTP verwenden, können nicht auf SQL Server-2017 unter Linux wiederhergestellt werden. Zum Wiederherstellen einer SQL Server 2014-Datenbank, die in-Memory OLTP verwendet, zunächst ein upgrade der Datenbanken auf SQL Server 2016 oder 2017 von SQL Server unter Windows bevor sie in SQL Server on Linux verschoben, über sichern/wiederherstellen oder trennen/anfügen.

- Benutzerberechtigung **ADMINISTER BULK OPERATIONS** wird unter Linux zu diesem Zeitpunkt nicht unterstützt.

#### <a name="networking"></a>Netzwerk

Funktionen zur ausgehende TCP-Verbindungen von der Sqlservr-Prozess, z. B. auf Verbindungsservern oder Verfügbarkeitsgruppen, funktionieren möglicherweise nicht, wenn die beiden folgenden Bedingungen erfüllt sind:

1. Der Zielserver wird als einen Hostnamen und keine IP-Adresse angegeben.

1. Die Quellinstanz wurde deaktiviert, die im Kernel von IPv6. Um sicherzustellen, dass dem System IPv6 im Kernel-aktiviert sind, müssen die folgenden Tests übergeben:

   - `cat /proc/cmdline` Die Boot-Cmdline aktuelle Kernelversionen wird gedruckt werden. Die Ausgabe darf keinen `ipv6.disable=1`.
   - / Proc/Sys/net/ipv6/Verzeichnis muss vorhanden sein.
   - Ein C-Programm, das Aufrufe `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` sollte erfolgreich sein – die Syscall muss ein fd zurückgeben! =-1 und nicht mit EAFNOSUPPORT fehl.

Der genaue Fehler hängt von der Funktion ab. Für den Verbindungsserver manifestiert dies als ein Timeoutfehler für die Anmeldung aus. Für Verfügbarkeitsgruppen die `ALTER AVAILABILITY GROUP JOIN` DDL auf dem sekundären Replikat nach 5 Minuten mit einem Download-Konfigurationsfehler Timeout fehl.

Um dieses Problem zu umgehen, führen Sie eine der folgenden:

1. Verwenden Sie IP-Adressen anstelle von Hostnamen, um das Ziel der TCP-Verbindung anzugeben.

1. Aktivieren von IPv6-Umgebung in den Kernel durch Entfernen von `ipv6.disable=1` aus Boot Cmdline. Die Möglichkeit hierzu hängt davon ab, die Linux-Distribution und Startladeprogramm, z. B. Grub. Wenn Sie IPv6 deaktiviert werden soll, Sie können weiterhin das Feature deaktivieren festlegen `net.ipv6.conf.all.disable_ipv6 = 1` in der `sysctl` Konfiguration (z. B. `/etc/sysctl.conf`). Dies wird immer noch verhindern, dass das System Netzwerkadapter eine IPv6-Adresse abrufen, ermöglicht jedoch die Sqlservr Funktionen ausgeführt.

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
Bei Verwendung von **System NFS (Network File)** Remotefreigaben in der Produktion Beachten Sie die folgenden Anforderungen für die Unterstützung:

- Verwenden Sie NFS Version **4.2 oder höher**. Ältere Versionen von NFS unterstützen keine erforderliche Features, z. B. Fallocate und Erstellung von Dateien mit geringer Dichte, moderne Dateisystemen gemeinsam.
- Suchen Sie nur die **/var/opt/mssql** Verzeichnisse auf dem NFS-Bereitstellungspunkt. Andere Dateien, z. B. die SQL Server-System-Binärdateien werden nicht unterstützt.
- Stellen Sie sicher, dass die NFS-Clients die Option "Nolock" verwenden, wenn die Remotefreigabe bereitstellen.

#### <a name="localization"></a>Lokalisierung

- Wenn das Gebietsschema Englisch (En_us) nicht während des Setups ist, müssen Sie die UTF-8-Codierung in der Bash-Sitzung/Terminaldienste verwenden. Wenn Sie die ASCII-Codierung verwenden, wird möglicherweise eine Fehlermeldung ähnlich der folgenden angezeigt:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Wenn Sie UTF-8-Codierung verwenden können, führen Sie Setup mithilfe der Umgebungsvariable MSSQL_LCID Ihrer Wahl der Sprache angeben.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Wenn Mssql-Conf-Setup ausführen, und Durchführen einer nicht englischen-Installation von SQL Server falsche erweiterten Zeichen nach dem lokalisierten Text "Konfigurieren von SQL Server..." angezeigt werden. Oder, bei nicht-lateinische basierend Installationen des Satzes fehlt möglicherweise vollständig. Fehlende Satz die lokalisierte Zeichenfolge sollte angezeigt werden: "die Lizenzierung PID wurde erfolgreich verarbeitet.  Die neue Edition ist [\<Namen\> Edition] ". Diese Zeichenfolge wird nur zu Informationszwecken ausgeben, und die nächste Instanz von kumulative Update für SQL Server wird dies für alle Sprachen lösen. Dies wirkt sich nicht auf die erfolgreiche Installation von SQL Server in keiner Weise aus. 

#### <a name="full-text-search"></a>Volltextsuche

- Nicht alle Filter sind in dieser Version, z. B. Filter für Office-Dokumente verfügbar. Eine Liste der unterstützten Filter, finden Sie unter [installieren Sie SQL Server-Volltextsuche unter Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- Die **Mssql Server ist** Paket SUSE in dieser Version nicht unterstützt wird. Es wird zurzeit auf Ubuntu und auf Red Hat Enterprise Linux (RHEL) unterstützt.

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

Eine Liste der integrierten SSIS-Komponenten, die derzeit nicht unterstützt, oder mit Einschränkungen unterstützt werden, finden Sie unter [Einschränkungen und bekannten Probleme für SSIS unter Linux](sql-server-linux-ssis-known-issues.md#components).

Weitere Informationen zu SSIS unter Linux finden Sie unter den folgenden Artikeln:
-   [Blog Post Ankündigung SSIS-Unterstützung für Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Installieren von SQL Server Integration Services (SSIS) unter Linux](sql-server-linux-setup-ssis.md)
-   [Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)

Die folgenden Einschränkungen gelten für SSMS unter Windows, die mit SQL Server on Linux verbunden.

- Ausführen von Wartungsplänen werden nicht unterstützt.

- Management Data Warehouse (MDW) und der Datensammler in SSMS werden nicht unterstützt. 

- SSMS-UI-Komponenten, die Windows-Authentifizierung oder Windows-Ereignisprotokoll-Optionen verfügen funktionieren nicht mit Linux. Sie können diese Funktionen weiterhin mit anderen Optionen, z. B. SQL-Anmeldenamen verwenden. 

- Anzahl der Protokolldateien beibehalten werden sollen, nicht geändert werden.

## <a name="next-steps"></a>Nächste Schritte

Um zu beginnen, finden Sie in der folgenden Schnellstarts:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)
- [Provision a SQL VM in Azure (Bereitstellen einer SQL-VM in Azure)](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [Ausführen und Verbinden – Cloud](quickstart-install-connect-clouds.md)
