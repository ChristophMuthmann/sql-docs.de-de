---
title: Synchronisieren von Abonnements (Replikation) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- synchronization [SQL Server replication], subscriptions
- subscriptions [SQL Server replication], synchronizing
- replication [SQL Server], synchronization
ms.assetid: cbe13120-8dd9-4309-88dd-07a801c68f5f
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c03c4e5ac9974003e5be7e7f647d425618d06fd7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="synchronize-subscriptions-replication"></a>Synchronisieren von Abonnements (Replikation)
  Abonnements werden von Replikations-Agents synchronisiert. Der Verteilungs-Agent synchronisiert Abonnements für Transaktions- und Momentaufnahmeabonnements, und der Merge-Agent synchronisiert Abonnements für Mergeveröffentlichungen. Sie können mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], gespeicherten Replikationsprozeduren und Replikationsverwaltungsobjekten (RMO) Abonnements synchronisieren und das Sychronisierungsverhalten steuern. In den folgenden Themen wird beschrieben, wie Sie Abonnements synchronisieren und Synchronisierungsoptionen angeben.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Erstellen und Anwenden der Anfangsmomentaufnahme](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit Parametrisierten Filtern](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Aktivieren der Initialisierung mit einer Sicherung für Transaktionsveröffentlichungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/enable-initialization-with-backup-for-transactional-publications.md)  
  
-   [Initialisieren eines Transaktionsabonnements von einer Sicherung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [Manuelles Initialisieren eines Abonnements](../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [Synchronisieren eines Pullabonnements](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [Synchronisieren eines Pushabonnements](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [Erneutes Initialisieren eines Abonnements](../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [Ausführen von Skripts vor und nach dem Anwenden einer Momentaufnahme &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [Ausführen von Skripts während der Synchronisierung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [Anzeigen und Lösen von Datenkonflikten für Mergeveröffentlichungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [Anzeigen von Datenkonflikten für Transaktionsveröffentlichungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [Synchronisieren eines Abonnements mithilfe der Synchronisierungsverwaltung von Windows &#40;Synchronisierungsverwaltung von Windows&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)  
  
-   [Implementieren eines Geschäftslogikhandlers für einen Mergeartikel](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [Debuggen eines Geschäftslogikhandlers &#40;Replikationsprogrammierung&#41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [Kontrollieren des Verhaltens von Triggern und Einschränkungen während der Synchronisierung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [Implementieren eines benutzerdefinierten Konfliktlösers für einen Mergeartikel](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Synchronisieren von Daten](../../relational-databases/replication/synchronize-data.md)  
  
  
