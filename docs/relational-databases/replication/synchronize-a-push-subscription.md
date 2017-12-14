---
title: Synchronisieren eines Pushabonnements | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- synchronization [SQL Server replication], push subscriptions
- subscriptions [SQL Server replication], push
- push subscriptions [SQL Server replication], synchronizing
ms.assetid: 0cfa7ae5-91d3-4a4f-9edf-a852d45783b5
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 41040dbb6c399f45f3aebdb961640910742162d1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="synchronize-a-push-subscription"></a>Synchronisieren eines Pushabonnements
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie ein Pushabonnement in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [Replikations-Agents](../../relational-databases/replication/agents/replication-agents-overview.md) oder Replikationsverwaltungsobjekten (Replication Management Objects, RMO) synchronisiert wird.  
  
 **In diesem Thema**  
  
-   **So synchronisieren Sie ein Pushabonnement mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Replication Agents](#ReplProg)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Abonnements werden durch den Verteilungs-Agent (für Momentaufnahme- und Transaktionsveröffentlichungen) oder durch den Merge-Agent (für Mergeveröffentlichungen) synchronisiert. Agents können kontinuierlich, bei Bedarf oder nach einem Zeitplan ausgeführt werden. Weitere Informationen zum Angeben von Synchronisierungszeitplänen finden Sie unter [Angeben von Synchronisierungszeitplänen](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
 Die bedarfsgesteuerte Synchronisierung eines Abonnements kann über die Ordner **Lokale Veröffentlichungen** und **Lokale Abonnements** in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und the **Alle Abonnements** im Replikationsmonitor erfolgen. Abonnements von Oracle-Veröffentlichungen können vom Abonnenten nicht bedarfsgesteuert synchronisiert werden. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### <a name="to-synchronize-a-push-subscription-on-demand-in-management-studio-at-the-publisher"></a>So führen Sie die bedarfsgesteuerte Synchronisierung eines Pushabonnements in Management Studio durch (auf dem Verleger)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die Veröffentlichung, für die Abonnements synchronisiert werden sollen.  
  
4.  Klicken Sie mit der rechten Maustaste auf das zu synchronisierende Abonnement, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
5.  Klicken Sie im Dialogfeld **Synchronisierungsstatus anzeigen - \<Abonnent>:\<SubscriptionDatabase>** auf **Start**. Nach Abschluss der Synchronisierung wird die Meldung **Synchronisierung abgeschlossen** eingeblendet.  
  
6.  Klicken Sie auf **Schließen**.  
  
#### <a name="to-synchronize-a-push-subscription-on-demand-in-management-studio-at-the-subscriber"></a>So führen Sie die bedarfsgesteuerte Synchronisierung eines Pushabonnements in Management Studio durch (auf dem Abonnenten)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Abonnements** .  
  
3.  Klicken Sie mit der rechten Maustaste auf das zu synchronisierende Abonnement, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
4.  Es wird gemeldet, dass eine Verbindung mit dem Verteiler hergestellt wird. Klicken Sie auf **OK**.  
  
5.  Klicken Sie im Dialogfeld **Synchronisierungsstatus anzeigen – \<Subscriber>:\<SubscriptionDatabase>** auf **Start**. Nach Abschluss der Synchronisierung wird die Meldung **Synchronisierung abgeschlossen** eingeblendet.  
  
6.  Klicken Sie auf **Schließen**.  
  
#### <a name="to-synchronize-a-push-subscription-on-demand-in-replication-monitor"></a>So führen Sie die bedarfsgesteuerte Synchronisierung eines Pushabonnements im Replikationsmonitor durch  
  
1.  Erweitern Sie im Replikationsmonitor im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
3.  Klicken Sie mit der rechten Maustaste auf das Abonnement, das Sie synchronisieren möchten, und klicken Sie dann auf **Synchronisierung starten**.  
  
4.  Wenn Sie den Status der Synchronisierung anzeigen möchten, klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Details anzeigen**.  
  
##  <a name="ReplProg"></a> Verwenden von Replikations-Agents  
 Pushabonnements können programmgesteuert oder bei Bedarf synchronisiert werden, indem die entsprechende ausführbare Datei für den Replikations-Agent an der Eingabeaufforderung ausgeführt wird. Welche ausführbare Datei für den Replikations-Agent ausgeführt wird, hängt vom Typ der Veröffentlichung ab, zu der die Pushveröffentlichung gehört.  
  
#### <a name="to-start-the-distribution-agent-to-synchronize-a-push-subscription-to-a-transactional-publication"></a>So starten Sie den Verteilungs-Agent, um ein Pushabonnement für eine Transaktionsveröffentlichung zu synchronisieren  
  
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
  
#### <a name="to-start-the-merge-agent-to-synchronize-a-push-subscription-to-a-merge-publication"></a>So starten Sie den Merge-Agent, um ein Pushabonnement für eine Mergeveröffentlichung zu synchronisieren  
  
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
  
#### <a name="to-synchronize-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>So synchronisieren Sie ein Pushabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransSubscription> -Klasse, und legen Sie die folgenden Eigenschaften fest:  
  
    -   Den Namen der Veröffentlichungsdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Den Namen der Veröffentlichung, zu der das Abonnement gehört, für <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   Den Namen der Abonnementdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Den Namen des Abonnenten für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Die in Schritt 1 erstellte Verbindung für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf, um die restlichen Abonnementeigenschaften abzurufen. Überprüfen Sie, ob das Abonnement vorhanden ist, wenn diese Methode **false**zurückgibt.  
  
4.  Starten Sie den Verteilungs-Agent auf eine der folgenden Arten auf dem Verteiler:  
  
    -   Rufen Sie die <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizeWithJob%2A> -Methode für die <xref:Microsoft.SqlServer.Replication.TransSubscription> -Instanz aus Schritt 2 auf. Diese Methode startet den Verteilungs-Agent asynchron, und die Steuerung wird sofort an die Anwendung zurückgegeben, während der Agentauftrag ausgeführt wird. Sie können diese Methode nicht aufrufen, wenn das Abonnement mit dem Wert **false** for <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A>.  
  
    -   Rufen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> -Klasse von der <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizationAgent%2A> -Eigenschaft ab, und rufen Sie die <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> -Methode auf. Diese Methode startet den Agent synchron, und die Steuerung bleibt beim ausgeführten Agentauftrag. Während der synchronen Ausführung können Sie das <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> -Ereignis verarbeiten, während der Agent ausgeführt wird.  
  
#### <a name="to-synchronize-a-push-subscription-to-a-merge-publication"></a>So synchronisieren Sie ein Pushabonnement mit einer Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSubscription> -Klasse, und legen Sie die folgenden Eigenschaften fest:  
  
    -   Den Namen der Veröffentlichungsdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Den Namen der Veröffentlichung, zu der das Abonnement gehört, für <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   Den Namen der Abonnementdatenbank für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Den Namen des Abonnenten für <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Die in Schritt 1 erstellte Verbindung für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf, um die restlichen Abonnementeigenschaften abzurufen. Überprüfen Sie, ob das Abonnement vorhanden ist, wenn diese Methode **false**zurückgibt.  
  
4.  Starten Sie den Merge-Agent auf eine der folgenden Arten auf dem Verteiler:  
  
    -   Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizeWithJob%2A> -Methode für die <xref:Microsoft.SqlServer.Replication.MergeSubscription> -Instanz aus Schritt 2 auf. Diese Methode startet den Merge-Agent asynchron, und die Steuerung wird sofort an die Anwendung zurückgegeben, während der Agentauftrag ausgeführt wird. Sie können diese Methode nicht aufrufen, wenn das Abonnement mit dem Wert **false** for <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A>.  
  
    -   Rufen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> -Klasse von der <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizationAgent%2A> -Eigenschaft ab, und rufen Sie die <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> -Methode auf. Diese Methode startet den Merge-Agent synchron, und die Steuerung bleibt beim ausgeführten Agentauftrag. Während der synchronen Ausführung können Sie das <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> -Ereignis verarbeiten, während der Agent ausgeführt wird.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 In diesem Beispiel wird ein Pushabonnement mit einer Transaktionsveröffentlichung synchronisiert, wobei der Agent mit dem Agentauftrag asynchron gestartet wird.  
  
 [!code-cs[HowTo#rmo_SyncTranPushSub_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_synctranpushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_synctranpushsub_withjob)]  
  
 In diesem Beispiel wird ein Pushabonnement mit einer Transaktionsveröffentlichung synchronisiert, wobei der Agent synchron gestartet wird.  
  
 [!code-cs[HowTo#rmo_SyncTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_synctranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_synctranpushsub)]  
  
 In diesem Beispiel wird ein Pushabonnement mit einer Mergeveröffentlichung synchronisiert, wobei der Agent asynchron mit dem Agentauftrag gestartet wird.  
  
 [!code-cs[HowTo#rmo_SyncMergePushSub_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_syncmergepushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_syncmergepushsub_withjob)]  
  
 In diesem Beispiel wird ein Pushabonnement mit einer Mergeveröffentlichung synchronisiert, wobei der Agent synchron gestartet wird.  
  
 [!code-cs[HowTo#rmo_SyncMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_syncmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_syncmergepushsub)]  
  
## <a name="see-also"></a>Siehe auch  
 [Konzepte für Replikationsverwaltungsobjekte (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Synchronisieren von Daten](../../relational-databases/replication/synchronize-data.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
