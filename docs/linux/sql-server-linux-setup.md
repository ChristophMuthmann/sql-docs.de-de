---
title: -Installationsleitfaden für SQL Server-2017 unter Linux | Microsoft Docs
description: Installieren, aktualisieren und Deinstallieren von SQL Server on Linux. In diesem Artikel werden online, offline und unbeaufsichtigte Szenarien behandelt.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/06/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.workload: Active
ms.openlocfilehash: 69b56cf027a1c7d8f536b4d9ad80e5ef3b627469
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>-Installationsleitfaden für SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieser Artikel enthält Hinweise zum Installieren, aktualisieren und Deinstallieren von SQL Server-2017 unter Linux.

> [!TIP]
> Dieses Handbuch coves verschiedene Bereitstellungsszenarien. Wenn Sie nur für-Schritt-Anweisungen suchen, wechseln Sie in eines der Schnellstarts:
> - [RHEL-Schnellstart](quickstart-install-connect-red-hat.md)
> - [SLES-Schnellstart](quickstart-install-connect-suse.md)
> - [Ubuntu-Schnellstart](quickstart-install-connect-ubuntu.md)
> - [Docker-Schnellstart](quickstart-install-connect-docker.md)

Antworten auf häufig gestellte Fragen, finden Sie unter der [SQL Server on Linux – häufig gestellte Fragen](../linux/sql-server-linux-faq.md).

## <a id="supportedplatforms"></a> Unterstützte Plattformen

SQL Server-2017 wird unter Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) und Ubuntu unterstützt. Es wird auch als ein Docker Bild unterstützt, die auf den Docker-Modul unter Linux oder Docker für Windows/Mac ausgeführt werden können

| Platform | Unterstützte Versionen | Herunterladen
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3 oder 7.4 | [RHEL 7.4 abrufen](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [SLES v12 SP2 abrufen](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Ubuntu 16.04 abrufen](http://www.ubuntu.com/download/server)
| **Docker-Modul** | 1.8+ | [Abrufen von Docker](http://www.docker.com/products/overview)

Microsoft unterstützt auch bereitstellen und Verwalten von SQL Server-Container mithilfe von OpenShift und Kubernetes.

> [!NOTE]
> SQL Server wird getestet und für die zuvor aufgelisteten Verteilungen unter Linux unterstützt. Wenn Sie entscheiden, SQL Server auf ein nicht unterstütztes Betriebssystem zu installieren, lesen Sie bitte die **Supportrichtlinie** Teil der [technischen Support-Richtlinie für Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) zu verstehen, die Unterstützung Auswirkungen auf.

## <a id="system"></a> Systemanforderungen

SQL Server-2017 hat die folgenden Systemanforderungen für Linux:

|||
|-----|-----|
| **Speicher** | 2 GB |
| **Dateisystem** | **XFS** oder **EXT4** (andere Dateisysteme, z. B. **BTRFS**, werden nicht unterstützt) |
| **Speicherplatz** | 6 GB |
| **Taktfrequenz des Prozessors** | 2 GHz |
| **Prozessorkerne** | 2 Kerne |
| **Prozessortyp** | X64-kompatiblen |

Bei Verwendung von **System NFS (Network File)** Remotefreigaben in der Produktion Beachten Sie die folgenden Anforderungen für die Unterstützung:

- Verwenden Sie NFS Version **4.2 oder höher**. Ältere Versionen von NFS unterstützen keine erforderliche Features, z. B. Fallocate und Erstellung von Dateien mit geringer Dichte, moderne Dateisystemen gemeinsam.
- Suchen Sie nur die **/var/opt/mssql** Verzeichnisse auf dem NFS-Bereitstellungspunkt. Andere Dateien, z. B. die SQL Server-System-Binärdateien werden nicht unterstützt.
- Stellen Sie sicher, dass die NFS-Clients die Option "Nolock" verwenden, wenn die Remotefreigabe bereitstellen.

## <a id="repositories"></a> Konfigurieren von quellrepositorys

Beim Installieren oder Aktualisieren von SQL Server, erhalten Sie die neueste Version von SQL Server-2017 von Ihr konfigurierte Microsoft-Repository. Verwenden Sie die Schnellstarts der **kumulativen Update (CU)** Repository. Sie können aber stattdessen Konfigurieren der **GDR** Repository. Weitere Informationen zu Repositorys und deren Konfiguration finden Sie unter [konfigurieren Repositorys für SQL Server on Linux](sql-server-linux-change-repo.md).

> [!IMPORTANT]
> Wenn Sie eine CTP-Version oder RC-Version von SQL Server-2017 zuvor installiert haben, müssen Sie entfernen die Preview-Repository und registrieren einen allgemeinen Verfügbarkeit (GA) eine. Weitere Informationen finden Sie unter [konfigurieren Repositorys für SQL Server on Linux](sql-server-linux-change-repo.md).

## <a id="platforms"></a> Installieren von SQL Server

Sie können SQL Server on Linux über die Befehlszeile installieren. Anleitungen hierzu finden Sie eine der folgenden Schnellstarts aus:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-docker.md)
- [Provision a SQL VM in Azure (Bereitstellen einer SQL-VM in Azure)](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

## <a id="upgrade"></a> Aktualisieren Sie SQLServer

Beim Aktualisieren der **Mssql Server** Paket auf die neueste Version, verwenden Sie die folgenden Befehle, die basierend auf Ihrer Plattform:

| Platform | Paket-Update-Befehle |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

Diese Befehle die neuesten Downloadpaket und Ersetzen Sie die Binärdateien befindet sich im `/opt/mssql/`. Der vom Benutzer generierte Datenbanken und Systemdatenbanken werden von diesem Vorgang nicht betroffen.

## <a id="rollback"></a> Rollback SQLServer

Verwenden Sie Rollback oder Downgrade für die SQL Server auf einer früheren Version die folgenden Schritte aus:

1. Identifizieren Sie die Versionsnummer für das SQL Server-Paket beim downgrade auf den gewünschten. Eine Liste der Paket-Zahlen, finden Sie unter der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md).

1. Ein Downgrade auf eine frühere Version von SQL Server. Ersetzen Sie in den folgenden Befehlen `<version_number>` mit der SQL Server-Versionsnummer, die Sie in Schritt 1 identifiziert.

   | Platform | Paket-Update-Befehle |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> Es wird nur unterstützt, um ein Downgrade auf eine Version, innerhalb der gleichen Hauptversion, z. B. SQL Server-2017 auszuführen.

## <a id="versioncheck"></a> Überprüfen Sie die installierte Version von SQL Server

Um Ihre aktuelle Version und Edition von SQL Server on Linux zu überprüfen, verwenden Sie das folgende Verfahren:

1. Wenn noch nicht installiert, installieren Sie die [SQL Server-Befehlszeilentools](sql-server-linux-setup-tools.md).

1. Verwendung **Sqlcmd** einen Transact-SQL-Befehl ausführen, die dem SQL Server-Version und Edition angezeigt.

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> Deinstallieren von SQLServer

So entfernen Sie die **Mssql Server** Paket auf Linux, verwenden Sie die folgenden Befehle, die basierend auf Ihrer Plattform:

| Platform | Paket entfernen Befehle |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

Das Entfernen des Pakets werden die generierten Dateien nicht gelöscht werden. Wenn Sie die Datenbankdateien löschen möchten, verwenden Sie den folgenden Befehl aus:

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="unattended"></a> Unbeaufsichtigte Installation

Sie können eine unbeaufsichtigte Installation auf folgende Weise ausführen:

- Führen Sie der ersten in Schritten der [Schnellstarts](#platforms) Repositorys registrieren und Installieren von SQL Server.
- Bei der Ausführung `mssql-conf setup`legen [Umgebungsvariablen](sql-server-linux-configure-environment-variables.md) und Verwenden der `-n` (keine Aufforderung) Option.

Das folgende Beispiel konfiguriert die Developer Edition von SQL Server mit der **MSSQL_PID** -Umgebungsvariablen angegeben. Außerdem akzeptiert den Endbenutzer-Lizenzvertrag (**ACCEPT_EULA**) und legt das SA-Benutzerkennwort (**MSSQL_SA_PASSWORD**). Die `-n` Parameter führt eine unaufgefordert-Installation, in dem die Konfigurationswerte aus der Umgebungsvariablen abgerufen werden.

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

Sie können auch ein Skript erstellen, das andere Aktionen ausführt. Beispielsweise konnten Sie andere SQL Server-Pakete installieren.

Eine ausführlichere Beispielskript finden Sie unter den folgenden Beispielen:

- [Red Hat-Skript für die unbeaufsichtigte Installation](sample-unattended-install-redhat.md)
- [SUSE-Skript für die unbeaufsichtigte Installation](sample-unattended-install-suse.md)
- [Ubuntu Skript für die unbeaufsichtigte Installation](sample-unattended-install-ubuntu.md)

## <a id="offline"></a> Offline-Installation

Wenn Ihre Linux-Computer auf den online-Repositorys verwendet keinen Zugriff hat die [Schnellstarts](#platforms), Sie können die Paketdateien direkt herunterladen. Diese Pakete befinden sich im Repository Microsoft [ https://packages.microsoft.com ](https://packages.microsoft.com).

> [!TIP]
> Wenn Sie die Schritte in der Schnellstarts erfolgreich installiert, müssen Sie nicht herunterladen oder installieren Sie manuell die SQL Server-Pakete. Dieser Abschnitt ist nur für das Offlineszenario.

1. **Laden Sie das Datenbank-Engine-Paket für Ihre Plattform**. Finden Sie im Abschnitt Details Paket Downloadlinks Paket die [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md).

1. **Verschieben Sie das heruntergeladene Paket auf den Linux-Computer**. Wenn Sie einen anderen Computer verwendet, um die Pakete herunterzuladen, ist eine Möglichkeit zum Verschieben der Pakete auf den Linux-Computer mit der **scp** Befehl.

1. **Installieren Sie das Datenbank-Engine-Paket**. Verwenden Sie die folgenden Befehle, die basierend auf Ihrer Plattform. Ersetzen Sie den Namen der Paketdatei in diesem Beispiel wird mit dem genauen Namen, den Sie heruntergeladen haben.

   | Platform | Paket installieren-Befehl |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > Sie können auch die RPM-Pakete (RHEL und SLES) installieren, mit der `rpm -ivh` -Befehl, aber die Befehle in der vorherigen Tabelle automatisch installieren von Abhängigkeiten von verfügbaren Repositorys genehmigt.

1. **Alle fehlenden Abhängigkeiten müssen aufgelöst**: Sie müssen möglicherweise an diesem Punkt fehlenden Abhängigkeiten. Wenn dies nicht der Fall ist, können Sie diesen Schritt überspringen. Auf Ubuntu, wenn Sie Zugriff auf genehmigten Repositorys, enthält diese Abhängigkeiten die einfachste Lösung ist die Verwendung der `apt-get -f install` Befehl. Dieser Befehl schließt auch die Installation von SQL Server. Um Abhängigkeiten manuell zu überprüfen, verwenden Sie die folgenden Befehle ein:

   | Platform | Abhängigkeiten auflisten (Befehl) |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   Versuchen Sie nach der fehlenden Abhängigkeiten werden aufgelöst, das Paket Mssql-Server erneut zu installieren.

1. **Schließen Sie das SQL Server-Setup**. Verwendung **Mssql-Conf** um das SQL Server-Setup abzuschließen:

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="optional-sql-server-features"></a>Optionale SQL Server-Funktionen

Nach der Installation können Sie auch installieren oder optionale Features von SQL Server aktivieren.

- [SQL Server-Befehlszeilentools](sql-server-linux-setup-tools.md)
- [SQL Server-Agent](sql-server-linux-setup-sql-agent.md)
- [SQL Server-Volltextsuche](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integrationsservices (Ubuntu)](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> Antworten auf häufig gestellte Fragen, finden Sie unter der [SQL Server on Linux – häufig gestellte Fragen](sql-server-linux-faq.md).
