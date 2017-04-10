---
title: "Erstellen eines Pushabonnements | Microsoft Docs"
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
  - "Pushabonnements [SQL Server-Replikation], erstellen"
  - "Abonnieren einer Mergereplikation [SQL Server-Replikation], Pushabonnements"
  - "Abonnements [SQL Server-Replikation], Push"
  - "Momentaufnahmereplikation [SQL Server], abonnieren"
  - "Transaktionsreplikation, abonnieren"
ms.assetid: adfbbc61-58d1-4330-9ad6-b14ab1142e2b
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Erstellen eines Pushabonnements
  In diesem Thema wird beschrieben, wie erstellen Sie ein Pushabonnement in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)], oder Replikationsverwaltungsobjekten (RMO). Informationen zum Erstellen eines Pushabonnements für einen nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten finden Sie unter [Erstellen eines Abonnements für einen nicht-SQL Server-Abonnenten](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
 
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Erstellen Sie mit dem Assistenten für neue Abonnements ein Pushabonnement auf dem Verleger oder dem Abonnenten. Folgen Sie den Seiten im Assistenten für folgende Aufgaben:  
  
-   Angeben des Verlegers und der Veröffentlichung.  
  
-   Auswählen, wo die Replikations-Agents ausgeführt werden. Wählen Sie für ein Pushabonnement **Führen Sie alle Agents auf dem Verteiler (Pushabonnements)** auf die **Agent Vertriebsort** Seite oder **Speicherort des Merge-Agent** je nach Typ der Veröffentlichung.  
  
-   Angeben der Abonnenten und Abonnentendatenbanken.  
  
-   Angeben der Anmeldenamen und Kennwörter für Verbindungen zwischen den Replikations-Agents:  
  
    -   Bei Abonnements für Momentaufnahme- und Transaktionsveröffentlichungen geben Sie die Anmeldeinformationen auf der Seite **Sicherheit für den Verteilungs-Agent** an.  
  
    -   Bei Abonnements für Mergeveröffentlichungen geben Sie die Anmeldeinformationen auf der Seite **Sicherheit für den Merge-Agent** an.  
  
     Informationen zu den einzelnen Agents erforderlichen Berechtigungen finden Sie unter [Sicherheitsmodell des Replikations-Agent](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Angeben eines Synchronisierungszeitplans und wann der Abonnent initialisiert werden soll.  
  
-   Angeben weiterer Optionen für Mergeveröffentlichungen: Abonnementtyp und Werte für parametrisierte Filter.  
  
-   Angeben weiterer Optionen für Transaktionsveröffentlichungen, die aktualisierbare Abonnements zulassen: ob Abonnenten sofort ein Commit für Änderungen auf dem Verleger ausführen oder die Änderungen in eine Warteschlange schreiben sollen; die Anmeldeinformationen zum Herstellen einer Verbindung zwischen Abonnenten und Verleger.  
  
-   Optionale Skripterstellung für das Abonnement.  
  
#### So erstellen Sie ein Pushabonnement auf dem Verleger  
  
1.  Stellen Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Mit der rechten Maustaste in der Veröffentlichung, für die Sie ein oder mehrere Abonnements erstellen, und klicken Sie dann auf möchten **neue Abonnements**.  
  
4.  Schließen Sie die Seiten im Assistenten für neue Abonnements ab.  
  
#### So erstellen Sie ein Pushabonnement auf dem Abonnenten  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** .  
  
3.  Mit der rechten Maustaste die **Lokale Abonnements** Ordner, und klicken Sie dann auf **neue Abonnements**.  
  
4.  Auf der **Veröffentlichung** Seite des Assistenten für neue Abonnements, wählen Sie **\< SQL Server-Verleger suchen>** oder **\< Oracle-Verleger suchen>** aus der **Publisher** Dropdown-Liste.  
  
5.  Stellen Sie im Dialogfeld **Verbindung mit Server herstellen** eine Verbindung mit dem Verleger her.  
  
6.  Wählen Sie auf der Seite **Veröffentlichung** eine Veröffentlichung aus.  
  
7.  Schließen Sie die Seiten im Assistenten für neue Abonnements ab.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Pushabonnements können mithilfe von gespeicherten Replikationsprozeduren programmgesteuert erstellt werden. Die verwendeten gespeicherten Prozeduren hängen vom Typ der Veröffentlichung ab, zu der das Abonnement gehört.  
  
> **WICHTIG!** Die Benutzer sollten nach Möglichkeit während der Laufzeit zur Eingabe von Anmeldeinformationen aufgefordert werden. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
#### So erstellen Sie ein Pushabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung.  
  
1.  Auf dem Verleger für die Veröffentlichungsdatenbank, stellen Sie sicher, dass die Veröffentlichung Pushabonnements, indem unterstützt [Sp_helppublication](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md).  
  
    -   Wenn der Wert der **Allow_push** ist **1**, werden Pushabonnements unterstützt.  
  
    -   Wenn der Wert der **Allow_push** ist **0**, führen Sie [Sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), wobei **Allow_push** für **@property** und **true** für **@value**.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addsubscription](https://msdn.microsoft.com/library/ms181702.aspx). Geben Sie **@publication**, **@subscriber** und **@destination_db**. Geben Sie den Wert **Push** für **@subscription_type**. Informationen zum Aktualisieren von Abonnements, finden Sie unter [Erstellen eines aktualisierbaren Abonnements für eine Transaktionsveröffentlichung](https://msdn.microsoft.com/library/ms152769.aspx).  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank, [Sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Geben Sie Folgendes an:  
  
    -   Die **@subscriber**, **@subscriber_db**, und **@publication** Parameter.  
  
    -   Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen, unter dem der Verteilungsagent auf dem Verteiler ausgeführt, für die wird **@job_login** und **@job_password**.  
  
        > **Hinweis:** Verbindungen, die immer mit der integrierten Windows-Authentifizierung verwenden, die Windows-Anmeldeinformationen, die durch angegebene **@job_login** und **@job_password**. Der Verteilungs-Agent stellt die lokale Verbindung mit dem Verteiler immer mithilfe der Windows-Authentifizierung her. Standardmäßig stellt der Agent mithilfe der integrierten Windows-Authentifizierung eine Verbindung mit dem Abonnenten her.  
  
    -   (Optional) Der Wert **0** für **@subscriber_security_mode** und [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@subscriber_login** und **@subscriber_password**. Geben Sie diese Parameter an, falls Sie beim Herstellen einer Verbindung mit dem Abonnenten die SQL Server-Authentifizierung verwenden müssen.  
  
    -   Einen Zeitplan für den Verteilungs-Agentauftrag für dieses Abonnement. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > **WICHTIG!** Beim Erstellen eines Pushabonnements auf einem Verleger mit einem Remoteverteiler werden die angegebenen Werte für alle Parameter einschließlich *Job_login* und *Job_password*, werden als nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### So erstellen Sie ein Pushabonnement für eine Mergeveröffentlichung  
  
1.  Auf dem Verleger für die Veröffentlichungsdatenbank, stellen Sie sicher, dass die Veröffentlichung Pushabonnements, indem unterstützt [Sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md).  
  
    -   Wenn der Wert der **Allow_push** ist **1**, die Veröffentlichung Pushabonnements unterstützt.  
  
    -   Wenn der Wert der **Allow_push** ist nicht **1**, führen Sie [Sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), wobei **Allow_push** für **@property** und **true** für **@value**.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md), geben Sie die folgenden Parameter:  
  
    -   **@publication**. Das ist der Name der Veröffentlichung.  
  
    -   **@subscriber_type**. Geben Sie für ein Clientabonnement **local** und für ein Serverabonnement **global**an.  
  
    -   **@subscription_priority**. Geben Sie für ein Serverabonnement eine Priorität für das Abonnement (**0,00** zu **99,99**).  
  
         Weitere Informationen finden Sie unter [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank, [Sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Geben Sie Folgendes an:  
  
    -   Die **@subscriber**, **@subscriber_db**, und **@publication** Parameter.  
  
    -   Die Windows-Anmeldeinformationen, unter dem der Merge-Agent auf dem Verteiler ausgeführt, für die wird **@job_login** und **@job_password**.  
  
        > **Hinweis:**  Verbindungen, die immer mit der integrierten Windows-Authentifizierung verwenden, die Windows-Anmeldeinformationen, die durch angegebene **@job_login** und **@job_password**. Der Merge-Agent stellt die lokale Verbindung mit dem Verteiler immer mithilfe der Windows-Authentifizierung her. Standardmäßig stellt der Agent mithilfe der integrierten Windows-Authentifizierung eine Verbindung mit dem Abonnenten her.  
  
    -   (Optional) Der Wert **0** für **@subscriber_security_mode** und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@subscriber_login** und **@subscriber_password**. Geben Sie diese Parameter an, falls Sie beim Herstellen einer Verbindung mit dem Abonnenten die SQL Server-Authentifizierung verwenden müssen.  
  
    -   (Optional) Der Wert **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Geben Sie diese Werte an, falls Sie beim Herstellen einer Verbindung mit dem Verleger die SQL Server-Authentifizierung verwenden müssen.  
  
    -   Einen Zeitplan für den Merge-Agentauftrag für dieses Abonnement. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > **WICHTIG!** Beim Erstellen eines Pushabonnements auf einem Verleger mit einem Remoteverteiler werden die angegebenen Werte für alle Parameter einschließlich *Job_login* und *Job_password*, werden als nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Im folgenden Beispiel wird ein Pushabonnement für eine Transaktionsveröffentlichung erstellt. Die Werte für den Anmeldenamen und das Kennwort werden zur Laufzeit mithilfe von **sqlcmd** -Skriptvariablen bereitgestellt.  
  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/create-a-push-subscription_1.sql)]  
  
 Im folgenden Beispiel wird ein Pushabonnement für eine Mergeveröffentlichung erstellt. Die Werte für den Anmeldenamen und das Kennwort werden zur Laufzeit mithilfe von **sqlcmd** -Skriptvariablen bereitgestellt.  
  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/create-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Pushabonnements mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert erstellen. Die RMO-Klassen, die Sie zum Erstellen eines Pushabonnements verwenden, hängen vom Typ der Veröffentlichung ab, für die das Abonnement erstellt wird.  
  
> **WICHTIG!** Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen speichern müssen, verwenden Sie die [Kryptografiedienste](http://go.microsoft.com/fwlink/?LinkId=34733) von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
#### So erstellen Sie ein Pushabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung.  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPublication> Klasse, indem Sie die verlegerverbindung aus Schritt 1. Geben Sie <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, und <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Wenn diese Methode **false**zurückgibt, sind entweder die in Schritt 2 angegebenen Eigenschaften falsch definiert, oder die Veröffentlichung ist auf dem Server nicht vorhanden.  
  
4.  Führen Sie ein bitweises logisches AND (**&** in Visual c# und **und** in Visual Basic) zwischen den <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> Eigenschaft und <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Wenn das Ergebnis <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, legen <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> auf das Ergebnis eines bitweisen logischen OR (**|** in Visual c# und **oder** in Visual Basic) zwischen <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> und <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Rufen Sie dann <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> um Pushabonnements zu aktivieren.  
  
5.  Wenn die Abonnementdatenbank nicht vorhanden ist, erstellen sie mithilfe der <xref:Microsoft.SqlServer.Management.Smo.Database> Klasse. Weitere Informationen finden Sie unter [erstellen, ändern und Entfernen von Datenbanken](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransSubscription> Klasse.  
  
7.  Legen Sie folgende Eigenschaften für das Abonnement fest:  
  
    -   Die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> auf dem Verleger erstellt, die Schritt 1 für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Name der Abonnementdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Name des Abonnenten für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Name der Veröffentlichungsdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Name der Veröffentlichung für <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   Die <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> und <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> oder <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> Felder <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> für die Anmeldeinformationen für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Verteilungsagent auf dem Verteiler ausgeführt wird. Mit diesem Konto werden lokale Verbindungen mit dem Verteiler sowie Remoteverbindungen mithilfe der Windows-Authentifizierung hergestellt.  
  
        > **Hinweis:** Einstellung <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> ist nicht erforderlich, wenn das Abonnement, von einem Mitglied erstellt wird der **Sysadmin** festen Serverrolle, es wird jedoch empfohlen. In diesem Fall nimmt der Agent die Identität des SQL Server-Agent-Kontos an. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Optional) Der Wert **true** (Standard) für <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> um einen Agentauftrag zu erstellen, die zum Synchronisieren des Abonnements verwendet wird. Wenn Sie **false**angeben, kann das Abonnement nur programmgesteuert synchronisiert werden.  
  
    -   (Optional) Legen Sie die <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> oder <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> Felder <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> beim SQL Server-Authentifizierung mit dem Abonnenten herstellen.  
  
8.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> Methode.  
  
    > **WICHTIGE!!**Beim Erstellen eines Pushabonnements auf einem Verleger mit einem Remoteverteiler werden die angegebenen Werte für alle Eigenschaften, einschließlich <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, werden als nur-Text an den Verteiler gesendet. Verschlüsseln Sie die Verbindung zwischen dem Verleger und die zugehörigen Remoteverteiler vor dem Aufruf der <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> Methode. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### So erstellen Sie ein Pushabonnement für eine Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication> Klasse, indem Sie die verlegerverbindung aus Schritt 1. Geben Sie <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, und <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Wenn diese Methode **false**zurückgibt, sind entweder die in Schritt 2 angegebenen Eigenschaften falsch definiert, oder die Veröffentlichung ist auf dem Server nicht vorhanden.  
  
4.  Führen Sie ein bitweises logisches AND (**&** in Visual c# und **und** in Visual Basic) zwischen den <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> Eigenschaft und <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Wenn das Ergebnis <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, legen <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> auf das Ergebnis eines bitweisen logischen OR (**|** in Visual c# und **oder** in Visual Basic) zwischen <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> und <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Rufen Sie dann <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> um Pushabonnements zu aktivieren.  
  
5.  Wenn die Abonnementdatenbank nicht vorhanden ist, erstellen sie mithilfe der <xref:Microsoft.SqlServer.Management.Smo.Database> Klasse. Weitere Informationen finden Sie unter [erstellen, ändern und Entfernen von Datenbanken](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSubscription> Klasse.  
  
7.  Legen Sie folgende Eigenschaften für das Abonnement fest:  
  
    -   Die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> auf dem Verleger erstellt, die Schritt 1 für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Name der Abonnementdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Name des Abonnenten für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Name der Veröffentlichungsdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Name der Veröffentlichung für <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   Die <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> und <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> oder <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> Felder <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> für die Anmeldeinformationen für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Merge-Agent auf dem Verteiler ausgeführt wird. Mit diesem Konto werden lokale Verbindungen mit dem Verteiler sowie Remoteverbindungen mithilfe der Windows-Authentifizierung hergestellt.  
  
        > **Hinweis:** Einstellung <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> ist nicht erforderlich, wenn das Abonnement, von einem Mitglied erstellt wird der **Sysadmin** festen Serverrolle, es wird jedoch empfohlen. In diesem Fall nimmt der Agent die Identität des SQL Server-Agent-Kontos an. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Optional) Der Wert **true** (Standard) für <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> um einen Agentauftrag zu erstellen, die zum Synchronisieren des Abonnements verwendet wird. Wenn Sie **false**angeben, kann das Abonnement nur programmgesteuert synchronisiert werden.  
  
    -   (Optional) Legen Sie die <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> oder <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> Felder <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> beim SQL Server-Authentifizierung mit dem Abonnenten herstellen.  
  
    -   (Optional) Legen Sie die <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> oder <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> Felder <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> beim SQL Server-Authentifizierung mit dem Verleger herstellen.  
  
8.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> Methode.  
  
    > **WICHTIG!**  Beim Erstellen eines Pushabonnements auf einem Verleger mit einem Remoteverteiler werden die angegebenen Werte für alle Eigenschaften, einschließlich <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, werden als nur-Text an den Verteiler gesendet. Verschlüsseln Sie die Verbindung zwischen dem Verleger und die zugehörigen Remoteverteiler vor dem Aufruf der <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> Methode. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 Im folgenden Beispiel wird ein neues Pushabonnement für eine Transaktionsveröffentlichung erstellt. Die Anmeldeinformationen für das Windows-Konto, mit dem der Verteilungs-Agent-Auftrag ausgeführt wird, werden zur Laufzeit übergeben.  
  
 [!code-csharp[HowTo#rmo_CreateTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpushsub)]  
  
 Im folgenden Beispiel wird ein neues Pushabonnement für eine Mergeveröffentlichung erstellt. Die Anmeldeinformationen für das Windows-Konto, mit dem der Merge-Agent-Auftrag ausgeführt wird, werden zur Laufzeit übergeben.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## Siehe auch  
 [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Konzepte für Replikationsverwaltungsobjekte (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Synchronisieren eines Pushabonnements](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [Verwenden von sqlcmd mit Skriptvariablen](../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)  
  
  