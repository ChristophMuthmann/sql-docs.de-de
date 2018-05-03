---
title: Feedback von Kunden für SQLServer on Linux | Microsoft Docs
description: Beschreibt, wie SQL Server Feedback von Kunden aufgelistet und auf Linux konfiguriert ist.
author: annashres
ms.author: anshrest
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
ms.openlocfilehash: f495899a262ae31c99ee2409a06dcd09ee6c44c4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="customer-feedback-for-sql-server-on-linux"></a>Feedback von Kunden für SQLServer on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Microsoft SQL Server erfasst standardmäßig Informationen darüber, wie Kunden die Anwendung verwenden. Dies bedeutet, dass SQL Server Informationen zur Installationserfahrung, Nutzung und Leistung sammelt. Mit diesen Informationen kann Microsoft besser an die Bedürfnisse der Kunden anpassen. Microsoft erfasst z.B. Informationen zu Fehlercodes von Kunden, sodass wir damit verknüpfte Probleme beheben, die Dokumentation zu SQL Server verbessern und bestimmen können, ob wir dem Produkt weitere Funktionen hinzufügen müssen, um die Benutzererfahrung zu optimieren.

Dieses Dokument enthält ausführliche Informationen dazu, welche Arten von Informationen gesammelt werden und Informationen zum Konfigurieren von Microsoft SQL Server für Linux, um das gesammelten senden Informationen an Microsoft. SQL Server-2017 enthält eine Datenschutzrichtlinie, die welche Informationen erläutern wir führen und Sammeln von Benutzern nicht. Lesen Sie die Datenschutzrichtlinie an.

Microsoft sendet nicht die folgenden Informationen mit diesem Mechanismus:

- Werte aus Benutzertabellen
- Anmeldeinformationen oder andere Authentifizierungsinformationen
- personenbezogene Informationen (PII)

SQL Server 2017 erfasst und sammelt kontinuierlich Informationen zur Installationserfahrung des Einrichtungsvorgangs, damit wir schnell Installationsprobleme erkennen und beheben können, die der Kunde hat. 2017 von SQL Server kann konfiguriert werden, nicht, zum Senden von Informationen (regelmäßig Instanz pro Server) an Microsoft über **Mssql-Conf**. MSSQL-Conf ist ein Konfigurationsskript, der mit SQL Server-2017 für Red Hat Enterprise Linux, SUSE Linux Enterprise Server und Ubuntu installiert.

> [!NOTE]
> Sie können das Senden von Informationen an Microsoft nur in bezahlten Versionen von SQL Server deaktivieren.

## <a name="disable-customer-feedback"></a>Deaktivieren von Kundenfeedback

Diese Option können Sie ändern, wenn SQL Server Feedback an Microsoft oder ein nicht sendet. Dieser Wert wird standardmäßig festgelegt auf "true". Um den Wert zu ändern, führen Sie die folgenden Befehle ein:

### <a name="on-red-hat-suse-and-ubuntu"></a>Auf Red Hat und SUSE Ubuntu

1. Führen Sie das Skript Mssql-Conf als Root mit der **festgelegt** -Befehl für **telemetry.customerfeedback**. Im folgende Beispiel wird deaktiviert Kundenfeedback durch Angabe **"false"**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Starten Sie SQL Server-Dienst neu:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Für Docker
So deaktivieren Sie die Kundenfeedback auf Docker benötigen Sie Docker [behält Ihre Daten](sql-server-linux-configure-docker.md). 

1. Hinzufügen einer `mssql.conf` Datei mit den Zeilen `[telemetry]` und `customerfeedback = false` im Hostverzeichnis:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```
2. Führen Sie das Container-Bild
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="local-audit-for-sql-server-on-linux-usage-feedback-collection"></a>Lokale Überwachung für SQLServer on Linux Feedback Nutzungserfassung

2017 von Microsoft SQL Server enthält internetfähige Funktionen, die sammeln und Informationen zu Ihrem Computer oder Gerät ("Standardcomputerinformationen") an Microsoft senden können. Die lokale Überwachung-Komponente des SQL Server-Nutzung Feedback Auflistung kann auf den angegebenen Ordner Darstellung der Daten (Protokolle), die an Microsoft gesendet werden, vom Dienst gesammelten Daten schreiben. Der Zweck der lokalen Überwachung besteht darin, dass es Benutzern gestattet wird, alle Daten hinsichtlich Zustimmung, behördlicher Bestimmungen oder aus Datenschutzgründen anzuzeigen, die Microsoft mithilfe dieses Features erfasst.

In SQL Server unter Linux ist auf Instanzebene für SQL Server-Datenbankmodul lokale Überwachung konfigurierbar. Andere SQL Server-Komponenten und Tools für SQL Server müssen nicht lokale Überwachungsfunktion für die Sammlung von Verwendungsdaten Feedback.

### <a name="enable-local-audit"></a>Lokale Überwachung aktivieren

Diese Option ermöglicht lokalen Überwachung und das Verzeichnis festgelegt, in die lokale Überwachungsprotokolle erstellt werden.

1. Erstellen Sie ein Zielverzeichnis für neue lokale Überwachungsprotokolle ein. Das folgende Beispiel erstellt ein neues **/Tmp/Audit** Verzeichnis:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. Ändern Sie den Besitzer und die Gruppe des Verzeichnisses, das die **Mssql** Benutzer:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. Führen Sie das Skript Mssql-Conf als Root mit der **festgelegt** -Befehl für **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. Starten Sie SQL Server-Dienst neu:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Für Docker
Zum Aktivieren der lokalen Überwachung auf Docker benötigen Sie Docker [behält Ihre Daten](sql-server-linux-configure-docker.md). 

1. Das Zielverzeichnis für neue lokale Überwachungsprotokolle werden im Container. Erstellen Sie ein Zielverzeichnis für neue lokale Überwachungsprotokolle im Hostverzeichnis auf Ihrem Computer. Das folgende Beispiel erstellt ein neues **/audit** Verzeichnis:

   ```bash
   sudo mkdir <host directory>/audit
   ```

   
1. Hinzufügen einer `mssql.conf` Datei mit den Zeilen `[telemetry]` und `userrequestedlocalauditdirectory = <host directory>/audit` im Hostverzeichnis:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```
2. Führen Sie das Container-Bild
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu SQL Server unter Linux finden Sie unter der [Übersicht über die von SQL Server on Linux](sql-server-linux-overview.md).
