---
Title: 'Tutorial: Connect and Query SQL Server using SQL Server Management Studio'
description: Tutorial zum Herstellen einer Verbindung mit SQL Server über SQL Server Management Studio und zum Ausführen grundlegender T-SQL-Abfragen
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 7b389c5b58dc0afde077f70e2fd8bec7c6cac4d0
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-connect-and-query-sql-server-using-sql-server-management-studio"></a>Tutorial: Herstellen einer Verbindung mit und Abfragen von SQL Server über SQL Server Management Studio
In diesem Tutorial erfahren Sie, wie Sie mit SQL Server Management Studio (SSMS) eine Verbindung mit einer SQL Server-Instanz herstellen und grundlegende T-SQL-Befehle (Transact-SQL) ausführen. Dieser Artikel enthält Beispiele für folgende Themen:
    - [Herstellen einer Verbindung mit SQL Server](#connect-to-a-sql-server)
    - [Erstellen einer neuen Datenbank (**TutorialDB**)](#create-a-database)
    - [Erstellen einer Tabelle (**Customers**) in der neuen Datenbank](#create-a-table)
    - [Einfügen von Zeilen in die neue **Customers**-Tabelle](#insert-rows)
    - [Abfragen der **Customers**-Tabelle und Aufrufen der Ergebnisse](#view-query-results)
    - [Überprüfen der Verbindungseigenschaften mit der Tabelle im Abfragefenster](#verify-your-query-window-connection-properties)
    - [Ändern der Serververbindung für das Abfragefenster](#change-server-connection-within-query-window)


## <a name="prerequisites"></a>Voraussetzungen
Für dieses Tutorial benötigen Sie SQL Server Management Studio und Zugriff auf einen Server mit SQL Server. Hierfür ist Folgendes erforderlich: 

- Installieren Sie [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).

Wenn Sie über keinen Zugriff auf einen Server mit SQL Server verfügen, müssen Sie die von Ihnen verwendete Plattform über einen der folgenden Links auswählen. Falls Sie die SQL-Authentifizierung nutzen, ist es erforderlich, dass Sie sich den SQL-Anmeldenamen und das zugehörige Kennwort merken.
- [Windows: Herunterladen der SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS: Herunterladen von SQL Server 2017 für Docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)


## <a name="connect-to-a-sql-server"></a>Herstellen einer Verbindung mit SQL Server

1. Starten Sie SQL Server Management Studio (SSMS).
1. Beim ersten Ausführen von SSMS wird das Dialogfeld **Connect to Server** (Verbindung mit Server herstellen) geöffnet. 
      - Wenn das Dialogfeld **Connect to Server** (Verbindung mit Server herstellen) nicht geöffnet wird, können Sie es selbst über **Objekt-Explorer** > **Verbinden** (oder über das nebenstehende Symbol) > **Datenbank-Engine** öffnen.

        ![Option „Verbinden“ im Objekt-Explorer](media/connect-query-sql-server/connectobjexp.png)

1. Wählen Sie im Dialogfeld **Connect to Server** (Verbindung mit Server herstellen) Ihre Verbindungsoptionen aus: 

    - **Servertyp**: Datenbank-Engine (in der Regel die Standardauswahl)
    - **Authentifizierung**: Windows-Authentifizierung (in diesem Artikel wird die Windows-Authentifizierung verwendet; bei Nutzung der SQL-Anmeldung, die ebenfalls unterstützt wird, müssen Sie Ihren Benutzernamen und Ihr Kennwort eingeben)

      ![Verbindung](media/connect-query-sql-server/connection.png)

        Sie können außerdem zusätzliche Verbindungsoptionen ändern (z.B. die Datenbank, mit der die Verbindung hergestellt werden soll, das Zeitlimit für die Verbindungszeit sowie das Netzwerkprotokoll), indem Sie auf die Schaltfläche **Optionen** klicken. In diesem Artikel werden die Standardeinstellungen beibehalten. 

1. Klicken Sie nach dem Ausfüllen der Felder auf **Verbinden**. 

1. Ob eine Verbindung mit SQL Server hergestellt wurde, können Sie überprüfen, indem Sie sich die Objekte im **Objekt-Explorer** ansehen: 

   ![Erfolgreicher Verbindungsaufbau](media/connect-query-sql-server/successfulconnection.png)


## <a name="create-a-database"></a>Erstellen einer Datenbank
Mit den folgenden Schritten wird eine neue Datenbank mit dem Namen „TutorialDB“ erstellt. 

1. Klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf Ihren Server und anschließend mit der linken auf **Neue Abfrage**:

   ![Neue Abfrage](media/connect-query-sql-server/newquery.png)
   
1. Fügen Sie den folgenden T-SQL-Codeausschnitt in das Abfragefenster ein: 
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

   ![Ausführen der Abfrage](media/connect-query-sql-server/execute.png)
  
 
Nachdem die Abfrage abgeschlossen ist, wird die neue Datenbank **TutorialDB** in der Datenbankliste im **Objekt-Explorer** angezeigt. Wenn die Datenbank nicht angezeigt wird, klicken Sie zuerst mit der rechten Maustaste auf den Datenbankenknoten und anschließend mit der linken auf **Aktualisieren**.  


## <a name="create-a-table"></a>Erstellen einer Tabelle
Mit den folgenden Schritten erstellen Sie nun eine Tabelle in der neuen Datenbank **TutorialDB**. Für den Abfrage-Editor ist als Verbindungskontext allerdings immer noch die *Masterdatenbank* und nicht *TutorialDB* ausgewählt. 

1. Sie müssen daher den Verbindungskontext in **TutorialDB** ändern, indem Sie die gewünschte Datenbank über die zugehörige Dropdownliste auswählen. 

   ![Ändern der Datenbank](media/connect-query-sql-server/changedb.png)

1. Fügen Sie den folgenden T-SQL-Codeausschnitt in das Abfragefenster ein, markieren Sie ihn, und klicken Sie auf **Ausführen** (oder drücken Sie F5): 
    - Sie können entweder den vorhandenen Text im Abfragefenster ersetzen oder weiteren Text am Ende anfügen. Wenn Sie den gesamten Code im Abfragefenster ausführen möchten, klicken Sie auf **Ausführen**. Wenn Sie nur einen Teil des Codes ausführen möchten, markieren Sie diese Stelle, und klicken Sie anschließend auf **Ausführen**.  
  
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
Nachdem die Abfrage abgeschlossen ist, wird die neue Tabelle **Customers** in der Tabellenliste im **Objekt-Explorer** angezeigt. Wenn die Tabelle nicht angezeigt wird, klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf den Knoten **TutorialDB > Tabellen** und anschließend mit der linken auf **Aktualisieren**.

## <a name="insert-rows"></a>Einfügen von Zeilen
Durch den folgenden Schritt fügen Sie mehrere Zeilen in die zuvor erstellte Tabelle **Customers** ein. 

Fügen Sie den folgenden T-SQL-Codeausschnitt in das Abfragefenster ein, und klicken Sie auf **Ausführen**: 


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

## <a name="view-query-results"></a>Aufrufen der Abfrageergebnisse
Die Ergebnisse einer Abfrage werden unter dem Abfragetextfenster angezeigt. Mit den unten aufgeführten Schritten können Sie die Tabelle **Customers** abfragen und sich die zuvor eingefügten Zeilen anzeigen lassen.  

1. Fügen Sie den folgenden T-SQL-Codeausschnitt in das Abfragefenster ein, und klicken Sie auf **Ausführen**: 

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```
1. Die Ergebnisse der Abfrage werden unter dem Bereich angezeigt, in dem Text eingegeben wurde: 

   ![Abfrageergebnisse](media/connect-query-sql-server/queryresults.png)


1.  Sie können die Darstellung der angezeigten Ergebnisse durch eine der folgenden Optionen ändern:

     ![Ergebnisse](media/connect-query-sql-server/results.png)

    - Als Standardeinstellung für die Darstellung der Ergebnisse wird die **Rasteransicht** verwendet, durch die die Ergebnisse in einer Tabelle angezeigt werden. Diese Option kann über die mittlere Schaltfläche ausgewählt werden. 
    - Mit der linken Schaltfläche werden die Ergebnisse in der **Textansicht** dargestellt, wie in der Abbildung im nächsten Abschnitt zu sehen ist.
    - Über die rechte Schaltfläche können Sie die Ergebnisse in einer Datei speichern, wobei *.rpt das Standardsuffix ist.

## <a name="verify-your-query-window-connection-properties"></a>Überprüfen von Verbindungseigenschaften des Abfragefensters
Informationen zu Verbindungseigenschaften finden Sie unter den Ergebnissen einer Abfrage. 
- Nachdem Sie die Abfrage aus dem vorherigen Schritt ausgeführt haben, können Sie sich die Verbindungseigenschaften im unteren Bereich des Abfragefensters ansehen.
    - Hier wird angezeigt, mit welchem Server und welcher Datenbank Sie verbunden sind. Außerdem ist der Benutzername zu sehen, mit dem Sie angemeldet sind.
    - Des Weiteren sind auch die Abfragedauer und die Anzahl der Zeilen sichtbar, die von der zuvor ausgeführten Abfrage zurückgegeben wurden.
    
    ![Verbindungseigenschaften](media/connect-query-sql-server/connectionproperties.png)  
    In dieser Abbildung werden die Ergebnisse in der **Textansicht** dargestellt.  

## <a name="change-server-connection-within-query-window"></a>Ändern der Serververbindung im Abfragefenster
Mit den folgenden Schritten können Sie die Serververbindung für das aktuelle Abfragefenster ändern:
1. Klicken Sie mit der mit der rechten Maustaste in das Abfragefenster und rufen Sie „Verbindung“ > „Verbindung ändern“ auf.
2. Dadurch wird das Dialogfeld **Connect to Server** (Verbindung mit Server herstellen) im Dialogfeld erneut geöffnet, sodass Sie für die Abfrageverbindung einen anderen Server festlegen können. 
 
   ![Verbindung ändern](media/connect-query-sql-server/changeconnection.png)
   - Beachten Sie, dass diese Änderung keine Auswirkung auf den Server hat, mit dem der **Objekt-Explorer** verbunden ist. Die Änderung betrifft ausschließlich das aktuelle Abfragefenster. 



