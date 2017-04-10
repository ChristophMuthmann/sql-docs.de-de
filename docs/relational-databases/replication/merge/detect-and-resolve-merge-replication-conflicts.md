---
title: "Erkennen und Beseitigen von Konflikten bei der Mergereplikation | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Konfliktlösung bei der Mergereplikation [SQL Server-Replikation], Informationen zur Konfliktlösung"
  - "Standardkonfliktlöser"
  - "Konfliktlösung [SQL Server-Replikation]"
  - "Anzeigen von Konflikten bei der Mergereplikation"
  - "Auflösen von Konflikten bei der Mergereplikation"
  - "Artikel [SQL Server-Replikation], Konfliktlösung"
  - "Konfliktlösung bei der Mergereplikation [SQL Server-Replikation]"
  - "Konfliktlösung [SQL Server-Replikation], Mergereplikation "
ms.assetid: 0d033c76-e8c9-4e35-ab95-4d335abb18c1
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Erkennen und Beseitigen von Konflikten bei der Mergereplikation
  Wenn zwischen einem Verleger und einem Abonnenten eine Verbindung besteht und die Synchronisierung vorgenommen wird, werden jegliche Konflikte vom Merge-Agent erkannt. Wenn Konflikte erkannt werden, legt der Merge-Agent mithilfe eines Konfliktlösers fest, welche Daten akzeptiert und für andere Sites weitergegeben werden.  
  
> [!NOTE]  
>  Obwohl ein Abonnement die Synchronisierung mit dem Verleger vornimmt, treten Konflikte in der Regel zwischen Updates auf, die auf verschiedenen Abonnenten vorgenommen wurden, und nicht notwendigerweise zwischen Updates auf einem Abonnenten und dem Verleger.  
  
 Die Mergereplikation bietet eine Reihe unterschiedlicher Methoden zur Erkennung und Lösung von Konflikten. Für die meisten Anwendungen empfiehlt sich die Standardmethode.  
  
-   Wenn es zwischen einem Verleger und einem Abonnenten zu einem Konflikt kommt, wird die Verlegeränderung beibehalten und die Abonnentenänderung verworfen.  
  
-   Wenn es zwischen zwei Abonnenten bei der Verwendung von Clientabonnements (dem Standardtyp für Pullabonnements) zu einem Konflikt kommt, wird die Änderung des Abonnenten beibehalten, der als erster die Synchronisierung mit dem Verleger vornimmt. Die Änderung des zweiten Abonnenten wird verworfen. Informationen zum Angeben von Client- und serverabonnements finden Sie unter [Geben Sie den Abonnementtyp zusammenführen und Konfliktlösungspriorität & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/specify a merge subscription type and conflict resolution priority.md).  
  
-   Wenn es zwischen zwei Abonnenten bei der Verwendung von Serverabonnements (dem Standardtyp für Pushabonnements) zu einem Konflikt kommt, wird die Änderung des Abonnenten mit dem höchsten priority-Wert beibehalten, die Änderung des zweiten Abonnenten wird verworfen. Wenn die priority-Werte identisch sind, wird die Änderung des Abonnenten beibehalten, der als erster die Synchronisierung mit dem Verleger vornimmt.  
  
 Weitere Informationen zur Konflikterkennung und -lösung bei der Mergereplikation finden Sie unter [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
## Siehe auch  
 [Artikeloptionen für die Mergereplikation](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  