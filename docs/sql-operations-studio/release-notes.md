---
title: Versionshinweise für Microsoft SQL Operations Studio (preview) | Microsoft Docs
description: Versionshinweise für Microsoft SQL Operations Studio (preview)
ms.custom: tools|sos
ms.date: 03/28/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba86403e791af25de4f7bcd8b1cbd7b5f188897b
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="sql-operations-studio-preview-release-notes"></a>Versionshinweise für SQL Operations Studio (preview)

**[Herunterladen der öffentlichen Vorschau von März](download.md)**

## <a name="march-2018-march-public-preview"></a>März 2018 (März öffentliche Vorschau)

Veröffentlichungsdatum: 28 März 2018  
version: 0.27.3

Die *März Public Preview* weiterhin die wichtigsten GitHub-Probleme zu beheben und konzentriert sich auf die Verbesserung unserer Story Erweiterbarkeit. Insbesondere Erweiterungs-Manager aktivieren, Verbessern der Dashboard-Management und Bereitstellen von SQL-Agent und Erweiterungen Einblicke. Diese Version umfasst die folgenden Verbesserungen:

- Erweitern Sie das Dashboard-Erweiterbarkeitsmodell zur Unterstützung von im Registerkartenformat Einblicke und Konfiguration Bereiche.
   - Erweiterungs-Manager ermöglicht die einfache Übernahme von Erweiterungen.
   - Dashboard-Erweiterungen für Sp_whoisactive aus [whoisactive.com](http://www.whoisactive.com).
   - Weitere Informationen finden Sie unter [Erweitern der Funktionalität von SQL Operations Studio](extensions.md).
- Hinzufügen zusätzlicher [-Erweiterbarkeits-APIs für die Verbindung und Objekt-Explorer](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API) Management.
- Weiterhin wichtige Auswirkungen auf Kunden beheben [GitHub Probleme](https://github.com/Microsoft/sqlopsstudio/issues).

Weitere Informationen finden Sie unter der [Änderungsprotokoll](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md).


## <a name="february-2018-february-public-preview"></a>Februar 2018 (Februar öffentliche Vorschau)

Veröffentlichungsdatum: 15-Version von Februar 2018  
version: 0.26.7

Die *Public Preview-Version von Februar* enthält einige neue Features vorschlagen und hoher Priorität Fehlerkorrekturen. Diese Version umfasst die folgenden Verbesserungen:

- Einführung in die Installation automatisch aktualisiert, bereitstellt, der eine Benachrichtigung bei eine neue Version zum Herunterladen verfügbar ist 
- Das Verbindungsdialogfeld "Database"-Feld ist jetzt eine dynamisch aufgefüllt Dropdown-Liste, die eine Liste der Datenbanken, die vom angegebenen Server aufgefüllt enthalten soll.
- Beheben Sie [ausstellen 6](https://github.com/Microsoft/sqlopsstudio/issues/6): Verbindung und die ausgewählte Datenbank beibehalten, beim Öffnen der neuen abfrageregisterkarten.
- Beheben Sie [ausstellen 22](https://github.com/Microsoft/sqlopsstudio/issues/22): "Servername" und "Datenbankname" – können Sie diese Dropdownfelder anstelle von Textfeldern werden?
- Beheben Sie [ausstellen 549](https://github.com/Microsoft/sqlopsstudio/issues/549): Silent/sehr automatische Installation führt zur Anwendung, die nach der Installation öffnet.
- Beheben Sie [ausstellen 481](https://github.com/Microsoft/sqlopsstudio/issues/481): Fügen Sie die Option "Nach Updates suchen".
- SQL-Editor farbliche Kennzeichnung und automatische Vervollständigung Problembehebungen:
   - Beheben Sie [ausstellen 584](https://github.com/Microsoft/sqlopsstudio/issues/584): Schlüsselwort "FULL", nicht hervorgehoben von IntelliSense.
   - Beheben Sie [ausstellen 345](https://github.com/Microsoft/sqlopsstudio/issues/345): zur farblichen Kennzeichnung der SQL-Funktionen innerhalb des Editors.
   - Beheben Sie [ausstellen 300](https://github.com/Microsoft/sqlopsstudio/issues/300): [#tempData] neuesten "]" wird grün angezeigt.
   - Beheben Sie [ausstellen 225](https://github.com/Microsoft/sqlopsstudio/issues/225): Schlüsselwort Farben stimmen nicht überein.
   - Beheben Sie [ausstellen 60](https://github.com/Microsoft/sqlopsstudio/issues/60): Ungültige Sql Farbe syntaxhervorhebung bei Verwendung der temporären Tabelle in from-Klausel.
- Führen Sie die Verbindung-Erweiterbarkeits-API.
- Visual Studio Code-Editor 1.19 Integration.
- Aktualisieren Sie JustinPealing/html-Abfrageplan Komponente übernommen Abfrageplan Viewer verbessert.


## <a name="january-2018-january-public-preview"></a>Januar 2018 (Januar öffentliche Vorschau)

Veröffentlichungsdatum: 17 Januar 2018  
version: 0.25.4

Die *Public Preview Januar* enthält einige neue Features vorschlagen und hoher Priorität Fehlerkorrekturen. Diese Version umfasst die folgenden Verbesserungen:

- Gespeicherten serververbindungen stehen im Verbindungsdialogfeld.
- Aktivieren Sie im laufenden Systembetrieb beenden. Im laufenden Systembetrieb beenden ist deaktiviert, so aktivieren Sie ausführliche Informationen finden Sie in der Standardeinstellung [Hot beenden Einstellung](settings.md#hot-exit).
- Registerkartenfärbung basierend auf der Gruppe "Server". Registerkartenfärbung ist deaktiviert, so aktivieren Sie ausführliche Informationen finden Sie in der Standardeinstellung [Registerkarte Farbe Einstellung](settings.md#tab-color).
- Änderung *Servernamen* auf *Server* im Verbindungsdialogfeld.
- Fehlerhafte Fix *aktuelle Abfrage ausführen* Befehl.
- Korrigieren Sie die Drag-and-Drop-wichtige scripting Fehler.
- Korrigieren Sie falsche angeheftete Startmenü-Symbol.
- Beheben Sie fehlende branding Symbol Azure-Konto.


## <a name="december-2017-december-public-preview"></a>Dezember 2017 (Dezember öffentliche Vorschau)

Veröffentlichungsdatum: 19 Dezember 2017  
version: 0.24.1

Die *öffentliche Vorschau Dezember* behebt mehrere Fehler für alle Funktionsbereiche sowie die folgenden Verbesserungen:

- Erstellen Sie Firewall-Regel Dialogfeld steht zum Herstellen einer Verbindung mit Azure SQL-Datenbank und Azure SQL Data Warehouse unterstützen.
- Hinzugefügte Windows Setup, und Linux-DEB und RPM-Installationspakete.
- Verwalten Sie Dashboard visuelle Layout-Editor.
- *Alter-Skript als* und *Ausführen von Skripts als* Befehle.
- *Führen Sie die aktuelle Abfrage mit Istplan* Befehl.
- Visual Studio Code 1.18.1-Editor-Plattform zu integrieren.
- Aktivieren Sie die Sideload-VSIX-Erweiterung Dateien.
- "N wechseln" Batch-Iterationssyntax zu unterstützen.


## <a name="november-2017"></a>November 2017

Veröffentlichungsdatum: 15 November 2017  
version: 0.23.6

- Erste Version des [!INCLUDE[name-sos](../includes/name-sos-short.md)].


## <a name="next-steps"></a>Nächste Schritte

Finden Sie in der folgenden Schnellstarts für den Einstieg:
- [Eine Verbindung herstellen und Abfragen von SQLServer](quickstart-sql-server.md)
- [Eine Verbindung herstellen und Abfragen von Azure SQL-Datenbank](quickstart-sql-database.md)
- [Eine Verbindung herstellen und Abfragen von Azure Datawarehouse](quickstart-sql-dw.md)

Tragen zu [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio)
