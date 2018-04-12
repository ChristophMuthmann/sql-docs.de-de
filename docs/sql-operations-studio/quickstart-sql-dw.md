---
title: 'Schnellstart: Eine Verbindung herstellen und Abfragen einer Azure SQL Data Warehouse mit SQL Operations Studio (preview) | Microsoft Docs'
description: Dieser Schnellstart veranschaulicht, wie SQL Operations Studio (preview) zum Herstellen einer Verbindung mit einer SQL-Datenbank, und führen Sie eine Abfrage
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d4ed7d25abb2780c719c5b8201ecae54e8e86bf
ms.sourcegitcommit: 6c06267f3eeeb3f0d6fc4c57e1387621720ca8bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/09/2018
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>Schnellstart: Verwenden [!INCLUDE[name-sos](../includes/name-sos-short.md)] eine Verbindung herstellen und Abfragen von Daten in Azure SQL Data Warehouse

Dieser Schnellstart veranschaulicht, wie [!INCLUDE[name-sos](../includes/name-sos-short.md)] zum Herstellen einer Verbindung mit Azure SQL Datawarehouse, und verwenden Sie Transact-SQL-Anweisungen erstellen, einfügen, und wählen Sie die Daten. 

## <a name="prerequisites"></a>Erforderliche Komponenten
Um diesen Schnellstart durchzuführen, müssen Sie [!INCLUDE[name-sos](../includes/name-sos-short.md)], und eine Azure SQL Datawarehouse.

- [Installieren Sie [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Wenn Sie eine SQL Datawarehouse noch nicht haben, finden Sie unter [Erstellen eines SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Denken Sie daran, den Servernamen und Anmeldeinformationen!


## <a name="connect-to-your-data-warehouse"></a>Herstellen einer Verbindung mit Ihrem Datawarehouse

Verwendung [!INCLUDE[name-sos](../includes/name-sos-short.md)] zum Herstellen einer Verbindung mit Ihrem Azure SQL Data Warehouse-Server.

1. Die erste Ausführung [!INCLUDE[name-sos](../includes/name-sos-short.md)] der **Verbindung** Seite sollte geöffnet werden. Wenn Sie sehen die **Verbindung** auf **Verbindung hinzufügen**, oder die **neue Verbindung** Symbol in der **Server** Randleiste:
   
   ![Symbol "neue Verbindung"](media/quickstart-sql-dw/new-connection-icon.png)

2. In diesem Artikel verwendet *SQL-Anmeldung*, aber *Windows-Authentifizierung* wird ebenfalls unterstützt. Ausfüllen der Felder, die wie folgt mithilfe der Servername, Benutzername und das Kennwort für *Ihrer* Azure SQL-Server:

   | Einstellung       | Empfohlener Wert | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servername** | Der vollqualifizierte Servername | Der Name sollte etwa wie folgt sein: **sqldwsample.database.windows.net** |
   | **Authentifizierung** | SQL-Anmeldung| In diesem Lernprogramm wird die SQL-Authentifizierung verwendet. |
   | **Benutzername** | Das Konto des Serveradministrators | Dabei handelt es sich um das Konto, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort (SQL-Anmeldung)** | Das Kennwort für das Konto des Serveradministrators | Dabei handelt es sich um das Kennwort, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort speichern** | Ja oder Nein | Wählen Sie Ja aus, wenn Sie nicht, das Kennwort jedes Mal eingeben möchten. |
   | **Datenbankname** | *Leer lassen* | Dies ist der Name der Datenbank, mit der eine Verbindung hergestellt werden soll. |
   | **Gruppe "Server"** | Wählen Sie<Default> | Wenn Sie eine Servergruppe erstellt haben, können Sie mit einer bestimmten Servergruppe festlegen. | 

   ![Symbol "neue Verbindung"](media/quickstart-sql-dw/new-connection-screen.png) 

3. Wenn Ihr Server eine Firewallregel, die SQL Operations Studio eine Verbindung herstellen, sodass keine der **neue Firewallregel erstellen** bilden wird geöffnet. Füllen Sie das Formular zum Erstellen einer neuen Firewallregel. Weitere Informationen finden Sie unter [Firewallregeln](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Neue Firewallregel](media/quickstart-sql-dw/firewall.png)  

4. Nach dem Öffnen einer erfolgreichen auf Ihrem Server in der *Server* Randleiste.

## <a name="create-the-tutorial-data-warehouse"></a>Erstellen Sie das Lernprogramm Datawarehouse
1. Klicken Sie mit der rechten Maustaste auf dem Server im Objekt-Explorer, und wählen Sie **neue Abfrage.**

1. Fügen Sie den folgenden Ausschnitt in den Abfrage-Editor, und klicken Sie auf **ausführen**:

   ```sql
    IF NOT EXISTS (
       SELECT name
       FROM sys.databases
       WHERE name = N'TutorialDB'
    )
    CREATE DATABASE [TutorialDB] (EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
    GO  
    
    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
   ```


## <a name="create-a-table"></a>Erstellen einer Tabelle

Weiterhin mit der Abfrage-Editor verbunden ist die *master* Datenbank, aber wir möchten Erstellen einer Tabelle in der *TutorialDB* Datenbank. 

1. Ändern den Verbindungskontext für **TutorialDB**:

   ![Kontext ändern](media/quickstart-sql-database/change-context.png)


1. Fügen Sie den folgenden Ausschnitt in den Abfrage-Editor, und klicken Sie auf **ausführen**:

   > [!NOTE]
   > Sie können fügen diese Option, um, oder überschreiben Sie die vorherige Abfrage im Editor. Beachten Sie, dass beim Klicken auf **ausführen** führt nur die Abfrage, die ausgewählt wird. Wenn nichts ausgewählt ist, klicken Sie auf **ausführen** führt alle Abfragen im Editor.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>Einfügen von Zeilen

1. Fügen Sie den folgenden Ausschnitt in den Abfrage-Editor, und klicken Sie auf **ausführen**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```


## <a name="view-the-result"></a>Zeigen Sie das Ergebnis an.
1. Fügen Sie den folgenden Ausschnitt in den Abfrage-Editor, und klicken Sie auf **ausführen**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Die Ergebnisse der Abfrage werden angezeigt:

   ![Select-Ergebnisse](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Andere Artikel in dieser Auflistung bauen auf diesem Schnellstart. Wenn Sie auf Weiter mit nachfolgenden Schnellstarts arbeiten möchten, nicht bereinigen die Ressourcen, die in diesem Schnellstart erstellt. Wenn Sie nicht beabsichtigen, um den Vorgang fortzusetzen, verwenden Sie die folgenden Schritte aus, um Ressourcen, die von diesem Schnellstart im Azure-Portal erstellte zu löschen.
Bereinigen von Ressourcen durch Löschen von Ressourcengruppen, die Sie ohne mehr benötigen. Weitere Informationen finden Sie unter [Bereinigen von Ressourcen](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-portal#clean-up-resources).


## <a name="next-steps"></a>Nächste Schritte

Probieren Sie erfolgreich eine Verbindung hergestellt haben eine Azure SQL Datawarehouse und die Ausführung einer Abfrage, die [Code-Editor-Lernprogramm](tutorial-sql-editor.md).