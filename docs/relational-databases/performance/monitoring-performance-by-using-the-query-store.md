---
title: "Überwachen der Leistung mit dem Abfragespeicher | Microsoft -Dokumentation"
ms.custom: 
ms.date: 10/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store
- Query Store, described
ms.assetid: e06344a4-22a5-4c67-b6c6-a7060deb5de6
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 29ba7f266a86e53f95668b8bf8ca4ce879bb62f8
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="monitoring-performance-by-using-the-query-store"></a>Leistungsüberwachung mit dem Abfragespeicher
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abfragespeicher bietet Ihnen Einblick in die Auswahl und die Leistung eines Abfrageplans. Er vereinfacht das Beheben von Leistungsproblemen, indem er das schnelle Auffinden von Leistungsabweichungen durch Änderungen an Abfrageplänen ermöglicht. Der Abfragespeicher erfasst automatisch einen Verlauf der Abfragen, Pläne und Laufzeitstatistiken und bewahrt diese zur Überprüfung auf. Es unterteilt die Daten nach Zeitfenstern, sodass Sie Verwendungsmuster für Datenbanken erkennen können und verstehen, wann Abfrageplanänderungen auf dem Server aufgetreten sind. Sie können den Abfragespeicher mit der Option [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) konfigurieren. 
  
 Informationen zum Betrieb des Abfragespeichers in Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)] finden Sie unter [Verwenden des Abfragespeichers in Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/).  
  
##  <a name="Enabling"></a> Aktivieren des Abfragespeichers  
 Der Abfragespeicher ist bei neuen Datenbanken standardmäßig nicht aktiviert.  
  
#### <a name="use-the-query-store-page-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>Verwenden der Seite „Abfragespeicher“ in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf eine Datenbank und anschließend auf **Eigenschaften**.  
  
    > [!NOTE]  
    > Erfordert mindestens Version 16 von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Wählen Sie im Dialogfeld **Datenbankeigenschaften** die Seite **Abfragespeicher** aus.  
  
3.  Wählen Sie im Feld **Betriebsmodus (angefordert)** die Option **Ein**.  
  
#### <a name="use-transact-sql-statements"></a>Verwenden von Transact-SQL-Anweisungen  
  
Mit der **ALTER DATABASE** -Anweisung können Sie den Abfragespeicher aktivieren. Zum Beispiel:  
  
```sql  
ALTER DATABASE AdventureWorks2012 SET QUERY_STORE = ON;  
```  
  
Weitere Syntaxoptionen im Zusammenhang mit dem Abfragespeicher finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
> [!NOTE]  
>  Sie können den Abfragespeicher nicht für die **master** - oder **tempdb** -Datenbank aktivieren.  
 
## <a name="About"></a> Informationen im Abfragespeicher  
 Die Ausführungspläne für eine bestimmte Abfrage in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verändern sich i. Allg. im Laufe der Zeit aufgrund unterschiedlicher Ursachen wie z.B. statischer Änderungen, Schemaänderungen, des Erstellens/Löschens von Indizes usw. Der Prozedurcache (in dem zwischengespeicherte Abfragepläne gespeichert werden) speichert nur den letzten Ausführungsplan. Pläne werden auch bei Speicherplatzknappheit aus dem Plancache entfernt. Aus diesem Grund kann die Problembehandlung bei einer Regression der Abfrageleistung schwierig und zeitaufwendig sein.  
  
 Da der Abfragespeicher mehrere Ausführungspläne pro Abfrage beibehält, kann er über Richtlinien den Abfrageprozessor anweisen, für eine Abfrage einen bestimmten Ausführungsplan zu verwenden. Dies wird als Planerzwingung bezeichnet. Das Erzwingen eines Plans im Abfragespeicher erfolgt ähnlich wie beim Abfragehinweis [USE PLAN](../../t-sql/queries/hints-transact-sql-query.md) , es erfordert jedoch keine Änderung an Benutzeranwendungen. Durch das Erzwingen eines Plans können Sie eine Regression der Abfrageleistung aufgrund einer Änderung des Plans in sehr kurzer Zeit beheben.  

 Durch **Wartestatistiken** erhalten Sie weitere Informationen, die Ihnen bei der Problembehandlung der Leistung in SQL Server helfen können. Lange Zeit waren Wartestatistiken nur auf Instanzebene verfügbar, wodurch es schwierig war, sie der tatsächlichen Abfrage zuzuordnen. In SQL Server 2017 und Azure SQL-Datenbank haben wir eine weitere Dimension im Abfragedatenspeicher hinzugefügt, die Wartestatistiken nachverfolgt. 

 Häufige Szenarios für die Verwendung des Abfragespeichers:  
  
-   Schnelles Auffinden und Beheben von Regressionen der Planleistung durch Erzwingung des vorherigen Abfrageplans Korrigieren von Abfragen, die in der Vergangenheit aufgrund von Änderungen am Ausführungsplan die Leistung vermindert haben  
-   Bestimmen der Ausführungshäufigkeit einer Abfrage in einem festgelegten Zeitraum mit Unterstützung eines DBAs bei der Behandlung von Leistungsproblemen mit Ressourcen  
-   Identifizieren der häufigsten *n* Abfragen (nach Ausführungszeit, Speicherverbrauch usw.) in den letzten *x* Stunden.  
-   Überwachen des Verlaufs von Abfrageplänen für eine bestimmte Abfrage  
-   Analysieren der Verwendungsmuster einer Ressource (CPU, E/A und Arbeitsspeicher) für eine bestimmte Datenbank  
-   Identifizieren Sie Top-N-Abfragen, die auf den Ressourcen warten. 
-   Erhalten Sie Einblick in die Wartedetails einer bestimmten Abfrage oder eines bestimmten Plans.
  
Der Abfragespeicher enthält drei Speicher:
- einen **Planspeicher**, der die Informationen zum Ausführungsplan speichert     
- einen **Speicher für Laufzeitstatistiken**, der die Informationen zum Ausführungsstatistiken speichert    
- einen **Speicher für Wartestatistiken**, der die Informationen zum Wartestatistiken speichert     
 
Die Anzahl der eindeutigen Pläne, die für eine Abfrage gespeichert werden können, wird durch die Konfigurationsoption **max_plans_per_query** begrenzt. Zum Verbessern der Leistung werden diese Informationen asynchron in die Speicher geschrieben. Um die Speicherverwendung zu minimieren, werden die statistischen Daten zur Laufzeitausführung im Speicher für Laufzeitstatistiken über ein festes Zeitintervall aggregiert. Die Informationen in diesen Speichern können durch Abfragen der Katalogsichten für den Abfragespeicher angezeigt werden.  
  
Die folgende Abfrage gibt Informationen über Abfragen und Pläne im Abfragespeicher zurück.  
  
```sql  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
INNER JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
INNER JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
 
##  <a name="Regressed"></a> Verwenden der Funktion „Zurückgestellte Abfragen“  
 Aktualisieren Sie nach der Aktivierung des Abfragespeichers den Datenbankbereich im Objekt-Explorer-Bereich, um den Abschnitt **Abfragespeicher** hinzuzufügen.  
  
 ![Abfragespeicherstruktur im Objekt-Explorer](../../relational-databases/performance/media/objectexplorerquerystore.PNG "Abfragespeicherstruktur im Objekt-Explorer")  
  
 Wählen Sie **Zurückgestellte Abfragen** aus, um den Bereich **Zurückgestellte Abfragen** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]zu öffnen. Im Bereich „Regressed Queries“ werden die Abfragen und Pläne im Abfragespeicher angezeigt. Verwenden Sie die Dropdownfelder oben, um Abfragen anhand verschiedener Kriterien auszuwählen. Wählen Sie einen Plan aus, um die grafische Darstellung des Abfrageplans anzuzeigen. Über verschiedene Schaltflächen können Sie die Quellabfrage anzeigen, einen Abfrageplan erzwingen und die Erzwingung wieder aufheben und die Ansicht aktualisieren.  
  
 ![Zurückgesetzte Abfragen im Objekt-Explorer](../../relational-databases/performance/media/objectexplorerregressedqueries.PNG "Zurückgesetzte Abfragen im Objekt-Explorer")  
  
 Wählen Sie eine Abfrage und einen Plan aus, und klicken Sie anschließend auf **Plan erzwingen**, um einen Plan zu erzwingen. Sie können nur Pläne erzwingen, die mit dem Abfrageplanfeature gespeichert wurden und sich noch im Abfrageplancache befinden.  
##  <a name="Waiting"></a> Suchen von Warteanfragen

Ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CTP 2.0 und [!INCLUDE[ssSDS](../../includes/sssds-md.md)] sind im Abfragespeicher Wartestatistiken pro Abfrage über Zeit verfügbar. Im Abfragespeicher werden Wartetypen in **Wartekategorien** zusammengefasst. Die Zuordnung von Wartekategorien zu Wartetypen finden Sie unter [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md#wait-categories-mapping-table).

**Wartekategorien** fassen mehrere Wartetypen in Buckets zusammen, die sich in ihrer Art ähneln. Verschiedene Wartekategorien erfordern verschiedene Analysen zur Problembehebung. Wartetypen aus der gleichen Kategorien führen jedoch zu sehr ähnlichen Problembehebungsvorgängen. Wenn nun die betroffenen Abfrage in den Wartezuständen bereitgestellt wird, kann ein Großteil der Überprüfungen erfolgreich abgeschlossen werden.

Im folgenden finden Sie einige Beispiele, wie Sie ausführlicheren Einblick in Ihre Workload erhalten, bevor oder nachdem Wartekategorien im Abfragespeicher eingefügt wurden:

|||| 
|-|-|-|  
|Frühere Erfahrung|Neue Erfahrung|Aktion|
|Lange Wartezustände von RESOURCE_SEMAPHORE pro Datenbank|Lange Speicherwartezustände im Abfragespeicher für bestimmte Abfragen|Machen Sie die Abfragen im Abfragespeicher ausfindig, die am meisten Speicher nutzen. Es liegt wahrscheinlich an diesen Abfragen, dass der Fortschritt der betroffen Abfragen verzögert wird. Ziehen Sie in Betracht, den Abfragehinweis „MAX_GRANT_PERCENT“ für diese Abfragen oder für die betroffene Abfrage zu verwenden.|
|Lange Wartezustände von LCK_M_X pro Datenbank|Lange Sperrwartezustände im Abfragespeicher für bestimmte Abfragen|Überprüfen Sie die Abfragetexte der betroffenen Abfragen, und identifizieren Sie die Zielentitäten. Suchen Sie im Abfragespeicher nach anderen Abfragen, die die gleiche Entität modifizieren und die häufig ausgeführt werden bzw. oder eine lange Dauer haben. Nachdem Sie diese Abfragen identifiziert haben, denken Sie darüber nach, die Anwendungslogik zu ändern, um die Parallelität zu verbessern, oder verwenden Sie eine weniger einschränkende Transaktionsisolationsstufe.|
|Lange Wartezustände von PAGEIOLATCH_SH pro Datenbank|Lange Wartezustände der Puffer-E/A im Abfragespeicher für bestimmte Abfragen|Suchen Sie im Abfragespeicher nach Abfragen mit einer hohen Zahl an physische Lesevorgängen. Wenn Sie mit den Abfragen mit langen E/A-Wartezuständen übereinstimmen, denken Sie darüber nach, einen Index auf der zugrunde liegenden Entität einzufügen, damit Suchvorgänge statt Scanvorgängen durchgeführt werden und damit der E/A-Aufwand der Abfragen gesenkt wird.|
|Lange Wartezustände von SOS_SCHEDULER_YIELD pro Datenbank|Lange CPU-Wartezustände im Abfragespeicher für bestimmte Abfragen|Machen Sie die Abfragen im Abfragespeicher ausfindig, die am meisten CPU nutzen. Bestimmen Sie dann, welche dieser Abfragen sowohl eine hohe CPU-Auslastung als auch lange CPU-Wartezustände für die betroffenen Abfragen aufweisen. Konzentrieren Sie sich darauf, diese Abfragen zu optimieren: möglicherweise gibt es eine Planregression oder es fehlt ein Index.|

##  <a name="Options"></a> Konfigurationsoptionen 

Die folgenden Optionen sind zur Konfiguration von Abfragespeicherparametern verfügbar.

*OPERATION_MODE*  
**READ_WRITE** (Standardeinstellung) oder READ_ONLY sind möglich.  
  
*CLEANUP_POLICY (STALE_QUERY_THRESHOLD_DAYS)*  
Konfigurieren Sie das `STALE_QUERY_THRESHOLD_DAYS`-Argument, um die Anzahl der Tage anzugeben, für die Daten im Abfragespeicher beibehalten werden sollen. Der Standardwert ist 30. Für die Basic Edition von [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ist der Standardwert **7** Tage.
  
*DATA_FLUSH_INTERVAL_SECONDS*  
Bestimmt die Häufigkeit, mit der in den Abfragespeicher geschriebene Daten auf Datenträger gespeichert werden. Um die Leistung zu optimieren, werden durch den Abfragespeicher gesammelte Daten asynchron auf den Datenträger geschrieben. Die Häufigkeit, mit der diese asynchrone Übertragung auftritt, wird mit `DATA_FLUSH_INTERVAL_SECONDS` konfiguriert. Der Standardwert ist **900** (15 Minuten).  
  
*MAX_STORAGE_SIZE_MB*  
Konfiguriert die maximale Größe des Abfragespeichers. Wenn die Daten im Abfragespeicher die `MAX_STORAGE_SIZE_MB`-Grenze erreichen, ändert sich der Status des Abfragespeichers automatisch von Lese-/ Schreibzugriff in den schreibgeschützten Modus, und es werden keine neuen Daten mehr erfasst.  Der Standardwert ist 100 MB. Der Standardwert für die Premium Edition von [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] liegt bei **1 GB**, für die Basic Edition von [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] bei **10 MB**.
  
*INTERVAL_LENGTH_MINUTES*  
Bestimmt das Zeitintervall, mit dem statistische Daten zur Laufzeitausführung im Abfragespeicher aggregiert werden. Um die Speicherverwendung zu optimieren, werden die statistischen Daten zur Laufzeitausführung im Speicher für Laufzeitstatistiken über ein festes Zeitintervall aggregiert. Dieses feste Zeitintervall wird mit `INTERVAL_LENGTH_MINUTES` konfiguriert. Der Standardwert lautet **60**. 
  
*SIZE_BASED_CLEANUP_MODE*  
Steuert, ob die Bereinigung automatisch aktiviert wird, wenn sich die Gesamtmenge der Daten der maximalen Größe nähert. **AUTO** (Standardeinstellung) oder OFF sind möglich.  
  
*QUERY_CAPTURE_MODE*  
Gibt an, ob der Abfragespeicher alle oder, ausgehend von der Anzahl der Ausführungen und dem Ressourcenverbrauch, nur relevante Abfragen erfasst, oder ob der Abfragespeicher das Hinzufügen neuer Abfragen beendet und nur aktuelle Abfragen nachverfolgt. **ALL** (alle Abfragen erfassen), AUTO (seltene Abfragen und Abfragen mit minimaler Kompilierungs- und Ausführungsdauer ignorieren) oder NONE (neue Abfragen nicht mehr erfassen) ist möglich. Der Standardwert für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (von [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) ist gleich ALL, während er für Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)] gleich AUTO ist.
  
*MAX_PLANS_PER_QUERY*  
Eine ganze Zahl, die die maximale Anzahl von Plänen darstellt, die für jede Abfrage beibehalten werden. Der Standardwert ist **200**.  
 
*WAIT_STATS_CAPTURE_MODE*  
Steuert, ob der Abfragespeicher Wartestatistikinformationen erfasst. **ON** (Standardeinstellung) oder OFF sind möglich.  
 
Fragen Sie die Sicht **sys.database_query_store_options** ab, um die aktuellen Optionen des Abfragespeichers zu ermitteln. Weitere Informationen zu den Werten finden Sie unter [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md).  
  
Weitere Informationen zum Festlegen der Optionen mit [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen finden Sie unter [Optionsverwaltung](#OptionMgmt).  
  
## <a name="Related"></a> Zugehörige Sichten, Funktionen und Prozeduren  
 Überprüfen und verwalten Sie den Abfragespeicher mit [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oder mithilfe der folgenden Sichten und Prozeduren.  

### <a name="query-store-functions"></a>Funktionen des Abfragespeichers  
 Funktionen unterstützen Sie bei den Vorgängen des Abfragespeichers. 
 
||| 
|-|-|  
|[sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)|| 
  
### <a name="query-store-catalog-views"></a>Katalogsichten des Abfragespeichers  
 Katalogsichten stellen Informationen über den Abfragespeicher bereit.  

||| 
|-|-|  
|[sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)|[sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)|  
|[sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)|[sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)|  
|[sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|[sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)|  
|[sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)|[sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)|  
  
### <a name="query-store-stored-procedures"></a>Gespeicherte Prozeduren für den Abfragespeicher  
 Gespeicherte Prozeduren ermöglichen das Konfigurieren des Abfragespeichers.  

||| 
|-|-|  
|[sp_query_store_flush_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)|[sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)|  
|[sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)|[sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)|  
|[sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)|[sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)|  
 
##  <a name="Scenarios"></a> Wichtige Verwendungsszenarien  
  
###  <a name="OptionMgmt"></a> Optionsverwaltung  
 Dieser Abschnitt enthält einige Richtlinien zum Verwalten des Abfragespeichers selbst.  
  
 **Ist der Abfragespeicher derzeit aktiv?**  
  
 Der Abfragespeicher speichert seine Daten in der Benutzerdatenbank und besitzt aus diesem Grund eine Größenbegrenzung (konfiguriert mit `MAX_STORAGE_SIZE_MB`). Wenn die Daten im Abfragespeicher dieses Limit erreichen, ändert sich der Status automatisch vom Lese-/ Schreibzugriff in den schreibgeschützten Modus, und es werden keine neuen Daten mehr erfasst.  
  
 Fragen Sie [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) ab, um zu ermitteln, ob der Abfragespeicher zurzeit aktiv ist und Laufzeitstatistiken erfasst.  
  
```sql  
SELECT actual_state, actual_state_desc, readonly_reason,   
    current_storage_size_mb, max_storage_size_mb  
FROM sys.database_query_store_options;  
```  
  
 Der Status des Abfragespeichers wird durch die „actual_state“-Spalte bestimmt. Wenn er vom gewünschten Status abweicht, können Sie über die `readonly_reason`-Spalte weitere Informationen erhalten.   
Wenn die Größe des Abfragespeichers das Kontingent überschreitet, wird die Funktion in den „readon_only“-Modus wechseln.  
  
 **Abrufen von Optionen zum Abfragespeicher**  
  
 Führen Sie zum Abrufen detaillierter Informationen zum Status des Abfragespeichers Folgendes in einer Benutzerdatenbank aus.  
  
```sql  
SELECT * FROM sys.database_query_store_options;  
```  
  
 **Festlegen des Abfragespeicherintervalls**  
  
 Sie können das Intervall zum Sammeln von Statistiken zur Abfragelaufzeit  überschreiben (der Standardwert ist 60 Minuten).  
  
```sql  
ALTER DATABASE <database_name>   
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);  
```  
  
 > [!NOTE]
 > Ganzzahlige Werte sind für den Typ `INTERVAL_LENGTH_MINUTES` nicht zulässig. Sie können eine der folgenden Möglichkeiten verwenden: 1, 5, 10, 15, 30, 60 oder 1440 Minuten.  
  
 Der neue Wert für das Intervall wird über die Sicht **sys.database_query_store_options** offen gelegt.  
  
 **Die Speicherplatzverwendung des Abfragespeichers**  
  
 So überprüfen Sie die aktuelle Größe des Abfragespeichers und begrenzen die folgende Anweisung in der Benutzerdatenbank.  
  
```sql  
SELECT current_storage_size_mb, max_storage_size_mb   
FROM sys.database_query_store_options;  
```  
  
 Mit der folgenden Anweisung können Sie den Speicher erweitern, wenn der Abfragespeicher voll ist.  
  
```sql  
ALTER DATABASE <database_name>   
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);  
```  
  
 **Festlegen von Optionen zum Abfragespeicher**  
  
 Sie können mehrere Optionen zum Abfragespeicher gleichzeitig mit einer einzigen ALTER DATABASE-Anweisung festlegen.  
  
```sql  
ALTER DATABASE <database name>   
SET QUERY_STORE (  
    OPERATION_MODE = READ_WRITE,  
    CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30),  
    DATA_FLUSH_INTERVAL_SECONDS = 3000,  
    MAX_STORAGE_SIZE_MB = 500,  
    INTERVAL_LENGTH_MINUTES = 15,  
    SIZE_BASED_CLEANUP_MODE = AUTO,  
    QUERY_CAPTURE_MODE = AUTO,  
    MAX_PLANS_PER_QUERY = 1000,
    WAIT_STATS_CAPTURE_MODE = ON 
);  
```  
  
 **Bereinigen des Speicherplatzes**  
  
 Die internen Tabellen des Abfragespeichers werden beim Erstellen der Datenbank in der PRIMÄREN Dateigruppe erstellt. Diese Konfiguration kann später nicht mehr geändert werden. Wenn nicht mehr genügend Speicherplatz vorhanden ist, sollten Sie mithilfe der folgenden Anweisung ältere Daten aus dem Abfragespeicher löschen.  
  
```sql  
ALTER DATABASE <db_name> SET QUERY_STORE CLEAR;  
```  
  
 Sie können auch nur Ad-hoc-Abfragedaten löschen, da diese evtl. für die Abfrageoptimierung und Plananalyse weniger wichtig sind, aber trotzdem viel Platz einnehmen.  
  
 **Löschen von Ad-hoc-Abfragen** : Hiermit löschen Sie Abfragen, die nur einmal ausgeführt wurden und mehr als 24 Stunden alt sind.  
  
```sql  
DECLARE @id int  
DECLARE adhoc_queries_cursor CURSOR   
FOR   
SELECT q.query_id  
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON q.query_text_id = qt.query_text_id  
JOIN sys.query_store_plan AS p   
    ON p.query_id = q.query_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
GROUP BY q.query_id  
HAVING SUM(rs.count_executions) < 2   
AND MAX(rs.last_execution_time) < DATEADD (hour, -24, GETUTCDATE())  
ORDER BY q.query_id ;  
  
OPEN adhoc_queries_cursor ;  
FETCH NEXT FROM adhoc_queries_cursor INTO @id;  
WHILE @@fetch_status = 0  
    BEGIN   
        PRINT @id  
        EXEC sp_query_store_remove_query @id  
        FETCH NEXT FROM adhoc_queries_cursor INTO @id  
    END   
CLOSE adhoc_queries_cursor ;  
DEALLOCATE adhoc_queries_cursor;  
```  
  
 Sie können eine eigene Prozedur mit abweichender Logik für das Bereinigen von Daten definieren, die Sie nicht mehr benötigen.  
  
 Im Beispiel oben wird die erweiterte gespeicherte Prozedur **sp_query_store_remove_query** verwendet, um nicht benötigte Daten zu entfernen. Sie können auch folgenden Prozeduren verwenden:  
  
-   **sp_query_store_reset_exec_stats**, um Laufzeitstatistiken für einen bestimmten Plan zu löschen.  
-   **sp_query_store_remove_plan**, um einen einzelnen Plan zu entfernen.  
 
  
###  <a name="Peformance"></a> Leistungsüberwachung und Problembehandlung  
 Der Abfragespeicher protokolliert den Verlauf der Kompilierungs- und Laufzeitmetriken während der Abfrageausführungen, sodass Sie Fragen zu Ihrer Arbeitsauslastung stellen können.  
  
 **Welche waren die letzten *n* Abfragen, die für die Datenbank ausgeführt wurden?**  
  
```sql  
SELECT TOP 10 qt.query_sql_text, q.query_id,   
    qt.query_text_id, p.plan_id, rs.last_execution_time  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
ORDER BY rs.last_execution_time DESC;  
```  
  
 **Wie oft wurde jede Abfrage ausgeführt?**  
  
```sql  
SELECT q.query_id, qt.query_text_id, qt.query_sql_text,   
    SUM(rs.count_executions) AS total_execution_count  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
GROUP BY q.query_id, qt.query_text_id, qt.query_sql_text  
ORDER BY total_execution_count DESC;  
```  
  
 **Wie viele Abfragen weisen die längste durchschnittliche Ausführungszeit innerhalb der letzten Stunde auf?**  
  
```sql  
SELECT TOP 10 rs.avg_duration, qt.query_sql_text, q.query_id,  
    qt.query_text_id, p.plan_id, GETUTCDATE() AS CurrentUTCTime,   
    rs.last_execution_time   
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
WHERE rs.last_execution_time > DATEADD(hour, -1, GETUTCDATE())  
ORDER BY rs.avg_duration DESC;  
```  
  
 **Wie viele Abfragen weisen die umfangreichsten durchschnittlichen physischen E/A-Lesevorgänge in den letzten 24 Stunden auf (mit der entsprechenden durchschnittlichen Zeilen- und Ausführungsanzahl)?**  
  
```sql  
SELECT TOP 10 rs.avg_physical_io_reads, qt.query_sql_text,   
    q.query_id, qt.query_text_id, p.plan_id, rs.runtime_stats_id,   
    rsi.start_time, rsi.end_time, rs.avg_rowcount, rs.count_executions  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rsi.runtime_stats_interval_id = rs.runtime_stats_interval_id  
WHERE rsi.start_time >= DATEADD(hour, -24, GETUTCDATE())   
ORDER BY rs.avg_physical_io_reads DESC;  
```  
  
 **Gab es Abfragen mit mehreren Plänen?** Diese Abfragen sind besonders interessant, da sie bei Änderungen der Planauswahl zu einer Regression führen können. Die folgende Abfrage erkennt diese Abfragen sowie alle Pläne:  
  
```sql  
WITH Query_MultPlans  
AS  
(  
SELECT COUNT(*) AS cnt, q.query_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q  
    ON qt.query_text_id = q.query_text_id  
JOIN sys.query_store_plan AS p  
    ON p.query_id = q.query_id  
GROUP BY q.query_id  
HAVING COUNT(distinct plan_id) > 1  
)  
  
SELECT q.query_id, object_name(object_id) AS ContainingObject,   
    query_sql_text, plan_id, p.query_plan AS plan_xml,  
    p.last_compile_start_time, p.last_execution_time  
FROM Query_MultPlans AS qm  
JOIN sys.query_store_query AS q  
    ON qm.query_id = q.query_id  
JOIN sys.query_store_plan AS p  
    ON q.query_id = p.query_id  
JOIN sys.query_store_query_text qt   
    ON qt.query_text_id = q.query_text_id  
ORDER BY query_id, plan_id;  
```  
  
 **Gab es Abfragen, bei denen kürzlich eine Leistungsregression stattgefunden hat (im Vergleich zu einem anderen Zeitpunkt)?** Das folgende Abfragebeispiel gibt alle Abfragen zurück, für die sich die Ausführungszeit in den letzten 48 Stunden aufgrund einer Änderung der Planauswahl verdoppelt hat. Die Abfrage vergleicht alle Intervalle der Laufzeitstatistiken miteinander.  
  
```sql  
SELECT   
    qt.query_sql_text,   
    q.query_id,   
    qt.query_text_id,   
    rs1.runtime_stats_id AS runtime_stats_id_1,  
    rsi1.start_time AS interval_1,   
    p1.plan_id AS plan_1,   
    rs1.avg_duration AS avg_duration_1,   
    rs2.avg_duration AS avg_duration_2,  
    p2.plan_id AS plan_2,   
    rsi2.start_time AS interval_2,   
    rs2.runtime_stats_id AS runtime_stats_id_2  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p1   
    ON q.query_id = p1.query_id   
JOIN sys.query_store_runtime_stats AS rs1   
    ON p1.plan_id = rs1.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi1   
    ON rsi1.runtime_stats_interval_id = rs1.runtime_stats_interval_id   
JOIN sys.query_store_plan AS p2   
    ON q.query_id = p2.query_id   
JOIN sys.query_store_runtime_stats AS rs2   
    ON p2.plan_id = rs2.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi2   
    ON rsi2.runtime_stats_interval_id = rs2.runtime_stats_interval_id  
WHERE rsi1.start_time > DATEADD(hour, -48, GETUTCDATE())   
    AND rsi2.start_time > rsi1.start_time   
    AND p1.plan_id <> p2.plan_id  
    AND rs2.avg_duration > 2*rs1.avg_duration  
ORDER BY q.query_id, rsi1.start_time, rsi2.start_time;  
```  
  
 Wenn Sie alle Leistungsregressionen (nicht nur die im Zusammenhang mit einer Änderung der Planauswahl) anzeigen möchten, entfernen Sie einfach die Bedingung `AND p1.plan_id <> p2.plan_id` aus der vorherigen Abfrage.  

 **Abfragen mit der längsten Wartezeit?**
Die Abfrage gibt die 10 Abfragen zurück, die am längsten warten. 
 
 ```sql 
  SELECT TOP 10
    qt.query_text_id,
    q.query_id,
    p.plan_id,
    sum(total_query_wait_time_ms) AS sum_total_wait_ms
FROM sys.query_store_wait_stats ws
JOIN sys.query_store_plan p ON ws.plan_id = p.plan_id
JOIN sys.query_store_query q ON p.query_id = q.query_id
JOIN sys.query_store_query_text qt ON q.query_text_id = qt.query_text_id
GROUP BY qt.query_text_id, q.query_id, p.plan_id
ORDER BY sum_total_wait_ms DESC
 ```
 
 **Gab es Abfragen, bei denen kürzlich eine Leistungsregression stattgefunden hat (Vergleich jüngerer und älterer Ausführungen)?** Die nächste Abfrage vergleicht die Abfrageausführung basierend auf den Zeiträumen der Ausführung. In diesem speziellen Beispiel vergleicht die Abfrage die Ausführung in jüngster Zeit (1 Stunde) mit einem älteren Zeitraum (letzter Tag) und identifiziert Ausführungen, die zu `additional_duration_workload`geführt haben. Diese Metrik wird als Differenz zwischen aktueller durchschnittlicher Ausführung und älterer durchschnittlicher Ausführung multipliziert mit der Anzahl der letzten Ausführungen berechnet. Sie stellt damit tatsächlich dar, wie viel zusätzliche Zeit die letzten Ausführungen im Vergleich zu älteren benötigt haben:  
  
```sql  
--- "Recent" workload - last 1 hour  
DECLARE @recent_start_time datetimeoffset;  
DECLARE @recent_end_time datetimeoffset;  
SET @recent_start_time = DATEADD(hour, -1, SYSUTCDATETIME());  
SET @recent_end_time = SYSUTCDATETIME();  
  
--- "History" workload  
DECLARE @history_start_time datetimeoffset;  
DECLARE @history_end_time datetimeoffset;  
SET @history_start_time = DATEADD(hour, -24, SYSUTCDATETIME());  
SET @history_end_time = SYSUTCDATETIME();  
  
WITH  
hist AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
     FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @history_start_time   
               AND rs.last_execution_time < @history_end_time)  
        OR (rs.first_execution_time \<= @history_start_time   
               AND rs.last_execution_time > @history_start_time)  
        OR (rs.first_execution_time \<= @history_end_time   
               AND rs.last_execution_time > @history_end_time)  
    GROUP BY p.query_id  
),  
recent AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
    FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @recent_start_time   
               AND rs.last_execution_time < @recent_end_time)  
        OR (rs.first_execution_time \<= @recent_start_time   
               AND rs.last_execution_time > @recent_start_time)  
        OR (rs.first_execution_time \<= @recent_end_time   
               AND rs.last_execution_time > @recent_end_time)  
    GROUP BY p.query_id  
)  
SELECT   
    results.query_id query_id,  
    results.query_text query_text,  
    results.additional_duration_workload additional_duration_workload,  
    results.total_duration_recent total_duration_recent,  
    results.total_duration_hist total_duration_hist,  
    ISNULL(results.count_executions_recent, 0) count_executions_recent,  
    ISNULL(results.count_executions_hist, 0) count_executions_hist   
FROM  
(  
    SELECT  
        hist.query_id query_id,  
        qt.query_sql_text query_text,  
        ROUND(CONVERT(float, recent.total_duration/  
                   recent.count_executions-hist.total_duration/hist.count_executions)  
               *(recent.count_executions), 2) AS additional_duration_workload,  
        ROUND(recent.total_duration, 2) total_duration_recent,   
        ROUND(hist.total_duration, 2) total_duration_hist,  
        recent.count_executions count_executions_recent,  
        hist.count_executions count_executions_hist     
    FROM hist   
        JOIN recent   
            ON hist.query_id = recent.query_id   
        JOIN sys.query_store_query AS q   
            ON q.query_id = hist.query_id  
        JOIN sys.query_store_query_text AS qt   
            ON q.query_text_id = qt.query_text_id      
) AS results  
WHERE additional_duration_workload > 0  
ORDER BY additional_duration_workload DESC  
OPTION (MERGE JOIN);  
```  
 
###  <a name="Stability"></a> Erhalten einer stabilen Abfrageleistung  
 Für mehrfach ausgeführte Abfragen werden Sie möglicherweise feststellen, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verschiedene Pläne verwendet, die eine unterschiedliche Ressourcenverwendung und Dauer nach sich ziehen. Mit dem Abfragespeicher können Sie erkennen, wenn die Abfrageleistung abfällt, und den optimalen Plan innerhalb des gewünschten Zeitraums bestimmen. Anschließend können Sie diesen optimalen Plan für zukünftige Abfrageausführungen erzwingen.  
  
 Sie können auch abweichende Abfrageleistungen für eine Abfrage mit Parametern ermitteln (entweder automatisch oder manuell parametrisiert). Sie können unter den verschiedenen Plänen den Plan identifizieren, der schnell und ausreichend geeignet für alle oder die meisten Parameterwerte ist, und diesen anschließend erzwingen. So erhalten Sie eine vorhersagbare Leistung für eine größere Anzahl von Benutzerszenarien.  
  
 **Erzwingen eines Plans für eine Abfrage (Anwenden einer Durchsetzungsrichtlinie).** Wenn ein Plan für eine bestimmte Abfrage erzwungen wird, erfolgen sämtliche Ausführungen dieser Abfrage mit dem erzwungenen Plan.  
  
```sql  
EXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;  
```  
  
 Durch die Verwendung von **sp_query_store_force_plan** können Sie ausschließlich solche Pläne erzwingen, die vom Abfragespeicher als Plan für diese Abfrage aufgezeichnet wurden. Es stehen für eine Abfrage also nur Pläne zur Verfügung, die bereits zum Ausführen dieser Abfrage verwendet wurden, während der Abfragespeicher aktiv war.  
  
 **Aufheben der Erzwingung eines Plans für eine Abfrage.** Wenn Sie wieder den Abfrageoptimierer von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden möchten, um den optimalen Abfrageplan zu berechnen, heben Sie mit **sp_query_store_unforce_plan** das Erzwingen des für die Abfrage ausgewählten Plans auf.  
  
```sql  
EXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Best Practices für den Abfragespeicher](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Verwenden des Abfragespeichers mit In-Memory-OLTP](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [Verwendungsszenarien für den Abfragespeicher](../../relational-databases/performance/query-store-usage-scenarios.md)   
 [So werden Daten im Abfragespeicher gesammelt](../../relational-databases/performance/how-query-store-collects-data.md)   
 [Gespeicherte Prozeduren für den Abfragespeicher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Katalogsichten des Abfragespeichers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Überwachen und Optimieren der Leistung](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [Tools für die Leistungsüberwachung und -optimierung](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)   
 [Öffnen des Aktivitätsmonitors &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [Live-Abfragestatistik](../../relational-databases/performance/live-query-statistics.md)   
 [Aktivitätsmonitor](../../relational-databases/performance-monitor/activity-monitor.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)  
 [Betrieb des Abfragespeichers in Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/) 
  
