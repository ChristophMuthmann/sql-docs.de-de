---
title: "Konfigurieren des Repositorys für SQL Server on Linux | Microsoft Docs"
description: "Überprüfen Sie, und konfigurieren Sie quellrepositorys für SQL Server-2017 unter Linux. Das Quellrepository wirkt sich auf die Version von SQL Server, der während der Installation und Aktualisierung angewendet wird."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/07/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Active
ms.openlocfilehash: 82a1f6d840897311dbb52ffbbf2620c8ec3994ec
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>Konfigurieren des Repositorys für die Installation und Upgrade von SQL Server on Linux

Dieser Artikel beschreibt die richtige Repository für 2017 von SQL Server-Installationen und-Aktualisierungen unter Linux konfigurieren.

> [!IMPORTANT]
> Wenn Sie eine CTP-Version oder RC-Version von SQL Server-2017 zuvor installiert haben, müssen Sie die Schritte in diesem Artikel verwenden, um ein Repository für die allgemeine Verfügbarkeit (GA) zu registrieren und zu aktualisieren oder neu zu installieren. Die Preview-Versionen von SQL Server-2017 werden nicht unterstützt und läuft.

## <a id="repositories"></a>Repositorys

Wenn Sie SQL Server on Linux installieren, müssen Sie ein Microsoft-Repository konfigurieren. Dieses Repository dient zum Abrufen der Datenbank-Engine-Paket **Mssql Server**, und beziehen Sie SQL Server-Paketen. Es gibt derzeit drei wichtigsten Repositorys:

| Repository | Name | Description |
|---|---|---|
| **Vorschau** | **mssql-server** | Vorschau-Repository für die CTP-Version und RC-Versionen von SQL Server. Dieses Repository ist für SQL Server-2017 nicht unterstützt. |
| **CU** | **mssql-server-2017** | SQL Server 2017 kumulativen Update (CU)-Repository. |
| **GDR** | **mssql-server-2017-gdr** | SQL Server 2017 GDR-Repository für nur kritische Updates. |

## <a id="cuversusgdr"></a>Kumulatives Update im Vergleich zu GDR

Es ist wichtig zu beachten, dass es zwei Haupttypen von Repositorys für jede Verteilung gibt:

- **Kumulative Updates (CU)**: das kumulative Update (CU)-Repository enthält Pakete für die grundlegenden SQL Server-Version sowie alle Programmfehlerbehebungen und Verbesserungen seit diesem Release. Kumulative Updates sind spezifisch für die endgültige Produktversion, z. B. SQL Server-2017. Sie werden in einem regulären Rhythmus veröffentlicht.

- **GDR**: die GDR-Repository enthält Pakete für die grundlegenden SQL Server-Version und nur kritische Updates und Sicherheitsupdates seit diesem Release. Diese Updates werden auch auf die nächste CU-Version hinzugefügt.

Jeder CU und GDR-Version enthält die vollständige SQL Server-Paket und alle vorherigen Updates für das Repository. Aktualisieren von einer GDR-Version für eine CU-Version wird durch Ändern des konfigurierten Repositorys für SQL Server unterstützt. Sie können auch [downgrade](sql-server-linux-setup.md#rollback) auf eine beliebige Version innerhalb der Hauptversion (zum Beispiel: 2017).

> [!NOTE]
> Sie können von einer GDR-Version aktualisieren, um CU jederzeit freigegeben werden, indem ein Repositorys ändern. Aktualisieren von ein CU-Version mit einer GDR-Version wird nicht unterstützt. 

## <a id="configure"></a>Konfigurieren Sie ein repository

In den folgenden Abschnitten wird beschrieben, wie zum Überprüfen und konfigurieren ein Repository für die folgenden Plattformen unterstützten:

- [Red Hat Enterprise Server](#rhel)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#sles)

## <a id="rhel"></a>RHEL Repositorys konfigurieren
Verwenden Sie die folgenden Schritte aus, um Repositorys auf Red Hat Enterprise Server (RHEL) konfigurieren.

### <a name="check-for-previously-configured-repositories-rhel"></a>Überprüfen Sie zuvor konfigurierten Repositorys (RHEL)
Überprüfen Sie zunächst, ob Sie bereits ein SQL Server-Repository registriert haben.

1. Zeigen Sie die Dateien in den **/etc/yum.repos.d** Verzeichnis mit den folgenden Befehl aus:

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. Suchen Sie nach einer Datei, die das SQL Server-Verzeichnis, wie z. B. konfiguriert **Mssql-server.repo**.

3. Druckt den Inhalt der Datei.

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. Die **Namen** Eigenschaft ist für die konfigurierten Repository. Sie können mit der Tabelle im Identifizieren der [Repositorys](#repositories) Abschnitt dieses Artikels.

### <a name="remove-old-repository-rhel"></a>Entfernen Sie alte Repository (RHEL)
Entfernen Sie ggf. das alte Repository mit dem folgenden Befehl.

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

Mit diesem Befehl wird davon ausgegangen, dass die Datei identifiziert, die im vorherigen Abschnitt benannt wurde **Mssql-server.repo**.

### <a name="configure-new-repository-rhel"></a>Konfigurieren Sie neue Repository (RHEL)
Konfigurieren Sie das neue Repository für SQL Server-Installationen und Upgrades verwenden. Verwenden Sie einen der folgenden Befehle aus, um das Repository Ihrer Wahl zu konfigurieren.

| Repository | Befehl |
|---|---|
| **CU** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

## <a id="sles"></a>SLES Repositorys konfigurieren
Verwenden Sie die folgenden Schritte aus, um auf SLES Repositorys konfigurieren.

### <a name="check-for-previously-configured-repositories-sles"></a>Überprüfen Sie zuvor konfigurierten Repositorys (SLES)
Überprüfen Sie zunächst, ob Sie bereits ein SQL Server-Repository registriert haben.

1. Verwendung **Zypper Info** um Informationen über alle zuvor konfigurierten Repository abzurufen.

   ```bash
   sudo zypper info mssql-server
   ```

2. Die **Repository** Eigenschaft ist für die konfigurierten Repository. Sie können mit der Tabelle im Identifizieren der [Repositorys](#repositories) Abschnitt dieses Artikels.

### <a name="remove-old-repository-sles"></a>Entfernen Sie alte Repository (SLES)
Entfernen Sie ggf. das alte Repository. Verwenden Sie die folgenden Befehle, die basierend auf den zuvor konfigurierten Repository-Typ.

| Repository | Befehl zum Entfernen |
|---|---|
| **Vorschau** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

### <a name="configure-new-repository-sles"></a>Konfigurieren Sie neue Repository (SLES)
Konfigurieren Sie das neue Repository für SQL Server-Installationen und Upgrades verwenden. Verwenden Sie einen der folgenden Befehle aus, um das Repository Ihrer Wahl zu konfigurieren.

| Repository | Befehl |
|---|---|
| **CU** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

## <a id="ubuntu"></a>Ubuntu-Repositorys konfigurieren
Verwenden Sie die folgenden Schritte aus, um auf Ubuntu Repositorys konfigurieren.

### <a name="check-for-previously-configured-repositories-ubuntu"></a>Überprüfen Sie zuvor konfigurierten Repositorys (Ubuntu)
Überprüfen Sie zunächst, ob Sie bereits ein SQL Server-Repository registriert haben.

1. Anzeigen des Inhalts der **/etc/apt/sources.list** Datei.

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. Überprüfen Sie die Paket-URL für Mssql-Server. Sie können mit der Tabelle im Identifizieren der [Repositorys](#repositories) Abschnitt dieses Artikels.

### <a name="remove-old-repository-ubuntu"></a>Entfernen Sie alte Repository (Ubuntu)
Entfernen Sie ggf. das alte Repository. Verwenden Sie die folgenden Befehle, die basierend auf den zuvor konfigurierten Repository-Typ.

| Repository | Befehl zum Entfernen |
|---|---|
| **Vorschau** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` 
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

### <a name="configure-new-repository-ubuntu"></a>Konfigurieren Sie neue Repository (Ubuntu)
Konfigurieren Sie das neue Repository für SQL Server-Installationen und Upgrades verwenden.

1. Importieren Sie die öffentlichen Repositorys GPG Schlüssel.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Verwenden Sie einen der folgenden Befehle aus, um das Repository Ihrer Wahl zu konfigurieren.

   | Repository | Befehl |
   |---|---|
   | **CU** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. Führen Sie **apt-Get Update**.

   ```bash
   sudo apt-get update
   ```

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie das richtige Repository konfiguriert haben, können Sie zu Fortfahren [installieren](sql-server-linux-setup.md#platforms) oder [aktualisieren](sql-server-linux-setup.md#upgrade) SQL Server und der verbundenen Pakete aus dem Repository neue.

> [!IMPORTANT]
> An diesem Punkt, wenn Sie einen Artikel Installation z. B. Verwenden der [Schnellstarts](sql-server-linux-setup.md#platforms), denken Sie daran, dass Sie bereits im Zielrepository konfiguriert haben. Wiederholen Sie diesen Schritt nicht in den Lernprogrammen. Dies ist insbesondere dann, wenn Sie das Repository GDR konfigurieren, da die Schnellstarts CU-Repository verwenden.

> [!IMPORTANT]
> Eine beliebige Version von SQL Server-2017 vor der CTP-Version 2.1 muss auf mindestens 2.1 aktualisiert werden, vor dem Upgrade auf GA Eine andere Möglichkeit besteht darin Sichern Ihrer Datenbanken, die frühere Version deinstallieren und anschließend Ausführen eine Neuinstallation von GA-Version.

Weitere Informationen zum Installieren von SQL Server-2017 unter Linux finden Sie unter [-Installationsleitfaden für SQL Server on Linux](sql-server-linux-setup.md).
