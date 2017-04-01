---
title: "L&#246;schen einer Ver&#246;ffentlichung | Microsoft Docs"
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
  - "Entfernen von Veröffentlichungen"
  - "Veröffentlichungen [SQL Server-Replikation], löschen"
  - "Artikel [SQL Server-Replikation], löschen"
  - "Löschen von Veröffentlichungen"
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# L&#246;schen einer Ver&#246;ffentlichung
  In diesem Thema wird beschrieben, wie eine Veröffentlichung in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) gelöscht wird.  
  
 **In diesem Thema**  
  
-   **So löschen Sie eine Veröffentlichung mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Verwenden Sie zum Löschen von Veröffentlichungen den Ordner **Lokale Veröffentlichungen** in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
#### So löschen Sie eine Veröffentlichung  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Mit der rechten Maustaste in der Publikation zu löschen, und klicken Sie dann auf **Löschen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Veröffentlichungen können programmgesteuert mit gespeicherten Replikationsprozeduren gelöscht werden. Welche gespeicherten Prozeduren Sie verwenden, hängt vom Typ der zu löschenden Veröffentlichung ab.  
  
> [!NOTE]  
>  Durch das Löschen einer Veröffentlichung werden weder die veröffentlichten Objekte aus der Veröffentlichungsdatenbank noch die zugehörigen Objekte aus der Abonnementdatenbank entfernt. Verwenden Sie den `DROP <object>` -Befehl, um diese Objekte bei Bedarf manuell zu entfernen.  
  
#### So löschen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung.  
  
1.  Führen Sie eines der folgenden Verfahren aus:  
  
    -   Führen Sie zum Löschen einer Veröffentlichung [Sp_droppublication](../../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank.  
  
    -   Um alle Veröffentlichungen in und alle Replikationsobjekte aus einer veröffentlichten Datenbank zu entfernen, führen Sie [Sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) auf dem Verleger. Geben Sie für **@type** den Wert **tran**an. (Optional) Wenn der Verteiler nicht zugegriffen werden kann oder wenn der Status der Datenbank fehlerverdächtig oder offline ist, geben Sie den Wert **1** für **@force**. (Optional) Geben Sie den Namen der Datenbank für **@dbname** Wenn [Sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) für die Veröffentlichungsdatenbank nicht ausgeführt wird.  
  
        > [!NOTE]  
        >  Bei Angabe des Werts **1** für **@force** replikationsbezogene veröffentlichungsobjekte in der Datenbank lassen.  
  
2.  (Optional) Wenn diese Datenbank keine anderen Veröffentlichungen verfügt, führen Sie [Sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) So deaktivieren Sie die Veröffentlichung der aktuellen Datenbank mit der Snapshot- oder Transaktionsreplikation.  
  
3.  (Optional) Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_subscription_cleanup](../../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) alle verbleibenden Replikationsmetadaten aus der Abonnementdatenbank zu entfernen.  
  
#### So löschen Sie eine Mergeveröffentlichung  
  
1.  Führen Sie eines der folgenden Verfahren aus:  
  
    -   Führen Sie zum Löschen einer Veröffentlichung [Sp_dropmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank.  
  
    -   Um alle Veröffentlichungen in und alle Replikationsobjekte aus einer veröffentlichten Datenbank zu entfernen, führen Sie [Sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) auf dem Verleger. Geben Sie für **@type** den Wert **merge**an. (Optional) Wenn der Verteiler nicht zugegriffen werden kann oder wenn der Status der Datenbank fehlerverdächtig oder offline ist, geben Sie den Wert **1** für **@force**. (Optional) Geben Sie den Namen der Datenbank für **@dbname** Wenn [Sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) für die Veröffentlichungsdatenbank nicht ausgeführt wird.  
  
        > [!NOTE]  
        >  Bei Angabe des Werts **1** für **@force** replikationsbezogene veröffentlichungsobjekte in der Datenbank lassen.  
  
2.  (Optional) Wenn diese Datenbank keine anderen Veröffentlichungen verfügt, führen Sie [Sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) Deaktivieren der Veröffentlichung der aktuellen Datenbank mithilfe der Mergereplikation.  
  
3.  (Optional) Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_mergesubscription_cleanup & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md) So entfernen Sie alle verbleibenden Replikationsmetadaten in der Abonnementdatenbank.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Dieses Beispiel zeigt, wie eine Transaktionsveröffentlichung entfernt und die Transaktionsveröffentlichung für eine Datenbank deaktiviert wird. In diesem Beispiel wird davon ausgegangen, dass alle Abonnements vorher entfernt wurden. Weitere Informationen finden Sie unter [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) oder [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md).  
  
 [!code-sql[HowTo#sp_droppublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_1.sql)]  
  
 Dieses Beispiel zeigt, wie eine Mergeveröffentlichung entfernt und die Mergeveröffentlichung für eine Datenbank deaktiviert wird. In diesem Beispiel wird davon ausgegangen, dass alle Abonnements vorher entfernt wurden. Weitere Informationen finden Sie unter [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) oder [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md).  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Veröffentlichungen mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert löschen. Welche RMO-Klassen Sie zum Entfernen von Veröffentlichungen verwenden, hängt vom Typ der zu entfernenden Veröffentlichung ab.  
  
#### So entfernen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPublication> Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> und <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Eigenschaften für die Veröffentlichung, und legen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die in Schritt 1 erstellte Verbindung.  
  
4.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> Eigenschaft, um sicherzustellen, dass die Publikation vorhanden ist. Wenn der Wert dieser Eigenschaft **false**lautet, wurden entweder die Veröffentlichungseigenschaften in Schritt 3 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> Methode.  
  
6.  (Optional) Wenn für diese Datenbank keine anderen Transaktionsveröffentlichungen vorhanden sind, kann die Datenbank wie folgt für Transaktionsveröffentlichungen deaktiviert werden:  
  
    1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> Klasse. Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft, um die Instanz von <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1.  
  
    2.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Wenn diese Methode **false**zurückgibt, überzeugen Sie sich davon, dass die Datenbank vorhanden ist.  
  
    3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> -Eigenschaft **false**.  
  
    4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode.  
  
7.  Trennen Sie die Verbindung.  
  
#### So entfernen Sie eine Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication> Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> und <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Eigenschaften für die Veröffentlichung, und legen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die in Schritt 1 erstellte Verbindung.  
  
4.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> Eigenschaft, um sicherzustellen, dass die Publikation vorhanden ist. Wenn der Wert dieser Eigenschaft **false**lautet, wurden entweder die Veröffentlichungseigenschaften in Schritt 3 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> Methode.  
  
6.  (Optional) Wenn für diese Datenbank keine anderen Mergeveröffentlichungen vorhanden sind, kann die Datenbank wie folgt für Mergeveröffentlichungen deaktiviert werden:  
  
    1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> Klasse. Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft, um die Instanz von <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1.  
  
    2.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Wenn diese Methode **false**zurückgibt, überzeugen Sie sich davon, dass die Datenbank vorhanden ist.  
  
    3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> -Eigenschaft **false**.  
  
    4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode.  
  
7.  Trennen Sie die Verbindung.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 Im folgenden Beispiel wird eine Transaktionsveröffentlichung gelöscht. Wenn für diese Datenbank keine anderen Transaktionsveröffentlichungen vorhanden sind, werden Transaktionsveröffentlichungen zudem deaktiviert.  
  
 [!code-csharp[HowTo#rmo_DropTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 Im folgenden Beispiel wird eine Mergeveröffentlichung gelöscht. Wenn für diese Datenbank keine anderen Mergeveröffentlichungen vorhanden sind, werden Mergeveröffentlichungen zudem deaktiviert.  
  
 [!code-csharp[HowTo#rmo_DropMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## Siehe auch  
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  