---
title: Abfrage- und Text-Editoren (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: VS.TextEditor
helpviewer_keywords:
- Query Editor [SQL Server Management Studio]
- Code Editor [SQL Server Management Studio], about Query Editor
- Query Editor [SQL Server Management Studio], full screen mode
- Query Editor [Database Engine], templates
- full screen mode [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], templates
- writing scripts
- modifying scripts
- SQL Server Management Studio [SQL Server], query editor
- Query Editor [SQL Server Management Studio], about Query Editor
- writing queries
- SQL Server Management Studio [SQL Server], editor
- scripts [SQL Server], SQL Server Management Studio
- queries [SQL Server], SQL Server Management Studio
ms.assetid: 062051e4-4b77-4969-98ae-d2547c24ce3e
caps.latest.revision: "53"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a59b16fa58991062b137ce94fe5fcab82571a600
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="query-and-text-editors-sql-server-management-studio"></a>Abfrage- und Text-Editoren (SQL Server Management Studio)
  Mit den Editoren in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] lassen sich [!INCLUDE[tsql](../../includes/tsql-md.md)]-, MDX-, DMX- oder XML/A-Skripts interaktiv bearbeiten und testen sowie XML- oder einfache Textdateien bearbeiten. Die einzelnen Editoren werden durch einen sprachspezifischen Dienst unterstützt, der Schlüsselwörter farblich kennzeichnet und den Code auf Syntaxfehler überprüft. Der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor enthält einen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger, mit dem Sie Probleme in [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code beheben können.  
  
## <a name="sql-server-management-studio-editors"></a>Editoren in SQL Server Management Studio  
 Die vier Editoren in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] weisen die gleiche Architektur auf. Der Text-Editor implementiert die Basisfunktionalitätsstufe und kann als grundlegender Editor für Textdateien verwendet werden. Die anderen drei Editoren oder Abfrage-Editoren bieten erweiterte Funktionalität, indem sie einen Sprachdienst einschließen, der die Syntax von einer der in SQL Server unterstützten Sprachen definiert. Die Abfrage-Editoren implementieren darüber hinaus verschiedene Ebenen der Unterstützung für Editor-Funktionen, z. B. IntelliSense und Debugging. Die Abfrage-Editoren beinhalten den Abfrage-Editor des Datenbankmoduls zur Verwendung bei der Erstellung von Skripts mit Transact-SQL- und XQuery-Anweisungen, den MDX-Editor für die MDX-Sprache, den DMX-Editor für die DMX-Sprache sowie den XML/A-Editor für die XML for Analysis-Sprache.  
  
## <a name="common-components"></a>Allgemeine Komponenten  
 Alle Editoren in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] enthalten diese Komponenten:  
  
 **Codebereich**  
 Der Bereich, in den Sie die Abfragen oder den Text eingeben. In den Abfrage-Editoren enthält er die Funktionen für den Anweisungs-Generator, die für Ihre Sprache zur Verfügung stehen. Die Textbearbeitungsumgebung unterstützt Funktionen wie Suchen und Ersetzen, Massenkommentare und benutzerdefinierte Schriftarten und Farben.  
  
 Sie können Optionen festlegen, die das Verhalten des Texts im Codebereich beeinflussen in Bezug auf den Einzug, das Registerformat, Ziehen und Ablegen von Text usw. Abfragefenster können so konfiguriert werden, dass sie als Registerkarten im Dokumentfenster oder in separaten Dokumenten verfügbar sind.  
  
 **Auswahlrahmen**  
 Eine Spalte mit Leerzeichen zwischen der Randindikatorleiste und dem Codetext, auf die Sie zur Auswahl von Textzeilen klicken können. Sie können den Auswahlrand ausblenden oder anzeigen.  
  
 **Horizontale und vertikale Bildlaufleisten**  
 Ermöglichen Ihnen das Durchführen eines Bildlaufes durch den Codebereich in horizontaler und vertikaler Richtung, sodass Sie Code anzeigen können, der außerhalb des angezeigten Codebereichs liegt.  
  
 **Zeilennummerierung**  
 Zeigt im Editor links vom Text oder Code Zeilennummern an. Sie können zu bestimmten Zeilennummern navigieren.  
  
 **Zeilenumbruch**  
 Zeigt lange Text- oder Codezeilen über mehrere Zeilen verteilt an. Dadurch wird der gesamte Text einer Zeile angezeigt. Der Zeilenumbruch hat keinen Einfluss auf die Darstellung des Texts, wenn er ausgeführt oder gedruckt wird. Der Zeilenumbruch wird unter **Extras**über das Dialogfeld **Optionen** auf der Seite „Text-Editor“ &gt; „Alle Sprachen“ &gt; „Allgemein“ oder auf einer bestimmten Seite des Editors aktiviert.  
  
## <a name="code-editor-components"></a>Komponenten des Code-Editors  
 Die Code-Editoren enthalten zusätzlich zu den Funktionen, die sie mit dem Text- und XML-Editor gemeinsam haben, folgende Funktionen:  
  
 **Ergebnisse**  
 In diesem Fenster können Sie die Ergebnisse einer Abfrage anzeigen. Im Fenster können die Ergebnisse in Rastern oder Text angezeigt werden. Alternativ können die Ereignisse an eine Datei weitergeleitet werden. Ergebnisraster können in Form von einzelnen Fenstern im Registerformat angezeigt werden.  
  
 **IntelliSense**  
 Zeigen Sie im Editor im Menü **Bearbeiten** auf **IntelliSense**, um die [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense-Optionen anzuzeigen.  
  
 **Farbcodierung**  
 Zeigt verschiedene Farben für die einzelnen Syntaxelementtypen an, wodurch die Lesbarkeit von komplexen Anweisungen verbessert wird.  
  
 **Codegliederung**  
 Zeigt Codegruppen mit Gliederungslinien links vom Code an. Zur einfacheren Überprüfung des Codes lassen sich Codegruppen reduzieren und erweitern.  
  
 **Vorlage**  
 Vorlagen sind Dateien, die die grundlegende Struktur der Anweisungen enthalten. Diese Struktur wird beim Erstellen von Objekten in einer Datenbank benötigt. Sie können zum Beschleunigen der Skripterstellung verwendet werden.  
  
 **Meldungen**  
 Zeigt Fehler, Warnungen und Informationsmeldungen an, die beim Ausführen eines Skripts vom Server zurückgegeben werden. Die Liste von Meldungen ändert sich nicht, bis das Skript erneut ausgeführt wird.  
  
 **Statusleiste**  
 Zeigt Systeminformationen an, die dem Abfrage-Editorfenster zugeordnet sind, beispielsweise mit welcher Instanz der Abfrage-Editor verbunden ist.  
  
## <a name="database-engine-query-editor-components"></a>Komponenten des Datenbankmodul-Abfrage-Editors  
 Diese Komponenten sind nur im Datenbankmodul-Abfrage-Editor verfügbar:  
  
 **Debugger**  
 Ermöglicht es, die Ausführung des Codes für bestimmte Anweisungen anzuhalten. Sie können dann Daten und Systeminformationen anzeigen, die bei der Suche nach Fehlern im Code helfen.  
  
 **Fehlerliste**  
 Zeigt von IntelliSense gefundene Syntax und Semantikfehler an. Die Fehlerliste ändert sich dynamisch, während Sie [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts bearbeiten.  
  
 **Grafischer Showplan**  
 Zeigt die in den Ausführungsplan einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung integrierten logischen Schritte an.  
  
 **Clientstatistiken**  
 Zeigt Informationen zur Ausführung der Abfrage nach Kategorien geordnet an. Wenn **Clientstatistiken einschließen** vom Menü **Abfrage** ausgewählt ist, wird das Fenster **Clientstatistiken** nach jedem Ausführen einer Abfrage angezeigt. Statistiken von aufeinander ausgeführten Abfragen werden mit Durchschnittswerten aufgelistet. Wählen Sie **Clientstatistiken zurücksetzen** im Menü **Abfrage** aus, um den Durchschnitt zurückzusetzen.  
  
 **Codeausschnitte**  
 Vorlagen, die Sie als Ausgangspunkt beim Hinzufügen von Anweisungen im Datenbankmodul-Abfrage-Editor verwenden können. Sie können die vordefinierten in SQL Server enthaltenen Ausschnitte einfügen oder eigene Ausschnitte hinzufügen.  
  
 **SQLCMD-Modus**  
 Führt [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts aus, die den vom sqlcmd-Hilfsprogramm unterstützten Satz von Befehlen enthalten. Weitere Informationen finden Sie in den [Themen zur Vorgehensweise für sqlcmd](http://msdn.microsoft.com/library/dd7a2d2b-6327-4d77-ac5a-580d36073ad4).  
  
## <a name="editor-tasks"></a>Editor-Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie die grundlegenden Funktionen im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor angezeigt und verwendet werden.|[Abfrage-Editor des Datenbankmoduls &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)|  
|Beschreibt, wie die grundlegenden Funktionen im MDX-Abfrage-Editor angezeigt und verwendet werden.|[MDX-Abfrage-Editor &#40;Analysis Services – Mehrdimensionale Daten&#41;](http://msdn.microsoft.com/library/777f2c23-1c1c-4b72-9d19-48a4866551f8)|  
|Beschreibt, wie die grundlegenden Funktionen im DMX-Abfrage-Editor angezeigt und verwendet werden.|[DMX-Abfrage-Editor &#40;Analysis Services &mdash; Data Mining&#41;](http://msdn.microsoft.com/library/7ac877a1-0f29-46b9-9a51-73b02172bef1)|  
|Beschreibt, wie die grundlegenden Funktionen im XML/A-Abfrage-Editor angezeigt und verwendet werden.|[XML-Editor &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/xml-editor-sql-server-management-studio.md)|  
|Beschreibt, wie Optionen für die verschiedenen Editoren konfiguriert werden, z. B. Zeilennummerierung und IntelliSense-Optionen.|[Konfigurieren von Editoren &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-editors-sql-server-management-studio.md)|  
|Beschreibt die verschiedenen Methoden zum Öffnen der Editoren in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].|[Öffnen eines Editors &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/open-an-editor-sql-server-management-studio.md)|  
|Beschreibt, wie der Anzeigemodus, z. B. Zeilenumbruch, Aufteilen eines Fensters oder Registerkarten, verwaltet wird.|[Verwalten des Editors und des Ansichtsmodus](../../relational-databases/scripting/manage-the-editor-and-view-mode.md)|  
|Beschreibt, wie Formatierungsoptionen festgelegt werden, z. B. ausgeblendeter Text oder Einzug.|[Verwalten der Codeformatierung](../../relational-databases/scripting/manage-code-formatting.md)|  
|Beschreibt, wie Sie mit Funktionen wie der inkrementellen Suche oder "Gehe zu" durch den Text in einem Editor-Fenster navigieren.|[Navigieren in Code und Text](../../relational-databases/scripting/navigate-code-and-text.md)|  
|Beschreibt, wie Farbcodierungsoptionen für verschiedene Syntaxklassen festgelegt werden, wodurch das Lesen komplexer Anweisungen vereinfacht wird.|[Farbcodierung im Abfrage-Editor](../../relational-databases/scripting/color-coding-in-query-editors.md)|  
|Beschreibt, wie Codegliederung verwendet wird, um Teile komplexer Skripts auszublenden, an denen Sie derzeit nicht arbeiten.|[Codegliederung](../../relational-databases/scripting/code-outlining.md)|  
|Beschreibt, wie Text von einer Position in einem Skript gezogen und an einer anderen Position abgelegt wird.|[Verschieben von Text mit Drag und Drop](../../relational-databases/scripting/drag-and-drop-text.md)|  
|Beschreibt, wie globales Suchen und Ersetzen durchgeführt wird, z. B. beim Ändern von Spaltennamen.|[Suchen und Ersetzen](../../relational-databases/scripting/search-and-replace.md)|  
|Beschreibt, wie Lesezeichen festgelegt werden, damit wichtige Codeteile leichter wiedergefunden werden können.|[Verwalten von Lesezeichen](../../relational-databases/scripting/manage-bookmarks.md)|  
|Beschreibt, wie Skripts oder die Ergebnisse in einem Fenster oder einem Raster gedruckt werden.|[Drucken von Code und Ergebnissen](../../relational-databases/scripting/print-code-and-results.md)|  
|Beschreibt, wie die sqlcmd-Funktionen im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor verwendet werden.|[Bearbeiten von SQLCMD-Skripts mit dem Abfrage-Editor](../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)|  
|Beschreibt, wie IntelliSense-Funktionen verwendet werden, z. B. das automatische Vervollständigen von Objektnamen bei der Eingabe oder das Sicherstellen, dass Breakpoints an gültigen Positionen eingefügt werden.|[IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/intellisense-sql-server-management-studio.md)|  
|Beschreibt, wie Codeausschnitte im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor verwendet werden. Ausschnitte sind Vorlagen für häufig verwendete Anweisungen oder Blöcke. Sie können angepasst oder erweitert werden, um sitespezifische Ausschnitte einzuschließen.|[Transact-SQL-Codeausschnitte](../../relational-databases/scripting/transact-sql-code-snippets.md)|  
|Beschreibt, wie der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger verwendet wird, um Code in Einzelschritten auszuführen und Debuggininformationen anzuzeigen, z. B. die Werte in Variablen und Parametern.|[Transact-SQL-Debugger](../../relational-databases/scripting/transact-sql-debugger.md)|  
|Beschreibt, wie benutzerdefinierte Farben für verschiedene Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)]und diese Farben als Hintergrund der Statusleiste in [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor-Fenstern festgelegt werden.|[Statusleiste &#40;Abfrage-Editor des Datenbankmoduls&#41;](../../relational-databases/scripting/status-bar-database-engine-query-editor.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Tastenkombinationen für SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
