---
title: "L&#246;schen eines Pullabonnements | Microsoft Docs"
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
  - "Löschen von Abonnements"
  - "Pullabonnements [SQL Server-Replikation], löschen"
  - "Abonnements [SQL Server-Replikation], Pull"
ms.assetid: 997c0b8e-d8d9-4eed-85b1-6baa1f8594ce
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# L&#246;schen eines Pullabonnements
  In diesem Thema wird beschrieben, wie ein Pullabonnement in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) gelöscht wird.  
  
 **In diesem Thema**  
  
-   **So löschen Sie ein Pullabonnement mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Löschen eines Pullabonnements auf dem Verleger (aus der **lokale Publikationen** im Ordner [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) oder auf dem Abonnenten (aus der **Lokale Abonnements** Ordner). Beim Löschen eines Abonnements werden keine Objekte oder Daten aus dem Abonnement entfernt, diese müssen manuell entfernt werden.  
  
#### So löschen Sie ein Pullabonnement auf dem Verleger  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die Veröffentlichung, der das zu löschende Abonnement zugeordnet ist.  
  
4.  Maustaste auf das Abonnement, und klicken Sie dann auf **Löschen**.  
  
5.  Wählen Sie im Bestätigungsdialogfeld aus, ob zum Löschen der Abonnementinformationen eine Verbindung mit dem Abonnenten hergestellt werden soll. Wenn Sie das Kontrollkästchen **Verbindung mit Abonnenten herstellen** deaktivieren, müssen Sie zum Löschen der Informationen später eine Verbindung mit dem Abonnenten herstellen.  
  
#### So löschen Sie ein Pullabonnement auf dem Abonnenten  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Abonnements** .  
  
3.  Mit der rechten Maustaste des Abonnements zu löschen, und klicken Sie dann auf **Löschen**.  
  
4.  Wählen Sie im Bestätigungsdialogfeld aus, ob zum Löschen der Abonnementinformationen eine Verbindung mit dem Verleger hergestellt werden soll. Wenn Sie das Kontrollkästchen **Verbindung mit Verleger herstellen** deaktivieren, müssen Sie zum Löschen der Informationen später eine Verbindung mit dem Verleger herstellen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Pullabonnements können mithilfe von gespeicherten Replikationsprozeduren programmgesteuert gelöscht werden. Die verwendeten gespeicherten Prozeduren hängen vom Typ der Veröffentlichung ab, zu der das Abonnement gehört.  
  
#### So löschen Sie ein Pullabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_droppullsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md). Geben Sie **@publication**, **@publisher**, und **@publisher_db**.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_dropsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). Geben Sie **@publication** und **@subscriber**an. Geben Sie für **@article** den Wert **all**an. (Optional) Wenn der Verteiler nicht zugegriffen werden kann, geben Sie den Wert **1** für **@ignore_distributor** das Abonnement zu löschen, ohne die damit verbundenen Objekte auf dem Verteiler.  
  
#### So löschen Sie ein Pullabonnement für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_dropmergepullsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md). Geben Sie **@publication**, **@publisher**, und **@publisher_db**.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_dropmergesubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md). Geben Sie **@publication**, **@subscriber**, und **@subscriber_db**. Geben Sie den Wert **Pull** für **@subscription_type**. (Optional) Wenn der Verteiler nicht zugegriffen werden kann, geben Sie den Wert **1** für **@ignore_distributor** das Abonnement zu löschen, ohne die damit verbundenen Objekte auf dem Verteiler.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Im folgenden Beispiel wird ein Pullabonnement für eine Transaktionsveröffentlichung gelöscht. Der erste Batch wird auf dem Abonnenten ausgeführt und der zweite wird auf dem Verleger ausgeführt.  
  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_1.sql)]  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_2.sql)]  
  
 Im folgenden Beispiel wird ein Pullabonnement für eine Mergeveröffentlichung gelöscht. Der erste Batch wird auf dem Abonnenten ausgeführt und der zweite wird auf dem Verleger ausgeführt.  
  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_3.sql)]  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_4.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Pullabonnements mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert löschen. Die RMO-Klassen, mit denen Sie ein Pullabonnement löschen, hängen vom Typ der Veröffentlichung ab, für die das Pullabonnement abonniert wird.  
  
#### So löschen Sie ein Pullabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Erstellen von Verbindungen mit dem Abonnenten und dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPullSubscription> Klasse, und legen die <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, und <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Eigenschaften. Verwenden Sie die Verbindung zum Abonnenten aus Schritt 1 Festlegen der <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
3.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> -Eigenschaft überprüfen, ob das Abonnement vorhanden ist. Wenn der Wert dieser Eigenschaft **false**ist, wurden entweder die Abonnementeigenschaften in Schritt 2 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> Methode.  
  
5.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPublication> Klasse, indem Sie die verlegerverbindung aus Schritt 1. Geben Sie <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> und <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Wenn diese Methode **false**zurückgibt, sind entweder die in Schritt 5 angegebenen Eigenschaften falsch definiert, oder die Veröffentlichung ist auf dem Server nicht vorhanden.  
  
7.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.TransPublication.RemovePullSubscription%2A> Methode. Geben Sie den Namen des Abonnenten und der Abonnementdatenbank für die Parameter *subscriber* und *subscriberDB* an.  
  
#### So löschen Sie ein Pullabonnement für eine Mergeveröffentlichung  
  
1.  Erstellen von Verbindungen mit dem Abonnenten und dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePullSubscription> Klasse, und legen die <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, und <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Eigenschaften. Verwenden Sie die Verbindung aus Schritt 1 Festlegen der <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
3.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> -Eigenschaft überprüfen, ob das Abonnement vorhanden ist. Wenn der Wert dieser Eigenschaft **false**ist, wurden entweder die Abonnementeigenschaften in Schritt 2 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> Methode.  
  
5.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication> Klasse, indem Sie die verlegerverbindung aus Schritt 1. Geben Sie <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> und <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Wenn diese Methode **false**zurückgibt, sind entweder die in Schritt 5 angegebenen Eigenschaften falsch definiert, oder die Veröffentlichung ist auf dem Server nicht vorhanden.  
  
7.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergePublication.RemovePullSubscription%2A> Methode. Geben Sie den Namen des Abonnenten und der Abonnementdatenbank für die Parameter *subscriber* und *subscriberDB* an.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 In diesem Beispiel wird ein Pullabonnement für eine Transaktionsveröffentlichung gelöscht und die Registrierung des Abonnements auf dem Verleger entfernt.  
  
 [!code-csharp[HowTo#rmo_DropTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpullsub)]  
  
 In diesem Beispiel wird ein Pullabonnement für eine Mergeveröffentlichung gelöscht und die Registrierung des Abonnements auf dem Verleger entfernt.  
  
 [!code-csharp[HowTo#rmo_DropMergePullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepullsub)]  
  
## Siehe auch  
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  