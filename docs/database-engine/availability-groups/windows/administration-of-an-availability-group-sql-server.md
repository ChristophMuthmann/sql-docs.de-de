---
title: "Verwaltung einer Verfügbarkeitsgruppe (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], managing
ms.assetid: 0b7542fa-235e-413d-81bf-3eff9ee07480
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c71b0db60e8d35d14d615f953d5f9bc11439dc8a
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="administration-of-an-availability-group-sql-server"></a>Verwaltung einer Verfügbarkeitsgruppe (SQL Server)
 Die Verwaltung einer vorhandenen Always On-Verfügbarkeitsgruppe in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] schließt folgende Tasks ein:  
  
-   Ändern der Eigenschaften eines vorhandenen Verfügbarkeitsreplikats, z. B. Ändern des Clientverbindungszugriffs (zum Konfigurieren lesbarer sekundärer Replikate), des Failovermodus, Verfügbarkeitsmodus oder der Timeouteinstellung für die Sitzung  
  
-   Hinzufügen oder Entfernen sekundärer Replikate  
  
-   Hinzufügen oder Entfernen einer Datenbank  
  
-   Anhalten oder Fortsetzen einer Datenbank  
  
-   Ausführen eines geplanten manuellen Failovers ( *manuelles Failover*) oder eines erzwungenen manuellen Failovers ( *erzwungenes Failover*)  
  
-   Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners  
  
-   Verwalten [lesbarer sekundärer Replikate](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) für eine angegebene Verfügbarkeitsgruppe. Dies umfasst die Konfiguration eines oder mehrerer Replikate für den schreibgeschütztem Zugriff unter der sekundären Rolle sowie die Konfiguration von schreibgeschütztem Routing.  
  
-   Verwalten von [Sicherungen auf sekundären Replikaten](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) für eine angegebene Verfügbarkeitsgruppe. Dies umfasst die Konfiguration des bevorzugten Orts für die Ausführung von Sicherungsaufträgen und die anschließende Skripterstellung für Sicherungsaufträge, um die Sicherungseinstellung zu implementieren. Sie müssen Sicherungsauftragsskripts für jede Datenbank in der Verfügbarkeitsgruppe auf jeder Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] erstellen, die ein Verfügbarkeitsreplikat hostet.  
  
-   Löschen einer Verfügbarkeitsgruppe  
  
-   Clusterübergreifende Migration von Always On-Verfügbarkeitsgruppen für Betriebssystemupgrade  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So konfigurieren Sie eine vorhandene Verfügbarkeitsgruppe**  
  
-   [Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Entfernen einer sekundären Replikats aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Hinzufügen einer Datenbank zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)  
  
-   [Entfernen einer sekundären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Entfernen einer primären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Konfigurieren der flexiblen Failoverrichtlinie zum Steuern der Bedingungen für ein automatisches Failover &#40;Always On-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
 **So verwalten Sie eine Verfügbarkeitsgruppe**  
  
-   [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Ausführen eines geplanten manuellen Failovers einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Ausführen eines erzwungenen manuellen Failovers einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Entfernen einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
 **So verwalten Sie ein Verfügbarkeitsreplikat**  
  
-   [Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Entfernen einer sekundären Replikats aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Ändern des Verfügbarkeitsmodus eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Ändern des Failovermodus eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Zugriffs auf ein Verfügbarkeitsreplikat &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Routing für eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Ändern des Sitzungstimeouts für ein Verfügbarkeitsreplikat &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **So verwalten Sie eine Verfügbarkeitsdatenbank**  
  
-   [Hinzufügen einer Datenbank zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)  
  
-   [Verknüpfen einer sekundären Datenbank mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Entfernen einer primären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Entfernen einer sekundären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Anhalten einer Verfügbarkeitsdatenbank &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md)  
  
-   [Fortsetzen einer Verfügbarkeitsdatenbank &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)  
  
 **So überwachen Sie eine Verfügbarkeitsgruppe**  
  
-   [Überwachen von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
 **So unterstützen Sie das Migrieren von Verfügbarkeitsgruppen zu einem neuen WSFC-Cluster (Kreuzclustermigration)**  
  
-   [Ändern des HADR-Clusterkontexts der Serverinstanz &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
-   [Offlineschalten einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   **Blogs:**  
  
     [SQL Server AlwaysOn-Teamblogs: Der offizielle SQL Server AlwaysOn-Teamblog](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server-Technikblogs](http://blogs.msdn.com/b/psssql/)  
  
-   **Videos:**  
  
     [Microsoft SQL Server Codename „Denali“ Always On-Reihe, Teil 1:Introducing the Next Generation High Availability Solution (Einführung in die nächste Generation von Lösungen mit hoher Verfügbarkeit)](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named "Denali" Always On Series,Part 2: Building a Mission-Critical High Availability Solution Using Always On (in englischer Sprache)](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepaper:**  
  
     [Microsoft-Whitepapers für SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Whitepapers des SQL Server-Kundenberatungsteams](http://sqlcat.com/)  
  
## <a name="see-also"></a>Siehe auch  
 [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Konfiguration einer Serverinstanz für Always On-Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)   
 [Erstellung und Konfiguration von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [Aktive sekundäre Replikate: Lesbare sekundäre Replikate (Always On-Verfügbarkeitsgruppen)](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Aktive sekundäre Replikate: Sicherung auf sekundären Replikaten (Always On-Verfügbarkeitsgruppen)](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)   
 [Verfügbarkeitsgruppenlistener, Clientkonnektivität und Anwendungsfailover &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [Always On Policies for Operational Issues with Always On Availability Groups (SQL Server) (Always On-Richtlinien für Betriebsprobleme mit Always On-Verfügbarkeitsgruppen (SQL Server))](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)   
 [Überwachen von Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)   
 [Always On-Verfügbarkeitsgruppen: Interoperabilität (SQL Server)](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [Übersicht über Transact-SQL-Anweisungen für Always On-Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md)   
 [Übersicht über PowerShell-Cmdlets für Always On-Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
   

