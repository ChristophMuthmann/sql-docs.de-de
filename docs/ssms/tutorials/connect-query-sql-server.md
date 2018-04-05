---
Title: 'Tutorial: Connect to and query a SQL Server instance by using SQL Server Management Studio'
description: Ein Tutorial für die Herstellung einer Verbindung zu einer SQL Server-Instanz durch Verwendung von SQL Server Management Studio und Ausführen grundlegender T-SQL-Abfragen
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: fe8d438d95e994438df565013eaf79da92ccf9b3
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2018
---
# <a name="tutorial-connect-to-and-query-a-sql-server-instance-by-using-sql-server-management-studio"></a>Tutorial: Herstellen einer Verbindung mit und Abfragen von einer SQL Server-Instanz über SQL Server Management Studio
In diesem Tutorial erfahren Sie, wie Sie mit SQL Server Management Studio (SSMS) eine Verbindung mit einer SQL Server-Instanz herstellen und grundlegende T-SQL-Befehle (Transact-SQL) ausführen. In diesem Artikel erhalten Sie Informationen zu folgenden Themen:

> [!div class="checklist"]  
> * Eine Verbindung mit einer SQL Server-Instanz herstellen    
> * Erstellen einer Datenbank („TutorialDB“)    
> * Erstellen einer Tabelle („Customers“) in Ihrer neuen Datenbank   
> * Einfügen von Zeilen in Ihre neue Tabelle 
> * Abfragen der neuen Tabelle und Aufrufen der Ergebnisse    
> * Überprüfen der Verbindungseigenschaften mit der Tabelle im Abfragefenster 
> * Ändern des Servers, mit dem Ihr Abfragefenster verbunden ist

## <a name="prerequisites"></a>Voraussetzungen
Zur Durchführung dieses Tutorials benötigen Sie SQL Server Management Studio und Zugriff auf eine SQL Server-Instanz. 

- Installieren Sie [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).

Wenn Sie über keinen Zugriff auf eine SQL Server-Instanz verfügen, wählen Sie Ihre Plattform aus den folgenden Links aus. Wenn Sie die SQL-Authentifizierung wählen, verwenden Sie Ihre SQL Server-Anmeldeinformationen.
- **Windows**: [Herunterladen der SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- **macOS**: [Herunterladen von SQL Server 2017 für Docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)


## <a name="connect-to-a-sql-server-instance"></a>Eine Verbindung mit einer SQL Server-Instanz herstellen

1. Starten von SQL Server Management Studio  
    Beim ersten Ausführen von SSMS wird das Fenster **Connect to Server** (Verbindung mit Server herstellen) geöffnet. Wenn das Fenster nicht geöffnet wird, können Sie es manuell öffnen, indem Sie auf **Objekt-Explorer** > **Verbinden** > **Datenbank-Engine** klicken.

    ![Die Verknüpfung „Verbinden“ im Objekt-Explorer](media/connect-query-sql-server/connectobjexp.png)

2. Führen Sie im Fenster **Mit Server verbinden** folgende Aktionen aus: 

    - Wählen Sie für **Servertyp** die Option **Datenbank-Engine** (normalerweise die Standardoption) aus.
    - Geben Sie für **Servername** den Namen Ihrer SQL Server-Instanz ein. (In diesem Artikel wird der Instanzname „SQL2016ST“ auf dem Hostnamen „NODE5“ [NODE5\SQL2016ST] verwendet.) Wenn Sie nicht genau wissen, wie Sie Ihren SQL Server-Instanznamen bestimmen sollen, erhalten Sie hier [zusätzliche Tipps und Tricks für die Verwendung von SSMS](ssms-tricks.md#determine-sql-server-name).  

    ![Feld „Servername“ mit Beispielinstanznamen](media/connect-query-sql-server/connection.png)

    ![Feld „Servername“ mit der Option zur Verwendung der SQL Server-Instanz](media/connect-query-sql-server/connection2.png)

    - Wählen Sie für **Authentifizierung** die Option **Windows-Authentifizierung** aus. In diesem Artikel wird die Windows-Authentifizierung verwendet, jedoch wird ebenso die SQL Server-Anmeldung unterstützt. Wenn Sie **SQL-Anmeldung** auswählen, werden Sie aufgefordert, Ihren Benutzernamen und Ihr Kennwort einzugeben. Weitere Informationen zu Authentifizierungstypen finden Sie unter [Verbindung mit Server herstellen (Datenbank-Engine)](https://docs.microsoft.com/en-us/sql/ssms/f1-help/connect-to-server-database-engine).

    Sie können auch zusätzliche Verbindungsoptionen ändern, indem Sie **Optionen** auswählen. Beispiele für Verbindungsoptionen sind die Datenbank, mit der Sie sich verbinden, der Verbindungstimeoutwert und das Netzwerkprotokoll. In diesem Artikel werden die Standardwerte für alle Optionen verwendet. 

3. Nachdem Sie alle Felder ausgefüllt haben, klicken Sie auf **Verbinden**. 

4. Überprüfen Sie, ob die Verbindung mit Ihrer SQL Server-Instanz erfolgreich ist, indem Sie die Objekte im Objekt-Explorer wie hier dargestellt durchsuchen: 

   ![Erfolgreicher Verbindungsaufbau](media/connect-query-sql-server/successfulconnection.png)

## <a name="create-a-database"></a>Erstellen einer Datenbank
Erstellen Sie mithilfe folgender Schritte eine Datenbank namens „TutorialDB“: 

1. Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf Ihre Serverinstanz und anschließend mit der linken auf **Neue Abfrage**:

   ![Die Verknüpfung „Neue Abfrage“](media/connect-query-sql-server/newquery.png)
   
2. Fügen Sie den folgenden T-SQL-Codeausschnitt in das Abfragefenster ein: 
   ```sql
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```
2. Klicken Sie zum Ausführen der Abfrage auf **Ausführen**, oder drücken Sie F5. 

   ![Befehl „Ausführen“](media/connect-query-sql-server/execute.png)
  
    Nachdem die Abfrage abgeschlossen ist, wird die neue Datenbank „TutorialDB“ in der Datenbankliste im Objekt-Explorer angezeigt. Wenn die Datenbank nicht angezeigt wird, klicken Sie zuerst mit der rechten Maustaste auf den **Datenbankenknoten** und anschließend mit der linken auf **Aktualisieren**.  


## <a name="create-a-table-in-the-new-database"></a>Erstellen einer Tabelle in der neuen Datenbank
In diesem Abschnitt erstellen Sie nun eine Tabelle in der neuen Datenbank „TutorialDB“. Da sich der Abfrage-Editor immer noch im Kontext der *Master*-Datenbank befindet, ändern Sie den Verbindungskontext in die *TutorialDB*-Datenbank, indem Sie folgende Schritte ausführen: 

1. Wählen Sie in der Dropdownliste die gewünschte Datenbank aus, so wie hier dargestellt: 

   ![Ändern der Datenbank](media/connect-query-sql-server/changedb.png)

2. Fügen Sie den folgenden T-SQL-Codeausschnitt in das Abfragefenster ein, wählen Sie ihn aus, und klicken Sie auf **Ausführen** (oder drücken Sie F5).  
   Sie können entweder den vorhandenen Text im Abfragefenster ersetzen oder weiteren Text am Ende anfügen. Um den gesamten Code im Abfragefenster auszuführen, klicken Sie auf **Ausführen**. Wenn Sie nur einen Teil des Codes ausführen möchten, markieren Sie diese Stelle, und klicken Sie anschließend auf **Ausführen**.  
  
   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

Nachdem die Abfrage abgeschlossen ist, wird die neue Tabelle „Customers“ in der Tabellenliste im Objekt-Explorer angezeigt. Wenn die Tabelle nicht angezeigt wird, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Knoten **TutorialDB** > **Tabellen** und anschließend mit der linken Maustaste auf **Aktualisieren**.

## <a name="insert-rows-into-the-new-table"></a>Einfügen von Zeilen in die neue Tabelle
Fügen Sie einige Zeilen in die Tabelle „Customers“ ein, die Sie zuvor erstellt haben. Fügen Sie dazu den folgenden T-SQL-Codeausschnitt in das Abfragefenster ein, und klicken Sie auf **Ausführen**: 


   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="query-the-table-and-view-the-results"></a>Abfragen der Tabelle und Aufrufen der Ergebnisse
Die Ergebnisse einer Abfrage werden unter dem Abfragetextfenster angezeigt. Um die Tabelle Customers abzufragen und sich die zuvor eingefügten Zeilen anzeigen zu lassen, führen Sie folgende Schritte aus:  

1. Fügen Sie den folgenden T-SQL-Codeausschnitt in das Abfragefenster ein, und klicken Sie auf **Ausführen**: 

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

    Die Ergebnisse der Abfrage werden unter dem Bereich angezeigt, in dem Text eingegeben wurde: 

   ![Die Ergebnisliste](media/connect-query-sql-server/queryresults.png)

2. Ändern Sie die Darstellung der angezeigten Ergebnisse durch eine der folgenden Optionen:

     ![Drei Optionen zum Anzeigen von Abfrageergebnissen](media/connect-query-sql-server/results.png)

    - Die mittlere Schaltfläche zeigt die Ergebnisse in der **Rasteransicht**, also in der Standardansicht, an. 
    - Mit der linken Schaltfläche werden die Ergebnisse in der **Textansicht** dargestellt, wie in der Abbildung im nächsten Abschnitt zu sehen ist.
    - Mit der dritten Schaltfläche können Sie die Ergebnisse in einer Datei speichern, deren Erweiterung standardmäßig nicht RPT ist.

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>Überprüfen Ihrer Verbindungseigenschaften mit der Tabelle im Abfragefenster
Informationen zu Verbindungseigenschaften finden Sie unter den Ergebnissen einer Abfrage. Nachdem Sie die Abfrage aus dem vorherigen Schritt ausgeführt haben, können Sie sich die Verbindungseigenschaften im unteren Bereich des Abfragefensters ansehen.

- Hier wird angezeigt, mit welchem Server und welcher Datenbank Sie verbunden sind. Außerdem ist der Benutzername zu sehen, mit dem Sie angemeldet sind.
- Des Weiteren sind auch die Abfragedauer und die Anzahl der Zeilen angezeigt, die von der zuvor ausgeführten Abfrage zurückgegeben wurden.

    ![Verbindungseigenschaften](media/connect-query-sql-server/connectionproperties.png)
    
    Beachten Sie, dass in dieser Abbildung die Ergebnisse in der **Textansicht** dargestellt werden. 

## <a name="change-the-server-that-the-query-window-is-connected-to"></a>Ändern des Servers, mit dem das Abfragefenster verbunden ist
Mit den folgenden Schritten können Sie die Serververbindung für das aktuelle Abfragefenster ändern:

1. Klicken Sie mit der rechten Maustaste in das Abfragefenster, und wählen Sie dann **Verbindung** > **Verbindung ändern** aus.  
    Das Fenster **Mit Server verbinden** wird erneut geöffnet.
2. Ändern Sie den Server, mit dem Ihr Abfragefenster verbunden ist. 
 
   ![Der Befehl „Verbindung ändern“](media/connect-query-sql-server/changeconnection.png)

    > [!NOTE]
    > Diese Aktion ändert nur den Server, mit dem das Abfragefenster verbunden ist und nicht den Server, mit dem der Objekt-Explorer verbunden ist. 



