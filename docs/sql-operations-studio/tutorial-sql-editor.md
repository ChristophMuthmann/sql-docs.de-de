---
title: 'Lernprogramm: Verwenden den SQL-Vorgänge Studio (Vorschau) Transact-SQL-Editor zum Erstellen von Datenbankobjekten | Microsoft Docs'
description: Dieses Lernprogramm veranschaulicht die wichtigsten Funktionen in SQL Operations Studio (Vorschau), die mithilfe des T-SQL-vereinfachen.
ms.custom: tools|sos
ms.date: 03/13/2018
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.openlocfilehash: 608ae192eacdfec2c657484015d967ae0506e791
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>Tutorial: Verwenden von Transact-SQL-Editor zum Erstellen von Datenbankobjekten- [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Erstellen und Ausführen von Abfragen, werden gespeicherte Prozeduren, Skripts usw. die zentralen Aufgaben Datenbankexperten. Dieses Lernprogramm veranschaulicht die wichtigsten Funktionen in der T-SQL-Editor, um Datenbankobjekte zu erstellen.

In diesem Lernprogramm erfahren Sie, wie Sie [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] an:
> [!div class="checklist"]
> * Suchen von Datenbankobjekten
> * Bearbeiten Sie Tabellendaten 
> * Verwenden Sie Ausschnitte, um schnell T-SQL schreiben
> * Ansicht Datenbank Details zum Objekt mit *Peek-Definition* und *Gehe zu Definition*


## <a name="prerequisites"></a>Erforderliche Komponenten

Dieses Lernprogramm erfordert die SQL Server- oder Azure SQL-Datenbank *TutorialDB*. Zum Erstellen der *TutorialDB* Datenbank, führen Sie eines der folgenden Schnellstarts:

- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des SQL Server ab [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des Azure SQL-Datenbank ab [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>Schnell ermitteln Sie ein Datenbankobjekt, und führen Sie eine häufige Aufgabe

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] bietet eine Suche Widget Datenbankobjekte schnell zu finden. Die Ergebnisliste enthält ein Kontextmenü für allgemeine Aufgaben, die relevant für das ausgewählte Objekt, z. B. *Daten bearbeiten* für eine Tabelle.

1. Öffnen die Randleiste Servern (**STRG + G**), erweitern Sie **Datenbanken**, und wählen Sie **TutorialDB**. 

1. Öffnen der *TutorialDB Dashboard* durch Rechtsklicken auf **TutorialDB** auswählen und **verwalten** aus dem Kontextmenü:

   ![Kontextmenü: Verwalten](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. Auf dem Dashboard mit der Maustaste **Dbo. Kunden** (im Widget "Suchen"), und wählen Sie **Daten bearbeiten**.
   
   > [!TIP]
   > Verwenden Sie für Datenbanken mit vielen Objekten das Widget "Suche", um schnell zu finden, die Tabelle, Sicht usw., die Sie suchen.

   ![Schnellsuche-widget](./media/tutorial-sql-editor/quick-search-widget.png)

1. Bearbeiten der **E-Mail** Spalte in der ersten Zeile Typ *orlando0@adventure-works.com*, und drücken Sie **EINGABETASTE** um die Änderung zu speichern.

   ![Bearbeiten von Daten](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>Verwenden Sie zum Erstellen gespeicherter Prozeduren T-SQL-Ausschnitten

SQL-Vorgänge Studio stellt viele integrierte T-SQL-Ausschnitte für das schnelle Erstellen von Anweisungen bereit.


1. Öffnen Sie einen neues Abfrage-Editor, indem Sie mit **STRG + N**.

2. Typ **Sql** im Editor, Pfeil nach unten bis zum **SqlCreateStoredProcedure**, und drücken Sie die *Registerkarte* Schlüssel (oder *EINGABETASTE*) gespeicherten erstellen laden Prozedur-Ausschnitt.

   ![Snippet-Liste](./media/tutorial-sql-editor/snippet-list.png)

3. Der erstellen-gespeicherte Prozedur-Ausschnitt enthält zwei Felder, die zur schnellen Bearbeitung einrichten *StoredProcedureName* und *SchemaName*. Wählen Sie *StoredProcedureName*, mit der rechten Maustaste, und wählen **ändern alle Vorkommen**. Geben Sie nun *GetCustomer* und alle *StoredProcedureName* Einträge zu ändern, um *GetCustomer*.

   ![Codeausschnittauswahl](./media/tutorial-sql-editor/snippet.png)

5. Ersetzen Sie alle Vorkommen von *SchemaName* auf *Dbo*. 
6. Der Ausschnitt enthält für Platzhalterparameter und Nachrichtentext, die Aktualisierung benötigt. Die *EXECUTE* -Anweisung enthält ebenfalls Platzhaltertext, da die Prozedur verfügt über wie viele Parameter unbekannt nicht. Für dieses Lernprogramm aktualisieren Sie den Ausschnitt sieht es so wie im folgenden Code:

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
    SELECT  c.CustomerId, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerId = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. Um die gespeicherte Prozedur erstellen, und geben Sie ihm einen Testlauf, drücken Sie die **F5**.

Nun wird die gespeicherte Prozedur erstellt, und die **Ergebnisse** Bereich zeigt die zurückgegebenen Kunden im JSON-Format. Um formatierte JSON anzuzeigen, klicken Sie auf die zurückgegebenen Datensatz. 


## <a name="use-peek-definition"></a>Verwenden von "Definition einsehen" 

SQL-Vorgänge Studio bietet die Möglichkeit zum Anzeigen der Definition einer Objekte mit der Peek-Definition-Funktion. In diesem Abschnitt wird eine zweite gespeicherte Prozedur erstellt und "Definition einsehen" verwendet, um festzustellen, welche Spalten in einer Tabelle, um schnell den Text der gespeicherten Prozedur zu erstellen sind.

1. Öffnen Sie einen neuen Editor durch Drücken von **STRG + N**. 

2. Typ *Sql* im Editor, Pfeil nach unten bis zum *SqlCreateStoredProcedure*, und drücken Sie die *Registerkarte* Schlüssel (oder *EINGABETASTE*) gespeicherten erstellen laden Prozedur-Ausschnitt.
3. Geben Sie in *SetCustomer* für *StoredProcedureName* und *Dbo* für *SchemaName*

3. Ersetzen Sie die @param -Platzhalter durch die folgenden Parameterdefinition:

   ```sql
   @json_val nvarchar(max)
   ```

4. Ersetzen Sie den Text der gespeicherten Prozedur durch den folgenden Code ein:
   ```sql
   INSERT INTO dbo.Customers
   ```

5. In der *einfügen* Zeile Sie soeben hinzugefügten mit der rechten Maustaste **Dbo. Kunden** , und wählen Sie **Peek-Definition**.

   !["Definition einsehen"](./media/tutorial-sql-editor/peek-definition.png)

6. Die Tabellendefinition wird angezeigt, sodass Sie schnell sehen können, welche Spalten in der Tabelle sind. Finden Sie in der Spaltenliste, um die Anweisungen für die gespeicherte Prozedur auf einfache Weise abschließen. Beenden Sie die INSERT-Anweisung, die Sie zuvor hinzugefügt haben, um den Text der gespeicherten Prozedur abgeschlossen ist, und Schließen des Peek-definitionsfensters erstellen:

   ```sql
   INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
    )
   ```
7. Löschen (oder kommentieren Sie Sie aus) das *EXECUTE* Befehl am Ende der Abfrage.
8. Die gesamte Anweisung sollte wie der folgende Code aussehen:

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
       INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. Zum Erstellen der *SetCustomer* gespeicherte Prozedur, drücken Sie **F5**.

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>Verwenden Sie Abfrageergebnisse als JSON zum Testen der SetCustomer gespeicherte Prozedur speichern

Die *SetCustomer* im vorherigen Abschnitt erstellte gespeicherte Prozedur erfordert JSON Daten übergeben werden, in der *@json_val* Parameter. In diesem Abschnitt veranschaulicht das Abrufen eine ordnungsgemäß formatierte Bit der JSON-der Parameter übergeben, sodass Sie die gespeicherte Prozedur testen können.

1. In der **Server** Randleiste Maustaste die *Dbo. Kunden* Tabelle, und klicken Sie auf **oberste 1000 Zeilen auswählen**.

2. Wählen Sie die erste Zeile in der Ergebnisansicht, stellen Sie sicher, dass die gesamte Zeile ausgewählt ist (klicken Sie auf die Zahl 1 in der Spalte ganz links), und wählen Sie **speichern als JSON**.  
3. Ändern Sie den Ordner an einem Speicherort Sie erinnern Dadurch können Sie löschen Sie die Datei später (für Beispiel Desktop), und klicken Sie auf **speichern**. Die JSON-Format geöffnet.

   ![Speichern Sie als JSON](./media/tutorial-sql-editor/save-as-json.png)

4. Wählen Sie die JSON-Daten im Editor, und kopieren Sie ihn.
5. Öffnen Sie einen neuen Editor durch Drücken von **STRG + N**.
6. Die vorherigen Schritte anzeigen, wie Sie einfach die ordnungsgemäß formatierten Daten den Aufruf abgeschlossen abrufen können die *SetCustomer* Prozedur. Sie sehen, dass der folgende Code verwendet das gleiche JSON-Format mit neuen Kundendetails, sodass wir testen können die *SetCustomer* Prozedur. Die Anweisung enthält Syntax zum Deklarieren Sie den Parameter, und führen Sie die neue Get und set-Prozeduren. Fügen Sie die kopierten Daten aus dem vorherigen Abschnitt können, und sie bearbeiten, damit sie das folgende Beispiel entspricht oder einfach die folgende Anweisung in der Abfrage-Editor einfügen.

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerId": 5,
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


Informationen zum Aktivieren der **fünf langsamsten Abfragen** Widget "", den nächsten Lernprogrammen abzuschließen:

> [!div class="nextstepaction"]
> [Aktivieren Sie das langsame Abfragen Beispiel Insight-widget](tutorial-qds-sql-server.md)
