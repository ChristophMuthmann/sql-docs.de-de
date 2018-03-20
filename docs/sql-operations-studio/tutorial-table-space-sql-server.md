---
title: "Lernprogramm: Aktivieren des Tabelle Speicherplatz Nutzung Beispiel Einblicke Widgets in SQL-Vorgänge Studio (Vorschau) | Microsoft Docs"
description: "Dieses Lernprogramm veranschaulicht, wie die Tabelle Speicherplatz Nutzung Beispiel Einblicke Widget im Datenbank-Dashboard SQL-Vorgänge Studio (Vorschau) aktiviert."
ms.custom: tools|sos
ms.date: 03/19/2018
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
ms.openlocfilehash: 09a1ebe6fda1baf546923887f28b51d416a80b59
ms.sourcegitcommit: 6bd21109abedf64445bdb3478eea5aaa7553fa46
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2018
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>Lernprogramm: Aktivieren der Tabelle Speicherplatz Nutzung Beispiel Einblicke Widget mit [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Dieses Lernprogramm veranschaulicht, wie ein Widget Insight im Datenbank-Dashboard bietet eine Ansicht auf einen Blick, über die Speicherplatzverwendung für alle Tabellen in einer Datenbank aktiviert wird. Bei diesem Lernprogramm erfahren Sie, wie Sie:

> [!div class="checklist"]
> * Schalten Sie schnell eine Insight-Widget mithilfe einer integrierten Insight Widget-Beispiel
> * Zeigen Sie die Details der Verwendung des Tabellenbereichs
> * Filtern von Daten und Bezeichnung Detail auf ein Diagramm Insight anzeigen

## <a name="prerequisites"></a>Erforderliche Komponenten

Dieses Lernprogramm erfordert die SQL Server- oder Azure SQL-Datenbank *TutorialDB*. Zum Erstellen der *TutorialDB* Datenbank, führen Sie eines der folgenden Schnellstarts:

- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des SQL Server ab [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des Azure SQL-Datenbank ab [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>Aktivieren Sie auf ein Management-Insight [!INCLUDE[name-sos](../includes/name-sos-short.md)]des Datenbank-Dashboard
[!INCLUDE[name-sos](../includes/name-sos-short.md)] verfügt über ein integriertes Beispiel Widget von Tabellen in einer Datenbank verwendeten Speicherplatz zu überwachen.

1. Öffnen Sie *Benutzereinstellungen* durch Drücken von **STRG + UMSCHALT + P** So öffnen die *Befehl Palette*.
2. Typ *Einstellungen* in das Suchfeld, und wählen **Voreinstellungen: Öffnen von Benutzereinstellungen**.
2. Typ *Dashboard* Eingabefeld in der Suche der Einstellungen, und suchen Sie **dashboard.database.widgets**.

3. Anpassen der **dashboard.database.widgets** Einstellungen, die Sie bearbeiten möchten die **dashboard.database.widgets** Eintrag in der **BENUTZEREINSTELLUNGEN** Abschnitt (die Spalte in der Rechte Seite). Liegt keine **dashboard.database.widgets** in der **BENUTZEREINSTELLUNGEN** Abschnitt, zeigen Sie auf die **dashboard.database.widgets** Text in den Standardeinstellungen-Spalte und klicken Sie auf das Stiftsymbol, die auf der linken Seite den Text und klicken Sie auf **kopieren, um Einstellungen**. Wenn das Popupfenster daneben **ersetzen Sie in den Einstellungen**, nicht klicken Sie darauf! Wechseln Sie zu der **BENUTZEREINSTELLUNGEN** Spalte rechts, und suchen Sie die **dashboard.database.widgets** Abschnitt und den vorbestellungsdaten mit dem nächsten Schritt fort.

4. In der **dashboard.database.widgets** Abschnitt, fügen Sie Folgendes hinzu:

   ```json
        {
            "name": "Space Used by Tables",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "table-space-db-insight": null
            }
        },
    ```
Die **dashboard.database.widgets** Abschnitt sollte wie in der folgenden Abbildung aussehen:

   ![Sucheinstellungen](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. Drücken Sie **STRG + S** zum Speichern der Einstellungen.

6. Öffnen einer Datenbank-Dashboard durch Rechtsklicken auf **TutorialDB** , und klicken Sie auf **verwalten**.

7. Anzeigen der *Tabelle Speicherplatz* Insight-Widget wie in der folgenden Abbildung gezeigt: 

   ![Widget](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>Arbeiten mit der Insight-Diagramm

[!INCLUDE[name-sos](../includes/name-sos-short.md)]der Insight-Diagramm enthält, Filtern und MouseHover-Details. Zum Testen die folgenden Schritte aus:

1. Klicken Sie auf und Umschalten der *Row_count* Legende des Diagramms. [!INCLUDE[name-sos](../includes/name-sos-short.md)] Zeigt an, und blendet die Datenreihe aus, wie Sie eine Legende ein- und auszuschalten.
    
2. Zeigen Sie den Mauszeiger auf das Diagramm ein. [!INCLUDE[name-sos](../includes/name-sos-short.md)] Zeigt weitere Informationen über die reihenbezeichnung Daten und seinen Wert an, wie im folgenden Screenshot gezeigt.

   ![Diagramm zum ein-/ausschalten und Legende](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>Nächste Schritte
In diesem Lernprogramm haben Sie gelernt, wie:
> [!div class="checklist"]
> * Schalten Sie schnell eine Insight-Widget mithilfe einer Stichprobe von integrierten Insight Widget aus.
> * Zeigen Sie die Details der Speicherplatzverwendung für die Tabelle ein.
> * Filtern von Daten und Bezeichnung Detail auf ein Diagramm Insight anzeigen

Um zu erfahren, wie eine benutzerdefinierte Einblicke Widget "erstellen", den nächsten Lernprogrammen abzuschließen:

> [!div class="nextstepaction"]
> [Erstellen Sie eine benutzerdefinierte Einblicke Widget](tutorial-build-custom-insight-sql-server.md).