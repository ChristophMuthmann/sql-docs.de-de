---
title: Sys. dm_hadr_availability_replica_states (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_states
- sys.dm_hadr_availability_replica_states_TSQL
- sys.dm_hadr_availability_replica_states
- dm_hadr_availability_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_replica_states dynamic management view
ms.assetid: d2e678bb-51e8-4a61-b223-5c0b8d08b8b1
caps.latest.revision: 65
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 49ed5ae45fcd3f5c760481a4dce85f8a5bd8e5a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmhadravailabilityreplicastates-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede lokale Replikat und eine Zeile für jede remotereplikat in derselben AlwaysOn-verfügbarkeitsgruppe wie ein lokales Replikat zurück. Jede Zeile enthält Informationen über den Status eines bestimmten Replikats.  
  
> [!IMPORTANT]  
>  Um Informationen zu jedem Replikat in einer bestimmten verfügbarkeitsgruppe abzurufen, Fragen **Sys. dm_hadr_availability_replica_states** auf der Serverinstanz, die das primäre Replikat gehostet wird. Findet die Abfrage in einer Serverinstanz statt, die ein sekundäres Replikat einer Verfügbarkeitsgruppe hostet, gibt diese dynamische Verwaltungssicht nur lokale Informationen für die Verfügbarkeitsgruppe zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Eindeutiger Bezeichner des Replikats.|  
|**group_id**|**uniqueidentifier**|Eindeutiger Bezeichner der Verfügbarkeitsgruppe.|  
|**is_local**|**bit**|Gibt an, ob das Replikat wird eine der:<br /><br /> 0 = Gibt ein sekundäres Remotereplikat in einer Verfügbarkeitsgruppe an, deren primäres Replikat von der lokalen Serverinstanz gehostet wird. Dieser Wert kommt nur am primären Replikatspeicherort vor.<br /><br /> 1 = gibt ein lokales Replikat. Auf sekundären Replikaten ist dies der einzige verfügbare Wert für die Verfügbarkeitsgruppe, zu der das Replikat gehört.|  
|**Rolle ""**|**tinyint**|Aktuelle [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] Rolle ein lokales Replikat oder ein verbundenen remotereplikat, eine der:<br /><br /> 0 = Wird aufgelöst<br /><br /> 1 = Primär<br /><br /> 2 = Sekundär<br /><br /> Informationen über [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Rollen finden Sie unter [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|**role_desc**|**nvarchar(60)**|Beschreibung des **Rolle**, eine von:<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|Aktuellen Betriebszustand des eines Replikats:<br /><br /> 0 = Ausstehendes Failover<br /><br /> 1 = Ausstehend<br /><br /> 2 = Online<br /><br /> 3 = Offline<br /><br /> 4 = Fehler<br /><br /> 5 = Fehler, kein Quorum<br /><br /> NULL = Das Replikat ist nicht lokal.<br /><br /> Weitere Informationen finden Sie unter [Rollen und Betriebszustände](#RolesAndOperationalStates)weiter unten in diesem Thema.|  
|**operational\_state\_desc**|**nvarchar(60)**|Beschreibung des **operational\_Status**, eine von:<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**Wiederherstellung\_Integrität**|**tinyint**|Rollup der **Datenbank\_Zustand** Spalte die [Sys. dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) -verwaltungssicht. Im folgenden sind die möglichen Werte und deren Beschreibungen.<br /><br /> 0: in Bearbeitung.  Mindestens eine verknüpfte Datenbank verfügt über einen anderen Datenbankstatus als ONLINE (**Datenbank\_Zustand** ist nicht 0 ist).<br /><br /> 1: online. Alle verknüpften Datenbanken haben den Datenbankstatus ONLINE (**Database_state** ist 0).<br /><br /> NULL: **Is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|Beschreibung des **Recovery_health**, eine von:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**Synchronisierung\_Integrität**|**tinyint**|Stellt ein Rollup von der datenbanksynchronisierungsstatus (**Synchronization_state**) aller verknüpften verfügbarkeitsdatenbanken (auch bekannt als *Replikate*) und den Verfügbarkeitsmodus für das Replikat () synchroner oder asynchroner Commit-Modus). Das Rollup wider der am wenigsten fehlerfreien akkumulierten Status der Datenbanken auf dem Replikat. Im folgenden sind die möglichen Werte und deren Beschreibungen.<br /><br /> 0: nicht fehlerfrei.   Mindestens eine verknüpfte Datenbank weist den Status NOT SYNCHRONIZING auf.<br /><br /> 1: teilweise fehlerfrei. Einige Replikate befinden sich nicht im Zielsynchronisierungsstatus: Replikate mit synchronem Commit sollten synchronisiert sein, und Replikate mit asynchronem Commit sollten synchronisiert werden.<br /><br /> 2: fehlerfrei. Alle Replikate befinden sich im Zielsynchronisierungsstatus: Replikate mit synchronem Commit sind synchronisiert, und Replikate mit asynchronem Commit werden synchronisiert.|  
|**synchronization_health_desc**|**nvarchar(60)**|Beschreibung des **"synchronization_health"**, eine von:<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|Gibt an, ob ein sekundäres Replikat derzeit mit dem primären Replikat verbunden ist. Die möglichen Werte werden mit ihren Beschreibungen unten gezeigt.<br /><br /> 0: getrennt. Die Antwort des eines verfügbarkeitsreplikats auf den Status DISCONNECTED hängt von dessen Rolle: auf dem primären Replikat ein sekundäres Replikat getrennt ist, ihre sekundären Datenbanken werden markiert, als NOT SYNCHRONIZED auf dem primären Replikat wartet, bis das sekundäre erneut eine Verbindung herstellen; Auf einem sekundären Replikat wird erkannt, dass getrennt ist versucht das sekundäre Replikat mit dem primären Replikat wiederherzustellen.<br /><br /> 1: verbunden.<br /><br /> Jedes primäre Replikat verfolgt den Verbindungsstatus für jedes sekundäre Replikat in der gleichen Verfügbarkeitsgruppe nach. Sekundäre Replikate verfolgen nur den Verbindungsstatus des primären Replikats nach.|  
|**connected_state_desc**|**nvarchar(60)**|Beschreibung des **Connection_state**, eine von:<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|Die Nummer des letzten Verbindungsfehlers.|  
|**last_connect_error_description**|**nvarchar(1024)**|Der Text der **Last_connect_error_number** Nachricht.|  
|**last_connect_error_timestamp**|**datetime**|Datums- und Zeitstempel, der angibt, wann die **Last_connect_error_number** Fehler aufgetreten ist.|  
  
##  <a name="RolesAndOperationalStates"></a> Rollen und Betriebszustände  
 Die Rolle **Rolle**, gibt den Status eines bestimmten verfügbarkeitsreplikats und den Betriebsstatus wieder **Operational_state**, beschreibt, ob das Replikat bereit ist, für alle Clientanforderungen verarbeiten ist die die Datenbank des verfügbarkeitsreplikats. Im folgenden finden Sie eine Zusammenfassung der Betriebszustände, die für jede Rolle möglich sind: RESOLVING, PRIMARY und SECONDARY.  
  
 **RESOLVING:** bei der ein verfügbarkeitsreplikat die Rolle RESOLVING ist, sind folgende Betriebszustände möglich, wie in der folgenden Tabelle gezeigt.  
  
|Betriebszustand|Description|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|Derzeit wird ein Failoverbefehl für die Verfügbarkeitsgruppe verarbeitet.|  
|OFFLINE|Alle Konfigurationsdaten für das Verfügbarkeitsreplikat wurden im WSFC-Cluster und auch in den lokalen Metadaten aktualisiert, aber in der Verfügbarkeitsgruppe fehlt derzeit ein primäres Replikat.|  
|FAILED|Beim Versuch, Informationen aus dem WSFC-Cluster abzurufen, ist ein Lesefehler aufgetreten.|  
|FAILED_NO_QUORUM|Der lokale wsfc-Knoten ist kein Quorum besitzt. Dies ist ein abgeleiteter Status.|  
  
 **PRIMARY:** Wenn ein verfügbarkeitsreplikat die primäre Rolle ausführt, ist derzeit das primäre Replikat. Folgende Betriebszustände möglich sind, wie in der folgenden Tabelle gezeigt.  
  
|Betriebszustand|Description|  
|-----------------------|-----------------|  
|PENDING|Dies ist ein vorübergehender Status, aber ein primäres Replikat kann in diesem Status hangen bleiben, wenn keine Arbeitsthreads zum Verarbeiten der Anforderungen verfügbar sind.|  
|ONLINE|Die Verfügbarkeitsgruppenressource ist online, und alle Datenbankarbeitsthreads wurden abgerufen.|  
|FAILED|Das Verfügbarkeitsreplikat kann nicht aus dem WSFC-Cluster lesen oder in den WSFC-Cluster schreiben.|  
  
 **SECONDARY:** bei der ein verfügbarkeitsreplikat die sekundäre Rolle spielt, er ist derzeit ein sekundäres Replikat. Folgende Betriebszustände möglich sind, wie in der folgenden Tabelle gezeigt.  
  
|Betriebszustand|Description|  
|-----------------------|-----------------|  
|ONLINE|Das lokale sekundäre Replikat ist mit dem primären Replikat verbunden.|  
|FAILED|Das lokale sekundäre Replikat kann nicht aus dem WSFC-Cluster lesen oder in den WSFC-Cluster schreiben.|  
|NULL|Auf einem primären Replikat wird dieser Wert zurückgegeben, wenn sich die Zeile auf ein sekundäres Replikat bezieht.|  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
