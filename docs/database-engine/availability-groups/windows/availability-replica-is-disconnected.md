---
title: "Verfügbarkeitsreplikat wird getrennt | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.agdashboard.arp2connected.issues.f1
helpviewer_keywords: Availability Groups [SQL Server], policies
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
caps.latest.revision: "12"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c81fc6a1851792d62ed947d88591675eeeed5366
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="availability-replica-is-disconnected"></a>Verfügbarkeitsreplikat wird getrennt
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Verfügbarkeitsreplikat-Verbindungsstatus|  
|**Problem**|Das Verfügbarkeitsreplikat wird getrennt.|  
|**Kategorie**|**Kritisch**|  
|**Facet**|Verfügbarkeitsreplikat|  
  
## <a name="description"></a>Beschreibung  
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
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
