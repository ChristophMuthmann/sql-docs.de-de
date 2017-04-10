---
title: "Synchronisieren von Daten | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Synchronisierung [SQL Server-Replikation], Informationen zur Synchronisierung"
  - "Mergereplikationssynchronisierung [SQL Server-Replikation]"
  - "Skripts [SQL Server-Replikation], Synchronisierung und"
  - "Synchronisierung [SQL Server-Replikation]"
  - "Momentaufnahmereplikation [SQL Server], Synchronisierung"
  - "Transaktionsreplikation, Synchronisierung"
  - "Abonnements [SQL Server-Replikation], synchronisieren"
  - "Skriptausführung bei Bedarf"
  - "Replikation [SQL Server], Synchronisierung"
  - "Skripts [SQL Server-Replikation]"
ms.assetid: 724802f7-7d69-46d3-a330-bd8aa7f53114
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Synchronisieren von Daten
  Das Synchronisieren von Daten bezieht sich auf den Prozess des Weitergebens von Daten- und Schemaänderungen zwischen dem Verleger und Abonnenten, nachdem die Anfangsmomentaufnahme auf dem Abonnenten angewendet wurde. Die Synchronisierung kann auf verschiedene Weise ausgeführt werden:  
  
-   Fortlaufend, was typisch für die Transaktionsreplikation ist.  
  
-   Bedarfsgesteuert, was typisch für die Mergereplikation ist.  
  
-   Nach einem Zeitplan, was typisch für die Momentaufnahmereplikation ist.  
  
 Wenn ein Abonnement synchronisiert wird, werden basierend auf dem verwendeten Replikationstyp verschiedene Prozesse ausgeführt:  
  
-   Momentaufnahmereplikation. Synchronisieren bedeutet, dass der Verteilungs-Agent die Momentaufnahme erneut auf dem Abonnenten anwendet, sodass Schema und Daten in der Abonnementdatenbank mit der Veröffentlichungsdatenbank übereinstimmen.  
  
     Wenn Änderungen an den Daten oder dem Schema auf dem Verleger vorgenommen wurden, muss für die Weitergabe der Änderungen an den Abonnenten eine neue Momentaufnahme generiert werden.  
  
-   Transaktionsreplikation. Synchronisieren bedeutet, dass der Verteilungs-Agent Updates, Einfügungen, Löschungen und andere Änderungen von der Verteilungsdatenbank auf den Abonnenten überträgt.  
  
-   Mergereplikation. Synchronisieren bedeutet, dass der Merge-Agent Änderungen vom Abonnenten auf den Verleger hochlädt und dann die Änderungen vom Verleger auf den Abonnenten herunterlädt. Eventuelle Konflikte werden erkannt und gelöst. Die Daten werden konvergiert, sodass der Verleger und die Abonnenten schließlich die gleichen Datenwerte aufweisen. Wenn Konflikte erkannt und gelöst wurden, bedeutet das, dass Arbeiten, die einige der Benutzer ausgeführt haben, so geändert worden sind, dass der Konflikt entsprechend der von Ihnen definierten Richtlinien gelöst wurde.  
  
 Durch Momentaufnahmeveröffentlichungen wird das Schema auf dem Abonnenten bei jeder Synchronisierung vollständig aktualisiert, sodass alle Schemaänderungen auf den Abonnenten angewendet werden. Auch die Transaktions- und die Mergereplikation unterstützen die häufigsten Schemaänderungen. Weitere Informationen finden Sie unter [vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 Informationen zum Synchronisieren eines Pushabonnements finden Sie unter [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
 Informationen zum Synchronisieren eines Pullabonnements finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
 Informationen zum Festlegen von Synchronisierungszeitplänen finden Sie unter [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
 **So zeigen Sie Synchronisierungskonflikte an und lösen Sie die Konflikte**  
  
-   [! INCLUDE [SsManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [View and Resolve Data Conflicts for Merge Publications &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view and resolve data conflicts for merge publications.md)  
  
-   [! INCLUDE [SsManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [View Data Conflicts for Transactional Publications &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
## Ausführen von Code während der Synchronisierung  
 Die Replikation unterstützt zwei Methoden zum Ausführen von Code während der Synchronisierung.  
  
-   Das bedarfsgesteuerte Ausführen von Skripts wird für die Transaktions- und die Mergereplikation unterstützt. Beim bedarfsgesteuerten Ausführen von Skripts können Sie angeben, dass ein SQL-Skript während der Synchronisierung ausgeführt wird. Das Skript wird auf den Abonnenten kopiert und mithilfe von **sqlcmd** am Anfang des Synchronisierungsvorgangs ausgeführt. Das Skript hat keinen Zugriff auf die replizierten Änderungen, wenn diese auf den Abonnenten angewendet werden. Weitere Informationen finden Sie unter [Ausführen von Skripts während der Synchronisierung & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   Geschäftslogikhandler werden für die Mergereplikation unterstützt. Das Geschäftslogikhandler-Framework ermöglicht es Ihnen, eine verwaltete Codeassembly zu schreiben, die während der Mergesynchronisierung aufgerufen wird. Die Assembly enthält Geschäftslogik, die auf viele Bedingungen während der Synchronisierung reagieren kann: Datenänderungen, Konflikte und Fehler. Weitere Informationen finden Sie unter [führen Business Logic During Merge Synchronization](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
## Siehe auch  
 [Erkennen und Beseitigen von Konflikten bei der Mergereplikation](../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md)  
  
  