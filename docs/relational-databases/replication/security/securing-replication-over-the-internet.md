---
title: "Absichern der Replikation &#252;ber das Internet | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sicherheit [SQL Server-Replikation], Internet"
  - "Internet [SQL Server-Replikation], Sicherheit"
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Absichern der Replikation &#252;ber das Internet
  Die Replikation über das Internet bietet die größtmögliche Flexibilität, insbesondere für mobile Abonnenten. In diesem Fall muss jedoch die Internetreplikation entsprechend konfiguriert werden, um so die Sicherheit sicherstellen zu können. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] empfohlen:  
  
-   Ein virtuelles privates Netzwerk (VPN)  
  
-   Die Websynchronisierungsoption für die Mergereplikation  
  
## Virtuelles privates Netzwerk  
 Virtuelle private Netzwerke bieten ein unkompliziertes und sicheres, in Schichten aufgebautes Verfahren zum Replizieren von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Daten über das Internet. Die VPN-Verbindung über das Internet funktioniert logisch gesehen als WAN-Verbindung (Wide Area Network) zwischen den Standorten.  
  
 Dies wird erreicht, weil der Benutzer Tunnel über das Internet oder ein anderes öffentliches Netzwerk mithilfe eines Protokolls wie z. B. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Point-Tunneling-Protokoll (PPTP) zur Verfügung, mit der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT Version 4.0 oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000-Betriebssystem oder Layer Two Tunneling Protocol (L2TP) mit dem Betriebssystem Windows 2000 verfügbar. Das Verfahren bietet die gleiche Sicherheit und die gleichen Funktionen, wie sie in einem privaten Netzwerk verfügbar sind.  
  
 Weitere Informationen zum Einrichten eines VPN finden Sie in der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Dokumentation.  
  
## Websynchronisierung über IIS  
 Mit der Websynchronisierung für die Mergereplikation ist es möglich, Daten mit dem HTTPS-Protokoll zu replizieren; so können auch Daten durch eine Firewall repliziert werden. Weitere Informationen finden Sie unter [Configure Web Synchronization](../../../relational-databases/replication/configure-web-synchronization.md) und [-Sicherheitsarchitektur für die Synchronisierung von](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md).  
  
## Siehe auch  
 [Bewährte Methoden für die Replikationssicherheit](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicherheit und Schutz & #40; Replikation & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  