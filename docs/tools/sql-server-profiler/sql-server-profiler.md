---
title: "SQL Server Profiler | Microsoft Docs"
ms.custom: ""
ms.date: "10/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Profiler [SQL Server Profiler], Informationen zu SQL Server Profiler"
  - "Ablaufverfolgung [SQL Server], SQL Server Profiler"
  - "Datenbanküberwachung [SQL Server], SQL Server Profiler"
  - "Optimieren von Datenbanken [SQL Server], SQL Server Profiler"
  - "SQL Server Profiler"
  - "Serverleistung [SQL Server], SQL Server Profiler"
  - "Profiler [SQL Server Profiler]"
  - "Ablaufverfolgung [SQL Server]"
  - "Überwachen der Leistung [SQL Server], SQL Server Profiler"
  - "Ereignisse [SQL Server], SQL Server Profiler"
  - "SQL Server Profiler, Informationen zu SQL Server Profiler"
  - "Tools [SQL Server], SQL Server Profiler"
  - "Datenbankleistung [SQL Server], SQL Server Profiler"
  - "trace [SQL Server]"
ms.assetid: 3ad5f33d-559e-41a4-bde6-bb98792f7f1a
caps.latest.revision: 46
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 46
---
# SQL Server Profiler
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ist eine Benutzeroberfläche zum Erstellen und Verwalten von Ablaufverfolgungen sowie zum Analysieren und Wiedergeben derer Ergebnisse. Die Ereignisse werden in einer Ablaufverfolgungsdatei gespeichert, die später analysiert oder beim Versuch, ein Problem zu diagnostizieren, zur Wiedergabe einer bestimmten Reihe von Schritten verwendet werden kann.  
  
>**WICHTIG!**  
> Wir kündigen die Veraltung von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] für die [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Ablaufverfolgungssammlung und -Ablaufverfolgungswiedergabe an. Diese Funktionen stehen **noch** in SQL Server 2016 zur Verfügung, werden jedoch in einer späteren Version entfernt.
>   
>  Der *Microsoft.SqlServer.Management.Trace* -Namespace, der die Objekte für die Microsoft SQL Server-Ablaufverfolgung und -Wiedergabe enthält, ist ebenfalls veraltet.                     
**Beachten Sie** , dass [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] für die Analysis Services-Arbeitsauslastungen NICHT veraltet ist und weiterhin unterstützt wird.
>
> Übermitteln Sie Ihr Feedback und Ihre Fragen auf unserer **[Connect-Seite](https://connect.microsoft.com/SQLServer/Feedback)**

 ## Wo befindet sich der Profiler?
 
 Sie können den Profiler auf verschiedene Arten in SSMS starten. [In diesem Thema werden die Verfahren zum Starten des Profilers aufgeführt.](https://msdn.microsoft.com/library/ms173799.aspx)
  
## Aufzeichnen und Wiedergeben von Ablaufverfolgungsdaten 
In der folgenden Tabelle werden die Funktionen angezeigt, deren Verwendung wir in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] empfehlen, um Ablaufverfolgungsdaten zu erfassen und wiederzugeben.
  
||||  
|-|-|-|  
|**Funktion/Zielarbeitsauslastung**|**Relationales Modul**|**Analysis Services**|  
|**Ablaufverfolgungssammlung**|Grafische Benutzeroberfläche für[erweiterte Ereignisse](https://msdn.microsoft.com/library/bb630282.aspx) in SQL Server Management Studio|SQL Server Profiler|  
|**Ablaufverfolgungswiedergabe**|[Distributed Replay](https://msdn.microsoft.com/library/ff878183.aspx)|SQL Server Profiler|  
  
## SQL Server Profiler  
 Microsoft [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ist eine grafische Benutzeroberfläche für die SQL-Ablaufverfolgung zur Überwachung einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] oder Analysis Services. Daten über die einzelnen Ereignisse können aufgezeichnet und in einer Datei oder Tabelle zur späteren Analyse gespeichert werden. Beispielsweise können Sie eine Produktionsumgebung überwachen und feststellen, welche gespeicherten Prozeduren langsam ablaufen und dadurch die Leistung beeinträchtigen. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] wird für Aktivitäten verwendet, wie z. B.:  
  
-   Schrittweises Untersuchen problematischer Abfragen, um die Ursache des Problems zu ermitteln.  
  
-   Suchen und Diagnostizieren von Abfragen, die sehr langsam ausgeführt werden.  
  
-   Erfassen der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, die zu einem Problem geführt haben. Mithilfe der gespeicherten Ablaufverfolgung kann das Problem auf einem Testserver repliziert werden, um es dort zu diagnostizieren.  
  
-   Überwachen der Leistung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Optimierung der Arbeitsauslastung. Informationen zum Optimieren des physischen Datenbankentwurfs für Datenbankarbeitslasten finden Sie unter [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md).  
  
-   Korrelieren von Leistungsindikatoren zur Diagnose von Problemen.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] unterstützt auch die Überwachung von Aktionen, die für Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt werden. Durch Überwachungen werden sicherheitsbezogene Aktionen aufgezeichnet, die später von einem Sicherheitsadministrator überprüft werden können.  
  
## SQL Server Profiler-Konzepte  
 Um [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]verwenden zu können, müssen Sie die Begriffe verstehen, mit denen die Funktionsweise des Tools beschrieben wird.  
  
>**HINWEIS!** Das Verständnis von der SQL-Ablaufverfolgung hilft ungemein bei der Arbeit mit SQL Server Profiler. Weitere Informationen finden Sie unter [SQL Trace](../../relational-databases/sql-trace/sql-trace.md).  
  
 **Ereignis**  
 Ein Ereignis ist eine Aktion, die innerhalb einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]generiert wird. Im Folgenden sind Beispiele dafür aufgeführt:  
  
-   Anmeldeverbindungen, fehlgeschlagene und getrennte Verbindungen.  
  
-   Die Transact-SQL-Anweisungen SELECT, INSERT, UPDATE und DELETE.  
  
-   Der Status von RPC-Batches (Remote Procedure Call, Remoteprozeduraufruf).  
  
-   Der Start oder das Ende einer gespeicherten Prozedur.  
  
-   Der Start oder das Ende von Anweisungen innerhalb gespeicherter Prozeduren.  
  
-   Der Start oder das Ende eines SQL-Batches.  
  
-   Ein Fehler, der in das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll geschrieben wird.  
  
-   Eine Sperre, die für ein Datenbankobjekt eingerichtet oder aufgehoben wird.  
  
-   Ein geöffneter Cursor.  
  
-   Überprüfungen der Sicherheitsberechtigungen.  
  
 Die gesamten von einem Ereignis generierten Daten werden in der Ablaufverfolgung in einer einzelnen Zeile angezeigt. Diese Zeile wird von Datenspalten unterbrochen, die Details zu den Ereignissen enthält.  
  
 **EventClass**  
 Eine Ereignisklasse ist ein Ereignistyp, dessen Ablauf verfolgt werden kann. Die Ereignisklasse enthält alle Daten, die von einem Ereignis berichtet werden können. Im Folgenden sind Beispiele für Ereignisklassen aufgeführt:  
  
-   **SQL:BatchCompleted**  
  
-   **Audit Login**  
  
-   **Audit Logout**  
  
-   **Lock:Acquired**  
  
-   **Lock:Released**  
  
 **EventCategory**  
 Eine Ereigniskategorie bestimmt, wie Ereignisse innerhalb von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]zusammengefasst werden. So sind beispielsweise alle Sperrereignisklassen in der Ereigniskategorie **Sperren** zusammengefasst. Ereigniskategorien sind jedoch nur in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]vorhanden. Dieser Begriff drückt nicht aus, wie Modulereignisse gruppiert werden.  
  
 **DataColumn**  
 Eine Datenspalte ist ein Attribut einer Ereignisklasse, die in der Ablaufverfolgung erfasst ist. Da von der Ereignisklasse der Typ der Daten festgelegt wird, die gesammelt werden können, gelten nicht alle Datenspalten für alle Ereignisklassen. In einer Ablaufverfolgung, in der die **Lock:Acquired** -Ereignisklasse erfasst wird, enthält die **BinaryData** -Datenspalte beispielsweise den Wert der gesperrten Seiten-ID oder der Zeile, aber die **Integer Data** -Datenspalte enthält keine Werte, weil sie nicht auf die erfasste Ereignisklasse anwendbar ist.  
  
 **Vorlage**  
 Eine Vorlage definiert die Standardkonfiguration für eine Ablaufverfolgung. Dazu gehören insbesondere die Ereignisklassen, die mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]überwacht werden sollen. Sie können beispielsweise eine Vorlage erstellen, mit der die zu verwendenden Ereignisse, Datenspalten und Filter angegeben werden. Eine Vorlage wird nicht ausgeführt, sondern als Datei mit der Erweiterung TDF gespeichert. Nach dem Speichern steuert die Vorlage die Ablaufverfolgungsdaten, die beim Starten einer auf der Vorlage basierenden Ablaufverfolgung erfasst werden.  
  
 **Ablaufverfolgung**  
 Eine Ablaufverfolgung zeichnet Daten auf der Grundlage der ausgewählten Ereignisklassen, Datenspalten und Filter auf. Sie können beispielsweise eine Ablaufverfolgung erstellen, um Ausnahmefehler aufzuzeichnen. Wählen Sie dazu die **Exception** -Ereignisklasse und die Datenspalten **Fehler**, **Status**und **Schweregrad** aus. Daten aus diesen drei Spalten müssen gesammelt werden, damit die Ablaufverfolgung sinnvolle Daten als Ergebnis liefert. Sie können dann eine solcherart konfigurierte Ablaufverfolgung ausführen und Daten aufgrund aller **Exception** -Ereignisse sammeln, die auf dem Server auftreten. Ablaufverfolgungsdaten können gespeichert oder sofort für Analysezwecke verwendet werden. Ablaufverfolgungen können zu einem späteren Zeitpunkt wiedergegeben werden, obwohl bestimmte Ereignisse wie **Exception** -Ereignisse nie wiedergegeben werden. Sie können die Ablaufverfolgung als Vorlage speichern, um in Zukunft ähnliche Ablaufverfolgungen zu erstellen.  
  
 SQL Server bietet zwei Möglichkeiten für die Ablaufverfolgung einer Instanz von SQL Server: [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] und gespeicherte Systemprozeduren.  
  
 **Filter**  
 Beim Erstellen einer Ablaufverfolgung oder Vorlage können Sie Kriterien definieren, um die von dem Ereignis gesammelten Daten zu filtern. Damit Ablaufverfolgungen nicht zu groß werden, können Sie sie filtern, sodass nur eine Teilmenge der Ereignisdaten gesammelt wird. Sie können beispielsweise die Microsoft Windows-Benutzernamen in der Ablaufverfolgung auf bestimmte Benutzer beschränken, wodurch die Ausgabedatenmenge kleiner wird.  
  
 Ist kein Filter eingerichtet, werden alle Ereignisse der ausgewählten Ereignisklassen in der Ablaufverfolgungsausgabe zurückgegeben.  
  
## SQL Server Profiler-Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Listet die vordefinierten Vorlagen, die SQL Server zum Überwachen bestimmter Ereignistypen bereitstellt, und die zum Wiedergeben von Ablaufverfolgungen erforderlichen Berechtigungen auf.|[Vorlagen und Berechtigungen in SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)|  
|Beschreibt, wie SQL Server Profiler ausgeführt wird.|[Erforderliche Berechtigungen zum Ausführen von SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgung erstellt wird.|[Erstellen einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)|  
|Beschreibt, wie Ereignisse und Datenspalten für eine Ablaufverfolgungsdatei angegeben werden.|[Angeben von Ereignissen und Datenspalten für eine Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)|  
|Beschreibt, wie Ablaufverfolgungsergebnisse in einer Datei gespeichert werden.|[Speichern von Ablaufverfolgungsergebnissen in einer Datei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)|  
|Beschreibt, wie Ablaufverfolgungsergebnisse in einer Tabelle gespeichert werden.|[Speichern von Ablaufverfolgungsergebnissen in einer Tabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)|  
|Beschreibt, wie Ereignisse in einer Ablaufverfolgung gefiltert werden.|[Filtern von Ereignissen in einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)|  
|Beschreibt, wie Filterinformationen angezeigt werden.|[Anzeigen von Filterinformationen &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)|  
|Beschreibt, wie ein Filter geändert wird.|[Ändern eines Filters &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)|  
|Beschreibt, wie eine maximale Dateigröße für eine Ablaufverfolgungsdatei (SQL Server Profiler) festgelegt wird.|[Festlegen einer maximalen Dateigröße für eine Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)|  
|Beschreibt, wie eine maximale Tabellengröße für eine Ablaufverfolgungstabelle festgelegt wird.|[Festlegen der maximalen Tabellengröße für eine Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgung gestartet wird.|[Starten einer Ablaufverfolgung](../../tools/sql-server-profiler/start-a-trace.md)|  
|Beschreibt, wie eine Ablaufverfolgung nach dem Herstellen einer Verbindung mit einem Server automatisch gestartet wird.|[Automatisches Starten einer Ablaufverfolgung nach dem Herstellen einer Verbindung mit einem Server &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)|  
|Beschreibt, wie Ereignisse basierend auf der Ereignisstartzeit gefiltert werden.|[Filtern von Ereignissen nach Ereignisstartzeit &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)|  
|Beschreibt, wie Ereignisse basierend auf der Ereignisendzeit gefiltert werden.|[Filtern von Ereignissen anhand der Ereignisendzeit &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)|  
|Beschreibt, wie Serverprozess-IDs (SPIDs) in einer Ablaufverfolgung gefiltert werden.|[Filtern von Server-Prozess-IDs &#40;SPIDs&#41; in einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgung angehalten wird.|[Anhalten einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgung beendet wird.|[Beenden einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgung ausgeführt wird, nachdem sie angehalten oder beendet wurde.|[Ausführen einer Ablaufverfolgung, nachdem sie angehalten oder beendet wurde &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)|  
|Beschreibt, wie ein Ablaufverfolgungsfenster gelöscht wird.|[Löschen des Inhalts eines Ablaufverfolgungsfensters &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)|  
|Beschreibt, wie ein Ablaufverfolgungsfenster geschlossen wird.|[Schließen eines Ablaufverfolgungsfensters &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)|  
|Beschreibt, wie Standardeinstellungen für Ablaufverfolgungsdefinitionen festgelegt werden.|[Festlegen der Standardeinstellungen für Ablaufverfolgungsdefinitionen &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)|  
|Beschreibt, wie Standardeinstellungen für die Ablaufverfolgungsanzeige festgelegt werden.|[Festlegen der Standardeinstellungen für die Ablaufverfolgungsanzeige &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgungsdatei geöffnet wird.|[Öffnen einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgungstabelle geöffnet wird.|[Öffnen einer Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgungstabelle wiedergegeben wird.|[Wiedergeben einer Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgungsdatei wiedergegeben wird.|[Wiedergeben einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)|  
|Beschreibt, wie jeweils ein einzelnes Ereignis wiedergegeben wird.|[Wiedergeben von jeweils einem einzelnen Ereignis &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)|  
|Beschreibt die Wiedergabe bis zu einem Breakpoint.|[Wiedergeben bis zu einem Breakpoint &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)|  
|Beschreibt die Wiedergabe bis zu einer Cursorposition.|[Wiedergeben bis zu einer Cursorposition &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)|  
|Beschreibt, wie ein Transact-SQL-Skript wiedergegeben wird.|[Wiedergeben eines Transact-SQL-Skripts&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgungsvorlage erstellt wird.|[Erstellen einer Ablaufverfolgungsvorlage &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgungsvorlage geändert wird.|[Ändern einer Ablaufverfolgungsvorlage &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)|  
|Beschreibt, wie globale Ablaufverfolgungsoptionen festgelegt werden.|[Festlegen globaler Ablaufverfolgungsoptionen &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)|  
|Beschreibt, wie ein Wert oder eine Datenspalte während der Ablaufverfolgung gesucht wird.|[Suchen eines Wertes oder einer Datenspalte während der Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)|  
|Beschreibt, wie eine Vorlage aus einer ausgeführten Ablaufverfolgung abgeleitet wird.|[Ableiten einer Vorlage von einer zurzeit ausgeführten Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)|  
|Beschreibt, wie eine Vorlage aus einer Ablaufverfolgungsdatei oder Ablaufverfolgungstabelle abgeleitet wird.|[Ableiten einer Vorlage von einer Ablaufverfolgungsdatei oder Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)|  
|Beschreibt, wie ein Transact-SQL-Skript für das Ausführen einer Ablaufverfolgung erstellt wird.|[Erstellen eines Transact-SQL-Skripts zum Ausführen einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgungsvorlage exportiert wird.|[Exportieren einer Ablaufverfolgungsvorlage &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgungsvorlage importiert wird.|[Importieren einer Ablaufverfolgungsvorlage &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)|  
|Beschreibt, wie ein Skript aus einer Ablaufverfolgung extrahiert wird.|[Extrahieren eines Skripts aus einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)|  
|Beschreibt, wie eine Ablaufverfolgung mit Windows-Leistungsprotokolldaten korreliert wird.|[Korrelieren einer Ablaufverfolgung mit Windows-Leistungsprotokolldaten &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)|  
|Beschreibt, wie in einer Ablaufverfolgung angezeigte Spalten organisiert werden.|[Organisieren von in einer Ablaufverfolgung angezeigten Spalten &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)|  
|Beschreibt, wie SQL Server Profiler gestartet wird.|[Starten von SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)|  
|Beschreibt, wie Ablaufverfolgungen und Ablaufverfolgungsvorlagen gespeichert werden.|[Speichern von Ablaufverfolgungen und Ablaufverfolgungsvorlagen](../../tools/sql-server-profiler/save-traces-and-trace-templates.md)|  
|Beschreibt, wie Ablaufverfolgungsvorlagen geändert werden.|[Ändern von Ablaufverfolgungsvorlagen](../../tools/sql-server-profiler/modify-trace-templates.md)|  
|Beschreibt, wie eine Ablaufverfolgung mit Windows-Leistungsprotokolldaten korreliert wird.|[Korrelieren einer Ablaufverfolgung mit Windows-Leistungsprotokolldaten](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data.md)|  
|Beschreibt, wie Ablaufverfolgungen mit SQL Server Profiler angezeigt und analysiert werden.|[Anzeigen und Analysieren von Ablaufverfolgungen mit SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)|  
|Beschreibt, wie Deadlocks mit SQL Server Profiler analysiert werden.|[Analysieren von Deadlocks mit SQL Server Profiler](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)|  
|Beschreibt, wie Abfragen mit SHOWPLAN-Ergebnissen in SQL Server Profiler analysiert werden.|[Analysieren von Abfragen mit SHOWPLAN-Ergebnissen in SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)|  
|Beschreibt, wie Ablaufverfolgungen mit SQL Server Profiler gefiltert werden.|[Filtern von Ablaufverfolgungen mit SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)|  
|Beschreibt, wie die Wiedergabefunktionen von SQL Server Profiler verwendet werden.|[Wiedergeben von Ablaufverfolgungen](../../tools/sql-server-profiler/replay-traces.md)|  
|Listet die kontextbezogenen Hilfethemen für SQL Server Profiler auf.|[SQL Server Profiler (F1-Hilfe)](../../tools/sql-server-profiler/sql-server-profiler-f1-hilfe.md)|  
|Listet die von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zur Leistungs- und Aktivitätsüberwachung verwendeten gespeicherten Systemprozeduren auf.|[Gespeicherte Prozeduren von SQL Server Profiler &#40;SQL Server Profiler&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)|  
  
## Siehe auch  
 [Sperren-Ereigniskategorie](../../relational-databases/event-classes/locks-event-category.md)   
 [Sessions-Ereigniskategorie](../../relational-databases/event-classes/sessions-event-category.md)   
 [Gespeicherte Prozeduren (Ereigniskategorie)](../../relational-databases/event-classes/stored-procedures-event-category.md)   
 [TSQL-Ereigniskategorie](../../relational-databases/event-classes/tsql-event-category.md)   
 [Überwachen der Serverleistung und -aktivität](../../relational-databases/performance/server-performance-and-activity-monitoring.md)  
  
  