---
title: Erneutes Initialisieren von Abonnements | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
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
- initializing subscriptions [SQL Server replication], reinitializing
- subscriptions [SQL Server replication], reinitializing
- reinitializing subscriptions
ms.assetid: fb13712b-e7ad-4f1f-b605-4554bad0cb60
caps.latest.revision: "51"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6992c5af122689e75b9cf145f831346f9f63de32
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="reinitialize-subscriptions"></a>Erneutes Initialisieren von Abonnements
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Beim erneuten Initialisieren eines Abonnements wird eine neue Momentaufnahme auf einen oder mehrere Artikel auf einem oder mehreren Abonnenten angewendet, wobei bei der Transaktions- und der Momentaufnahmenreplikation das erneute Initialisieren einzelner Artikel möglich ist, während bei der Mergereplikation alle Artikel erneut initialisiert werden müssen. Knoten in einer Peer-zu-Peer-Transaktionsreplikationstopologie können nicht erneut initialisiert werden. Wenn Sie sicherstellen müssen, dass ein Knoten eine neue Kopie der Daten besitzt, stellen Sie an diesem Knoten eine Sicherung wieder her. Die Neuinitialisierung erfolgt aus einem der folgenden beiden Gründe:  
  
-   Sie kennzeichnen explizit ein Abonnement für die Neuinitialisierung.  
  
-   Sie führen eine Aktion, wie z. B. die Änderung einer Eigenschaft, aus, die eine Neuinitialisierung erforderlich macht. Weitere Informationen zu Aktionen, die eine Neuinitialisierung erfordern, finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
 In beiden Fällen wird bei der nächsten Ausführung des Verteilungs-Agents oder des Merge-Agents auf den Abonnenten die neueste Momentaufnahme angewendet. Bei der Momentaufnahme- und Transaktionsreplikation werden während der Neuinitialisierung alle auf dem Abonnenten vorgenommenen Änderungen, die noch nicht mit dem Verleger synchronisiert wurden, durch Anwenden der neuen Momentaufnahme überschrieben.  
  
 Bei der Mergereplikation können Sie festlegen, ob vor der Anwendung der Momentaufnahme alle Datenänderungen vom Abonnenten hochgeladen werden. Alle ausstehenden Schemaänderungen vom Verleger werden auf den Abonnenten angewendet. Anschließend werden alle Updates auf dem Abonnenten seit der letzten Synchronisierung an den Verleger weitergeleitet, bevor die Momentaufnahme erneut angewendet wird. Dieses Verhalten wird durch die **upload_first** - und **automatic_reinitialization_policy** -Eigenschaften gesteuert. Weitere Informationen dazu finden Sie unter [Reinitialize a Subscription](../../relational-databases/replication/reinitialize-a-subscription.md). Wenn Sie ein Abonnement für eine Neuinitialisierung in SQL Server Management Studio oder im Replikationsmonitor kennzeichnen, können Sie im Dialogfeld **Abonnements erneut initialisieren** festlegen, dass zuerst die Änderungen hochgeladen werden.  
  
> [!IMPORTANT]  
>  Wenn Sie einen parametrisierten Filter in einer Mergereplikation hinzufügen, löschen oder ändern, können die ausstehenden Änderungen auf dem Abonnenten während der erneuten Initialisierung nicht auf den Verleger hochgeladen werden. Wenn Sie ausstehende Änderungen hochladen möchten, sollten Sie vor dem Ändern des Filters alle Abonnements synchronisieren.  
  
 Wenn Sie beim Erstellen des Abonnements angegeben haben, dass keine Anfangsmomentaufnahme auf den Abonnenten angewendet werden soll, und Sie dann dieses Abonnement für eine erneute Initialisierung kennzeichnen, wird keine Momentaufnahme angewendet. Weitere Informationen finden Sie unter [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)initialisiert wird.  
  
 **So initialisieren Sie ein Abonnement erneut**  
  
 Wenn alle Artikel in einem Abonnement erneut initialisiert werden sollen, verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], gespeicherte Prozeduren oder Replikationsverwaltungsobjekte (RMO, Replication Management Objects). Wenn nur bestimmte Artikel in einer Momentaufnahme- oder Transaktionsveröffentlichung erneut initialisiert werden sollen, müssen Sie dazu gespeicherte Prozeduren verwenden. Weitere Informationen finden Sie unter [Reinitialize a Subscription](../../relational-databases/replication/reinitialize-a-subscription.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Initialisieren eines Abonnements](../../relational-databases/replication/initialize-a-subscription.md)   
 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
