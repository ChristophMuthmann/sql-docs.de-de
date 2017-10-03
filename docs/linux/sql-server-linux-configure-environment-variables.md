---
title: Konfigurieren von SQL Server mit Umgebungsvariablen | Microsoft Docs
description: Dieses Thema beschreibt die Umgebungsvariablen zu verwenden, um bestimmte 2017 von SQL Server-Einstellungen unter Linux konfigurieren.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/21/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 2bbb64b775ab59665ac2c8eefdd21e514b4906cd
ms.contentlocale: de-de
ms.lasthandoff: 10/02/2017

---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Konfigurieren von SQL Server mit Umgebungsvariablen unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

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
| **MSSQL_PID** | Legen Sie die Edition oder Product Key für SQL Server. Folgende Werte sind möglich: Evaluation, Developer, Express, Web, Standard, Enterprise oder einen Product Key in Form von ###-###-###-###-###, wobei "#", eine Zahl oder ein Buchstabe ist. |
| **MSSQL_LCID** | Legt die Sprach-ID für SQL Server verwendet. 1036 befindet sich z. B. Französisch. |
| **MSSQL_COLLATION** | Legt die standardsortierung für SQL Server fest. Dies überschreibt die standardzuordnung der Sprach-Id (LCID), Sortierung. |
| **MSSQL_MEMORY_LIMIT_MB** | Legt die Höchstmenge an Arbeitsspeicher (in MB), die SQL Server verwenden können. Es ist standardmäßig 80 % des gesamten physischen Arbeitsspeichers. |
| **MSSQL_TCP_PORT** | Konfigurieren Sie den TCP-Port, den SQL Server (Standardport: 1433) überwacht. |
| **MSSQL_IP_ADDRESS** | Legen Sie die IP-Adresse ein. Derzeit muss die IP-Adresse IPv4-Format (0.0.0.0) sein. |
| **MSSQL_BACKUP_DIR** | Legen Sie den Standardspeicherort für das Sicherungsverzeichnis. |
| **MSSQL_DATA_DIR** | Ändern Sie das Verzeichnis, in dem die neuen SQL Server-Datenbank-Datendateien (MDF) erstellt werden. |
| **MSSQL_LOG_DIR** | Ändern Sie das Verzeichnis, in dem die neue SQL Server-Protokolldateien (LDF) Datenbankdateien erstellt werden. |
| **MSSQL_DUMP_DIR** | Ändern Sie das Verzeichnis, in dem SQL Server die Speicherabbilder und andere Dateien zur Problembehandlung in der Standardeinstellung ablegt. |
| **MSSQL_ENABLE_HADR** | Aktivieren von Verfügbarkeitsgruppen. |

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

## <a name="next-steps"></a>Nächste Schritte

Andere SQL Server-Einstellungen, die hier nicht aufgelistet sind, finden Sie unter [konfigurieren Sie SQL Server unter Linux mit dem Tool Mssql-Conf](sql-server-linux-configure-mssql-conf.md).

Weitere Informationen zum Installieren und Ausführen von SQL Server unter Linux finden Sie unter [Installieren von SQL Server on Linux](sql-server-linux-setup.md).

