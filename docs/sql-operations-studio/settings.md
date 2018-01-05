---
title: "SQL-Vorgänge Studio (Vorschau) Benutzer und Arbeitsbereichseinstellungen | Microsoft Docs"
description: "Vorgehensweise: Ändern von SQL-Vorgänge Studio (Vorschau) Benutzer und Arbeitsbereichseinstellungen."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2edea069c05e7ac0316042250f336f1a8c455af0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="user-and-workspace-settings"></a>Arbeitsbereichseinstellungen für Benutzerzustand und

Es ist einfach zu konfigurieren [!INCLUDE[name-sos](../includes/name-sos-short.md)] nach Belieben über die Einstellungen. Nahezu jeder Teil [!INCLUDE[name-sos](../includes/name-sos-short.md)]des Editor-Benutzeroberfläche und funktionalen Verhalten bietet Optionen können Sie ändern.

[!INCLUDE[name-sos](../includes/name-sos-short.md)]bietet zwei unterschiedliche Gültigkeitsbereiche für Einstellungen:

* **Benutzer** diese Einstellungen gelten global für alle Instanzen der [!INCLUDE[name-sos](../includes/name-sos-short.md)] Sie öffnen.
* **Arbeitsbereich** arbeitsbereichseinstellungen für die Einstellungen für einen Ordner auf Ihrem Computer spezifisch sind, und sind nur verfügbar, wenn der Ordner in der Randleiste Explorer geöffnet ist. In diesem Bereich definierte Einstellungen außer Kraft setzen den Benutzerbereich durchgeführt.

## <a name="creating-user-and-workspace-settings"></a>Erstellen von Benutzer- und Arbeitsbereichseinstellungen

Der Menübefehl **Datei** > **Voreinstellungen** > **Einstellungen** (**Code**  >  **Voreinstellungen** > **Einstellungen** auf Mac) bietet den Einstiegspunkt zum Konfigurieren der Einstellungen für Benutzer und den Arbeitsbereich. Sie werden eine Liste mit den Standardeinstellungen bereitgestellt. Kopieren Sie jede Einstellung, die Sie in das entsprechende ändern möchten `settings.json` Datei. Die Registerkarten auf der rechten Seite können Sie schnell zwischen Einstellungsdateien Benutzer- und Arbeitsbereich wechseln.

Sie können auch die Einstellungen für Benutzerzustand und Arbeitsbereich aus öffnen die **Befehl Palette** (**STRG + UMSCHALT + P**) mit **Voreinstellungen: Öffnen von Benutzereinstellungen** und  **Voreinstellungen: Öffnen von Arbeitsbereichseinstellungen** oder verwenden Sie die Tastenkombination (**STRG +**).

Das folgende Beispiel deaktiviert die Zeilennummern im Editor und konfiguriert Zeilen Text automatisch basierend auf der Größe des Editors zu umschließen.

![Beispieleinstellungen](media/settings/sample-settings.png)

Änderungen an den Einstellungen von Hostrichtlinien [!INCLUDE[name-sos](../includes/name-sos-short.md)] nach geänderten `settings.json` -Datei gespeichert ist.

>**Hinweis:** arbeitsbereichseinstellungen eignen sich für projektspezifische Einstellungen für ein Team freigegeben.

## <a name="settings-file-locations"></a>Dateispeicherorte für Einstellungen

Abhängig von Ihrer Plattform befindet sich die benutzereinstellungsdatei hier:

* **Windows**`%APPDATA%\sqlops\User\settings.json`
* **Mac**`$HOME/Library/Application Support/sqlops/User/settings.json`
* **Linux**`$HOME/.config/sqlops/User/settings.json`

Die Einstellungsdatei Arbeitsbereich befindet sich unter dem `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` Ordner des Projekts.


## <a name="additional-resources"></a>Weitere Ressourcen

Da [!INCLUDE[name-sos](../includes/name-sos-short.md)] erbt seine Benutzer- und im Arbeitsbereich Einstellungen, die Funktionen von Visual Studio-Code, ausführliche Informationen zu den Einstellungen in wird der [Einstellungen für Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings) Artikel.