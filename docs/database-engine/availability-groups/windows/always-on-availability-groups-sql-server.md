---
title: Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], about
- secondary replicas, see Availability Groups [SQL Server]
- availability [SQL Server]
- AlwaysOn [SQL Server], see Availability Groups [SQL Server]
- Availability Groups [SQL Server]
ms.assetid: aa427606-8422-4656-b205-c9e665ddc8c1
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4250994b203bad822bb68d571871bae87c611317
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="always-on-availability-groups-sql-server"></a>Always On-Verfügbarkeitsgruppen (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Die Funktion [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ist eine Lösung für hohe Verfügbarkeit und Notfallwiederherstellung, die eine Alternative zur Datenbankspiegelung auf Unternehmensebene bietet. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]wurden in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] eingeführt und maximieren die Verfügbarkeit einer Gruppe von Benutzerdatenbanken für ein Unternehmen. Eine *Verfügbarkeitsgruppe* unterstützt eine Failoverumgebung für einen diskreten Satz von Benutzerdatenbanken (als *Verfügbarkeitsdatenbanken*bezeichnet), die zusammen ein Failover ausführen. Eine Verfügbarkeitsgruppe unterstützt einen Satz primärer Datenbanken mit Lese-/Schreibzugriff und einen bis acht Sätze entsprechender sekundärer Datenbanken. Optional können sekundäre Datenbanken für schreibgeschützten Zugriff und/oder einige Sicherungsvorgänge verfügbar gemacht werden.  
  
 Eine Verfügbarkeitsgruppe führt auf der Ebene eines Verfügbarkeitsreplikats ein Failover aus. Failover werden nicht durch Datenbankprobleme verursacht, z. B., wenn eine Datenbank aufgrund eines Verlusts einer Datendatei, des Löschens einer Datenbank oder der Beschädigung eines Transaktionsprotokolls, verdächtig wird.  
 
 >[HINWEIS] Der vollständige, formale Name für diese Verfügbarkeitsfunktionen lautet „Always On-Verfügbarkeitsgruppen“. Die englische Abkürzung für diesen Begriff lautet AG (Always On Availability groups). Bitte verwenden Sie nicht die Abkürzungen AOAG oder AAG. 
  
##  <a name="Benefits"></a> Vorteile  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] stellen ein breites Spektrum von Optionen bereit, durch die die Datenbankverfügbarkeit verbessert und eine optimale Ressourcenverwendung ermöglicht werden. Die wichtigsten Komponenten sind:  
  
-   Unterstützt bis zu neun Verfügbarkeitsreplikate. Ein *Verfügbarkeitsreplikat* ist eine Instanziierung einer Verfügbarkeitsgruppe, die von einer bestimmten Instanz von SQL Server gehostet wird und eine lokale Kopie jeder Verfügbarkeitsdatenbank beibehält, die zur Verfügbarkeitsgruppe gehört. Jede Verfügbarkeitsgruppe unterstützt ein primäres Replikat und bis zu acht sekundäre Replikate. Weitere Informationen finden Sie unter [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Jedes Verfügbarkeitsreplikat muss sich in einem anderen Knoten eines einzelnen WSFC-Clusters (Windows Server-Failoverclustering) befinden. Informationen zu Voraussetzungen, Einschränkungen und Empfehlungen für Verfügbarkeitsgruppen finden Sie unter [Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Unterstützt die folgenden alternativen Verfügbarkeitsmodi:  
  
    -   *Modus für asynchrone Commits*. Dieser Verfügbarkeitsmodus ist eine Lösung für die Notfallwiederherstellung, die gut funktioniert, wenn die Verfügbarkeitsreplikate über große Entfernungen verteilt sind.  
  
    -   *Modus für synchrone Commits*. Bei diesem Verfügbarkeitsmodus haben hohe Verfügbarkeit und Datenschutz Vorrang vor Leistung, und dies hat eine höhere Transaktionslatenz zur Folge. Eine bestimmte Verfügbarkeitsgruppe kann bis zu drei Verfügbarkeitsreplikate mit synchronem Commit (einschließlich des aktuellen primären Replikats) unterstützen.  
  
     Weitere Informationen finden Sie unter [Verfügbarkeitsmodi &#40;Always On-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)ausgetauscht werden.  
  
-   Unterstützt mehrere Failovermethoden für Verfügbarkeitsgruppen: automatisches Failover, geplantes manuelles Failover (im Allgemeinen "manuelles Failover" genannt) und erzwungenes manuelles Failover (im Allgemeinen "erzwungenes Failover" genannt). Weitere Informationen finden Sie weiter unten in diesem Thema unter [Failover und Failovermodi &#40;Always On-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).  
  
-   Ermöglicht es Ihnen, ein angegebenes Verfügbarkeitsreplikat so zu konfigurieren, dass es entweder eines oder beide der folgenden Funktionen für aktive sekundäre Replikate unterstützt:  
  
    -   Lesezugriff, der es schreibgeschützten Verbindungen erlaubt, auf das Replikat zuzugreifen und dessen Datenbanken zu lesen, wenn es als sekundäres Replikat ausgeführt wird. Weitere Informationen finden Sie unter [Aktive sekundäre Replikate: Lesbare sekundäre Replikate &#40;Always On-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
    -   Das Ausführen von Sicherungsvorgängen für seine Datenbanken, wenn es als sekundäres Replikat ausgeführt wird. Weitere Informationen finden Sie unter [Aktive sekundäre Replikate: Sicherung auf sekundären Replikaten &#40;Always On-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
     Durch die Verwendung aktiver sekundärer Replikate lassen sich durch die bessere Ressourcennutzung sekundärer Hardware die IT-Effizienz erhöhen und die Kosten reduzieren. Außerdem trägt das Auslagern reiner Lesevorgänge und Sicherungsaufträge auf sekundäre Replikate dazu bei, die Leistung auf dem primären Replikat zu verbessern.  
  
-   Unterstützt einen Verfügbarkeitsgruppenlistener für jede Verfügbarkeitsgruppe. Ein *Verfügbarkeitsgruppenlistener* ist ein Servername, mit dem Clients eine Verbindung herstellen können, um auf eine Datenbank in einem primären oder sekundären Replikat einer Always On-Verfügbarkeitsgruppe zuzugreifen. Verfügbarkeitsgruppenlistener leiten eingehende Verbindungen an das primäre Replikat oder ein schreibgeschütztes sekundäres Replikat weiter. Der Listener ermöglicht ein schnelles Anwendungsfailover, nachdem für eine Verfügbarkeitsgruppe ein Failover ausgeführt wurde. Weitere Informationen finden Sie unter [Verfügbarkeitsgruppenlistener, Clientkonnektivität und Anwendungsfailover &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)wichtig sind.  
  
-   Unterstützt eine flexible Failoverrichtlinie, um größere Kontrolle über das Failover von Verfügbarkeitsgruppen zu erlangen. Weitere Informationen finden Sie unter [Failover und Failovermodi &#40;Always On-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).  
  
-   Unterstützt die automatische Seitenreparatur als Schutz vor Seitenbeschädigungen. Weitere Informationen finden Sie unter [Automatische Seitenreparatur &#40;Verfügbarkeitsgruppen/Datenbankspiegelung&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md).  
  
-   Unterstützt Verschlüsselung und Komprimierung, die einen sicheren, leistungsstarken Transport ermöglichen.  
  
-   Stellt einen integrierten Satz von Tools bereit, um die Bereitstellung und Verwaltung von Verfügbarkeitsgruppen zu erleichtern. Dazu gehören:  
  
    -   [!INCLUDE[tsql](../../../includes/tsql-md.md)] -DDL-Anweisungen zum Erstellen und Verwalten von Verfügbarkeitsgruppen. Weitere Informationen finden Sie unter [Übersicht über Transact-SQL-Anweisungen für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] -Tools:  
  
        -   Mit dem [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] wird eine Verfügbarkeitsgruppe erstellt und verwaltet. In einigen Umgebungen kann dieser Assistent auch die sekundären Datenbanken automatisch vorbereiten und die Datensynchronisierung für jede von ihnen starten. Weitere Informationen finden Sie unter [Verwenden des Dialogfelds „Neue Verfügbarkeitsgruppe“ &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md).  
  
        -   Der [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] fügt einer vorhandenen Verfügbarkeitsgruppe eine oder mehrere primäre Datenbanken hinzu. In einigen Umgebungen kann dieser Assistent auch die sekundären Datenbanken automatisch vorbereiten und die Datensynchronisierung für jede von ihnen starten. Weitere Informationen finden Sie unter [Verwenden des Assistenten zum Hinzufügen von Datenbanken zu Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md).  
  
        -   Der [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] fügt einer vorhandenen Verfügbarkeitsgruppe ein oder mehrere sekundäre Replikate hinzu. In einigen Umgebungen kann dieser Assistent auch die sekundären Datenbanken automatisch vorbereiten und die Datensynchronisierung für jede von ihnen starten. Weitere Informationen finden Sie unter [Verwenden des Assistenten zum Hinzufügen von Replikaten zu Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md).  
  
        -   Der [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)] initiiert ein manuelles Failover für eine Verfügbarkeitsgruppe. Abhängig von der Konfiguration und dem Zustand des sekundären Replikats, das Sie als Failoverziel angeben, kann der Assistent entweder ein geplantes oder ein erzwungenes manuelles Failover ausführen. Weitere Informationen finden Sie unter [Verwenden des Assistenten für Failover-Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md).  
  
    -   Das [!INCLUDE[ssAoDash](../../../includes/ssaodash-md.md)] überwacht Always On-Verfügbarkeitsgruppen, -Verfügbarkeitsreplikate und -Verfügbarkeitsdatenbanken und wertet Ergebnisse für Always On-Richtlinien aus. Weitere Informationen finden Sie unter [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md).  
  
    -   Der Detailbereich im Objekt-Explorer zeigt grundlegende Informationen zu vorhandenen Verfügbarkeitsgruppen an. Weitere Informationen finden Sie unter [Verwenden der Details zum Objekt-Explorer zum Überwachen von Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   PowerShell-Cmdlets. Weitere Informationen finden Sie unter [Übersicht über PowerShell-Cmdlets für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md).  
  
##  <a name="TermsAndDefinitions"></a> Begriffe und Definitionen  
 **Verfügbarkeitsgruppe**  
 Ein Container für eine Gruppe von Datenbanken ( *Verfügbarkeitsdatenbanken*), für die zusammen ein Failover ausgeführt wird.  
  
 **Verfügbarkeitsdatenbank**  
 Eine Datenbank, die zu einer Verfügbarkeitsgruppe gehört. Für jede Verfügbarkeitsdatenbank verwaltet die Verfügbarkeitsgruppe eine einzelne Lese-/Schreibkopie (die *primäre Datenbank*) und eine bis acht schreibgeschützte Kopien (*sekundäre Datenbanken*).  
  
 **Primäre Datenbank**  
 Die Lese-/Schreibkopie einer Verfügbarkeitsdatenbank.  
  
 **Sekundäre Datenbank**  
 Eine schreibgeschützte Kopie einer Verfügbarkeitsdatenbank.  
  
 **Verfügbarkeitsreplikat**  
 Eine Instanziierung einer Verfügbarkeitsgruppe, die von einer bestimmten Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gehostet wird und eine lokale Kopie jeder Verfügbarkeitsdatenbank beibehält, die zur Verfügbarkeitsgruppe gehört. Zwei Typen von Verfügbarkeitsreplikaten sind vorhanden: ein einzelnes *primäres Replikat* und ein bis acht *sekundäre Replikate*.  
  
 **Primäres Replikat**  
 Das Verfügbarkeitsreplikat, das die primären Datenbanken für Lese-/Schreibverbindungen von Clients verfügbar macht und darüber hinaus Transaktionsprotokoll-Datensätze für jede primäre Datenbank an jedes sekundäre Replikat sendet.  
  
 **Sekundäres Replikat**  
 Ein Verfügbarkeitsreplikat, das eine sekundäre Kopie jeder Verfügbarkeitsdatenbank beibehält und als potenzielles Failoverziel für die Verfügbarkeitsgruppe dient. Optional kann ein sekundäres Replikat schreibgeschützten Zugriff auf sekundäre Datenbanken und das Erstellen von Sicherungen für sekundäre Datenbanken unterstützen.  
  
 **Verfügbarkeitsgruppenlistener**  
 Ein Servername, mit dem Clients eine Verbindung herstellen können, um auf eine Datenbank in einem primären oder sekundären Replikat einer Always On-Verfügbarkeitsgruppe zuzugreifen. Verfügbarkeitsgruppenlistener leiten eingehende Verbindungen an das primäre Replikat oder ein schreibgeschütztes sekundäres Replikat weiter.  
  
> [!NOTE]  
>  Weitere Informationen finden Sie unter [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="Interoperability"></a> Interoperabilität und Koexistenz mit anderen Datenbankmodul-Funktionen  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] können mit den folgenden Funktionen oder Komponenten von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verwendet werden:  
  
-   [Über Change Data Capture &#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
-   [Informationen zur Änderungsnachverfolgung &#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
-   [Eigenständige Datenbanken](../../../relational-databases/databases/contained-databases.md)  
  
-   [Datenbankverschlüsselung](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
-   [Datenbank-Momentaufnahmen](../../../database-engine/availability-groups/windows/database-snapshots-with-always-on-availability-groups-sql-server.md)  
  
-   [FILESTREAM](../../../relational-databases/blob/filestream-sql-server.md)  
  
-   [FileTable](../../../relational-databases/blob/filetables-sql-server.md)  
  
-   [Protokollversand](../../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
-   [Remote Blob Store (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
-   [Replikation](../../../relational-databases/replication/sql-server-replication.md)  
  
-   [Service Broker](../../../database-engine/configure-windows/sql-server-service-broker.md)  
  
-   [SQL Server-Agent](http://msdn.microsoft.com/library/8d1dc600-aabb-416f-b3af-fbc9fccfd0ec)  
  
-   [Reporting Services](../../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)  
  
> [!WARNING]  
>  Informationen zu Einschränkungen bei der Verwendung anderer Funktionen mit [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] finden Sie unter [Always On-Verfügbarkeitsgruppen: Interoperabilität &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Erste Schritte mit Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   **Blogs:**  
  
     [SQL Server Always On Team Blogs: The official SQL Server Always On Team Blog (SQL Server Always On-Teamblogs: Der offizielle SQL Server Always On-Teamblog)](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server-Technikblogs](http://blogs.msdn.com/b/psssql/)  
  
-   **Videos:**  
  
     [Microsoft SQL Server Codename „Denali“ Always On-Reihe, Teil 1:Introducing the Next Generation High Availability Solution (Einführung in die nächste Generation von Lösungen mit hoher Verfügbarkeit)](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Codename „Denali“ Always On-Reihe, Teil 2: Building a Mission-Critical High Availability Solution Using Always On (Erstellen einer unternehmenswichtigen Lösung für hohe Verfügbarkeit mit Always On)](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepaper:**  
  
     [Microsoft SQL Server AlwaysOn-Lösungshandbuch zu hoher Verfügbarkeit und Notfallwiederherstellung](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Microsoft-Whitepapers für SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Whitepapers des SQL Server-Kundenberatungsteams](http://sqlcat.com/)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Konfiguration einer Serverinstanz für Always On-Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)   
 [Erstellung und Konfiguration von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [Verwaltung einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)   
 [Übersicht über Transact-SQL-Anweisungen für Always On-Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md)   
 [Übersicht über PowerShell-Cmdlets für Always On-Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
