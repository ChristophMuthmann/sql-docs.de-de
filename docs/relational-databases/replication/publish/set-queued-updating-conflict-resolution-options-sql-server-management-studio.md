---
title: "Festlegen der Konfliktlösungsoptionen für verzögerte Updates über eine Warteschlange (SQL Server Management Studio) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b381a3aedb418c95b5f10ce9a238eb27a9f6fcf8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>Festlegen der Konfliktlösungsoptionen für verzögerte Updates über eine Warteschlange (SQL Server Management Studio)
  Die Konfliktlösungsoptionen für Veröffentlichungen, die Abonnements mit verzögertem Update über eine Warteschlange unterstützen, werden auf der Seite **Abonnementoptionen** des Dialogfelds **Veröffentlichungseigenschaften - \<Veröffentlichung>** festgelegt. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>So legen Sie die Konfliktlösungsoptionen für das verzögerte Update über eine Warteschlange fest  
  
1.  Wählen Sie auf der Seite **Abonnementoptionen** des Dialogfelds **Veröffentlichungseigenschaften - \<Veröffentlichung>** für die Option **Richtlinie zur Konfliktlösung** einen der folgenden Werte aus:  
  
    -   **Verlegeränderung beibehalten**  
  
    -   **Abonnentenänderung beibehalten**  
  
    -   **Abonnement erneut initialisieren**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Aktivieren des Aktualisierens von Abonnements für Transaktionsveröffentlichungen](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
