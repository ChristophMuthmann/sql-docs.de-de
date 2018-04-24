---
title: Konfigurieren von SQL Server mit Umgebungsvariablen | Microsoft Docs
description: Dieser Artikel beschreibt die Umgebungsvariablen zu verwenden, um bestimmte 2017 von SQL Server-Einstellungen unter Linux konfigurieren.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: On Demand
ms.openlocfilehash: 523959047c7b7cd7cce36138650b8cc52873f73e
ms.sourcegitcommit: f3aa02a0f27cc1d3d5450f65cc114d6228dd9d49
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2018
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Konfigurieren von SQL Server mit Umgebungsvariablen unter Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Mehrere verschiedene Umgebungsvariablen können Sie SQL Server-2017 unter Linux konfigurieren. Diese Variablen werden in zwei Szenarien verwendet:

- Zum Konfigurieren von anfänglichen Setup mit der `mssql-conf setup` Befehl.
- So konfigurieren Sie ein neues [SQL Server-Container in Docker](quickstart-install-connect-docker.md).

> [!TIP]
> Wenn Sie SQL Server nach diesen setupszenarien konfigurieren müssen, finden Sie unter [konfigurieren Sie SQL Server unter Linux mit dem Tool Mssql-Conf](sql-server-linux-configure-mssql-conf.md).

## <a name="environment-variables"></a>Umgebungsvariablen

| Umgebungsvariable | Description |
|-----|-----|
| **ACCEPT_EULA** | Akzeptieren Sie den SQL Server-Lizenzvertrag bei Festlegung auf einen beliebigen Wert (z. B. "Y"). |
| **MSSQL_SA_PASSWORD** | Konfigurieren Sie das SA-Kennwort ein. |
| **MSSQL_PID** | Legen Sie die Edition oder Product Key für SQL Server. Zulässige Werte: </br></br>**Evaluation**</br>**Entwickler**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Einen Product key**</br></br>Wenn Sie einen Product Key angeben, muss es in Form von ###-###-###-###-###, sein, wobei "#" eine Zahl oder ein Buchstabe ist.|
| **MSSQL_LCID** | Legt die Sprach-ID für SQL Server verwendet. 1036 befindet sich z. B. Französisch. |
| **MSSQL_COLLATION** | Legt die standardsortierung für SQL Server fest. Dies überschreibt die standardzuordnung der Sprach-Id (LCID), Sortierung. |
| **MSSQL_MEMORY_LIMIT_MB** | Legt die Höchstmenge an Arbeitsspeicher (in MB), die SQL Server verwenden können. Es ist standardmäßig 80 % des gesamten physischen Arbeitsspeichers. |
| **MSSQL_TCP_PORT** | Konfigurieren Sie den TCP-Port, den SQL Server (Standardport: 1433) überwacht. |
| **MSSQL_IP_ADDRESS** | Legen Sie die IP-Adresse ein. Derzeit muss die IP-Adresse IPv4-Format (0.0.0.0) sein. |
| **MSSQL_BACKUP_DIR** | Legen Sie den Standardspeicherort für das Sicherungsverzeichnis. |
| **MSSQL_DATA_DIR** | Ändern Sie das Verzeichnis, in dem die neuen SQL Server-Datenbank-Datendateien (MDF) erstellt werden. |
| **MSSQL_LOG_DIR** | Ändern Sie das Verzeichnis, in dem die neue SQL Server-Protokolldateien (LDF) Datenbankdateien erstellt werden. |
| **MSSQL_DUMP_DIR** | Ändern Sie das Verzeichnis, in dem SQL Server die Speicherabbilder und andere Dateien zur Problembehandlung in der Standardeinstellung ablegt. |
| **MSSQL_ENABLE_HADR** | Aktivieren der Verfügbarkeitsgruppe. Beispielsweise "1" aktiviert ist, und "0" ist deaktiviert. |
| **MSSQL_AGENT_ENABLED** | SQL Server-Agent zu aktivieren. Beispielsweise "true" aktiviert ist, und 'false' ist deaktiviert. Agent ist standardmäßig deaktiviert.  |
| **MSSQL_MASTER_DATA_FILE** | Legt den Speicherort der master-Datenbank-Datendatei an. |
| **MSSQL_MASTER_LOG_FILE** | Legt den Speicherort der master-Datenbank-Protokolldatei fest. |
| **MSSQL_ERROR_LOG_FILE** | Legt den Speicherort der Dateien im Fehlerprotokoll. |


## <a name="example-initial-setup"></a>Beispiel: Anfangssetup

In diesem Beispiel wird `mssql-conf setup` Umgebungsvariablen konfiguriert. Die folgenden Umgebungsvariablen werden angegeben:

- **ACCEPT_EULA** den Endbenutzer-Lizenzvertrag akzeptiert.
- **MSSSQL_PID** gibt an, die kostenlos lizenzierte Developer Edition von SQL Server für die nicht produktive Verwendung.
- **MSSQL_SA_PASSWORD** legt ein sicheres Kennwort.
- **MSSQL_TCP_PORT** legt den TCP-Port, der SQL Server bei 1234 überwacht.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="example-docker"></a>Beispiel: Docker

Diese Beispiel-Befehl "Docker" verwendet die folgenden Umgebungsvariablen, um einen neuen 2017 von SQL Server-Container erstellen:

- **ACCEPT_EULA** den Endbenutzer-Lizenzvertrag akzeptiert.
- **MSSSQL_PID** gibt an, die kostenlos lizenzierte Developer Edition von SQL Server für die nicht produktive Verwendung.
- **MSSQL_SA_PASSWORD** legt ein sicheres Kennwort.
- **MSSQL_TCP_PORT** legt den TCP-Port, der SQL Server bei 1234 überwacht. Dies bedeutet, dass anstelle von Mapping-Port 1433 (Standard) an einen hostPort, der benutzerdefinierte TCP-Port zugeordnet werden muss, mit der `-p 1234:1234` in diesem Beispiel den Befehl.

Wenn Sie Docker auf Linux/MacOS ausführen, verwenden Sie die folgende Syntax in einfache Anführungszeichen eingeschlossen:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d microsoft/mssql-server-linux:2017-latest
```

Wenn Sie Docker unter Windows ausgeführt werden, verwenden Sie die folgende Syntax mit doppelten Anführungszeichen an:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d microsoft/mssql-server-linux:2017-latest
```

> [!NOTE]
> Die Vorgehensweise zum Ausführen von Produktionseditionen in Containern weicht hiervon minimal ab. Weitere Informationen finden Sie unter [Run production container images (Ausführen von Containerimages für Produktionsumgebungen)](sql-server-linux-configure-docker.md#production).

## <a name="next-steps"></a>Nächste Schritte

Andere SQL Server-Einstellungen, die hier nicht aufgelistet sind, finden Sie unter [konfigurieren Sie SQL Server unter Linux mit dem Tool Mssql-Conf](sql-server-linux-configure-mssql-conf.md).

Weitere Informationen zum Installieren und Ausführen von SQL Server unter Linux finden Sie unter [Installieren von SQL Server on Linux](sql-server-linux-setup.md).
