---
title: Erkennen und Beseitigen von Konflikten bei der Mergereplikation | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67147bca1980bb0ff8e53faf8ff51147ec4ab1de
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="advanced-merge-replication---resolve-merge-replication-conflicts"></a>Erweiterte Mergereplikation – Beseitigen von Mergereplikation bei Konflikten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Wenn zwischen einem Verleger und einem Abonnenten eine Verbindung besteht und die Synchronisierung vorgenommen wird, werden jegliche Konflikte vom Merge-Agent erkannt. Wenn Konflikte erkannt werden, legt der Merge-Agent mithilfe eines Konfliktlösers fest, welche Daten akzeptiert und für andere Sites weitergegeben werden.  
  
> [!NOTE]  
>  Obwohl ein Abonnement die Synchronisierung mit dem Verleger vornimmt, treten Konflikte in der Regel zwischen Updates auf, die auf verschiedenen Abonnenten vorgenommen wurden, und nicht notwendigerweise zwischen Updates auf einem Abonnenten und dem Verleger.  
  
 Die Mergereplikation bietet eine Reihe unterschiedlicher Methoden zur Erkennung und Lösung von Konflikten. Für die meisten Anwendungen empfiehlt sich die Standardmethode.  
  
-   Wenn es zwischen einem Verleger und einem Abonnenten zu einem Konflikt kommt, wird die Verlegeränderung beibehalten und die Abonnentenänderung verworfen.  
  
-   Wenn es zwischen zwei Abonnenten bei der Verwendung von Clientabonnements (dem Standardtyp für Pullabonnements) zu einem Konflikt kommt, wird die Änderung des Abonnenten beibehalten, der als erster die Synchronisierung mit dem Verleger vornimmt. Die Änderung des zweiten Abonnenten wird verworfen. Informationen zum Angeben von Client- und Serverabonnements finden Sie unter [Angeben eines Mergeabonnementtyps und einer Konfliktlösungspriorität &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md).  
  
-   Wenn es zwischen zwei Abonnenten bei der Verwendung von Serverabonnements (dem Standardtyp für Pushabonnements) zu einem Konflikt kommt, wird die Änderung des Abonnenten mit dem höchsten priority-Wert beibehalten, die Änderung des zweiten Abonnenten wird verworfen. Wenn die priority-Werte identisch sind, wird die Änderung des Abonnenten beibehalten, der als erster die Synchronisierung mit dem Verleger vornimmt.  
  
 Weitere Informationen zur Konflikterkennung und -lösung bei der Mergereplikation finden Sie unter [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Article Options for Merge Replication](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
