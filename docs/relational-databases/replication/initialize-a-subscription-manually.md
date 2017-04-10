---
title: "Manuelles Initialisieren eines Abonnements | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Manuelle Abonnementinitialisierung [SQL Server-Replikation]"
  - "Abonnements [SQL Server-Replikation], initialisieren"
  - "Initialisieren von Abonnements [SQL Server-Replikation], ohne Momentaufnahmen"
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Manuelles Initialisieren eines Abonnements
  In diesem Thema wird beschrieben, wie ein Abonnement manuell in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]initialisiert wird. Obwohl die Anfangsmomentaufnahme normalerweise zum Initialisieren eines Abonnements verwendet wird, können Abonnements für Veröffentlichungen ohne eine Momentaufnahme initialisiert werden. Voraussetzung dafür ist allerdings, dass der Abonnent das Schema und die Ausgangsdaten bereits besitzt.  
  

##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn es zwischen dem Zeitpunkt, zu dem die Daten und das Schema auf den Abonnenten kopiert wurden, und dem Zeitpunkt, zu dem das Abonnement manuell initialisiert wurde, auf einer Datenbank, die mit einer Transaktionsreplikation veröffentlicht wurde, zu einer Aktivität gekommen ist, kann es passieren, dass Änderungen, die sich aus dieser Aktivität ergeben, nicht auf den Abonnenten repliziert werden.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Um ein Abonnement für eine Veröffentlichung manuell zu initialisieren, kopieren Sie das Schema (und in der Regel auch einige Daten) in die Abonnementdatenbank. Das Schema und die Daten sollten mit der Veröffentlichungsdatenbank übereinstimmen. Geben Sie anschließend im Assistenten für neue Abonnements auf der Seite **Abonnements initialisieren** an, dass für das Abonnement kein Schema und keine Daten erforderlich sind. Weitere Informationen zum Aufrufen dieses Assistenten finden Sie unter [eine Transaktionsabonnements ohne Momentaufnahme initialisieren](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) und [Erstellen Sie ein Pullabonnement](../../relational-databases/replication/create-a-pull-subscription.md).  
  
 Beim ersten Synchronisieren des Abonnements werden die für die Replikation erforderlichen Objekte und Metadaten in die Abonnementdatenbank kopiert.  
  
#### So initialisieren Sie ein Abonnement für eine Veröffentlichung manuell  
  
1.  Stellen Sie sicher, dass das Schema und die Daten in die Abonnementdatenbank kopiert wurden.  
  
2.  Deaktivieren Sie im Assistenten für neue Abonnements auf der Seite **Abonnements initialisieren** das Kontrollkästchen **Initialisieren** . Wiederholen Sie diesen Schritt für alle Abonnements, bei denen nur die Replikationsobjekte und -metadaten kopiert werden sollen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Abonnements können manuell mit gespeicherten Replikationsprozeduren initialisiert werden.  
  
#### So wird ein Pullabonnement für eine Transaktionsveröffentlichung manuell initialisiert  
  
1.  Stellen Sie sicher, dass das Schema und die Daten in der Abonnementdatenbank vorhanden sind. Weitere Informationen finden Sie unter [eine Transaktionsabonnements ohne Momentaufnahme initialisieren](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Geben Sie **@publication**, **@subscriber**, den Namen der Datenbank auf dem Abonnenten mit den veröffentlichten Daten für **@destination_db**, den Wert **Pull** für **@subscription_type**, und der Wert **nur replikationsunterstützung** für **@sync_type**. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  Führen Sie auf dem Abonnenten [sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) aus. Aktualisieren von Abonnements finden Sie unter [Erstellen eines aktualisierbaren Abonnements für eine Transaktionsveröffentlichung](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
4.  Führen Sie auf dem Abonnenten [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) aus. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Starten Sie den Verteilungs-Agent, um Replikationsobjekte zu übertragen und die neuesten Änderungen vom Verleger herunterzuladen. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### So wird ein Pushabonnement für eine Transaktionsveröffentlichung manuell initialisiert  
  
1.  Stellen Sie sicher, dass das Schema und die Daten in der Abonnementdatenbank vorhanden sind. Weitere Informationen finden Sie unter [eine Transaktionsabonnements ohne Momentaufnahme initialisieren](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Geben Sie den Namen der Datenbank auf dem Abonnenten mit den veröffentlichten Daten für **@destination_db**, den Wert **Push** für **@subscription_type**, und der Wert **nur replikationsunterstützung** für **@sync_type**. Aktualisieren von Abonnements finden Sie unter [Erstellen eines aktualisierbaren Abonnements für eine Transaktionsveröffentlichung](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank, [Sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Starten Sie den Verteilungs-Agent, um Replikationsobjekte zu übertragen und die neuesten Änderungen vom Verleger herunterzuladen. Weitere Informationen finden Sie unter [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### So wird ein Pullabonnement für eine Mergeveröffentlichung manuell initialisiert  
  
1.  Stellen Sie sicher, dass das Schema und die Daten in der Abonnementdatenbank vorhanden sind. Sie können dazu eine Sicherung der Veröffentlichungsdatenbank auf dem Abonnenten wiederherstellen.  
  
2.  Führen Sie auf dem Verleger [Sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Geben Sie **@publication**, **@subscriber**, **@subscriber_db**, und der Wert **Pull** für **@subscription_type**. Damit wird das Pullabonnement registriert.  
  
3.  Führen Sie auf dem Abonnenten für die Datenbank mit den veröffentlichten Daten, [Sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Geben Sie den Wert **keine** für **@sync_type**.  
  
4.  Führen Sie auf dem Abonnenten [Sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md). Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Starten Sie den Merge-Agent, um Replikationsobjekte zu übertragen und die neuesten Änderungen vom Verleger herunterzuladen. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### So wird ein Pushabonnement für eine Mergeveröffentlichung manuell initialisiert  
  
1.  Stellen Sie sicher, dass das Schema und die Daten in der Abonnementdatenbank vorhanden sind. Sie können dazu eine Sicherung der Veröffentlichungsdatenbank auf dem Abonnenten wiederherstellen.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Geben Sie den Namen der Datenbank auf dem Abonnenten mit den veröffentlichten Daten für **@subscriber_db**, den Wert **Push** für **@subscription_type**, und der Wert **keine** für **@sync_type**.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank, [Sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Starten Sie den Merge-Agent, um Replikationsobjekte zu übertragen und die neuesten Änderungen vom Verleger herunterzuladen. Weitere Informationen finden Sie unter [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## Siehe auch  
 [Initialisieren eines Transaktionsabonnements ohne Momentaufnahme](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)   
 [Sichern und Wiederherstellen von replizierten Datenbanken](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  