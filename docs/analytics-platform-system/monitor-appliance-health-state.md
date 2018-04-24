---
title: Überwachen der Integrität der Appliance – Analytics Platform System
description: So überwachen Sie den Status eines Geräts Analytics Platform System mithilfe der Verwaltungskonsole oder durch direkte Abfrage der dynamischen Verwaltungssichten Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d8616d291dcaa8afadc01c9bd237903ca6c13573
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="monitor-appliance-health-state"></a>Integritätsstatus des Monitors Appliance
In diesem Artikel erläutert, wie den Status eines Geräts Analytics Platform System mithilfe der Verwaltungskonsole oder durch direkte Abfrage der dynamischen Verwaltungssichten Parallel Data Warehouse überwachen. 
  
## <a name="to-monitor-the-appliance-state"></a>Zum Überwachen des Status der Anwendung  
Ein Systemadministrator können der Verwaltungskonsole oder der SQL Server PDW dynamische Verwaltungssichten (DMVs) Sie die vollständige Hierarchie von Knoten, Komponenten und Software abrufen. Das folgende Diagramm bietet eine allgemeine Vorstellung der Komponenten, die von SQL Server PDW überwacht.  
  
![Übersicht über den](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>Monitor-Komponentenstatus mithilfe der Verwaltungskonsole  
Um die Komponentenstatus abrufen, indem Sie mithilfe der Verwaltungskonsole:  
  
1.  Klicken Sie auf die **Anwendungszustand** Registerkarte.  
  
2.  Klicken Sie auf der Seite Anwendungszustand in der auf einem bestimmten Knoten, um die knotendetails anzuzeigen.  
  
    ![PDW-Verwaltungskonsole, Status](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>Monitor-Komponentenstatus mithilfe von Systemsichten  
Verwenden Sie zum Abrufen von Komponentenstatus mithilfe von Systemsichten [sys.dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md). Die folgende Abfrage ruft z. B. den Status für alle Komponenten ab.  
  
```sql  
SELECT   
   s.[pdw_node_id],  
   n.[name] as [node_name],  
   n.[address] ,  
   g.[group_id] ,  
   g.[group_name] ,  
   c.[component_id] ,  
   c.[component_name] ,  
   s.[component_instance_id] ,   
   p.[property_name] ,  
   s.[property_value] ,  
   s.[update_time]  
FROM [sys].[dm_pdw_component_health_status] AS s  
JOIN sys.dm_pdw_nodes AS n   
   ON s.[pdw_node_id] = n.[pdw_node_id]  
JOIN [sys].[pdw_health_components] AS c   
   ON s.[component_id] = c.[component_id]  
JOIN [sys].[pdw_health_component_groups] AS g   
   ON c.[group_id] = g.[group_id]  
JOIN [sys].[pdw_health_component_properties] AS p   
   ON s.[property_id] = p.[property_id] AND s.[component_id] = p.[component_id]  
WHERE p.property_name = 'Status'  
ORDER BY  
   s.[pdw_node_id],  
   g.[group_name] ,   
   s.[component_instance_id] ,  
   c.[component_name] ,   
   p.[property_name];  
```  
  
Mögliche Werte für die Status-Eigenschaft zurückgegeben werden:  
  
-   Okay  
  
-   Nicht schwerwiegender  
  
-   Kritisch  
  
-   Unknown  
  
-   Nicht unterstützt  
  
-   Nicht erreichbar.  
  
-   Nicht behebbarer  
  
Zum Anzeigen aller Eigenschaften für alle Komponenten entfernen der `WHERE  p.property_name = 'Status'` Klausel.  
  
Die **[Update_time]** zeigt Spalte der letzten Ausführung die Komponente wurde vom SQL Server PDW-Systemintegritäts-Agents abgerufen.  
  
> [!CAUTION]  
> Achten Sie darauf, dass Sie das Problem zu untersuchen, wenn eine Komponente nicht 5 Minuten oder länger nicht mehr abgerufen wurde. Es kann eine Warnung aus, die ein Problem mit der Software Takte angibt.  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Überwachen der Appliance &#40;Analyseplattformsystem&#41;](appliance-monitoring.md)  
  
