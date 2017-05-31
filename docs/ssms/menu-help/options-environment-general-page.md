---
title: "Optionen (Umgebung – Seite „Allgemein“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.TOOLSOPTIONSPAGES.ENVIRONMENT.GENERAL
- VS.ToolsOptionsPages.Environment.SQLEnvironmentOptions
- DevLang-TSQL
ms.assetid: c32ccdb8-2cf8-4c78-b474-a3abd3dbbd13
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 18ee84388c584423bc7f5b416d1540d1a287a0ba
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="options-environment---general-page"></a>Optionen (Umgebung – Seite „Allgemein“)
Im Dialogfeld **Optionen** können Sie die Startaktionen, Optionen für die Fensterverwaltung und andere allgemeine Optionen für [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] konfigurieren. Klicken Sie im Menü **Extras** auf **Optionen**, erweitern Sie den Ordner **Umgebung** , und klicken Sie anschließend auf **Allgemein**.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
**Beim Start**  
Wählen Sie die Aktion aus, die beim Start von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ausgeführt werden soll. Folgende Optionen sind verfügbar:  
  
-   Mit**Objekt-Explorer öffnen** werden Sie aufgefordert, eine Verbindung anzugeben, und der Objekt-Explorer wird aufgerufen.  
  
-   Mit**Neues Abfragefenster öffnen** werden Sie aufgefordert, eine Verbindung anzugeben, und der SQL-Abfrage-Editor wird aufgerufen.  
  
-   Mit**Objekt-Explorer und neue Abfrage öffnen** werden Sie aufgefordert, eine Verbindung anzugeben, und anschließend werden mit dieser Verbindung sowohl der Objekt-Explorer als auch der SQL-Abfrage-Editor geöffnet.  
  
-   Mit**Leere Umgebung öffnen** wird [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] aufgerufen, ohne dass das Fenster des SQL-Abfrage-Editors geöffnet oder eine Objekt-Explorer-Verbindung zu einem Server hergestellt wird.  
  
**Systemobjekte im Objekt-Explorer ausblenden**  
Aktivieren Sie dieses Kontrollkästchen, um Systemdatenbanken, Systemtabellen, Systemsichten und gespeicherte Systemprozeduren aus der Struktursicht des Objekt-Explorers zu entfernen. Systemfunktionen und Systemdatentypen werden nicht ausgeblendet. Diese Option betrifft nur Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , d. h., sie wirkt sich nicht auf Server aus, die im Objekt-Explorer bereits verbunden wurden.  
  
## <a name="environment-layout"></a>Umgebungslayout  
Um zwischen den Umgebungsmodi MDI-Schnittstelle (Multiple Document Interface) und Dokumente im Registerformat wechseln zu können, müssen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] schließen und wieder öffnen.  
  
**Dokumente im Registerformat**  
Wählen Sie diese Option aus, um Dokumentfenster anzuzeigen, die in Editoren als Registerkarten zusammengefasst sind. Dokumentfenster im Registerformat werden verwendet, um mehrere offene Dokumente zu organisieren und problemlos zwischen den Dokumenten wechseln zu können.  
  
**MDI-Umgebung**  
Wählen Sie diese Option aus, um Dokumente in einer MDI-Umgebung zu öffnen. MDI-Dokumentfenster werden verwendet, um auf dem Bildschirm wieder Platz zu gewinnen, der andernfalls durch die Registerkarten der Dokumente im Registerformat belegt ist. Wenn Sie im MDI-Modus arbeiten und zwischen Dokumenten wechseln müssen, verwenden Sie die Tastenkombination STRG+TAB oder die im Menü **Fenster** verfügbaren Optionen zum Anordnen von Fenstern.  
  
## <a name="docked-tool-window-behavior"></a>Verhalten angedockter Toolfenster  
**Die Schaltfläche 'Schließen' betrifft nur die aktive Registerkarte**  
Wenn dieses Kontrollkästchen aktiviert wird, werden nicht alle Toolfenster im angedockten Satz, sondern nur das aktuell fokussierte Toolfenster geschlossen. Standardmäßig ist dieses Kontrollkästchen aktiviert.  
  
**Die Schaltfläche zum automatischen Ausblenden betrifft nur die aktive Registerkarte**  
Wenn dieses Kontrollkästchen aktiviert wird, werden nicht alle Toolfenster im angedockten Satz, sondern nur das aktuell fokussierte Toolfenster ausgeblendet. Standardmäßig ist dieses Kontrollkästchen deaktiviert.  
  
## <a name="display"></a>Anzeige  
**Dateien in der Liste zuletzt verwendeter Dateien**  
Passt die Anzahl zuletzt bearbeiteter Projekte und Dateien an, die im Menü **Datei** angezeigt werden. Geben Sie eine Zahl zwischen 1 und 24 ein. Der Standardwert ist "4". Diese Option erleichtert das Abrufen kürzlich verwendeter Skriptprojekte und -dateien.  
  

