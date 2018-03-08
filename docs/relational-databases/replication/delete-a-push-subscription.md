---
title: "Löschen eines Pushabonnements |Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
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
- removing subscriptions
- push subscriptions [SQL Server replication], deleting
- deleting subscriptions
- subscriptions [SQL Server replication], push
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
caps.latest.revision: "35"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b551fe093df2bbb838b63f54a013b670f054eae
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="delete-a-push-subscription"></a>Löschen eines Pushabonnements
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie ein Pushabonnement in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (Replication Management Objects, RMO) gelöscht wird.  
  
 **In diesem Thema**  
  
-   **So löschen Sie ein Pushabonnement mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 Ein Pushabonnement wird beim Verleger (im Ordner **Lokale Veröffentlichungen** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) oder beim Abonnenten (im Ordner **Lokale Abonnements** ) gelöscht. Beim Löschen eines Abonnements werden keine Objekte oder Daten aus dem Abonnement entfernt, diese müssen manuell entfernt werden.  
  
#### <a name="to-delete-a-push-subscription-at-the-publisher"></a>So löschen Sie ein Pushabonnement beim Verleger  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die Veröffentlichung, der das zu löschende Abonnement zugeordnet ist.  
  
4.  Klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Löschen**.  
  
5.  Wählen Sie im Bestätigungsdialogfeld aus, ob zum Löschen der Abonnementinformationen eine Verbindung mit dem Abonnenten hergestellt werden soll. Wenn Sie das Kontrollkästchen **Verbindung mit Abonnenten herstellen** deaktivieren, sollten Sie später eine Verbindung mit dem Abonnenten herstellen, um die Informationen zu löschen.  
  
#### <a name="to-delete-a-push-subscription-at-the-subscriber"></a>So löschen Sie ein Pushabonnement auf dem Abonnenten  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Abonnements** .  
  
3.  Klicken Sie mit der rechten Maustaste auf das Abonnement, das Sie löschen möchten, und klicken Sie dann auf **Löschen**.  
  
4.  Wählen Sie im Bestätigungsdialogfeld aus, ob zum Löschen der Abonnementinformationen eine Verbindung mit dem Verleger hergestellt werden soll. Wenn Sie das Kontrollkästchen **Verbindung mit Verleger herstellen** deaktivieren, müssen Sie zum Löschen der Informationen später eine Verbindung mit dem Verleger herstellen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Pushabonnements können mithilfe von gespeicherten Replikationsprozeduren programmgesteuert gelöscht werden. Welche gespeicherten Prozeduren verwendet werden, hängt vom Typ der Veröffentlichung ab, zu der das Abonnement gehört.  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>So löschen Sie ein Pushabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md) aus. Geben Sie **@publication** und **@subscriber**verfügbar ist. Geben Sie für **@article** den Wert **@article**. (Optional) Wenn auf den Verteiler nicht zugegriffen werden kann, geben Sie den Wert **1** den Wert **@ignore_distributor** an, um das Abonnement ohne die damit verbundenen Objekte auf dem Verteiler zu löschen.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) aus, um Replikationsmetadaten aus der Abonnementdatenbank zu entfernen.  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>So löschen Sie ein Pushabonnement für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md) aus, und geben Sie **@publication**, **@subscriber** und **@subscriber_db** an. (Optional) Wenn auf den Verteiler nicht zugegriffen werden kann, geben Sie den Wert **1** den Wert **@ignore_distributor** an, um das Abonnement ohne die damit verbundenen Objekte auf dem Verteiler zu löschen.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md) aus. Geben Sie **@publisher**, **@publisher_db**und **@publication**verfügbar ist. Damit werden Mergemetadaten aus der Abonnementdatenbank gelöscht.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Im folgenden Beispiel wird ein neues Pushabonnement für eine Transaktionsveröffentlichung gelöscht.  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_1.sql)]  
  
 Im folgenden Beispiel wird ein neues Pushabonnement für eine Mergeveröffentlichung gelöscht.  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Die RMO-Klassen, mit denen Sie ein Pushabonnement löschen, hängen vom Typ der Veröffentlichung ab, für die das Pushabonnement abonniert wird.  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>So löschen Sie ein Pushabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransSubscription> -Klasse.  
  
3.  Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>und <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> fest.  
  
4.  Legen Sie <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft fest.  
  
5.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> -Eigenschaft, um festzustellen, ob das Abonnement vorhanden ist. Wenn der Wert dieser Eigenschaft **false**ist, wurden entweder die Abonnementeigenschaften in Schritt 2 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> -Methode auf.  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>So löschen Sie ein Pushabonnement für eine Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSubscription> -Klasse.  
  
3.  Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>und <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> fest.  
  
4.  Legen Sie <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft fest.  
  
5.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> -Eigenschaft, um festzustellen, ob das Abonnement vorhanden ist. Wenn der Wert dieser Eigenschaft **false**ist, wurden entweder die Abonnementeigenschaften in Schritt 2 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> -Methode auf.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 Sie können Pushabonnements mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert löschen.  
  
 [!code-cs[HowTo#rmo_DropTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
