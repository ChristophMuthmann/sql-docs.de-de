---
title: Erstellen eines Auftrags des SQL Server-Agents zum Archivieren von Datenbank-E-Mail-Nachrichten und Ereignisprotokollen | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- archiving mail messages and attachments [SQL Server]
- removing mail messages and attachements
- Database Mail [SQL Server], archiving
- saving mail messages and attachments
ms.assetid: 8f8f0fba-f750-4533-9b76-a9cdbcdc3b14
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bfba800ce9266e7a27c6e27e8e3ea9dfc2f2b08e
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs"></a>Erstellen eines Auftrags des SQL Server-Agents zum Archivieren von Datenbank-E-Mail-Nachrichten und Ereignisprotokollen
  Kopien von Datenbank-E-Mail-Nachrichten und deren Anlagen werden zusammen mit dem Datenbank-E-Mail-Ereignisprotokoll in **msdb** -Tabellen gespeichert. Sie sollten die Größe der Tabellen regelmäßig reduzieren und Nachrichten und Ereignisse archivieren, die nicht mehr benötigt werden. Die folgenden Prozeduren erstellen einen Auftrag des SQL Server-Agents, um diesen Prozess zu automatisieren.  
  
-   **Vorbereitungen:**  , [Voraussetzungen](#Prerequisites), [Empfehlungen](#Recommendations), [Berechtigungen](#Permissions)  
  
-   **To Archive Database Mail messages and logs using :**  [SQL Server Agent](#Process_Overview)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Voraussetzungen  
 Die neuen Tabellen zum Speichern der Archivdaten können sich in einer speziellen Archivdatenbank befinden. Alternativ können die Zeilen in eine Textdatei exportiert werden.  
   
###  <a name="Recommendations"></a> Empfehlungen  
 Für die Verwendung in einer Produktionsumgebung sollten Sie eine zusätzliche Fehlerprüfung einfügen und eine E-Mail-Nachricht an Operatoren senden, wenn beim Auftrag ein Fehler auftritt.  
  
  
###  <a name="Permissions"></a> Berechtigungen  
 Sie müssen Mitglied der festen Serverrolle **sysadmin** sein, um die in diesem Thema beschriebenen gespeicherten Prozeduren auszuführen.  
  
  
###  <a name="Process_Overview"></a> Übersicht über den Prozess  
  
-   Die erste Prozedur erstellt den Auftrag "Datenbank-E-Mail archivieren" in den folgenden Schritten:  
  
    1.  Kopieren Sie alle Nachrichten aus den Datenbank-E-Mail-Tabellen in eine neue Tabelle, die nach dem vorhergehenden Monat im Format **DBMailArchive_***Jahr_Monat* benannt wird.  
  
    2.  Kopieren Sie die zu den im ersten Schritt kopierten Nachrichten gehörenden Anlagen aus den Datenbank-E-Mail-Tabellen in eine neue Tabelle, die nach dem vorhergehenden Monat im Format **DBMailArchive_Attachments_***Jahr_Monat* benannt wird.  
  
    3.  Kopieren Sie die zu den im ersten Schritt kopierten Nachrichten gehörenden Ereignisse aus dem Datenbank-E-Mail-Ereignisprotokoll aus den Datenbank-E-Mail-Tabellen in eine neue Tabelle, die nach dem vorhergehenden Monat im Format **DBMailArchive_Log_***Jahr_Monat* benannt wird.  
  
    4.  Löschen Sie die Datensätze der übertragenen E-Mail-Elemente aus den Datenbank-E-Mail-Tabellen.  
  
    5.  Löschen Sie die zu den übertragenen E-Mail-Elementen gehörenden Ereignisse aus dem Datenbank-E-Mail-Ereignisprotokoll.  
  
-   Planen Sie die regelmäßige Ausführung des Auftrags.  
  
  
## <a name="to-create-a-sql-server-agent-job"></a>So erstellen Sie einen Auftrag für den SQL Server-Agent  
  
1.  Erweitern Sie im Objekt-Explorer den Knoten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent, klicken Sie mit der rechten Maustaste auf **Aufträge**, und klicken Sie dann auf **Neuer Auftrag**.  
  
2.  Geben Sie im Dialogfeld **Neuer Auftrag** im Feld **Name** den Namen **Datenbank-E-Mail archivieren**ein.  
  
3.  Bestätigen Sie im Feld **Besitzer** , dass der Besitzer Mitglied der festen Serverrolle **sysadmin** ist.  
  
4.  Klicken Sie im Feld **Kategorie** auf **Datenbankwartung**.  
  
5.  Geben Sie im Feld **Beschreibung** als Beschreibung **Datenbank-E-Mail-Nachrichten archivieren**ein, und klicken Sie dann auf **Schritte**.  
  
 [Übersicht](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-messages"></a>So erstellen Sie einen Schritt zum Archivieren der Datenbank-E-Mail-Nachrichten  
  
1.  Klicken Sie auf der Seite **Schritte** auf **Neu**.  
  
2.  Geben Sie im Feld **Schrittname** den Namen **Datenbank-E-Mail-Elemente kopieren**ein.  
  
3.  Klicken Sie im Feld **Typ** auf **Transact-SQL-Skript (T-SQL)**.  
  
4.  Klicken Sie im Feld **Datenbank** auf **msdb**.  
  
5.  Geben Sie im Feld **Befehl** die folgende Anweisung zum Erstellen einer Tabelle ein, die nach dem vorhergehenden Monat benannt wird und Zeilen enthält, die aus der Zeit vor Beginn des aktuellen Monats stammen:  
  
    ```tsql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_' + @LastMonth + '] FROM sysmail_allitems WHERE send_request_date < ''' + @CopyDate +'''';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  Klicken Sie auf **OK** , um den Schritt zu speichern.  
  
 [Übersicht](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-attachments"></a>So erstellen Sie einen Schritt zum Archivieren der Datenbank-E-Mail-Anlagen  
  
1.  Klicken Sie auf der Seite **Schritte** auf **Neu**.  
  
2.  Geben Sie im Feld **Schrittname** den Namen **Datenbank-E-Mail-Anlagen kopieren**ein.  
  
3.  Klicken Sie im Feld **Typ** auf **Transact-SQL-Skript (T-SQL)**.  
  
4.  Klicken Sie im Feld **Datenbank** auf **msdb**.  
  
5.  Geben Sie im Feld **Befehl** die folgende Anweisung zum Erstellen einer Tabelle mit Anlagen ein, die nach dem vorhergehenden Monat benannt wird und die Anlagen zu den im vorhergehenden Schritt übertragenen Nachrichten enthält:  
  
    ```tsql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Attachments_' + @LastMonth + '] FROM sysmail_attachments   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  Klicken Sie auf **OK** , um den Schritt zu speichern.  
  
 [Übersicht](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-log"></a>So erstellen Sie einen Schritt zum Archivieren des Datenbank-E-Mail-Protokolls  
  
1.  Klicken Sie auf der Seite **Schritte** auf **Neu**.  
  
2.  Geben Sie im Feld **Schrittname** den Namen **Datenbank-E-Mail-Protokoll kopieren**ein.  
  
3.  Klicken Sie im Feld **Typ** auf **Transact-SQL-Skript (T-SQL)**.  
  
4.  Klicken Sie im Feld **Datenbank** auf **msdb**.  
  
5.  Geben Sie im Feld **Befehl** die folgende Anweisung zum Erstellen einer Protokolltabelle ein, die nach dem vorhergehenden Monat benannt wird und die Protokolleinträge zu den in einem vorhergehenden Schritt übertragenen Nachrichten enthält:  
  
    ```tsql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Log_' + @LastMonth + '] FROM sysmail_Event_Log   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  Klicken Sie auf **OK** , um den Schritt zu speichern.  
  
 [Übersicht](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-rows-from-database-mail"></a>So erstellen Sie einen Schritt zum Entfernen der archivierten Zeilen aus der Datenbank-E-Mail  
  
1.  Klicken Sie auf der Seite **Schritte** auf **Neu**.  
  
2.  Geben Sie im Feld **Schrittname** den Namen **Zeilen aus Datenbank-E-Mail entfernen**ein.  
  
3.  Klicken Sie im Feld **Typ** auf **Transact-SQL-Skript (T-SQL)**.  
  
4.  Klicken Sie im Feld **Datenbank** auf **msdb**.  
  
5.  Geben Sie im Feld **Befehl** die folgende Anweisung ein, um Zeilen aus den Datenbank-E-Mail-Tabellen zu entfernen, die älter als der aktuelle Monat sind:  
  
    ```tsql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @CopyDate ;  
    ```  
  
6.  Klicken Sie auf **OK** , um den Schritt zu speichern.  
  
 [Übersicht](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-items-from-database-mail-event-log"></a>So erstellen Sie einen Schritt zum Entfernen der archivierten Elemente aus dem Datenbank-E-Mail-Ereignisprotokoll  
  
1.  Klicken Sie auf der Seite **Schritte** auf **Neu**.  
  
2.  Geben Sie im Feld **Schrittname** den Namen **Zeilen aus dem Datenbank-E-Mail-Protokoll entfernen**ein.  
  
3.  Klicken Sie im Feld **Typ** auf **Transact-SQL-Skript (T-SQL)**.  
  
4.  Geben Sie im Feld **Befehl** die folgende Anweisung ein, um Zeilen aus dem Datenbank-E-Mail-Ereignisprotokoll zu entfernen, die älter als der aktuelle Monat sind:  
  
    ```tsql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_log_sp @logged_before = @CopyDate ;  
    ```  
  
5.  Klicken Sie auf **OK** , um den Schritt zu speichern.  
  
 [Übersicht](#Process_Overview)  
  
## <a name="to-schedule-the-job-to-run-periodically"></a>So planen Sie die regelmäßige Ausführung des Auftrags  
  
1.  Klicken Sie im Dialogfeld **Neuer Auftrag** auf **Zeitpläne**.  
  
2.  Klicken Sie auf der Seite **Zeitpläne** auf **Neu**.  
  
3.  Geben Sie im Feld **Name** den Namen **Datenbank-E-Mail archivieren**ein.  
  
4.  Klicken Sie im Feld **Zeitplantyp** auf **Wiederholt**.  
  
5.  Wählen Sie im Bereich **Häufigkeit** die Optionen zum regelmäßigen Ausführen des Auftrags, z. B. am ersten Tag eines jeden Monats, aus.  
  
6.  Klicken Sie im Bereich **Häufigkeit pro Tag** auf **Wird einmal um \<Uhrzeit>** ausgeführt.  
  
7.  Überprüfen Sie, ob die anderen Optionen wie gewünscht konfiguriert sind, und klicken Sie dann auf **OK** , um den Zeitplan zu speichern.  
  
8.  Klicken Sie auf **OK** , um den Auftrag zu speichern.  
  
 [Übersicht](#Process_Overview)  
  
  

