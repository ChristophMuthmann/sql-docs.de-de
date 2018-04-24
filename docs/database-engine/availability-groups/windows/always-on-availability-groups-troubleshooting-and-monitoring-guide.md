---
title: Leitfaden zur Problembehandlung und Überwachung von Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation
ms.custom: ag-guide
ms.date: 05/10/2016
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8d6d9954-ff6b-4e58-882e-eff0174f0d07
caps.latest.revision: 8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b78d697f5e8359580e8ebbf602587584964b017c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="always-on-availability-groups-troubleshooting-and-monitoring-guide"></a>Leitfaden zur Problembehandlung und Überwachung von Always On-Verfügbarkeitsgruppen
 Dieser Leitfaden unterstützt Sie bei den ersten Schritten mit der Überwachung von Always On-Verfügbarkeitsgruppen und der Behandlung einiger gängiger Probleme in Bezug auf Verfügbarkeitsgruppen. Zudem bietet der Leitfaden Originalinhalte sowie eine Angebotsseite mit nützlichen Informationen, die an anderer Stelle veröffentlicht wurden. Im Rahmen dieses Leitfadens können zwar nicht alle Probleme, die auf dem umfassenden Gebiet der Verfügbarkeitsgruppen auftreten können, im Detail erläutert werden, allerdings kann auf die richtige Richtung bezüglich der Ursachenanalyse und Problemlösung gewiesen werden. 
 
 Da Verfügbarkeitsgruppen eine integrierte Technologie darstellen, sind viele der auftretenden Probleme möglicherweise Anzeichen für andere Probleme in Ihrem Datenbanksystem. Einige Probleme werden durch Einstellungen in einer Verfügbarkeitsgruppe verursacht, z.B. eine angehaltene Verfügbarkeitsdatenbank. Darüber hinaus können Probleme mit anderen Aspekten von SQL Server auftreten, z.B. SQL Server-Einstellungen und Bereitstellungen von Datenbankdateien, sowie systemische Leistungsprobleme, die unabhängig von der Verfügbarkeit bestehen. Dennoch können andere Probleme außerhalb von SQL Server auftreten, z.B. Probleme mit Netzwerk-E/As, TCP/IP, Active Directory und Windows Server Failover Clustering (WSFC). Oftmals muss bei Problemen, die sich bei einer Verfügbarkeitsgruppe, einem Replikat oder einer Datenbank abzeichnen, an mehreren Technologien Korrekturen vorgenommen werden, um die Ursache zu ermitteln.  
  

  
##  <a name="BKMK_SCENARIOS"></a> Problembehandlungsszenarien  
 Die folgende Tabelle enthält Links zu allgemeinen Problembehandlungsszenarien für Verfügbarkeitsgruppen. Sie werden nach den jeweiligen Szenariotypen kategorisiert, z.B. Konfiguration, Clientkonnektivität, Failover und Leistung.  
  
|Szenario|Szenariotyp|Description|  
|--------------|-------------------|-----------------|  
|[Behandlung von Problemen bei der Konfiguration von Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](troubleshoot-always-on-availability-groups-configuration-sql-server.md)|Konfiguration|Enthält Informationen, um Sie bei der Behandlung typischer Probleme mit der Konfiguration von Serverinstanzen für Verfügbarkeitsgruppen zu unterstützen. Zu typischen Konfigurationsproblemen zählen Folgende: Verfügbarkeitsgruppen sind deaktiviert, Konten sind falsch konfiguriert, Datenbankspiegelungsendpunkte sind nicht vorhanden, es kann nicht auf Endpunkte zugegriffen werden (SQL Server-Fehler 1418), es ist kein Netzwerkzugriff vorhanden und bei dem Befehl zum Verknüpfen einer Datenbank tritt ein Fehler auf (SQL Server-Fehler 35250).|  
|[Problembehandlung bei einem fehlgeschlagenen Vorgang zum Hinzufügen einer Datei &#40;Always On-Verfügbarkeitsgruppen&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)|Konfiguration|Ein Vorgang zum Hinzufügen einer Datei hat dazu geführt, dass die sekundäre Datenbank angehalten wird und sich im Zustand SYNCHRONISIERUNG WIRD NICHT AUSGEFÜHRT befindet.|  
|[Es kann keine Verbindung mit dem Verfügbarkeitsgruppenlistener in einer Umgebung mit mehreren Subnetzen hergestellt werden.](http://support.microsoft.com/kb/2792139/en-us)|Clientkonnektivität|Wenn Sie keinen Verfügbarkeitsgruppenlistener konfiguriert haben, können Sie nicht den Listener pingen oder eine Verbindung zwischen diesem und einer Anwendung herstellen.|  
|[Behandlung von Fehlern bei einem automatischen Failover](http://support.microsoft.com/kb/2833707)|Failover|Ein automatisches Failover wurde nicht erfolgreich durchgeführt.|  
|[Problembehandlung: Verfügbarkeitsgruppe hat RTO überschritten](troubleshoot-availability-group-exceeded-rto.md)|Leistung|Nach einem automatischen Failover oder einem geplanten manuellen Failover ohne Datenverlust überschreitet die Failoverzeit die RTO. Ein anderer Fall: Wenn Sie die Failoverzeit eines sekundären Replikats im synchronen Commitmodus (z.B. eines Partners für das automatische Failover) einschätzen, stellen Sie fest, dass diese Ihre RTO überschreitet.|  
|[Problembehandlung: Verfügbarkeitsgruppe hat RPO überschritten](troubleshoot-availability-group-exceeded-rpo.md)|Leistung|Nachdem Sie ein erzwungenes manuelles Failover ausgeführt haben, ist der Datenverlust größer als Ihre RPO. Ein anderer Fall: Wenn Sie den möglichen Datenverlust eines sekundäres Replikats im asynchronen Commitmodus berechnen, stellen Sie fest, dass dieser Ihre RPO überschreitet.|  
|[Problembehandlung: Änderungen am primären Replikat spiegeln sich nicht im sekundären Replikat wider](troubleshoot-primary-changes-not-reflected-on-secondary.md)|Leistung|Die Clientanwendung führt erfolgreich ein Update für das primäre Replikat durch, wobei jedoch die Abfrage des sekundären Replikats ergibt, dass die Änderung nicht widergespiegelt wird.|  
|[Problembehandlung: Hoher HADR_SYNC_COMMIT-Wartetyp mit Always On-Verfügbarkeitsgruppen](https://blogs.msdn.microsoft.com/sql_server_team/troubleshooting-high-hadr_sync_commit-wait-type-with-always-on-availability-groups/)|Leistung|Wenn HADR_SYNC_COMMIT ungewöhnlich lang ist, besteht ein Leistungsproblem beim Datenverschiebungsfluss oder der Protokollfestschreibung für ein sekundäres Replikat.|  

##  <a name="BKMK_TOOLS"></a> Hilfreiche Tools für die Problembehandlung  
 Bei der Konfiguration oder Ausführung von Verfügbarkeitsgruppen können Sie mithilfe verschiedener Tools unterschiedliche Arten von Problemen diagnostizieren. Die folgende Tabelle enthält Links zu nützlichen Informationen über die Tools.  
  
|Tool|Description|  
|----------|-----------------|  
|[Verwenden des AlwaysOn-Dashboards &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)|Bietet auf einer benutzerfreundlichen Oberfläche einen prägnanten Überblick über die Integrität der Verfügbarkeitsgruppe.|  
|[Always On-Richtlinien](always-on-policies.md)|Werden vom Always On-Dashboard verwendet.|  
|[SQL Server-Fehlerprotokoll &#40;Always On-Verfügbarkeitsgruppen&#41;](sql-server-error-log-always-on-availability-groups.md)|Protokolliert Statusübergangsereignisse für Verfügbarkeitsgruppen, -replikate und -datenbanken, Status von anderen Always On-Komponenten und Always On-Fehler.|  
|[CLUSTER.LOG &#40;Always On-Verfügbarkeitsgruppen&#41;](cluster-log-always-on-availability-groups.md)|Protokolliert Clusterereignisse wie Statusübergänge der Verfügbarkeitsgruppenressource sowie Ereignisse und Fehler der SQL Server-Ressourcen-DLL.|  
|[Always On-Integritätsdiagnoseprotokoll](always-on-health-diagnostics-log.md)|Protokolliert die SQL Server-Integritätsdiagnose, die dem WSFC-Cluster (SQL Server-Ressourcen-DLL) mit [sp_server_diagnostics &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) gemeldet wird.|  
|[Dynamische Verwaltungssichten und Systemkatalogsichten &#40;Always On-Verfügbarkeitsgruppen&#41;](dynamic-management-views-and-system-catalog-views-always-on-availability-groups.md)|Meldet Informationen zu den Verfügbarkeitsgruppen wie Konfiguration, Integritätsstatus und Leistungsmetriken.|  
|[Erweiterte Always On-Ereignisse](always-on-extended-events.md)|Stellt ausführliche Diagnoseinformationen zu den Verfügbarkeitsgruppen bereit und ist für Ursachenanalysen geeignet.|  
|[Always On-Wartetypen](always-on-wait-types.md)|Stellt die Wartestatistik speziell für Verfügbarkeitsgruppen bereit und ist für die Leistungsoptimierung geeignet.|  
|Always On-Leistungsindikatoren|Überwachen die im Systemmonitor dargestellte Verfügbarkeitsgruppenaktivität und sind für die Leistungsoptimierung geeignet. Weitere Informationen finden Sie unter [SQL Server-Verfügbarkeitsreplikat](~/relational-databases/performance-monitor/sql-server-availability-replica.md) und [SQL Server-Datenbankreplikat](~/relational-databases/performance-monitor/sql-server-database-replica.md).|  
|[Always On-Ringpuffer](always-on-ring-buffers.md)|Erfassen Warnungen innerhalb des SQL Server-Systems für die interne Diagnose und können zum Debuggen von Problemen im Zusammenhang mit Verfügbarkeitsgruppen verwendet werden.|  
  
##  <a name="BKMK_MONITOR"></a> Überwachen von Verfügbarkeitsgruppen  
 Der ideale Zeitpunkt, um ein Problem mit einer Verfügbarkeitsgruppe zu behandeln, bevor ein Problem ein Failover erfordert, unabhängig davon, ob dieses automatisch oder manuell erfolgt. Dies kann erreicht werden, indem die Leistungsmetriken der Verfügbarkeitsgruppe überwacht und Warnungen gesendet werden, wenn die Verfügbarkeitsreplikate außerhalb der Beschränkungen Ihrer Vereinbarung zum Servicelevel (SLA) ausgeführt werden. Wenn ein sekundäres Replikat im synchronen Commitmodus beispielsweise Leistungsprobleme aufweist, die dazu führen, dass sich die geschätzte Failoverzeit verlängert, sollten Sie nicht bis zum Auftreten eines automatischen Failovers warten. Anderenfalls werden Sie feststellen, dass die Failoverzeit Ihre Recovery Time Objective überschreitet.  
  
 Da Verfügbarkeitsgruppen zu Hochverfügbarkeits- und Notfallwiederherstellungslösungen gehören, stellen die wichtigsten zu überwachenden Leistungsmetriken die geschätzte Failoverzeit (Ihre Recovery Time Objective, RTO, betreffend) und der potenzielle Datenverlust bei einem Notfall (Ihre Recovery Point Objective, RPO, betreffend) dar. Sie können diese Metriken anhand der Daten erfassen, die SQL Server zu einem bestimmten Zeitpunkt verfügbar macht, sodass Sie über Probleme mit den HADR-Funktionen (High Availability Disaster Recovery) Ihres Systems benachrichtigt werden, bevor tatsächlich Fehlerereignisse auftreten. Aus diesem Grund ist es wichtig, sich mit dem Datensynchronisierungsprozess von Verfügbarkeitsgruppen vertraut zu machen und die entsprechenden Metriken zu erfassen.  
  
 Die untenstehende Tabelle verweist auf Themen, mit denen Sie die Integrität Ihrer Verfügbarkeitsgruppenlösung überwachen können.  
  
|Thema|Description|  
|-----------|-----------------|  
|[Überwachen der Leistung von Always On-Verfügbarkeitsgruppen](monitor-performance-for-always-on-availability-groups.md)|In diesem Thema werden der Datensynchronisierungsprozess für Verfügbarkeitsgruppen, die Flusssteuerungsgates und nützliche Metriken für die Überwachung einer Verfügbarkeitsgruppe sowie der Prozess zum Erfassen der Metriken RTO und RPO beschrieben.|  
|[Überwachen von Verfügbarkeitsgruppen &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)|Dieses Thema enthält Informationen zu Tools für die Überwachung einer Verfügbarkeitsgruppe.|  
|[The Always On Health Model Part 1 – Health Model Architecture (Das Always On-Integritätsmodell Teil 1 – Architektur des Integritätsmodells)](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/09/overview-of-the-alwayson-manageability-health-model.aspx)|Dieses Thema enthält eine Übersicht über das Always On-Integritätsmodell.|  
|[The Always On Health Model Part 2 – Extending the Health Model (Das Always On-Integritätsmodell Teil 2 – Erweitern des Integritätsmodells)](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)|In diesem Thema wird erläutert, wie das Always On-Integritätsmodell und das Always On-Dashboard zur Anzeige weiterer Informationen angepasst werden.|  
|[Monitoring Always On Health with PowerShell – Part 1: Basic Cmdlet Overview (Überwachen der Always On-Integrität mit PowerShell – Teil 1: Übersicht über grundlegende Cmdlets)](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-1.aspx)|Dieses Thema enthält eine grundlegende Übersicht über die PowerShell-Cmdlets, die zur Überwachung der Integrität einer Verfügbarkeitsgruppe verwendet werden können.|  
|[Monitoring Always On Health with PowerShell – Part 2: Advanced Cmdlet Usage (Überwachen der Always On-Integrität mit PowerShell – Teil 2: Verwendung erweiterter Cmdlets)](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-2.aspx)|Dieses Thema enthält Informationen über die erweiterte Verwendung der Always On-PowerShell-Cmdlets zum Überwachen der Integrität einer Verfügbarkeitsgruppe.|  
|[Monitoring Always On Health with PowerShell – Part 3 : A Simple Monitoring Application (Überwachen der Always On-Integrität mit PowerShell – Teil 3: Eine einfache Überwachungsanwendung)](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/monitoring-alwayson-health-with-powershell-part-3.aspx)|In diesem Thema wird erläutert, wie eine Verfügbarkeitsgruppe mit einer Anwendung automatisch überwacht wird.|  
|[Monitoring Always On Health with PowerShell – Part 4 : Integration with SQL Server Agent (Überwachen der Always On-Integrität mit PowerShell – Teil 4: Integration im SQL Server-Agent)](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/the-always-on-health-model-part-4.aspx)|Dieses Thema enthält Informationen darüber, wie die Überwachung der Verfügbarkeitsgruppe in SQL Server-Agent integriert und Benachrichtigung für die zuständigen Personen bei Problemen konfiguriert werden.|  

## <a name="next-steps"></a>Nächste Schritte  
 [SQL Server Always On-Teamblog](http://blogs.msdn.com/b/sqlalwayson/)   
 [CSS SQL Server-Technikblogs](http://blogs.msdn.com/b/psssql/)  
  
  
