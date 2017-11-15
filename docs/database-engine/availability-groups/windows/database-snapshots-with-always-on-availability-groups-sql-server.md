---
title: "Datenbankmomentaufnahmen bei Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database snapshots [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 7432da1c-ce2f-4cd9-af41-54c97744166b
caps.latest.revision: "7"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6be95323b653b2b283d6b1f903e33b0bca5cfc8f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="database-snapshots-with-always-on-availability-groups-sql-server"></a>Datenbankmomentaufnahmen bei AlwaysOn-Verfügbarkeitsgruppen (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Sie können auf einer primären oder sekundären Datenbank in einer Verfügbarkeitsgruppe eine Datenbankmomentaufnahme erstellen. Die Replikatrolle muss entweder PRIMARY oder SECONDARY sein und darf nicht den Status RESOLVING aufweisen.  
  
 Der Datenbanksynchronisierungsstatus sollte SYNCHRONIZING oder SYNCHRONIZED sein, wenn Sie eine Datenbankmomentaufnahme erstellen. Datenbankmomentaufnahmen können jedoch auch erstellt werden, wenn der Datenbanksynchronisierungsstatus NOT SYNCHRONIZING lautet.  
  
 Eine Datenbankmomentaufnahme auf einem sekundären Replikat sollte weiterhin funktionieren, wenn das Replikat mit DISCONNECTED vom primären Replikat getrennt wird.  
  
 Einige [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Bedingungen bewirken, dass sowohl die Quelldatenbank als auch deren Datenbankmomentaufnahmen neu gestartet werden, wobei die Verbindung für Benutzer vorübergehend getrennt wird. Nachfolgend sind diese Bedingungen aufgeführt:  
  
-   Das primäre Replikat ändert Rollen, entweder, weil das aktuelle primäre Replikat offline und dann auf der gleichen Serverinstanz wieder online geschaltet wird, oder weil die Verfügbarkeitsgruppe ein Failover ausführt.  
  
-   Die Datenbank wechselt zur sekundäre Rolle.  
  
 Wenn das Verfügbarkeitsreplikat, das Datenbankmomentaufnahmen hostet, ein Failover ausgeführt hat, bleiben die Datenbankmomentaufnahmen auf der Serverinstanz, auf der sie erstellt wurden. Benutzer können die Momentaufnahmen nach dem Failover weiter verwenden. Wenn die Leistung in Ihrer Umgebung wichtig ist, empfiehlt es sich, dass Sie Datenbankmomentaufnahmen nur auf sekundären Datenbanken erstellen, die von einem sekundären Replikat gehostet werden, das für manuellen Failovermodus konfiguriert ist.  Sollte es je zu einem manuellen Failover der Verfügbarkeitsgruppe zu diesem sekundären Replikat kommen, können Sie auf einem anderen sekundären Replikat einen neuen Satz von Datenbankmomentaufnahmen erstellen, Clients an die neuen Datenbankmomentaufnahmen umleiten und alle Datenbankmomentaufnahmen aus den jetzt primären Datenbanken löschen.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Datenbank-Momentaufnahmen &#40;SQL Server&#41;](../../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
