---
title: Verfügbarkeitsreplikat wird getrennt | Microsoft-Dokumentation
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
f1_keywords:
- sql13.swb.agdashboard.arp2connected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5aa01f0ea773dfd57b258e4cc43b08a98360604f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="availability-replica-is-disconnected"></a>Verfügbarkeitsreplikat wird getrennt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Verfügbarkeitsreplikat-Verbindungsstatus|  
|**Problem**|Das Verfügbarkeitsreplikat wird getrennt.|  
|**Kategorie**|**Kritisch**|  
|**Facet**|Verfügbarkeitsreplikat|  
  
## <a name="description"></a>Description  
 Diese Richtlinie überprüft den Verbindungsstatus zwischen Verfügbarkeitsreplikaten. Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn der Verbindungsstatus des Verfügbarkeitsreplikats DISCONNECTED lautet. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Availability replica is disconnected](http://go.microsoft.com/fwlink/p/?LinkId=220857) (Verfügbarkeitsreplikat ist getrennt).  
  
## <a name="possible-causes"></a>Mögliche Ursachen  
 Das sekundäre Replikat ist nicht mit dem primären Replikat verbunden. Der Verbindungsstatus lautet DISCONNECTED. Dieses Problem kann folgende Ursachen haben:  
  
-   Für den Verbindungsport besteht ein Konflikt mit einer anderen Anwendung.  
  
-   Der Verschlüsselungstyp oder der Algorithmus stimmt nicht überein.  
  
-   Der Verbindungsendpunkt wurde gelöscht oder nicht gestartet.  
  
-   Die Verbindung des Transports wurde getrennt.  
  
## <a name="possible-solutions"></a>Mögliche Lösungen  
 Für dieses Problem gibt es die folgenden möglichen Lösungen:  
  
-   Überprüfen Sie die Datenbankspiegelungs-Endpunktkonfiguration für die Instanzen des primären und sekundären Replikats, und aktualisieren Sie die nicht übereinstimmende Konfiguration.  
  
-   Überprüfen Sie, ob für den Port ein Konflikt besteht, und ändern Sie ggf. die Portnummer.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des AlwaysOn-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
