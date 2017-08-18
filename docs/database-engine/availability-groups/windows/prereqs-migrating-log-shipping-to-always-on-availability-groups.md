---
title: "Voraussetzungen für die Migration des Protokollversands zu Always On-Verfügbarkeitsgruppen | Microsoft-Dokumentation"
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
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d7a1d4061f306f5129082d7a3245a76ed0086b32
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="prereqs-migrating-log-shipping-to-always-on-availability-groups"></a>Voraussetzungen für die Migration des Protokollversands zu Always On-Verfügbarkeitsgruppen
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden die erforderlichen Komponenten zum Konvertieren einer primären Datenbank für den Protokollversand zusammen mit einer oder mehreren sekundären Datenbanken in eine primäre AlwaysOn-Datenbank und sekundäre Datenbank(en) beschrieben.  
  
> [!NOTE]  
>  Sie können jede primäre oder sekundäre (ggf. lesbare) Datenbank in einer Verfügbarkeitsgruppe als primäre Datenbank für den Protokollversand konfigurieren.  
  
 **In diesem Thema:**  
  
-   [Erforderliche Komponenten für Verfügbarkeitsgruppen](#AGPrereqsRealAddress)  
  
-   [Erforderliche Komponenten für den Protokollversand](#LogShipPrereqs)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
-   [Verwandte Inhalte](#RelatedContent)  
  
##  <a name="AGPrereqsRealAddress"></a> Erforderliche Komponenten für Verfügbarkeitsgruppen  
 Damit Sicherungsaufträge auf dem primären Replikat der Verfügbarkeitsgruppe ausgeführt werden können, verwenden Sie die folgenden Sicherungseinstellungen für AlwaysOn-Verfügbarkeitsgruppen:  
  
|Eigenschaft|Einstellung|  
|--------------|-------------|  
|Die Voreinstellung für die automatisierte Sicherung der Verfügbarkeitsgruppe.|Nur auf dem primären Replikat|  
|Sicherungspriorität des primären Replikats.|>0|  
  
 **Weitere Informationen:**  
  
 [Anzeigen von Verfügbarkeitsgruppeneigenschaften &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
 [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="LogShipPrereqs"></a> Erforderliche Komponenten für den Protokollversand  
  
-   Die primäre Datenbank für den Protokollversand muss sich auf der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] befinden, auf der das anfängliche/aktuelle primäre Replikat der Verfügbarkeitsgruppe gehostet wird.  
  
-   Damit eine angegebene sekundäre Datenbank für den Protokollversand in eine sekundäre AlwaysOn-Datenbank konvertiert werden kann, muss Folgendes erfüllt sein:  
  
    -   Sie muss den gleichen Namen wie die primäre Datenbank verwenden.  
  
    -   Sie muss auf einer Serverinstanz befinden, auf der ein sekundäres Replikat für die Verfügbarkeitsgruppe gehostet wird.  
  
 Sobald der Sicherungsauftrag auf der primären Datenbank ausgeführt wurde, deaktivieren Sie den Sicherungsauftrag, und sobald der Wiederherstellungsauftrag auf einer angegebenen sekundären Datenbank ausgeführt wurde, deaktivieren Sie den Wiederherstellungsauftrag.  
  
 Nachdem Sie alle sekundären Datenbanken für die Verfügbarkeitsgruppe erstellt haben, sofern Sie Sicherungen auf sekundären Replikaten ausführen möchten, müssen Sie die Voreinstellung zur automatisierten Sicherung der Verfügbarkeitsgruppe neu konfigurieren.  
  
 **Weitere Informationen:**  
  
 [Konvertieren einer Protokollversandkonfiguration in eine Verfügbarkeitsgruppe](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/09/converting-a-logshipping-configuration-to-availability-group/) (ein SQL Server-Blog)  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **Protokollversand**  
  
-   [Aktualisieren des Protokollversands auf SQL Server 2016 &#40;Transact-SQL&#41;](../../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Entfernen des Protokollversands &#40;SQL Server&#41;](../../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
 **AlwaysOn-Verfügbarkeitsgruppen**  
  
-   [Verwenden des Assistenten für Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Verwenden des Dialogfelds „Neue Verfügbarkeitsgruppe“ &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Erstellen einer Verfügbarkeitsgruppe &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [Erstellen einer Verfügbarkeitsgruppe &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
-   [Verknüpfen einer sekundären Datenbank mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   **Blogs:**  
  
     [Konvertieren einer Protokollversandkonfiguration in eine Verfügbarkeitsgruppe](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/09/converting-a-logshipping-configuration-to-availability-group/)  
  
     [Hinzufügen einer primären Datenbank für den Protokollversand und mindestens einer sekundären Datenbank zu einer vorhandenen Verfügbarkeitsgruppe](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/01/add-a-log-shipping-primary-database-and-secondary-databases-to-an-existing-availability-group/)  
  
     [SQL Server AlwaysOn-Teamblogs: Der offizielle SQL Server AlwaysOn-Teamblog](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server-Technikblogs](http://blogs.msdn.com/b/psssql/)  
  
-   **Whitepaper:**  
  
     [Migrationshandbuch: Migrieren zu AlwaysOn-Verfügbarkeitsgruppen von vorherigen Bereitstellungen, in denen Datenbankspiegelung und Protokollversand kombiniert sind](http://msdn.microsoft.com/library/jj635217)  
  
     [Microsoft-Whitepapers für SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Whitepapers des SQL Server-Kundenberatungsteams](http://sqlcat.com/)  
  
## <a name="see-also"></a>Siehe auch  
 [Informationen zum Protokollversand &#40;SQL Server&#41;](../../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  

