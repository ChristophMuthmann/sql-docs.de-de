---
title: Überwachen der Leistung für Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dfd2b639-8fd4-4cb9-b134-768a3898f9e6
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 0d41627a8c08e2fd06a9d5fdb391f5e626599233
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="monitor-performance-for-always-on-availability-groups"></a>Überwachen der Leistung für Always On-Verfügbarkeitsgruppen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Der Leistungsaspekt der Always On-Verfügbarkeitsgruppen ist entscheidend, um die Vereinbarung zum Servicelevel (SLA) für Ihre unternehmenskritischen Datenbanken zu erfüllen. Wenn Sie den Vorgang bei Verfügbarkeitsgruppen zum Senden von Protokollen an sekundäre Replikate verstehen, können Sie die Recovery Time Objective (RTO) und Recovery Point Objective (RPO) Ihrer Verfügbarkeitsimplementierung besser einschätzen und Engpässe bei leistungsschwachen Verfügbarkeitsgruppen oder Replikaten ausfindig machen. In diesem Artikel werden der Synchronisierungsprozess und die Berechnung einiger der wichtigsten Metriken beschrieben. Zudem enthält der Artikel Links zu einigen allgemeinen leistungsbezogenen Problembehandlungsszenarien.  
  
 Die folgenden Themen werden erörtert:  
  
-   [Datensynchronisierungsprozess](#BKMK_DATA_SYNC_PROCESS)  
  
-   [Flusssteuerungsgates](#BKMK_FLOW_CONTROL_GATES)  
  
-   [Einschätzen der Failoverzeit (RTO)](#BKMK_RTO)  
  
-   [Einschätzen des möglichen Datenverlusts (RPO)](#BKMK_RPO)  
  
-   [Überwachen von RTO und RPO](#BKMK_Monitoring_for_RTO_and_RPO)  
  
-   [Leistungsbezogene Problembehandlungsszenarien](#BKMK_SCENARIOS)  
  
-   [Nützliche erweiterte Ereignisse](#BKMK_XEVENTS)  
  
##  <a name="BKMK_DATA_SYNC_PROCESS"></a> Datensynchronisierungsprozess  
 Um die Zeit bis zur vollständigen Synchronisierung einzuschätzen und den Engpass zu identifizieren, müssen Sie den Synchronisierungsprozess verstehen. Leistungsengpässe können an einer beliebigen Stelle im Prozess auftreten. Durch die Ermittlung des Engpasses können Sie den zugrunde liegenden Problemen besser auf den Grund gehen. Der folgende Abbildung und Tabelle veranschaulichen den Datensynchronisierungsprozess:  
  
 ![Datensynchronisierung von Verfügbarkeitsgruppen](media/always-onag-datasynchronization.gif "Availability group data synchronization")  
  
|||||  
|-|-|-|-|  
|**Sequenz**|**Beschreibung des Schritts**|**Kommentare**|**Nützliche Metriken**|  
|1|Protokollgenerierung|Protokolldaten werden auf den Datenträger geleert. Dieses Protokoll muss in die sekundären Replikate repliziert werden. Die Protokolldatensätze werden in die Sendewarteschlange eingereiht.|[SQL Server: Datenbank > Geleerte Protokollbytes/Sekunde](~/relational-databases/performance-monitor/sql-server-databases-object.md)|  
|2|Erfassung|Für jede Datenbank werden Protokolle erfasst und an die entsprechende Partnerwarteschlange gesendet (eine pro Datenbankreplikatspaar). Dieser Erfassungsprozess wird fortlaufend ausgeführt, solange das Verfügbarkeitsreplikat verbunden ist und die Datenverschiebung nicht aus irgendeinem Grund angehalten wird. Der Status des Datenbankreplikatspaar lautet entweder „Wird synchronisiert“ oder „Synchronisiert“. Wenn die Nachrichten beim Erfassungsprozess nicht schnell genug überprüft und in die Warteschlange eingereiht werden können, führt dies zum Anwachsen der Protokollsendewarteschlange.|[SQL Server: Verfügbarkeitsreplikat > An Replikat gesendete Bytes/Sekunde](~/relational-databases/performance-monitor/sql-server-availability-replica.md): Eine Aggregation der Summe aller Datenbanknachrichten in der Warteschlange für dieses Verfügbarkeitsreplikat.<br /><br /> [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB) und [log_bytes_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB/s) für das primäre Replikat|  
|3|Send|Die Nachrichten in jeder Datenbankreplikatswarteschlange werden aus der Warteschlange entfernt und über das Netzwerk an das entsprechende sekundäre Replikat gesendet.|[SQL Server: Verfügbarkeitsreplikat >An den Transport gesendete Bytes/Sekunde](~/relational-databases/performance-monitor/sql-server-availability-replica.md) und [SQL Server: Verfügbarkeitsreplikat > Nachrichtenbestätigungszeit](~/relational-databases/performance-monitor/sql-server-availability-replica.md) (ms)|  
|4|Empfang und Zwischenspeicherung|Jedes sekundäre Replikat empfängt und speichert die Nachricht zwischen.|Leistungsindikator [SQL Server: Verfügbarkeitsreplikat > Empfangene Protokollbytes/Sekunde](~/relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|5|Festschreibung|Ein Protokoll wird zur Festschreibung für das sekundäre Replikat geleert. Nach der Protokollleerung wird eine Bestätigung an das primäre Replikat zurückgesendet.<br /><br /> Ist das Protokoll festgeschrieben, wurde ein Datenverlust abgewendet.|Leistungsindikator [SQL Server: Datenbank > Geleerte Protokollbytes/Sekunde](~/relational-databases/performance-monitor/sql-server-databases-object.md)<br /><br /> Wartetyp [HADR_LOGCAPTURE_SYNC](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
|6|Wiederholen|Wiederholen Sie die geleerten Seiten auf dem sekundären Replikat. Seiten werden in der Wiederholungswarteschlange beibehalten, während sie darauf warten, wiederholt zu werden.|[SQL Server: Datenbankreplikat > Wiederholte Bytes/Sekunde](~/relational-databases/performance-monitor/sql-server-database-replica.md)<br /><br /> [redo_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB) und [redo_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).<br /><br /> Wartetyp [REDO_SYNC](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
  
##  <a name="BKMK_FLOW_CONTROL_GATES"></a> Flusssteuerungsgates  
 Verfügbarkeitsgruppen werden mit Flusssteuerungsdaten für das primäre Replikat entworfen, um eine übermäßige Ressourcenauslastung wie etwa bei Netzwerk- und Speicherressourcen für alle Verfügbarkeitsreplikate zu vermeiden. Diese Flusssteuerungsgates wirken sich nicht auf den Synchronisierungsintegritätszustand der Verfügbarkeitsreplikate aus, können jedoch die allgemeine Leistung der Verfügbarkeitsdatenbanken beeinflussen, einschließlich der RPO.  
  
 Nachdem die Protokolle für das primäre Replikat erfasst wurden, unterliegen sie zwei Ebenen der Flusssteuerungen, wie in der folgenden Tabelle gezeigt.  
  
|||||  
|-|-|-|-|  
|**Level**|**Anzahl der Gates**|**Anzahl der Nachrichten**|**Nützliche Metriken**|  
|Transport|1 pro Verfügbarkeitsreplikat|8192|Erweiterte Ereignisse **database_transport_flow_control_action**|  
|Datenbank|1 pro Verfügbarkeitsdatenbank|11200 (x64)<br /><br /> 1600 (x86)|[DBMIRROR_SEND](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)<br /><br /> Erweitertes Ereignis **hadron_database_flow_control_action**|  
  
 Sobald der Nachrichtenschwellenwert von einem der beiden Gates erreicht wird, werden keine Protokollnachrichten mehr an ein bestimmtes Replikat oder für eine bestimmte Datenbank gesendet. Nachrichten können gesendet werden, sobald Bestätigungsnachrichten für die gesendeten Nachrichten empfangen wurden, um die Anzahl der gesendeten Nachrichten auf einen Wert unterhalb des Schwellenwerts zu senken.  
  
 Neben den Flusssteuerungsgates gibt es einen weiteren Faktor, der das Senden der Protokollnachrichten verhindern kann. Durch die Synchronisierung von Replikaten wird sichergestellt, dass die Nachrichten gesendet und in der Reihenfolge der Protokollfolgenummern (Log Sequence Numbers, LSN) angewendet werden. Bevor eine Protokollnachricht gesendet wird, wird auch dessen LSN mit der niedrigsten bestätigten LSN-Zahl abgeglichen, um sicherzustellen, dass diese unter einem der Schwellenwerte (abhängig vom Nachrichtentyp) liegt. Wenn die Diskrepanz zwischen den zwei LSN-Zahlen größer als der Schwellenwert ist, werden die Nachrichten nicht gesendet. Wenn die Diskrepanz wieder unter dem Schwellenwert liegt, werden die Nachrichten gesendet.  
  
 Die zwei nützlichen Leistungsindikatoren [SQL Server: Verfügbarkeitsreplikat > Flusssteuerung/Sekunde](~/relational-databases/performance-monitor/sql-server-availability-replica.md) und [SQL Server: Verfügbarkeitsreplikat > Flusssteuerungszeit (ms/Sekunde)](~/relational-databases/performance-monitor/sql-server-availability-replica.md) zeigen, wie oft die Flusssteuerung innerhalb der letzten Sekunde aktiviert und wie viel Zeit für das Warten auf die Flusssteuerung benötigt wurde. Längere Wartezeiten bei der Flusssteuerung bedeuten eine höhere RPO. Weitere Informationen zu den Arten von Problemen, die eine lange Wartezeit für die Flusssteuerung verursachen können, finden Sie unter [Problembehandlung: Verfügbarkeitsgruppe überschreiten RPO](troubleshoot-availability-group-exceeded-rpo.md).  
  
##  <a name="BKMK_RTO"></a> Einschätzen der Failoverzeit (RTO)  
 Die RTO in Ihrer SLA hängt von der Failoverzeit Ihrer Always On-Implementierung an einem bestimmten Zeitpunkt ab, die mit der folgenden Formel ausgedrückt werden kann:  
  
 ![Verfügbarkeitsgruppen – Berechnung der RTO](media/always-on-rto.gif "Availability groups RTO calculation")  
  
> [!IMPORTANT]  
>  Wenn eine Verfügbarkeitsgruppe mehr als eine Verfügbarkeitsdatenbank enthält, wird die Verfügbarkeitsdatenbank mit dem höchsten Tfailover-Wert zum Grenzwert für die RTO-Konformität.  
  
 Die Ausfallerkennungszeit, Tdetection, ist der Zeitaufwand, den das System zur Erkennung des Fehlers benötigt. Diese Zeit hängt von den Einstellungen auf Clusterebene ab, nicht von den einzelnen Verfügbarkeitsreplikaten. Abhängig von der konfigurierten Bedingung für ein automatisches Failover kann ein Failover als sofortige Antwort auf einen kritischen internen SQL Server-Fehler wie verwaiste Spinlocks ausgelöst werden. In diesem Fall kann die Erkennung genauso schnell sein wie das Senden des Fehlerberichts [sp_server_diagnostics &#40;Transact-SQL&#41; ](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) an den WSFC-Cluster (das Standardintervall beträgt 1/3 des Timeout für die Integritätsprüfung). Ein Failover kann auch aufgrund eines Timeouts ausgelöst werden, z.B., wenn das Timeout für die Clusterintegritätsprüfung (standardmäßig 30 Sekunden) oder die Lease zwischen Ressourcen-DLLs und der SQL Server-Instanz (standardmäßig 20 Sekunden) abgelaufen ist. In diesem Fall ist die Erkennungszeit genauso lang wie das Timeoutintervall. Weitere Informationen finden Sie unter [Flexible Failoverrichtlinie für automatisches Failover einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](https://msdn.microsoft.com/library/hh710061(SQL.120).aspx).  
  
 Um für ein Failover bereit zu sein, muss das sekundäre Replikat lediglich eine Wiederholung ausführen, um das Ende des Protokolls zu erreichen. Die Wiederholungszeit, Tredo, wird mit der folgenden Formel berechnet:  
  
 ![Berechnung der Wiederholungszeit von Verfügbarkeitsgruppen](media/always-on-redo.gif "Availability groups redo time calculation")  
  
 Hierbei steht *redo_queue* für den Wert in [redo_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) und *redo_rate* für den Wert in [redo_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).  
  
 Der zeitliche Mehraufwand für das Failover, Toverhead, schließt den Zeitaufwand ein, der für ein Failover des WSFC-Clusters und die Aktivierung der Datenbanken erforderlich ist. Diese Zeit ist normalerweise kurz und konstant.  
  
##  <a name="BKMK_RPO"></a> Einschätzen des möglichen Datenverlusts (RPO)  
 Die RPO in Ihrer SLA hängt von dem möglichen Datenverlust Ihrer Always On-Implementierung zu einem beliebigen Zeitpunkt ab. Dieser mögliche Datenverlust kann mit der folgenden Formel ausgedrückt werden:  
  
 ![Verfügbarkeitsgruppen – Berechnung der RPO](media/always-on-rpo.gif "Availability groups RPO calculation")  
  
 Hierbei steht *log_send_queue* für den Wert von [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) und *log generation rate* für den Wert von [SQL Server: Datenbank > Geleerte Protokollbytes/Sekunde](~/relational-databases/performance-monitor/sql-server-databases-object.md).  
  
> [!WARNING]  
>  Wenn eine Verfügbarkeitsgruppe mehr als eine Verfügbarkeitsdatenbank enthält, wird die Verfügbarkeitsdatenbank mit der höchsten Tdata_loss-Wert zum Grenzwert für die RPO-Konformität.  
  
 Die Protokollsendewarteschlange stellt alle Daten dar, die aufgrund eines schwerwiegenden Fehlers verloren gehen können. Auf den ersten Blick fällt auf, dass anstelle der Protokollsenderate die Protokollgenerierungsrate verwendet wird (siehe [log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)). Denken Sie jedoch daran, dass Sie durch Verwendung der Protokollsenderate lediglich die Zeit zur Synchronisierung erhalten, während die RPO den Datenverlust abhängig von der Dauer des Datenverlusts misst, nicht abhängig von der Synchronisierungsdauer.  
  
 Eine einfachere Möglichkeit zur Einschätzung von Tdata_loss bietet die Verwendung von [last_commit_time](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md). Die DMV für das primäre Replikat meldet diesen Wert für alle Replikate. Sie können die Diskrepanz zwischen dem Wert für das primäre Replikat und dem für das sekundäre Replikat berechnen, um einzuschätzen, wie schnell das Protokoll für das sekundäre Replikat im Vergleich zum primären Replikat verarbeitet wird. Wie bereits erwähnt, sagt diese Berechnung nichts über den möglichen Datenverlust basierend auf der Dauer der Protokollgenerierung aus, sollte jedoch eine weitgehende Annäherung darstellen.  
  
##  <a name="BKMK_Monitoring_for_RTO_and_RPO"></a> Überwachen von RTO und RPO  
 In diesem Abschnitt wird das Überwachen von Verfügbarkeitsgruppen für die Metriken RTO und RPO veranschaulicht. Diese Demo ähnelt dem GUI-Tutorial unter [The Always On health model, part 2: Extending the health model](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx) (Das Always On-Zustandsmodells, Teil 2: Erweitern des Zustandsmodells).  
  
 Elemente der Failoverzeit und Berechnungen des möglichen Datenverlusts unter [Einschätzen der Failoverzeit (RTO)](#BKMK_RTO) und [Einschätzen des möglichen Datenverlusts (RPO)](#BKMK_RPO) werden praktischerweise als Leistungsmetriken in der Richtlinienverwaltungsfacets **Datenbankreplikatszustand** bereitgestellt (siehe [Anzeigen der Facets der richtlinienbasierten Verwaltung für ein SQL Server-Objekt](~/relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)). Sie können diese beiden Metriken nach einem Zeitplan überwachen und werden benachrichtigt, wenn die Metriken Ihre RTO bzw. RPO überschreiten.  
  
 Die angezeigten Skripts erstellen zwei Systemrichtlinien mit den folgenden Merkmalen, die basierend auf ihren jeweiligen Zeitplänen ausgeführt werden:  
  
-   Eine RTO-Richtlinie mit einer Auswertung im 5-Minuten-Takt, bei der ein Fehler auftritt, wenn die geschätzte Failoverzeit 10 Minuten überschreitet  
  
-   Eine RPO-Richtlinie mit einer Auswertung im 30-Minuten-Takt, bei der ein Fehler auftritt, wenn die geschätzte Failoverzeit 1 Stunde überschreitet  
  
-   Beide Richtlinien weisen die gleich Konfiguration für alle Verfügbarkeitsreplikate auf.  
  
-   Auf allen Servern werden Richtlinien ausgewertet, jedoch nur für die Verfügbarkeitsgruppen, bei denen das lokale Verfügbarkeitsreplikat das primäre Replikat darstellt. Wenn das lokale Verfügbarkeitsreplikat nicht das primäre Replikat darstellt, werden die Richtlinien nicht ausgewertet.  
  
-   Richtlinienfehler werden praktischerweise auf dem Always On-Dashboard angezeigt, wenn Sie diese für das primäre Replikat anzeigen.  

Um die Richtlinien zu erstellen, befolgen Sie die nachfolgenden Anweisungen für alle Serverinstanzen, die in der Verfügbarkeitsgruppe enthalten sind:  

1.  [Starten Sie den SQL Server-Agent-Dienst](~/ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md), sofern dieser noch nicht gestartet wurde.  
  
2.  Klicken Sie in SQL Server Management Studio im Menü **Tools** auf **Optionen**.  
  
3.  Wählen Sie auf der Registerkarte **SQL Server Always On** die Option **Benutzerdefinierte Always On-Richtlinie aktivieren** aus, und klicken Sie auf **OK**.  
  
     Durch diese Einstellung können Sie ordnungsgemäß konfigurierte benutzerdefinierte Richtlinien auf dem Always On-Dashboard anzeigen.  
  
4.  Erstellen Sie eine [richtlinienbasierte Verwaltungsbedingung](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) mit den folgenden Spezifikationen:  
  
    -   **Name**: `RTO`  
  
    -   **Facet**: **Zustand des Datenbankreplikats**  
  
    -   **Feld**: `Add(@EstimatedRecoveryTime, 60)`  
  
    -   **Operator**: **<=**  
  
    -   **Wert**: `600`  
  
     Bei dieser Bedingung tritt ein Fehler auf, wenn die mögliche Failoverzeit 10 Minuten überschreitet, einschließlich eines Mehraufwands von 60 Sekunden für die Fehlererkennung und das Failover.  
  
5.  Erstellen Sie eine zweite [richtlinienbasierte Verwaltungsbedingung](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) mit den folgenden Spezifikationen:  
  
    -   **Name**: `RPO`  
  
    -   **Facet**: **Zustand des Datenbankreplikats**  
  
    -   **Feld**: `@EstimatedDataLoss`  
  
    -   **Operator**: **<=**  
  
    -   **Wert**: `3600`  
  
     Bei dieser Bedingung tritt ein Fehler auf, wenn der Datenverlust 1 Stunde überschreitet.  
  
6.  Erstellen Sie eine dritte [richtlinienbasierte Verwaltungsbedingung](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) mit den folgenden Spezifikationen:  
  
    -   **Name**: `IsPrimaryReplica`  
  
    -   **Facet**: **Verfügbarkeitsgruppe**  
  
    -   **Feld**: `@LocalReplicaRole`  
  
    -   **Operator**: **=**  
  
    -   **Wert**: `Primary`  
  
     Diese Bedingung überprüft, ob das lokale Verfügbarkeitsreplikat für eine bestimmte Verfügbarkeitsgruppe das primäre Replikat ist.  
  
7.  Erstellen Sie eine [richtlinienbasierte Verwaltungsrichtlinie](~/relational-databases/policy-based-management/create-a-policy-based-management-policy.md) mit den folgenden Spezifikationen:  
  
    -   Seite **Allgemein**:  
  
        -   **Name**: `CustomSecondaryDatabaseRTO`  
  
        -   **Bedingung überprüfen**: `RTO`  
  
        -   **Für Ziele**: **Alle DatabaseReplicaState** in **IsPrimaryReplica AvailabilityGroup**  
  
             Durch diese Einstellung wird sichergestellt, dass die Richtlinie nur für Verfügbarkeitsgruppen ausgewertet wird, bei denen das lokale Verfügbarkeitsreplikat das primäre Replikat darstellt.  
  
        -   **Auswertungsmodus**: **Nach Zeitplan**  
  
        -   **Zeitplan**: **CollectorSchedule_Every_5min**  
  
        -   **Aktiviert**: **Ausgewählt**  
  
    -   Seite **Beschreibung**:  
  
        -   **Kategorie**: **Warnungen zu Verfügbarkeitsdatenbanken**  
  
             Mit dieser Einstellung können die Ergebnisse der Richtlinienauswertung auf dem Always On-Dashboard angezeigt werden.  
  
        -   **Beschreibung**: **Das aktuelle Replikat ist eine RTO, die 10 Minuten überschreitet. Hierbei wird von einem Mehraufwand von 1 Minute für die Erkennung und das Failover ausgegangen. Sie sollten Leistungsprobleme in der jeweiligen Serverinstanz sofort untersuchen.**  
  
        -   **Anzuzeigender Text**: **RTO überschritten**  
  
8.  Erstellen Sie eine zweite [richtlinienbasierte Verwaltungsrichtlinie](~/relational-databases/policy-based-management/create-a-policy-based-management-policy.md) mit den folgenden Spezifikationen:  
  
    -   Seite **Allgemein**:  
  
        -   **Name**: `CustomAvailabilityDatabaseRPO`  
  
        -   **Bedingung überprüfen**: `RPO`  
  
        -   **Für Ziele**: **Alle DatabaseReplicaState** in **IsPrimaryReplica AvailabilityGroup**  
  
        -   **Auswertungsmodus**: **Nach Zeitplan**  
  
        -   **Zeitplan**: **CollectorSchedule_Every_30min**  
  
        -   **Aktiviert**: **Ausgewählt**  
  
    -   Seite **Beschreibung**:  
  
        -   **Kategorie**: **Warnungen zu Verfügbarkeitsdatenbanken**  
  
        -   **Beschreibung**: **Die Verfügbarkeitsdatenbank hat Ihre RPO von 1 Stunde überschritten. Sie sollten Leistungsprobleme in den Verfügbarkeitsreplikaten sofort untersuchen.**  
  
        -   **Anzuzeigender Text**: **RPO überschritten**  
  
 Wenn Sie fertig sind, werden zwei neue SQL Server-Agent-Aufträge erstellt, jeweils einer für den Richtlinienauswertungszeitplan. Diese Aufträge sollten mit Namen versehen werden, die mit **syspolicy_check_schedule** beginnen.  
  
 Sie können zur Überprüfen der Auswertungsergebnisse den Auftragsverlauf einsehen. Fehler bei der Auswertung werden auch im Windows-Anwendungsprotokoll (in der Ereignisanzeige) mit der Ereignis-ID 34052 erfasst. Sie können auch den SQL Server-Agent für das Senden von Warnungen für Richtlinienfehler konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von Warnungen zur Benachrichtigung von Richtlinienadministratoren bei Richtlinienfehlern](~/relational-databases/policy-based-management/configure-alerts-to-notify-policy-administrators-of-policy-failures.md).  
  
##  <a name="BKMK_SCENARIOS"></a> Leistungsbezogene Problembehandlungsszenarien  
 Die folgende Tabelle enthält die allgemeinen leistungsbezogenen Problembehandlungsszenarien.  
  
|Szenario|Description|  
|--------------|-----------------|  
|[Problembehandlung: Verfügbarkeitsgruppe hat RTO überschritten](troubleshoot-availability-group-exceeded-rto.md)|Nach einem automatischen Failover oder einem geplanten manuellen Failover ohne Datenverlust überschreitet die Failoverzeit die RTO. Ein anderer Fall: Wenn Sie die Failoverzeit eines sekundären Replikats im synchronen Commitmodus (z.B. eines Partners für das automatische Failover) einschätzen, stellen Sie fest, dass diese Ihre RTO überschreitet.|  
|[Problembehandlung: Verfügbarkeitsgruppe hat RPO überschritten](troubleshoot-availability-group-exceeded-rpo.md)|Nachdem Sie ein erzwungenes manuelles Failover ausgeführt haben, ist der Datenverlust größer als Ihre RPO. Ein anderer Fall: Wenn Sie den möglichen Datenverlust eines sekundäres Replikats im asynchronen Commitmodus berechnen, stellen Sie fest, dass dieser Ihre RPO überschreitet.|  
|[Problembehandlung: Änderungen am primären Replikat werden nicht beim sekundären Replikat widergespiegelt](troubleshoot-primary-changes-not-reflected-on-secondary.md)|Die Clientanwendung führt erfolgreich ein Update für das primäre Replikat durch, wobei jedoch die Abfrage des sekundären Replikats ergibt, dass die Änderung nicht widergespiegelt wird.|  
  
##  <a name="BKMK_XEVENTS"></a> Nützliche erweiterte Ereignisse  
 Für die Behandlung von Problemen mit Replikaten im Zustand **Wird synchronisiert** sind folgende erweiterte Ereignisse nützlich.  
  
|Ereignisname|Kategorie|Channel|Verfügbarkeitsreplikat|  
|----------------|--------------|-------------|--------------------------|  
|redo_caught_up|Transaktionen|Debuggen|Secondary|  
|redo_worker_entry|Transaktionen|Debuggen|Secondary|  
|hadr_transport_dump_message|`alwayson`|Debuggen|Primär|  
|hadr_worker_pool_task|`alwayson`|Debuggen|Primär|  
|hadr_dump_primary_progress|`alwayson`|Debuggen|Primär|  
|hadr_dump_log_progress|`alwayson`|Debuggen|Primär|  
|hadr_undo_of_redo_log_scan|`alwayson`|Analytic|Secondary|  
  
  