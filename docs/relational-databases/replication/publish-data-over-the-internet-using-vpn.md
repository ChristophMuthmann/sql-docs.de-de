---
title: "Veröffentlichen von Daten über das Internet mithilfe von VPN | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- VPNs [SQL Server replication]
- Web publishing [SQL Server replication], VPNs
- Internet [SQL Server replication], VPNs
ms.assetid: 9ffb6546-9973-4574-aaa0-8fe0017e3601
caps.latest.revision: "33"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a851ec36920e6300a25ebf815e8f1c6998263d5
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="publish-data-over-the-internet-using-vpn"></a>Veröffentlichen von Daten über das Internet mithilfe von VPN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die VPN-Technologie (Virtual Private Network) ermöglicht Benutzern, die von zu Hause aus, in Niederlassungen, an Remoteclients oder in anderen Unternehmen arbeiten, eine Verbindung mit einem Unternehmensnetzwerk über das Internet herzustellen, während gleichzeitig die Sicherheit der Verbindung aufrechterhalten wird. Benutzer können die Windows-Authentifizierung so verwenden, als ob sie sich in einem lokalen Netzwerk (Local Area Network, LAN) befänden. Alle Arten der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation können Daten über VPN replizieren, aber Sie sollten beim Verwenden der Mergereplikation die Websynchronisierung verwenden, da durch die Websynchronisierung VPN nicht mehr erforderlich ist. Weitere Informationen finden Sie unter [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Ein VPN enthält Clientsoftware, sodass sich Computer über das Internet (oder in besonderen Fällen auch über ein Intranet) mit Software auf einem dedizierten Computer oder einem Server verbinden können. Optional können auf beiden Seiten die Verschlüsselung sowie Methoden zur Benutzerauthentifizierung verwendet werden. Die VPN-Verbindung über das Internet funktioniert logisch gesehen als WAN-Verbindung (Wide Area Network) zwischen den Standorten.  
  
 Ein VPN verbindet die Komponenten eines Netzwerks über ein anderes Netzwerk. Zu diesem Zweck stellt der Benutzer mithilfe eines Protokolls, wie z. B. des [!INCLUDE[msCoName](../../includes/msconame-md.md)] PPTP (Point-to-Point Tunneling Protocol) oder des L2TP (Layer Two Tunneling Protocol), eine Tunnelverbindung über das Internet oder ein anderes öffentliches Netzwerk her. Das Verfahren bietet die gleiche Sicherheit und die gleichen Funktionen, wie sie zuvor nur in einem privaten Netzwerk verfügbar waren. PPTP ist mit den Betriebssystemen Microsoft Windows NT, Version 4.0, und [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 (und höher) verfügbar; L2TP ist mit Windows 2000 und höher verfügbar.  
  
 Für den Benutzer ist die temporäre Routinginfrastruktur über das Internet nicht sichtbar, und es entsteht der Eindruck, als ob die Daten über einen dedizierten privaten Link gesendet werden. Was die Benutzer angeht, so ist das VPN eine Punkt-zu-Punkt-Verbindung zwischen dem Benutzercomputer und einem Unternehmensserver.  
  
 Nachdem Sie den Remoteclient konfiguriert haben, sodass er eine Verbindung mithilfe eines VPNs herstellt, und der Client über Internetzugriff verfügt und sich am unternehmenseigenen LAN anmeldet, können Sie die Replikation so konfigurieren, als ob der Remoteclient direkt mit dem LAN verbunden ist. Aus Sicherheitsgründen besteht die Möglichkeit, dass verschiedene Netzwerkressourcen für die Benutzer, die über VPN verbunden sind, und für die Benutzer, die direkt im LAN arbeiten, verfügbar sind.  
  
 Weitere Informationen zum Einrichten eines VPN finden Sie in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Dokumentation.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Replikation über das Internet](../../relational-databases/replication/replication-over-the-internet.md)  
  
  
