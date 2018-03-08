---
title: MSSQLSERVER_41030 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 41030 (Database Engine error)
ms.assetid: c85341ae-0fbf-42ae-9275-4cfe678238f0
caps.latest.revision: "6"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb6128fc5009532100df1b35b4414a014a9f09f4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver41030"></a>MSSQLSERVER_41030
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|41030|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|OPEN_CLUSTER_SUB_KEY|  
|Meldungstext|Fehler beim Öffnen des WSFC (Windows Server Failover Clustering)-Registrierungsunterschlüssels '%.*ls' (Fehlercode %d).  Der übergeordnete Schlüssel ist der Clusterstammschlüssel.  Der WSFC-Dienst wird möglicherweise nicht ausgeführt, der Zugriff auf den Dienst ist möglicherweise im aktuellen Zustand nicht möglich, oder die angegebenen Argumente sind ungültig. Wurde die entsprechende Verfügbarkeitsgruppe gelöscht, wird dieser Fehler erwartet. Informationen zu diesem Fehlercode finden Sie in der Dokumentation für die Windows-Entwicklung im Abschnitt zu Systemfehlercodes.|  
  
## <a name="explanation"></a>Erklärung  
Wenn ein WSFC-Cluster zerstört wird, werden alle auf [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] bezogenen Registrierungsschlüssel entfernt.  
  
## <a name="user-action"></a>Benutzeraktion  
Nach dem Neuerstellen eines WSFC-Clusters deaktivieren und aktivieren Sie dann AlwaysOn auf jedem Clusterknoten erneut, auf dem eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz für AlwaysOn aktiviert wird. Sie können für diese Aufgabe den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager verwenden.  
  
## <a name="see-also"></a>Siehe auch  
[Aktivieren und Deaktivieren von Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
[Windows Server-Failoverclustering &#40;WSFC&#41; mit SQL Server](~/sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
