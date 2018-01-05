---
title: "Lernprogramm: Verwenden den SQL-Vorgänge Studio (Vorschau) Transact-SQL-Editor zum Erstellen von Datenbankobjekten | Microsoft Docs"
description: Dieses Lernprogramm veranschaulicht die wichtigsten Funktionen in SQL Operations Studio (Vorschau), die mithilfe des T-SQL-vereinfachen.
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2754a998963be5a25d00aa58dcb9b4105bb8f37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>Tutorial: Verwenden von Transact-SQL-Editor zum Erstellen von Datenbankobjekten-[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Erstellen und Ausführen von Abfragen, werden gespeicherte Prozeduren, Skripts usw. die zentralen Aufgaben Datenbankexperten. Dieses Lernprogramm veranschaulicht die wichtigsten Funktionen in der T-SQL-Editor, um Datenbankobjekte zu erstellen.

In diesem Lernprogramm erfahren Sie, wie Sie [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] an:
> [!div class="checklist"]
> * Suchen von Datenbankobjekten
> * Bearbeiten Sie Tabellendaten 
> * Verwenden Sie Ausschnitte, um schnell T-SQL schreiben
> * Ansicht Datenbank Details zum Objekt mit *Peek-Definition* und *Gehe zu Definition*


## <a name="prerequisites"></a>Voraussetzungen

Dieses Lernprogramm erfordert die SQL Server- oder Azure SQL-Datenbank *TutorialDB*. Zum Erstellen der *TutorialDB* Datenbank, führen Sie eines der folgenden Schnellstarts:

- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des SQL Server ab[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des Azure SQL-Datenbank ab[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>Schnell ermitteln Sie ein Datenbankobjekt, und führen Sie eine häufige Aufgabe

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]bietet eine Suche Widget Datenbankobjekte schnell zu finden. Die Ergebnisliste enthält ein Kontextmenü für allgemeine Aufgaben, die relevant für das ausgewählte Objekt, z. B. *Daten bearbeiten* für eine Tabelle.

1. Öffnen die Randleiste Servern (**STRG + G**), erweitern Sie **Datenbanken**, und wählen Sie **TutorialDB**. 

1. Öffnen der *TutorialDB Dashboard* dazu **verwalten** aus dem Kontextmenü.

   ![Kontextmenü: Verwalten](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. Suchen Sie die *Kunden* Tabelle dazu *Cus* im Widget "Suchen".
1. Mit der rechten Maustaste **Dbo. Kunden** , und wählen Sie **Bearbeiten von Daten**.

   ![Schnellsuche-widget](./media/tutorial-sql-editor/quick-search-widget.png)

1. Bearbeiten der **E-Mail** Spalte in der ersten Zeile Typ  *orlando0@adventure-works.com* , und drücken Sie **EINGABETASTE** um die Änderung zu speichern.

   ![Bearbeiten von Daten](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-a-stored-procedure"></a>Verwenden Sie zum Erstellen einer gespeicherten Prozedur T-SQL-Ausschnitten

### <a name="use-snippets-in-includename-sos-shortincludesname-sos-shortmd"></a>Verwenden von Codeausschnitten in[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]

1. Öffnen Sie einen neues Abfrage-Editor, indem Sie mit **STRG + N**.

2. Typ **Sql** im Editor, Pfeil nach unten bis zum **SqlCreateStoredProcedure**, und drücken Sie die *Registerkarte* , um den neuen Ausschnitt der gespeicherten Prozedur zu laden.

   ![Snippet-Liste](./media/tutorial-sql-editor/snippet-list.png)

3. Typ *GetCustomer* und alle *StoredProcedureName* Einträge zu ändern, um *GetCustomer*. 

   ![Codeausschnittauswahl](./media/tutorial-sql-editor/snippet.png)

4. Ersetzen Sie den Rest der gespeicherten Prozedur mit der folgenden T-SQL an:

    ```sql
    -- Create a new stored procedure called 'getCustomer' in schema 'dbo'
    -- Drop the stored procedure if it already exists
    IF EXISTS (
    SELECT *
    FROM INFORMATION_SCHEMA.ROUTINES
    WHERE SPECIFIC_SCHEMA = N'dbo'
    AND SPECIFIC_NAME = N'getCustomer'
    )
    DROP PROCEDURE dbo.getCustomer
    GO
    -- Create the stored procedure in the specified schema
    CREATE PROCEDURE dbo.getCustomer
    @ID int
    -- add more stored procedure parameters here
    AS
    -- body of the stored procedure
    SELECT  c.CustomerID, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerID = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. Um die gespeicherte Prozedur erstellen, und geben Sie ihm einen Testlauf, drücken Sie die **F5**.

## <a name="use-peek-definition-and-go-to-definition"></a>"Definition einsehen" Verwendung "und" Gehe zu Definition 

1. Öffnen Sie einen neuen Editor durch Drücken von **STRG + N**. 

2. Geben Sie ein, und wählen Sie **SqlCreateStoredProcedure** aus der Liste der Ausschnitt Vorschlag. Geben Sie in **SetCustomer** für **StoredProcedureName** und **Dbo** für **SchemaName**

3. Ersetzen Sie die @param Zeilen mit den folgenden Parameterdefinition:

   ```sql
       @json_val nvarchar(max)
   ```

4. Ersetzen Sie den Text der gespeicherten Prozedur durch Folgendes:
   ```sql
   -- body of the stored procedure
   INSERT INTO dbo.Customers
   ```

5. Mit der rechten Maustaste **Dbo. Kunden** , und wählen Sie **Peek-Definition**.

   !["Definition einsehen"](./media/tutorial-sql-editor/peek-definition.png)

6. Führen folgende Insert-Anweisung mithilfe der Tabelle (Definition):

   ```sql
   INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
   ```
7. Die letzte Anweisung sollte Folgendes sein:

   ```sql
   -- Create a new stored procedure called 'setCustomer' in schema 'dbo'
   -- Drop the stored procedure if it already exists
   IF EXISTS (
   SELECT *
       FROM INFORMATION_SCHEMA.ROUTINES
       WHERE SPECIFIC_SCHEMA = N'dbo'
       AND SPECIFIC_NAME = N'setCustomer'
   )
   DROP PROCEDURE dbo.setCustomer
   GO
   -- Create the stored procedure in the specified schema
   CREATE PROCEDURE dbo.setCustomer
       @json_val nvarchar(max) 
   AS
       -- body of the stored procedure
       INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. Um das Skript auszuführen, drücken Sie die **F5**.

## <a name="use-save-query-results-as-json-to-test-our-stored-procedure"></a>Verwenden Sie Abfrageergebnisse als JSON So testen Sie die gespeicherte Prozedur speichern

1. **OBERSTE 1000 Zeilen auswählen** aus der *Dbo. Kunden* Tabelle.

2. Wählen Sie die erste Zeile in der Ergebnisansicht und auf **speichern als JSON**.  
3. Klicken Sie auf **speichern**, und es wird die markierte Zeile im JSON-Format geöffnet.

   ![Speichern Sie als JSON](./media/tutorial-sql-editor/save-as-json.png)

4. Wählen Sie die JSON-Daten, und kopieren Sie ihn.

5. Öffnen Sie eine neue Abfrage für *TutorialDB* und führen Sie das folgende Testskript unter Verwendung der JSON-Daten als eine Vorlage aus dem vorherigen Schritt. Ändern Sie die Werte für *CustomerID*, *Namen*, *Speicherort*, und *E-Mail*.

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerID": 5,
           "Name": "Lucy",
           "Location": "Canada",
           "Email": "lucy0@adventure-works.com"
       }
   ]'

   EXECUTE dbo.setCustomer @json_val = @json
   GO

   EXECUTE dbo.getCustomer @ID = 5
   ```

7. Führen Sie das Skript durch Drücken von **F5**. Das Skript fügt einen neuen Kunden und den neuen Kunden Informationen im JSON-Format zurückgegeben. Klicken Sie auf das Ergebnis um eine formatierte Ansicht zu öffnen.

   ![Testergebnis](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>Nächste Schritte
In diesem Lernprogramm haben Sie gelernt, wie:
> [!div class="checklist"]
> * Schnelle Suchen von Schemaobjekten
> * Bearbeiten Sie Tabellendaten 
> * Schreiben von T-SQL-Skript mithilfe von Ausschnitten
> * Erfahren Sie mehr über die Datenbankdetails-Objekt mit der Peek-Definition und Gehe zu Definition


Informationen zum Aktivieren der **fünf langsamsten Abfragen** Insight zugreifen können, führen Sie den nächsten Lernprogrammen:

> [!div class="nextstepaction"]
> [Aktivieren Sie das langsame Abfragen Beispiel Insight-widget](tutorial-qds-sql-server.md)
