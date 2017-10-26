---
title: "Verfügbarkeitsgruppe ist offline | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.agdashboard.agp2online.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 093c5208-bf7a-49f4-a546-72b48197cadf
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c64ddb1c8c152594a359c1b10e0cb621e25bc11e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="availability-group-is-offline"></a>Verfügbarkeitsgruppe ist offline
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Onlinezustand der Verfügbarkeitsgruppe|  
|**Problem**|Die Verfügbarkeitsgruppe ist offline.|  
|**Kategorie**|**Kritisch**|  
|**Facet**|Verfügbarkeitsgruppe|  
  
## <a name="description"></a>Beschreibung  
 Diese Richtlinie überprüft den Online- oder Offlinestatus der Verfügbarkeitsgruppe. Die Richtlinie befindet sich in einem fehlerhaften Zustand, und eine Warnung wird ausgelöst, wenn die Clusterressource der Verfügbarkeitsgruppe offline ist oder wenn die Verfügbarkeitsgruppe nicht über ein primäres Replikat verfügt.  
  
 Der Zustand der Richtlinie ist fehlerfrei, wenn die Clusterressource der Verfügbarkeitsgruppe online ist und die Verfügbarkeitsgruppe über ein primäres Replikat verfügt.  
  
> [!NOTE]  
>  Für dieses Release von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Availability group is offline](http://go.microsoft.com/fwlink/p/?LinkId=220850) (Verfügbarkeitsgruppe ist offline).  
  
## <a name="possible-causes"></a>Mögliche Ursachen  
 Dieses Problem kann von einem Fehler in der Serverinstanz verursacht werden, die das primäre Replikat hostet, oder dadurch, dass die Windows Server-Failovercluster (WSFC)-Verfügbarkeitsgruppenressource offline geht. Im Folgenden sind mögliche Ursachen für den Offlinezustand der Verfügbarkeitsgruppe aufgeführt:  
  
-   Die Verfügbarkeitsgruppe ist nicht für den automatischen Failovermodus konfiguriert. Das primäre Replikat ist nicht mehr verfügbar, und alle Replikate in der Verfügbarkeitsgruppe nehmen den Status RESOLVING an.  
  
    -   Der Instanzdienst des primären Replikats ist ausgefallen oder reagiert nicht.  
  
    -   Für die Verfügbarkeitsgruppe besteht ein Problem bei der Verbindung zum Cluster.  
  
-   Die Verfügbarkeitsgruppe wurde mit automatischem Failovermodus konfiguriert und nicht erfolgreich abgeschlossen.  
  
    -   Während des automatischen Failovers tritt für die primäre Bereitschaftsüberprüfung auf dem Zielreplikat ein Fehler auf, und es ist kein Replikat verfügbar, das zum neuen primären Replikat werden kann.  
  
-   Die Verfügbarkeitsgruppenressource im Cluster ist offline.  
  
    -   In einer abhängigen Clusterressource tritt ein schwerwiegendes Problem auf, und die Ressource wird in den Offlinezustand versetzt. Die Verfügbarkeitsgruppenressource ist ebenfalls offline, bis die abhängige Ressource online geschaltet wird.  
  
    -   Durch ein schwerwiegendes Problem im Cluster wird die Verfügbarkeitsgruppenressource deaktiviert.  
  
-   Für die Verfügbarkeitsgruppe wird ein automatisches, manuelles oder erzwungenes Failover durchgeführt.  
  
## <a name="possible-solutions"></a>Mögliche Lösungen  
 Für dieses Problem gibt es die folgenden möglichen Lösungen:  
  
-   Wenn die SQL Server-Instanz des primären Replikats ausgefallen ist, starten Sie den Server neu, und überprüfen Sie dann, ob die Verfügbarkeitsgruppe wieder einen ordnungsgemäßen Zustand erreicht.  
  
-   Falls anscheinend für das automatische Failover ein Fehler aufgetreten ist, überprüfen Sie, ob die Datenbanken auf dem Replikat mit dem zuvor bekannten primären Replikat synchronisiert werden, und führen Sie dann das Failover auf das primäre Replikat durch. Falls die Datenbanken nicht synchronisiert werden, wählen Sie ein Replikat mit einem minimalen Datenverlust aus und stellen dann den Failovermodus wieder her.  
  
-   Falls die Ressource im Cluster offline ist, während die Instanzen von SQL Server anscheinend fehlerfrei sind, verwenden Sie den Failovercluster-Manager, um den Clusterzustand oder andere Clusterprobleme auf dem Server zu überprüfen. Sie können mit dem Failovercluster-Manager auch versuchen, die Verfügbarkeitsgruppenressource wieder in den Onlinezustand zu versetzen.  
  
-   Falls gerade ein Failover durchgeführt wird, warten Sie, bis das Failover abgeschlossen ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  

