---
title: 'Lernprogramm: Erstellen Sie ein Widget eines benutzerdefinierten Einblicke in SQL-Vorgänge Studio (Vorschau) | Microsoft Docs'
description: Dieses Lernprogramm veranschaulicht, wie benutzerdefinierte Insight-Widgets erstellen, und fügen sie Datenbank- und Dashboards im SQL-Vorgänge Studio (Vorschau) hinzu.
ms.custom: tools|sos
ms.date: 11/15/2017
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
ms.workload: Inactive
ms.openlocfilehash: 97a5177bf4f0dd9e5ae3ae1b097285bd7a8d42b5
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="tutorial-build-a-custom-insight-widget"></a>Lernprogramm: Erstellen Sie eine benutzerdefinierte Insight-widget

Dieses Lernprogramm veranschaulicht, wie Sie eigene Abfragen Einblicke zu verwenden, um benutzerdefinierte Einblicke Widgets erstellen.

Bei diesem Lernprogramm erfahren Sie, wie Sie:
> [!div class="checklist"]
> * Führen Sie eine eigene Abfrage und zeigen Sie ihn in einem Diagramm
> * Erstellen Sie eine benutzerdefinierte Einblicke Widget aus dem Diagramm
> * Hinzufügen des Diagramms zu einem Server oder Datenbank-dashboard
> * Hinzufügen von Details zu Ihrer benutzerdefinierten Insight-widget

## <a name="prerequisites"></a>Voraussetzungen

Dieses Lernprogramm erfordert die SQL Server- oder Azure SQL-Datenbank *TutorialDB*. Zum Erstellen der *TutorialDB* Datenbank, führen Sie eines der folgenden Schnellstarts:

- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des SQL Server ab [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des Azure SQL-Datenbank ab [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>Eine eigene Abfrage auszuführen und das Ergebnis in einer Diagrammsicht anzeigen
Führen Sie in diesem Schritt ein Sql-Skript, um die aktuelle aktiven Sitzungen abzufragen.

1. Um einen neuen Editor zu öffnen, drücken Sie die **STRG + N**. 

2. Ändern den Verbindungskontext für **TutorialDB**.

3. Fügen Sie die folgende Abfrage in den Abfrage-Editor ein:

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. Speichern Sie die Abfrage-Editor eine \*.sql-Datei. Für dieses Lernprogramm speichern Sie das Skript *activeSession.sql*.

5. Um die Abfrage auszuführen, drücken Sie die **F5**.

6. Nachdem die Ergebnisse der Abfrage angezeigt werden, klicken Sie auf **als Diagramm anzeigen**, klicken Sie dann auf die **Diagramm Viewer** Registerkarte.

7. Änderung **Diagrammtyp** auf **Anzahl**. Diese Einstellungen werden ein Count-Diagramm gerendert.

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>Fügen Sie die benutzerdefinierte Einblicke mit dem datenbankdashboard

1. Um die Einblicke Widget-Konfiguration zu öffnen, klicken Sie auf **erstellen Insight** auf *Diagramm Viewer*:

   ![Konfiguration](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. Kopieren Sie die Insight-Konfiguration (die JSON-Daten). 

3. Drücken Sie **STRG + Komma** öffnen *Benutzereinstellungen*.

4. Typ *Dashboard* in *Sucheinstellungen*.

5. Klicken Sie auf **bearbeiten** für *dashboard.database.widgets*.

   ![Dashboardeinstellungen](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. Fügen Sie die Konfiguration Insight JSON in *dashboard.database.widgets*. Datenbank-Dashboard Einstellungen sieht wie folgt:

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql"
                }
            }
        }
    ]
   ```

7. Speichern Sie die *Benutzereinstellungen* Datei, und öffnen Sie die *TutorialDB* datenbankdashboard, um das Widget aktive Sitzungen finden Sie unter:

   ![Activesession Einblicke](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>Hinzufügen von Details zu benutzerdefinierten Einblicke

1. Um einen neuen Editor zu öffnen, drücken Sie die **STRG + N**.

2. Ändern den Verbindungskontext für **TutorialDB**.

3. Fügen Sie die folgende Abfrage in den Abfrage-Editor ein:

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. Speichern Sie die Abfrage-Editor eine \*.sql-Datei. Für dieses Lernprogramm speichern Sie das Skript *activeSessionDetail.sql*.

5. Drücken Sie **STRG + Komma** öffnen *Benutzereinstellungen*.

6. Bearbeiten Sie den vorhandenen *dashboard.database.widgets* Knoten in die Einstellungsdatei:

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql",
                    "details": {
                        "queryFile": "{your file folder}/activeSessionDetail.sql",
                        "label": "SID",
                        "value": "Login Name"
                    }
                }
            }
        }
    ]
   ```

7. Speichern Sie die *Benutzereinstellungen* Datei, und öffnen Sie die *TutorialDB* Datenbank-Dashboard. Klicken Sie auf die Schaltfläche mit den Auslassungszeichen (...) neben *eigene Widgets* um die Details anzuzeigen:

    ![Activesession Einblicke](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>Nächste Schritte
In diesem Lernprogramm haben Sie gelernt, wie:
> [!div class="checklist"]
> * Führen Sie eine eigene Abfrage und zeigen Sie ihn in einem Diagramm
> * Erstellen Sie eine benutzerdefinierte Einblicke Widget aus dem Diagramm
> * Hinzufügen des Diagramms zu einem Server oder Datenbank-dashboard
> * Hinzufügen von Details zu Ihrer benutzerdefinierten Insight-widget

Weitere Informationen zum Sichern und Wiederherstellen von Datenbanken, führen Sie den nächsten Lernprogrammen:

> [!div class="nextstepaction"]
> [Sichern und Wiederherstellen von Datenbanken](tutorial-backup-restore-sql-server.md).