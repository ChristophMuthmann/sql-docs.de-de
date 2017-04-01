---
title: "Erstellung und Konfiguration von Verf&#252;gbarkeitsgruppen (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verfügbarkeitsgruppen [SQL Server], bereitstellen"
  - "Verfügbarkeitsgruppen [SQL Server], Konfigurieren"
  - "Verfügbarkeitsgruppen [SQL Server], erstellen"
ms.assetid: 7f89fab8-6ee2-4273-9de0-e594bfb9407f
caps.latest.revision: 30
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 29
---
# Erstellung und Konfiguration von Verf&#252;gbarkeitsgruppen (SQL Server)
  Die Themen in diesem Abschnitt erklären, wie eine [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]-Implementierung auf Instanzen von [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] bereitgestellt wird, die sich auf unterschiedlichen WSFC-Knoten (Windows Server-Failoverclustering) innerhalb eines einzelnen WSFC-Failoverclusters befinden.  
  
 Es wird dringend empfohlen, dass Sie sich vor dem Erstellen der ersten Verfügbarkeitsgruppe mit den Informationen in den folgenden Themen vertraut machen:  
  
 [Voraussetzungen, Einschränkungen und Empfehlungen für AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs, restrictions, recommendations - always on availability.md)  
 In diesem Thema werden die erforderlichen Voraussetzungen, Einschränkungen und Empfehlungen für Computer, WSFC-Knoten, Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Verfügbarkeitsgruppen, Replikate und Datenbanken beschrieben. Das Thema enthält auch Informationen zu Sicherheitsaspekten.  
  
 [Erste Schritte mit AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)  
 Enthält Informationen zu den Schritten zum Konfigurieren einer Serverinstanz, Erstellen einer Verfügbarkeitsgruppe, Konfigurieren der Verfügbarkeitsgruppe für Clientverbindungen, Verwalten von Verfügbarkeitsgruppen und Überwachen von Verfügbarkeitsgruppen.  
  
 **In diesem Thema:**  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
-   [Verwandte Inhalte](#RelatedContent)  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So konfigurieren Sie eine Serverinstanz für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]**  
  
-   [Aktivieren und Deaktivieren von AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [Erstellen eines Datenbankspiegelungs-Endpunkts für AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database mirroring - always on availability groups- powershell.md)  
  
-   [Erstellen eines Endpunkts der Datenbankspiegelung für Windows-Authentifizierung &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Ermöglichen des Verwendens von Zertifikaten für ausgehende Verbindungen für einen Datenbankspiegelungs-Endpunkt &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database mirroring - use certificates for outbound connections.md)  
  
 **Erste Schritte bei der Konfiguration von AlwaysOn-Verfügbarkeitsgruppen**  
  
-   [Erste Schritte mit AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)  
  
 **So erstellen und konfigurieren Sie eine neue Verfügbarkeitsgruppe**  
  
-   [Verwenden des Assistenten für Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Erstellen einer Verfügbarkeitsgruppe &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [Erstellen einer Verfügbarkeitsgruppe &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
-   [Verwenden des Dialogfelds „Neue Verfügbarkeitsgruppe“ &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Angeben der Endpunkt-URL beim Hinzufügen oder Ändern eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify endpoint url - adding or modifying availability replica.md)  
  
-   [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Konfigurieren der flexiblen Failoverrichtlinie zum Steuern der Bedingungen für ein automatisches Failover &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/configure flexible automatic failover policy.md)  
  
-   [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Zugriffs auf ein Verfügbarkeitsreplikat &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Routing für eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Starten der Datenverschiebung auf einer sekundären AlwaysOn-Datenbank &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [Manuelles Vorbereiten einer sekundären Datenbank auf eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Verknüpfen einer sekundären Datenbank mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Verwaltung von Anmeldungen und Aufträgen für die Datenbanken einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/logins and jobs for availability group databases.md)  
  
 **So beheben Sie Probleme**  
  
-   [Problembehandlung für die AlwaysOn-Verfügbarkeitsgruppenkonfiguration &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Problembehandlung bei einem fehlgeschlagenen Vorgang zum Hinzufügen einer Datei &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   **Blogs:**  
  
     [AlwaysOn – HADRON-Lernreihe: Nutzung des Arbeitsthreadpools für HADRON-fähige Datenbanken](http://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn-Teamblogs: Der offizielle SQL Server AlwaysOn-Teamblog](http://blogs.msdn.com/b/sqlAlways%20On/)  
  
     [CSS SQL Server-Technikblogs](http://blogs.msdn.com/b/psssql/)  
  
-   **Videos:**  
  
     [Microsoft SQL Server Code namens „Denali“ AlwaysOn-Series, Teil 1: Einführung in die Lösung für hohe Verfügbarkeit der nächsten Generation](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code namens „Denali“ AlwaysOn-Series, Teil 2: Erstellen einer unternehmenswichtigen Lösung für hohe Verfügbarkeit mithilfe von AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepaper:**  
  
     [Microsoft SQL Server AlwaysOn-Lösungshandbuch zu hoher Verfügbarkeit und Notfallwiederherstellung](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Microsoft-Whitepapers für SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Whitepapers des SQL Server-Kundenberatungsteams](http://sqlcat.com/)  
  
## Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwaltung einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)   
 [AlwaysOn-Richtlinien für Betriebsprobleme mit AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always on policies for operational issues - always on availability.md)   
 [Überwachen von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn-Verfügbarkeitsgruppen: Interoperabilität &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  