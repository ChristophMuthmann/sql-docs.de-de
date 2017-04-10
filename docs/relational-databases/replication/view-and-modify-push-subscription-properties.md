---
title: "Anzeigen und &#196;ndern der Eigenschaften von Pushabonnements | Microsoft Docs"
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
  - "Anzeigen von Replikationseigenschaften"
  - "Pushabonnements [SQL Server-Replikation], Eigenschaften"
  - "Abonnements [SQL Server-Replikation], Push"
  - "Pushabonnements [SQL Server-Replikation], ändern"
  - "Ändern von Replikationseigenschaften, Pushabonnements"
  - "Ändern von Abonnements, SQL Server Management Studio"
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Anzeigen und &#196;ndern der Eigenschaften von Pushabonnements
  In diesem Thema wird beschrieben, wie die Eigenschaften von Pushabonnements in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) angezeigt und geändert werden.  
  
 **In diesem Thema**  
  
-   **So können Sie Eigenschaften von Pushabonnements anzeigen und ändern mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Sie können die Eigenschaften von Pushabonnements vom Verleger an den folgenden Stellen anzeigen und ändern:  
  
-   Die **Abonnementeigenschaften - \< Publisher>: \< PublicationDatabase>** Dialogfeld aus [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   Auf der Registerkarte **Alle Abonnements** , verfügbar im Replikationsmonitor. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### So zeigen Sie Eigenschaften von Pushabonnement in Management Studio an und ändern Sie die Eigenschaften  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die entsprechende Veröffentlichung, mit der rechten Maustaste ein Abonnement, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
#### So zeigen Sie Eigenschaften von Pushabonnement im Replikationsmonitor an und ändern Sie die Eigenschaften  
  
1.  Erweitern Sie im linken Bereich des Replikationsmonitors eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
3.  Mit der rechten Maustaste ein Abonnement, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Pushabonnements können geändert und auf ihre Eigenschaften kann mithilfe gespeicherter Replikationsprozeduren programmgesteuert zugegriffen werden. Welche gespeicherten Prozeduren verwendet werden, hängt vom Typ der Veröffentlichung ab, zu der das Abonnement gehört.  
  
#### So zeigen Sie die Eigenschaften eines Pushabonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung an  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md). Geben Sie **@publication**, **@subscriber**und den Wert **all** für **@article**an.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), wobei **@subscriber**.  
  
#### So ändern Sie die Eigenschaften eines Pushabonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changesubscriber](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md), wobei **@subscriber** sowie Parameter für die Abonnenteneigenschaften an.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank, [Sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md). Geben Sie **@publication**, **@subscriber**, **@destination_db**, den Wert **alle** für **@article**, die Abonnementeigenschaft als **@property**, und der neue Wert als **@value**. Dadurch werden die Sicherheitseinstellungen für das Pushabonnement geändert.  
  
3.  (Optional) Um die Data Transformation Services (DTS)-Paketeigenschaften eines Abonnements zu ändern, führen Sie [Sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md) auf dem Abonnenten für die Abonnementdatenbank. Geben Sie die ID des Auftrags des Verteilungs-Agents für **@jobid** und die folgenden DTS-Paketeigenschaften an:  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     Dadurch werden die DTS-Paketeigenschaften eines Abonnements geändert.  
  
    > [!NOTE]  
    >  Auftrags-ID abgerufen werden kann, durch Ausführen von [Sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md).  
  
#### So zeigen Sie die Eigenschaften eines Pushabonnements für eine Mergeveröffentlichung an  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md). Geben Sie **@publication** und **@subscriber**an.  
  
2.  Führen Sie auf dem Verleger [Sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), wobei **@subscriber**.  
  
#### So ändern Sie die Eigenschaften eines Pushabonnements für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md). Geben Sie **@publication**, **@subscriber**, **@subscriber_db**, die Abonnementeigenschaft als **@property**, und der neue Wert als **@value**.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Die RMO-Klassen, mit denen Sie die Eigenschaften von Pushabonnements anzeigen oder ändern, hängen vom Typ der Veröffentlichung ab, für die das Pushabonnement abonniert wird.  
  
#### So zeigen Sie die Eigenschaften eines Pushabonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung an oder ändern sie  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransSubscription> Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, und <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> Eigenschaften.  
  
4.  Legen Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Einstellung der Eigenschaft.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, wurden entweder die Abonnementeigenschaften in Schritt 3 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
6.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eines der <xref:Microsoft.SqlServer.Replication.TransSubscription> Eigenschaften, die festgelegt werden können, und rufen Sie dann die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode.  
  
7.  (Optional) Um die neuen Einstellungen anzuzeigen, rufen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> Methode, um die Eigenschaften für das Abonnement erneut zu laden.  
  
#### So zeigen Sie die Eigenschaften eines Pushabonnements für eine Mergeveröffentlichung an oder ändern sie  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSubscription> Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, und <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> Eigenschaften.  
  
4.  Legen Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Einstellung der Eigenschaft.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, wurden entweder die Abonnementeigenschaften in Schritt 3 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
6.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eines der <xref:Microsoft.SqlServer.Replication.MergeSubscription> Eigenschaften, die festgelegt werden können, und rufen Sie dann die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode.  
  
7.  (Optional) Um die neuen Einstellungen anzuzeigen, rufen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> Methode, um die Eigenschaften für das Abonnement erneut zu laden.  
  
## Siehe auch  
 [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  