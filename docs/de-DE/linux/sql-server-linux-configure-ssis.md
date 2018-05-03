---
title: Konfigurieren von SSIS unter Linux mit Ssis-Conf | Microsoft Docs
description: Dieser Artikel beschreibt das Konfigurieren von SQL Server Integration Services (SSIS) unter Linux mit dem Ssis-Conf-Hilfsprogramm.
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
ms.openlocfilehash: 1858b0d6db8d54ff54b507de348b2a6764165dc8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>Konfigurieren von SQL Server Integration Services unter Linux mit Ssis-conf

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Sie führen die `ssis-conf` Konfigurationsskript bei der Installation von SQL Server Integration Services (SSIS) für Red Hat Enterprise Linux und Ubuntu. Weitere Informationen zum Installieren von SSIS finden Sie unter [installieren Sie SQL Server Integration Services (SSIS) unter Linux](sql-server-linux-setup-ssis.md).

Sie können auch die `ssis-conf` Hilfsprogramm so konfigurieren Sie die folgenden Eigenschaften:

| Befehl | Description |
|-------------|---------------------------------------------------------------------|
| Set-edition | Legen Sie die Edition von SQL Server                                       |
| Telemetrie   | Aktivieren Sie oder deaktivieren Sie der telemetriedienst für SQL Server Integration Services |
| Setup       | Initialisieren und Einrichten von Microsoft SQL Server Integration Services      |
|||

## <a name="run-ssis-conf"></a>Ausführen von Ssis-conf

In den Beispielen in diesem Artikel ausführen `ssis-conf` durch den vollständigen Pfad angeben: `/opt/ssis/bin/ssis-conf`. Wenn Sie zu diesem Speicherort navigieren, vor dem Ausführen `ssis-conf`, führen Sie das Hilfsprogramm im Kontext des aktuellen Verzeichnisses: `./ssis-conf`.

Achten Sie darauf, dass die Befehle, die beschrieben werden in diesem Artikel mit Root-Berechtigungen ausgeführt. Führen Sie z. B. `sudo /opt/ssis/bin/ssis-conf setup` und nicht `/opt/ssis/bin/ssis-conf setup`.

Führen Sie diese Befehle mit Abfragen in der Sprache, die Sie lieber können Sie ein Gebietsschema angeben. Angenommen, um aufforderungen auf Chinesisch zu erhalten, führen den folgenden Befehl: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>Verwenden Sie Set-Edition, um die Edition von SQL Server Integration Services festzulegen

Die Edition von SSIS wird mit der Edition von SQL Server ausgerichtet.

Geben Sie den folgenden Befehl: `$ sudo /opt/ssis/bin/ssis-conf set-edition`.

Nachdem Sie den Befehl eingegeben haben, erhalten Sie die folgende Meldung angezeigt:

```
Choose an edition of SQL Server:

1) Evaluation (free, no production use rights, 180-day limit)

2) Developer (free, no production use rights)

3) Express (free)

4) Web (PAID)

5) Standard (PAID)

6) Enterprise (PAID)

7) Enterprise Core (PAID)

8) I bought a license through a retail sales channel and have a product key to enter.

Details about editions can be found at https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409.

Use of PAID editions of this software requires separate licensing through a Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate number of licenses in place to install and run this software.

Enter your edition (1-8):
```

Wenn Sie einen Wert von 1 bis 7 eingeben, wird das System eine Edition kostenlose oder bezahlt konfiguriert. Wenn Sie auf "8" eingeben, fordert das Dienstprogramm Sie den Product Key eingeben, den Sie gekauft haben:

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>Verwenden Sie Telemetrie, um Kundenfeedback zu konfigurieren

Die `telemetry` Befehl wird bestimmt, ob SSIS Feedback an Microsoft sendet.

Für kostenlose Editionen (d. h. Express, Developer und Evaluation-Editionen) ist der telemetriedienst immer aktiviert. Wenn Sie eine kostenlose Edition haben, können keine der `telemetry` Befehl zum Deaktivieren der Telemetrie.

Geben Sie den folgenden Befehl: `$ sudo /opt/ssis/bin/ssis-conf telemetry`.

Für bezahlte Editionen Nachdem Sie den Befehl aus, geben Sie erhalten die folgende Meldung Sie:

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

Bei Auswahl des **Ja**, der telemetriedienst aktiviert ist und ausgeführt wird. Der Dienst startet automatisch nach jedem Startvorgang. Bei Auswahl des **keine**, der telemetriedienst beendet und ist deaktiviert.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>Mithilfe von Setup initialisieren und Einrichten von Microsoft SQL Server Integration Services

Verwenden der `setup` Befehl jedes Mal, wenn Sie SSIS installieren.

Geben Sie den folgenden Befehl: `sudo /opt/ssis/bin/ssis-conf setup`.

Das Hilfsprogramm fordert Ihre bestätigen oder geben Sie Werte für die folgenden Elemente:
-   Produktlizenz
-   Endbenutzer-Lizenzvertrag
-   Telemetriedienst
-   Die von Integration Services verwendete Sprache

Zum Ausführen der `setup` Befehl mit den Anweisungen in der Sprache, mit dem Sie es vorziehen, können Sie ein Gebietsschema angeben. Angenommen, um aufforderungen auf Chinesisch zu erhalten, führen den folgenden Befehl: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="ssisconf-format"></a>SSIS.conf-format

Die folgenden `/var/opt/ssis/ssis.conf` Datei bietet ein Beispiel für jede Einstellung.

Für SQL Server, können Sie Systemeinstellungen ändern, indem die Werte in der `mssql.conf` Datei. Für SSIS die Sie *kann nicht* Systemeinstellungen ändern, indem Sie die Werte in der `ssis.conf` Datei. Die `ssis.conf` -Datei zeigt nur die Ergebnisse der Installation. Wenn Sie die Einstellungen für SSIS ändern möchten, können Sie löschen die `ssis.conf` , und führen Sie die `setup` erneut aus.

Hier ist ein Beispiel für `ssis.conf` Datei. Jedes Feld entspricht das Ergebnis des einschrittigen Installation.

```
[LICENSE]
                       
registered = Y        
                       
pid = enterprisecore  
                       
[EULA]
                       
accepteula = Y        
                       
[TELEMETRY]
                       
enabled = Y           
                       
[language]
                       
lcid = 2052
```

## <a name="related-content-about-ssis-on-linux"></a>Verwandte Inhalte über SSIS unter Linux
-   [Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS](sql-server-linux-migrate-ssis.md)
-   [Installieren von SQL Server Integration Services (SSIS) unter Linux](sql-server-linux-setup-ssis.md)
-   [Einschränkungen und bekannten Probleme für SSIS unter Linux](sql-server-linux-ssis-known-issues.md)
-   [Zeitplan SQL Server Integration Services-paketausführung unter Linux mit cron](sql-server-linux-schedule-ssis-packages.md)
