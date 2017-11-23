---
title: Bestimmen Sie, welche Clusterknoten (Analytics Platform System) ist fehlgeschlagen.
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e001117-a1b6-4357-bf25-e85aba3f1cf0
caps.latest.revision: "21"
ms.openlocfilehash: 59f188526cff2d605c5bffcf2187b3c765276c81
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="determine-which-cluster-node-failed"></a>Feststellen Sie, welche Clusterknoten fehlgeschlagen
In diesem Thema wird beschrieben, wie Sie den Namen des SQL Server PDW-Knotens zu ermitteln, die fehlgeschlagen ein Clusterfailover aufgetreten ist und eine Cluster-Failover-Warnung ausgelöst wurde. Im Rahmen der Problembehandlung eines clusterfailovers durchgeführt müssen Sie den Namen des Knotens ermitteln, die nicht vor der Kontaktaufnahme mit Microsoft, um das Problem zu beheben.  
  
## <a name="Background"></a>Im Hintergrund  
Für hohe Verfügbarkeit in SQL Server PDW werden die Knoten "Zugriffssteuerung" und die Serverknoten als aktiv oder Passiv Komponenten des Windows-Failovercluster konfiguriert. Wenn ein aktiver Server nicht auf kritische System-Anforderungen reagieren, wird der passive Server ein Failover und führt die Funktionen des Servers, der Fehler.  
  
Nach einem Clusterfailover beim SQL Server PDW Knotenstatus, meldet der passive Server muss eines fehlerhaften über Status. Allerdings ist es nicht offensichtliche Fehler bei der Server oder Knoten, insbesondere dann, wenn der Server, der Fehler noch immer online ist. Um den Fehler zu beheben, müssen Sie den Namen des Knotens ermitteln, die ein Failover ausgeführt.  
  
## <a name="AdminConsoleSolution"></a>-Verwaltungskonsole-Lösung  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>Um den Namen des Knotens zu finden, die fehlgeschlagen  
  
1.  Öffnen Sie die Admin-Konsole. Weitere Informationen über die Verwaltungskonsole finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40; Analyseplattformsystem &#41; ](monitor-the-appliance-by-using-the-admin-console.md). Nach dem Failover auftritt, ist das failoverereignis in die Anzahl der Warnungen auf enthalten die **INTEGRITÄT** Seite. Ist ein **INTEGRITÄT** Seite für die PDW-Region, HDI-Region und für den Bereich "Fabric" der Anwendung. Jede Seite Integrität verfügt über eine **WARNUNGEN** Registerkarte. Klicken Sie auf der Statusseite der Registerkarte "Warnungen", und klicken Sie dann auf eine Warnung, um weitere Informationen zu einer Warnung.  
  
## <a name="SystemView"></a>System-Ansicht-Lösung  
Die folgende SQL-Anweisung zeigt, wie die [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) Systemsicht, um den Namen des Servers zu finden, die nicht.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
