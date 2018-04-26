---
title: 'Schnellstart: Verbinden und Abfragen von SQL Server mithilfe von SQL-Vorgänge Studio (Vorschau) | Microsoft Docs'
description: Dieser Schnellstart veranschaulicht, wie SQL-Vorgänge Studio (Vorschau) eine Verbindung mit SQL Server, und führen Sie eine Abfrage
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql
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
ms.openlocfilehash: a1820cd0a69313afa2a57b6d96721f375307cb71
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>Schnellstart: Eine Verbindung herstellen Sie und Fragen Sie mithilfe des SQL Server ab [!INCLUDE[name-sos](../includes/name-sos-short.md)]
Dieser Schnellstart veranschaulicht, wie [!INCLUDE[name-sos](../includes/name-sos-short.md)] zum Herstellen einer Verbindung mit SQL Server, und verwenden dann Transact-SQL (T-SQL)-Anweisungen zum Erstellen der *TutorialDB* verwendet [!INCLUDE[name-sos](../includes/name-sos-short.md)] Lernprogramme.

## <a name="prerequisites"></a>Erforderliche Komponenten

Um diesen Schnellstart durchzuführen, müssen Sie [!INCLUDE[name-sos](../includes/name-sos-short.md)], und der Zugriff auf einen SQL-Server.

- [Installieren Sie [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Wenn Sie Zugriff auf einen SQL-Server haben, wählen Sie Ihre Plattform aus den folgenden Links (Stellen Sie sicher, dass Sie Ihre SQL-Anmeldung und Kennwort merken!):
- [Windows: Herunterladen der SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS: Herunterladen von SQL Server 2017 für Docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)
- [Linux - Download SQL Server 2017 Developer Edition](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-overview#install) -müssen Sie nur die Schritte bis zu *Create "und" Abfragedaten*.


## <a name="connect-to-a-sql-server"></a>Herstellen einer Verbindung mit SQL Server

   
1. Starten Sie **[!INCLUDE[name-sos](../includes/name-sos-short.md)]**.
1. Die erste Ausführung *[!INCLUDE[name-sos](../includes/name-sos-short.md)]* der **Verbindung** Dialogfeld wird geöffnet. Wenn die **Verbindung** Dialogfeld nicht öffnen, klicken Sie auf die **neue Verbindung** Symbol in der **Server** Seite:
   
   ![Symbol "neue Verbindung"](media/quickstart-sql-server/new-connection-icon.png)

1. In diesem Artikel verwendet *SQL-Anmeldung*, aber *Windows-Authentifizierung* wird unterstützt. Füllen Sie die Felder wie folgt aus:
 
    - **Name des Servers:** "localhost"
    - **Authentifizierungstyp:** SQL-Anmeldung  
    - **Benutzername:** Benutzername für den SQL Server  
    - **Kennwort:** Kennwort für den SQLServer  
    - **Datenbankname:** dieses Feld leer lassen 
    - **Gruppe "Server":** \<Standard\>  

   ![Bildschirm für neue Verbindung](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>Erstellen einer Datenbank

Die folgenden Schritte erstellen Sie eine Datenbank namens **TutorialDB**:

1. Klicken Sie mit der rechten Maustaste auf Ihrem Server **"localhost"**, und wählen Sie **neue Abfrage.**
1. Fügen Sie den folgenden Ausschnitt in das Abfragefenster ein: 

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

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```
1. Um die Abfrage auszuführen, klicken Sie auf **ausführen** .

Nachdem die Abfrage abgeschlossen ist, die neue **TutorialDB** in der Liste der Datenbanken angezeigt. Wenn es nicht angezeigt wird, mit der rechten Maustaste die **Datenbanken** Knoten, und wählen **aktualisieren**.


## <a name="create-a-table"></a>Erstellen einer Tabelle

Weiterhin mit der Abfrage-Editor verbunden ist die *master* Datenbank, aber wir möchten Erstellen einer Tabelle in der *TutorialDB* Datenbank. 

1. Ändern den Verbindungskontext für **TutorialDB**:

   ![Kontext ändern](media/quickstart-sql-server/change-context.png)



1. Fügen Sie den folgenden Ausschnitt in das Abfragefenster ein, und klicken Sie auf **ausführen**:

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
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

Nachdem die Abfrage abgeschlossen ist, die neue **Kunden** Tabelle wird in der Liste der Tabellen angezeigt. Möglicherweise müssen Sie mit der rechten Maustaste die **TutorialDB > Tabellen** Knoten, und wählen **aktualisieren**.

## <a name="insert-rows"></a>Einfügen von Zeilen

- Fügen Sie den folgenden Ausschnitt in das Abfragefenster ein, und klicken Sie auf **ausführen**:

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



## <a name="view-the-data-returned-by-a-query"></a>Zeigen Sie die von einer Abfrage zurückgegebene Daten
1. Fügen Sie den folgenden Ausschnitt in das Abfragefenster ein, und klicken Sie auf **ausführen**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Die Ergebnisse der Abfrage werden angezeigt:

   ![Select-Ergebnisse](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>Nächste Schritte
Nachdem Sie erfolgreich eine Verbindung mit SQL Server und Ausführen einer Abfrage hergestellt haben, können Sie die [Code-Editor-Lernprogramm](tutorial-sql-editor.md).


