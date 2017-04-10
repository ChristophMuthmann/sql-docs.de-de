---
title: "Anzeigen und &#196;ndern der Eigenschaften von Pullabonnements | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Ändern von Abonnements"
  - "Anzeigen von Replikationseigenschaften"
  - "Ändern von Replikationseigenschaften, Pullabonnements"
  - "Pullabonnements [SQL Server-Replikation], ändern"
  - "Abonnements [SQL Server-Replikation], Pull"
  - "Pullabonnements [SQL Server-Replikation], Eigenschaften"
  - "Ändern von Abonnements, SQL Server Management Studio"
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Anzeigen und &#196;ndern der Eigenschaften von Pullabonnements
  In diesem Thema wird beschrieben, wie die Eigenschaften von Pullabonnements in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) angezeigt und geändert werden.  
  
 **In diesem Thema**  
  
-   **So können Sie Eigenschaften von Pullabonnements anzeigen und ändern mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Anzeigen der Eigenschaften von Pullabonnements vom Verleger oder Abonnenten in der **Abonnementeigenschaften - \< Publisher>: \< PublicationDatabase>** Dialogfeld aus [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Weitere Eigenschaften können vom Abonnenten aus angezeigt werden, und das Ändern der Eigenschaften ist auf dem Abonnenten möglich. Das Anzeigen von Eigenschaften ist vom Verleger aus über die Registerkarte **Alle Abonnements** möglich, die im Replikationsmonitor verfügbar ist. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### So zeigen Sie Eigenschaften von Pullabonnements vom Verleger aus in Management Studio an  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die entsprechende Veröffentlichung, mit der rechten Maustaste ein Abonnement, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Zeigen Sie die Eigenschaften an, und klicken Sie dann auf **OK**.  
  
#### So zeigen Sie Eigenschaften von Pullabonnements vom Abonnent aus in Management Studio an und ändern sie  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Abonnements** .  
  
3.  Mit der rechten Maustaste ein Abonnement, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
#### So zeigen Sie Eigenschaften von Pullabonnements vom Verleger aus im Replikationsmonitor an  
  
1.  Erweitern Sie im linken Bereich des Replikationsmonitors eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
3.  Mit der rechten Maustaste ein Abonnement, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Zeigen Sie die Eigenschaften an, und klicken Sie dann auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Pullabonnements können geändert und auf ihre Eigenschaften kann mithilfe gespeicherter Replikationsprozeduren programmgesteuert zugegriffen werden. Welche gespeicherten Prozeduren verwendet werden, hängt vom Typ der Veröffentlichung ab, zu der das Abonnement gehört.  
  
#### So zeigen Sie die Eigenschaften eines Pullabonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung an  
  
1.  Führen Sie auf dem Abonnenten [Sp_helppullsubscription](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md). Geben Sie **@publisher**, **@publisher_db**, und **@publication**. Dadurch werden Informationen über das Abonnement zurückgegeben, das in Systemtabellen beim Abonnenten gespeichert ist.  
  
2.  Führen Sie auf dem Abonnenten [Sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md). Geben Sie **@publisher**, **@publisher_db**, **@publication**, und einen der folgenden Werte für **@publication_type**:  
  
    -   **0** -Abonnement gehört zu einer Transaktionspublikation.  
  
    -   **1** -Abonnement gehört zu einer momentaufnahmeveröffentlichung.  
  
3.  Führen Sie auf dem Verleger [Sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md). Geben Sie **@publication** und **@subscriber**an.  
  
4.  Führen Sie auf dem Verleger [Sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), wobei **@subscriber**. Dadurch werden Informationen zu dem Abonnenten angezeigt.  
  
#### So ändern Sie die Eigenschaften eines Pullabonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Abonnenten [Sp_change_subscription_properties](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), wobei **@publisher**, **@publisher_db**, **@publication**, entweder den Wert **0** (Transaktionsreplikation) oder **1** (Snapshot) für **@publication_type**, die Abonnementeigenschaft als **@property**, und den neuen Wert als **@value**.  
  
2.  (Optional) Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md). Geben Sie die ID des Verteilungs-Agent-Auftrags, für **@jobid**, und die folgenden Data Transformation Services (DTS) Paketeigenschaften:  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     Dadurch werden die DTS-Paketeigenschaften eines Abonnements geändert.  
  
    > [!NOTE]  
    >  Auftrags-ID abgerufen werden kann, durch Ausführen von [Sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md).  
  
#### So zeigen Sie die Eigenschaften eines Pullabonnements für eine Mergeveröffentlichung an  
  
1.  Führen Sie auf dem Abonnenten [Sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md). Geben Sie **@publisher**, **@publisher_db**, und **@publication**.  
  
2.  Führen Sie auf dem Abonnenten [Sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md). Geben Sie **@publisher**, **@publisher_db**, **@publication**, und der Wert 2 für **@publication_type**.  
  
3.  Führen Sie auf dem Verleger [Sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md) um Abonnementinformationen anzuzeigen. Um Informationen zu einem bestimmten Abonnement zurückzugeben, geben Sie **@publication**, **@subscriber**, und der Wert **Pull** für **@subscription_type**.  
  
4.  Führen Sie auf dem Verleger [Sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), wobei **@subscriber**. Dadurch werden Informationen zu dem Abonnenten angezeigt.  
  
#### So ändern Sie die Eigenschaften eines Pullabonnements für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Abonnenten [Sp_changemergepullsubscription](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md). Geben Sie **@publication**, **@publisher**, **@publisher_db**, die Abonnementeigenschaft als **@property**, und der neue Wert als **@value**.  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Die RMO-Klassen, mit denen Sie die Eigenschaften von Pullabonnements anzeigen oder ändern, hängen vom Typ der Veröffentlichung ab, für die das Pullabonnement erstellt wird.  
  
#### So zeigen Sie die Eigenschaften eines Pullabonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung an oder ändern sie  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPullSubscription> Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, und <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Eigenschaften.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, wurden entweder die Abonnementeigenschaften in Schritt 3 falsch definiert, oder das Abonnement ist auf dem Server nicht vorhanden.  
  
6.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eines der <xref:Microsoft.SqlServer.Replication.TransPullSubscription> Eigenschaften, die festgelegt werden können, und rufen Sie dann die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode.  
  
7.  (Optional) Um die neuen Einstellungen anzuzeigen, rufen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> Methode, um die Eigenschaften für den Artikel erneut zu laden.  
  
8.  Trennen Sie alle Verbindungen.  
  
#### So zeigen Sie die Eigenschaften eines Pullabonnements für eine Mergeveröffentlichung an oder ändern sie  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePullSubscription> Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, und <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Eigenschaften.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, wurden entweder die Abonnementeigenschaften in Schritt 3 falsch definiert, oder das Abonnement ist auf dem Server nicht vorhanden.  
  
6.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eines der <xref:Microsoft.SqlServer.Replication.MergePullSubscription> Eigenschaften, die festgelegt werden können, und rufen Sie dann die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode.  
  
7.  (Optional) Um die neuen Einstellungen anzuzeigen, rufen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> Methode, um die Eigenschaften für den Artikel erneut zu laden.  
  
8.  Trennen Sie alle Verbindungen.  
  
## Siehe auch  
 [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  