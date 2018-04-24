---
title: Nachverfolgen der Appliance Warnungen – Analytics Platform System | Microsoft Docs
description: Verfolgen Sie die Appliance-Warnungen in Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 82803e6f20e4a710f317e2e7a541c4a1c72ed08d
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>Appliance-Warnungen in Analytics Platform System nachverfolgen
In diesem Thema wird erläutert, wie mit der Admin-Konsole und Systemsichten Warnungen in einer SQL Server PDW Appliance nachverfolgt wird.  
  
## <a name="to-track-appliance-alerts"></a>Zum Nachverfolgen von Appliance-Warnungen  
SQL Server PDW erstellt Warnungen für Hardware und Software-Probleme, die ein Eingreifen erforderlich machen. Jede Warnung enthält einen Titel und eine Beschreibung des Problems.  
  
SQL Server PDW protokolliert Warnungen in der [sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV. Das System behält maximal 10.000 Benachrichtigungen und löscht zuerst die älteste Warnung, wenn die Grenze überschritten wird.  
  
### <a name="view-alerts-by-using-the-admin-console"></a>Anzeigen von Warnungen mithilfe der Verwaltungskonsole  
Es ist ein **Warnungen** Registerkarte für die PDW-Region, HDI-Region und für den Bereich "Fabric" der Anwendung. Nach dem Failover auftritt, ist das failoverereignis in die Anzahl der Warnungen auf der Seite enthalten. Es wird eine Seite für die PDW-Region, HDI-Region und für den Bereich "Fabric" der Anwendung. Jede Seite "Integrität" verfügt über eine Registerkarte. Weitere Informationen zu einer Warnung, klicken Sie auf die **Integrität** Seite der **Warnungen** Registerkarte, und klicken Sie dann auf eine Warnung.  
  
![PDW-Verwaltungskonsole, Warnungen](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
Auf der **Warnungen** Seite:  
  
-   Um der Warnung dem Verlauf anzuzeigen, klicken Sie auf die **Überprüfung Warnungsverlauf** Link.  
  
-   Um die Warnung Komponente und ihre aktuellen Eigenschaftswerte anzuzeigen, klicken Sie auf der abrufalgorithmen auf.  
  
-   Zum Anzeigen von Details über den Knoten, die die Warnung ausgelöst hat, klicken Sie auf den Knotennamen.  
  
### <a name="view-alerts-by-using-the-system-views"></a>Anzeigen von Warnungen mithilfe von Systemsichten  
Fragen Sie zum Anzeigen von Warnungen mithilfe von Systemsichten [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md). Diese DMV zeigt Warnungen, die nicht korrigiert wurden. Verwenden Sie die Hilfe zu selektieren Warnungen und Fehler, die [sys.dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV.  
  
Im folgende Beispiel wird eine allgemeine Abfrage für die aktuellen Warnungen anzeigen.  
  
```sql  
SELECT   
    aa.[pdw_node_id],  
    n.[name] AS [node_name],  
    g.[group_name] ,  
    c.[component_name] ,  
    aa.[component_instance_id] ,   
    a.[alert_name] ,  
    a.[state] ,  
    a.[severity] ,  
    aa.[current_value] ,  
    aa.[previous_value] ,  
    aa.[create_time] ,  
    a.[description]   
FROM [sys].[dm_pdw_component_health_active_alerts] AS aa  
    INNER JOIN sys.dm_pdw_nodes AS n   
        ON aa.[pdw_node_id] = n.[pdw_node_id]  
    INNER JOIN [sys].[pdw_health_components] AS c   
        ON aa.[component_id] = c.[component_id]  
    INNER JOIN [sys].[pdw_health_component_groups] AS g   
        ON c.[group_id] = g.[group_id]  
    INNER JOIN [sys].[pdw_health_alerts] AS a   
        ON aa.[alert_id] = a.[alert_id] and aa.[component_id] = c.[component_id]  
ORDER BY  
    a.alert_id ,  
    aa.[pdw_node_id];  
```  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[Überwachen der Appliance &#40;Analyseplattformsystem&#41;](appliance-monitoring.md)  
  
