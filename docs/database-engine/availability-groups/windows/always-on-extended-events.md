---
title: Erweiterte Ereignisse von Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5950f98a-3950-473d-95fd-cde3557b8fc2
caps.latest.revision: 6
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 29966508374b8deec94ac60dd151ab7379ede1e7
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="always-on-availability-groups-extended-events"></a>Erweiterte Ereignisse von Always On-Verfügbarkeitsgruppen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server definiert erweiterte Ereignisse, die speziell für Always On-Verfügbarkeitsgruppen gelten. Sie können diese erweiterten Ereignisse in einer Sitzung aktivieren, die Ihnen bei der Ursachendiagnose helfen, wenn Sie Probleme mit einer Verfügbarkeitsgruppe behandeln. Sie können erweiterte Ereignisse der Verfügbarkeitsgruppe mit der folgenden Abfrage anzeigen:  
  
```sql  
SELECT * FROM sys.dm_xe_objects WHERE name LIKE '%hadr%'  
```  
  
 [Alwayson_health-Sitzung](always-on-extended-events.md#BKMK_alwayson_health)  
  
 [Erweiterte Ereignisse zum Debuggen](always-on-extended-events.md#BKMK_Debugging)  
  
 [Referenz zu erweiterten Ereignisse von Always On-Verfügbarkeitsgruppen](always-on-extended-events.md#BKMK_Reference)  
  
##  <a name="BKMK_alwayson_health"></a> Alwayson_health-Sitzung  
 Die alwayson_health-Sitzung mit den erweiterten Ereignissen wird automatisch beim Erstellen der Verfügbarkeitsgruppe erstellt und erfasst eine Teilmenge verwandter Ereignisse der Verfügbarkeitsgruppe. Diese Sitzung ist als nützliches und praktisches Tool vorkonfiguriert, mit dem Sie schnell die ersten Schritte bei der Behandlung von Problemen mit einer Verfügbarkeitsgruppe durchführen können. Der Assistent zum Erstellen von Verfügbarkeitsgruppen startet automatisch die Sitzung für jedes beteiligte Verfügbarkeitsreplikat, das im Assistenten konfiguriert ist.  
  
> [!IMPORTANT]  
>  Wenn Sie die Verfügbarkeitsgruppe nicht mithilfe des **Assistenten für neue Verfügbarkeitsgruppen** erstellt haben, wird die alwayson_health-Sitzung möglicherweise nicht automatisch gestartet. Wenn die Sitzung nicht gestartet wird, können beim Auftreten eines unerwarteten Problems keine Ereignisdaten erfasst werden. Sie sollten die Sitzung manuell starten und für den automatischen Start konfigurieren, indem Sie die Sitzungseigenschaften konfigurieren.  
  
 So zeigen Sie die Definition der alwayson_health-Sitzung an  
  
1.  Erweitern Sie im **Objekt-Explorer** die Knoten **Verwaltung**, **Erweiterte Ereignisse** und **Sitzungen**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Alwayson_health**, zeigen Sie dann auf **Skript für Sitzung als** sowie auf **CREATE To**, und klicken Sie dann auf **Neues Abfrage-Editor-Fenster**.  

Informationen zu einigen der von alwayson_health abgedeckten Ereignisse finden Sie in der [Referenz zu erweiterten Ereignissen](always-on-extended-events.md#BKMK_Reference).  


##  <a name="BKMK_Debugging"></a> Erweiterte Ereignisse zum Debuggen  
 Neben den von der Alwayson_health-Sitzung abgedeckten erweiterten Ereignissen definiert SQL Server eine große Bandbreite an Debugereignissen für Verfügbarkeitsgruppen. Um diese zusätzlichen erweiterten Ereignisse in einer Sitzung nutzen zu können, führen Sie die folgenden Verfahren aus:  
  
1.  Erweitern Sie im **Objekt-Explorer** die Knoten **Verwaltung**, **Erweiterte Ereignisse** und **Sitzungen**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Sitzungen** , und wählen Sie anschließend **Neue Sitzung**. Klicken Sie alternativ mit der rechten Maustaste auf **Alwayson_health**, und wählen Sie **Eigenschaften** aus.  
  
3.  Klicken Sie im Fensterbereich **Seite auswählen** auf **Ereignisse**.  
  
4.  Wählen Sie in der Ereignisbibliothek in der Spalte **Kategorie** die Kategorie **alwayson** aus, und deaktivieren Sie alle anderen Kategorien.  
  
5.  Wählen Sie in der Spalte **Kanal** die Option **Debuggen** aus. Alle Ereignisse im Zusammenhang mit der Verfügbarkeitsgruppe, die noch nicht ausgewählt sind, werden nun in der Ereignisbibliothek angezeigt.  
  
6.  Markieren Sie ein Ereignis in der Ereignisbibliothek, und klicken Sie auf die Schaltfläche **>**, um es für die Sitzung auszuwählen.  
  
7.  Wenn Sie mit der Sitzung fertig sind, klicken Sie auf **OK**, um sie zu schließen. Stellen Sie sicher, dass die Sitzung gestartet wurde, damit sie die von Ihnen ausgewählten Ereignisse erfasst.  
  
##  <a name="BKMK_Reference"></a> Referenz zu erweiterten Ereignissen von Always On-Verfügbarkeitsgruppen  
 In diesem Abschnitt werden einige der erweiterten Ereignisse beschrieben, die zum Überwachen der Verfügbarkeitsgruppen verwendet werden.  
  
 [availability_replica_state_change](#BKMK_availability_replica_state_change)  
  
 [availability_group_lease_expired](#BKMK_availability_group_lease_expired)  
  
 [availability_replica_automatic_failover_validation](#BKMK_availability_replica_automatic_failover_validation)  
  
 [error_reported (mehrere Fehlernummern): bei Transport- oder Verbindungsproblemen](#BKMK_error_reported)  
  
 [data_movement_suspend_resume](#BKMK_data_movement_suspend_resume)  
  
 [alwayson_ddl_executed](#BKMK_alwayson_ddl_executed)  
  
 [availability_replica_manager_state](#BKMK_availability_replica_manager_state)  
  
 [error_reported (1480): Änderung von Datenbankreplikatsrollen](#BKMK_error_reported_1480)  
  
###  <a name="BKMK_availability_replica_state_change "></a> availability_replica_state_change  
 Tritt auf, wenn der Status eines Verfügbarkeitsreplikats geändert wurde. Dieses Ereignis kann durch Erstellen einer Verfügbarkeitsgruppe oder Verknüpfen eines Verfügbarkeitsreplikats ausgelöst werden. Es eignet sich für die Diagnose eines fehlerhaften automatischen Failovers. Zudem können damit auch die Failoverschritte nachverfolgt werden.  
  
#### <a name="event-information"></a>Informationen zu Ereignissen  
  
|Spalte|Description|  
|------------|-----------------|  
|Name|availability_replica_state_change|  
|Kategorie|alwayson|  
|Channel|Operational|  
  
#### <a name="event-fields"></a>Ereignisfelder  
  
|Name|Type_name|Description|  
|----------|----------------|-----------------|  
|availability_group_id|guid|Die ID der Verfügbarkeitsgruppe.|  
|availability_group_name|unicode_string|Der Name der Verfügbarkeitsgruppe.|  
|availability_replica_id|guid|Die ID des Verfügbarkeitsreplikats.|  
|previous_state|availability_replica_state|Die Rolle des Replikats vor der Änderung.<br /><br /> **Folgende Werte sind möglich:**<br /><br /> Primary_Normal<br /><br /> Secondary_Normal<br /><br /> Resolving_Pending_Failover<br /><br /> Resolving_Normal<br /><br /> Primary_Pending<br /><br /> Not_Available|  
|current_state|availability_replica_state|Die Rolle des Replikats nach der Änderung.<br /><br /> **Folgende Werte sind möglich:**<br /><br /> Primary_Normal<br /><br /> Secondary_Normal<br /><br /> Resolving_Pending_Failover<br /><br /> Resolving_Normal<br /><br /> Primary_Pending<br /><br /> Not_Available|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health-Sitzungsdefinition  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT availability_replica_state_change  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_availability_group_lease_expired"></a> availability_group_lease_expired  
 Tritt auf, wenn bei dem Cluster und der Verfügbarkeitsgruppe ein Konnektivitätsproblem auftritt und die Leasedauer abgelaufen ist. Dieses Ereignis zeigt an, dass die Konnektivität zwischen der Verfügbarkeitsgruppe und dem zugrunde liegenden WSFC-Cluster getrennt ist. Wenn das Konnektivitätsproblem beim primären Replikat auftritt, kann das Ereignis ein automatisches Failover auslösen oder dazu führen, dass die Verfügbarkeitsgruppe offline geschaltet wird.  
  
#### <a name="event-information"></a>Informationen zu Ereignissen  
  
|Spalte|Description|  
|------------|-----------------|  
|Name|availability_group_lease_expired|  
|Kategorie|alwayson|  
|Channel|Operational|  
  
#### <a name="event-fields"></a>Ereignisfelder  
  
|Name|Type_name|Description|  
|----------|----------------|-----------------|  
|availability_group_id|guid|Die ID der Verfügbarkeitsgruppe.|  
|availability_group_name|unicode_string|Der Name der Verfügbarkeitsgruppe.|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health-Sitzungsdefinition  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT availability_group_lease_expired  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_availability_replica_automatic_failover_validation"></a> availability_replica_automatic_failover_validation  
 Tritt auf, wenn das automatische Failover die Bereitschaft eines Verfügbarkeitsreplikats als primärem Replikat überprüft, und anzeigt, ob das Zielverfügbarkeitsreplikat als neues primäres Replikat bereit ist. Beispielsweise gibt die Failoverüberprüfung „false“ zurück, wenn nicht alle Datenbanken synchronisiert oder verknüpft sind. Dieses Ereignis ist für die Bereitstellung eines Single Point of Failure bei einem Failover konzipiert. Diese Informationen sind für den Datenbankadministrator von Interesse, insbesondere im Hinblick auf automatische Failover, da ein automatisches Failover ein unbeaufsichtigter Vorgang ist. Der Datenbankadministrator kann das Ereignis überprüfen, um festzustellen, warum bei einem automatischen Failover ein Fehler aufgetreten ist.  
  
#### <a name="event-information"></a>Informationen zu Ereignissen  
  
|Name|Description|  
|----------|-----------------|  
|availability_replica_automatic _failover_validation||  
|Kategorie|alwayson|  
|Channel|Analytic|  
  
#### <a name="event-fields"></a>Ereignisfelder  
  
|Name|Type_name|Description|  
|----------|----------------|-----------------|  
|availability_group_id|guid|Die ID der Verfügbarkeitsgruppe.|  
|availability_group_name|unicode_string|Der Name der Verfügbarkeitsgruppe.|  
|availability_replica_id|guid|Die ID des Verfügbarkeitsreplikats.|  
|forced_quorum|validation_result_type|Lautet der Wert TRUE, wird das automatische Failover für dieses Verfügbarkeitsreplikat unwirksam gemacht.<br /><br /> TRUE<br /><br /> FALSE|  
|joined_and_synchronized|validation_result_type|Lautet der Wert FALSE, wird das automatische Failover für dieses Verfügbarkeitsreplikat dann unwirksam gemacht.<br /><br /> TRUE<br /><br /> FALSE|  
|previous_primary_or_automatic_failover_target|validation_result_type|Lautet der Wert FALSE, wird das automatische Failover für dieses Verfügbarkeitsreplikat dann unwirksam gemacht.<br /><br /> TRUE<br /><br /> FALSE|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health-Sitzungsdefinition  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT availability_replica_automatic_failover_validation (  
WHERE (  
[forced_quorum]=(TRUE) OR [joined_and_synchronized]=(FALSE) OR [previous_primary_or_automatic_failover_target]=(TRUE)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
  
```  
  
###  <a name="BKMK_error_reported"></a> error_reported (mehrere Fehlernummern): bei Transport- oder Verbindungsproblemen  
 Jedes gefilterte Ereignis zeigt an, dass ein Konnektivitätsproblem beim Transport- oder Datenbankspiegelungsendpunkt, von dem diese Verfügbarkeitsgruppe abhängig ist, aufgetreten ist.  
  
|Spalte|Description|  
|------------|-----------------|  
|Name|error_reported<br /><br /> Zu filternde Zahlen: 35201, 35202, 35206, 35204, 35207, 9642, 9666, 9691, 9692, 9693, 28034, 28036, 28080, 28091, 33309|  
|Kategorie|errors|  
|Channel|Admin|  
  
#### <a name="error-numbers-to-filter"></a>Zu filternde Fehlernummern  
  
|Fehlernummer|Description|  
|------------------|-----------------|  
|35201|Bei dem Versuch, eine Verbindung mit dem Verfügbarkeitsreplikat '%ls' herzustellen, ist ein Timeout aufgetreten.|  
|35202|Für die Verfügbarkeitsgruppe '%ls' wurde erfolgreich eine Verbindung zwischen dem Verfügbarkeitsreplikat '%ls' mit der ID [%ls] und dem mit der ID [%ls] hergestellt.  Diese Meldung dient nur zu Informationszwecken. Es ist keine Benutzeraktion erforderlich.|  
|35206|Bei einer zuvor hergestellten Verbindung mit dem Verfügbarkeitsreplikat '%ls' ist ein Timeout aufgetreten.|  
|35204|Die Verbindung zwischen Instanz '%ls' und '%ls' wurde aufgrund des Vorgangs zum Herunterfahren eines Endpunkts deaktiviert.|  
|Timeout + verbunden|  
|35207|Fehler in der Verfügbarkeitsgruppe mit der ID '%ls'. Es konnte keine Verbindung zwischen Replikat-ID %ls' und Replikat-ID '%ls' hergestellt werden. Fehler: %d, Schweregrad: %d, Status: %d.  Schweregrad: %d, Status: %d. (Möglicherweise wurde die DBA nicht optimal eingesetzt. Überprüfen Sie dies, und entfernen Sie sie in diesem Fall.)|  
|9642|Fehler bei einem Verbindungsendpunkt des Transports für Service Broker/Datenbankspiegelung, Fehler: %i, Status: %i. (Nahe Endpunktrolle: %S_MSG, entfernte Endpunktadresse: '%.*hs') Fehler: %i Status: %i. (Nahe Endpunktrolle: %S_MSG, entfernte Endpunktadresse: '%.\*hs')|  
|9666|Der %S_MSG-Endpunkt befindet sich im Zustand „Deaktiviert“ oder „Beendet“.|  
|9691|Der %S_MSG-Endpunkt hat das Lauschen auf Verbindungen beendet.|  
|9692|Der %S_MSG-Endpunkt kann an Port %d nicht lauschen, weil er von einem anderen Prozess verwendet wird.|  
|9693|Der %S_MSG-Endpunkt kann aufgrund des folgenden Fehlers nicht auf Verbindungen lauschen: '%.*ls'.|  
|28034|Fehler beim Verbindungshandshake. Die Anmeldung '%.*ls' besitzt keine CONNECT-Berechtigung für den Endpunkt. Status %d.|  
|28036|Fehler beim Verbindungshandshake. Das von diesem Endpunkt verwendete Zertifikat wurde nicht gefunden: %S_MSG. Verwenden Sie DBCC CHECKDB in der master-Datenbank, um die Metadatenintegrität der Endpunkte zu überprüfen. Status %d.|  
|28080|Fehler beim Verbindungshandshake. Der Endpunkt '%S_MSG' ist nicht konfiguriert. Status %d.|  
|28091|Das Starten des Endpunkts für %S_MSG ohne Authentifizierung wird nicht unterstützt.|  
|33309|Der Clusterendpunkt kann nicht gestartet werden, weil die Standardkonfiguration des Endpunkts %S_MSG noch nicht geladen wurde.|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health-Sitzungsdefinition  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT sqlserver.error_reported(  
    WHERE   
(  
--Connectivity Error Messages  
[error_number]=(35201)   
OR [error_number]=(35202)   
OR [error_number]=(35204)   
OR [error_number]=(35206)   
OR [error_number]=(35207)   
OR [error_number]=(9642)   
--OR [error_number]=(9666)   
OR [error_number]=(9691)   
OR [error_number]=(9692)   
OR [error_number]=(9693)   
OR [error_number]=(28034)   
OR [error_number]=(28036)   
OR [error_number]=(28080)   
OR [error_number]=(28091)   
OR [error_number]=(33309)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_data_movement_suspend_resume"></a> data_movement_suspend_resume  
 Tritt auf, wenn die Datenbankverschiebung eines Datenbankreplikats angehalten oder fortgesetzt wird.  
  
#### <a name="event-information"></a>Informationen zu Ereignissen  
  
|Spalte|Description|  
|------------|-----------------|  
|Name|data_movement_suspend_resume|  
|Kategorie|Alwayson|  
|Channel|Operational|  
  
#### <a name="event-fields"></a>Ereignisfelder  
  
||||  
|-|-|-|  
|Name|Type_name|Description|  
|availability_group_id|guid|Die ID der Verfügbarkeitsgruppe.|  
|availability_group_name|unicode_string|Der Name der Verfügbarkeitsgruppe, falls vorhanden.|  
|availability_replica_id|guid|Die ID des Verfügbarkeitsreplikats.|  
|database_replica_id|guid|Die ID der Verfügbarkeitsdatenbank.|  
|database_replica_name|unicode_string|Der Name der Verfügbarkeitsdatenbank.|  
|database_id|uint32|Die ID der Verfügbarkeitsdatenbank.|  
|suspend_status|suspend_status_type|Die suspend_status-Werte.<br /><br /> SUSPEND_NULL<br /><br /> RESUMED<br /><br /> SUSPENDED<br /><br /> SUSPENDED_INVALID|  
|suspend_source|suspend_source_type|Die Quelle der Aktion zum Anhalten oder Fortsetzen.|  
|suspend_reason|unicode_string|Der Grund für die Aktion zum Anhalten, die im Datenbankreplikats-Manager erfasst wird.|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health-Sitzungsdefinition  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT data_movement_suspend_resume (  
WHERE (  
[suspend_status]=(SUSPENDED)or [suspend_status]=(SUSPENDED_INVALID) or   
[suspend_status]=(SUSPEND_NULL)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_alwayson_ddl_executed"></a> alwayson_ddl_executed  
 Tritt auf, wenn eine DLL-Anweisung (Data Definition Language, Datendefinitionssprache) einer Verfügbarkeitsgruppe ausgeführt wird, einschließlich einer CREATE-, ALTER- oder DROP-Anweisung. Die Hauptaufgabe des Ereignisses besteht darin, ein Problem mit einer Benutzeraktion für ein Verfügbarkeitsreplikat oder den Ausgangspunkt einer operativen Aktion anzugeben, an die im Anschluss ein Runtimeproblem auftritt (z.B. ein manuelles Failover, ein erzwungenes Failover, eine angehaltene Datenverschiebung oder eine fortgesetzte Datenverschiebung).  
  
#### <a name="event-information"></a>Informationen zu Ereignissen  
  
|Spalte|Description|  
|------------|-----------------|  
|Name|alwayson_ddl_execution|  
|Kategorie|alwayson|  
|Channel|Analytic|  
  
#### <a name="event-fields"></a>Ereignisfelder  
  
|Name|Type_name|Description|  
|----------|----------------|-----------------|  
|availability_group_id|Guid|Die ID der Verfügbarkeitsgruppe.|  
|availability_group_name|unicode_string|Der Name der Verfügbarkeitsgruppe.|  
|ddl_action|alwayson_ddl_action|Gibt den Typ der DDL-Aktion an: CREATE, ALTER oder DROP.|  
|ddl_phase|ddl_opcode|Gibt die Phase des DDL-Vorgangs an: BEGIN, COMMIT oder ROLLBACK.|  
|-Anweisung.|unicode_string|Der Text der ausgeführten Anweisung.|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health-Sitzungsdefinition  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT alwayson_ddl_executed  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_availability_replica_manager_state"></a> availability_replica_manager_state  
 Tritt auf, wenn der Status des Verfügbarkeitsreplikat-Managers geändert wurde. Dieses Ereignis gibt den Heartbeat des Verfügbarkeitsreplikat-Managers an. Wenn sich der Verfügbarkeitsreplikat-Manager nicht in einem fehlerfreien Zustand befindet, fallen alle Verfügbarkeitsreplikate in der SQL Server-Instanz aus.  
  
#### <a name="event-information"></a>Informationen zu Ereignissen  
  
|Spalte|Description|  
|------------|-----------------|  
|Name|availability_replica_manager_state_change|  
|Kategorie|alwayson|  
|Channel|Operational|  
  
#### <a name="event-fields"></a>Ereignisfelder  
  
|Name|Type_name|Description|  
|----------|----------------|-----------------|  
|current_state|manager_state|Der aktuelle Status des Verfügbarkeitsreplikat-Managers.<br /><br /> Online<br /><br /> Offline<br /><br /> WaitingForClusterCommunication|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health-Sitzungsdefinition  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT availability_replica_manager_state (  
WHERE ([current_state]=(OFFLINE))  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_error_reported_1480"></a> error_reported (1480): Änderung von Datenbankreplikatsrollen  
 Dieses gefilterte error_reported-Ereignis tritt asynchron auf, nachdem eine Verfügbarkeitsreplikatsrolle geändert wurde. Es gibt an, bei welcher Verfügbarkeitsdatenbank die erwartete Rolle während des Failoverprozesses nicht geändert werden konnte.  
  
#### <a name="event-information"></a>Informationen zu Ereignissen  
  
|Spalte|Description|  
|------------|-----------------|  
|Name|error_reported<br /><br /> Fehlernummer 1480: Bei der REPLICATION_TYPE_MSG-Datenbank „DATABASE_NAME“ werden aufgrund von REASON_MSG Rollen von „OLD_ROLE“ in „NEW_ROLE“ geändert.|  
|Kategorie|errors|  
|Channel|Admin|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health-Sitzungsdefinition  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT sqlserver.error_reported(  
    WHERE   
(  
--database replica role change message  
OR [error_number] = (1480)  
  
--database replica runtime error messages  
OR [error_number]=(823)   
OR [error_number]=(824)   
OR [error_number]=(829)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
## <a name="next-steps"></a>Nächste Schritte  
 [Anzeigen von Ereignissitzungsdaten](https://msdn.microsoft.com/library/hh710068(v=sql.110).aspx)   
 
  