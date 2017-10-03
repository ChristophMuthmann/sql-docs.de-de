---
title: Planen von SSIS-Pakete auf Linux mit Cron | Microsoft Docs
description: In diesem Artikel zeigt, wie SQL Server Integration Services-Pakete auf Linux mit dem Cron-Dienst zu planen.
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 09/26/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: integration-services
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 31d5fb63a9c2a4d8825aa39c6fa7e3377ddc8d91
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>Zeitplan SQL Server Integration Services-paketausführung unter Linux mit cron

Beim Ausführen von SQL Server Integration Services (SSIS) und SQL Server unter Windows können Sie die Ausführung von SSIS-Paketen mit SQL Server-Agent automatisieren. Beim Ausführen von SQL Server- und SSIS auf Linux steht jedoch das SQL Server-Agent-Hilfsprogramm zum Planen von Aufträgen unter Linux. Verwenden Sie stattdessen **Cron** Dienst, der häufig unter Linux-Plattformen verwendet wird, um die Ausführung des Pakets zu automatisieren.

Dieser Artikel enthält Beispiele, die die Ausführung von SSIS-Paketen zu automatisieren. In den Beispielen wurden zur Ausführung auf Red Hat Enterprise geschrieben. Der Code ist ähnlich für andere Linux-Distributionen, z. B. Ubuntu.

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie die Cron-Diensts zum Ausführen von Aufträgen verwenden können, müssen Sie überprüfen, ob der Cron-Dienst auf Ihrem Computer ausgeführt wird.

Verwenden Sie folgenden Befehl aus, um den Status des Cron-Diensts zu überprüfen.

`systemctl status crond.service`

Wenn der Dienst nicht aktiv ist (d. h., nicht ausgeführt), wenden Sie sich an Ihren Administrator, um eingerichtet und den Cron-Dienst ordnungsgemäß konfiguriert.

## <a name="create-jobs"></a>Erstellen von Aufträgen

Ein Cron-Auftrag ist eine Aufgabe, die Sie konfigurieren können, um regelmäßig in einem angegebenen Intervall ausgeführt. Der Auftrag kann so einfach wie ein Befehl sein, die Sie normalerweise direkt in die Konsole eingeben oder als ein Shell-Skript ausführen würden.

Für einfache Verwaltung und Wartungszwecke wurde empfohlen, um die Ausführungsbefehle des Pakets in ein Skript mit einem aussagekräftigen Namen zu versetzen.

Hier ist ein einfaches Beispiel für ein Shellskript, das nur einzelnen Befehl zum Ausführen eines Pakets enthält. Sie können nach Bedarf weitere Befehle hinzufügen.

```
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Planen von Aufträgen mit der Cron-Diensts

Nachdem Sie Ihre Aufträge definiert haben, können Sie diese automatisch mithilfe des Cron-Diensts ausgeführt planen.

Wenn Ihr Auftrag für Cron auszuführende hinzufügen möchten, müssen Sie den Auftrag im Hinzufügen der `crontab` Datei. So öffnen die `crontab` Datei in einem Editor, in dem Hinzufügen oder aktualisieren den Auftrag, den folgenden Befehl verwenden:

`crontab -e`

Fügen Sie Informationen zum Planen des zuvor beschriebenen Auftrags täglich um 2:10:00 Uhr ausgeführt folgende Zeile auf die `crontab` Datei:

```
# run SSIS package Name at 2:10AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Speichern Sie die `crontab` Datei, und beenden Sie den Editor.

Überprüfen Sie die Informationen im folgenden Abschnitt, um das Format des beispielbefehls zu verstehen.
 
## <a name="format-of-a-crontab-file"></a>Format einer Crontab-Datei

Die folgende Abbildung zeigt die Format-Beschreibung der Auftrag Zeile hinzugefügt, die `crontab` Datei.

![Format-Beschreibung für den Eintrag in der Datei crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Eine ausführlichere Beschreibung des abzurufenden der `crontab` Dateiformat vorliegen, verwenden Sie den folgenden Befehl:

`man 5 crontab`

Hier ist eine partielle Beispiel der Ausgabe, die hilft, die im Beispiel in diesem Artikel wird erläutert:

![Ausführliche teilweise Beschreibung der Crontab-format](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

