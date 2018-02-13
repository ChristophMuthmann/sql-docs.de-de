---
title: sys.dm_hadr_database_replica_states (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/11/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_database_states_TSQL
- sys.dm_hadr_database_states
- dm_hadr_database_states
- dm_hadr_database_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_database_replica_states dynamic management view
ms.assetid: 1a17b0c9-2535-4f3d-8013-cd0a6d08f773
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c69d36319ca4273fad7b1c4890bf27e4e4fa0797
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="sysdmhadrdatabasereplicastates-transact-sql"></a>sys.dm_hadr_database_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Datenbank, die Teil ist in einer Always On-verfügbarkeitsgruppe zurück, für die der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein verfügbarkeitsreplikat hostet. Diese dynamische Verwaltungssicht macht Statusinformationen für sowohl primäre als auch sekundäre Replikate verfügbar. Auf einem sekundären Replikat gibt diese Sicht eine Zeile für jede sekundäre Datenbank der Serverinstanz zurück. Auf dem primären Replikat gibt diese Sicht eine Zeile für jede primäre Datenbank und eine zusätzliche Zeile für die entsprechende sekundäre Datenbank zurück.  
  
> [!IMPORTANT]
> Abhängig von der Aktion und den Statuswerten auf höherer Ebene sind Datenbankstatusinformationen möglicherweise nicht verfügbar oder veraltet. Zudem sind die Werte nur lokal relevant. Z. B. auf dem primären Replikat, den Wert von der **Last_hardened_lsn** Spalte wiedergibt, die Informationen zu einer bestimmten sekundären Datenbank, die derzeit für das primäre Replikat verfügbar ist, nicht den tatsächlichen festgeschriebene LSN-Wert, der Sekundäres Replikat möglicherweise derzeit.  
   
|Spaltenname|Datentyp|Beschreibung (auf primärem Replikat)|  
|-----------------|---------------|----------------------------------------|  
|**database_id**|**int**|Der Bezeichner der Datenbank, der innerhalb einer Instanz von SQL Server eindeutig ist. Dies ist der gleiche Wert wie angezeigt, in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt.|  
|**group_id**|**uniqueidentifier**|Der Bezeichner der Verfügbarkeitsgruppe, zu der die Datenbank gehört.|  
|**replica_id**|**uniqueidentifier**|Der Bezeichner des Verfügbarkeitsreplikats in der Verfügbarkeitsgruppe.|  
|**group_database_id**|**uniqueidentifier**|Der Bezeichner der Datenbank in der Verfügbarkeitsgruppe. Dieser Bezeichner ist auf jedem Replikat, mit dem diese Datenbank verknüpft ist, identisch.|  
|**is_local**|**bit**|Gibt an, ob die Verfügbarkeitsdatenbank lokal ist. Folgende Werte sind möglich:<br /><br /> 0 = Die Datenbank ist für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz nicht lokal.<br /><br /> 1 = Die Datenbank ist für die Serverinstanz lokal.|  
|**is_primary_replica**|**bit**|Gibt 1 zurück, wenn das Replikat primär ist, oder 0 bei einem sekundären Replikat.<br /><br />**Gilt für:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**synchronization_state**|**tinyint**|Status der datenverschiebung, einen der folgenden Werte.<br /><br /> 0 = nicht synchronisiert. Gibt bei einer primären Datenbank an, dass die Datenbank nicht bereit ist, das Transaktionsprotokoll mit den entsprechenden sekundären Datenbanken zu synchronisieren. Gibt bei einer sekundären Datenbank an, dass die Protokollsynchronisierung für die Datenbank aufgrund eines Verbindungsproblems nicht gestartet wurde oder beim Start oder einem Rollenwechsel verschiedene Übergangsstatuswerte durchläuft.<br /><br /> 1 = wird synchronisiert. Gibt bei einer primären Datenbank an, dass diese Datenbank bereit ist, eine Scananforderung von einer sekundären Datenbank zu akzeptieren. Gibt bei einer sekundären Datenbank an, dass eine aktive Datenverschiebung für die Datenbank erfolgt.<br /><br /> 2 = Synchronized. Primäre Datenbanken werden mit dem Status SYNCHRONISIERT und nicht mit dem Status WIRD SYNCHRONISIERT angezeigt. Eine sekundäre Datenbank mit synchronem Commit wird als SYNCHRONISIERT angezeigt, wenn gemäß dem lokalen Cache die Datenbank für das Failover bereit ist und eine Synchronisierung erfolgt.<br /><br /> 3 = zurücksetzen. Gibt die Rollbackphase an, wenn eine sekundäre Datenbank aktiv Seiten von der primären Datenbank abruft.<br />**Vorsicht:** Wenn eine Datenbank auf einem sekundären Replikat im Status REVERTING befindet, das Erzwingen eines Failovers zum sekundären Replikat belässt die Datenbank in einem Zustand, in dem er als primäre Datenbank gestartet werden kann nicht. Entweder muss erneut eine Verbindung mit der Datenbank als sekundäre Datenbank hergestellt werden, oder Sie müssen neue Protokolldatensätze aus einer Protokollsicherung übernehmen.<br /><br /> 4 = wird initialisiert. Gibt die Rollbackphase an, wenn das Transaktionsprotokoll (erforderlich, um eine sekundäre Datenbank auf den gleichen Stand wie die Rückgängig-LSN zu bringen) übermittelt und auf einem sekundären Replikat festgeschrieben wird.<br />**Vorsicht:** Wenn eine Datenbank auf einem sekundären Replikat den Status INITIALIZING aufweist, ist das Erzwingen eines Failovers auf dem sekundären Replikat bewirkt, dass der Datenbank in einem Zustand in der sie als primäre Datenbank gestartet werden. Entweder muss erneut eine Verbindung mit der Datenbank als sekundäre Datenbank hergestellt werden, oder Sie müssen neue Protokolldatensätze aus einer Protokollsicherung übernehmen.|  
|**synchronization_state_desc**|**nvarchar(60)**|Beschreibung des Datenverschiebungsstatus. Folgende Werte sind möglich:<br /><br /> NOT SYNCHRONIZING<br /><br /> SYNCHRONIZING<br /><br /> SYNCHRONIZED<br /><br /> REVERTING<br /><br /> INITIALIZING|  
|**is_commit_participant**|**bit**|0 = Ein Transaktionscommit wird nicht in Bezug auf diese Datenbank synchronisiert.<br /><br /> 1 = Ein Transaktionscommit wird in Bezug auf diese Datenbank synchronisiert.<br /><br /> Für eine Datenbank mit einem Verfügbarkeitsreplikat für asynchrone Commits muss dieser Wert immer 0 sein.<br /><br /> Bei einer Datenbank mit einem Verfügbarkeitsreplikat für synchrone Commits ist dieser Wert nur für die primäre Datenbank genau.|  
|**synchronization_health**|**tinyint**|Stellt den Synchronisierungsstatus einer Datenbank, die mit der verfügbarkeitsgruppe auf dem verfügbarkeitsreplikat verknüpft ist und den Verfügbarkeitsmodus des verfügbarkeitsreplikats (synchroner oder asynchroner Commit-Modus), eines der folgende Werte.<br /><br /> 0 = nicht fehlerfrei. Die **Synchronization_state** der Datenbank ist 0 (nicht synchronisiert).<br /><br /> 1 = teilweise fehlerfrei. Eine Datenbank auf ein verfügbarkeitsreplikat für synchrone Commits wird als teilweise fehlerfrei angesehen Wenn **Synchronization_state** 1 ist (SYNCHRONIZING).<br /><br /> 2 = Healthy. Eine Datenbank auf einem verfügbarkeitsreplikat für synchrone Commits wird als fehlerfrei angesehen, wenn **Synchronization_state** ist 2 (synchronisiert) und eine Datenbank auf einem verfügbarkeitsreplikat für asynchrone Commits wird als fehlerfrei angesehen, wenn **Synchronization_state** 1 ist (SYNCHRONIZING).|  
|**synchronization_health_desc**|**nvarchar(60)**|Beschreibung der **"synchronization_health"** der verfügbarkeitsdatenbank.<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**database_state**|**tinyint**|0 = Online<br /><br /> 1 = Wird wiederhergestellt<br /><br /> 2 = Wiederherstellung wird ausgeführt<br /><br /> 3 = Wiederherstellung steht aus<br /><br /> 4 = Fehlerverdächtig<br /><br /> 5 = Notfall<br /><br /> 6 = Offline<br /><br /> **Hinweis:** wie **Zustand** Spalte in ' sys.Databases '.|  
|**database_state_desc**|**nvarchar(60)**|Beschreibung der **Database_state** des verfügbarkeitsreplikats.<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> EMERGENCY<br /><br /> OFFLINE<br /><br /> **Hinweis:** wie **"state_desc"** Spalte in ' sys.Databases '.|  
|**is_suspended**|**bit**|Der Status der Datenbank. Folgende Werte sind möglich:<br /><br /> 0 = Fortgesetzt<br /><br /> 1 = Angehalten|  
|**suspend_reason**|**tinyint**|Gibt den Grund für das Anhalten an, wenn die Datenbank angehalten wurde. Folgende Werte sind möglich:<br /><br /> 0 = Benutzeraktion<br /><br /> 1 = Aussetzen für: Partner<br /><br /> 2 = Wiederholen<br /><br /> 3 = Erfassen<br /><br /> 4 = Übernehmen<br /><br /> 5 = Neu starten<br /><br /> 6 = Rückgängig<br /><br /> 7 = Erneute Überprüfung<br /><br /> 8 = Fehler bei der Berechnung des Synchronisierungspunkts des sekundären Replikats|  
|**suspend_reason_desc**|**nvarchar(60)**|Beschreibung des Grunds für das Anhalten der Datenbank. Folgende Werte sind möglich:<br /><br /> SUSPEND_FROM_USER = Die Datenverschiebung wurde von einem Benutzer manuell angehalten.<br /><br /> SUSPEND_FROM_PARTNER = Das Datenbankreplikat wurde nach einem erzwungenen Failover angehalten.<br /><br /> SUSPEND_FROM_REDO = Während der Rollforwardphase ist ein Fehler aufgetreten.<br /><br /> SUSPEND_FROM_APPLY = Beim Schreiben des Protokolls in die Datei ist ein Fehler aufgetreten (siehe Fehlerprotokoll).<br /><br /> SUSPEND_FROM_CAPTURE = Beim Aufzeichnen des Protokolls auf dem primären Replikat ist ein Fehler aufgetreten.<br /><br /> SUSPEND_FROM_RESTART = Das Datenbankreplikat wurde vor dem Neustart der Datenbank angehalten (siehe Fehlerprotokoll).<br /><br /> SUSPEND_FROM_UNDO = Während der Rollbackphase ist ein Fehler aufgetreten (siehe Fehlerprotokoll).<br /><br /> SUSPEND_FROM_REVALIDATION = Beim Wiederherstellen der Verbindung wurde ein Konflikt zwischen Protokolländerungen erkannt (siehe Fehlerprotokoll).<br /><br /> SUSPEND_FROM_XRF_UPDATE = Der allgemeine Protokollpunkt wurde nicht gefunden (siehe Fehlerprotokoll).|  
|**recovery_lsn**|**numeric(25,0)**|Beim primären Replikat das Ende des Transaktionsprotokolls, bevor die primäre Datenbank nach einer Wiederherstellung oder einem Failover neue Protokolldatensätze schreibt. Wenn dieser Wert bei einer angegebenen sekundären Datenbank kleiner als die aktuelle festgeschriebene LSN (last_hardened_lsn) ist, ist recovery_lsn der Wert, den die sekundäre Datenbank für die erneute Synchronisierung (d. h. zurücksetzen und erneut initialisieren) verwenden müsste. Wenn dieser Wert größer oder gleich der aktuellen festgeschriebenen LSN ist, wäre eine erneute Synchronisierung unnötig und würde nicht ausgeführt.<br /><br /> **Recovery_lsn** stellt eine Protokollblock-ID, die mit Nullen (0) dar. Es ist keine tatsächliche Protokollfolgenummer (LSN). Weitere Informationen dazu, wie dieser Wert abgeleitet wird, finden Sie unter [Grundlegendes zu LSN-Spaltenwerten](#LSNcolumns)weiter unten in diesem Thema.|  
|**truncation_lsn**|**numeric(25,0)**|Gibt für das primäre Replikat der primären Datenbank den Mindestwert für die Protokollkürzungs-LSN aller entsprechenden sekundären Datenbanken an. Wenn die lokale Protokollkürzung blockiert wird (z. B. durch einen Sicherungsvorgang), kann diese LSN größer als die lokale Kürzungs-LSN sein.<br /><br /> Stellt bei einer bestimmten sekundären Datenbank den Protokollkürzungspunkt dieser Datenbank dar.<br /><br /> **Truncation_lsn** stellt eine Protokollblock-ID, die mit Nullen (0) dar. Es ist keine tatsächliche Protokollfolgenummer.|  
|**last_sent_lsn**|**numeric(25,0)**|Der Protokollblockbezeichner, der den Punkt angibt, bis zu den alle Protokollblöcke von der primären Datenbank gesendet wurden. Dies ist die ID des nächsten Protokollblocks, der gesendet wird, und nicht die ID des zuletzt gesendeten Protokollblocks.<br /><br /> **Last_sent_lsn** eine Protokollblock-ID wiedergibt mit Nullen aufgefüllt, es ist keine tatsächliche protokollfolgenummer.|  
|**last_sent_time**|**datetime**|Die Zeit, zu der der letzte Protokollblock gesendet wurde.|  
|**last_received_lsn**|**numeric(25,0)**|Die Protokollblock-ID, die den Punkt angibt, bis zu dem alle Protokollblöcke vom sekundären Replikat empfangen wurden, das diese sekundäre Datenbank hostet.<br /><br /> **Last_received_lsn** stellt eine Protokollblock-ID, die mit Nullen (0) dar. Es ist keine tatsächliche Protokollfolgenummer.|  
|**last_received_time**|**datetime**|Die Zeit, zu der die in der letzten Meldung empfangene Protokollblock-ID auf dem sekundären Replikat gelesen wurde.|  
|**last_hardened_lsn**|**numeric(25,0)**|Start des Protokollblocks, der die Protokolldatensätze der letzten festgeschriebenen LSN für eine sekundären Datenbank enthält.<br /><br /> Für eine primäre Datenbank mit asynchronem Commit oder synchronem Commit, deren aktuelle Richtlinie "Verzögerung" ist, lautet der Wert NULL. Für andere primären Datenbanken mit synchronem Commit **Last_hardened_lsn** gibt den Mindestwert der festgeschriebenen LSN für alle sekundären Datenbanken an.<br /><br /> **Hinweis: Last_hardened_lsn** stellt eine Protokollblock-ID, die mit Nullen (0) dar. Es ist keine tatsächliche Protokollfolgenummer. Weitere Informationen finden Sie unter [Grundlegendes zu LSN-Spaltenwerten](#LSNcolumns)weiter unten in diesem Thema.|  
|**last_hardened_time**|**datetime**|In einer sekundären Datenbank, Zeitpunkt der der protokollblockbezeichner für die letzte festgeschriebene LSN (**Last_hardened_lsn**). Gibt für eine primäre Datenbank die Zeit an, die der festgeschriebenen LSN mit dem Mindestwert entspricht.|  
|**last_redone_lsn**|**numeric(25,0)**|Tatsächliche Protokollfolgenummer des letzten Protokolldatensatzes, der zuletzt für die sekundäre Datenbank wiederholt wurde. **Last_redone_lsn** ist immer kleiner als **Last_hardened_lsn**.|  
|**last_redone_time**|**datetime**|Die Zeit, zu der der letzte Protokolldatensatz in der sekundären Datenbank wiederholt wurde.|  
|**log_send_queue_size**|**bigint**|Die Menge der Protokolldatensätze der primären Datenbank, die noch nicht an die sekundären Datenbanken gesendet wurden (in KB).|  
|**log_send_rate**|**bigint**|Dies ist die durchschnittliche Rate an, welche primären Replikat Instanz gesendeten Daten während der letzten aktiven Zeitraum, in Kilobyte (KB) / Sekunde.|  
|**redo_queue_size**|**bigint**|Die Größe der Protokolldatensätze in den Protokolldateien des sekundären Replikats, das noch nicht wiederholt wurde (in KB).|  
|**redo_rate**|**bigint**|Rate, mit der die Protokolldatensätze für eine angegebene sekundäre Datenbank wiederholt werden (in KB/s).|  
|**filestream_send_rate**|**bigint**|Die Rate in KB/Sekunde, mit der die FILESTREAM-Dateien an das sekundäre Replikat übertragen werden.|  
|**end_of_log_lsn**|**numeric(25,0)**|Lokale Protokollende-LSN. Die tatsächliche LSN, die dem letzten Protokolldatensatz im Protokollcache der primären und sekundären Datenbanken entspricht. Für das primäre Replikat geben die sekundären Zeilen die Protokollende-LSN der letzten Statusmeldungen an, die die sekundären Replikate an das primäre Replikat gesendet haben.<br /><br /> **End_of_log_lsn** stellt eine Protokollblock-ID, die mit Nullen (0) dar. Es ist keine tatsächliche Protokollfolgenummer. Weitere Informationen finden Sie unter [Grundlegendes zu LSN-Spaltenwerten](#LSNcolumns)weiter unten in diesem Thema.|  
|**last_commit_lsn**|**Numeric(25,0)**|Tatsächliche Protokollfolgenummer, die dem letzten Commitdatensatz im Transaktionsprotokoll entspricht.<br /><br /> Entspricht bei der primären Datenbank dem zuletzt verarbeiteten Commitdatensatz. In den Zeilen für sekundäre Datenbanken wird die Protokollfolgenummer angezeigt, die das sekundäre Replikat dem primären Replikat gesendet hat.<br /><br /> Beim sekundären Replikat ist dies der letzte Commitdatensatz, der wiederholt wurde.|  
|**last_commit_time**|**datetime**|Die Zeit, die dem letzten Commitdatensatz entspricht.<br /><br /> Bei der sekundären Datenbank ist diese Zeit mit der für die primäre Datenbank identisch.<br /><br /> Auf dem primären Replikat zeigt jede Zeile für die sekundäre Datenbank die Zeit an, die das sekundäre Replikat, das die sekundäre Datenbank hostet, dem primären Replikat zurückgemeldet hat. Der Zeitunterschied zwischen der Zeile für die primäre Datenbank und der Zeile einer bestimmten sekundären Datenbank stellt die ungefähre Wiederherstellungszeit-Zielsetzung dar. Es wird angenommen, dass der Wiederholungsprozess abgefangen wird und dass der Fortschritt vom sekundären Replikat an das primäre Replikat zurückgemeldet wurde.|  
|**low_water_mark_for_ghosts**|**bigint**|Eine monoton steigende Zahl für die Datenbank, die eine Untergrenze angibt, die für das Cleanup inaktiver Datensätze verwendet wurde. Wenn diese Zahl im Zeitverlauf nicht zunimmt, weist dies darauf hin, dass das Cleanup für inaktive Datensätze möglicherweise nicht erfolgt ist. Um zu entscheiden, welche Zeilen mit inaktiven Datensätzen bereinigt werden sollen, verwendet das primäre Replikat den Mindestwert dieser Spalte für alle Verfügbarkeitsreplikate (einschließlich des primären Replikats) für diese Datenbank.|  
|**secondary_lag_seconds**|**bigint**|Die Anzahl der Sekunden an, denen das sekundäre Replikat hinter das primäre Replikat während der Synchronisierung wird.<br /><br />**Gilt für:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
##  <a name="LSNcolumns"></a> Grundlegendes zu LSN-Spaltenwerten  
 Die Werte der **End_of_log_lsn**, **Last_hardened_lsn**, **Last_received_lsn**, **Last_sent_lsn**, **Wiederherstellung _lsn**, und **Truncation_lsn** Spalten sind keine tatsächlichen protokollfolgenummern (LSNs). Diese Werte stellen eine mit Nullen aufgefüllte Protokollblock-ID dar.  
  
 **End_of_log_lsn**, **Last_hardened_lsn**, und **Recovery_lsn** sind leerungs-LSNs. Beispielsweise **Last_hardened_lsn** zeigt den Beginn des nächsten Blocks hinter den Blöcken an, die bereits auf dem Datenträger vorhanden sind.  Daher ist jede LSN < dem Wert des **Last_hardened_lsn** ist auf dem Datenträger.  Eine LSN, die >= diesem Wert ist, wird nicht geleert.  
  
 Der zurückgegebene LSN-Werte **dm_hadr_database_replica_states**, nur **Last_redone_lsn** eine tatsächliche LSN.  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
