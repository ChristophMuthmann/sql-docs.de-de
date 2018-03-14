---
title: "Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement (Replikationsmonitor) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
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
- subscriptions [SQL Server replication], viewing information
- subscriptions [SQL Server replication], Replication Monitor tasks
- viewing subscription information
ms.assetid: 54aac83b-6f29-40d7-8901-cf059749867f
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e860780f284c6d7315045e9fd3bd04a7a4a83b8
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="view-information-and-perform-tasks-for-a-subscription-replication-monitor"></a>Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement (Replikationsmonitor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Der Replikationsmonitor umfasst folgende Registerkarten mit Informationen zu Abonnements:  
  
-   **Alle Abonnements**  
  
     Auf dieser Registerkarte werden Informationen zu allen Abonnements für die ausgewählte Veröffentlichung angezeigt.  
  
-   **Überwachungsliste für Abonnements**  
  
     Auf dieser Registerkarte werden Informationen zu Abonnements von allen auf dem ausgewählten Verleger vorhandenen Veröffentlichungen angezeigt, für die Fehlermeldungen oder Warnungen ausgegeben wurden bzw. bei denen Leistungsprobleme aufgetreten sind. Bei Verteilern, auf denen Versionen vor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]ausgeführt werden, wird diese Registerkarte nicht angezeigt.  
  
 Weitere Informationen zu den Optionen der einzelnen Registerkarten finden Sie, wenn Sie auf die Registerkarte im rechten Bereich und dann auf **Hilfe** auf der Menüleiste klicken. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-all-subscriptions-tab"></a>So zeigen Sie Informationen für Abonnements in der Registerkarte Alle Abonnements an und führen Aufgaben aus  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Um Informationen zu Abonnements anzuzeigen, klicken Sie auf die Registerkarte **Alle Abonnements** . Um nur die Abonnements anzuzeigen, die sich in einem bestimmten Status befinden, wie z. B. diejenigen, die gerade synchronisiert werden, wählen Sie die entsprechende Option aus der Dropdownliste **Anzeigen** aus.  
  
3.  Zum Anzeigen und Ändern von Abonnementeigenschaften klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Eigenschaften**. Sie können auf dieser Registerkarte auch auf detailliertere Informationen zugreifen und Aufgaben ausführen. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agent &#40;Replikationsmonitor &#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-subscription-watch-list-tab"></a>So zeigen Sie Informationen für Abonnements in der Registerkarte "Überwachungsliste für Abonnements" an und führen Aufgaben aus  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, und klicken Sie dann auf einen Verleger.  
  
2.  Um Informationen zu Abonnements anzuzeigen, klicken Sie auf die Registerkarte **Überwachungsliste für Abonnements** .  
  
3.  Wählen Sie den anzuzeigenden Abonnementtyp aus der Dropdownliste **\<SubscriptionType>-Abonnements anzeigen** aus. Um nur die Abonnements anzuzeigen, die sich in einem bestimmten Status befinden, wie z. B. diejenigen, die gerade synchronisiert werden, wählen Sie die entsprechende Option aus der Dropdownliste **Anzeigen** aus.  
  
4.  Zum Anzeigen und Ändern von Abonnementeigenschaften klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Eigenschaften**. Sie können auf dieser Registerkarte auch auf detailliertere Informationen zugreifen und Aufgaben ausführen. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agent &#40;Replikationsmonitor &#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
