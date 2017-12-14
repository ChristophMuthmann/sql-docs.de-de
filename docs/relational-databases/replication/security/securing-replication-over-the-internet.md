---
title: "Absichern der Replikation über das Internet | Microsoft-Dokumentation"
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
- security [SQL Server replication], Internet
- Internet [SQL Server replication], security
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d8ddd74c1e1e44c2b905a80b8e622d08a7758a5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="securing-replication-over-the-internet"></a>Absichern der Replikation über das Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die Replikation über das Internet bietet die größtmögliche Flexibilität, insbesondere für mobile Abonnenten. In diesem Fall muss jedoch die Internetreplikation entsprechend konfiguriert werden, um so die Sicherheit sicherstellen zu können. Für die sichere Freigabe von Daten über das Internet werden die folgenden beiden Verfahren von[!INCLUDE[msCoName](../../../includes/msconame-md.md)] empfohlen:  
  
-   Ein virtuelles privates Netzwerk (VPN)  
  
-   Die Websynchronisierungsoption für die Mergereplikation  
  
## <a name="virtual-private-network"></a>Virtuelles privates Netzwerk  
 Virtuelle private Netzwerke bieten ein unkompliziertes und sicheres, in Schichten aufgebautes Verfahren zum Replizieren von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Daten über das Internet. Die VPN-Verbindung über das Internet funktioniert logisch gesehen als WAN-Verbindung (Wide Area Network) zwischen den Standorten.  
  
 Dies wird erreicht, indem der Benutzer eine Tunnelverbindung über das Internet oder ein anderes öffentliches Netzwerk herstellen kann (mithilfe eines Protokolls, z. B. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] PPTP (Point-to-Point Tunneling Protocol), das mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT 4.0 oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000 verfügbar ist, oder L2TP (Layer Two Tunneling Protocol), das als Bestandteil des Betriebssystems Windows 2000 verfügbar ist). Das Verfahren bietet die gleiche Sicherheit und die gleichen Funktionen, wie sie in einem privaten Netzwerk verfügbar sind.  
  
 Weitere Informationen zum Einrichten eines VPN finden Sie in der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Dokumentation.  
  
## <a name="web-synchronization-through-iis"></a>Websynchronisierung über IIS  
 Mit der Websynchronisierung für die Mergereplikation ist es möglich, Daten mit dem HTTPS-Protokoll zu replizieren; so können auch Daten durch eine Firewall repliziert werden. Weitere Informationen finden Sie unter [Konfigurieren der Websynchronisierung](../../../relational-databases/replication/configure-web-synchronization.md) und [Sicherheitsarchitektur für die Websynchronisierung](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicherheit und Schutz &#40;Replikation&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
