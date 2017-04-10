---
title: "Synchronisieren eines Pushabonnements | Microsoft Docs"
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
  - "Synchronisierung [SQL Server-Replikation], Pushabonnements"
  - "Abonnements [SQL Server-Replikation], Push"
  - "Pushabonnements [SQL Server-Replikation], synchronisieren"
ms.assetid: 0cfa7ae5-91d3-4a4f-9edf-a852d45783b5
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# Synchronisieren eines Pushabonnements
  In diesem Thema wird beschrieben, wie ein Pushabonnement in synchronisieren [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [Replikations-Agents](../../relational-databases/replication/agents/replication-agents-overview.md), oder Replikationsverwaltungsobjekten (RMO).  
  
 **In diesem Thema**  
  
-   **So synchronisieren Sie ein Pushabonnement mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Replikations-Agents](#ReplProg)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Abonnements werden durch den Verteilungs-Agent (für Momentaufnahme- und Transaktionsveröffentlichungen) oder durch den Merge-Agent (für Mergeveröffentlichungen) synchronisiert. Agents können kontinuierlich, bei Bedarf oder nach einem Zeitplan ausgeführt werden. Weitere Informationen zum Angeben von Synchronisierungszeitplänen finden Sie unter [Geben Sie Synchronisierungszeitpläne](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
 Die bedarfsgesteuerte Synchronisierung eines Abonnements kann über die Ordner **Lokale Veröffentlichungen** und **Lokale Abonnements** in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und the **Alle Abonnements** im Replikationsmonitor erfolgen. Abonnements von Oracle-Veröffentlichungen können vom Abonnenten nicht bedarfsgesteuert synchronisiert werden. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### So führen Sie die bedarfsgesteuerte Synchronisierung eines Pushabonnements in Management Studio durch (auf dem Verleger)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die Veröffentlichung, für die Abonnements synchronisiert werden sollen.  
  
4.  Mit der rechten Maustaste des Abonnements zu synchronisieren, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
5.  In der **Synchronisierungsstatus anzeigen - \< Abonnent>: \< SubscriptionDatabase>** im Dialogfeld klicken Sie auf **Start**. Nach Abschluss der Synchronisierung wird die Meldung **Synchronisierung abgeschlossen** eingeblendet.  
  
6.  Klicken Sie auf **Schließen**.  
  
#### So führen Sie die bedarfsgesteuerte Synchronisierung eines Pushabonnements in Management Studio durch (auf dem Abonnenten)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Abonnements** .  
  
3.  Mit der rechten Maustaste des Abonnements zu synchronisieren, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
4.  Es wird gemeldet, dass eine Verbindung mit dem Verteiler hergestellt wird. Klicken Sie auf **OK**.  
  
5.  In der **Synchronisierungsstatus anzeigen - \< Abonnent>: \< SubscriptionDatabase>** im Dialogfeld klicken Sie auf **Start**. Nach Abschluss der Synchronisierung wird die Meldung **Synchronisierung abgeschlossen** eingeblendet.  
  
6.  Klicken Sie auf **Schließen**.  
  
#### So führen Sie die bedarfsgesteuerte Synchronisierung eines Pushabonnements im Replikationsmonitor durch  
  
1.  Erweitern Sie im Replikationsmonitor im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
3.  Mit der rechten Maustaste des Abonnements zu synchronisieren, und klicken Sie dann auf **Synchronisierung starten**.  
  
4.  Status der Synchronisierung anzeigen, mit der rechten Maustaste des Abonnements, und klicken Sie auf **Details zum**.  
  
##  <a name="ReplProg"></a> Verwenden von Replikations-Agents  
 Pushabonnements können programmgesteuert oder bei Bedarf synchronisiert werden, indem die entsprechende ausführbare Datei für den Replikations-Agent an der Eingabeaufforderung ausgeführt wird. Welche ausführbare Datei für den Replikations-Agent ausgeführt wird, hängt vom Typ der Veröffentlichung ab, zu der die Pushveröffentlichung gehört.  
  
#### So starten Sie den Verteilungs-Agent, um ein Pushabonnement für eine Transaktionsveröffentlichung zu synchronisieren  
  
1.  Führen Sie auf dem Verteiler an der Eingabeaufforderung oder in einer Batchdatei **distrib.exe**aus. Geben Sie die folgenden Befehlszeilenargumente an:  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType = 0**  
  
     Wenn Sie die SQL Server-Authentifizierung verwenden, müssen Sie auch die folgenden Argumente angeben:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode = 0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode = 0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode = 0**  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
#### So starten Sie den Merge-Agent, um ein Pushabonnement für eine Mergeveröffentlichung zu synchronisieren  
  
1.  Führen Sie auf dem Verteiler an der Eingabeaufforderung oder in einer Batchdatei **replmerg.exe**aus. Geben Sie die folgenden Befehlszeilenargumente an:  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType = 0**  
  
     Wenn Sie die SQL Server-Authentifizierung verwenden, müssen Sie auch die folgenden Argumente angeben:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode = 0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode = 0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode = 0**  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
###  <a name="TsqlExample"></a> Beispiele (Replikations-Agents)  
 Im folgenden Beispiel wird der Verteilungs-Agent gestartet, um ein Pushabonnement zu synchronisieren.  
  
```  
  
REM -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks2012  
SET SubscriptionDB=AdventureWorks2012Replica   
SET Publication=AdvWorksProductsTran  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4  
  
```  
  
 Im folgenden Beispiel wird der Merge-Agent gestartet, um ein Pushabonnement zu synchronisieren.  
  
```  
  
REM -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks2012  
SET SubscriptionDB=AdventureWorks2012Replica   
SET Publication=AdvWorksSalesOrdersMerge  
  
REM -- Start the Merge Agent.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE"  -Publisher %Publisher%   
-Subscriber  %Subscriber%  -Distributor %Publisher% -PublisherDB  %PublicationDB%   
-SubscriberDB %SubscriptionDB% -Publication %Publication% -PublisherSecurityMode 1   
-OutputVerboseLevel 3  -Output -SubscriberSecurityMode 1  -SubscriptionType 0   
-DistributorSecurityMode 1  
  
```  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Pushabonnements mit Replikationsverwaltungsobjekten (RMO) und dem Zugriff von verwaltetem Code auf Funktionen des Replikations-Agents programmgesteuert synchronisieren. Welche Klassen für die Synchronisierung eines Pushabonnements verwendet werden, hängt vom Typ der Veröffentlichung ab, zu der das Abonnement gehört.  
  
> [!NOTE]  
>  Starten Sie den Agent asynchron, wenn Sie eine Synchronisierung starten möchten, die autonom ausgeführt wird, ohne sich auf die Anwendung auszuwirken. Wenn Sie während der Synchronisierung das Ergebnis der Synchronisierung überwachen und Rückrufe vom Agent empfangen möchten (z. B. über eine Statusanzeige), müssen Sie den Agent synchron starten. Für [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] -Abonnenten müssen Sie den Agent synchron starten.  
  
#### So synchronisieren Sie ein Pushabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransSubscription> Klasse, und legen Sie die folgenden Eigenschaften:  
  
    -   Den Namen der Veröffentlichungsdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Der Name der Veröffentlichung, zu dem das Abonnement, für die gehört <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   Der Name der Abonnementdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Der Name des Abonnenten für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Die in Schritt 1 erstellte Verbindung <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode, um die restlichen Abonnementeigenschaften abzurufen. Überprüfen Sie, ob das Abonnement vorhanden ist, wenn diese Methode **false**zurückgibt.  
  
4.  Starten Sie den Verteilungs-Agent auf eine der folgenden Arten auf dem Verteiler:  
  
    -   Rufen Sie die <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizeWithJob%2A> Methode für die Instanz von <xref:Microsoft.SqlServer.Replication.TransSubscription> aus Schritt 2. Diese Methode startet den Verteilungs-Agent asynchron, und die Steuerung wird sofort an die Anwendung zurückgegeben, während der Agentauftrag ausgeführt wird. Sie können diese Methode nicht aufrufen, wenn das Abonnement, mit dem Wert erstellt wurde **false** für <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A>.  
  
    -   Rufen Sie eine Instanz von der <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> -Klasse von der <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizationAgent%2A> -Eigenschaft, und rufen die <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> Methode. Diese Methode startet den Agent synchron, und die Steuerung bleibt beim ausgeführten Agentauftrag. Sie können während der synchronen Ausführung behandeln die <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> Ereignis während der Agent ausgeführt wird.  
  
#### So synchronisieren Sie ein Pushabonnement mit einer Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSubscription> Klasse, und legen Sie die folgenden Eigenschaften:  
  
    -   Den Namen der Veröffentlichungsdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Der Name der Veröffentlichung, zu dem das Abonnement, für die gehört <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   Der Name der Abonnementdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Der Name des Abonnenten für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Die in Schritt 1 erstellte Verbindung <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode, um die restlichen Abonnementeigenschaften abzurufen. Überprüfen Sie, ob das Abonnement vorhanden ist, wenn diese Methode **false**zurückgibt.  
  
4.  Starten Sie den Merge-Agent auf eine der folgenden Arten auf dem Verteiler:  
  
    -   Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizeWithJob%2A> Methode für die Instanz von <xref:Microsoft.SqlServer.Replication.MergeSubscription> aus Schritt 2. Diese Methode startet den Merge-Agent asynchron, und die Steuerung wird sofort an die Anwendung zurückgegeben, während der Agentauftrag ausgeführt wird. Sie können diese Methode nicht aufrufen, wenn das Abonnement, mit dem Wert erstellt wurde **false** für <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A>.  
  
    -   Rufen Sie eine Instanz von der <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> -Klasse von der <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizationAgent%2A> -Eigenschaft, und rufen die <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> Methode. Diese Methode startet den Merge-Agent synchron, und die Steuerung bleibt beim ausgeführten Agentauftrag. Sie können während der synchronen Ausführung behandeln die <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> Ereignis während der Agent ausgeführt wird.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 In diesem Beispiel wird ein Pushabonnement mit einer Transaktionsveröffentlichung synchronisiert, wobei der Agent mit dem Agentauftrag asynchron gestartet wird.  
  
 [!code-csharp[HowTo#rmo_SyncTranPushSub_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_synctranpushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_synctranpushsub_withjob)]  
  
 In diesem Beispiel wird ein Pushabonnement mit einer Transaktionsveröffentlichung synchronisiert, wobei der Agent synchron gestartet wird.  
  
 [!code-csharp[HowTo#rmo_SyncTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_synctranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_synctranpushsub)]  
  
 In diesem Beispiel wird ein Pushabonnement mit einer Mergeveröffentlichung synchronisiert, wobei der Agent asynchron mit dem Agentauftrag gestartet wird.  
  
 [!code-csharp[HowTo#rmo_SyncMergePushSub_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_syncmergepushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_syncmergepushsub_withjob)]  
  
 In diesem Beispiel wird ein Pushabonnement mit einer Mergeveröffentlichung synchronisiert, wobei der Agent synchron gestartet wird.  
  
 [!code-csharp[HowTo#rmo_SyncMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_syncmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_syncmergepushsub)]  
  
## Siehe auch  
 [Konzepte für Replikationsverwaltungsobjekte (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Synchronisieren von Daten](../../relational-databases/replication/synchronize-data.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  