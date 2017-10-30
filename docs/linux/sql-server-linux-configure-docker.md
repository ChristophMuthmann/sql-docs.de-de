---
title: "Konfigurationsoptionen für SQL Server-2017 auf Docker | Microsoft Docs"
description: "Untersuchen Sie verschiedene Arten der Verwendung von und Interaktion mit SQL Server-2017 von containerimages in Docker. Dies schließt beibehalten von Daten, zum Kopieren von Dateien und Problembehandlung."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: H1Hack27Feb2017
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 4b39b8dce2a9d6b940936a6d7072fc41c2b67e8f
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="configure-sql-server-2017-container-images-on-docker"></a>Konfigurieren von SQL Server-2017 Container Bilder auf Docker

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

In diesem Thema wird erläutert, wie Sie konfigurieren und Verwenden der [Mssql-Server-Linux-Container-Abbild](https://hub.docker.com/r/microsoft/mssql-server-linux/) mit Docker. Dieses Image besteht aus SQL Server auf Grundlage 16.04 Ubuntu Linux ausgeführt wird. Sie können mit dem Docker-Modul 1.8 unter Linux oder auf Docker für Mac/Windows verwendet werden.

> [!NOTE]
> Dieses Thema befasst sich speziell auf die mit dem Mssql-Server-Linux-Image. Das Windows-Abbild wird nicht behandelt, aber Sie können weitere Informationen finden sie auf der [Mssql-Server-Windows Docker Hub-Seite](https://hub.docker.com/r/microsoft/mssql-server-windows/).

## <a name="pull-and-run-the-container-image"></a>Ziehen Sie aus, und führen Sie das Container-Bild

Führen Sie zum Abrufen, und führen Sie die Docker Container-Image für SQL Server-2017, die Voraussetzungen und Schritte in der folgenden quick Start-Lernprogramm:

- [Führen Sie die 2017 von SQL Server-Container-Image mit Docker](quickstart-install-connect-docker.md)

Dieses Thema enthält Szenarien für die weitere Verwendung in den folgenden Abschnitten.

## <a id="production"></a>Führen Sie Produktion containerimages

Schnellstart-Tutorial im vorherigen Abschnitt führt die kostenlose Developer Edition von SQL Server von Docker Hub. Die meisten Informationen gilt weiterhin, wenn Produktion containerimages, z. B. Enterprise, Standard oder Web Edition ausgeführt werden soll. Es gibt jedoch einige Unterschiede, die im folgenden beschrieben werden.

- Sie können nur SQL Server in einer produktionsumgebung verwenden, wenn Sie eine gültige Lizenz verfügen. Sie erhalten eine kostenlose Lizenz für SQL Server Express Produktion [hier](https://go.microsoft.com/fwlink/?linkid=857693). Lizenzen für SQL Server Standard und Enterprise Edition stehen über [Microsoft Volume Licensing](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs.aspx).

- Produktion SQL Server-Container-Images müssen von abgerufen werden [Docker Store](https://store.docker.com). Wenn Sie einen noch nicht haben, erstellen Sie ein Konto im Docker-Speicher.

- Die Developer-Container-Abbild auf Docker-Speicher kann die Produktions-Editionen ausgeführt konfiguriert werden. Verwenden Sie die folgenden Schritte aus, um die Produktion-Editionen ausgeführt:

   1. Melden Sie sich zunächst auf die Docker-Id über die Befehlszeile.

      ```bash
      docker login
      ```

   1. Als Nächstes müssen Sie freien Entwickler containerimage in Docker-Informationsspeicher abzurufen. Wechseln Sie zu [https://store.docker.com/images/mssql-server-linux](https://store.docker.com/images/mssql-server-linux), klicken Sie auf **zur Kasse**, und befolgen Sie die Anweisungen.

   1. Überprüfen Sie die Anforderungen und Prozeduren ausführen, der [quick Start-Lernprogramm](quickstart-install-connect-docker.md). Es gibt jedoch zwei Unterschiede. Sie müssen das Image per Pull beziehen **Store/Microsoft/Mssql-Server – Linux:\<Tagname\>**  Docker Store. Außerdem müssen Sie angeben, die Produktion Edition mit der **MSSQL_PID** -Umgebungsvariablen angegeben. Im folgende Beispiel wird gezeigt, wie das neueste 2017 von SQL Server-Container-Bild für die Enterprise Edition ausgeführt wird:

      ```bash
      docker run --name sqlenterprise \
         -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
         -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
         -d store/microsoft/mssql-server-linux:2017-latest
      ```

      ```PowerShell
      docker run --name sqlenterprise `
         -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
         -e "MSSQL_PID=Enterprise" -p 1433:1433 `
         -d "store/microsoft/mssql-server-linux:2017-latest"
      ```

      > [!IMPORTANT]
      > Durch Übergeben des Werts **Y** der Umgebungsvariable **ACCEPT_EULA** und eines Werts Edition in **MSSQL_PID**, Sie sind, stehen Ihnen eine Lizenz gültige und vorhandene für Ausdrücken die Edition und die Version von SQL Server, die Sie verwenden möchten. Sie erklären sich auch, dass die Verwendung der SQL Server-Software auf einem Docker-Container-Abbild von den Bestimmungen des SQL Server-Lizenz geregelt werden wird.

      > [!NOTE]
      > Eine vollständige Liste der möglichen Werte für **MSSQL_PID**, finden Sie unter [konfigurieren Sie SQL Server-Einstellungen mit Umgebungsvariablen unter Linux](sql-server-linux-configure-environment-variables.md).

## <a name="connect-and-query"></a>Eine Verbindung herstellen und Abfragen

Sie können eine Verbindung herstellen und Abfragen von SQL Server in einem Container aus entweder außerhalb des Containers oder in den Container. In den folgenden Abschnitten wird erläutert, beide Szenarien. 

### <a name="tools-outside-the-container"></a>Tools, die außerhalb des Containers

Sie können mit der SQL Server-Instanz auf dem Docker-Computer alle externen Linux, Windows oder MacOS Tools eine Verbindung herstellen, die SQL-Verbindungen unterstützt. Einige häufig verwendete Tools umfassen:

- [Sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio-Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) unter Windows](sql-server-linux-develop-use-ssms.md)

Im folgenden Beispiel wird **Sqlcmd** zur Verbindung mit SQL Server in einem Docker-Container ausgeführt. Die IP-Adresse in der Verbindungszeichenfolge ist die IP-Adresse des Hostcomputers, die im Container ausgeführt wird.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Wenn Sie einen hostPort zugeordnet, die nicht die Standardeinstellung **1433**, diesen Port zur Verbindungszeichenfolge hinzufügen. Angenommen, Sie angegeben `-p 1400:1433` in Ihrer `docker run` Befehl aus, und klicken Sie dann verbinden, indem explizit Port 1400 angeben.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Tools, die innerhalb des Containers

Beginnend mit SQL Server 2017 CTP 2.0 die [SQL Server-Befehlszeilentools](sql-server-linux-setup-tools.md) sind in den Container-Image enthalten. Wenn Sie das Image mit einer interaktiven Eingabeaufforderung anfügen, können Sie die Tools lokal ausführen.

1. Verwenden der `docker exec -it` Befehl zum Starten einer interaktiven Bash-Shell innerhalb Ihres Containers ausgeführt. Im folgenden Beispiel `e69e056c702d` die Container-ID.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Sie müssen immer die gesamte Container-Id angeben. Sie müssen nur genügend Zeichen zur eindeutigen Identifizierung angeben. In diesem Beispiel wird es ausreichend, um die verwenden u. u. `e6` oder `e69` und nicht die vollständige Id.

2. Einmal innerhalb des Containers, verbinden Sie lokal mit Sqlcmd. Beachten Sie, dass diese Sqlcmd wird nicht im Pfad in der Standardeinstellung ist, müssen Sie den vollständigen Pfad angeben.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Wenn Sie mit Sqlcmd fertig sind, geben Sie `exit`.

4. Geben Sie abschließend mit der interaktiven Eingabeaufforderung `exit`. Der Container wird weiterhin ausgeführt wird, nach dem Beenden der interaktiven Bash-Shell.

## <a name="run-multiple-sql-server-containers"></a>Führen Sie mehrere SQL Server-Container

Docker bietet eine Möglichkeit, mehrere SQL Server-Container auf demselben Hostcomputer ausgeführt wird. Dies ist der Ansatz für Szenarien, die mehrere Instanzen von SQL Server auf demselben Host erfordern. Jeder Container muss sich auf einen anderen Port verfügbar machen.

Das folgende Beispiel erstellt zwei SQL Server-Container und ordnet sie Ports **1401** und **1402** auf dem Hostcomputer.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d microsoft/mssql-server-linux:2017-latest
```

Es gibt jetzt zwei Instanzen von SQL Server in separaten Containern ausgeführt. Clients können mit jeder SQL Server-Instanz verbinden, mit der IP-Adresse der Docker-Host und die Portnummer für den Container.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="persist"></a>Ihre Daten beibehalten

Ihre Änderungen an der Konfiguration von SQL Server und Datenbankdateien in den Container beibehalten werden, auch wenn Sie den Container mit neu starten `docker stop` und `docker start`. Jedoch, wenn Sie den Container mit entfernen `docker rm`, alle Elemente im Container gelöscht wird, einschließlich SQL Server und Datenbanken. Im folgende Abschnitt erläutert die Verwendung **Datenvolumes** Datenbankdateien beibehalten, auch wenn die zugehörigen Container gelöscht werden.

> [!IMPORTANT]
> Für SQL Server ist es wichtig, dass Sie verstehen, dass die Datenpersistenz in Docker. Zusätzlich zu der Diskussion in diesem Abschnitt finden Sie unter der Docker-Dokumentation auf [zum Verwalten von Daten in Docker-Containern](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Bereitstellen einer Verzeichnisses des Webhosts als Datenträger für Daten

Die erste Möglichkeit besteht in einem Verzeichnis auf dem Host als Datenträger für Daten im Container eingebunden. Verwenden Sie hierzu die `docker run` -Befehl mit der `-v <host directory>:/var/opt/mssql` Flag. Dadurch werden die Daten zwischen Ausführungen Container wiederhergestellt werden.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

Mit dieser Technik können auch freigeben, und zeigen Sie die Dateien auf dem Docker-Host.

> [!IMPORTANT]
> Host-Volume-Zuordnungen für Docker auf einem Mac mit dem SQL Server auf Linux-Image wird zu diesem Zeitpunkt nicht unterstützt. Verwenden Sie stattdessen datenvolumecontainer. Diese Einschränkung bezieht sich auf die `/var/opt/mssql` Verzeichnis. Lesen aus einer bereitgestellten Verzeichnis funktioniert. Sie können z. B. ein Hostverzeichnis mit – V auf einem Mac bereitstellen und Wiederherstellung einer Sicherung von einem bak-Datei, die auf dem Host befindet.

### <a name="use-data-volume-containers"></a>Verwenden Sie datenvolumecontainer

Die zweite Möglichkeit ist die Verwendung ein volumecontainers Daten. Sie können einen Volume-Container erstellen, unter Angabe eines Namens Volume, anstatt ein Hostverzeichnis mit den `-v` Parameter. Das folgende Beispiel erstellt eine freigegebene Datenvolume mit dem Namen **Sqlvolume**.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

> [!NOTE]
> Dieses Verfahren zum Erstellen von einem Datenvolume implizit in den ausgeführten Befehls funktioniert nicht mit älteren Versionen von Docker. In diesem Fall verwenden Sie die explizite Schritte in der Dokumentation Docker [erstellen und Bereitstellen eines volumecontainers Daten](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Auch wenn Sie beenden und diesen Container zu entfernen, behält das Datenvolumen. Sehen Sie es mit der `docker volume ls` Befehl.

```bash
docker volume ls
```

Wenn Sie einen anderen Container klicken Sie dann mit dem gleichen Volume-Namen erstellen, verwendet der neue Container auf dem Volume enthaltenen SQL Server-Daten.

Verwenden Sie zum Entfernen eines volumecontainers Daten der `docker volume rm` Befehl.

> [!WARNING]
> Wenn Sie den volumecontainer Daten löschen, ist SQL Server-Daten im Container *dauerhaft* gelöscht.

### <a name="backup-and-restore"></a>Sichern und Wiederherstellen

Zusätzlich zu diesen Verfahren Container können Sie auch die Verwendung der standardmäßigen SQL Server-Sicherung und Techniken wiederherstellen. Sicherungsdateien können zum Schutz Ihrer Daten oder die Daten in eine andere SQL Server-Instanz verschieben. Weitere Informationen finden Sie unter [Sicherungs- und SQL Server-Datenbanken unter Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Wenn Sie Sicherungen erstellen, stellen Sie sicher, erstellen oder kopieren die Sicherungsdateien außerhalb der Container. Wenn der Container entfernt wird, werden die Sicherungsdateien hingegen ebenfalls gelöscht.

## <a name="execute-commands-in-a-container"></a>Führen Sie Befehle in einem container

Wenn Sie einen aktiven Container verfügen, können Sie Befehle innerhalb des Containers aus einer terminal Host ausführen.

So führen Sie die Container-ID zu erhalten:

```bash
docker ps
```

So starten Sie eine Bash Terminaldienste im Container ausführen:

```bash
docker exec -ti <Container ID> /bin/bash
```

Jetzt können Sie Befehle ausführen, als wären Sie sie am Terminal innerhalb des Containers ausgeführt werden. Wenn Sie fertig sind, geben Sie `exit`. Dies wird in der interaktiven Sitzung beendet, aber Ihres Containers wird weiterhin ausgeführt.

## <a name="copy-files-from-a-container"></a>Kopieren von Dateien aus einem container

Um eine Datei aus dem Container kopieren möchten, verwenden Sie den folgenden Befehl ein:

```bash
docker cp <Container ID>:<Container path> <host path>
```

**Beispiel:**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>Kopieren von Dateien in einen container

Um eine Datei in den Container zu kopieren, verwenden Sie den folgenden Befehl ein:

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**Beispiel:**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

## <a name="run-a-specific-sql-server-container-image"></a>Führen Sie ein bestimmtes SQL Server-Container-Bild

Es gibt Szenarien, in denen nicht empfehlenswert, verwenden Sie das neueste SQL Server-Container-Bild. Verwenden Sie zum Ausführen einer bestimmten SQL Server-Container-Image die folgenden Schritte aus:

1. Identifizieren Sie die Docker **Tag** für die Version, die Sie verwenden möchten. Um die verfügbaren Tags anzuzeigen, finden Sie unter [der Mssql-Server-Linux-Docker Hub-Seite](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Ziehen Sie das SQL Server-Container-Bild mit dem Tag. Um das Bild RC1 per Pull abzurufen, ersetzen Sie z. B. `<image_tag>` in den folgenden Befehl mit `rc1`.

   ```bash
   docker pull microsoft/mssql-server-linux:<image_tag>
   ```

1. Um einen neuen Container mit dem sich das Bild auszuführen, geben Sie den Tagnamen in der `docker run` Befehl. Ersetzen Sie in den folgenden Befehl `<image_tag>` mit der Version, die Sie ausführen möchten.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
   ```

Diese Schritte können auch einen vorhandenen Container herabgestuft werden, verwendet werden. Sie können z. B. zurücksetzen möchten oder downgrade einen aktiven Container für die Problembehandlung oder testen. Um einen aktiven Container ein Downgrade auszuführen, müssen Sie eine Technik für die Persistenz für den Datenordner verwenden. Befolgen Sie die gleichen Schritte der [Abschnitt Aktualisieren](#upgrade), aber der Tagname der älteren Version angeben, wenn Sie den neuen Container ausführen.

> [!IMPORTANT]
> Upgrades und Downgrades werden nur zwischen RC1 und RC2 zu diesem Zeitpunkt unterstützt.

## <a id="upgrade"></a>Upgrade von SQL Server-Container

Um die Container-Image mit Docker zu aktualisieren, müssen Sie zuerst identifizieren Sie das Tag für die Version für das Upgrade. Ziehen Sie aus der Registrierung mit dieser Version der `docker pull` Befehl:

```bash
docker pull microsoft/mssql-server-linux:<image_tag>
```

Dadurch wird die SQL Server-Images für neue Container erstellten aktualisiert, aber nicht SQL Server in allen ausgeführten Containern aktualisiert. Zu diesem Zweck müssen Sie einen neuen Container mit der neuesten SQL Server-Container-Image Erstellen und migrieren Ihre Daten auf diesen neuen Container.

1. Stellen Sie sicher, dass Sie eines der [Data Persistenz Techniken](#persist) für Ihre vorhandenen SQL Server-Container. Dadurch können Sie einen neuen Container mit denselben Daten zu starten.

1. Beenden Sie den SQL Server-Container mit dem `docker stop` Befehl.

1. Erstellen Sie einen neuen SQL Server-Container mit `docker run` , und geben Sie ein Hostverzeichnis zugeordneten oder einen Volume-Container. Stellen Sie sicher, die bestimmte Tags für die SQL Server-Upgrade. Der neue Container verwendet jetzt eine neue Version von SQL Server mit Ihrer vorhandenen SQL Server-Daten.

   > [!IMPORTANT]
   > Upgrade wird nur zwischen RC1, RC2 und GA zu diesem Zeitpunkt unterstützt.

1. Überprüfen Sie Ihre Datenbanken und die Daten in den neuen Container.

1. Entfernen Sie optional den alten Container mit `docker rm`.

## <a id="troubleshooting"></a>Problembehandlung bei

Die folgenden Abschnitte enthalten Vorschläge zur Problembehandlung für SQL Server in Containern ausgeführt wird.

### <a name="docker-command-errors"></a>Fehler der Docker-Befehl

Wenn Sie für alle Fehler angezeigt werden `docker` Befehle, stellen Sie sicher, dass der Docker-Dienst ausgeführt wird, und führen Sie mit erweiterten Berechtigungen aus.

Beispielsweise unter Linux, möglicherweise erhalten Sie die folgende Fehlermeldung beim Ausführen `docker` Befehle:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Wenn Sie diesen Fehler für Linux erhalten, führen Sie den gleichen Befehlen mit vorangestelltem `sudo`. Wenn dies fehlschlägt, überprüfen Sie der Docker-Dienst ausgeführt wird, und starten Sie ihn bei Bedarf.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

Unter Windows stellen Sie sicher, dass Sie PowerShell oder die Eingabeaufforderung als Administrator starten.

### <a name="sql-server-container-startup-errors"></a>SQL Server-Container Startfehlern

Wenn der SQL Server-Container nicht ausgeführt werden, versuchen Sie die folgenden Tests:

- Wenn Sie eine Fehlermeldung, wie z. B. erhalten **"Fehler beim Erstellen des Endpunkts CONTAINER_NAME auf Netzwerkbrücke. Fehler beim Starten der Proxy: Überwachung Tcp 0.0.0.0:1433 Bind: Adresse wird bereits verwendet. "** , und Sie versuchen, die Container-Port 1433, der einen Port zugeordnet, die bereits verwendet wird. Dies kann geschehen, wenn Sie SQL Server lokal auf dem Hostcomputer ausgeführt werden. Es kann auch vorkommen, wenn Sie zwei SQL Server-Container starten und versuchen, sie beide auf demselben hostPort zuzuordnen. In diesem Fall verwenden die `-p` der Container-Port 1433 an einen anderen hostPort zuzuordnenden Parameters. Beispiel: 

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d microsoft/mssql-server-linux:2017-latest`.
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d microsoft/mssql-server-linux:2017-latest`.
    ```

- Überprüfen Sie, wenn Fehlermeldungen aus Container vorhanden sind.

    ```bash
    docker logs e69e056c702d
    ```

- Stellen Sie sicher, dass Sie den Arbeitsspeicher und Datenträger im angegebenen Mindestanforderungen der [Anforderungen](#requirements) Abschnitt dieses Themas.

- Wenn Sie einer Container-Management-Software verwenden, stellen Sie sicher, dass er als Stamm ausgeführten Container-Prozesse unterstützt. Sqlservr-Prozess im Container wird als Root ausgeführt werden.

- Überprüfen Sie die [Setup und SQL Server-Fehlerprotokollen](#errorlogs).

### <a name="enable-dump-captures"></a>Dump Erfassungen aktivieren

Wenn SQL Server-Prozess innerhalb des Containers ein Fehler auftritt, erstellen Sie einen neuen Container mit **SYS_PTRACE** aktiviert. Dadurch wird die Linux-Funktion, um einen Prozess zu verfolgen, der zum Erstellen einer Dumpdatei auf eine Ausnahme erforderlich ist. Die Dumpdatei kann hinsichtlich der Unterstützung verwendet werden, um Hilfe bei der Fehlerbehebung. Die folgenden "Docker run" Befehl ermöglicht diese Funktion.

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux:2017-latest
```

### <a name="sql-server-connection-failures"></a>SQL Server-Verbindungsfehler

Wenn Sie mit der SQL Server-Instanz, die in Ihrem Container ausgeführte herstellen können, versuchen Sie die folgenden Tests:

- Stellen Sie sicher, dass die SQL Server-Container ausgeführt wird, durch einen Blick auf die **STATUS** Spalte die `docker ps -a` Ausgabe. Verwenden Sie ggf. `docker start <Container ID>` , ihn zu starten.

- Wenn Sie einen nicht standardmäßiger hostPort (nicht 1433) zugeordnet, stellen Sie sicher, dass Sie den Port in der Verbindungszeichenfolge angeben. Sehen Sie die portzuordnung in der **PORTS** Spalte die `docker ps -a` Ausgabe. Der folgende Befehl verbindet z. B. Sqlcmd zu einem Container 1401-Port überwacht:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Bei Verwendung `docker run` mit einem vorhandenen zugeordneten Datenvolumen oder die Volume-Container für Daten, SQL Server ignoriert den Wert der `MSSQL_SA_PASSWORD`. Stattdessen wird das Kennwort vorkonfiguriert, dass SA aus den SQL Server-Daten in das Datenvolumen oder Data-Volume-Container verwendet. Stellen Sie sicher, dass Sie verknüpft sind mit den Daten, denen Sie anfügen möchten, an das SA-Kennwort verwenden.

- Überprüfen Sie die [Setup und SQL Server-Fehlerprotokollen](#errorlogs).

### <a name="sql-server-availability-groups"></a>SQL Server-Verfügbarkeitsgruppen

Wenn Sie Docker mit SQL Server-Verfügbarkeitsgruppen verwenden, sind zwei zusätzliche Anforderungen.

- Ordnen Sie den Port, der für die Replikat-Kommunikation (Standard 5022) verwendet wird. Geben Sie z. B. `-p 5022:5022` als Teil Ihrer `docker run` Befehl.

- Explizit den Hostnamen des Container durch Festlegen der `-h YOURHOSTNAME` Parameter von der `docker run` Befehl. Dieser Hostname wird verwendet, wenn Sie die Verfügbarkeitsgruppe konfigurieren. Wenn Sie nicht mit angeben `-h`, wird standardmäßig die Container-ID.

### <a id="errorlogs"></a>Setup und SQL Server-Fehlerprotokollen

SQL Server-Setup können Sie anzeigen und Fehlerprotokolle **/var/opt/mssql/log**. Wenn der Container nicht ausgeführt wird, starten Sie zuerst den Container aus. Verwenden Sie dann ein interaktives Befehlszeilen, um die Protokolle zu überprüfen.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

Führen Sie in der Bash-Sitzung innerhalb Ihres Containers die folgenden Befehle ein:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Wenn Sie ein Hostverzeichnis bereitgestellt **/var/opt/mssql** , wenn Sie den Container erstellt haben, können Sie stattdessen Suchen in der **Protokoll** Unterverzeichnis für den zugeordneten Pfad auf dem Host.

## <a name="next-steps"></a>Nächste Schritte

Erste Schritte mit SQL Server-2017 Container Bilder auf Docker durch das Durchlaufen der [quick Start-Lernprogramm](quickstart-install-connect-docker.md).

Siehe auch die [Mssql-Docker-GitHub-Repository](https://github.com/Microsoft/mssql-docker) für Ressourcen, Feedback und bekannte Probleme.

