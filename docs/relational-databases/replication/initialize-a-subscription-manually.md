---
title: Manuelles Initialisieren eines Abonnements | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/25/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 56c0ac907724c7bf587476099a31548dc4a64e6a
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="initialize-a-subscription-manually"></a>Manuelles Initialisieren eines Abonnements
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie ein Abonnement manuell in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]initialisiert wird. Obwohl die Anfangsmomentaufnahme normalerweise zum Initialisieren eines Abonnements verwendet wird, können Abonnements für Veröffentlichungen ohne eine Momentaufnahme initialisiert werden. Voraussetzung dafür ist allerdings, dass der Abonnent das Schema und die Ausgangsdaten bereits besitzt.  
  

##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn es zwischen dem Zeitpunkt, zu dem die Daten und das Schema auf den Abonnenten kopiert wurden, und dem Zeitpunkt, zu dem das Abonnement manuell initialisiert wurde, auf einer Datenbank, die mit einer Transaktionsreplikation veröffentlicht wurde, zu einer Aktivität gekommen ist, kann es passieren, dass Änderungen, die sich aus dieser Aktivität ergeben, nicht auf den Abonnenten repliziert werden.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 Um ein Abonnement für eine Veröffentlichung manuell zu initialisieren, kopieren Sie das Schema (und in der Regel auch einige Daten) in die Abonnementdatenbank. Das Schema und die Daten sollten mit der Veröffentlichungsdatenbank übereinstimmen. Geben Sie anschließend im Assistenten für neue Abonnements auf der Seite **Abonnements initialisieren** an, dass für das Abonnement kein Schema und keine Daten erforderlich sind. Weitere Informationen zum Zugreifen auf diesen Assistenten finden Sie unter [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) und [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)initialisiert wird.  
  
 Beim ersten Synchronisieren des Abonnements werden die für die Replikation erforderlichen Objekte und Metadaten in die Abonnementdatenbank kopiert.  
  
#### <a name="to-initialize-a-subscription-to-a-publication-manually"></a>So initialisieren Sie ein Abonnement für eine Veröffentlichung manuell  
  
1.  Stellen Sie sicher, dass das Schema und die Daten in die Abonnementdatenbank kopiert wurden.  
  
2.  Deaktivieren Sie im Assistenten für neue Abonnements auf der Seite **Abonnements initialisieren** das Kontrollkästchen **Initialisieren** . Wiederholen Sie diesen Schritt für alle Abonnements, bei denen nur die Replikationsobjekte und -metadaten kopiert werden sollen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Abonnements können manuell mit gespeicherten Replikationsprozeduren initialisiert werden.  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-transactional-publication"></a>So wird ein Pullabonnement für eine Transaktionsveröffentlichung manuell initialisiert  
  
1.  Stellen Sie sicher, dass das Schema und die Daten in der Abonnementdatenbank vorhanden sind. Weitere Informationen finden Sie unter [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)initialisiert wird.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)aus. Geben Sie **@publication**, **@subscriber**, den Namen der Datenbank auf dem Abonnenten mit den veröffentlichten Daten für **@destination_db**, den Wert **pull** für **@subscription_type**und den Wert **replication support only** für **@sync_type**initialisiert wird. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  Führen Sie auf dem Abonnenten [sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)aus. Informationen zum Aktualisieren von Abonnements finden Sie unter [Create an Updatable Subscription to a Transactional Publication](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
4.  Führen Sie auf dem Abonnenten [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)aus. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Starten Sie den Verteilungs-Agent, um Replikationsobjekte zu übertragen und die neuesten Änderungen vom Verleger herunterzuladen. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-transactional-publication"></a>So wird ein Pushabonnement für eine Transaktionsveröffentlichung manuell initialisiert  
  
1.  Stellen Sie sicher, dass das Schema und die Daten in der Abonnementdatenbank vorhanden sind. Weitere Informationen finden Sie unter [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)initialisiert wird.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)aus. Geben Sie den Namen der Datenbank auf dem Abonnenten mit den veröffentlichten Daten für **@destination_db**, den Wert **push** für **@subscription_type**und den Wert **replication support only** für **@sync_type**initialisiert wird. Informationen zum Aktualisieren von Abonnements finden Sie unter [Create an Updatable Subscription to a Transactional Publication](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)aus. Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Starten Sie den Verteilungs-Agent, um Replikationsobjekte zu übertragen und die neuesten Änderungen vom Verleger herunterzuladen. Weitere Informationen finden Sie unter [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-merge-publication"></a>So wird ein Pullabonnement für eine Mergeveröffentlichung manuell initialisiert  
  
1.  Stellen Sie sicher, dass das Schema und die Daten in der Abonnementdatenbank vorhanden sind. Sie können dazu eine Sicherung der Veröffentlichungsdatenbank auf dem Abonnenten wiederherstellen.  
  
2.  Führen Sie auf dem Verleger [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)aus. Geben Sie **@publication**, **@subscriber**, **@subscriber_db**und den Wert **pull** für **@subscription_type**initialisiert wird. Damit wird das Pullabonnement registriert.  
  
3.  Führen Sie auf dem Abonnenten für die Datenbank, die die veröffentlichten Daten enthält, [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)aus. Geben Sie für **@sync_type** für **@sync_type**initialisiert wird.  
  
4.  Führen Sie auf dem Abonnenten [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)aus. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Starten Sie den Merge-Agent, um Replikationsobjekte zu übertragen und die neuesten Änderungen vom Verleger herunterzuladen. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-merge-publication"></a>So wird ein Pushabonnement für eine Mergeveröffentlichung manuell initialisiert  
  
1.  Stellen Sie sicher, dass das Schema und die Daten in der Abonnementdatenbank vorhanden sind. Sie können dazu eine Sicherung der Veröffentlichungsdatenbank auf dem Abonnenten wiederherstellen.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)aus. Geben Sie den Namen der Datenbank auf dem Abonnenten mit den veröffentlichten Daten für **@subscriber_db**, den Wert **push** für **@subscription_type**und den Wert **@sync_type** für **@sync_type**initialisiert wird.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)aus. Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Starten Sie den Merge-Agent, um Replikationsobjekte zu übertragen und die neuesten Änderungen vom Verleger herunterzuladen. Weitere Informationen finden Sie unter [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)   
 [Sichern und Wiederherstellen von replizierten Datenbanken](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
