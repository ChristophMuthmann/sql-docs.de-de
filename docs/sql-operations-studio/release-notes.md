---
title: Versionshinweise für Microsoft SQL Operations Studio (Vorschau) | Microsoft Docs
description: Versionshinweise für Microsoft SQL Operations Studio (Vorschau)
ms.custom: tools|sos
ms.date: 04/25/2018
ms.prod: sql
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
ms.openlocfilehash: 233572c87f785e10a0cde4ac78a7c8ee75c5a801
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sql-operations-studio-preview-release-notes"></a>Versionshinweise für SQL-Vorgänge Studio (Vorschau)

**[April Public Preview herunterladen](download.md)**


## <a name="april-2018-april-public-preview"></a>April 2018 (April öffentliche Vorschau)

Veröffentlichungsdatum: 25 April 2018  
Version: 0.28.6

Die *April Public Preview* enthält Fehlerbehebungen und Verbesserungen. 

- Verbesserungen an der Erweiterung SQL Agent-Vorschau.
- Verbesserte dateiunterstützung für große und geschützte zum Speichern von Admin geschützt und > 256 MB-Dateien in Studio für SQL-Vorgänge.
- Integrierte Terminaldienste aufteilen, um gleichzeitig mit mehreren open Terminals arbeiten.
- Reduzierte Installation Datei auf dem Datenträger Anzahl Foot für schnellere Installationen und Startzeiten drucken.
- Den Vorgang fortzusetzen Sie, GitHub-Probleme zu beheben:
   - Beheben Sie [ausstellen 37](https://github.com/Microsoft/sqlopsstudio/issues/37): unerwartetes Verhalten tritt auf, wenn Benutzer einen Fehler auslöst,.
   - Beheben Sie [ausstellen 462](https://github.com/Microsoft/sqlopsstudio/issues/462): anfordern Funktion: Option für Servergruppen standardmäßig erweitert wird.
   - Beheben Sie [ausstellen 606](https://github.com/Microsoft/sqlopsstudio/issues/606): Intellisense - ungültige Vorschlag für den Befehl 'update'.
   - Beheben Sie [ausstellen 967](https://github.com/Microsoft/sqlopsstudio/issues/967): erwarten Abfrageplan Wenn XML-Showplan im Ergebnisraster auswählen.
   - Beheben Sie [ausstellen 1023](https://github.com/Microsoft/sqlopsstudio/issues/1023): eckige Klammern für Ms_foreachdb Aufruf aus Flyfishingdba hinzufügen.
   - Beheben Sie [ausstellen 1048](https://github.com/Microsoft/sqlopsstudio/issues/1048): vor der Anmeldung SSL/TLS-Handshake-Fehler.
   - Beheben Sie [1050 ausstellen](https://github.com/Microsoft/sqlopsstudio/issues/1050): Clear Einblicke anzuzeigen, vor dem Fehler anzeigen.
   - Beheben Sie [ausstellen 1057](https://github.com/Microsoft/sqlopsstudio/issues/1057): Wiederherstellen und neue Abfrageaktionen im Explorer-Widget werden unterbrochen.
   - Beheben Sie [ausstellen 1068](https://github.com/Microsoft/sqlopsstudio/issues/1068): Dashboard Ausgabe Windows Pop--Up mit Fehlermeldung für Azure SQL-Datenbank.
   - Beheben Sie [ausstellen 1069](https://github.com/Microsoft/sqlopsstudio/issues/1069): Verbindungsdialogfeld zeigt Server erforderlich, Fehler beim ersten anzeigen.
   - Beheben Sie [ausstellen 1070](https://github.com/Microsoft/sqlopsstudio/issues/1070): Server-Gruppen erfordern jetzt ein Doppelklick zu erweitern.
   - Beheben Sie [ausstellen 1072](https://github.com/Microsoft/sqlopsstudio/issues/1072): Auswahlsteuerelement Hintergrund ist halb transparent.
   - Beheben Sie [ausstellen 1115](https://github.com/Microsoft/sqlopsstudio/issues/1115): Beheben Sie alle hoher Kontrast Probleme mit dem Zugriff auf SQL-Vorgänge Studio.
   - Beheben Sie [ausstellen 1101](https://github.com/Microsoft/sqlopsstudio/issues/1101): Erweiterung kann keine Aktualisierung "herunterladen Manually" Link beginnt am falschen Ort.
   - Beheben Sie [ausstellen 1103](https://github.com/Microsoft/sqlopsstudio/issues/1103): V Scroll funktioniert nicht auf Registerkarte "Home".
   - Beheben Sie [ausstellen 1104](https://github.com/Microsoft/sqlopsstudio/issues/1104): SQL-Erweiterung Registerkarten hat die Arbeit.


Eine erhebliche Hervorhebung der öffentlichen Vorschau von April ist der Visual Studio Code 1.21 Plattform Source Code aktualisieren. Daraufhin wird in mehrere Updates für die Core-Editor und den workbenchcomputer aus der vorherigen 1.19 Synchronisierungspunkt. Die folgenden: Beispiele

- [Benutzeroberfläche für neue Benachrichtigungen](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) - leichter zu verwalten und überprüfen Sie die SQL-Vorgänge Studio-Benachrichtigungen.
- [Integrierte Terminal teilen](https://code.visualstudio.com/updates/v1_21#_split-terminals) -arbeiten mit mehreren open Terminals gleichzeitig.
- [Speichern von großen und geschützte Dateien](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges) – speichert Admin geschützt und > 256 MB-Dateien in Studio für SQL-Vorgänge.
- [Verbesserte Unterstützung für große Datei](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements) -Text-Puffer Optimierungen bei großen Dateien.
- [Verbesserte Einstellungen Suchvorgänge](https://code.visualstudio.com/updates/v1_20#_settings-search) - leichter finden Sie die richtige Einstellung mit der Suche in natürlicher Sprache.
- [Globale Ausschnitte](https://code.visualstudio.com/updates/v1_20#_global-snippets) -Codeausschnitten Sie über alle Dateitypen können zu erstellen.
- [Explorer-Mehrfachauswahl](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer) -Aktionen für mehrere Dateien gleichzeitig ausführen.
- [Fehler und Warnungen im Explorer](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer) – schnell zu Fehlern in Ihrer Codebasis navigieren.
- [Ziehen Sie drop kopieren &, fügen Sie über Windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support) -Dateien über SQL Operations Studio-Fenstern zu verschieben.
- [Unterstützung für Git Untermodul](https://code.visualstudio.com/updates/v1_20#_git-submodules) -Git führen Vorgänge für geschachtelte Git-Repositorys.
- [Terminalfenster Reader Unterstützung](https://code.visualstudio.com/updates/v1_20#_screen-reader-support) -integrierten Terminaldienste weist jetzt "Bildschirm Reader optimiert" Modus.
- [Zentriert Editor Layout](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout) -Codes anzeigen Bildschirmfläche zu maximieren.
- [Horizontale Suchergebnisse (Vorschau)](https://code.visualstudio.com/updates/v1_21#_horizontal-search) – Sie können jetzt Anzeigen der Suchergebnisse in einem horizontalen Bereich.

Weitere Informationen Checkout der [Visual Studio Code-Version von Februar Release Notes](https://code.visualstudio.com/updates/v1_21), und die [Visual Studio Code Januar Versionshinweise](https://code.visualstudio.com/updates/v1_20).

Weitere Informationen finden Sie unter der [Änderungsprotokoll](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md).

## <a name="march-2018-march-public-preview"></a>März 2018 (März öffentliche Vorschau)

Veröffentlichungsdatum: 28 März 2018  
Version: 0.27.3

Die *März Public Preview* weiterhin die wichtigsten GitHub-Probleme zu beheben und konzentriert sich auf die Verbesserung unserer Story Erweiterbarkeit. Insbesondere Erweiterungs-Manager aktivieren, Verbessern der Dashboard-Management und Bereitstellen von SQL-Agent und Erweiterungen Einblicke. Diese Version umfasst die folgenden Verbesserungen:

- Erweitern Sie das Dashboard-Erweiterbarkeitsmodell zur Unterstützung von im Registerkartenformat Einblicke und Konfiguration Bereiche.
   - Erweiterungs-Manager ermöglicht die einfache Übernahme von Erweiterungen.
   - Dashboard-Erweiterungen für Sp_whoisactive aus [whoisactive.com](http://www.whoisactive.com).
   - Weitere Informationen finden Sie unter [Erweitern der Funktionalität von SQL-Vorgänge Studio](extensions.md).
- Hinzufügen zusätzlicher [-Erweiterbarkeits-APIs für die Verbindung und Objekt-Explorer](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API) Management.
- Weiterhin wichtige Auswirkungen auf Kunden beheben [GitHub Probleme](https://github.com/Microsoft/sqlopsstudio/issues).


## <a name="february-2018-february-public-preview"></a>Februar 2018 (Februar öffentliche Vorschau)

Veröffentlichungsdatum: 15-Version von Februar 2018  
Version: 0.26.7

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
Version: 0.25.4

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
Version: 0.24.1

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
Version: 0.23.6

- Erste Version des [!INCLUDE[name-sos](../includes/name-sos-short.md)].


## <a name="next-steps"></a>Nächste Schritte

Finden Sie in der folgenden Schnellstarts für den Einstieg:
- [Eine Verbindung herstellen und Abfragen von SQLServer](quickstart-sql-server.md)
- [Eine Verbindung herstellen und Abfragen von Azure SQL-Datenbank](quickstart-sql-database.md)
- [Eine Verbindung herstellen und Abfragen von Azure Datawarehouse](quickstart-sql-dw.md)

Tragen zu [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio)
