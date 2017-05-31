---
title: "Anzeigen und Ändern der Eigenschaften von Pullabonnements | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying subscriptions
- viewing replication properties
- modifying replication properties, pull subscriptions
- pull subscriptions [SQL Server replication], modifying
- subscriptions [SQL Server replication], pull
- pull subscriptions [SQL Server replication], properties
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e62ba6a0d4aebf9cb6c929e5564645e8407da3ee
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="view-and-modify-pull-subscription-properties"></a>Anzeigen und Ändern der Eigenschaften von Pullabonnements
  In diesem Thema wird beschrieben, wie die Eigenschaften von Pullabonnements in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekten (RMO) angezeigt und geändert werden.  
  
 **In diesem Thema**  
  
-   **So können Sie Eigenschaften von Pullabonnements anzeigen und ändern mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Anzeigen der Eigenschaften von Pullabonnements vom Verleger oder Abonnenten aus ist über das Dialogfeld **Abonnementeigenschaften - \<Verleger>:\<Veröffentlichungsdatenbank>** möglich, das in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügbar ist. Weitere Eigenschaften können vom Abonnenten aus angezeigt werden, und das Ändern der Eigenschaften ist auf dem Abonnenten möglich. Das Anzeigen von Eigenschaften ist vom Verleger aus über die Registerkarte **Alle Abonnements** möglich, die im Replikationsmonitor verfügbar ist. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-management-studio"></a>So zeigen Sie Eigenschaften von Pullabonnements vom Verleger aus in Management Studio an  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die entsprechende Veröffentlichung, klicken Sie mit der rechten Maustaste auf ein Abonnement, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Zeigen Sie die Eigenschaften an, und klicken Sie dann auf **OK**.  
  
#### <a name="to-view-and-modify-pull-subscription-properties-from-the-subscriber-in-management-studio"></a>So zeigen Sie Eigenschaften von Pullabonnements vom Abonnent aus in Management Studio an und ändern sie  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Abonnements** .  
  
3.  Klicken Sie mit der rechten Maustaste auf ein Abonnement, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-replication-monitor"></a>So zeigen Sie Eigenschaften von Pullabonnements vom Verleger aus im Replikationsmonitor an  
  
1.  Erweitern Sie im linken Bereich des Replikationsmonitors eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
3.  Klicken Sie mit der rechten Maustaste auf ein Abonnement, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Zeigen Sie die Eigenschaften an, und klicken Sie dann auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Pullabonnements können geändert und auf ihre Eigenschaften kann mithilfe gespeicherter Replikationsprozeduren programmgesteuert zugegriffen werden. Welche gespeicherten Prozeduren verwendet werden, hängt vom Typ der Veröffentlichung ab, zu der das Abonnement gehört.  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>So zeigen Sie die Eigenschaften eines Pullabonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung an  
  
1.  Führen Sie auf dem Abonnenten [sp_helppullsubscription](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)aus. Geben Sie **@publisher**, **@publisher_db**und **@publication**verfügbar ist. Dadurch werden Informationen über das Abonnement zurückgegeben, das in Systemtabellen beim Abonnenten gespeichert ist.  
  
2.  Führen Sie auf dem Abonnenten [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)aus. Geben Sie **@publisher**, **@publisher_db**, **@publication**und einen der folgenden Werte für **@publication_type**an:  
  
    -   **0** &ndash; Das Abonnement gehört zu einer Transaktionsveröffentlichung  
  
    -   **1** &ndash; Das Abonnement gehört zu einer Momentaufnahmeveröffentlichung.  
  
3.  Führen Sie auf dem Verleger [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)aus. Geben Sie **@publication** und **@subscriber**verfügbar ist.  
  
4.  Führen Sie auf dem Verleger [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)aus, und geben Sie **@subscriber**verfügbar ist. Dadurch werden Informationen zu dem Abonnenten angezeigt.  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>So ändern Sie die Eigenschaften eines Pullabonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Abonnenten [sp_change_subscription_properties](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)aus, und geben Sie **@publisher**, **@publisher_db**, **@publication**, den Wert **0** (Transaktionsveröffentlichung) oder **1** (Momentaufnahmeveröffentlichung) für **@publication_type**, die zu ändernde Abonnementeigenschaft für **@property**sowie den neuen Wert der Eigenschaft für **@value**verfügbar ist.  
  
2.  (Optional) Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md)aus. Geben Sie die ID des Verteilungs-Agentauftrags für **@jobid**und die folgenden DTS (Data Transformation Services)-Paketeigenschaften an:  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     Dadurch werden die DTS-Paketeigenschaften eines Abonnements geändert.  
  
    > [!NOTE]  
    >  Die Auftrag-ID erhalten Sie, wenn Sie [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)ausführen.  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>So zeigen Sie die Eigenschaften eines Pullabonnements für eine Mergeveröffentlichung an  
  
1.  Führen Sie auf dem Abonnenten [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)aus. Geben Sie **@publisher**, **@publisher_db**und **@publication**verfügbar ist.  
  
2.  Führen Sie auf dem Abonnenten [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)aus. Geben Sie **@publisher**, **@publisher_db**, **@publication**und den Wert 2 für **@publication_type**verfügbar ist.  
  
3.  Führen Sie auf dem Verleger [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md) aus, um Abonnementinformationen anzuzeigen. Um Informationen zu einem bestimmten Abonnement zu erhalten, müssen Sie **@publication**, **@subscriber**und den Wert **pull** für **@subscription_type**verfügbar ist.  
  
4.  Führen Sie auf dem Verleger [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)aus, und geben Sie **@subscriber**verfügbar ist. Dadurch werden Informationen zu dem Abonnenten angezeigt.  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>So ändern Sie die Eigenschaften eines Pullabonnements für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Abonnenten [sp_changemergepullsubscription](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)aus. Geben Sie **@publication**, **@publisher**, **@publisher_db**, die zu ändernde Abonnementeigenschaft für **@property**sowie den neuen Wert der Eigenschaft für **@value**verfügbar ist.  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Die RMO-Klassen, mit denen Sie die Eigenschaften von Pullabonnements anzeigen oder ändern, hängen vom Typ der Veröffentlichung ab, für die das Pullabonnement erstellt wird.  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>So zeigen Sie die Eigenschaften eines Pullabonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung an oder ändern sie  
  
1.  Stellen Sie eine Verbindung mit dem Abonnenten her, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPullSubscription>-Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, und <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>-Eigenschaften fest.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft fest.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, wurden entweder die Abonnementeigenschaften in Schritt 3 falsch definiert, oder das Abonnement ist auf dem Server nicht vorhanden.  
  
6.  (Optional) Zum Ändern der Eigenschaften legen Sie einen neuen Wert für eine der <xref:Microsoft.SqlServer.Replication.TransPullSubscription>-Eigenschaften fest, die definiert werden können, und rufen Sie dann die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>-Methode auf.  
  
7.  (Optional) Um die neuen Einstellungen anzuzeigen, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A>-Methode auf, um die Eigenschaften für den Artikel erneut zu laden.  
  
8.  Trennen Sie alle Verbindungen.  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-merge-publication"></a>So zeigen Sie die Eigenschaften eines Pullabonnements für eine Mergeveröffentlichung an oder ändern sie  
  
1.  Stellen Sie eine Verbindung mit dem Abonnenten her, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePullSubscription>-Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, und <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>-Eigenschaften fest.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft fest.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, wurden entweder die Abonnementeigenschaften in Schritt 3 falsch definiert, oder das Abonnement ist auf dem Server nicht vorhanden.  
  
6.  (Optional) Zum Ändern der Eigenschaften legen Sie einen neuen Wert für eine der <xref:Microsoft.SqlServer.Replication.MergePullSubscription>-Eigenschaften fest, die definiert werden können, und rufen Sie dann die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>-Methode auf.  
  
7.  (Optional) Um die neuen Einstellungen anzuzeigen, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A>-Methode auf, um die Eigenschaften für den Artikel erneut zu laden.  
  
8.  Trennen Sie alle Verbindungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement &#40;Replikationsmonitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
