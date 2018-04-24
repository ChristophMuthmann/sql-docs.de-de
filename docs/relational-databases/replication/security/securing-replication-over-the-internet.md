---
title: Absichern der Replikation über das Internet | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- security [SQL Server replication], Internet
- Internet [SQL Server replication], security
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
caps.latest.revision: 28
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 56518cc9870f2fc788bdb1e434323ffcb46c0bb7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="securing-replication-over-the-internet"></a>Securing Replication Over the Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die Replikation über das Internet bietet die größtmögliche Flexibilität, insbesondere für mobile Abonnenten. In diesem Fall muss jedoch die Internetreplikation entsprechend konfiguriert werden, um so die Sicherheit sicherstellen zu können. Für die sichere Freigabe von Daten über das Internet werden die folgenden beiden Verfahren von[!INCLUDE[msCoName](../../../includes/msconame-md.md)] empfohlen:  
  
-   Ein virtuelles privates Netzwerk (VPN)  
  
-   Die Websynchronisierungsoption für die Mergereplikation  
  
## <a name="virtual-private-network"></a>Virtuelles privates Netzwerk  
 Virtuelle private Netzwerke bieten ein unkompliziertes und sicheres, in Schichten aufgebautes Verfahren zum Replizieren von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Daten über das Internet. Die VPN-Verbindung über das Internet funktioniert logisch gesehen als WAN-Verbindung (Wide Area Network) zwischen den Standorten.  
  
 Dies wird erreicht, indem der Benutzer eine Tunnelverbindung über das Internet oder ein anderes öffentliches Netzwerk herstellen kann (mithilfe eines Protokolls, z. B. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] PPTP (Point-to-Point Tunneling Protocol), das mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT 4.0 oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000 verfügbar ist, oder L2TP (Layer Two Tunneling Protocol), das als Bestandteil des Betriebssystems Windows 2000 verfügbar ist). Das Verfahren bietet die gleiche Sicherheit und die gleichen Funktionen, wie sie in einem privaten Netzwerk verfügbar sind.  
  
 Weitere Informationen zum Einrichten eines VPN finden Sie in der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Dokumentation.  
  
## <a name="web-synchronization-through-iis"></a>Websynchronisierung über IIS  
 Mit der Websynchronisierung für die Mergereplikation ist es möglich, Daten mit dem HTTPS-Protokoll zu replizieren; so können auch Daten durch eine Firewall repliziert werden. Weitere Informationen finden Sie unter [Konfigurieren der Websynchronisierung](../../../relational-databases/replication/configure-web-synchronization.md) und [Sicherheitsarchitektur für die Websynchronisierung](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicherheit und Schutz &#40;Replikation&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
