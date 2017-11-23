---
title: "Erstellen und Ausführen von Aufträgen für SQL Server on Linux | Microsoft Docs"
description: "In diesem Lernprogramm wird gezeigt, wie SQL Server-Agent-Auftrag auf dem Linux ausgeführt wird."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.workload: Inactive
ms.openlocfilehash: 93fd18e532605d4ce9dfe0ee705d05297136cbd4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>Erstellen und Ausführen von SQL Server-Agent-Aufträge unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server-Aufträge werden verwendet, um regelmäßig die gleiche Sequenz von Befehlen in der SQL Server-Datenbank ausführen. Dieses Lernprogramm enthält ein Beispiel zum Erstellen eines SQL Server-Agent-Auftrags unter Linux mit Transact-SQL und SQL Server Management Studio (SSMS).

> [!div class="checklist"]
> * Installieren von SQL Server-Agent für Linux
> * Erstellen Sie zum Durchführen von täglichen datenbanksicherungen einen neuen Auftrag
> * Planen und Ausführen des Auftrags
> * Führen Sie die gleichen Schritte aus, in SSMS (optional)

Bekannte Probleme mit SQL Server-Agent für Linux finden Sie unter der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Die folgenden Voraussetzungen sind erforderlich, um dieses Lernprogramm abzuschließen:

* Linux-Computer mit den folgenden Voraussetzungen:
  * SQL Server-2017 ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), oder [Ubuntu](quickstart-install-connect-ubuntu.md)) mit den Befehlszeilentools.

Die folgenden erforderlichen Komponenten sind optional:

* Windows-Computer mit SSMS:
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) für optionale SSMS Schritte.

## <a name="install-sql-server-agent"></a>Installieren von SQL Server-Agent

Um SQL Server-Agent für Linux verwenden, installieren Sie zuerst die **Mssql-Server-Agent** Paket auf einem Computer, die bereits von SQL Server-2017 installiert.

1. Installieren Sie **Mssql-Server-Agent** mit den entsprechenden Befehl für Ihr Betriebssystem Linux.

   | Platform | Installation Befehle |
   |-----|-----|
   | RHEL | `sudo yum install mssql-server-agent` |
   | SLES | `sudo zypper refresh`<br/>`sudo zypper update mssql-server-agent` |
   | Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server-agent` |

1. Starten Sie SQL Server mit dem folgenden Befehl ein:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="create-a-sample-database"></a>Erstellen einer Beispieldatenbank

Verwenden Sie die folgenden Schritte zum Erstellen einer Beispieldatenbank mit dem Namen **SampleDB**. Diese Datenbank ist für den täglichen Sicherungsauftrag verwendet.

1. Öffnen Sie eine terminal Bash-Sitzung, auf dem Linux-Computer.

1. Verwendung **Sqlcmd** zum Ausführen einer Transact-SQL **CREATE DATABASE** Befehl.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. Stellen Sie sicher, dass die Datenbank erstellt wird, indem Sie die Datenbanken auf dem Server auflisten.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>Erstellen eines Auftrags mit Transact-SQL

Die folgenden Schritte erstellen einen SQL Server-Agent-Auftrag unter Linux mit Transact-SQL-Befehlen. Der Auftrag ausgeführt wird, tägliche eine Sicherung der-Beispieldatenbank, **SampleDB**.

> [!TIP]
> Alle T-SQL-Client können Sie diese Befehle werden ausgeführt. Beispielsweise unter Linux können Sie [Sqlcmd](sql-server-linux-setup-tools.md) oder [Visual Studio Code](sql-server-linux-develop-use-vscode.md). Von einem Remoteserver mit Windows können Sie auch Ausführen von Abfragen in SQL Server Management Studio (SSMS) oder mithilfe der UI-Schnittstelle für die auftragsverwaltung, die im nächsten Abschnitt beschrieben wird.

1. Verwendung [Sp_add_job](../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md) beim Erstellen eines Auftrags mit dem Namen `Daily SampleDB Backup`.

   ```sql
   -- Adds a new job executed by the SQLServerAgent service
   -- called 'Daily SampleDB Backup'
   USE msdb ;
   GO
   EXEC dbo.sp_add_job
      @job_name = N'Daily SampleDB Backup' ;
   GO
   ```

1. Rufen Sie [Sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md) Sie einen Auftragsschritt zu erstellen, eine Sicherung erstellt, die `SampleDB` Datenbank.

   ```sql
   -- Adds a step (operation) to the job
   EXEC sp_add_jobstep
      @job_name = N'Daily SampleDB Backup',
      @step_name = N'Backup database',
      @subsystem = N'TSQL',
      @command = N'BACKUP DATABASE SampleDB TO DISK = \
         N''/var/opt/mssql/data/SampleDB.bak'' WITH NOFORMAT, NOINIT, \
         NAME = ''SampleDB-full'', SKIP, NOREWIND, NOUNLOAD, STATS = 10',
      @retry_attempts = 5,
      @retry_interval = 5 ;
   GO
   ```

1. Erstellen Sie einen täglichen Zeitplan für den Auftrag mit [Sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md).

   ```sql
   -- Creates a schedule called 'Daily'
   EXEC dbo.sp_add_schedule
      @schedule_name = N'Daily SampleDB',
      @freq_type = 4,
      @freq_interval = 1,
      @active_start_time = 233000 ;
   USE msdb ;
   GO
   ```

1. Fügen Sie dem Auftrag mit den Auftragszeitplan [Sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md).

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. Verwendung [Sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md) ein Zielserver den Auftrag zuweisen. In diesem Beispiel ist das Ziel des lokalen Servers.

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. Starten des Auftrags mit der [Sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>Erstellen eines Auftrags mit SSMS

Sie können auch erstellen und verwalten Aufträge mehr Remote mit SQL Server Management Studio (SSMS) unter Windows.

1. Starten Sie SSMS unter Windows, und Verbinden mit Ihrer Linux SQL Server-Instanz. Weitere Informationen finden Sie unter [Verwalten von SQL Server unter Linux mit SSMS](sql-server-linux-develop-use-ssms.md).

1. Stellen Sie sicher, dass Sie eine Beispieldatenbank mit dem Namen erstellt haben **SampleDB**.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. Stellen Sie sicher, dass die SQL-Agent war [installiert](sql-server-linux-setup-sql-agent.md) und ordnungsgemäß konfiguriert. Suchen Sie auf das Pluszeichen neben SQL Server-Agent im Objekt-Explorer. Wenn SQL Server-Agent nicht aktiviert ist, starten Sie den **Mssql Server** -Dienst unter Linux.

   ![Stellen Sie sicher, dass SQL Server-Agent installiert wurde](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. Erstellen Sie einen neuen Auftrag.

   ![Einen neuen Auftrag erstellen](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. Benennen Sie Ihre Arbeit und erstellen Sie Ihre Auftragsschritt zu.

   ![Erstellen eines Auftragsschritts](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. Geben Sie, welche Subsystem, das Sie verwenden möchten und welche Aktion der Auftragsschritt ausführen soll.

   ![Auftrags-subsystem](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![Schritt Auftragsaktion](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. Erstellen Sie einen neuen Auftragszeitplan.

   ![Auftragszeitplan](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![Auftragszeitplan](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. Starten Sie Ihren Auftrag ein.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>Nächste Schritte

In diesem Lernprogramm haben Sie gelernt, wie:

> [!div class="checklist"]
> * Installieren von SQL Server-Agent für Linux
> * Verwenden von Transact-SQL und gespeicherte Systemprozeduren zur Erstellung von Aufträgen
> * Erstellen eines Auftrags, das tägliche datenbanksicherungen ausführt.
> * Verwenden von SSMS UI erstellen und Verwalten von Aufträgen

Als Nächstes lernen Sie andere Funktionen zum Erstellen und Verwalten von Aufträgen:

> [!div class="nextstepaction"]
>[SQL Server-Agent-Dokumentation](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
