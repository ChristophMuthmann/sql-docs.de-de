---
title: Erstellen eines Transact-SQL-Auftragsschritts | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: 69c571a7-debe-4063-9d38-e4b6a1e8e84c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 30d692969db247383010a268c9dd58ee5d2bd3ea
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-transact-sql-job-step"></a>Erstellen eines Transact-SQL-Auftragsschritts
In diesem Thema wird beschrieben, wie Sie einen Auftragsschritt des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents, der [!INCLUDE[tsql](../../includes/tsql_md.md)] - Skripts in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)]oder SQL Server Management Objects ausführt, erstellen können.  
  
Diese Auftragsschrittskripts können gespeicherte Prozeduren und erweiterte gespeicherte Prozeduren aufrufen. Ein einzelner [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschritt kann mehrere Batches und eingebettete GO-Befehle enthalten. Weitere Informationen zum Erstellen eines Auftrags finden Sie unter [Erstellen von Aufträgen](../../ssms/agent/create-jobs.md).  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **So erstellen Sie einen Transact-SQL-Auftragsschritt mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-create-a-transact-sql-job-step"></a>So erstellen Sie einen Transact-SQL-Auftragsschritt  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **SQL Server-Agent**, erstellen Sie einen neuen Auftrag, oder klicken Sie mit der rechten Maustaste auf einen vorhandenen Auftrag, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **Auftragseigenschaften** auf die Seite **Schritte** und dann auf **Neu**.  
  
4.  Geben Sie im Dialogfeld **Neuer Auftragsschritt** unter **Schrittname**einen Schrittnamen für den Auftrag ein.  
  
5.  Klicken Sie in der Liste **Typ** auf **Transact-SQL-Skript (TSQL)**.  
  
6.  Geben Sie im Feld **Befehl** die [!INCLUDE[tsql](../../includes/tsql_md.md)] -Befehlsbatches ein, oder klicken Sie auf **Öffnen** , um eine [!INCLUDE[tsql](../../includes/tsql_md.md)] -Datei auszuwählen, die als Befehl verwendet werden soll.  
  
7.  Klicken Sie auf **Analysieren** , um die Syntax zu überprüfen.  
  
8.  Wenn die Syntax richtig ist, wird die Meldung "Analyse erfolgreich" angezeigt. Wenn ein Fehler gefunden wird, müssen Sie die Syntax korrigieren, bevor Sie den Vorgang fortsetzen.  
  
9. Klicken Sie auf die Seite **Erweitert** , um Optionen für Auftragsschritte festzulegen, z.&nbsp;B. welche Aktion ausgeführt werden soll, wenn ein Auftragsschritt erfolgreich ausgeführt wird oder einen Fehler erzeugt, wie häufig der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent versuchen soll, den Auftragsschritt auszuführen, und in welche Datei oder Tabelle der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent die Auftragsschrittausgabe schreiben soll. Nur Mitglieder der festen Serverrolle **sysadmin** können die Auftragsschrittausgabe in eine Betriebssystemdatei schreiben. Alle Benutzer des SQL Server-Agents können die Ausgabe in einer Tabelle protokollieren.  
  
10. Wenn Sie ein Mitglied der festen Serverrolle **sysadmin** sind und diesen Auftragsschritt unter einem anderen SQL-Anmeldenamen ausführen möchten, wählen Sie den SQL-Anmeldenamen in der Liste **Ausführen als Benutzer** aus.  
  
## <a name="TSQL"></a>Verwenden von Transact-SQL  
  
#### <a name="to-create-a-transact-sql-job-step"></a>So erstellen Sie einen Transact-SQL-Auftragsschritt  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- creates a job step that that uses Transact-SQL  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755).  
  
## <a name="SMO"></a>Verwendung von SQL Server Management Objects  
**So erstellen Sie einen Transact-SQL-Auftragsschritt**  
  
Verwenden Sie die **JobStep** -Klasse indem Sie eine von Ihnen ausgewählte Programmiersprache, z. B. Visual Basic, Visual C# oder PowerShell verwenden.  
  

