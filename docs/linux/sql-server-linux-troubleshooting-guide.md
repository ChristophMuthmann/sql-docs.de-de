---
title: Problembehandlung bei SQLServer on Linux | Microsoft Docs
description: Bietet Tipps zur Problembehandlung für die Verwendung von SQL Server-2017 unter Linux.
author: annashres
ms.author: anshrest
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.workload: On Demand
ms.openlocfilehash: b3dc37601859ee4125f9f7885592e3a0653e8d0c
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="troubleshoot-sql-server-on-linux"></a>Problembehandlung bei SQLServer on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieses Dokument beschreibt die Behebung von Microsoft SQL Server unter Linux oder auf einem Docker-Container ausgeführt wird. Bei der Problembehandlung SQL Server on Linux Denken Sie daran, überprüfen die unterstützten Funktionen und bekannte Einschränkungen in der [SQL Server on Linux Release Notes](sql-server-linux-release-notes.md).

> [!TIP]
> Antworten auf häufig gestellte Fragen, finden Sie unter der [SQL Server on Linux – häufig gestellte Fragen](sql-server-linux-faq.md).

## <a id="connection"></a> Problembehandlung bei Verbindungsfehlern
Wenn Sie Probleme beim Herstellen einer Verbindung mit dem Linux-SQL-Server haben, sind einige Dinge überprüfen. 

- Stellen Sie sicher, dass der Servername oder IP-Adresse von Ihrem Clientcomputer erreichbar ist.

   > [!TIP]
   > Um die IP-Adresse des Computers Ubuntu zu finden, können Sie den Befehl Ifconfig wie im folgenden Beispiel ausführen:
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Für Red Hat können Sie die IP-Adresse wie im folgenden Beispiel gezeigt:
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > Eine Ausnahme zu diesem Verfahren bezieht sich auf Azure-VMs. Damit Azure-VMs [finden Sie die öffentliche IP-Adresse für den virtuellen Computer im Azure-Portal](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect).

- Sofern zutreffend, überprüfen Sie, dass Sie die SQL Server-Port (Standardport: 1433) in der Firewall geöffnet haben.

- Damit Azure-VMs, überprüfen Sie, ob Sie eine [Netzwerksicherheits-Gruppenregel für die SQL Server-Standardport](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote).

- Stellen Sie sicher, dass der Benutzername und das Kennwort nicht Tippfehler oder zusätzliche Leerzeichen oder falsche Groß-/Kleinschreibung enthalten.

- Versuchen Sie, das Protokoll und Port Anzahl durch den Servernamen, wie im folgenden Beispiel explizit festgelegt: **Tcp:servername 1433**.

- Verbindungsprobleme können auch Verbindungsfehlern und Timeouts führen. Überprüfen die Verbindungsinformationen und die Netzwerkkonnektivität, versuchen Sie es erneut, die Verbindung.

## <a name="manage-the-sql-server-service"></a>Verwalten des SQL Server-Diensts

Die folgenden Abschnitte zeigen, wie starten, beenden, neu starten und überprüfen Sie den Status des SQL Server-Diensts. 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Verwalten des Mssql--Serverdiensts unter Red Hat Enterprise Linux (RHEL) und Ubuntu 

Überprüfen Sie den Status des SQL Server-Dienst mit dem folgenden Befehl ein:

   ```bash
   sudo systemctl status mssql-server
   ```

Sie können beenden, starten oder starten Sie SQL Server-Dienst nach Bedarf mit den folgenden Befehlen neu:

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>Verwalten Sie die Ausführung der Mssql-Docker-container

Sie können Status und Container-ID des zuletzt erstellten SQL Server-Docker Containers abrufen, indem Sie den folgenden Befehl ausführen (die ID ist unter den **CONTAINER-ID** Spalte):

   ```bash
   sudo docker ps -l
   ```
   
Sie können beenden oder starten Sie SQL Server-Dienst nach Bedarf mit den folgenden Befehlen neu:
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Weitere Tipps zur Problembehandlung für Docker finden Sie unter [Problembehandlung bei SQL Server-Docker-Containern](sql-server-linux-configure-docker.md#troubleshooting).

## <a name="access-the-log-files"></a>Zugriff auf die Protokolldateien
   
Die SQL Server-Datenbankmodul-Protokollen zur /var/opt/mssql/log/errorlog-Datei in die Linux und die Docker-Installationen. Sie müssen im Modus "Superuser", dieses Verzeichnis durchsuchen.

Das Installationsprogramm hier protokolliert: / Var/opt/Mssql/Setup-< Zeitstempel, der Zeitpunkt der Installation der darstellt > können Sie durchsuchen, in die Errorlog-Dateien mit einem beliebigen kompatiblen UTF-16-Tool wie "Vim" oder "cat" wie folgt: 

   ```bash
   sudo cat errorlog
   ```

Falls gewünscht, können Sie auch die Dateien in UTF-8, zum Lesen mit konvertieren "more" oder "kleiner", mit dem folgenden Befehl:
   
   ```bash
   sudo iconv –f UTF-16LE –t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>Erweiterte Ereignisse

Erweiterte Ereignisse können über einen SQL-Befehl abgefragt werden.  Weitere Informationen zu erweiterten Ereignissen verwendbaren [hier](https://technet.microsoft.com/en-us/library/bb630282.aspx):

## <a name="crash-dumps"></a>Absturzabbilder 

Suchen Sie nach dem Speicherabbilder im Protokollverzeichnis bereit unter Linux. Überprüfen Sie, ob unter dem Verzeichnis /var/opt/mssql/log Linux Core dumps (. tar.gz2-Erweiterung) oder SQL Minidumps (Erweiterung ".mdmp")

Für Core dumps 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

Für SQL-dumps 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>Starten Sie SQLServer in der Minimalkonfiguration oder im Einzelbenutzermodus

### <a name="start-sql-server-in-minimal-configuration-mode"></a>Starten Sie SQLServer im Modus der Minimalkonfiguration
Dies ist hilfreich, wenn der Server aufgrund der Einstellung eines Konfigurationswerts (z. B. aufgrund von Arbeitsspeichermangel) nicht gestartet werden kann.
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>Starten Sie SQLServer im Einzelbenutzermodus
Unter bestimmten Umständen müssen Sie möglicherweise eine Instanz von SQL Server im Einzelbenutzermodus starten, mithilfe der Startoption-m. Dies ist z. B. der Fall, wenn Sie Serverkonfigurationsoptionen ändern oder eine beschädigte master-Datenbank oder andere Systemdatenbanken wiederherstellen möchten. Beispielsweise sollten Sie Serverkonfigurationsoptionen ändern oder eine beschädigte master-Datenbank oder andere Systemdatenbanken wiederherstellen   

Starten Sie SQLServer im Einzelbenutzermodus
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

Starten Sie SQLServer im Einzelbenutzermodus mit SQLCMD
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  Starten Sie SQL Server unter Linux mit dem Benutzer „MSSQL“, um zukünftige Startprobleme zu vermeiden. Beispiel „sudo-u mssql /opt/mssql/bin/sqlservr [STARTOPTIONEN]“ 

Wenn Sie versehentlich SQL Server mit einem anderen Benutzer gestartet haben, müssen Sie den Besitz von SQL Server-Datenbankdateien zurück an den Benutzer "Mssql" vor dem Starten von SQL Server mit Systemd ändern. Angenommen, um den Besitz aller Datenbankdateien unter /var/opt/mssql für den Benutzer "Mssql" zu ändern, führen Sie den folgenden Befehl

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="common-issues"></a>Häufige Probleme

1. Sie können nicht mit der Remoteinstanz von SQL Server verbinden.

   Finden Sie im Abschnitt "Problembehandlung" des Artikels, [Herstellen einer Verbindung mit SQL Server on Linux](#connection).

2. Fehler: Der Hostname muss 15 Zeichen lang sein oder weniger.

   Dies ist ein bekanntes Problem, das ausgeführt wird, wenn mehr als 15 Zeichen, der Namen des Computers, der versucht, den SQLServer-Debian-Paket installieren ist. Es gibt derzeit keine problemumgehungen als den Namen des Computers ändern. Eine Möglichkeit, dies zu erreichen, wird die Hostname-Datei bearbeiten und Neustart des Computers ab. Die folgenden [Website Handbuch](http://www.cyberciti.biz/faq/ubuntu-change-hostname-command/) wird dies im Detail erläutert.

3. Das System-Verwaltung (SA)-Kennwort zurücksetzen.

   Wenn Sie vergessen haben das Systemadministratorkennwort ("SA") oder einem anderen Grund zurücksetzen müssen, gehen Sie folgendermaßen vor.

   > [!NOTE]
   > Beenden Sie die folgenden Schritte aus den SQL Server-Dienst vorübergehend.

   Melden Sie sich bei der Host-Terminal, führen Sie die folgenden Befehle ein, und befolgen Sie die Anweisungen zum Zurücksetzen des SA-Kennworts:

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. Verwenden von Sonderzeichen in Kennwort.

   Wenn Sie einige Zeichen in der SQL Server-Anmeldekennwort verwenden müssen Sie sie mit Escapezeichen, wenn sie in der abschließenden Linux verwenden. Sie müssen die $ mit Escapezeichen versehen jedes Mal, wenn mit einem umgekehrten Schrägstrich verwenden Sie ihn in einem Terminalserver Befehls-Shell-Skript:

   Ist nicht geeignet:

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   Funktionsweise:

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   Ressourcen: [Sonderzeichen](http://tldp.org/LDP/abs/html/special-chars.html)
   [Escaping](http://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
