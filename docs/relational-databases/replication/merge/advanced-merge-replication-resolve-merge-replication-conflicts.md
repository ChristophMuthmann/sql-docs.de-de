---
title: Erkennen und Beseitigen von Konflikten bei der Mergereplikation | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- conflict resolution [SQL Server replication]
- viewing merge replication conflicts
- resolving merge replication conflicts
- articles [SQL Server replication], conflict resolution
- merge replication conflict resolution [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 0d033c76-e8c9-4e35-ab95-4d335abb18c1
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea0d016f2fc6e73be6458ed44f34f42dfbd140bf
ms.lasthandoff: 04/11/2017

---
# <a name="advanced-merge-replication---resolve-merge-replication-conflicts"></a>Erweiterte Mergereplikation – Beseitigen von Mergereplikation bei Konflikten
  Wenn zwischen einem Verleger und einem Abonnenten eine Verbindung besteht und die Synchronisierung vorgenommen wird, werden jegliche Konflikte vom Merge-Agent erkannt. Wenn Konflikte erkannt werden, legt der Merge-Agent mithilfe eines Konfliktlösers fest, welche Daten akzeptiert und für andere Sites weitergegeben werden.  
  
> [!NOTE]  
>  Obwohl ein Abonnement die Synchronisierung mit dem Verleger vornimmt, treten Konflikte in der Regel zwischen Updates auf, die auf verschiedenen Abonnenten vorgenommen wurden, und nicht notwendigerweise zwischen Updates auf einem Abonnenten und dem Verleger.  
  
 Die Mergereplikation bietet eine Reihe unterschiedlicher Methoden zur Erkennung und Lösung von Konflikten. Für die meisten Anwendungen empfiehlt sich die Standardmethode.  
  
-   Wenn es zwischen einem Verleger und einem Abonnenten zu einem Konflikt kommt, wird die Verlegeränderung beibehalten und die Abonnentenänderung verworfen.  
  
-   Wenn es zwischen zwei Abonnenten bei der Verwendung von Clientabonnements (dem Standardtyp für Pullabonnements) zu einem Konflikt kommt, wird die Änderung des Abonnenten beibehalten, der als erster die Synchronisierung mit dem Verleger vornimmt. Die Änderung des zweiten Abonnenten wird verworfen. Informationen zum Angeben von Client- und Serverabonnements finden Sie unter [Angeben eines Mergeabonnementtyps und einer Konfliktlösungspriorität &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md).  
  
-   Wenn es zwischen zwei Abonnenten bei der Verwendung von Serverabonnements (dem Standardtyp für Pushabonnements) zu einem Konflikt kommt, wird die Änderung des Abonnenten mit dem höchsten priority-Wert beibehalten, die Änderung des zweiten Abonnenten wird verworfen. Wenn die priority-Werte identisch sind, wird die Änderung des Abonnenten beibehalten, der als erster die Synchronisierung mit dem Verleger vornimmt.  
  
 Weitere Informationen zur Konflikterkennung und -lösung bei der Mergereplikation finden Sie unter [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Artikeloptionen für die Mergereplikation](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
