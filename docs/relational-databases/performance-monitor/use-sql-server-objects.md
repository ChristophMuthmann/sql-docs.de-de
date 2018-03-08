---
title: Verwenden von SQL Server-Objekten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- server performance [SQL Server], objects for monitoring
- database monitoring [SQL Server], objects for monitoring
- charts [SQL Server]
- System Monitor [SQL Server], counters
- counters [SQL Server], listed
- objects [SQL Server], performance monitoring
- objects [SQL Server], Windows System Monitor
- performance counters [SQL Server], about performance counters
- System Monitor [SQL Server], objects
- performance counters [SQL Server]
- counters [SQL Server], about performance counters
- tuning databases [SQL Server], objects for monitoring
- database performance [SQL Server], objects for monitoring
- SQL Server, objects
- monitoring performance [SQL Server], objects for monitoring
- Windows System Monitor [SQL Server], objects
- Windows System Monitor [SQL Server], counters
- counters [SQL Server]
- performance counters [SQL Server], listed
ms.assetid: bcd731b1-3c4e-4086-b58a-af7a3af904ad
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4a11f27ebd08fc7d1e7377f7d84fb5e3f95f4e13
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="use-sql-server-objects"></a>Verwenden von SQL Server-Objekten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Objekte und Leistungsindikatoren bereitgestellt, die vom Systemmonitor zum Überwachen der Aktivität von Computern, die eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausführen, verwendet werden können. Ein Objekt ist eine beliebige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ressource, z.B. eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sperre oder ein Windows-Prozess. Jedes Objekt enthält einen oder mehrere Leistungsindikatoren, die verschiedene Aspekte der zu überwachenden Objekte ermitteln. So enthält z.B. das Objekt **SQL Server-Sperren** Leistungsindikatoren für die **Anzahl der Deadlocks/Sekunde** und die **Sperrtimeouts/Sekunde**.  
  
 Einige Objekte verfügen über mehrere Instanzen, wenn mehrere Ressourcen eines bestimmten Typs auf dem Computer vorhanden sind. So weist z.B. der Objekttyp **Prozessor** mehrere Instanzen auf, wenn ein System über mehrere Prozessoren verfügt. Der Objekttyp **Datenbanken** verfügt über eine Instanz für jede Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Einige Objekttypen (z.B. für den **Speicher-Manager** ) verfügen nur über eine Instanz. Wenn ein Objekttyp über mehrere Instanzen verfügt, können Sie Leistungsindikatoren hinzufügen, um die Statistiken für jede Instanz (oder in vielen Fällen für alle Instanzen gleichzeitig) nachzuverfolgen. Leistungsindikatoren für die Standardinstanz werden im Format **SQLServer:***\<Objektname>* angezeigt. Leistungsindikatoren für benannte Instanzen werden im Format **MSSQL$***\<Instanzname>***:***\<Indikatorname>* oder **SQLAgent$***\<Instanzname>***:***\<Indikatorname>* angezeigt.  
  
 Durch Hinzufügen oder Entfernen von Leistungsindikatoren zum bzw. aus dem Diagramm und Speichern der Diagrammeinstellungen können Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte und -Leistungsindikatoren angeben, die beim Starten des Systemmonitors überwacht werden.  
  
 Sie können den Systemmonitor so konfigurieren, dass Statistiken von jedem beliebigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Leistungsindikator angezeigt werden. Darüber hinaus können Sie einen Schwellenwert für jeden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Leistungsindikator festlegen und anschließend eine Warnung generieren, wenn ein Leistungsindikator einen Schwellenwert überschreitet. Weitere Informationen zum Einrichten von Warnungen finden Sie unter [Erstellen einer SQL Server-Datenbankwarnung](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md).  
  
> [!TIP]  
>  Sie können die Leistungsindikatorwerte auch zurückgeben, indem Sie die dynamische Verwaltungssicht [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) abfragen.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Statistiken werden nur angezeigt, wenn eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist. Wenn Sie eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]anhalten und neu starten, wird die Anzeige der Statistiken unterbrochen und anschließend automatisch fortgesetzt. Beachten Sie außerdem, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Leistungsindikatoren im Systemmonitor-Snap-In angezeigt werden, selbst wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht ausgeführt wird. Bei einer gruppierten Instanz sind Leistungsindikatoren nur auf dem Knoten funktionsfähig, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Leistungsobjekte für den SQL Server-Agent](#SQLServerAgentPOs)  
  
-   [Service Broker-Leistungsobjekte](#ServiceBrokerPOs)  
  
-   [SQL Server-Leistungsobjekte](#SQLServerPOs)  
  
-   [Leistungsobjekte für die SQL Server-Replikation](#SQLServerReplicationPOs)  
  
-   [SSIS-Pipelineleistungsindikatoren](#SsisPipelineCounters)  
  
-   [Erforderliche Berechtigungen](#RequiredPermissions)  
  
##  <a name="SQLServerAgentPOs"></a> Leistungsobjekte für den SQL Server-Agent  
 In der folgenden Tabelle sind die Leistungsobjekte für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent aufgeführt:  
  
|Leistungsobjekt|Description|  
|------------------------|-----------------|  
|[SQLAgent:Warnungen](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|Stellt Informationen zu Warnungen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents bereit.|  
|[SQLAgent:Aufträge](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|Stellt Informationen zu Aufträgen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents bereit.|  
|[SQLAgent:Auftragsschritte](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|Stellt Informationen zu Auftragsschritten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents bereit.|  
|[SQLAgent:Statistik](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|Stellt allgemeine Informationen zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent bereit.|  
  
##  <a name="ServiceBrokerPOs"></a> Service Broker-Leistungsobjekte  
 In der folgenden Tabelle sind die Leistungsobjekte für [!INCLUDE[ssSB](../../includes/sssb-md.md)]aufgeführt.  
  
|Leistungsobjekt|Description|  
|------------------------|-----------------|  
|[SQLServer:Broker-Aktivierung](../../relational-databases/performance-monitor/sql-server-broker-activation-object.md)|Stellt Informationen zu aktivierten [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Tasks bereit.|  
|[SQLServer:Broker-Statistik](../../relational-databases/performance-monitor/sql-server-broker-statistics-object.md)|Stellt allgemeine Informationen zu [!INCLUDE[ssSB](../../includes/sssb-md.md)] bereit.|  
|[SQLServer:Broker-Transport](../../relational-databases/performance-monitor/sql-server-broker-dbm-transport-object.md)|Stellt Informationen zum [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Netzwerk bereit.|  
  
##  <a name="SQLServerPOs"></a> SQL Server-Leistungsobjekte  
 In der folgenden Tabelle werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte beschrieben.  
  
|Leistungsobjekt|Description|  
|------------------------|-----------------|  
|[SQLServer:Zugriffsmethoden](../../relational-databases/performance-monitor/sql-server-access-methods-object.md)|Durchsucht und misst die Anzahl der Zuordnungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankobjekten (z.B. die Anzahl von Indexsuchläufen oder die Anzahl von Seiten, die Indizes und Daten zugeordnet sind).|  
|[SQLServer:Sicherungsmedium](../../relational-databases/performance-monitor/sql-server-backup-device-object.md)|Stellt Informationen über Sicherungsmedien bereit, die von Sicherungs- und Wiederherstellungsvorgängen verwendet werden, z. B. über den Durchsatz des Sicherungsmediums.|  
|[SQL Server: Statistiken zu Batchantworten](../../relational-databases/performance-monitor/sql-server-batch-resp-statistics-object.md)|Leistungsindikatoren zum Nachverfolgen der SQL-Batchantwortzeiten.| 
|[SQLServer:Puffer-Manager](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)|Stellt Informationen über die Speicherpuffer bereit, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden, z.B. **freier Arbeitsspeicher** und **Puffercache-Trefferquote**.|  
|[SQLServer: Buffer Node](../../relational-databases/performance-monitor/sql-server-buffer-node.md)|Stellt Informationen dazu bereit, wie oft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] freie Seiten anfordert und auf diese zugreift.|  
|[SQLServer: Katalogmetadaten](../../relational-databases/performance-monitor/sql-server-catalog-metadata-object.md)|Definiert einen Objektmanager für Katalogmetadaten für SQL Server.| 
|[SQLServer:CLR](../../relational-databases/performance-monitor/sql-server-clr-object.md)|Stellt Informationen über die Common Language Runtime (CLR) bereit.|  
|[SQLServer:Columnstore](../../relational-databases/performance-monitor/sql-server-columnstore-object.md)|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> Stellt Informationen zu Zeilengruppen und Segmenten für Columnstore-Indizes bereit.|  
|[SQLServer:Cursor-Manager nach Typ](../../relational-databases/performance-monitor/sql-server-cursor-manager-by-type-object.md)|Stellt Informationen zu Cursorn bereit.|  
|[SQLServer:Cursor-Manager gesamt](../../relational-databases/performance-monitor/sql-server-cursor-manager-total-object.md)|Stellt Informationen zu Cursorn bereit.|  
|[SQLServer:Datenbankspiegelung](../../relational-databases/performance-monitor/sql-server-database-mirroring-object.md)|Stellt Informationen zur Datenbankspiegelung bereit.|  
|[SQLServer:Datenbanken](../../relational-databases/performance-monitor/sql-server-databases-object.md)|Stellt Informationen zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank bereit, z.B. zum Umfang des freien Protokollspeichers oder zur Anzahl aktiver Transaktionen in der Datenbank. Es kann mehrere Instanzen dieses Objekts geben.|  
|[SQL Server:Als veraltet markierte Funktionen](../../relational-databases/performance-monitor/sql-server-deprecated-features-object.md)|Zählt, wie oft veraltete Funktionen verwendet werden.|  
|[SQLServer:Ausführungsstatistik](../../relational-databases/performance-monitor/sql-server-execstatistics-object.md)|Stellt Informationen zur Ausführungsstatistik bereit.|  
|[SQL Server:Externe Skripts](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> Stellt Informationen zur externen Skriptausführung bereit.|  
|[SQLServer: FileTable](../../relational-databases/performance-monitor/sql-server-filetable-object.md)|Mit „FileTable“ verknüpfte Statistiken und nicht transaktionsgebundener Zugriff.|  
|[SQLServer, Allgemeine Statistik](../../relational-databases/performance-monitor/sql-server-general-statistics-object.md)|Stellt Informationen zur allgemeinen serverweiten Aktivität bereit, z. B. die Anzahl von Benutzern, die mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verbunden sind.|  
|[SQL Server:HADR-Verfügbarkeitsreplikat](../../relational-databases/performance-monitor/sql-server-availability-replica.md)|Stellt Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] -Verfügbarkeitsreplikaten bereit.|  
|[SQL Server:HADR-Datenbankreplikat](../../relational-databases/performance-monitor/sql-server-database-replica.md)|Stellt Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] -Datenbankreplikaten bereit.|  
|[SQLServer:Latches](../../relational-databases/performance-monitor/sql-server-latches-object.md)|Stellt Informationen zu Latches auf internen Ressourcen (z. B. Datenbankseiten) bereit, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden.|  
|[SQLServer:Sperren](../../relational-databases/performance-monitor/sql-server-locks-object.md)|Stellt Informationen zu einzelnen Sperranforderungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bereit, z.B. Timeouts für Sperren und Deadlocks. Es kann mehrere Instanzen dieses Objekts geben.|  
|[SQLServer: LogPool FreePool](../../relational-databases/performance-monitor/sql-server-logpool-freepool-object.md)|Beschreibt Statistiken für den freien Pool innerhalb des Protokollpools.|
|[SQLServer: Speicherbrokerclerks](../../relational-databases/performance-monitor/sql-server-memory-broker-clerks-object.md)|Statistiken zu Speicherbrokerclerks.|
|[SQLServer:Speicher-Manager](../../relational-databases/performance-monitor/sql-server-memory-manager-object.md)|Stellt Informationen zur Speicherauslastung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereit, z.B. die Gesamtanzahl der aktuell zugewiesenen Sperrstrukturen.|  
|[SQLServer:Plancache](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)|Stellt Informationen zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Cache bereit, der zum Speichern von Objekten wie gespeicherten Prozeduren, Triggern und Abfrageplänen verwendet wird.|  
|[SQLServer: Abfragespeicher](../../relational-databases/performance-monitor/sql-server-query-store-object.md)|Stellt Informationen zum Abfragespeicher bereit.|  
|[SQLServer:Statistiken für Ressourcenpools](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)|Stellt Informationen über Statistiken für Ressourcenpools in der Ressourcenkontrolle bereit.|  
|[SQLServer:SQL-Fehler](../../relational-databases/performance-monitor/sql-server-sql-errors-object.md)|Stellt Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlern bereit.|  
|[SQLServer:SQL-Statistik](../../relational-databases/performance-monitor/sql-server-sql-statistics-object.md)|Stellt Informationen zu Aspekten von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen bereit, z.B. die Anzahl von Batches von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]empfangen hat.|  
|[SQLServer:Transaktionen](../../relational-databases/performance-monitor/sql-server-transactions-object.md)|Stellt Informationen zu den aktiven Transaktionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bereit, z.B. die Gesamtanzahl von Transaktionen und die Anzahl von Momentaufnahmetransaktionen.|  
|[SQLServer:Benutzerdefinierbar](../../relational-databases/performance-monitor/sql-server-user-settable-object.md)|Führt eine benutzerdefinierte Überwachung aus. Jeder Leistungsindikator kann eine benutzerdefinierte gespeicherte Prozedur oder eine beliebige [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung sein, die einen Wert zurückgibt, der überwacht werden soll.|  
|[SQLSERVER: Wartestatistik](../../relational-databases/performance-monitor/sql-server-wait-statistics-object.md)|Stellt Informationen zu Wartezeiten bereit.|  
|[SQLServer:Statistiken für Arbeitsauslastungsgruppen](../../relational-databases/performance-monitor/sql-server-workload-group-stats-object.md)|Stellt Informationen zur Ressourcenkontrollen-Arbeitsauslastungsgruppenstatistik bereit.|  
  
##  <a name="SQLServerReplicationPOs"></a> Leistungsobjekte für die SQL Server-Replikation  
 In der folgenden Tabelle sind die Leistungsobjekte für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation aufgeführt:  
  
|Leistungsobjekt|Description|  
|------------------------|-----------------|  
|**SQLServer:Replikations-Agents**<br /><br /> **SQLServer:Replikationsmomentaufnahme**<br /><br /> **SQLServer:Replikationsprotokollleser**<br /><br /> **SQLServer:Replikationsverteilung**<br /><br /> **SQLServer:Replikationsmerge**<br /><br /> Weitere Informationen finden Sie unter [Monitoring Replication with System Monitor](../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).|Stellt Informationen zur Aktivität des Replikations-Agents bereit.|  
  
##  <a name="SsisPipelineCounters"></a> SSIS-Pipelineleistungsindikatoren  
 Informationen zum **SSIS-Pipeline** -Leistungsindikator finden Sie unter [Leistungsindikatoren](../../integration-services/performance/performance-counters.md).  
  
##  <a name="RequiredPermissions"></a> Erforderliche Berechtigungen  
 Die Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekten hängt von Windows-Berechtigungen ab, außer für **SQLAgent:Warnungen**. Die Benutzer müssen Mitglied der festen Serverrolle **sysadmin** sein, um **SQLAgent:Warnungen**zu verwenden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwenden von Leistungsobjekten](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
