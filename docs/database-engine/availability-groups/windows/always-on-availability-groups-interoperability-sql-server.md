---
title: "Always On-Verfügbarkeitsgruppen: Interoperabilität (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], interoperability
ms.assetid: daf87f90-2623-42ca-912c-b8f07d210510
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6fd388af46d5522c112435bed0cc6f1985b94c36
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="always-on-availability-groups-interoperability-sql-server"></a>Always On-Verfügbarkeitsgruppen: Interoperabilität (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird die Interoperabilität von [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] mit anderen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Funktionen in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]dokumentiert.  
  
##  <a name="Interop"></a> Funktionen, die mit Always On-Verfügbarkeitsgruppen zusammenwirken  
 In der folgenden Tabelle sind [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Funktionen aufgeführt, die in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] mit [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]zusammenarbeiten. Ein Link in der Spalte **Weitere Informationen** weist darauf hin, dass zusätzliche Überlegungen zur Interoperabilität einer bestimmten Funktion vorhanden sind.  
  
|Funktion|Weitere Informationen|  
|-------------|----------------------|  
|Change Data Capture|[Replikation, Änderungsnachverfolgung, Change Data Capture und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|  
|Änderungsnachverfolgung|[Replikation, Änderungsnachverfolgung, Change Data Capture und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|  
|Eigenständige Datenbanken|[Eigenständige Datenbanken bei Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/contained-databases-with-always-on-availability-groups-sql-server.md)|  
|Datenbankverschlüsselung|[Verschlüsselte Datenbanken bei Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/encrypted-databases-with-always-on-availability-groups-sql-server.md)|  
|Datenbank-Momentaufnahmen|[Datenbankmomentaufnahmen bei Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/database-snapshots-with-always-on-availability-groups-sql-server.md)|  
|FILESTREAM und FileTable|[FILESTREAM und FileTable bei Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)|  
|Volltextsuche|Hinweis: Volltextindizes werden mit sekundären Always On-Datenbanken synchronisiert.|  
|Protokollversand|[Voraussetzungen für das Migrieren vom Protokollversand zu Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)|  
|Remote Blob Store (RBS)|[Remote Blob Store &#40;RBS&#41; und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)|  
|Replikation|[Konfigurieren der Replikation für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)<br /><br /> [Warten einer Always On-Veröffentlichungsdatenbank &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)<br /><br /> [Replikation, Änderungsnachverfolgung, Change Data Capture und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)<br /><br /> [Replikationsabonnenten und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)|  
|Analysis Services|[Analysis Services mit Always On-Verfügbarkeitsgruppen](../../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md)|  
|Reporting Services|Verwenden Sie schreibgeschützte sekundäre Replikate als Berichtsdatenquelle, und reduzieren Sie die Last des primären Lese-/Schreibreplikats.<br /><br /> [Reporting Services mit Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)|  
|Service Broker|[Service Broker mit Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)|  
|SQL Server-Agent||  
  
##  <a name="restrictions"></a> Features, die mit Einschränkungen mit Always On-Verfügbarkeitsgruppen zusammenwirken  
 Die folgenden Features wirken mit [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] unter bestimmten Einschränkungen zusammen. Weitere Informationen finden Sie in den verknüpften Themen.  
  
-   Datenbankübergreifende Transaktionen/verteilte Transaktionen ([!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] und Windows Server 2016). Weitere Informationen finden Sie unter [Datenbankübergreifende Transaktionen und verteilte Transaktionen für Always On-Verfügbarkeitsgruppen oder Datenbankspiegelung &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
##  <a name="NoInterop"></a> Funktionen, die nicht mit Always On-Verfügbarkeitsgruppen zusammenwirken  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] funktioniert nicht in Verbindung mit folgenden Funktionen:  
  
-   Datenbankspiegelung Weitere Informationen finden Sie unter [Datenbankübergreifende Transaktionen und verteilte Transaktionen für Always On-Verfügbarkeitsgruppen oder Datenbankspiegelung &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   **Blogs:**  
  
     [Migrationshandbuch: Migrieren zu SQL Server 2012-Failoverclustering und -Verfügbarkeitsgruppen von vorherigen Clustering- und Spiegelungsbereitstellungen](https://blogs.msdn.microsoft.com/sqlalwayson/2012/04/09/now-available-migration-guide-migrating-to-sql-server-2012-failover-clustering-and-availability-groups-from-prior-clustering-and-mirroring-deployments/)  
  
     [SQL Server Always On-Teamblogs: Der offizielle SQL Server Always On-Teamblog](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server-Technikblogs](http://blogs.msdn.com/b/psssql/)  
  
-   **Whitepaper:**  
  
     [Migrationshandbuch: Migrieren zu Always On-Verfügbarkeitsgruppen von vorherigen Bereitstellungen, in denen Datenbankspiegelung und Protokollversand kombiniert sind](http://msdn.microsoft.com/library/jj635217)  
  
     [Microsoft SQL Server Always On Solutions Guide for High Availability and Disaster Recovery (Microsoft SQL Server Always On-Lösungshandbuch zu hoher Verfügbarkeit und Notfallwiederherstellung)](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Microsoft-Whitepapers für SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Whitepapers des SQL Server-Kundenberatungsteams](http://sqlcat.com/)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  

