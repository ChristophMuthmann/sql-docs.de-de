---
title: Integrierte Terminaldienste in SQL-Vorgänge Studio (Vorschau) | Microsoft Docs
description: Informationen Sie zu den integrierten Terminaldienste in SQL-Vorgänge Studio (Vorschau).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: e33468679c7c499c4f55d25cff2ac816c051e272
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="integrated-terminal"></a>Integrierte Terminaldienste

In [!INCLUDE[name-sos](../includes/name-sos-short.md)], öffnen Sie eine integrierte Terminaldienste anfänglich im Stammverzeichnis des Arbeitsbereichs ab. Dies kann praktisch sein, da Sie nicht zum Wechseln von Windows oder ändern den Status einer vorhandenen Terminaldienste zum Ausführen einer schnellen Befehlszeilen-Aufgabe.

So öffnen Sie den Terminalserver:

* Verwenden der **STRG +'** Tastenkombination mit der Akzentzeichen.
* Verwenden der **Ansicht** | **integrierte Terminaldienste** Menübefehl.
* Aus der **Befehl Palette** (**STRG + UMSCHALT + P**), verwenden Sie die **integrierte Terminaldienste anzeigen: zum ein-/ausschalten** Befehl.

![Terminaldienste](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> Weiterhin können Sie eine externe-Shell öffnen, mit dem Explorer **öffnen Sie im Eingabeaufforderungsfenster** Befehl (**öffnen Sie in der Terminal** auf Mac- oder Linux), wenn Sie lieber außerhalb arbeiten [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="managing-multiple-terminals"></a>Verwalten von mehreren Terminals

Mehrere Terminals zu öffnen, um verschiedene Speicherorte erstellen können und problemlos zwischen ihnen navigieren. Terminaldienste-Instanzen hinzugefügt werden können, durch Erreichen des Plussymbols auf der oberen rechten Ecke des der **TERMINALDIENSTE** Bereich oder durch Auslösen der **STRG + UMSCHALT +'** Befehl. Dies erstellt einen weiteren Eintrag in der Dropdownliste aus, die verwendet werden kann, um zwischen ihnen zu wechseln.

![Mehrere Terminals](media/integrated-terminal/terminal-multiple-instances.png)

Entfernen der Terminalserver-Instanzen durch Drücken der Papierkorb können auf die Schaltfläche.

> [!TIP]
> Wenn Sie mehrere Terminals sehr häufig verwenden, können Sie hinzufügen, schlüsselbindungen für den `focusNext`, `focusPrevious` und `kill` Befehle beschrieben, die in der [Schlüssel Bindungsabschnitt](#key-bindings) ermöglichen die Navigation zwischen ihnen die Verwendung der Tastatur.

## <a name="configuration"></a>Konfiguration

Die Shell verwendet standardmäßig `$SHELL` auf Linux- und MacOS, PowerShell unter Windows 10 und cmd.exe in früheren Versionen von Windows. Dies können durch Festlegen von manuell überschrieben werden `terminal.integrated.shell.*` in [Einstellungen](settings.md). Argumente für die Terminaldienste-Shell übergeben werden können, auf Linux- und MacOS mithilfe der `terminal.integrated.shellArgs.*` Einstellungen.

### <a name="windows"></a>Windows

Konfigurieren Ihre Shell ordnungsgemäß unter Windows wird durch die richtige ausführbare Datei zu suchen, und aktualisieren die Einstellung. Im folgenden finden Sie eine Liste der allgemeinen ausführbare Shelldateien und ihren Standardspeicherorten:

```json
// 64-bit cmd if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\cmd.exe"
// 64-bit PowerShell if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\WindowsPowerShell\\v1.0\\powershell.exe"
// Git Bash
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
// Bash on Ubuntu (on Windows)
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe"
```

> [!NOTE]
> Als eine integrierte Terminaldienste verwendet werden soll, muss die Shell ausführbare Datei eine Konsolenanwendung, damit `stdin/stdout/stderr` umgeleitet werden können.

> [!TIP]
> Die integrierte Shell Terminaldienste ausgeführt wird, mit den Berechtigungen des [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Wenn Sie eine Shell-Befehl mit erhöhten Berechtigungen (Administrator) oder unterschiedliche Berechtigungen ausführen müssen, können Sie Plattform Dienstprogramme wie z. B. `runas.exe` in einem abschließenden.

### <a name="shell-arguments"></a>Shell-Argumente

Sie können Argumente an die Shell übergeben, wenn er gestartet wird.

Beispielsweise, um ausgeführte Bash als Login-Shell aktivieren (dem ausgeführt wird `.bash_profile`), übergeben Sie die `-l` Argument (mit doppelten Anführungszeichen):

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>Der Terminalserver Anzeigeeinstellungen

Sie können die integrierten terminal Schriftart und die Zeilenhöhe mit den folgenden Einstellungen anpassen:

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>Der Terminalserver Tastenbindungen

Die **anzeigen: ein-/ausschalten integrierten Terminal** Befehl gebunden ist **STRG +'** schnell integrierten terminal Bereich ein-und aktivieren bzw. deaktivieren.

Im folgenden sind die Tastenkombinationen aufgeführt, in der integrierten Terminaldienste schnell zu navigieren:

Key|Befehl
---|---
**STRG + "**|Anzeigen von integrierten Terminaldienste
**STRG + UMSCHALT + "**|Erstellen Sie neue Terminaldienste
**STRG + nach-oben**|Einen Bildlauf nach oben
**STRG + nach-unten**|Führen Sie einen Bildlauf nach unten
**Strg + Bild**|Führen Sie einen Bildlauf Bild-auf
**Strg + Bild-ab**|Führen Sie einen Bildlauf Bild-ab
**STRG + POS1**|Führen Sie einen Bildlauf nach oben
**STRG + Ende**|Führen Sie einen Bildlauf nach unten
**STRG + K**|Deaktivieren Sie die Terminaldienste

Andere terminal Befehle sind verfügbar und können an Ihre bevorzugte Tastenkombinationen gebunden werden.

Die Überladungen sind:

* `workbench.action.terminal.focus`: Das Terminal zu konzentrieren. Dies ist z. B. zum ein-/ausschalten jedoch liegt der Schwerpunkt des Terminals statt ausgeblendet, wenn es sichtbar ist.
* `workbench.action.terminal.focusNext`: Konzentriert sich das nächste terminal Instanz.
* `workbench.action.terminal.focusPrevious`: Liegt der Schwerpunkt der vorherigen Terminaldienste-Instanz.
* `workbench.action.terminal.kill`: Entfernen Sie die aktuelle terminal Instanz.
* `workbench.action.terminal.runSelectedText`: Führen Sie den markierten Text in der terminal-Instanz.
* `workbench.action.terminal.runActiveFile`: Führen Sie die aktive Datei in der terminal-Instanz.

### <a name="run-selected-text"></a>Führen Sie den markierten Text

Verwenden der `runSelectedText` Befehl, wählen Sie Text in einem Editor, und führen Sie den Befehl **Terminaldienste: Textauswahl Active Terminalfenster ausführen** über die **Befehl Palette** (**STRG + UMSCHALT + P**). Der Terminalserver versucht, den ausgewählten Text auszuführen:

![Führen Sie markierten text](media/integrated-terminal/terminal_run_selected.png)

Wenn im aktiven Editor kein Text ausgewählt ist, wird die Zeile, die der Cursor auf in der abschließenden ausgeführt.

### <a name="copy--paste"></a>Kopieren und einfügen

Der schlüsselbindungen zum Kopieren und Einfügen führen Sie die Plattform-Standards:

* Linux: **STRG + UMSCHALT + C** und **STRG + UMSCHALT + V**
* Mac: **Cmd + C** und **Cmd + V**
* Windows: **STRG + C** und **STRG + V**

### <a name="find"></a>Suchen

Die integrierten Terminaldienste hat grundlegende Suchfunktionen, die mit ausgelöst werden kann **STRG + F**.

Wenn Sie möchten **STRG + F** um an die Shell statt starten das Widget "Suchen" auf Linux- und Windows zu wechseln, müssen Sie die Keybinding entfernen wie folgt:

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>Umbenennen der terminalsitzungen

Integrierte terminalsitzungen können nun umbenannt werden mithilfe der **Terminaldienste: Umbenennen** (`workbench.action.terminal.rename`) Befehl. Der neue Name wird in der terminal Auswahl-Dropdownliste angezeigt.

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>Das Erzwingen des schlüsselbindungen für die Weiterleitung über den Terminalserver

Während der Fokus in der integrierten Terminaldienste befindet, funktioniert nicht viele tastenbindungen, da die Tastatureingaben übergeben und von der Terminaldienste selbst genutzt werden. Die `terminal.integrated.commandsToSkipShell` Einstellung kann verwendet werden, um dieses Problem umgehen. Sie enthält ein Array von Befehlsnamen, überspringen Sie die Verarbeitung von der Shell und von verarbeitet werden, deren tastenbindungen, die [!INCLUDE[name-sos](../includes/name-sos-short.md)] Bindungssystem Schlüssel. Standardmäßig schließt dies alle terminal tastenbindungen zusätzlich zu einer Option einige häufig verwendete tastenbindungen.

