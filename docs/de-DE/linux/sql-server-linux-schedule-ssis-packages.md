---
title: Planen von SSIS-Pakete auf Linux mit Cron | Microsoft Docs
description: Dieser Artikel beschreibt die Vorgehensweise beim Planen von SQL Server Integration Services (SSIS)-Pakete auf Linux mit dem Cron-Dienst.
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 880f5f9060bb47e5cdf4de1567251f541c2628b6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>Zeitplan SQL Server Integration Services-paketausführung unter Linux mit cron

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Beim Ausführen von SQL Server Integration Services (SSIS) und SQL Server unter Windows können Sie die Ausführung von SSIS-Paketen mit SQL Server-Agent automatisieren. Beim Ausführen von SQL Server- und SSIS auf Linux steht jedoch das SQL Server-Agent-Hilfsprogramm zum Planen von Aufträgen unter Linux. Verwenden Sie stattdessen die Cron-Diensts, was häufig auf Linux-Plattformen verwendet wird, um die Ausführung des Pakets zu automatisieren.

Dieser Artikel enthält Beispiele, die die Ausführung von SSIS-Paketen zu automatisieren. Die Beispiele sind zur Ausführung auf Red Hat Enterprise geschrieben. Der Code ist ähnlich für andere Linux-Distributionen, z. B. Ubuntu.

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie die Cron-Diensts zum Ausführen von Aufträgen verwenden, überprüfen Sie, ob sie auf Ihrem Computer ausgeführt wird.

Um den Status des Cron-Diensts zu überprüfen, verwenden Sie den folgenden Befehl: `systemctl status crond.service`.

Wenn der Dienst nicht aktiv ist (d. h. er wird nicht ausgeführt), wenden Sie sich an Ihren Administrator, um eingerichtet und den Cron-Dienst ordnungsgemäß konfiguriert.

## <a name="create-jobs"></a>Erstellen von Aufträgen

Ein Cron-Auftrag ist eine Aufgabe, die Sie konfigurieren können, um regelmäßig in einem angegebenen Intervall ausgeführt. Der Auftrag kann so einfach wie ein Befehl sein, die Sie normalerweise direkt in die Konsole eingeben oder als ein Shell-Skript ausführen würden.

Für einfache Verwaltung und Wartungszwecke wird empfohlen, dass Sie die Ausführung des Pakets Befehle in einem Skript einfügen, das einen beschreibenden Namen enthält.

Hier ist ein Beispiel für eine einfache Shell-Skript zum Ausführen eines Pakets. Sie enthält nur einen einzelnen Befehl, aber Sie können weitere Befehle hinzufügen, wie erforderlich.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Planen von Aufträgen mit der Cron-Diensts

Nachdem Sie Ihre Aufträge definiert haben, können Sie diese automatisch mithilfe des Cron-Diensts ausgeführt planen.

Um Ihren Auftrag für Cron auszuführende hinzuzufügen, fügen Sie den Auftrag in der Datei Crontab hinzu. Verwenden Sie zum Öffnen der Datei Crontab in einem Editor, in dem Hinzufügen oder aktualisieren den Auftrag, den folgenden Befehl: `crontab -e`.

Fügen Sie die folgende Zeile in die Datei Crontab, Informationen zum Planen des zuvor beschriebenen Auftrags täglich um 2:10 Uhr ausgeführt:

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Speichern Sie die Crontab-Datei, und beenden Sie den Editor.

Überprüfen Sie die Informationen im folgenden Abschnitt, um das Format des beispielbefehls zu verstehen.
 
## <a name="format-of-a-crontab-file"></a>Format einer Crontab-Datei

Die folgende Abbildung zeigt die Format-Beschreibung der Auftrag an, das die Crontab-Datei hinzugefügt wird.

![Format-Beschreibung für den Eintrag in der Datei crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Um eine ausführlichere Beschreibung des Dateiformats Crontab zu erhalten, verwenden Sie den folgenden Befehl: `man 5 crontab`.

Hier ist eine partielle Beispiel der Ausgabe, die hilft, die im Beispiel in diesem Artikel wird erläutert:

![Ausführliche teilweise Beschreibung der Crontab-format](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>Verwandte Inhalte über SSIS unter Linux
-   [Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS](sql-server-linux-migrate-ssis.md)
-   [Installieren von SQL Server Integration Services (SSIS) unter Linux](sql-server-linux-setup-ssis.md)
-   [Konfigurieren von SQL Server Integration Services unter Linux mit Ssis-conf](sql-server-linux-configure-ssis.md)
-   [Einschränkungen und bekannten Probleme für SSIS unter Linux](sql-server-linux-ssis-known-issues.md)
