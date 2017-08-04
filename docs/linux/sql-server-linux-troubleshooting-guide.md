---
title: Problembehandlung bei SQLServer on Linux | Microsoft Docs
description: "Bietet Tipps zur Problembehandlung für die Verwendung von SQL Server-2017 unter Linux."
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 05/08/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 21b7d94bcf15e1ae2d99dd44f4b0030929b92111
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="troubleshoot-sql-server-on-linux"></a>Problembehandlung bei SQLServer on Linux

Dieses Dokument beschreibt die Behebung von Microsoft SQL Server unter Linux oder auf einem Docker-Container ausgeführt wird. Stellen Sie die Einschränkungen dieser privaten Preview-Version Denken Sie daran, bei der Problembehandlung SQL Server on Linux. Sie finden eine Liste dieser in der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md).

## <a id="connection"></a>Problembehandlung bei Verbindungsfehlern
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
   > Eine Ausnahme zu diesem Verfahren bezieht sich auf Azure-VMs. Damit Azure-VMs [finden Sie die öffentliche IP-Adresse für den virtuellen Computer im Azure-Portal](sql-server-linux-azure-virtual-machine.md#connect).

- Sofern zutreffend, überprüfen Sie, dass Sie die SQL Server-Port (Standardport: 1433) in der Firewall geöffnet haben.

- Damit Azure-VMs, überprüfen Sie, ob Sie eine [Netzwerksicherheits-Gruppenregel für die SQL Server-Standardport](sql-server-linux-azure-virtual-machine.md#remote).

- Stellen Sie sicher, dass der Benutzername und das Kennwort nicht Tippfehler oder zusätzliche Leerzeichen oder falsche Groß-/Kleinschreibung enthalten.

- Versucht, explizit die Anzahl Protokoll und Port mit dem Namen des Servers wie folgt festgelegt: **Tcp:servername 1433**.

- Verbindungsprobleme können auch Verbindungsfehlern und Timeouts führen. Überprüfen die Verbindungsinformationen und die Netzwerkkonnektivität, versuchen Sie es erneut, die Verbindung.

## <a name="manage-the-sql-server-service"></a>Verwalten des SQL Server-Diensts

Die folgenden Abschnitte zeigen, wie starten, beenden, neu starten und überprüfen Sie den Status des SQL Server-Diensts. 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Verwalten des Mssql--Serverdiensts unter Red Hat Enterprise Linux (RHEL) und Ubuntu 

Überprüfen Sie den Status des Status des SQL Server-Dienst mit dem folgenden Befehl ein:

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

Sie erhalten den Status und Container-ID des zuletzt erstellten SQL Server-Docker Containers mithilfe des folgenden Befehls (die ID ist unter der Spalte "CONTAINER-ID"):

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

## <a name="common-issues"></a>Häufige Probleme

1. Sie können nicht mit der Remoteinstanz von SQL Server verbinden.

   Finden Sie im Problembehandlungsabschnitt im Thema [Herstellen einer Verbindung mit SQL Server on Linux](#connection).

2. Fehler: Der Hostname muss 15 Zeichen lang sein oder weniger.

   Dies ist ein bekanntes Problem, das ausgeführt wird, wenn mehr als 15 Zeichen, der Namen des Computers, der versucht, den SQLServer-Debian-Paket installieren ist. Es gibt derzeit keine problemumgehungen als den Namen des Computers ändern. Eine Möglichkeit, dies zu erreichen, wird die Hostname-Datei bearbeiten und Neustart des Computers ab. Die folgenden [Website Handbuch](http://www.cyberciti.biz/faq/ubuntu-change-hostname-command/) wird dies im Detail erläutert.

3. Das System-Verwaltung (SA)-Kennwort zurücksetzen.

   Wenn Sie die System-Administrator ("SA")-Kennwort vergessen haben oder sie einem anderen Grund zurückgesetzt müssen gehen Sie folgendermaßen vor.

   > [!NOTE]
   > Diese Schritte wird die SQL Server-Dienst vorübergehend zu beenden.

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

## <a name="support"></a>Support

Der Support ist über die Community zur Verfügung und überwachten, von dem engineering-Team. Antworten auf Fragen verwenden Sie die folgenden Ressourcen:

- [DBA-Stapel Exchange](https://dba.stackexchange.com/questions/tagged/sql-server): Datenbank-Verwaltung Fragen
- [Stapelüberlauf](http://stackoverflow.com/questions/tagged/sql-server): Fragen für die Entwicklung
- [MSDN-Foren](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): technische Fragen
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): Melden von Fehlern und Anforderung-Funktion
- [Reddit](https://www.reddit.com/r/SQLServer/): Besprechen Sie SQLServer
