---
title: Verwenden Sie Einblicke Widgets zum Überwachen von Servern und Datenbanken in SQL-Vorgänge Studio (Vorschau) | Microsoft Docs
description: Erfahren Sie, einen Einblick in Gadgets in SQL-Vorgänge Studio (Vorschau).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article"
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 590fc4002e051eea1f7e9e0c9ef41e9ff342b3d3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>Verwalten von Servern und Datenbanken mit Einblicke in Gadgets in [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Insight Widgets dauern die Transact-SQL (T-SQL) Abfragen, die Sie zum Überwachen von Servern und Datenbanken verwenden, und wandelt sie in aufschlussreiche Visualisierungen. 

Einblicke sind anpassbare Diagramme und Grafiken, die Server- und Überwachung von Dashboards hinzugefügt. Zeigen Sie auf einen Blick Einblicke von Servern und Datenbanken, und klicken Sie dann Drillvorgang auf Weitere Details, und starten Sie Verwaltungsaktionen, die Sie definieren. 

Sie können awesome Server- und Management-Dashboards ähnlich wie im folgenden Beispiel erstellen:

![Datenbank-dashboard](media/insight-widgets/database-dashboard.png)


Springen aus, und starten die verschiedene Typen von Insight-Widgets erstellen, überprüfen Sie die folgenden Lernprogramme ausführen:

- [Erstellen Sie eine benutzerdefinierte Insight-widget](tutorial-build-custom-insight-sql-server.md)
- *Aktivieren der integrierten Insight widgets*
   - [Aktivieren der anwendungsleistungsüberwachung Einblicke](tutorial-qds-sql-server.md)
   - [Aktivieren Sie die Tabelle Speicherplatz Nutzung Einblicke](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>SQL-Abfragen 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] versucht, vermeiden Sie unnötigen noch eine andere Sprache oder Extreme Benutzer Schnittstelle, damit er versucht, T-SQL-so weit wie möglich mit Minimalkonfiguration JSON zu verwenden. Konfigurieren von Widgets Einblicke mit T-SQL nutzt die zahllose Anzahl der vorhandenen Datenquellen hilfreich, T-SQL-Abfragen, die in Widgets aufschlussreiche umgewandelt werden können.

Insight Widgets bestehen aus einem oder zwei T-SQL-Abfragen:
* *Insight Widget Abfrage* ist obligatorisch, und die Abfrage, die die angezeigten Daten im Widget "" zurückgegeben wird.
* *Insight Details Abfrage* ist nur erforderlich, wenn Sie eine Detailseite Insight erstellen.

Eine Abfrage der Insight-Widget definiert ein Dataset, das eine Anzahl, oder Diagramm gerendert wird. Insight Details Abfrage wird verwendet, um relevante Einblick von Detailinformationen in einem tabellarischen Format in der Insight-Bereich "Details" aufzulisten. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] Insight Widget Abfragen ausgeführt und ein Diagramm Dataset Resultset der Abfrage zugeordnet, und klicken Sie dann rendert ihn. Wenn Benutzer einen Einblick Details zu öffnen, führt die Abfrage der Insight-Details und druckt das Ergebnis in einer Rasteransicht innerhalb des Dialogfelds.

Die Grundidee ist, eine T-SQL-Abfrage auf eine Weise zu schreiben, damit es als ein Dataset mit einer Count, Diagramm- und Graph-Widget verwendet werden kann. 

## <a name="summary"></a>Zusammenfassung

Bestimmen das Verhalten bei Widget Einblicke, die T-SQL-Abfrage und Resultset. Das Schreiben einer Abfrage für ein Diagramm oder die Zuordnung eines richtigen Diagrammtyps für vorhandene Abfrage ist die wichtige Überlegung eine effektive Insight Widgets erstellen.



## <a name="additional-resources"></a>Weitere Ressourcen
- [Abfrage-Editor](tutorial-sql-editor.md)

