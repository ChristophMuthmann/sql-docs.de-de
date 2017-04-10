---
title: "L&#246;schen eines Pushabonnements | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Entfernen von Abonnements"
  - "Pushabonnements [SQL Server-Replikation], löschen"
  - "Löschen von Abonnements"
  - "Abonnements [SQL Server-Replikation], Push"
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# L&#246;schen eines Pushabonnements
  In diesem Thema wird beschrieben, wie ein Pushabonnement in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) gelöscht wird.  
  
 **In diesem Thema**  
  
-   **So löschen Sie ein Pushabonnement mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Löschen eines Pushabonnements auf dem Verleger (aus der **lokale Publikationen** im Ordner [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) oder auf dem Abonnenten (aus der **Lokale Abonnements** Ordner). Beim Löschen eines Abonnements werden keine Objekte oder Daten aus dem Abonnement entfernt, diese müssen manuell entfernt werden.  
  
#### So löschen Sie ein Pushabonnement beim Verleger  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die Veröffentlichung, der das zu löschende Abonnement zugeordnet ist.  
  
4.  Maustaste auf das Abonnement, und klicken Sie dann auf **Löschen**.  
  
5.  Wählen Sie im Bestätigungsdialogfeld aus, ob zum Löschen der Abonnementinformationen eine Verbindung mit dem Abonnenten hergestellt werden soll. Wenn Sie das Kontrollkästchen **Verbindung mit Abonnenten herstellen** deaktivieren, sollten Sie später eine Verbindung mit dem Abonnenten herstellen, um die Informationen zu löschen.  
  
#### So löschen Sie ein Pushabonnement auf dem Abonnenten  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Abonnements** .  
  
3.  Mit der rechten Maustaste des Abonnements zu löschen, und klicken Sie dann auf **Löschen**.  
  
4.  Wählen Sie im Bestätigungsdialogfeld aus, ob zum Löschen der Abonnementinformationen eine Verbindung mit dem Verleger hergestellt werden soll. Wenn Sie das Kontrollkästchen **Verbindung mit Verleger herstellen** deaktivieren, müssen Sie zum Löschen der Informationen später eine Verbindung mit dem Verleger herstellen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Pushabonnements können mithilfe von gespeicherten Replikationsprozeduren programmgesteuert gelöscht werden. Welche gespeicherten Prozeduren verwendet werden, hängt vom Typ der Veröffentlichung ab, zu der das Abonnement gehört.  
  
#### So löschen Sie ein Pushabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_dropsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). Geben Sie **@publication** und **@subscriber**an. Geben Sie für **@article** den Wert **all**an. (Optional) Wenn der Verteiler nicht zugegriffen werden kann, geben Sie den Wert **1** für **@ignore_distributor** das Abonnement zu löschen, ohne die damit verbundenen Objekte auf dem Verteiler.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_subscription_cleanup & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) Metadaten in der Abonnementdatenbank zu entfernen.  
  
#### So löschen Sie ein Pushabonnement für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger [Sp_dropmergesubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md), wobei **@publication**, **@subscriber** und **@subscriber_db**. (Optional) Wenn der Verteiler nicht zugegriffen werden kann, geben Sie den Wert **1** für **@ignore_distributor** das Abonnement zu löschen, ohne die damit verbundenen Objekte auf dem Verteiler.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_mergesubscription_cleanup & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md). Geben Sie **@publisher**, **@publisher_db**, und **@publication**. Damit werden Mergemetadaten aus der Abonnementdatenbank gelöscht.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Im folgenden Beispiel wird ein neues Pushabonnement für eine Transaktionsveröffentlichung gelöscht.  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_1.sql)]  
  
 Im folgenden Beispiel wird ein neues Pushabonnement für eine Mergeveröffentlichung gelöscht.  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Die RMO-Klassen, mit denen Sie ein Pushabonnement löschen, hängen vom Typ der Veröffentlichung ab, für die das Pushabonnement abonniert wird.  
  
#### So löschen Sie ein Pushabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransSubscription> Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, und <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> Eigenschaften.  
  
4.  Legen Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
5.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> -Eigenschaft überprüfen, ob das Abonnement vorhanden ist. Wenn der Wert dieser Eigenschaft **false**ist, wurden entweder die Abonnementeigenschaften in Schritt 2 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> Methode.  
  
#### So löschen Sie ein Pushabonnement für eine Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSubscription> Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, und <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> Eigenschaften.  
  
4.  Legen Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
5.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> -Eigenschaft überprüfen, ob das Abonnement vorhanden ist. Wenn der Wert dieser Eigenschaft **false**ist, wurden entweder die Abonnementeigenschaften in Schritt 2 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> Methode.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 Sie können Pushabonnements mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert löschen.  
  
 [!code-csharp[HowTo#rmo_DropTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## Siehe auch  
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  