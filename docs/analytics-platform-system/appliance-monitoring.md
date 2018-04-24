---
title: Überwachen der Appliance - Analytics Platform System | Microsoft Docs
description: Dieses Überwachung Appliance-Handbuch beschreibt die Tools und Aufgaben für die Überwachung der Appliance Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f87734a14337e7e35655439ddf70f0a126147eb7
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>Einheit für Analytics Platform System überwachen
Dieses Überwachung Appliance-Handbuch beschreibt die Tools und Aufgaben für die Überwachung der Appliance Analytics Platform System.  
  
## <a name="Basics"></a>Überwachungsgrundlagen und Tools  
Die Werte und die Informationen, die überwacht werden, kann auf der SQL Server PDW Appliance sind umfangreiche. Beispielsweise sind die folgenden Überwachungsaufgaben.  
  
-   Überprüfen Sie für jede Warnung, die von SQL Server PDW ausgegeben.  
  
-   Monitor für fehlerhafte Hardware.  
  
-   Monitor für Probleme bei der Netzwerkkonnektivität.  
  
-   Suchen Sie nach Fehlern, die für Benutzer während der abfrageverarbeitung zurückgegeben.  
  
-   Zeigt die Anzahl der derzeit aktiven Sitzungen und Abfragen.  
  
-   Überprüfen Sie den Status von Lasten, Sicherungen und Wiederherstellungen.  
  
### <a name="appliance-monitoring-tools"></a>Appliance Überwachungstools  
Es sind mehrere Tools verfügbar, um die Anwendung zu überwachen.  
  
Verwaltungskonsole  
SQL Server PDW ist eine Verwaltungskonsole. Dies ist ein webbasiertes Tool, das Informationen zu Abfragen, lädt, Sicherung und Wiederherstellung, sperren, Sitzungen, Warnungen und Anwendungszustand anzeigt. Die-Verwaltungskonsole wird auf dem Gerät ausgeführt. Benutzer eine Verbindung herstellen, um die Verwaltungskonsole über Internet Explorer. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW-Verwaltungskonsole, Warnungen](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
Systemsichten  
SQL Server PDW enthält umfassende Systemsichten, die erhalten Sie detaillierte Informationen zur Integrität der Appliance, Status und Leistung zu ermöglichen. Eine Liste von Systemsichten für Überwachungsaufgaben finden Sie unter:  
  
-   [Überwachen Sie die Anwendung mithilfe von Systemsichten &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operationsmanager (SCOM)  
SQL Server PDW verfügt über umfassende Integration in System Center Operations Manager. Die Management Packs für SQL Server PDW sind als kostenloser Download verfügbar. Weitere Informationen zur Verwendung von System Center zum Überwachen von SQL Server PDW finden Sie hier:  
  
-   [Überwachen Sie die Anwendung mit System Center Operationsmanager &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
Benutzerdefinierte Lösungen  
Für Situationen können Sie beim System Center nicht verfügbar ist, mit Ihrem Rechenzentrum Überwachungstools, das Gerät überwachen, mit einem Drittanbieter-überwachungslösung. Installation von externen Softwareschwachstellen Agents wird in PDW derzeit nicht unterstützt, aber die meisten überwachungslösungen unterstützt Transact\-SQL Integration, damit der Systemadministrator, direkte Transact implementieren kann\-SQL-Abfragen für die PDW Appliance.  
  
Wenn Ihre überwachungslösung keine direkte Transact unterstützt\-SQL-Abfragen, oder Sie verfügen nicht über die Überwachungstools, dann können Sie Skripts zum Ausführen von Überwachungsaufgaben, wie etwa das Versenden von e-Mail, wenn eine Warnung auftritt.  TechNet-Wiki enthält ein Beispiel für skriptbasierte Überwachung Lösung.  
  
-   [Beispiel für SQLServer PDW Überwachung Power-Shell](http://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>Überwachen von Aufgaben beziehen  
  
|Tasks "Überwachung"|Description|  
|-------------------|---------------|  
|Überwachen Sie die Anwendung, indem Sie mithilfe der Verwaltungskonsole.|[Überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|Überwachen Sie das Gerät mithilfe von Systemsichten.|[Überwachen Sie die Anwendung mithilfe von Systemsichten &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-system-views.md)|  
|Überwachen Sie die Anwendung mithilfe von System Center|[Überwachen Sie die Anwendung mit System Center Operationsmanager &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|Überwachen des Status des Geräts.|[Integritätsstatus des Monitors Appliance &#40;Analyseplattformsystem&#41;](monitor-appliance-health-state.md)|  
|Taktüberwachung.|[Telemetriedaten an Microsoft senden &#40;SQLServer PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|Verfolgen Sie Appliance Warnungen.|[Nachverfolgen der Appliance Warnungen &#40;Analyseplattformsystem&#41;](track-appliance-alerts.md)|  
|Bestimmen Sie, wie viel Kapazität verwendet wird.|[Anzeigen der Kapazitätsauslastung &#40;Analyseplattformsystem&#41;](view-capacity-utilization.md)|  
|Bestimmt, wie häufig das Gerät abrufen.|[Bestimmen der Abrufintervalle &#40;Analyseplattformsystem&#41;](determine-polling-frequency.md)|  
|Wenn ein Fehler auftritt, bestimmen, welcher Cluster Knoten ist fehlgeschlagen.|[Feststellen, welche Clusterknoten konnte &#40;Analyseplattformsystem&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Appliance-Verwaltungsaufgaben &#40;Analyseplattformsystem&#41;](appliance-management-tasks.md)  
  
