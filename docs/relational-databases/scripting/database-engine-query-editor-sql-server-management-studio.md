---
title: Abfrage-Editor des Datenbankmoduls (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 40ac7dd736d0366fe5cb564719a375e2e6a6a43d
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="database-engine-query-editor-sql-server-management-studio"></a>Abfrage-Editor des Datenbankmoduls (SQL Server Management Studio)
  Mithilfe des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editors können Sie Skripts mit [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen erstellen und ausführen. Der Editor unterstützt auch das Ausführen von Skripts, die **sqlcmd** -Befehle enthalten.  
  
## <a name="transact-sql-f1-help"></a>F1-Hilfe für Transact-SQL  
 Der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor unterstützt bei der Auswahl von F1 den Link zu einem Referenzthema einer bestimmten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung. Markieren Sie hierzu den Namen einer Transact-SQL-Anweisung, und wählen Sie dann F1 aus. Das Hilfesuchmodul sucht dann nach einem Thema mit einem F1-Hilfeattribut, das der markierten Zeichenfolge entspricht.  
  
 Wenn das Hilfesuchmodul kein Thema mit einem F1-Hilfeschlüsselwort findet, das genau der markierten Zeichenfolge entspricht, wird dieses Thema angezeigt. In diesem Fall gibt es zwei Ansätze zum Suchen der gewünschten Hilfe:  
  
-   Kopieren Sie die markierte Zeichenfolge aus dem Editor, fügen Sie diese in der SQL Server-Onlinedokumentation in die Registerkarte "Suchen" ein, und führen Sie eine Suche aus.  
  
-   Markieren Sie nur den Teil der Transact-SQL-Anweisung, die am ehesten zu einem F1-Hilfeschlüsselwort passt, das auf ein Thema angewendet wird, und wählen Sie erneut F1 aus. Für das Suchmodul ist eine genaue Übereinstimmung zwischen der markierten Zeichenfolge und einem einem Thema zugewiesenen F1-Hilfeschlüsselwort erforderlich. Enthält die markierte Zeichenfolge für Ihre Umgebung eindeutige Elemente, z. B. Spalten- oder Parameternamen, erhält das Suchmodul keine Übereinstimmung. Zu den Zeichenfolgen, die markiert werden können, gehören die folgenden:  
  
    -   Der Name einer Transact-SQL-Anweisung, zum Beispiel SELECT, CREATE DATABASE oder BEGIN TRANSACTION.  
  
    -   Der Name einer integrierten Funktion, zum Beispiel SERVERPROPERTY oder @@VERSION.  
  
    -   Der Name einer im System gespeicherten Prozedurtabelle oder einer Sicht, z. B. "sys.data_spaces" oder "sp_tableoption".  
  
## <a name="working-with-the-database-engine-query-editor"></a>Arbeiten mit dem Datenbankmodul-Abfrage-Editor  
 Der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Abfrage-Editor ist einer von vier in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] implementierten Editoren. Eine Beschreibung der im [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Abfrage-Editor implementierten Funktionalität und der Hauptaufgaben, die Sie mit dem Editor ausführen können, finden Sie unter [Abfrage-Editor des Datenbankmoduls &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
## <a name="sql-editor-toolbar"></a>SQL-Editor-Symbolleiste  
 Wenn der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor geöffnet ist, wird die SQL-Editor-Symbolleiste mit den folgenden Schaltflächen angezeigt:  
  
 **Connect**  
 Öffnet das Dialogfeld **Verbindung mit Server herstellen** . Mithilfe dieses Dialogfelds können Sie eine Verbindung mit einem Server herstellen.  
  
 **Trennen**  
 Trennt den aktuellen Abfrage-Editor vom Server.  
  
 **Verbindung ändern**  
 Öffnet das Dialogfeld **Verbindung mit Server herstellen** . Mithilfe dieses Dialogfelds können Sie eine Verbindung mit einem anderen Server herstellen.  
  
 **Neue Abfrage mit aktueller Verbindung**  
 Öffnet ein neues Abfrage-Editor-Fenster und verwendet die Verbindungsinformationen des aktuellen Abfrage-Editor-Fensters.  
  
 **Verfügbare Datenbanken**  
 Wechselt die Verbindung zu einer anderen Datenbank auf demselben Server.  
  
 **Execute**  
 Führt den ausgewählten bzw. (wenn kein Code ausgewählt ist) den gesamten Code im Abfrage-Editor aus.  
  
 **Debuggen**  
 Aktiviert den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger. Dieser Debugger unterstützt Debugoperationen, wie das Festlegen von Breakpoints, das Beobachten von Variablen und die schrittweise Ausführung von Code.  
  
 **Ausführung der Abfrage abbrechen**  
 Sendet eine Abbruchsanforderung an den Server. Einige Abfragen können nicht sofort abgebrochen werden, sondern müssen auf angemessene Bedingungen für einen Abbruch warten. Beim Abbruch von Transaktionen können Verzögerungen auftreten, während für die Transaktionen ein Rollback ausgeführt wird.  
  
 **Analysieren**  
 Überprüft die Syntax des ausgewählten Codes. Wenn kein Code ausgewählt ist, wird die Syntax des gesamten Codes im Abfrage-Editor-Fenster geprüft.  
  
 **Geschätzten Ausführungsplan anzeigen**  
 Fordert einen Abfrageausführungsplan vom Abfrageprozessor an, ohne die Abfrage tatsächlich auszuführen. Der Plan wird im Fenster **Ausführungsplan** angezeigt. Dieser Plan verwendet Indexstatistiken als Schätzung für die Anzahl der zu erwartenden Zeilen, die während der einzelnen Schritte der Abfrageausführung zurückgegeben werden. Der tatsächlich verwendete Abfrageplan kann sich vom geschätzten Ausführungsplan unterscheiden. Dieser Fall kann eintreten, wenn die Anzahl der zurückgegebenen Zeilen erheblich von der Schätzung abweicht und der Abfrageprozessor den Plan aus Effizienzgründen ändert.  
  
 **Abfrageoptionen**  
 Öffnet das Dialogfeld **Abfrageoptionen** . Mithilfe dieses Dialogfelds konfigurieren Sie die Standardoptionen für die Abfrageausführung und die Abfrageergebnisse.  
  
 **IntelliSense aktiviert**  
 Gibt an, ob die IntelliSense-Funktionalität im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor verfügbar ist.  
  
 **Tatsächlichen Ausführungsplan einschließen**  
 Führt die Abfrage aus und gibt die Abfrageergebnisse sowie den Ausführungsplan, der für die Abfrage verwendet wurde, zurück. Letzterer wird im Fenster **Ausführungsplan** als grafischer Abfrageplan angezeigt.  
  
 **Clientstatistiken einschließen**  
 Schließt das Fenster **Clientstatistiken** ein, das Statistiken zu der Abfrage, den Netzwerkpaketen und der verstrichenen Zeit für die Abfrage enthält.  
  
 **Ergebnisse in Text**  
 Gibt die Abfrageergebnisse als Text im Fenster **Ergebnisse** zurück.  
  
 **Ergebnisse in Raster**  
 Gibt die Abfrageergebnisse als ein oder mehrere Raster im Fenster **Ergebnisse** zurück.  
  
 **Ergebnisse in Datei**  
 Wenn die Abfrage ausgeführt wird, wird das Dialogfeld **Ergebnisse speichern** geöffnet. Wählen Sie unter **Speichern in**den Ordner aus, in dem Sie die Datei speichern möchten. Geben Sie unter **Dateiname**den Namen der Datei ein, und klicken Sie dann auf **Speichern** , um die Abfrageergebnisse als **** Berichtsdatei mit der Dateierweiterung ".rpt" zu speichern. Klicken Sie auf den Pfeil nach unten auf der Schaltfläche **Speichern** , und klicken Sie anschließend auf **Mit Codierung speichern**, um erweiterte Optionen anzugeben.  
  
 **Auswahl kommentieren**  
 Markiert die aktuelle Zeile als Kommentar, indem am Zeilenanfang ein Kommentaroperator (--) hinzugefügt wird.  
  
 **Auskommentierung der Auswahl aufheben**  
 Markiert die aktuelle Zeile als aktive Quellanweisung, indem alle Kommentaroperatoren (--) am Zeilenanfang entfernt werden.  
  
 **Zeileneinzug verkleinern**  
 Verschiebt durch das Entfernen von Leerzeichen am Zeilenanfang den Text der Zeile nach links.  
  
 **Zeileneinzug vergrößern**  
 Verschiebt durch das Hinzufügen von Leerzeichen am Zeilenanfang den Text der Zeile nach rechts.  
  
 **Werte für Vorlagenparameter angeben**  
 Öffnet ein Dialogfeld, in dem Sie Werte für Parameter in gespeicherten Prozeduren und Funktionen festlegen können.  
  
 Sie können die SQL-Editor-Symbolleiste auch hinzufügen, indem Sie im Menü **Ansicht** nacheinander **Symbolleisten**und **SQL-Editor**auswählen. Wenn Sie die SQL-Editor-Symbolleiste hinzufügen, ohne dass ein Fenster des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editors geöffnet ist, steht keine der Schaltflächen zur Verfügung.  
  
## <a name="sql-editor-toolbar"></a>SQL-Editor-Symbolleiste  
 Wenn ein [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor-Fenster geöffnet ist, können Sie die Symbolleiste Debuggen hinzufügen, indem Sie im Menü **Ansicht** zuerst **Symbolleisten**und dann **Debuggen**auswählen. Wenn Sie die Symbolleiste Debuggen hinzufügen, ohne dass ein Fenster des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editors geöffnet ist, steht keine der Schaltflächen zur Verfügung.  
  
 **Continue**  
 Führt den Code im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor-Fenster bis zu einem Breakpoint aus.  
  
 **Alle unterbrechen**  
 Stellt den Debugger so ein, dass im Falle einer Unterbrechung alle Prozesse angehalten werden, an die der Debugger angefügt ist.  
  
 **Debuggen beenden**  
 Deaktiviert den Debugmodus für das ausgewählte [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor-Fenster und stellt den Standardausführungsmodus wieder her.  
  
 **Nächste Anweisung anzeigen**  
 Verschiebt den Cursor zur nächsten auszuführenden Anweisung.  
  
 **Einzelschritt**  
 Die nächste Anweisung wird ausgeführt. Wenn die nächste Anweisung eine gespeicherte Transact-SQL-Prozedur, eine Funktion oder einen Trigger aufruft, zeigt der Debugger ein neues **Abfrage-Editor** -Fenster an, das den Code des Moduls enthält. Das Fenster befindet sich im Debuggingmodus, und die Ausführung hält bei der ersten Anweisung im Modul an. Sie können sich dann durch das Modul bewegen, indem Sie z. B. Breakpoints festlegen oder den Code schrittweise durchlaufen.  
  
 **Prozedurschritt**  
 Die nächste Anweisung wird ausgeführt. Wenn die Anweisung eine gespeicherte Transact-SQL-Prozedur, eine Funktion oder einen Trigger aufruft, wird das Modul bis zum Ende ausgeführt, und die Ergebnisse werden an den aufrufenden Code zurückgegeben. Wenn Sie sicher sind, dass im Modul keine Fehler vorliegen, können Sie es überspringen. Die Ausführung hält bei der Anweisung an, die dem Aufruf des Moduls folgt.  
  
 **Rücksprung**  
 Springt zur nächsthöheren Aufrufebene (Funktion, gespeicherte Prozedur oder Trigger) zurück. Die Ausführung hält bei der Anweisung an, die dem Aufruf der gespeicherten Prozedur, der Funktion oder dem Trigger folgt.  
  
 **Windows**  
 Öffnet entweder das Fenster **Breakpoint** oder das **Direktfenster** .  
  
## <a name="see-also"></a>Siehe auch  
 [Tastenkombinationen für SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
