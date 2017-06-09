---
title: Synchronisieren von Daten | Microsoft-Dokumentation
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
- synchronization [SQL Server replication], about synchronization
- merge replication synchronization [SQL Server replication]
- scripts [SQL Server replication], synchronization and
- synchronization [SQL Server replication]
- snapshot replication [SQL Server], synchronization
- transactional replication, synchronization
- subscriptions [SQL Server replication], synchronizing
- on demand script execution
- replication [SQL Server], synchronization
- scripts [SQL Server replication]
ms.assetid: 724802f7-7d69-46d3-a330-bd8aa7f53114
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ccda32ba9e85f698a2a642d2dd52773e78ae6d06
ms.contentlocale: de-de
ms.lasthandoff: 06/05/2017

---
# <a name="synchronize-data"></a>Synchronisieren von Daten
  Das Synchronisieren von Daten bezieht sich auf den Prozess des Weitergebens von Daten- und Schemaänderungen zwischen dem Verleger und Abonnenten, nachdem die Anfangsmomentaufnahme auf dem Abonnenten angewendet wurde. Die Synchronisierung kann auf verschiedene Weise ausgeführt werden:  
  
-   Fortlaufend, was typisch für die Transaktionsreplikation ist.  
  
-   Bedarfsgesteuert, was typisch für die Mergereplikation ist.  
  
-   Nach einem Zeitplan, was typisch für die Momentaufnahmereplikation ist.  
  
 Wenn ein Abonnement synchronisiert wird, werden basierend auf dem verwendeten Replikationstyp verschiedene Prozesse ausgeführt:  
  
-   Momentaufnahmereplikation. Synchronisieren bedeutet, dass der Verteilungs-Agent die Momentaufnahme erneut auf dem Abonnenten anwendet, sodass Schema und Daten in der Abonnementdatenbank mit der Veröffentlichungsdatenbank übereinstimmen.  
  
     Wenn Änderungen an den Daten oder dem Schema auf dem Verleger vorgenommen wurden, muss für die Weitergabe der Änderungen an den Abonnenten eine neue Momentaufnahme generiert werden.  
  
-   Transaktionsreplikation. Synchronisieren bedeutet, dass der Verteilungs-Agent Updates, Einfügungen, Löschungen und andere Änderungen von der Verteilungsdatenbank auf den Abonnenten überträgt.  
  
-   Mergereplikation. Synchronisieren bedeutet, dass der Merge-Agent Änderungen vom Abonnenten auf den Verleger hochlädt und dann die Änderungen vom Verleger auf den Abonnenten herunterlädt. Eventuelle Konflikte werden erkannt und gelöst. Die Daten werden konvergiert, sodass der Verleger und die Abonnenten schließlich die gleichen Datenwerte aufweisen. Wenn Konflikte erkannt und gelöst wurden, bedeutet das, dass Arbeiten, die einige der Benutzer ausgeführt haben, so geändert worden sind, dass der Konflikt entsprechend der von Ihnen definierten Richtlinien gelöst wurde.  
  
 Durch Momentaufnahmeveröffentlichungen wird das Schema auf dem Abonnenten bei jeder Synchronisierung vollständig aktualisiert, sodass alle Schemaänderungen auf den Abonnenten angewendet werden. Auch die Transaktions- und die Mergereplikation unterstützen die häufigsten Schemaänderungen. Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 Informationen zum Synchronisieren eines Pushabonnements finden Sie unter [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
 Informationen zum Synchronisieren eines Pullabonnements finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
 Informationen zum Festlegen von Synchronisierungszeitplänen finden Sie unter [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
 **So zeigen Sie Synchronisierungskonflikte an und lösen Sie die Konflikte**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Anzeigen und Lösen von Datenkonflikten für Mergeveröffentlichungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Anzeigen von Datenkonflikten für Transaktionsveröffentlichungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
## <a name="executing-code-during-synchronization"></a>Ausführen von Code während der Synchronisierung  
 Die Replikation unterstützt zwei Methoden zum Ausführen von Code während der Synchronisierung.  
  
-   Das bedarfsgesteuerte Ausführen von Skripts wird für die Transaktions- und die Mergereplikation unterstützt. Beim bedarfsgesteuerten Ausführen von Skripts können Sie angeben, dass ein SQL-Skript während der Synchronisierung ausgeführt wird. Das Skript wird auf den Abonnenten kopiert und mithilfe von **sqlcmd** am Anfang des Synchronisierungsvorgangs ausgeführt. Das Skript hat keinen Zugriff auf die replizierten Änderungen, wenn diese auf den Abonnenten angewendet werden. Weitere Informationen finden Sie unter [Ausführen von Skripts während der Synchronisierung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   Geschäftslogikhandler werden für die Mergereplikation unterstützt. Das Geschäftslogikhandler-Framework ermöglicht es Ihnen, eine verwaltete Codeassembly zu schreiben, die während der Mergesynchronisierung aufgerufen wird. Die Assembly enthält Geschäftslogik, die auf viele Bedingungen während der Synchronisierung reagieren kann: Datenänderungen, Konflikte und Fehler. Weitere Informationen finden Sie unter [Ausführen von Geschäftslogik während der Mergesynchronisierung](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erkennen und Auflösen von Konflikten bei der Mergereplikation](../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)  
  
  
