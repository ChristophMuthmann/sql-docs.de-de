---
title: Schneller Zugriff auf Einblicke und häufige Aufgaben bei der SQL-Vorgänge Studio (Vorschau) | Microsoft Docs
description: Weitere Informationen Sie zum Anzeigen von aufschlussreiche Widgets in SQL-Vorgänge Studio (Vorschau).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad7fcbab5a01828cccd855da2d65ba3199e0b41b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>Dashboards in [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Ein Dashboard, mit der rechten Maustaste einen Server oder Datenbank anzeigen und auswählen **verwalten**.

![Beispiel-Dashboard](media/dashboards/sample-dashboard.png)

**Servereigenschaften** enthält die Eigenschaften des Servers, einschließlich der Version, Edition, Computernamen und Betriebssystemversion.

**Aufgaben** Commons Aufgaben wie das Wiederherstellen und neue Abfrage enthält.

**Suchen Sie die Datenbanken** Nachschlagen vorhandener Datenbanken auf dem Server, einschließlich Tabellen gespeichert.

**Sicherungsstatus** einfache Suche nach den Sicherungsstatus für vorhandene Datenbanken.

## <a name="configuring-insight-widgets"></a>Konfigurieren von Insight Widgets
Es wird dringend empfohlen, dass Sie arbeiten Sie das Lernprogramm zum Einrichten von Ihrem Dashboards, das sich [hier](tutorial-build-custom-insight-sql-server.md).

Stellen Sie außerdem sicher, dass sehen Sie sich die [Vorgehensweisen zum Konfigurieren von Insight Widgets]().

Nach dem Lesen dieses Lernprogramms folgende auf erfahren Sie mehr über bestimmte Widgets, die in diesem Lernprogramm nicht behandelt werden.

## <a name="insight-detail"></a>Insight-Detail
Die Einblicke Details Flyout bietet detailliertere Informationen zu verwandten Insight Widgets. 
- Ein Widget Insight rendert eine auf einen Blick Zusammenfassungsansicht mit Count, Linie, Diagramm usw. an. 
- Der Einblick Details Flyout bietet es sich um "einen Drilldown in" Details, auflisten pullanforderungs-von Daten für jedes Element im Allgemeinen Widget "Einblicke" aufgeführt. 
  - Die Details Flyout-Inhalte sind durch eine separate SQL-Abfrage an die Haupt-Widget-Abfrage definiert. 

Besteht keine Notwendigkeit Menge für eine Abfrage der Insight-Details, aber das Layout ist standard.
- Die obere Hälfte der Sicht wird immer eine Spalte 2 "Zusammenfassung". Die zu verwendenden Spalten werden durch die "Label" und "Wert" Eigenschaften der JSON-Konfiguration definiert.
- Durch Klicken auf eine Zeile in der Zusammenfassungstabelle, auf der unteren Hälfte der Flyout Listet den vollständigen Satz von Informationen für diese Zeile in der Spalte.

### <a name="insight-detail-configuration-in-packagejson"></a>Insight-Detail-Konfiguration in "Package.JSON"

Beispielkonfiguration für Einblicke Details flyout
```json
"details": {
    "queryFile": "./relative_path_to_sqlfile_from_package_json_file.sql",
    "label": {
        "icon": "database",
        "column": "first_column_name_for_summary_list_view",
        "state": [
            {
                "condition": {
                    "if": "equals",
                    "equals": "0"
                },
                "color": "red"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "1"
                },
                "color": "orange"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "2"
                },
                "color": "green"
            }
        ]
    },
    "value": "second_column_and_condition_check_value_column_for_summary_list_view",
```
|property|Typ|Wert|Standardwert|description|comment|
|:---|:---|:---|:---|:---|:---|
|Details|JSON-Objekt|||obligatorische Eigenschaft Insight-Detail-Definitionen in ihrer Struktur definieren.||
|queryFile|Zeichenfolge|||der Dateipfad der Insight Detail-Sql-Abfrage und den Dateinamen relativ zum Speicherort von "Package.JSON"||
|Bezeichnung|JSON-Objekt|||erforderliche Eigenschaft, jedes Zeilenelement in der Liste "Zusammenfassung" Ansicht definieren|in Zukunft den Namen dieser Eigenschaft so ändern Sie z. B. "SummaryList"|
|Symbol "|Zeichenfolge|||Geben Sie an der Symbolname zu geeignet für jedes Element der Liste "Zusammenfassung" anzeigen.|(tbd) Liste der unterstützten Symbole werden dokumentiert|
|column|Zeichenfolge|||Geben Sie den Namen der ersten Spalte in der Liste "Zusammenfassung" Ansicht aus dem Resultset der Abfrage|der Name dieser Eigenschaft wird in Zukunft intuitiver Namen geändert werden|
|Wert|Zeichenfolge|||Geben Sie den Namen der zweiten Spalte in der Liste "Zusammenfassung" Ansicht aus dem Resultset der Abfrage an. Der Wert dieser Spalte wird verwendet, um Bedingungen zu überprüfen und Festlegen der Farbe für jede Liste "Zusammenfassung" Ansichtselemente Farbe Punkt|der Name dieser Eigenschaft wird in Zukunft eine intuitivere ändern.|
|Bedingung|JSON-Objekt|||definiert die Bedingung der Suche nach Wert der Spalte, und bestimmen Sie die Farbe für jedes Element der Liste "Zusammenfassung" anzeigen||
|wenn|Zeichenfolge|immer gleich, ungleich, "GreaterThan", "LessThan", GreaterThanOrEqauls, kleiner als oder gleich||Bedingung Prüfvorgang|Der Eigenschaftsname wird in Zukunft in Operator geändert.|
|Ist gleich|Zeichenfolge|||Überprüfen der Bedingungswert|diesem Eigenschaftennamen wird in Zukunft in "Value" geändert.|

## <a name="insight-actions"></a>Insight-Aktionen
Mit einem Widget Einblicke und Einblicke Details können Sie problemlos stammen Einrichten einer Aktionsplan ein Problem zu verringern oder zu verwalten. Sie werden z. B. Ausführen von DBCC CHECKDB vorstellen, lesen die Fehlerprotokolle oder stellen Sie die Datenbank wieder her, wenn eine Datenbank in ein Wiederherstellung ausstehend ist. Oder es kann eine der Aktionen, die Sie ausführen möchten.

Mithilfe von [!INCLUDE[name-sos](../includes/name-sos-short.md)]des Insight Aktionen Konfiguration können Sie eine integrierte Aktionen wie wiederherstellen, oder bringen Ihre eigenen-Aktion mit einem SQL­Skript definiert zuordnen.

> Konfiguration von benutzerdefinierten Aktionen, die mit Sql-Skript in der Entwicklungsphase ist, und es ist noch nicht im Build private Vorschau verfügbar.

## <a name="sample-insight-action-definition"></a>Beispiel Einblicke Aktionsdefinition

```"actions"{}``` definiert eine Insight-Aktion an. Aktion kann z. B. über einen bestimmten Gültigkeitsbereich definiert werden ```"server"```, ```"database"``` usw. und [!INCLUDE[name-sos](../includes/name-sos-short.md)] übergibt den aktuellen Kontext Verbindungsinformationen an die Aktion. 

Z. B. beim Wiederherstellungsvorgang für Datenbank "wideworldimporters", gestartet wird ```"database": "${Database}"``` Definition gibt an, dass übergeben ```Database``` Spaltenwert in die Abfrageergebnisse, um die Wiederherstellungsaktion. Stellen Sie dann Aktion gestartet wird, für die Datenbank wieder her. ```"types"``` ist ein Json-Array und im Array können mehrere Aktionen aufgeführt werden. Es wird im Grunde ein Kontextmenü dieses Benutzers kann Insight Details im Dialogfeld "auf und führen Sie die Aktion. 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] Vorschau 0.17.1 hat "Sicherung", "Wiederherstellen", "neue Abfrage" und "neue-Datenbank" als Aktionstypen aktiviert.

```json
"details": {
    "queryFile": "./sql/database_state_detail.sql",
    "label": {...},
    "value": "state",
    "actions": {
        "database": "${Database}",
        "types": ["restore"]
    }
}
```
