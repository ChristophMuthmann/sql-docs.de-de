---
title: "Lernprogramm: Aktivieren Sie die fünf langsamste Abfragen Beispiel Widget - SQL-Vorgänge Studio (Vorschau) | Microsoft Docs"
description: "Dieses Lernprogramm veranschaulicht, wie die fünf langsamsten Abfragen Beispiel-Widget im Dashboard für die Datenbank aktiviert wird."
ms.custom: tools|sos
ms.date: 11/16/2017
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
ms.openlocfilehash: fc30051dff2bef07ac3e7d06aa98d92d4e05e79e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Lernprogramm: Hinzufügen der *fünf langsamsten Abfragen* Beispiel Widget auf die Datenbank-Dashboard

Dieses Lernprogramm demonstriert das Hinzufügen von mindestens einem der [!INCLUDE[name-sos](../includes/name-sos-short.md)]des integrierten Beispiel Widgets auf die *datenbankdashboard* schnell die fünf langsamsten Abfragen einer Datenbank angezeigt. Sie erfahren außerdem, wie die Details der langsamen Abfragen und Abfragepläne mit [!INCLUDE[name-sos](../includes/name-sos-short.md)]Funktionen. Bei diesem Lernprogramm erfahren Sie, wie Sie:

> [!div class="checklist"]
> * Aktivieren Sie Abfragespeicher in einer Datenbank
> * Hinzufügen von Widgets vorgefertigten Einblicke mit dem datenbankdashboard
> * Anzeigen von Details zu den langsamsten Abfragen der Datenbank
> * Anzeigen der Abfrageausführungspläne für langsamen Abfragen

[!INCLUDE[name-sos](../includes/name-sos-short.md)]enthält mehrere Insight Widgets Out-of-the-Box an. Dieses Lernprogramm veranschaulicht das Hinzufügen der *Query-Daten-Store-Db-Insight* Widget, aber die Schritte entsprechen im Wesentlichen für alle Widgets hinzufügen.

## <a name="prerequisites"></a>Voraussetzungen

Dieses Lernprogramm erfordert die SQL Server- oder Azure SQL-Datenbank *TutorialDB*. Zum Erstellen der *TutorialDB* Datenbank, führen Sie eines der folgenden Schnellstarts:

- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des SQL Server ab[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des Azure SQL-Datenbank ab[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>Der Abfragespeicher für die Datenbank aktivieren

Das Widget in diesem Beispiel erfordert *Abfragespeicher* werden daher führen folgende Transact-SQL (T-SQL)-Anweisung für die Datenbank aktiviert:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-an-insight-widget-to-your-database-dashboard"></a>Fügen Sie ein Insight Widget hinzu "", Datenbank-Dashboard

Um ein Widget Einblicke zu Ihrem Dashboard hinzuzufügen, bearbeiten die *dashboard.database.widgets* festlegen, die Ihrem *Benutzereinstellungen* Datei.

1. Öffnen Sie *Benutzereinstellungen* durch Drücken von **STRG + UMSCHALT + P** So öffnen die *Befehl Palette*.
2. Typ *Einstellungen* wählen Sie im Suchfeld und aus den verfügbaren Einstellungen **Voreinstellungen: Öffnen von Benutzereinstellungen**.

   ![Befehl des Benutzers öffnen-Einstellungen](./media/tutorial-qds-sql-server/open-user-settings.png)

2. Typ *Dashboard* in die Suche der Einstellungen und suchen **dashboard.database.widgets**.

   ![Sucheinstellungen](./media/tutorial-qds-sql-server/search-settings.png)

3. Anpassen der **dashboard.database.widgets** festlegen, zeigen Sie auf das Stiftsymbol links neben der **dashboard.database.widgets** Text, klicken Sie auf **bearbeiten**  >  **Kopieren, um Einstellungen**.

4. Nach dem Kopieren der Einstellungen für **dashboard.database.widgets**, platzieren Sie den Cursor am Ende der Zeile nach der öffnenden Klammer, drücken Sie **EINGABETASTE**, und fügen Sie wie folgt eine geschweifte Klammer (die schließende geschweifte Klammer wird automatisch angezeigt):

   ```json
   "dashboard.database.widgets": [
   {}
   ```
5. Mit dem Mauszeiger in der geschweiften Klammern, drücken Sie die **STRG + LEERTASTE** , und wählen Sie **Namen**. 
6. Beenden Sie das Einrichten des Widgets, sieht es wie folgt:

   ```json
    "dashboard.database.widgets": [
        {
            "name": "slow queries widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "query-data-store-db-insight": null
            }
        }
    ...
    ```

5. Drücken Sie **STRG + S** zum Speichern der geänderten **Benutzereinstellungen**.

6. Öffnen der *datenbankdashboard* durch Navigieren zum **TutorialDB** in der *Server* Randleiste, mit der rechten Maustaste und wählen Sie **verwalten**.

   ![Open-dashboard](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. Das Widget Einblick wird auf dem Dashboard angezeigt: 

   ![QDS-widget](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>Insight-Details für Weitere Informationen anzeigen

1. Um zusätzliche Informationen für ein Widget Einblicke anzuzeigen, klicken Sie auf die Auslassungspunkte (**...** ) in der oberen rechten, und wählen **Details anzeigen**.
2. Um weitere Details für ein Element anzuzeigen, wählen Sie ein beliebiges Element in **Diagrammdaten** Liste.

   ![Insight-Detail-Dialogfeld](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. Mit der rechten Maustaste **Query_sql_txt** in **Elementdetails** , und klicken Sie auf **Zelle kopieren**.

4. Schließen der **Insights** Bereich.

## <a name="view-the-query-plan"></a>Zeigen Sie den Abfrageplan an 

1. Öffnen Sie einen neues Abfrage-Editor, indem Sie mit **STRG + N**.

2. Geben Sie den Abfragetext aus den vorherigen Schritten in den Editor ein.

3. Klicken Sie auf **erläutern**.

   ![Insight QDS erklären](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. Zeigen Sie den Abfrageausführungsplan an:

   ![Showplan](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>Speichern Sie und öffnen Sie einen Abfrageplan 

1. Öffnen Sie das Insight-Dialogfeld "Details" ein.
2. Wählen Sie eine Abfrage Elemente.
2. Mit der rechten Maustaste **Query_plan** Wert ein, und wählen Sie **Zelle kopieren**

   ![Insights QDS plan](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. Drücken Sie **STRG + N** um einen neuen Editor zu öffnen.

4. Fügen Sie den kopierten Plan in Editor ein.

5. Drücken Sie **STRG + S** zum Speichern der Datei, und ändern die Dateierweiterung *.sqlplan*. Für dieses Lernprogramm benennen Sie die Datei *slowquery.sqlplan*.

6. Der Abfrageplan wird geöffnet, [!INCLUDE[name-sos](../includes/name-sos-short.md)]des Abfrage-Plan-Viewer:

   ![Insights QDS plan](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>Nächste Schritte
In diesem Lernprogramm haben Sie gelernt, wie:
> [!div class="checklist"]
> * Aktivieren Sie Abfragespeicher in einer Datenbank
> * Fügen Sie ein Insight-Widget hinzu "" mit dem datenbankdashboard
> * Anzeigen von Details zu den langsamsten Abfragen der Datenbank
> * Anzeigen der Abfrageausführungspläne für langsamen Abfragen


Informationen zum Aktivieren der **-Tabelle der speicherplatznutzung** Insight zugreifen können, führen Sie den nächsten Lernprogrammen:

> [!div class="nextstepaction"]
> [Aktivieren der Tabelle Platz Beispiel Einblicke Widgets](tutorial-table-space-sql-server.md)