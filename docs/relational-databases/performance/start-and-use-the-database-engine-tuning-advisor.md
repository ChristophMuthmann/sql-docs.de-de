---
title: Starten und Verwenden des Datenbankoptimierungsratgebers | Microsoft Docs
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dta.workload.f1
- sql13.dta.general.f1
- sql13.dta.advancedtuningoptions.f1
- sql13.dta.tuningoptions.f1
- sql13.dta.progress.f1
- sql13.dta.options.f1
helpviewer_keywords: Database Engine Tuning Advisor [SQL Server], starting
ms.assetid: a4e3226a-3917-4ec8-bdf0-472879d231c9
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 21efab98503bc82485097c87b04623bf38366a68
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="start-and-use-the-database-engine-tuning-advisor"></a>Starten und Verwenden des Datenbankoptimierungsratgebers
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie der Datenbankoptimierungsratgeber in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] gestartet und verwendet wird. Informationen zum Anzeigen der Ergebnisse und Arbeiten mit den Ergebnissen nach dem Optimieren einer Datenbank finden Sie unter [Anzeigen und Verwenden der Ausgabe des Datenbankoptimierungsratgebers](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md).  
  
##  <a name="Initialize"></a> Initialisieren des Datenbankoptimierungsratgebers  
 Bei der ersten Verwendung muss ein Benutzer, der Mitglied der festen Serverrolle **sysadmin** ist, den Datenbankoptimierungsratgeber starten. Das liegt daran, dass mehrere Systemtabellen in der Datenbank **msdb** erstellt werden müssen, um das Optimieren von Vorgängen zu unterstützen. Die Initialisierung ermöglicht darüber hinaus Benutzern, die Mitglieder der festen Datenbankrolle **db_owner** sind, Arbeitsauslastungen für Tabellen in Datenbanken zu optimieren, die sie besitzen.  
  
 Ein Benutzer mit Systemadministratorberechtigungen muss eine der folgenden Aktionen ausführen.  
  
-   Verwenden Sie die grafische Benutzeroberfläche des Datenbankoptimierungsratgebers, um eine Verbindung mit einer [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Instanz herzustellen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Starten Sie den Datenbankoptimierungsratgeber](#Start) .  
  
-   Verwenden Sie das Hilfsprogramm **dta** , um die erste Arbeitsauslastung zu optimieren. Weitere Informationen hierzu finden Sie unter [Verwenden des dta-Hilfsprogramms](#dta) an späterer Stelle in diesem Thema.  
  
##  <a name="Start"></a> Starten Sie den Datenbankoptimierungsratgeber  
 Sie können die grafische Benutzeroberfläche (GUI, Graphical User Interface) des Datenbankmodul-Optimierungsratgebers auf verschiedene Arten starten, um in einer Reihe von Szenarien das Optimieren von Datenbanken zu unterstützen. Zu den unterschiedlichen Startmöglichkeiten des Datenbankoptimierungsratgebers gehören Folgende: über das Menü **Start** , über das Menü **Extras** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], über den Abfrage-Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]und über das Menü **Extras** in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Wenn Sie den Datenbankoptimierungsratgeber zum ersten Mal starten, wird das Dialogfeld **Verbindung mit Server herstellen** angezeigt, in dem Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angeben können, zu der Sie eine Verbindung herstellen möchten.  
  
> [!WARNING]  
>  Starten Sie den Datenbankoptimierungsratgeber nicht, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Einzelbenutzermodus ausgeführt wird. Wenn Sie versuchen ihn zu starten, während der Server im Einzelbenutzermodus ausgeführt wird, wird ein Fehler zurückgegeben und der Datenbankoptimierungsratgeber wird nicht gestartet. Weitere Informationen zum Einzelbenutzermodus finden Sie unter [Starten von SQL Server im Einzelbenutzermodus](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md).  
  
#### <a name="to-start-database-engine-tuning-advisor-from-the-windows-start-menu"></a>So starten Sie den Datenbankoptimierungsratgeber aus dem Windows-Startmenü  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie nacheinander auf **Microsoft SQL Server**und **Leistungstools**, und klicken Sie dann auf **Datenbankoptimierungsratgeber**.  
  
#### <a name="to-start-the-database-engine-tuning-advisor-in-sql-server-management-studio"></a>So starten Sie den Datenbankoptimierungsratgeber in SQL Server Management Studio  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Extras** auf **Datenbankoptimierungsratgeber**.  
  
#### <a name="to-start-the-database-engine-tuning-advisor-from-the-sql-server-management-studio-query-editor"></a>So starten Sie den Datenbankoptimierungsratgeber über den Abfrage-Editor von SQL Server Management Studio  
  
1.  Öffnen Sie in [!INCLUDE[tsql](../../includes/tsql-md.md)] eine [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]-Skriptdatei. Weitere Informationen finden Sie unter [Abfrage- und Text-Editoren &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
2.  Wählen Sie im [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skript eine Abfrage aus, oder wählen Sie das gesamte Skript aus, klicken Sie mit der rechten Maustaste auf die Auswahl, und wählen Sie **Abfrage mit dem Datenbankoptimierungsratgeber analysieren**. Die GUI des Datenbankoptimierungsratgebers wird geöffnet und importiert das Skript als Arbeitsauslastung in Form einer XML-Datei. Sie können einen Namen für die Sitzung und Optimierungsoptionen angeben, um die ausgewählten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen als Arbeitsauslastung zu optimieren.  
  
#### <a name="to-start-the-database-engine-tuning-advisor-in-sql-server-profiler"></a>So starten Sie den Datenbankoptimierungsratgeber in SQL Server Profiler  
  
1.  Klicken Sie in SQL Server Profiler im Menü **Extras** auf **Datenbankoptimierungsratgeber**.  
  
##  <a name="Create"></a> Erstellen einer Arbeitsauslastung  
 Die Arbeitsauslastung besteht aus einer Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, die für eine oder mehrere Datenbanken ausgeführt werden, die Sie optimieren möchten. Der Datenbankoptimierungsratgeber analysiert diese Arbeitsauslastungen, um Indizes oder Partitionsstrategien zu empfehlen, die die Abfrageleistung Ihres Servers verbessern.  
  
 Sie können mit einer der folgenden Methoden ein neue Arbeitsauslastung erstellen.  
  
-   Verwenden Sie den [Abfragespeicher](../../relational-databases/performance/how-query-store-collects-data.md) als Arbeitsauslastung. Dadurch können Sie die manuelle Erstellung einer Auslastung vermeiden. Weitere Informationen finden Sie unter [Tuning Database Using Workload from Query Store (Datenbankoptimierung mithilfe der Arbeitsauslastung aus dem Abfragespeicher)](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md).  

      ||  
      |-|  
      |**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  

  
-   Verwenden Sie den Plancache als Arbeitsauslastung. Dadurch können Sie die manuelle Erstellung einer Auslastung vermeiden. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Optimieren einer Datenbank](#Tune) .  
  
-   Verwenden Sie den Abfrage-Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder einen bevorzugten Text-Editor, um [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skriptarbeitsauslastungen manuell zu erstellen.  
  
-   Um Arbeitsauslastungen für Ablaufverfolgungsdateien oder -tabellen zu erstellen, verwenden Sie [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  
  
    > [!NOTE]  
    >  Wenn als Arbeitsauslastung eine Ablaufverfolgungstabelle verwendet wird, muss diese Tabelle auf dem Server vorhanden sein, auf dem die Optimierung durch den Datenbankoptimierungsratgeber vorgenommen wird. Wenn Sie die Ablaufverfolgungstabelle auf einem anderen Server erstellen, müssen Sie sie dann auf den Server verschieben, der über den Datenbankoptimierungsratgeber optimiert wird.  
  
-   Arbeitsauslastungen können ebenfalls in eine XML-Eingabedatei eingebettet werden, in der Sie auch für jedes Ereignis eine Gewichtung angeben können. Weitere Informationen zum Bestimmen eingebetteter Arbeitslasten finden Sie weiter unten in diesem Thema unter [Erstellen einer XML-Eingabedatei](#XMLInput) .  
  
###  <a name="SSMS"></a> So erstellen Sie Transact-SQL-Skriptarbeitsauslastungen  
  
1.  Starten Sie den Abfrage-Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Weitere Informationen finden Sie unter [Abfrage- und Text-Editoren &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
2.  Geben Sie Ihr [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skript in den Abfrage-Editor ein. Dieses Skript sollte eine Gruppe von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen an mindestens eine zu optimierende Datenbank enthalten.  
  
3.  Speichern Sie die Datei mit der Erweiterung **SQL**. Die Datenbankoptimierungsratgeber-GUI und das Befehlszeilen-Hilfsprogramm **dta** können dieses [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript als Arbeitsauslastung verwenden.  
  
###  <a name="Profiler"></a> So erstellen Sie Arbeitsauslastungen für Ablaufverfolgungsdateien und -tabellen  
  
1.  Starten Sie [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] mithilfe einer der folgenden Methoden:  
  
    -   Zeigen Sie im Menü **Start** auf **Alle Programme**, **Microsoft SQL Server**, **Leistungstools**, und klicken Sie dann auf **SQL Server Profiler**.  
  
    -   Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]auf das Menü **Extras** , und klicken Sie dann auf **SQL Server Profiler**.  
  
2.  Erstellen Sie eine Ablaufverfolgungsdatei oder -tabelle mithilfe der [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Tuning** , wie in den folgenden schrittweisen Anleitungen beschrieben:  
  
    -   [Erstellen einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
    -   [Speichern von Ablaufverfolgungsergebnissen in einer Datei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
         Der Datenbankoptimierungsratgeber setzt voraus, dass die Ablaufverfolgungsdatei für die Arbeitsauslastung eine Rolloverdatei ist. Weitere Informationen zu Rolloverdateien finden Sie unter [Limit Trace File and Table Sizes](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md).  
  
    -   [Speichern von Ablaufverfolgungsergebnissen in einer Tabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
         Stellen Sie sicher, dass die Ablaufverfolgung beendet wurde, bevor Sie eine Ablaufverfolgungstabelle als Arbeitsauslastung verwenden.  
  
 Die Verwendung der Optimierungsvorlage von SQL Server Profiler zum Aufzeichnen von Arbeitsauslastungen für den Datenbankoptimierungsratgeber wird empfohlen.  
  
 Wenn Sie Ihre eigene Vorlage verwenden möchten, stellen Sie sicher, dass die folgenden Ablaufverfolgungsereignisse aufgezeichnet werden:  
  
-   **RPC:Completed**  
  
-   **SQL:BatchCompleted**  
  
-   **SP:StmtCompleted**  
  
 Sie können auch die **Starting** -Versionen dieser Ablaufverfolgungsereignisse verwenden. Zum Beispiel **SQL:BatchStarting**. Jedoch beinhalten die **Completed** -Versionen dieser Ablaufverfolgungsereignisse die **Duration** -Spalte, die es dem Datenbankoptimierungsratgeber ermöglichen, die Arbeitsauslastung effizienter zu optimieren. Der Datenbankoptimierungsratgeber optimiert keine anderen Arten von Ablaufverfolgungsereignissen. Weitere Informationen zu diesen Ablaufverfolgungsereignissen finden Sie unter [Stored Procedures Event Category](../../relational-databases/event-classes/stored-procedures-event-category.md) und [TSQL Event Category](../../relational-databases/event-classes/tsql-event-category.md). Informationen zum Verwenden der gespeicherten Prozeduren der SQL-Ablaufverfolgung zum Erstellen einer Arbeitsauslastung der Ablaufverfolgungsdatei finden Sie unter [Erstellen einer Ablaufverfolgung &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
### <a name="trace-file-or-trace-table-workloads-that-contain-the-loginname-data-column"></a>Ablaufverfolgungsdatei- oder Ablaufverfolgungstabellen-Arbeitsauslastungen, die die LoginName-Datenspalte enthalten  
 Der Datenbankoptimierungsratgeber übermittelt im Rahmen des Optimierungsprozesses Showplan-Anforderungen. Wenn eine Ablaufverfolgungstabelle oder -datei, die die **LoginName** -Datenspalte enthält, als Arbeitsauslastung verbraucht wird, nimmt der Datenbankoptimierungsratgeber die Identität des in **LoginName**angegebenen Benutzers an. Wenn dieser Benutzer keine SHOWPLAN-Berechtigung besitzt (über die der Benutzer für die in der Ablaufverfolgung enthaltenen Anweisungen Showplans erstellen und ausführen kann), werden diese Anweisungen nicht durch den Datenbankoptimierungsratgeber optimiert.  
  
##### <a name="to-avoid-granting-the-showplan-permission-to-each-user-specified-in-the-loginname-column-of-the-trace"></a>So vermeiden Sie, jedem der in der LoginName-Spalte der Ablaufverfolgung angegebenen Benutzer die SHOWPLAN-Berechtigung erteilen zu müssen  
  
1.  Optimieren Sie eine Ablaufverfolgungsdatei- oder Ablaufverfolgungstabellen-Arbeitsauslastung. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Optimieren einer Datenbank](#Tune) .  
  
2.  Überprüfen Sie das Optimierungsprotokoll auf Anweisungen, die aufgrund von unzureichenden Berechtigungen nicht optimiert wurden. Weitere Informationen finden Sie unter [Anzeigen und Verwenden der Ausgabe des Datenbankoptimierungsratgebers](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md).  
  
3.  Erstellen Sie eine neue Arbeitsauslastung, indem Sie die **LoginName** -Spalte der nicht optimierten Ereignisse löschen und anschließend nur die nicht optimierten Ereignisse in einer neuen Ablaufverfolgungsdatei oder -tabelle speichern. Weitere Informationen zum Löschen von Datenspalten aus einer Ablaufverfolgung finden Sie unter [Angeben von Ereignissen und Datenspalten für eine Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md) und [Ändern einer vorhandenen Ablaufverfolgung &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md).  
  
4.  Übermitteln Sie die neue Arbeitsauslastung ohne die **LoginName** -Spalte an den Datenbankoptimierungsratgeber.  
  
 Der Datenbankoptimierungsratgeber optimiert nun die neue Arbeitsauslastung, da in der Ablaufverfolgung keine Anmeldeinformationen angegeben sind. Wenn **LoginName** für eine Anweisung nicht vorhanden ist, optimiert der Datenbankoptimierungsratgeber diese Anweisung, indem er die Identität des Benutzers annimmt, der die Optimierungssitzung gestartet hat (ein Mitglied der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** ).  
  
##  <a name="Tune"></a> Optimieren einer Datenbank  
 Optimieren Sie eine Datenbank mithilfe der GUI des Datenbankoptimierungsratgebers oder des Hilfsprogramms **dta** .  
  
> [!NOTE]  
>  Stellen Sie sicher, dass die Ablaufverfolgung beendet wurde, bevor Sie eine Ablaufverfolgungstabelle als Arbeitsauslastung für den Datenbankoptimierungsratgeber verwenden. Der Datenbankoptimierungsratgeber kann keine Ablaufverfolgungstabelle als Arbeitsauslastung verwenden, in die noch Ablaufverfolgungsereignisse geschrieben werden.  
  
### <a name="use-the-database-engine-tuning-advisor-graphical-user-interface"></a>Verwenden der grafischen Benutzeroberfläche des Datenbankoptimierungsratgebers  
 Auf der grafischen Benutzeroberfläche des Datenbankoptimierungsratgebers können Sie eine Datenbank mithilfe des Plancache oder mithilfe von Arbeitsauslastungsdateien oder -tabellen optimieren Mit der grafischen Benutzeroberfläche des Datenbankoptimierungsratgebers können Sie die Ergebnisse Ihrer aktuellen Optimierungssitzung und die Ergebnisse voriger Optimierungssitzungen mühelos anzeigen. Weitere Informationen zu den Benutzeroberflächenoptionen finden Sie später in diesem Thema unter [Benutzeroberflächenbeschreibungen](#UI) . Weitere Informationen zum Arbeiten mit den Ergebnissen nach dem Optimieren einer Datenbank finden Sie unter [Anzeigen und Verwenden der Ausgabe des Datenbankoptimierungsratgebers](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md).  

####  <a name="PlanCache"></a> So optimieren Sie eine Datenbank mit dem Abfragespeicher
Weitere Informationen finden Sie unter [Tuning Database Using Workload from Query Store (Datenbankoptimierung mithilfe der Arbeitsauslastung aus dem Abfragespeicher)](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md).
  
####  <a name="PlanCache"></a> So optimieren Sie eine Datenbank mit dem Plancache  
  
1.  Starten Sie den Datenbankoptimierungsratgeber, und melden Sie sich bei einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]an. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Starten des Datenbankoptimierungsratgebers](#Start) .  
  
2.  Geben Sie auf der Registerkarte **Allgemein** einen Namen in **Sitzungsname** ein, um eine neue Optimierungssitzung zu erstellen. Bevor Sie eine Optimierungssitzung starten können, müssen Sie die Felder auf der Registerkarte **Allgemein** konfigurieren. Eine Änderung der Einstellungen auf der Registerkarte **Optimierungsoptionen** ist vor dem Starten einer Optimierungssitzung nicht erforderlich.  
  
3.  Wählen Sie **Plancache** als Arbeitsauslastungsoption aus. Der Datenbankoptimierungsratgeber wählt die obersten 1.000 Ereignisse aus dem für die Analyse zu verwendenden Plancache aus.  
  
4.  Wählen Sie die zu optimierenden Datenbanken aus, und wählen Sie optional unter **Ausgewählte Tabellen**eine oder mehrere Tabellen aus jeder Datenbank aus. Klicken Sie zum Einschließen von Cacheeinträgen für alle Datenbanken unter **Optimierungsoptionen**auf **Erweiterte Optionen** , und aktivieren Sie dann **Plancacheereignisse aus allen Datenbanken einschließen**.  
  
5.  Aktivieren Sie die Option **Optimierungsprotokoll speichern** , um eine Kopie des Optimierungsprotokolls zu speichern. Deaktivieren Sie das Kontrollkästchen, wenn Sie keine Kopie des Optimierungsprotokolls speichern möchten.  
  
     Nach der Analyse können Sie das Optimierungsprotokoll anzeigen, indem Sie die Sitzung öffnen und die Registerkarte **Status** auswählen.  
  
6.  Klicken Sie auf die Registerkarte **Optimierungsoptionen** , und wählen Sie eine der aufgeführten Optionen aus.  
  
7.  Klicken Sie auf **Analyse starten**.  
  
     Wenn Sie die Optimierungssitzung nach dem Start anhalten möchten, wählen Sie eine der folgenden Optionen aus dem Menü **Aktionen** aus:  
  
    -   **Analyse beenden (mit Empfehlungen)** beendet die Optimierungssitzung und fragt, ob Sie möchten, dass der Datenbankoptimierungsratgeber auf der Basis der bisher ausgeführten Analyse Empfehlungen generiert.  
  
    -   **Analyse beenden** beendet die Optimierungssitzung ohne Erstellung von Empfehlungen.  
  
> [!NOTE]  
>  Das Anhalten des Datenbankoptimierungsratgebers wird nicht unterstützt. Wenn Sie auf die Symbolleistenschaltfläche **Analyse starten** klicken, nachdem Sie auf eine der beiden Symbolleistenschaltflächen **Analyse beenden** oder **Analyse beenden (mit Empfehlungen)** geklickt haben, startet der Datenbankoptimierungsratgeber eine neue Optimierungssitzung.  
  
##### <a name="to-tune-a-database-using-a-workload-file-or-table-as-input"></a>So optimieren Sie eine Datenbank mithilfe einer Arbeitsauslastungsdatei oder -tabelle als Eingabe  
  
1.  Legen Sie die Datenbankfunktionen (Indizes, indizierte Sichten, Partitionierung) fest, die während der Analyse vom Datenbankoptimierungsratgeber hinzugefügt, entfernt oder beibehalten werden sollen.  
  
2.  Erstellen Sie eine Arbeitsauslastung. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Erstellen einer Arbeitsauslastung](#Create) .  
  
3.  Starten Sie den Datenbankoptimierungsratgeber, und melden Sie sich bei einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]an. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Starten des Datenbankoptimierungsratgebers](#Start) .  
  
4.  Geben Sie auf der Registerkarte **Allgemein** einen Namen in **Sitzungsname** ein, um eine neue Optimierungssitzung zu erstellen.  
  
5.  Wählen Sie entweder eine **Arbeitsauslastungsdatei** oder eine **Tabelle** aus, und geben Sie den Dateipfad bzw. den Namen der Tabelle in das daneben stehende Textfeld ein.  
  
     Das Format für die Angabe einer Tabelle lautet wie folgt:  
  
    ```  
  
    database_name.schema_name.table_name  
    ```  
  
     Klicken Sie auf **Durchsuchen**, um nach einer Arbeitsauslastungsdatei oder -tabelle zu suchen. Der Datenbankoptimierungsratgeber geht davon aus, dass es sich bei allen Arbeitsauslastungsdateien um Rolloverdateien handelt. Weitere Informationen zu Rolloverdateien finden Sie unter [Limit Trace File and Table Sizes](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md).  
  
     Wenn Sie eine Ablaufverfolgungstabelle als Arbeitsauslastung verwenden, muss die betreffende Tabelle auf dem Server vorhanden sein, der mit dem Datenbankoptimierungsratgeber optimiert wird. Wenn Sie die Ablaufverfolgungstabelle auf einem anderen Server erstellen, verschieben Sie sie auf den Server, der mit dem Datenbankmodul-Optimierungsratgeber optimiert wird, bevor Sie sie als Arbeitsauslastung verwenden.  
  
6.  Wählen Sie die Datenbanken und Tabellen aus, mit denen Sie die in Schritt 5 ausgewählte Arbeitsauslastung ausführen möchten. Klicken Sie zum Auswählen der Tabellen auf den Pfeil **Ausgewählte Tabellen** .  
  
7.  Aktivieren Sie die Option **Optimierungsprotokoll speichern** , um eine Kopie des Optimierungsprotokolls zu speichern. Deaktivieren Sie das Kontrollkästchen, wenn Sie keine Kopie des Optimierungsprotokolls speichern möchten.  
  
     Nach der Analyse können Sie das Optimierungsprotokoll anzeigen, indem Sie die Sitzung öffnen und die Registerkarte **Status** auswählen.  
  
8.  Klicken Sie auf die Registerkarte **Optimierungsoptionen** , und wählen Sie eine der aufgeführten Optionen aus.  
  
9. Klicken Sie auf der Symbolleiste auf **Analyse starten** .  
  
     Wenn Sie die Optimierungssitzung nach dem Start anhalten möchten, wählen Sie eine der folgenden Optionen aus dem Menü **Aktionen** aus:  
  
    -   **Analyse beenden (mit Empfehlungen)** beendet die Optimierungssitzung und fragt, ob Sie möchten, dass der Datenbankoptimierungsratgeber auf der Basis der bisher ausgeführten Analyse Empfehlungen generiert.  
  
    -   **Analyse beenden** beendet die Optimierungssitzung ohne Erstellung von Empfehlungen.  
  
> [!NOTE]  
>  Das Anhalten des Datenbankoptimierungsratgebers wird nicht unterstützt. Wenn Sie auf die Symbolleistenschaltfläche **Analyse starten** klicken, nachdem Sie auf eine der beiden Symbolleistenschaltflächen **Analyse beenden** oder **Analyse beenden (mit Empfehlungen)** geklickt haben, startet der Datenbankoptimierungsratgeber eine neue Optimierungssitzung.  
  
###  <a name="dta"></a> Verwenden des dta-Hilfsprogramms  
 Das Hilfsprogramm [dta](../../tools/dta/dta-utility.md) stellt eine ausführbare Datei für Eingabeaufforderungen zur Verfügung, mit der Datenbanken optimiert werden können. Sie können auf diese Weise den Datenbankoptimierungsratgeber in Batchdateien und Skripts verwenden. Das Hilfsprogramm **dta** akzeptiert Plancacheeinträge, Ablaufverfolgungsdateien und -tabellen sowie [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts als Arbeitsauslastung. Außerdem akzeptiert es XML-Eingaben, die dem XML-Schema des Datenbankoptimierungsratgebers entsprechen. Dieses Schema steht auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?linkid=43100)zur Verfügung.  
  
 Beachten Sie Folgendes, bevor Sie eine Arbeitsauslastung mit dem Hilfsprogramm **dta** optimieren:  
  
-   Wenn Sie eine Ablaufverfolgungstabelle als Arbeitsauslastung verwenden, muss die betreffende Tabelle auf dem Server vorhanden sein, der mit dem Datenbankoptimierungsratgeber optimiert wird. Wenn die Ablaufverfolgungstabelle auf einem anderen Server erstellt wird, muss sie anschließend auf den Server verschoben werden, auf dem die Optimierung durch den Datenbankoptimierungsratgeber vorgenommen wird.  
  
-   Stellen Sie sicher, dass die Ablaufverfolgung beendet wurde, bevor Sie eine Ablaufverfolgungstabelle als Arbeitsauslastung für den Datenbankoptimierungsratgeber verwenden. Der Datenbankoptimierungsratgeber kann keine Ablaufverfolgungstabelle als Arbeitsauslastung verwenden, in die noch Ablaufverfolgungsereignisse geschrieben werden.  
  
-   Wenn eine Optimierungssitzung länger als erwartet ausgeführt wird, können Sie die Sitzung durch Drücken der Tastenkombination STRG+C beenden und auf der Grundlage der bis zu diesem Zeitpunkt von **dta** abgeschlossenen Analyse Empfehlungen generieren. Daraufhin werden Sie aufgefordert zu entscheiden, ob Sie Empfehlungen generieren möchten. Drücken Sie erneut STRG+C, um die Optimierungssitzung zu beenden, ohne Empfehlungen zu generieren.  
  
 Weitere Informationen zur Syntax des Hilfsprogramms **dta** sowie Beispiele finden Sie unter [dta Utility](../../tools/dta/dta-utility.md).  
  
##### <a name="to-tune-a-database-by-using-the-plan-cache"></a>So optimieren Sie eine Datenbank mit dem Plancache  
  
1.  Geben Sie die Option **-ip** an. Die obersten 1.000 Plancacheereignisse für die ausgewählten Datenbanken werden analysiert.  
  
     Geben Sie an einer Eingabeaufforderung folgenden Befehl ein:  
  
    ```  
    dta -E -D DatabaseName -ip -s SessionName  
    ```  
  
2.  Geben Sie zum Ändern der Anzahl der für die Analyse zu verwendenden Ereignisse die Option **–n** an. Im folgenden Beispiel wird die Anzahl der Cacheeinträge auf 2.000 erhöht.  
  
    ```  
    dta -E -D DatabaseName -ip –n 2000-s SessionName1  
    ```  
  
3.  Geben Sie zum Analysieren der Ereignisse aller Datenbanken in der Instanz die Option **-ipf** an.  
  
    ```  
    dta -E -D DatabaseName -ip –ipf –n 2000 -s SessionName2  
    ```  
  
##### <a name="to-tune-a-database-by-using-a-workload-and-dta-utility-default-settings"></a>So optimieren Sie eine Datenbank mithilfe einer Arbeitsauslastung und den Standardeinstellungen des dta-Hilfsprogramms  
  
1.  Legen Sie die Datenbankfunktionen (Indizes, indizierte Sichten, Partitionierung) fest, die während der Analyse vom Datenbankoptimierungsratgeber hinzugefügt, entfernt oder beibehalten werden sollen.  
  
2.  Erstellen Sie eine Arbeitsauslastung. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Erstellen einer Arbeitsauslastung](#Create) .  
  
3.  Geben Sie an einer Eingabeaufforderung folgenden Befehl ein:  
  
    ```  
    dta -E -D DatabaseName -if WorkloadFile -s SessionName  
    ```  
  
     Dabei gibt `-E` an, dass die Optimierungssitzung eine vertrauenswürdige Verbindung (anstelle von Benutzernamen und Kennwort) verwendet. Und `-D` gibt den Namen der zu optimierenden Datenbank an. Standardmäßig stellt das Hilfsprogramm eine Verbindung zur Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem lokalen Computer her. (Verwenden Sie die Option `-S`, um eine Remotedatenbank laut dem folgenden Verfahren oder eine benannte Instanz anzugeben.) Die Option `-if` gibt den Namen und Pfad zu einer Arbeitsauslastungsdatei an (wobei es sich um ein [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skript oder um eine Ablaufverfolgungsdatei handeln kann), während `-s` einen Namen für die Optimierungssitzung angibt.  
  
     Die vier hier gezeigten Optionen (Datenbankname, Arbeitsauslastung, Verbindungstyp und Sitzungsname) müssen angegeben werden.  
  
##### <a name="to-tune-a-remote-database-or-a-named-instance-for-a-specific-duration"></a>So optimieren Sie eine Remotedatenbank oder eine benannte Instanz für eine bestimmte Dauer  
  
1.  Legen Sie die Datenbankfunktionen (Indizes, indizierte Sichten, Partitionierung) fest, die während der Analyse vom Datenbankoptimierungsratgeber hinzugefügt, entfernt oder beibehalten werden sollen.  
  
2.  Erstellen Sie eine Arbeitsauslastung. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Erstellen einer Arbeitsauslastung](#Create) .  
  
3.  Geben Sie an einer Eingabeaufforderung folgenden Befehl ein:  
  
    ```  
    dta -S ServerName\Instance -D DatabaseName -it WorkloadTableName   
    -U LoginID -P Password -s SessionName -A TuningTimeInMinutes  
    ```  
  
     Dabei gibt `-S` den Namen und die Instanz eines Remoteservers an (oder eine benannte Instanz auf dem lokalen Server), während `-D` den Namen der zu optimierenden Datenbank angibt. Die Option `-it` gibt den Namen der Arbeitsauslastungstabelle an, `-U` und `-P` geben den Benutzernamen und das Kennwort für die Remotedatenbank an, `-s` gibt den Namen der Optimierungssitzung an, und `-A` gibt die Dauer der Optimierungssitzung in Minuten an. Standardmäßig verwendet das Hilfsprogramm **dta** eine Optimierungsdauer von 8 Stunden. Wenn der Datenbankoptimierungsratgeber eine Arbeitsauslastung für einen unbegrenzten Zeitraum optimieren soll, geben Sie **0** (Null) mit der Option `-A` an.  
  
##### <a name="to-tune-a-database-using-an-xml-input-file"></a>So optimieren Sie eine Datenbank mithilfe einer XML-Eingabedatei  
  
1.  Legen Sie die Datenbankfunktionen (Indizes, indizierte Sichten, Partitionierung) fest, die während der Analyse vom Datenbankoptimierungsratgeber hinzugefügt, entfernt oder beibehalten werden sollen.  
  
2.  Erstellen Sie eine Arbeitsauslastung. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Erstellen einer Arbeitsauslastung](#Create) .  
  
3.  Erstellen Sie eine XML-Eingabedatei. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Erstellen von XML-Eingabedateien](#XMLInput) .  
  
4.  Geben Sie an einer Eingabeaufforderung folgenden Befehl ein:  
  
    ```  
    dta -E -S ServerName\Instance -s SessionName -ix PathToXMLInputFile  
    ```  
  
     Dabei gibt `-E` eine vertrauenswürdige Verbindung an, `-S` gibt einen Remoteserver und eine Instanz an bzw. eine benannte Instanz auf dem lokalen Server, `-s` gibt den Namen einer Optimierungssitzung an, und `-ix` gibt die XML-Eingabedatei an, die für diese Optimierungssitzung verwendet werden soll.  
  
5.  Wenn das Hilfsprogramm die Optimierung der Arbeitsauslastung abgeschlossen hat, können Sie die Ergebnisse von Optimierungssitzungen über die grafische Benutzeroberfläche des Datenbankoptimierungsratgebers anzeigen. Alternativ können Sie über die Option **-ox** auch angeben, dass die Optimierungsempfehlungen in eine XML-Datei geschrieben werden sollen. Weitere Informationen finden Sie unter [dta Utility](../../tools/dta/dta-utility.md).  
  
##  <a name="XMLInput"></a> Erstellen einer XML-Eingabedatei  
 Wenn Sie mit der XML-Entwicklung bereits gut vertraut sind, können Sie XML-Formatdateien erstellen, mit denen der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber Arbeitsauslastungen optimieren kann. Um diese XML-Dateien zu erstellen, verwenden Sie Ihre bevorzugten XML-Tools, und bearbeiten Sie eine Beispieldatei, oder generieren Sie eine Instanz des XML-Schemas für den [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber.  
  
 Das XML-Schema für den [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber ist in Ihrer Installation von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an folgendem Speicherort verfügbar:  
  
 C:\Programme\Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd  
  
 Das XML-Schema des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgebers ist auch online auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)verfügbar.  
  
 Diese URL öffnet eine Seite, auf der viele [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -XML-Schemas verfügbar sind. Führen Sie auf der Seite einen Bildlauf nach unten aus, bis Sie die Zeile für den [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber erreichen.  
  
#### <a name="to-create-an-xml-input-file-to-tune-workloads"></a>So erstellen Sie eine XML-Eingabedatei zum Optimieren von Arbeitsauslastungen  
  
1.  Erstellen Sie eine Arbeitsauslastung. Sie können eine Ablaufverfolgungsdatei oder -tabelle mithilfe der Optimierungsvorlage in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]verwenden, oder erstellen Sie ein [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript, das eine repräsentative Arbeitsauslastung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]reproduziert. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Erstellen einer Arbeitsauslastung](#Create) .  
  
2.  Erstellen Sie mithilfe einer der folgenden Methoden eine XML-Eingabedatei:  
  
    -   Kopieren Sie eines der [Beispiele für XML-Eingabedateien &#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md), und fügen Sie es in Ihren bevorzugten XML-Editor ein. Ändern Sie die Werte, um die entsprechenden Argumente für Ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation anzugeben, und speichern Sie die XML-Datei.  
  
    -   Generieren Sie mithilfe Ihres bevorzugten XML-Tools eine Instanz vom XML-Schema für den [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber.  
  
3.  Nachdem Sie die XML-Eingabedatei erstellt haben, verwenden Sie diese als Eingabe für das Befehlszeilen-Hilfsprogramm **dta** , um die Arbeitsauslastung zu optimieren. Informationen zum Verwenden von XML-Eingabedateien mit diesem Hilfsprogramm finden Sie weiter oben in diesem Thema unter [Verwenden des Hilfsprogramms dta](#dta) .  
  
> [!NOTE]  
>  Wenn Sie eine Inlinearbeitsauslastung verwenden möchten (d.h. eine Arbeitsauslastung, die direkt in der XML-Eingabedatei angegeben wird), verwenden Sie das [Beispiel für eine XML-Eingabedatei mit Inlinearbeitsauslastung &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
##  <a name="UI"></a> Benutzeroberflächenbeschreibungen  
  
### <a name="tools-menuoptions-page"></a>Extras (Menü)/Optionen (Seite)  
 Mit diesem Dialogfeld können Sie allgemeine Konfigurationsparameter für den Datenbankoptimierungsratgeber angeben.  
  
 **Beim Start**  
 Gibt an, welche Aktion der Datenbankoptimierungsratgeber beim Starten ausführen soll: ohne Datenbankverbindung öffnen, ein Dialogfeld **Neue Verbindung** anzeigen, eine neue Sitzung anzeigen oder die zuletzt geladene Sitzung laden.  
  
 **Schriftart ändern**  
 Gibt die Bildschirm-Schriftart an, die von den Tabellen des Datenbankoptimierungsratgebers verwendet werden.  
  
 **Anzahl der Elemente in der Liste zuletzt verwendeter Objekte**  
 Gibt die Anzahl der Sitzungen oder Dateien an, die im Menü **Datei** unter **Zuletzt geöffnete Sitzungen** oder **Zuletzt geöffnete Dateien** angezeigt werden sollen.  
  
 **Die letzten Optimierungsoptionen speichern**  
 Behält die Optimierungsoptionen zwischen Sitzungen bei. Standardmäßig ausgewählt. Deaktivieren Sie dieses Kontrollkästchen, wenn beim Start immer die Standardeinstellungen des Datenbankoptimierungsratgebers verwendet werden sollen.  
  
 **Dauerhaftes Löschen von Sitzungen bestätigen**  
 Zeigt vor dem Löschen von Sitzungen ein Bestätigungsdialogfeld an.  
  
 **Vor dem Beenden der Sitzungsanalyse fragen**  
 Zeigt vor dem Beenden der Analyse einer Arbeitsauslastung ein Bestätigungsdialogfeld an.  
  
#### <a name="general-tab-options"></a>Allgemeine Optionen (Registerkarte)  
 Bevor Sie eine Optimierungssitzung starten können, müssen Sie die Felder auf der Registerkarte **Allgemein** konfigurieren. Eine Änderung der Einstellungen auf der Registerkarte **Optimierungsoptionen** ist vor dem Starten einer Optimierungssitzung nicht erforderlich.  
  
 **Sitzungsname**  
 Geben Sie einen Namen für die Sitzung an. Der Sitzungsname weist einer Optimierungssitzung einen Namen zu. Anhand dieses Namens können Sie die Optimierungssitzung später überprüfen.  
  
 **Zuletzt geöffnete Dateien**  
 Geben Sie eine SQL-Skript- oder Ablaufverfolgungsdatei für eine Arbeitsauslastung an. Geben Sie Pfad und Dateinamen im zugehörigen Textfeld an. Der Datenbankoptimierungsratgeber setzt voraus, dass die Ablaufverfolgungsdatei für die Arbeitsauslastung eine Rolloverdatei ist. Weitere Informationen zu Rolloverdateien finden Sie unter [Limit Trace File and Table Sizes](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md).  
  
 **Tabelle**  
 Geben Sie eine Ablaufverfolgungstabelle für die Arbeitsauslastung an. Geben Sie den voll gekennzeichneten Namen der Ablaufverfolgungstabelle folgendermaßen in das zugehörige Textfeld ein:  
  
```  
database_name.owner_name.table_name  
```  
  
-   Stellen Sie sicher, dass die Ablaufverfolgung beendet wurde, bevor Sie eine Ablaufverfolgungstabelle als Arbeitsauslastung verwenden.  
  
-   Die Ablaufverfolgungstabelle muss auf demselben Server vorhanden sein, auf dem der Datenbankoptimierungsratgeber die Optimierung ausführt. Wenn die Ablaufverfolgungstabelle auf einem anderen Server erstellt wird, muss sie anschließend auf den Server verschoben werden, auf dem die Optimierung durch den Datenbankoptimierungsratgeber vorgenommen wird.  
  
 **Plancache**  
 Geben Sie den Plancache als Arbeitsauslastung an. Dadurch können Sie die manuelle Erstellung einer Auslastung vermeiden. Der Datenbankoptimierungsratgeber wählt die obersten 1.000 Ereignisse aus, die für die Analyse verwendet werden sollen.  
  
 **Xml**  
 Wird erst angezeigt, wenn Sie eine Arbeitsauslastungsabfrage aus [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]importieren.  
  
 So importieren Sie eine Arbeitsauslastungsabfrage aus [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
1.  Geben Sie eine Abfrage in den Abfrage-Editor ein, und markieren Sie sie.  
  
2.  Klicken Sie mit der rechten Maustaste auf die markierte Abfrage, und klicken Sie auf **Abfrage mit dem Datenbankoptimierungsratgeber analysieren**.  
  
 **Suchen Sie nach einer Arbeitsauslastungsdatei/Suchen Sie nach einer Arbeitsauslastungstabelle**  
 Wenn Sie als Arbeitsauslastungsquelle **Datei** oder **Tabelle** ausgewählt haben, können Sie mithilfe dieser Schaltfläche zum Durchsuchen das gewünschte Ziel auswählen.  
  
 **Zeigen Sie eine Vorschau der XML-Arbeitsauslastung an**  
 Zeigt eine aus [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]importierte, XML-formatierte Arbeitsauslastung an.  
  
 **Datenbank für Arbeitsauslastungsanalyse**  
 Geben Sie die erste Datenbank an, mit der der Datenbankoptimierungsratgeber beim Optimieren einer Arbeitsauslastung eine Verbindung herstellt. Nach dem Beginn der Optimierung stellt der Datenbankoptimierungsratgeber Verbindungen mit den Datenbanken her, die über die `USE DATABASE` -Anweisungen in der Arbeitsauslastung angegeben sind.  
  
 **Zu optimierende Datenbanken und Tabellen auswählen**  
 Geben Sie die zu optimierenden Datenbanken und Tabellen an. Um alle Datenbanken anzugeben, aktivieren Sie das Kontrollkästchen in der Spaltenüberschrift **Name** . Zur Angabe bestimmter Datenbanken aktivieren Sie jeweils das Kontrollkästchen neben dem Datenbanknamen. Standardmäßig werden alle Tabellen der ausgewählten Datenbanken bei der Optimierungssitzung automatisch berücksichtigt. Um Tabellen auszuschließen, klicken Sie auf den Pfeil in der Spalte **Ausgewählte Tabellen** , und deaktivieren Sie dann die Kontrollkästchen neben den Tabellen, die nicht optimiert werden sollen.  
  
 **Ausgewählte Tabellen** (Pfeil nach unten)  
 Erweitern Sie die Tabellenliste, um die Auswahl einzelner zu optimierender Tabellen zu ermöglichen.  
  
 **Optimierungsprotokoll speichern**  
 Erstellen Sie ein Protokoll, und zeichnen Sie die während der Sitzung auftretenden Fehler auf.  
  
> [!NOTE]  
>  Der Datenbankoptimierungsratgeber aktualisiert die Zeileninformationen für die auf der Registerkarte **Allgemein** angezeigten Tabellen nicht automatisch. Er verlässt sich stattdessen auf die Metadaten in der Datenbank. Wenn Sie vermuten, dass die Zeileninformationen veraltet sind, können Sie für die entsprechenden Objekte den Befehl DBCC UPDATEUSAGE ausführen.  
  
##### <a name="tuning-tab-options"></a>Optimierungsoptionen (Registerkarte)  
 Auf der Registerkarte **Optimierungsoptionen** werden die Standardeinstellungen der allgemeinen Optimierungsoptionen geändert. Eine Änderung der Einstellungen auf der Registerkarte **Optimierungsoptionen** ist vor dem Starten einer Optimierungssitzung nicht erforderlich.  
  
 **Optimierungszeit begrenzen**  
 Begrenzt die Dauer der aktuellen Optimierungssitzung. Wenn der Optimierung mehr Zeit eingeräumt wird, erhöht sich die Qualität der Empfehlungen. Um bestmögliche Empfehlungen zu erhalten, sollte diese Option nicht ausgewählt werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber beansprucht während der Analyse die Systemressourcen. Um die Optimierung vor dem Beginn von Zeiträumen mit erwartungsgemäß hoher Arbeitsauslastung auf dem optimierten Server zu beenden, verwenden Sie **Optimierungszeit begrenzen** .  
  
 **Erweiterte Optionen**  
 Mithilfe des Dialogfelds **Erweiterte Optimierungsoptionen** können Sie den maximalen Speicherplatz, die maximale Anzahl an Schlüsselspalten sowie Onlineindexempfehlungen konfigurieren.  
  
 **Max. Speicherplatz für Empfehlungen definieren (MB)**  
 Geben Sie die maximale Größe des Speicherplatzes ein, der den Empfehlungen des Datenbankoptimierungsratgebers entsprechend für physische Entwurfsstrukturen verwendet werden darf.  
  
 Wenn an dieser Stelle kein Wert eingegeben wird, nimmt der Datenbankoptimierungsratgeber die kleinere der folgenden Beschränkungen des Speicherplatzes an:  
  
-   Das Dreifache der aktuellen Rohdatengröße, einschließlich der Gesamtgröße der Heaps und gruppierten Indizes der Tabellen in der Datenbank.  
  
-   Der freie Speicherplatz auf allen angefügten Laufwerken plus die Rohdatengröße.  
  
 **Plancacheereignisse aus allen Datenbanken einschließen**  
 Geben Sie an, dass Plancacheereignisse aus allen Datenbanken analysiert werden.  
  
 **Max. Spaltenanzahl je Index**  
 Geben Sie die maximale Spaltenanzahl an, die in Indizes enthalten sein sollen. Der Standardwert ist 1023.  
  
 **Alle Empfehlungen sind Offlineempfehlungen**  
 Generiert die bestmöglichen Empfehlungen, ohne zu empfehlen, dass physische Entwurfsstrukturen online erstellt werden sollen.  
  
 **Sofern möglich, Onlineempfehlungen generieren**  
 Wählt beim Erstellen von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen zum Implementieren der Empfehlungen Methoden aus, die implementiert werden können, während der Server online ist. Diese Auswahl wird auch getroffen, wenn eine schnellere Offline-Methode verfügbar ist.  
  
 **Nur Onlineempfehlungen generieren**  
 Gibt nur Empfehlungen, bei denen der Server online bleiben kann.  
  
 **Beenden am**  
 Gibt das Datum und die Uhrzeit des Zeitpunkts an, zu dem der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber beendet werden soll.  
  
 **Indizes und indizierte Sichten**  
 Aktivieren Sie dieses Kontrollkästchen, um zum Hinzufügen von gruppierten Indizes, nicht gruppierten Indizes und indizierten Sichten Empfehlungen einzuschließen.  
  
 **Indizierte Sichten**  
 Empfehlungen werden nur zum Hinzufügen indizierter Sichten eingeschlossen. Für gruppierte und nicht gruppierte Indizes werden keine Empfehlungen gegeben.  
  
 **Gefilterte Indizes einschließen**  
 Enthält Empfehlungen zum Hinzufügen von gefilterten Indizes. Diese Option ist verfügbar, wenn Sie eine dieser physischen Entwurfsstrukturen auswählen: **Indizes und indizierte Sichten**, **Indizes**oder **Nicht gruppierte Indizes**.  
  
 **Indizes**  
 Empfehlungen werden nur zum Hinzufügen gruppierter und nicht gruppierter Indizes eingeschlossen. Für indizierte Sichten werden keine Empfehlungen gegeben.  
  
 **Nicht gruppierte Indizes**  
 Empfehlungen werden nur für nicht gruppierte Indizes eingeschlossen. Für gruppierte Indizes und indizierte Sichten werden keine Empfehlungen gegeben.  
  
 **Nur Auslastung vorhandener physischer Entwurfsstrukturen bewerten**  
 Bewertet die Effizienz der aktuellen Indizes. Für weitere Indizes oder indizierte Sichten werden jedoch keine Empfehlungen gegeben.  
  
 **Keine Partitionierung**  
 Für die Partitionierung werden keine Empfehlungen gegeben.  
  
 **Vollständige Partitionierung**  
 Für die Partitionierung werden Empfehlungen eingeschlossen.  
  
 **Ausgerichtete Partitionierung**  
 Neu empfohlene Partitionen werden so ausgerichtet, dass sie leicht zu warten sind.  
  
 **Keine vorhandenen physischen Entwurfsstrukturen beibehalten**  
 Es werden Empfehlungen für das Verwerfen unnötiger vorhandener Indizes, Sichten und Partitionierungen gegeben. Wenn eine vorhandene physische Entwurfsstruktur für die Arbeitsauslastung nützlich ist, wird vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber nicht empfohlen, diese zu verwerfen.  
  
 **Nur Indizes beibehalten**  
 Behält alle vorhandenen Indizes bei, empfiehlt jedoch, unnötige indizierte Sichten und Partitionierungen zu verwerfen.  
  
 **Alle vorhandenen physischen Entwurfsstrukturen beibehalten**  
 Alle vorhandenen Indizes, indizierten Sichten und Partitionierungen werden beibehalten.  
  
 **Nur gruppierte Indizes beibehalten**  
 Behält alle vorhandenen gruppierten Indizes bei, empfiehlt jedoch, unnötige indizierte Sichten, Partitionierungen und nicht gruppierte Indizes zu verwerfen.  
  
 **Ausgerichtete Partitionierung beibehalten**  
 Aktuell ausgerichtete Partitionierungsstrukturen werden beibehalten, es wird jedoch empfohlen, unnötige indizierte Sichten, Indizes und nicht ausgerichtete Partitionierungen zu verwerfen. Alle zusätzlich empfohlenen Partitionierungen werden am aktuellen Partitionierungsschema ausgerichtet.  
  
###### <a name="progress-tab-options"></a>Status (Optionen der Registerkarte)  
 Die Registerkarte **Status** des Datenbankoptimierungsratgebers wird angezeigt, wenn der Datenbankoptimierungsratgeber mit der Analyse der Arbeitslast begonnen hat.  
  
 Wenn Sie die Optimierungssitzung nach dem Start anhalten möchten, wählen Sie eine der folgenden Optionen aus dem Menü **Aktionen** aus:  
  
-   **Analyse beenden (mit Empfehlungen)** beendet die Optimierungssitzung und fragt, ob Sie möchten, dass der Datenbankoptimierungsratgeber auf der Basis der bisher ausgeführten Analyse Empfehlungen generiert.  
  
-   **Analyse beenden** beendet die Optimierungssitzung ohne Erstellung von Empfehlungen.  
  
 **Optimierungsstatus**  
 Zeigt den aktuellen Status des Optimierungsvorgangs an. Enthält die Anzahl der durchgeführten Aktionen und die Anzahl der erhaltenen Fehler-, Erfolgs- und Warnmeldungen.  
  
 **Details**  
 Enthält ein Symbol, das den Status anzeigt.  
  
 **Aktion**  
 Zeigt die ausgeführten Schritte an.  
  
 **Status**  
 Zeigt den Status des Aktionsschritts an.  
  
 **MessageBox**  
 Enthält alle Meldungen, die von den Aktionsschritten zurückgegeben werden.  
  
 **Optimierungsprotokoll**  
 Enthält Informationen bezüglich dieser Optimierungssitzung. Um dieses Protokoll zu drucken, klicken Sie mit der rechten Maustaste auf das Protokoll, und klicken Sie auf **Drucken**.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Verwenden der Ausgabe des Datenbankoptimierungsratgebers](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [dta Utility](../../tools/dta/dta-utility.md)  
  
  
