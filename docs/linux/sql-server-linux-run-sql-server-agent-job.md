---
title: "Erstellen und Ausführen von Aufträgen für SQL Server on Linux | Microsoft Docs"
description: "In diesem Lernprogramm wird gezeigt, wie SQL Server-Agent-Auftrag auf dem Linux ausgeführt wird."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3ffb76838940f42d7a696e1c17f227517d89012d
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>Erstellen und Ausführen von SQL Server-Agent-Aufträge unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server-Aufträge werden verwendet, um regelmäßig die gleiche Sequenz von Befehlen in der SQL Server-Datenbank ausführen. Dieses Thema enthält Beispiele zum Erstellen von SQL Server-Agent-Aufträge unter Linux mit Transact-SQL und SQL Server Management Studio (SSMS).

Bekannte Probleme mit SQL Server-Agent in dieser Version finden Sie unter der [Release Notes](sql-server-linux-release-notes.md).

## <a name="prerequisites"></a>Erforderliche Komponenten 
Zum Erstellen und Ausführen von Aufträgen, müssen Sie zunächst den SQL Server-Agent-Dienst installieren. Installationsanweisungen finden Sie unter der [Thema der SQL Server-Agent-Installation](sql-server-linux-setup-sql-agent.md).

## <a name="create-a-job-with-transact-sql"></a>Erstellen eines Auftrags mit Transact-SQL

Die folgenden Schritte bieten ein Beispiel zum Erstellen eines SQL Server-Agent-Auftrags unter Linux mit Transact-SQL-Befehlen. Dieser Auftrag in diesem Beispiel führt tägliche eine Sicherung auf einer Beispieldatenbank `SampleDB`. 


> [!TIP]
> Alle T-SQL-Client können Sie diese Befehle werden ausgeführt. Beispielsweise unter Linux können Sie [Sqlcmd](sql-server-linux-setup-tools.md) oder [Visual Studio Code](sql-server-linux-develop-use-vscode.md). Von einem Remoteserver mit Windows können Sie auch Ausführen von Abfragen in SQL Server Management Studio (SSMS) oder mithilfe der UI-Schnittstelle für die auftragsverwaltung, die im nächsten Abschnitt beschrieben wird.

1. **Erstellen des Auftrags**. Im folgenden Beispiel wird [Sp_add_job](https://msdn.microsoft.com/library/ms182079.aspx) beim Erstellen eines Auftrags mit dem Namen `Daily AdventureWorks Backup`.

    ```tsql
     -- Adds a new job executed by the SQLServerAgent service 
     -- called 'Daily SampleDB Backup'  
     CREATE DATABASE SampleDB
     USE msdb ;  
     GO  
     EXEC dbo.sp_add_job  
         @job_name = N'Daily SampleDB Backup' ;  
     GO

    ```

2. **Fügen Sie eine oder mehrere Auftragsschritte**. Das folgende Transact-SQL-Skript verwendet [Sp_add_jobstep](https://msdn.microsoft.com/library/ms187358.aspx) Sie einen Auftragsschritt zu erstellen, eine Sicherung erstellt, die `AdventureWlorks2014` Datenbank.

    ```tsql
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

3. **Erstellen Sie einen Auftragszeitplan**. Dieses Beispiel verwendet [Sp_add_schedule](https://msdn.microsoft.com/library/ms366342.aspx) um einen täglichen Zeitplan für den Auftrag zu erstellen.

    ```tsql
    -- Creates a schedule called 'Daily'  
    EXEC dbo.sp_add_schedule  
     @schedule_name = N'Daily SampleDB',  
     @freq_type = 4,  
     @freq_interval = 1,
     @active_start_time = 233000 ;  
   USE msdb ;  
   GO
    ```

4. **Fügen Sie den Auftragszeitplan an den Auftrag**. Verwendung [Sp_attach_schedule](https://msdn.microsoft.com/library/ms186766.aspx) den Auftragszeitplan an dem Auftrag angefügt.

    ```tsql
    -- Sets the 'Daily' schedule to the 'Daily AdventureWorks Backup' Job  
    EXEC sp_attach_schedule  
     @job_name = N'Daily SampleDB Backup',  
     @schedule_name = N'Daily SampleDB';  
    GO
    ```

5. **Weisen Sie den Auftrag auf einem Zielserver**. Weisen Sie den Auftrag auf einem Zielserver mit [Sp_add_jobserver](https://msdn.microsoft.com/library/ms178625.aspx). In diesem Beispiel ist der lokale Server das Ziel.

    ```tsql
    EXEC dbo.sp_add_jobserver  
     @job_name = N'Daily SampleDB Backup',  
     @server_name = N'(LOCAL)';  
    GO
    ```
6. **Starten Sie den Auftrag**. 

    ```tsql
    EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
    GO
    ```
## <a name="create-a-job-with-ssms"></a>Erstellen eines Auftrags mit SSMS

Sie können auch erstellen und verwalten Aufträge mehr Remote mit SQL Server Management Studio (SSMS) unter Windows.

1. **Starten Sie SSMS unter Windows, und Verbinden mit Ihrer Linux SQL Server-Instanz.** Weitere Informationen finden Sie unter [Verwalten von SQL Server unter Linux mit SSMS](sql-server-linux-develop-use-ssms.md).

1. **Erstellen Sie eine neue Datenbank mit der Bezeichnung SampleDB**.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

2. **Stellen Sie sicher, dass SQL-Agent installiert und ordnungsgemäß konfiguriert wurde.** Suchen Sie auf das Pluszeichen neben SQL Server-Agent im Objekt-Explorer. Wenn SQL Server-Agent nicht installiert ist, finden Sie unter [Installieren von SQL Server-Agent für Linux](sql-server-linux-setup-sql-agent.md).

    ![Stellen Sie sicher, dass SQL Server-Agent installiert wurde](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)


3. **Erstellen Sie einen neuen Auftrag.**

    ![Einen neuen Auftrag erstellen](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)


4. **Benennen Sie Ihre Arbeit und erstellen Sie Ihre Auftragsschritt zu.**

    ![Erstellen eines Auftragsschritts](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)


5. **Geben Sie, welche Subsystem, das Sie verwenden möchten und welche Aktion der Auftragsschritt ausführen soll.**

    ![Auftrags-subsystem](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

    ![Schritt Auftragsaktion](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

6. **Erstellen Sie einen neuen Auftragszeitplan.**

    ![Auftragszeitplan](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)
  
    ![Auftragszeitplan](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

7. **Starten Sie Ihren Auftrag ein.**

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Erstellen und Verwalten von SQL Server-Agent-Aufträgen finden Sie unter [SQL Server-Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent).

