---
title: "Löschen einer Veröffentlichung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing publications
- publications [SQL Server replication], deleting
- articles [SQL Server replication], deleting
- deleting publications
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ab912d7a972631b6fa63cb9ed9209cb41fd8ac7d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="delete-a-publication"></a>Löschen einer Veröffentlichung
  In diesem Thema wird beschrieben, wie eine Veröffentlichung in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekten (RMO) gelöscht wird.  
  
 **In diesem Thema**  
  
-   **So löschen Sie eine Veröffentlichung mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Verwenden Sie zum Löschen von Veröffentlichungen den Ordner **Lokale Veröffentlichungen** in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-delete-a-publication"></a>So löschen Sie eine Veröffentlichung  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Veröffentlichung, die Sie löschen möchten, und klicken Sie dann auf **Löschen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Veröffentlichungen können programmgesteuert mit gespeicherten Replikationsprozeduren gelöscht werden. Welche gespeicherten Prozeduren Sie verwenden, hängt vom Typ der zu löschenden Veröffentlichung ab.  
  
> [!NOTE]  
>  Durch das Löschen einer Veröffentlichung werden weder die veröffentlichten Objekte aus der Veröffentlichungsdatenbank noch die zugehörigen Objekte aus der Abonnementdatenbank entfernt. Verwenden Sie den `DROP <object>` -Befehl, um diese Objekte bei Bedarf manuell zu entfernen.  
  
#### <a name="to-delete-a-snapshot-or-transactional-publication"></a>So löschen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung.  
  
1.  Führen Sie eines der folgenden Verfahren aus:  
  
    -   Um eine einzelne Veröffentlichung zu löschen, führen Sie [sp_droppublication](../../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus.  
  
    -   Führen Sie [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) auf dem Verleger aus, um alle Veröffentlichungen in und alle Replikationsobjekte aus einer veröffentlichten Datenbank zu entfernen. Geben Sie für **@type** @type **@type**. (Optional) Wenn nicht auf den Verteiler zugegriffen werden kann oder wenn der Status der Datenbank fehlerverdächtig oder offline ist, geben Sie für **@force** @type **@force**. (Optional) Geben Sie für **@dbname** den Namen der Datenbank an, wenn [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) an der Veröffentlichungsdatenbank nicht ausgeführt wird.  
  
        > [!NOTE]  
        >  Bei Angabe des Werts **@force** @type **@force** bleiben möglicherweise replikationsbezogene Veröffentlichungsobjekte in der Datenbank zurück.  
  
2.  (Optional) Wenn diese Datenbank keine anderen Veröffentlichungen besitzt, führen Sie [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) aus, um die Veröffentlichung der aktuellen Datenbank mit der Momentaufnahme- oder der Transaktionsreplikation zu deaktivieren.  
  
3.  (Optional) Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_subscription_cleanup](../../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) aus, um alle verbleibenden Replikationsmetadaten aus der Abonnementdatenbank zu entfernen.  
  
#### <a name="to-delete-a-merge-publication"></a>So löschen Sie eine Mergeveröffentlichung  
  
1.  Führen Sie eines der folgenden Verfahren aus:  
  
    -   Um eine einzelne Veröffentlichung zu löschen, führen Sie [sp_dropmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus.  
  
    -   Führen Sie [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) auf dem Verleger aus, um alle Veröffentlichungen in und alle Replikationsobjekte aus einer veröffentlichten Datenbank zu entfernen. Geben Sie für **@type** @type **@type**. (Optional) Wenn nicht auf den Verteiler zugegriffen werden kann oder wenn der Status der Datenbank fehlerverdächtig oder offline ist, geben Sie für **@force** @type **@force**. (Optional) Geben Sie für **@dbname** den Namen der Datenbank an, wenn [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) an der Veröffentlichungsdatenbank nicht ausgeführt wird.  
  
        > [!NOTE]  
        >  Bei Angabe des Werts **@force** @type **@force** bleiben möglicherweise replikationsbezogene Veröffentlichungsobjekte in der Datenbank zurück.  
  
2.  (Optional) Wenn diese Datenbank keine anderen Veröffentlichungen besitzt, führen Sie [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) aus, um die Veröffentlichung der aktuellen Datenbank mit der Mergereplikation zu deaktivieren.  
  
3.  (Optional) Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md) aus, um alle verbleibenden Replikationsmetadaten aus der Abonnementdatenbank zu entfernen.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Dieses Beispiel zeigt, wie eine Transaktionsveröffentlichung entfernt und die Transaktionsveröffentlichung für eine Datenbank deaktiviert wird. In diesem Beispiel wird davon ausgegangen, dass alle Abonnements vorher entfernt wurden. Weitere Informationen finden Sie unter [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) oder [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md).  
  
 [!code-sql[HowTo#sp_droppublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_1.sql)]  
  
 Dieses Beispiel zeigt, wie eine Mergeveröffentlichung entfernt und die Mergeveröffentlichung für eine Datenbank deaktiviert wird. In diesem Beispiel wird davon ausgegangen, dass alle Abonnements vorher entfernt wurden. Weitere Informationen finden Sie unter [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) oder [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md).  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Veröffentlichungen mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert löschen. Welche RMO-Klassen Sie zum Entfernen von Veröffentlichungen verwenden, hängt vom Typ der zu entfernenden Veröffentlichung ab.  
  
#### <a name="to-remove-a-snapshot-or-transactional-publication"></a>So entfernen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPublication> -Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> -Eigenschaft und die <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> -Eigenschaft für die Veröffentlichung fest, und legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die in Schritt 1 erstellte Verbindung fest.  
  
4.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> -Eigenschaft, um festzustellen, ob die Veröffentlichung vorhanden ist. Wenn der Wert dieser Eigenschaft **false**lautet, wurden entweder die Veröffentlichungseigenschaften in Schritt 3 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> -Methode auf.  
  
6.  (Optional) Wenn für diese Datenbank keine anderen Transaktionsveröffentlichungen vorhanden sind, kann die Datenbank wie folgt für Transaktionsveröffentlichungen deaktiviert werden:  
  
    1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> -Klasse. Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die Instanz von <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 fest.  
  
    2.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf. Wenn diese Methode **false**zurückgibt, überzeugen Sie sich davon, dass die Datenbank vorhanden ist.  
  
    3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> -Eigenschaft auf **false**.  
  
    4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> -Methode auf.  
  
7.  Trennen Sie die Verbindung.  
  
#### <a name="to-remove-a-merge-publication"></a>So entfernen Sie eine Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication> -Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> -Eigenschaft und die <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> -Eigenschaft für die Veröffentlichung fest, und legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die in Schritt 1 erstellte Verbindung fest.  
  
4.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> -Eigenschaft, um festzustellen, ob die Veröffentlichung vorhanden ist. Wenn der Wert dieser Eigenschaft **false**lautet, wurden entweder die Veröffentlichungseigenschaften in Schritt 3 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> -Methode auf.  
  
6.  (Optional) Wenn für diese Datenbank keine anderen Mergeveröffentlichungen vorhanden sind, kann die Datenbank wie folgt für Mergeveröffentlichungen deaktiviert werden:  
  
    1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> -Klasse. Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die Instanz von <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 fest.  
  
    2.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf. Wenn diese Methode **false**zurückgibt, überzeugen Sie sich davon, dass die Datenbank vorhanden ist.  
  
    3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> -Eigenschaft auf **false**.  
  
    4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> -Methode auf.  
  
7.  Trennen Sie die Verbindung.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 Im folgenden Beispiel wird eine Transaktionsveröffentlichung gelöscht. Wenn für diese Datenbank keine anderen Transaktionsveröffentlichungen vorhanden sind, werden Transaktionsveröffentlichungen zudem deaktiviert.  
  
 [!code-cs[HowTo#rmo_DropTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 Im folgenden Beispiel wird eine Mergeveröffentlichung gelöscht. Wenn für diese Datenbank keine anderen Mergeveröffentlichungen vorhanden sind, werden Mergeveröffentlichungen zudem deaktiviert.  
  
 [!code-cs[HowTo#rmo_DropMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## <a name="see-also"></a>Siehe auch  
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
