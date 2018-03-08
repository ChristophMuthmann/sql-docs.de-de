---
title: "Lernprogramm: Aktivieren des Tabelle Speicherplatz Nutzung Beispiel Einblicke Widgets in SQL-Vorgänge Studio (Vorschau) | Microsoft Docs"
description: "Dieses Lernprogramm veranschaulicht, wie die Tabelle Speicherplatz Nutzung Beispiel Einblicke Widget im Datenbank-Dashboard SQL-Vorgänge Studio (Vorschau) aktiviert."
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
ms.openlocfilehash: 7c51c7d1804baa490e665d316a08d911038c9f11
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>Lernprogramm: Aktivieren der Tabelle Speicherplatz Nutzung Beispiel Einblicke Widget mit[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Dieses Lernprogramm veranschaulicht, wie ein Widget Insight im Datenbank-Dashboard bietet eine Ansicht auf einen Blick, über die Speicherplatzverwendung für alle Tabellen in einer Datenbank aktiviert wird. Bei diesem Lernprogramm erfahren Sie, wie Sie:

> [!div class="checklist"]
> * Schalten Sie schnell eine Insight-Widget mithilfe einer integrierten Insight Widget-Beispiel
> * Zeigen Sie die Details der Verwendung des Tabellenbereichs
> * Filtern von Daten und Bezeichnung Detail auf ein Diagramm Insight anzeigen

## <a name="prerequisites"></a>Voraussetzungen

Dieses Lernprogramm erfordert die SQL Server- oder Azure SQL-Datenbank *TutorialDB*. Zum Erstellen der *TutorialDB* Datenbank, führen Sie eines der folgenden Schnellstarts:

- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des SQL Server ab[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Eine Verbindung herstellen Sie und Fragen Sie mithilfe des Azure SQL-Datenbank ab[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>Aktivieren Sie auf ein Management-Insight [!INCLUDE[name-sos](../includes/name-sos-short.md)]des Datenbank-Dashboard
[!INCLUDE[name-sos](../includes/name-sos-short.md)]verfügt über ein integriertes Beispiel Widget von Tabellen in einer Datenbank verwendeten Speicherplatz zu überwachen.

1. Öffnen Sie **Benutzereinstellungen** durch Drücken von **STRG + UMSCHALT + P** öffnen *Befehl Palette*, Typ *Einstellungen* im Suchfeld, und wählen Sie  **Voreinstellungen: Öffnen von Benutzereinstellungen**.

   ![Befehl des Benutzers öffnen-Einstellungen](./media/tutorial-table-space-sql-server/open-user-settings.png)

2. Typ *Dashboard* Eingabefeld in der Suche der Einstellungen, und suchen Sie **dashboard.database.widgets**.

   ![Sucheinstellungen](./media/tutorial-table-space-sql-server/search-settings.png)

3. Anpassen der **dashboard.database.widgets** festlegen, zeigen Sie auf das Stiftsymbol links neben der **dashboard.database.widgets** Text, klicken Sie auf **bearbeiten**  >  **Kopieren, um Einstellungen**.

4. Mit [!INCLUDE[name-sos](../includes/name-sos-short.md)]des Insight IntelliSense konfigurieren *Namen* für den Titel Widget *GridItemConfig* für die Größe der Widget und *Widget* dazu **Tabelle-Space-Db-Insight** aus der Dropdown-Liste wie im folgenden Screenshot gezeigt:

   ![Insight-Einstellungen](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. Drücken Sie **STRG + S** zum Speichern der Einstellungen.

6. Öffnen einer Datenbank-Dashboard durch Rechtsklicken auf **TutorialDB** , und klicken Sie auf **verwalten**.

   ![Open-dashboard](./media/tutorial-table-space-sql-server/insight-open-dashboard.png)

7. Ansicht *von Tabellen belegter Speicherplatz* wie im folgenden Screenshot gezeigt: 

   ![Widgets](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>Arbeiten mit der Insight-Diagramm

[!INCLUDE[name-sos](../includes/name-sos-short.md)]der Insight-Diagramm enthält, Filtern und MouseHover-Details. Zum Testen die folgenden Schritte aus:

1. Klicken Sie auf und Umschalten der *Row_count* Legende des Diagramms. [!INCLUDE[name-sos](../includes/name-sos-short.md)]Zeigt an, und blendet die Datenreihe aus, wie Sie eine Legende ein- und auszuschalten.
    
2. Zeigen Sie den Mauszeiger auf das Diagramm ein. [!INCLUDE[name-sos](../includes/name-sos-short.md)]Zeigt weitere Informationen über die reihenbezeichnung Daten und seinen Wert an, wie im folgenden Screenshot gezeigt.

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