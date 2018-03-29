---
Title: 'Tutorial: Additional Tips and Tricks for using SSMS'
description: 'Ein Tutorial, das einige zusätzliche Tipps und Tricks für die Verwendung von SSMS enthält. '
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
ms.openlocfilehash: 9f633a8d624fd31913dc2aeb6fde34ff30b7645d
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-additional-tips-and-tricks-for-using-ssms"></a>Tutorial: Zusätzliche Tipps und Tricks für die Verwendung von SSMS
Dieses Tutorial enthält einige zusätzliche Tricks für die Verwendung von SQL Server Management Studio. In diesem Artikel lernen Sie Folgendes: 

> [!div class="checklist"]
> * Kommentieren/Aufheben der Auskommentierung Ihres T-SQL-Texts (Transact-SQL)
> * Einziehen Ihres Texts
> * Filtern von Objekten in Objekt-Explorer
> * Zugreifen auf Ihr SQL Server-Fehlerprotokoll
> * Suchen des Namens Ihrer SQL Server-Instanz

## <a name="prerequisites"></a>Voraussetzungen
Zur Durchführung dieses Tutorials benötigen Sie SQL Server Management Studio, Zugriff auf einen SQL-Server und eine AdventureWorks-Datenbank. 

- Installieren Sie [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Installieren Sie die [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Laden Sie eine [AdventureWorks-Beispieldatenbank](https://github.com/Microsoft/sql-server-samples/releases) herunter. Anweisungen zum Wiederherstellen von Datenbanken in SSMS finden Sie hier: [Restoring a Database (Wiederherstellen einer Datenbank)](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 

## <a name="comment--uncomment-your-t-sql-code"></a>Kommentieren Sie Ihren T-SQL-Code oder entfernen Sie die Kommentare
Über die Schaltfläche für Kommentare in der Symbolleiste können Sie bei Teilen Ihres Texts Kommentare hinzufügen und Auskommentierungen aufheben. Auskommentierter Text wird nicht ausgeführt. 

1. Öffnen Sie SQL Server Management Studio. 
2. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
3. Öffnen Sie das Fenster **Neue Abfrage**. 
4. Fügen Sie folgenden T-SQL-Codeausschnitt in Ihr Textfenster ein: 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 


5. Markieren Sie den Teil des Texts mit dem Befehl **Alter Database**, und klicken Sie in der Symbolleiste auf **Kommentar**: 

    ![Anmerkung](media/ssms-tricks/comment.png)
6. Klicken Sie auf **Ausführen**, um den Teil des Texts auszuführen, bei dem Auskommentierungen aufgehoben wurden. 
7. Markieren Sie den gesamten Text bis auf den Befehl **Alter Database**, und klicken Sie in der Symbolleiste auf **Kommentar**:

    ![Gesamten Text kommentieren](media/ssms-tricks/commenteverything.png)

8. Markieren Sie den Abschnitt mit dem Befehl **Alter Database**, und klicken Sie auf **Auskommentierung aufheben**, um die Auskommentierung des Texts aufzuheben:

    ![Auskommentierungen aufheben](media/ssms-tricks/uncomment.png)
    
9. Klicken Sie auf **Ausführen**, um den Teil des Texts auszuführen, bei dem Auskommentierungen aufgehoben wurden. 

## <a name="indent-your-text"></a>Einziehen Ihres Texts
Sie können den Einzug Ihres Texts über die Schaltflächen für den Einzug vergrößern oder verringern. 

1. Öffnen Sie das Fenster **Neue Abfrage**. 
2. Fügen Sie folgenden T-SQL-Codeausschnitt in Ihr Textfenster ein: 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 
 
3. Markieren Sie den Teil des Texts mit dem Befehl **Alter Database**, und klicken Sie in der Symbolleiste auf **Einzug vergrößern**, um diesen Text zu verschieben:

    ![Einzug vergrößern](media/ssms-tricks/increaseindent.png)

4. Markieren Sie erneut den Teil des Texts mit dem Befehl **Alter Database**, und klicken Sie diesmal auf **Einzug verkleinern**, um diesen Text wieder an die alte Position zu verschieben. 
    ![Einzug verkleinern](media/ssms-tricks/decreaseindent.png)


## <a name="filter-objects-in-object-explorer"></a>Filtern von Objekten in Objekt-Explorer
Wenn eine Datenbank viele Objekte enthält, kann sich die Suche nach einem bestimmten Objekt als schwierig erweisen. Zur Vereinfachung dieses Vorgangs können Sie Objekte filtern. In diesem Abschnitt wird erläutert, wie Tabellen gefiltert werden. Die gleichen Schritte können jedoch auch auf alle anderen Knoten in **Objekt-Explorer** angewendet werden.

1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken**.
3. Erweitern Sie den Datenbankknoten **AdventureWorks**. 
4. Erweitern Sie den Knoten **Tabellen**. 
   - Sie werden bemerken, dass Ihnen alle in der Datenbank enthaltenen Tabellen angezeigt werden.
5. Klicken Sie mit der rechten Maustaste auf den Knoten **Tabellen** > **Filter** > **Filtereinstellungen**:

    ![Filtereinstellungen](media/ssms-tricks/filtersettings.png)

6. Im Fenster „Filtereinstellungen“ können Sie die Filtereinstellungen ändern. Einige Beispiele:
    - Nach Namen filtern: ![Filter by Name](media/ssms-tricks/filterbyname.png) (Nach Namen filtern)
    - Nach Schema filtern: ![Filter by Schema](media/ssms-tricks/filterbyschema.png) (Nach Schema filtern)

7. Klicken Sie mit der rechten Maustaste auf **Tabellen** > **Filter entfernen**, um den Filter zu löschen.

    ![Filter entfernen](media/ssms-tricks/removefilter.png)
    


## <a name="access-your-sql-server-error-log"></a>Zugreifen auf Ihr SQL Server-Fehlerprotokoll
Das Fehlerprotokoll ist eine Datei mit Details zu Ereignissen, die auf Ihrem SQL-Server auftreten. Es kann in SSMS durchsucht und abgefragt werden. Es kann auch als Protokolldatei auf dem Datenträger gefunden werden.

### <a name="find-your-error-log-if-you-cannot-connect-to-sql"></a>Finden Ihres Fehlerprotokolls, wenn keine Verbindung zu SQL hergestellt werden kann
1. Öffnen Sie den SQL Server-Konfigurations-Manager. 
2. Erweitern Sie den Knoten **Dienste**.
3. Klicken Sie mit der rechten Maustaste auf Ihre SQL Server-Instanz > **Eigenschaften**:

    ![Servereigenschaften für den Konfigurations-Manager](media/ssms-tricks/serverproperties.PNG)

4. Wählen Sie die Registerkarte **Startparameter** aus.
5. Im Bereich **Vorhandene Parameter** ist im Pfad hinter „-e“ der Speicherort des Fehlerprotokolls enthalten: 
    
    ![Fehlerprotokoll](media/ssms-tricks/errorlog.png)
    - Sie werden feststellen, dass an diesem Speicherort mehrere errorlog.*-Dateien vorhanden sind. Bei der Datei mit „*.log“ handelt es sich um das aktuelle Fehlerprotokoll. Die Dateien, die mit Ziffern enden, sind vorhergehende Protokolle, da bei jedem Neustart von SQL Server ein neues Protokoll erstellt wird. 
6. Öffnen Sie diese Datei in Notepad. 

### <a name="find-your-error-log-if-youre-connected-to-sql"></a>Finden Ihres Fehlerprotokolls, wenn Sie mit SQL verbunden sind
1. Stellen Sie eine Verbindung mit SQL Server her.
2. Öffnen Sie das Fenster **Neue Abfrage**.
3. Fügen Sie folgenden T-SQL-Codeausschnitt in Ihr Abfragefenster ein, und klicken Sie auf **Ausführen**:


  ```sql
   SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location' 
  ```
3. Die Ergebnisse zeigen den Speicherort des Fehlerprotokolls innerhalb des Dateisystems an: 

![Fehlerprotokoll nach Abfrage suchen](media/ssms-tricks/finderrorlogquery.png)

### <a name="open-error-log-within-ssms"></a>Öffnen des Fehlerprotokolls in SSMS
1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Verwaltung** . 
3. Erweitern Sie den Knoten **SQL Server-Protokolle**. 
4. Klicken Sie mit der rechten Maustaste auf das Fehlerprotokoll **Aktuell** > **SQL Server-Protokoll anzeigen**:

    ![Fehlerprotokoll in SSMS anzeigen](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-error-log-within-ssms"></a>Abfragen des Fehlerprotokolls in SSMS
1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Öffnen Sie das Fenster **Neue Abfrage**.
3. Fügen Sie folgenden T-SQL-Codeausschnitt in Ihr Abfragefenster ein:

 ```sql
   sp_readerrorlog 0,1,'Server process ID' 
  ``` 
4. Ändern Sie den Text in einfachen Anführungszeichen in den gewünschten Text.
5. Führen Sie die Abfrage aus, und überprüfen Sie die Ergebnisse:
   
    ![Fehlerprotokoll abfragen](media/ssms-tricks/queryerrorlog.png)

## <a name="determine-sql-server-instance-name"></a>Bestimmen des Namens der SQL Server-Instanz, ...
Der Name Ihrer Instanz kann auf verschiedenen Wegen vor und nach dem Herstellen einer Verbindung mit Ihrem SQL Server bestimmt werden.  

### <a name="when-you-dont-know-it"></a>... wenn er Ihnen nicht bekannt ist
1. Führen Sie die Schritte zum Finden des [SQL Server-Fehlerprotokolls auf dem Datenträger](#finding-your-error-log-if-you-cannot-connect-to-sql) aus. 
2. Öffnen Sie die Datei „errorlog.log“ in Notepad. 
3. Navigieren Sie durch die Datei, bis Sie den Text „Server name is“ (Servername lautet) finden:
  - Bei dem Text, der in einfachen Anführungszeichen steht, handelt es sich um den Namen der Instanz, mit der Sie verbunden werden: ![Servername im Fehlerprotokoll](media/ssms-tricks/servernameinlog.png)

### <a name="once-youre-connected-to-sql"></a>Sobald Sie eine Verbindung mit SQL hergestellt haben 
Sie können den Namen der Instanz, mit der Sie verbunden sind, an drei Positionen finden. 

1. Der Name des Servers wird im **Objekt-Explorer** aufgeführt:

    ![Instanzname in Objekt-Explorer](media/ssms-tricks/nameinobjectexplorer.png)
2. Der Name des Servers wird im Abfragefenster aufgeführt:

    ![Name im Abfragefenster](media/ssms-tricks/nameinquerywindow.png)
3. zugreifen. Der Name des Servers wird zudem im Fenster **Eigenschaften** aufgeführt.
    - Öffnen Sie das Menü **Ansicht** > **Eigenschaften**, um darauf zugreifen zu können:

    ![Name in Eigenschaften](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>... wenn Sie mit einem Alias oder einem Verfügbarkeitsgruppenlistener verbunden sind 
Wenn Sie mit einem Alias oder einem Verfügbarkeitsgruppenlistener verbunden sind, wird Ihnen dies im **Objekt-Explorer** und im Fenster **Eigenschaften** angezeigt. In diesem Fall ist der SQL Server-Name möglicherweise nicht sofort erkennbar und muss abgefragt werden. 

1. Stellen Sie eine Verbindung mit SQL Server her.
2. Öffnen Sie das Fenster **Neue Abfrage**.
3. Fügen Sie folgenden T-SQL-Codeausschnitt in das Fenster ein: 

  ```sql
   select @@Servername 
 ``` 
4. Zeigen Sie die Ergebnisse der Abfrage an, um den SQL Server-Namen zu ermitteln, mit dem Sie verbunden sind: 
    
    ![Servernamen abfragen](media/ssms-tricks/queryservername.png)


