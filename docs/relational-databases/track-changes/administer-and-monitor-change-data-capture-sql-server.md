---
title: "Verwalten und Überwachen von Change Data Capture (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: track-changes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- change data capture [SQL Server], monitoring
- change data capture [SQL Server], administering
- change data capture [SQL Server], jobs
ms.assetid: 23bda497-67b2-4e7b-8e4d-f1f9a2236685
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 08908c187ec2e548b4379aae11517f1ad50626fe
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="administer-and-monitor-change-data-capture-sql-server"></a>Verwalten und Überwachen von Change Data Capture (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie Change Data Capture verwalten und überwachen können.  
  
##  <a name="Capture"></a> Aufzeichnungsauftrag  
 Der Aufzeichnungsauftrag wird durch Ausführen der parameterlosen gespeicherten Prozedur **sp_MScdc_capture_job**initiiert. Diese gespeicherte Prozedur beginnt mit dem Extrahieren der konfigurierten Werte für *maxtrans*, *maxscans*, *continuous*und *pollinginterval* für den Aufzeichnungsauftrag aus „msdb.dbo.cdc_jobs“. Diese konfigurierten Werte werden dann als Parameter an die gespeicherte Prozedur **sp_cdc_scan**übergeben. Dies wird verwendet, um **sp_replcmds** zum Ausführen des Protokollscans aufzurufen.  
  
### <a name="capture-job-parameters"></a>Parameter von Aufzeichnungsaufträgen  
 Um das Verhalten von Capture-Aufträgen zu verstehen, müssen Sie verstehen, wie die konfigurierbaren Parameter von **sp_cdc_scan**verwendet werden.  
  
#### <a name="maxtrans-parameter"></a>maxtrans-Parameter  
 Der *maxtrans* -Parameter gibt die maximale Anzahl von Transaktionen an, die während eines einzelnen Scanzyklus des Protokolls verarbeitet werden kann. Wenn während des Scans die Anzahl der zu verarbeitenden Transaktionen diese Grenze erreicht, werden keine zusätzlichen Transaktionen in den aktuellen Scan eingeschlossen. Wenn ein Scanzyklus abgeschlossen ist, ist die Anzahl der verarbeiteten Transaktionen immer kleiner als oder gleich *maxtrans*.  
  
#### <a name="maxscans-parameter"></a>maxscans-Parameter  
 Der Parameter *maxscans* gibt die maximale Anzahl der Scanzyklen an, die vor dem Zurückkehren (kontinuierlich = 0) oder dem Ausführen einer Waitfor-Anweisung (kontinuierlich = 1) auszuführen versucht werden, um das Protokoll zu leeren.  
  
#### <a name="continous-parameter"></a>continous-Parameter  
 Der Parameter *continuous* steuert, ob **sp_cdc_scan** die Steuerung entweder nach dem Leeren des Protokolls oder nach dem Ausführen der maximalen Anzahl von Scanzyklen (Einmalmodus) aufgibt. Er steuert auch, ob **sp_cdc_scan** weiter ausgeführt wird, bis er explizit beendet wird (kontinuierlicher Modus).  
  
##### <a name="one-shot-mode"></a>Einmalmodus  
 Im Einmalmodus fordert der Aufzeichnungsauftrag **sp_cdc_scan** auf, bis zu *maxtrans* Scans auszuführen, um zu versuchen, das Protokoll zu leeren und zurückzukehren. Alle Transaktionen zusätzlich zu *maxtrans* , die im Protokoll vorhanden sind, werden in späteren Scans verarbeitet.  
  
 Der Einmalmodus wird in gesteuerten Tests verwendet, bei denen die Anzahl der zu verarbeitenden Transaktionen bekannt ist und wo es vorteilhaft ist, dass der Auftrag nach seiner Beendigung automatisch geschlossen wird. Der Einmalmodus wird nicht für die Verwendung im Produktionsbereich empfohlen. Der Grund dafür ist, dass er für das Verwalten der Anzahl der Scanzyklen auf den Auftragszeitplan zurückgreift.  
  
 Bei der Ausführung im Einmalmodus können Sie mithilfe der folgenden Berechnung eine Obergrenze des erwarteten Durchsatzes für den Aufzeichnungsauftrag, angegeben in Transaktionen pro Sekunde, berechnen:  
  
 `(maxtrans * maxscans) / number of seconds between scans`  
  
 Selbst wenn die Zeit, die zum Durchsuchen des Protokolls und zum Füllen der Änderungstabellen nicht erheblich von 0 abweicht, kann der durchschnittliche Durchsatz des Auftrags nicht den Wert überschreiten, der durch Dividieren der Höchstzahl der erlaubten Transaktionen für einen einzelnen Scan multipliziert mit der Höchstzahl der erlaubten Scans durch die Anzahl der Sekunden, die die Protokollverarbeitungsvorgänge trennen, bestimmt wird.  
  
 Beim Verwenden des Einmalmodus zum Steuern von Protokollscanvorgängen müsste die Anzahl der Sekunden zwischen Protokollverarbeitungsvorgängen durch den Auftragszeitplan festgelegt werden. Wenn dieses Verhalten gewünscht wird, ist es besser, den Aufzeichnungsauftrag im kontinuierlichen Modus auszuführen, um das erneute Planen des Prokollscans zu verwalten.  
  
##### <a name="continuous-mode-and-the-polling-interval"></a>Kontinuierlicher Modus und das Abrufintervall  
 Im kontinuierlichen Modus wird durch den Aufzeichnungsauftrag das kontinuierliche Ausführen von **sp_cdc_scan** angefordert. Dadurch kann die gespeicherte Prozedur ihre eigene Warteschleife nicht nur durch Bereitstellen der Werte von maxtrans und maxscans, sondern auch durch Bereitstellen eines Wertes für die Anzahl der Sekunden zwischen Protokollverarbeitungsvorgängen (für das Abrufintervall) verwalten. Beim Ausführen in diesem Modus bleibt der Aufzeichnungsauftrag aktiv und führt zwischen Protokollscanvorgängen eine **WAITFOR** -Anweisung aus.  
  
> [!NOTE]  
>  Wenn der Wert des Abrufintervalls größer als 0 ist, gilt die gleiche Obergrenze für den Durchsatz für den wiederkehrenden Einmalauftrag auch für den Auftragsvorgang im kontinuierlichen Modus. Das heißt, (*maxtrans* \* *maxscans*) geteilt durch ein Abrufintervall ungleich null legt eine Obergrenze für die durchschnittliche Anzahl der Transaktionen fest, die durch den Aufzeichnungsauftrag verarbeitet werden können.  
  
### <a name="capture-job-customization"></a>Anpassen eines Aufzeichnungsauftrags  
 Sie können für den Aufzeichnungsauftrag statt eines festen Abrufintervalls zusätzliche Logik anwenden, um zu bestimmen, ob sofort ein neuer Scan beginnen soll oder ob vor einem neuen Scan ein Ruhezustand erzwungen wird. Die Wahl kann einfach auf der Uhrzeit basieren. Z. B. können sehr lange Ruhezustände während Spitzenzeiten erzwungen werden. Es sind auch Abrufintervalle von 0 zum Tagesende möglich, wenn die Verarbeitungsvorgänge des Tages abgeschlossen und die Vorgänge der Nacht vorbereitet werden müssen. Der Status des Aufzeichnungsprozesses kann außerdem überwacht werden, um zu bestimmen, wann alle Transaktionen, für die bis Mitternacht ein Commit ausgeführt wurde, gescannt und in Änderungstabellen abgelegt worden sind. Dies beendet den Aufzeichnungsauftrag, der durch einen geplanten täglichen Neustart neu gestartet wird. Durch Ersetzen des übermittelten Auftragsschritts, der **sp_cdc_scan** aufruft, durch einen Aufruf eines benutzerspezifischen Wrappers für **sp_cdc_scan**, kann durch wenig zusätzlichen Aufwand ein hochgradig angepasstes Verhalten erzielt werden.  
  
##  <a name="Cleanup"></a> Cleanupauftrag  
 Dieser Abschnitt enthält Informationen darüber, wie der Change Data Capture-Cleanupauftrag funktioniert.  
  
### <a name="structure-of-the-cleanup-job"></a>Struktur des Cleanupauftrags  
 Change Data Capture verwendet eine beibehaltungsbasierte Cleanupstrategie zum Verwalten der Größe der Änderungstabellen. Der Cleanupmechanismus besteht aus einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent- [!INCLUDE[tsql](../../includes/tsql-md.md)] -Auftrag, der erstellt wird, wenn die erste Datenbanktabelle aktiviert wird. Ein einzelner Cleanupauftrag verarbeitet das Cleanup für alle Datenbankänderungstabellen und wendet denselben Beibehaltungswert auf alle definierten Aufzeichnungsinstanzen an.  
  
 Der Cleanupauftrag wird durch Ausführen der parameterlosen gespeicherten Prozedur **sp_MScdc_cleanup_job**initiiert. Diese gespeicherte Prozedur beginnt mit dem Extrahieren der konfigurierten Beibehaltungs- und Schwellenwerte für den Cleanupauftrag aus **msdb.dbo.cdc_jobs**. Der Beibehaltungswert wird verwendet, um eine neue Untergrenzenmarkierung für die Änderungstabellen zu berechnen. Die angegebene Anzahl von Minuten wird von dem maximalen *tran_end_time* -Wert aus der **cdc.lsn_time_mapping** -Tabelle subtrahiert, um die neue Untergrenzenmarkierung, angegeben als „datetime“-Wert, zu erhalten. Anschließend wird die Tabelle „CDC.lsn_time_mapping“ verwendet, um diesen „datetime“-Wert in einen entsprechenden **lsn** -Wert zu konvertieren. Wenn mehrere Werte in der Tabelle dieselbe Commitzeit verwenden, wird der **lsn** , der dem Eintrag mit dem kleinsten **lsn** entspricht, als neue Untergrenzenmarkierung bestimmt. Dieser **lsn** -Wert wird an **sp_cdc_cleanup_change_tables** übergeben, um Einträge in den Änderungstabellen aus den Datenbankänderungstabellen zu entfernen.  
  
> [!NOTE]  
>  Das Verwenden der Commitzeit der letzten Transaktion zum Berechnen der neuen Untergrenzenmarkierung hat den Vorteil, dass Änderungen in den Änderungstabellen für die angegebene Zeit erhalten bleiben. Dies geschieht sogar, wenn der Aufzeichnungsprozess zurückliegt. Alle Einträge, die dieselbe Commitzeit verwenden wie die aktuelle Untergrenzenmarkierung, werden weiterhin in den Änderungstabellen durch Wählen des kleinsten **lsn** dargestellt, der die gemeinsame Commitzeit für die aktuelle Untergrenzenmarkierung aufweist.  
  
 Wenn ein Cleanup ausgeführt wird, wird die Untergrenzenmarkierung für alle Aufzeichnungsinstanzen zunächst in einer einzelnen Transaktion aktualisiert. Anschließend wird versucht, veraltete Einträge aus den Änderungstabellen und der Tabelle cdc.lsn_time_mapping zu entfernen. Der konfigurierbare Schwellenwert begrenzt, wie viele Einträge in jeder einzelnen Anweisung gelöscht werden. Das Fehlschlagen des Löschvorgangs für einzelne Tabellen führt nicht dazu, dass die Ausführung des Vorgangs nicht für die übrigen Tabellen versucht wird.  
  
### <a name="cleanup-job-customization"></a>Anpassen eines Cleanupauftrags  
 Die Anpassungsmöglichkeiten für den Cleanupauftrag bestehen in der Strategie, die verwendet wird, um zu bestimmen, welche Einträge in der Änderungstabelle verworfen werden sollen. Im übermittelten Cleanupauftrag wird nur eine zeitbasierte Strategie unterstützt. In diesem Fall wird die neue Untergrenzenmarkierung durch Subtrahieren der zulässigen Beibehaltungsdauer von der Commitzeit der letzten verarbeiteten Transaktion berechnet. Da die zugrunde liegenden Cleanupprozeduren auf **lsn** statt auf Zeit basieren, kann eine beliebe Anzahl von Strategien verwendet werden, um den kleinsten **lsn** zu bestimmen, der in den Änderungstabellen bewahrt werden soll. Nur einige von diesen sind streng zeitbasiert. Es könnte z. B. Wissen über die Clients zum Bereitstellen einer Sicherung verwendet werden, wenn nachfolgende Prozesse, die Zugriff auf die Änderungstabellen erfordern, nicht ausgeführt werden können. Obwohl die Standardstrategie denselben **lsn** für das Cleanup aller Änderungstabellen der Datenbank verwendet, kann auch die zugrunde liegende Cleanupprozedur für das Cleanup auf Aufzeichnungsinstanzebene aufgerufen werden.  
  
##  <a name="Monitor"></a> Überwachen des Change Data Capture-Prozesses  
 Indem Sie den Change Data Capture-Prozess überwachen, können Sie ermitteln, ob Änderungen korrekt und mit einer akzeptablen Latenzzeit in die Änderungstabellen geschrieben werden. Das Überwachen kann Ihnen auch dabei helfen, jegliche Fehler zu identifizieren, die auftreten könnten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügt über zwei dynamische Verwaltungssichten, womit Sie Change Data Capture überwachen können: [sys.dm_cdc_log_scan_sessions](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md) und [sys.dm_cdc_errors](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md).  
  
### <a name="identify-sessions-with-empty-result-sets"></a>Identifizieren von Sitzungen mit leeren Resultsets  
 Jede Zeile in sys.dm_cdc_log_scan_sessions stellt eine Protokollscansitzung (außer der Zeile mit einer ID von 0) dar. Eine Protokollscansitzung entspricht einer Ausführung von [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md). Während einer Sitzung kann der Scan entweder Änderungen oder ein leeres Ergebnis zurückgeben. Wenn das Resultset leer ist, wird die Spalte empty_scan_count in sys.dm_cdc_log_scan_sessions auf den Wert 1 gesetzt. Folgen noch weitere leere Resultsets, z. B. wenn der Aufzeichnungsauftrag dauerhaft ausgeführt wird, wird empty_scan_count in der letzten vorhandenen Zeile inkrementiert. Wenn sys.dm_cdc_log_scan_sessions z. B. bereits 10 Zeilen für Scans enthält, die Änderungen zurückgegeben haben, und fünf leere Ergebnisse aufeinander folgen, enthält die Sicht 11 Zeilen. Die letzte Zeile verfügt in der Spalte empty_scan_count über einen Wert von 5. Führen Sie die folgende Abfrage aus, um Sitzungen zu ermitteln, die einen leeren Scan aufweisen:  
  
 `SELECT * from sys.dm_cdc_log_scan_sessions where empty_scan_count <> 0`  
  
### <a name="determine-latency"></a>Bestimmen von Latenzzeit  
 Die Verwaltungssicht sys.dm_cdc_log_scan_sessions enthält eine Spalte, in der die Latenzzeit für die einzelnen Aufzeichnungssitzungen erfasst wird. Die Latenzzeit ist als die Zeitspanne zwischen dem Ausführen des Commit für eine Transaktion in einer Quelltabelle und dem Ausführen des Commit für die letzte aufgezeichnete Transaktion in der Änderungstabelle definiert. Die Latenzzeitspalte wird nur für aktive Sitzungen aufgefüllt. Für Sitzungen, die in der Spalte empty_scan_count column einen höheren Wert als 0 enthalten, wird die Latenzzeitspalte auf 0 gesetzt. Die folgende Abfrage gibt die durchschnittliche Latenzzeit für die letzten Sitzungen zurück:  
  
 `SELECT latency FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0`  
  
 Sie können Latenzzeitdaten verwenden, um zu ermitteln, wie schnell bzw. langsam der Aufzeichnungsprozess Transaktionen verarbeitet. Diese Daten sind sehr hilfreich, wenn der Aufzeichnungsprozess kontinuierlich ausgeführt wird. Wenn der Aufzeichnungsprozess gemäß einem Zeitplan ausgeführt wird, kann die Latenzzeit u. U. lang sein. Dies liegt an der Verzögerung zwischen den Transaktionen, für die in der Quelltabelle ein Commit ausgeführt wird, und dem Aufzeichnungsprozess, der zum geplanten Zeitpunkt ausgeführt wird.  
  
 Eine andere wichtige Kennzahl für die Effizienz des Aufzeichnungsprozesses ist der Durchsatz. Dies ist die durchschnittliche Anzahl von Befehlen pro Sekunde, die während einer Sitzung verarbeitet werden. Um den Durchsatz einer Sitzung zu ermitteln, teilen Sie den Wert in der Spalte command_count durch den Wert in der Spalte mit der Dauer (duration). Die folgende Abfrage gibt den durchschnittlichen Durchsatz für die letzten Sitzungen zurück:  
  
 `SELECT command_count/duration AS [Throughput] FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0`  
  
### <a name="use-data-collector-to-collect-sampling-data"></a>Verwenden des Datensammlers zum Erfassen von Samplingdaten  
 Mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datensammlers können Sie Momentaufnahmen von Daten aus allen Tabellen oder dynamischen Verwaltungssichten erfassen und ein Data Warehouse für die Leistung erstellen. Wenn für eine Datenbank Change Data Capture aktiviert ist, sollten Sie in regelmäßigen Abständen Momentaufnahmen der Sichten sys.dm_cdc_log_scan_sessions und sys.dm_cdc_errors erstellen, um später eine Analyse durchführen zu können. Die folgende Prozedur richtet einen Datensammler ein, der Datenstichproben aus der Verwaltungssicht sys.dm_cdc_log_scan_sessions entnimmt.  
  
 **Konfigurieren der Datensammlung**  
  
1.  Aktivieren Sie den Datensammler, und konfigurieren Sie ein Management Data Warehouse. Weitere Informationen finden Sie unter [Verwalten von Datensammlungen](../../relational-databases/data-collection/manage-data-collection.md).  
  
2.  Führen Sie den folgenden Code aus, um für Change Data Capture einen benutzerdefinierten Sammler zu erstellen.  
  
    ```sql  
    USE msdb;  
  
    DECLARE @schedule_uid uniqueidentifier;  
  
    -- Collect and upload data every 5 minutes  
    SELECT @schedule_uid = (  
    SELECT schedule_uid from sysschedules_localserver_view   
    WHERE name = N'CollectorSchedule_Every_5min')  
  
    DECLARE @collection_set_id int;  
  
    EXEC dbo.sp_syscollector_create_collection_set  
    @name = N' CDC Performance Data Collector',  
    @schedule_uid = @schedule_uid,          
    @collection_mode = 0,                   
    @days_until_expiration = 30,                
    @description = N'This collection set collects CDC metadata',  
    @collection_set_id = @collection_set_id output;  
  
    -- Create a collection item using statistics from   
    -- the change data capture dynamic management view.  
    DECLARE @paramters xml;  
    DECLARE @collection_item_id int;  
  
    SELECT @paramters = CONVERT(xml,   
        N'<TSQLQueryCollector>  
            <Query>  
              <Value>SELECT * FROM sys.dm_cdc_log_scan_sessions</Value>  
              <OutputTable>cdc_log_scan_data</OutputTable>  
            </Query>  
          </TSQLQueryCollector>');  
  
    EXEC dbo.sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = N'302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @name = ' CDC Performance Data Collector',  
    @frequency = 5,   
    @parameters = @paramters,  
    @collection_item_id = @collection_item_id output;  
  
    GO  
    ```  
  
3.  Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]die Option **Verwaltung**und dann die Option **Datensammlung**. Klicken Sie mit der rechten Maustaste auf **CDC Performance Data Collector**, und klicken Sie dann auf **Datensammlungssatz starten**.  
  
4.  Greifen Sie in dem Data Warehouse, das Sie in Schritt 1 konfiguriert haben, auf die Tabelle custom_snapshots.cdc_log_scan_data zu. Diese Tabelle stellt eine Verlaufs-Momentaufnahme der Daten von Protokollscansitzungen bereit. Sie können diese Daten verwenden, um die Latenzzeit, den Durchsatz und andere Leistungskennzahlen in Abhängigkeit der Zeit zu analysieren.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Über Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [Aktivieren und Deaktivieren von Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [Arbeiten mit Änderungsdaten &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
  
