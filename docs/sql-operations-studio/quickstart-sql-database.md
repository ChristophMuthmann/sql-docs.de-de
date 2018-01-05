---
title: "Schnellstart: Eine Verbindung herstellen und Abfragen eine Azure SQL-Datenbank, die mit SQL-Vorgänge Studio (Vorschau) | Microsoft Docs"
description: "Dieser Schnellstart veranschaulicht, wie SQL-Vorgänge Studio (Vorschau) zum Herstellen einer Verbindung mit einer SQL-Datenbank, und führen Sie eine Abfrage"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0e2d48ed411f883a904decce5d836dde7aaa41b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>Schnellstart: Verwenden [!INCLUDE[name-sos](../includes/name-sos-short.md)] zum Verbinden und Abfragen von Azure SQL-Datenbank

Dieser Schnellstart veranschaulicht, wie  *[!INCLUDE[name-sos](../includes/name-sos-short.md)]*  zum Herstellen einer Verbindung mit einer Azure SQL-Datenbank, und verwenden dann Transact-SQL (T-SQL)-Anweisungen zum Erstellen der *TutorialDB* verwendet [!INCLUDE[name-sos](../includes/name-sos-short.md)] Lernprogramme.

## <a name="prerequisites"></a>Voraussetzungen

Um diesen Schnellstart durchzuführen, müssen Sie [!INCLUDE[name-sos](../includes/name-sos-short.md)], und eine Azure SQL-Server.

- [Installieren Sie [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Wenn Sie eine Azure SQL-Server noch nicht haben, führen Sie eines der folgenden Azure SQL-Datenbank-Schnellstarts (Beachten Sie den Servernamen und Anmeldeinformationen!):

- [Erstellen Sie DB - Portal.](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Erstellen Sie DB - CLI.](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Erstellen von DB - PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Herstellen einer Verbindung mit dem Azure SQL-Datenbankserver

Verwendung [!INCLUDE[name-sos](../includes/name-sos-short.md)] zum Herstellen einer Verbindung mit Ihrem Azure SQL-Datenbankserver.

1. Die erste Ausführung [!INCLUDE[name-sos](../includes/name-sos-short.md)] der **Verbindung** Seite sollte geöffnet werden. Wenn die **Verbindung** keine Seite öffnen, klicken Sie auf die **neue Verbindung** Symbol in der **Server** Randleiste:
   
   ![Symbol "neue Verbindung"](media/quickstart-sql-database/new-connection-icon.png)

2. In diesem Artikel verwendet *SQL-Anmeldung*, aber *Windows-Authentifizierung* wird ebenfalls unterstützt. Füllen Sie die Felder wie folgt aus:

   | Einstellung       | Vorgeschlagener Wert | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servername** | Der vollqualifizierte Servername | Der Name sollte etwa wie folgt sein: **servername.database.windows.net** |
   | **Authentifizierung** | SQL-Anmeldung| In diesem Lernprogramm wird die SQL-Authentifizierung verwendet. |
   | **User name** | Das Konto des Serveradministrators | Dabei handelt es sich um das Konto, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort (SQL-Anmeldung)** | Das Kennwort für das Konto des Serveradministrators | Dabei handelt es sich um das Kennwort, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort speichern** | Ja oder Nein | Wählen Sie Ja aus, wenn Sie nicht, das Kennwort jedes Mal eingeben möchten. |
   | **Datenbankname** | *leer lassen* | Der Name der Datenbank, die, der Sie herstellen möchten. |
   | **Gruppe "Server"** | Wählen Sie<Default> | Wenn Sie eine Servergruppe erstellt haben, können Sie mit einer bestimmten Servergruppe festlegen. | 

   ![Symbol "neue Verbindung"](media/quickstart-sql-database/new-connection-screen.png)  

3. Wenn Sie eine Fehlermeldung zur Firewall erhalten, müssen Sie eine Firewallregel erstellen. Um eine Firewallregel erstellen, finden Sie unter [Firewallregeln](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

4. Nach einer erfolgreichen auf Ihrem Server in erscheint der *Server* Randleiste.

## <a name="create-the-tutorial-database"></a>Erstellen der Tutorial-Datenbank

Die *TutorialDB* Datenbank dient in mehreren [!INCLUDE[name-sos](../includes/name-sos-short.md)] Lernprogramme.

1. Klicken Sie mit der rechten Maustaste auf den Azure SQL-Server in der Randleiste mit Servern, und wählen Sie **neue Abfrage.**

1. Fügen Sie den folgenden Ausschnitt in den Abfrage-Editor ein.

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```

1. Um die Abfrage auszuführen, klicken Sie auf **ausführen**.


## <a name="create-a-table"></a>Erstellen einer Tabelle

Weiterhin mit der Abfrage-Editor verbunden ist die *master* Datenbank, aber wir möchten Erstellen einer Tabelle in der *TutorialDB* Datenbank. 

1. Ändern den Verbindungskontext für **TutorialDB**:

   ![Kontext ändern](media/quickstart-sql-database/change-context.png)



1. Fügen Sie den folgenden Ausschnitt in den Abfrage-Editor ein.

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
1. Um die Abfrage auszuführen, klicken Sie auf **ausführen**.

## <a name="insert-rows"></a>Einfügen von Zeilen

1. Fügen Sie den folgenden Ausschnitt in den Abfrage-Editor ein:
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

1. Um die Abfrage auszuführen, klicken Sie auf **ausführen**.

## <a name="view-the-result"></a>Zeigen Sie das Ergebnis an.
1. Fügen Sie den folgenden Ausschnitt in den Abfrage-Editor ein.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Um die Abfrage auszuführen, klicken Sie auf **ausführen**.

   ![Select-Ergebnisse](media/quickstart-sql-database/select-results.png)


## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Andere Artikel in dieser Auflistung bauen auf diesem Schnellstart. Wenn Sie auf Weiter mit nachfolgenden Schnellstarts arbeiten möchten, nicht bereinigen die Ressourcen, die in diesem Schnellstart erstellt. Wenn Sie nicht beabsichtigen, um den Vorgang fortzusetzen, verwenden Sie die folgenden Schritte aus, um Ressourcen, die von diesem Schnellstart im Azure-Portal erstellte zu löschen.
Bereinigen von Ressourcen durch Löschen von Ressourcengruppen, die Sie ohne mehr benötigen. Weitere Informationen finden Sie unter [Bereinigen von Ressourcen](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Nächste Schritte

Nun, dass Sie erfolgreich eine Verbindung eine Azure SQL-Datenbank hergestellt haben und eine Abfrage ausgeführt haben, probieren Sie die [Code-Editor-Lernprogramm](tutorial-sql-editor.md).
