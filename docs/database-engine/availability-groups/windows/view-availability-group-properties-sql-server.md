---
title: "Anzeigen von Verfügbarkeitsgruppeneigenschaften (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Availability Groups [SQL Server]
ms.assetid: 61243c87-bd62-4510-863f-2a8f347caf1f
caps.latest.revision: "13"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d4ebd963766c5017539f18cca11c8fddf905e261
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="view-availability-group-properties-sql-server"></a>Anzeigen von Verfügbarkeitsgruppeneigenschaften (SQL Server)
  In diesem Thema wird beschrieben, wie die Eigenschaften einer Verfügbarkeitsgruppe für eine AlwaysOn-Verfügbarkeitsgruppe unter Verwendung von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)] in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]angezeigt werden.  
  
-   **Anzeigen von Verfügbarkeitsgruppeneigenschaften mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 **So zeigen Sie die Eigenschaften einer Verfügbarkeitsgruppe an und ändern sie**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz her, die das primäre Verfügbarkeitsreplikat hostet, und erweitern Sie die Serverstruktur.  
  
2.  Erweitern Sie die Knoten **Hohe Verfügbarkeit mit AlwaysOn** und **Verfügbarkeitsgruppen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Verfügbarkeitsgruppe, deren Eigenschaften Sie anzeigen möchten, und wählen Sie den Befehl **Eigenschaften** aus.  
  
4.  Verwenden Sie im Dialogfeld **Eigenschaften der Verfügbarkeitsgruppe** die Seiten **Allgemein** und **Sicherungseinstellungen** , um Eigenschaften der ausgewählten Verfügbarkeitsgruppe anzuzeigen und in einigen Fällen zu ändern. Weitere Informationen finden Sie unter [Eigenschaften der Verfügbarkeitsgruppe: Neue Verfügbarkeitsgruppe &#40;Seite „Allgemein“&#41;](../../../database-engine/availability-groups/windows/availability-group-properties-new-availability-group-general-page.md) und [Eigenschaften der Verfügbarkeitsgruppe: Neue Verfügbarkeitsgruppe &#40;Seite „Sicherungseinstellungen&#41;](../../../database-engine/availability-groups/windows/availability-group-properties-new-availability-group-backup-preferences-page.md).  
  
     Verwenden Sie die Seite **Berechtigungen** , um die aktuellen Anmeldungen, Rollen und der Verfügbarkeitsgruppe zugeordneten expliziten Berechtigungen anzuzeigen. Weitere Informationen finden Sie unter [Permissions or Securables Page](../../../relational-databases/security/permissions-or-securables-page.md).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So zeigen Sie die Eigenschaften und den Status einer Verfügbarkeitsgruppe an**  
  
 Verwenden Sie zum Abfragen der Eigenschaften und des Status der Verfügbarkeitsgruppen, für die die Serverinstanz ein Verfügbarkeitsreplikat hostet, die folgenden Sichten:  
  
 [sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)  
 Gibt eine Zeile für jede Verfügbarkeitsgruppe zurück, für die die lokale Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ein Verfügbarkeitsreplikat hostet. Jede Zeile enthält eine zwischengespeicherte Kopie der Metadaten der Verfügbarkeitsgruppe.  
  
 **Spaltennamen:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](../../../relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)  
 Gibt eine Zeile für jede Verfügbarkeitsgruppe im WSFC-Cluster zurück. Jede Zeile enthält die Verfügbarkeitsgruppenmetadaten vom WSFC-Cluster (Windows Server-Failoverclustering).  
  
 **Spaltennamen:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
 Gibt eine Zeile für jede Verfügbarkeitsgruppe zurück, die ein Verfügbarkeitsreplikat in der lokalen Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]besitzt. In jede Zeile werden die Statuswerte angezeigt, die den Zustand einer angegebenen Verfügbarkeitsgruppe definieren.  
  
 **Spaltennamen:** group_id, primary_replica, primary_recovery_health, primary_recovery_health_desc, secondary_recovery_health, secondary_recovery_health_desc, synchronization_health, synchronization_health_desc  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So zeigen Sie Informationen zu Verfügbarkeitsgruppen an**  
  
-   [Anzeigen von Verfügbarkeitsreplikateigenschaften &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [Anzeigen von Eigenschaften des Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [Always On-Richtlinien für Betriebsprobleme mit Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)  
  
-   [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [Überwachen von Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
 **So konfigurieren Sie eine vorhandene Verfügbarkeitsgruppe**  
  
-   [Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Entfernen einer sekundären Replikats aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Hinzufügen einer Datenbank zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)  
  
-   [Entfernen einer sekundären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Entfernen eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Entfernen einer primären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Entfernen einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
 **So führen Sie manuell ein Failover für eine Verfügbarkeitsgruppe aus**  
  
-   [Ausführen eines geplanten manuellen Failovers einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Ausführen eines erzwungenen manuellen Failovers einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen (Transact-SQL)](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On-Richtlinien für Betriebsprobleme mit Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)  
  
  
