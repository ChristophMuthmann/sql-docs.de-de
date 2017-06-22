---
title: "Programmgesteuertes Überwachen der Replikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- sp_replmonitorhelppublisher
- sp_replmonitorhelpmergesessiondetail
- monitoring performance [SQL Server replication], publication status
- sp_replmonitorhelpmergesession
- sp_replmonitorhelppublicationthresholds
- monitoring performance [SQL Server replication], subscription status
- monitoring performance [SQL Server replication], Transact-SQL programming
- sp_replmonitorsubscriptionpendingcmds
- sp_replmonitorchangepublicationthreshold
- transactional replication, monitoring
- sp_replmonitorhelppublication
- sp_replmonitorhelpsubscription
- monitoring performance [SQL Server replication], thresholds and warnings
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b05b9c5af4ff9ed8626773fc6714c2c05f1605b2
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="programmatically-monitor-replication"></a>Programmgesteuertes Überwachen der Replikation
  Der Replikationsmonitor ist ein grafisches Tool, mit dem Sie eine Replikationstopologie überwachen können. Mithilfe von gespeicherten [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Replikationsprozeduren oder Replikationsverwaltungsobjekten (RMO) können Sie programmgesteuert auf diese Überwachungsdaten zugreifen. Diese Objekte ermöglichen das Programmieren der folgenden Tasks:  
  
-   Überwachen des Status von Verlegern, Veröffentlichungen und Abonnements.  
  
-   Überwachen von Merge-Agentsitzungen auf mindestens einem Abonnenten.  
  
-   Überwachen von Transaktionsbefehlen, die darauf warten, auf mindestens einem Abonnenten angewendet zu werden.  
  
-   Definieren von Schwellenwertmetriken, um bestimmen zu können, wann eine Veröffentlichung einen Eingriff erfordert.  
  
-   Überwachen des Status von Überwachungstoken.  
  
 **In diesem Thema:**  
  
 [Transact-SQL](#Tsql)  
  
 [Replikationsverwaltungsobjekte (RMO)](#RMO)  
  
##  <a name="Tsql"></a> Transact-SQL  
  
#### <a name="to-monitor-publishers-publications-and-subscriptions-from-the-distributor"></a>So überwachen Sie Verleger, Veröffentlichungen und Abonnements auf dem Verteiler  
  
1.  Führen Sie auf dem Verteiler für die Verteilerdatenbank [sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)aus. Dadurch werden Überwachungsinformationen zu allen Verlegern zurückgegeben, die diesen Verteiler verwenden. Um das Resultset auf nur einen Verleger zu beschränken, geben Sie **@publisher**aus.  
  
2.  Führen Sie auf dem Verteiler für die Verteilerdatenbank [sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)aus. Dadurch werden Überwachungsinformationen zu allen Veröffentlichungen zurückgegeben, die diesen Verteiler verwenden. Um das Resultset auf nur einen Verleger, eine Veröffentlichung oder eine veröffentlichte Datenbank zu beschränken, geben Sie **@publisher**, **@publication**bzw. **@publisher_db**an.  
  
3.  Führen Sie auf dem Verteiler für die Verteilerdatenbank [sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)aus. Dadurch werden Überwachungsinformationen zu allen Abonnements zurückgegeben, die diesen Verteiler verwenden. Um das Resultset auf Abonnements zu beschränken, die nur zu einem Verleger, einer Veröffentlichung oder einer veröffentlichten Datenbank gehören, geben Sie **@publisher**, **@publication**bzw. **@publisher_db**an.  
  
#### <a name="to-monitor-transactional-commands-waiting-to-be-applied-at-the-subscriber"></a>So überwachen Sie Transaktionsbefehle, die darauf warten, auf dem Abonnenten angewendet zu werden  
  
1.  Führen Sie auf dem Verteiler für die Verteilerdatenbank [sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md)aus. Dadurch werden Überwachungsinformationen zu allen Befehlen zurückgegeben, die für alle Abonnements ausstehen, die diesen Verteiler verwenden. Um das Resultset auf Befehle zu beschränken, die für Abonnements ausstehen, die nur zu einem Verleger, einem Abonnenten, einer Veröffentlichung oder einer veröffentlichten Datenbank gehören, geben Sie **@publisher**, **@subscriber**, **@publication**bzw. **@publisher_db**an.  
  
#### <a name="to-monitor-merge-changes-waiting-to-be-uploaded-or-downloaded"></a>So überwachen Sie Mergeänderungen, die darauf warten, hoch- oder heruntergeladen zu werden  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)aus. Dadurch wird ein Resultset mit Informationen zu Änderungen zurückgegeben, die darauf warten, auf Abonnenten repliziert zu werden. Um das Resultset auf Änderungen zu beschränken, die nur zu einer Veröffentlichung oder einem Artikel gehören, geben Sie **@publication** bzw. **@article**an.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)aus. Dadurch wird ein Resultset mit Informationen zu Änderungen zurückgegeben, die darauf warten, auf dem Verleger repliziert zu werden. Um das Resultset auf Änderungen zu beschränken, die nur zu einer Veröffentlichung oder einem Artikel gehören, geben Sie **@publication** bzw. **@article**an.  
  
#### <a name="to-monitor-merge-agent-sessions"></a>So überwachen Sie Merge-Agentsitzungen  
  
1.  Führen Sie auf dem Verteiler für die Verteilerdatenbank [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)aus. Dadurch werden zu allen Merge-Agentsitzungen für alle Abonnements, die diesen Verteiler verwenden, Überwachungsinformationen, beispielsweise **Session_id**, zurückgegeben. Sie können **Session_id** auch ermitteln, indem Sie eine Abfrage der [MSmerge_sessions](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) -Systemtabelle ausführen.  
  
2.  Führen Sie auf dem Verteiler für die Verteilerdatenbank [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)aus. Geben Sie einen Wert **Session_id** aus Schritt 1 für **@session_id**aus. Dadurch werden ausführliche Überwachungsinformationen zu der Sitzung angezeigt.  
  
3.  Wiederholen Sie Schritt 2 für jede Sitzung, die von Interesse ist.  
  
#### <a name="to-monitor-merge-agent-sessions-for-pull-subscriptions-from-the-subscriber"></a>So überwachen Sie Merge-Agentsitzungen für Pullabonnements auf dem Abonnenten  
  
1.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)aus. Geben Sie für ein bestimmtes Abonnement **@publisher**, **@publication**und den Namen der Veröffentlichungsdatenbank für **@publisher_db**aus. Dadurch werden Überwachungsinformationen zu den letzten fünf Merge-Agentsitzungen für dieses Abonnement zurückgegeben. Beachten Sie im Resultset den Wert **Session_id** für Sitzungen, die von Interesse sind.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)aus. Geben Sie einen Wert **Session_id** aus Schritt 1 für **@session_id**aus. Dadurch werden ausführliche Überwachungsinformationen zu der Sitzung angezeigt.  
  
3.  Wiederholen Sie Schritt 2 für jede Sitzung, die von Interesse ist.  
  
#### <a name="to-view-and-modify-the-monitor-threshold-metrics-for-a-publication"></a>So können Sie die Schwellenwertmetriken für die Überwachung für eine Veröffentlichung anzeigen und ändern  
  
1.  Führen Sie auf dem Verteiler für die Verteilerdatenbank [sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)aus. Dadurch werden Überwachungsschwellenwerte zurückgegeben, die für alle Veröffentlichungen festgelegt wurden, die diesen Verteiler verwenden. Um das Resultset auf Überwachungsschwellenwerte für Veröffentlichungen festzulegen, die nur zu einem Verleger, einer veröffentlichten Datenbank oder einer Veröffentlichung gehören, geben Sie **@publisher**, **@publisher_db**bzw. **@publication**an. Beachten Sie den Wert **Metric_id** für alle Schwellenwerte, die geändert werden müssen. Weitere Informationen finden Sie unter [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
2.  Führen Sie auf dem Verteiler für die Verteilerdatenbank [sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)aus. Geben Sie bei Bedarf Folgendes an:  
  
    -   Den in Schritt 1 ermittelten **Metric_id** -Wert für **@metric_id**aus.  
  
    -   Einen neuen Wert für die Schwellenwertmetrik für die Überwachung für **@value**aus.  
  
    -   Einen Wert **1** für **@shouldalert** für eine Warnung, die protokolliert wird, wenn dieser Schwellenwert erreicht wird, oder einen Wert **0** , wenn keine Warnung erforderlich ist.  
  
    -   Einen Wert **1** für **@mode** , um die Schwellenwertmetrik für die Überwachung zu aktivieren, oder der Wert **2** , um diese zu deaktivieren.  
  
##  <a name="RMO"></a> Replikationsverwaltungsobjekte (RMO)  
  
#### <a name="to-monitor-a-subscription-to-a-merge-publication-at-the-subscriber"></a>So überwachen Sie ein Abonnement für eine Mergeveröffentlichung auf dem Abonnenten  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor>-Klasse, legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A> und <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> für das Abonnement fest, und legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf <xref:Microsoft.SqlServer.Management.Common.ServerConnection> fest, die Sie in Schritt 1 erstellt haben.  
  
3.  Rufen Sie eine der folgenden Methoden auf, um Informationen zu Merge-Agentsitzungen für dieses Abonnement zurückzugeben:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A>: Gibt ein Array von <xref:Microsoft.SqlServer.Replication.MergeSessionSummary>-Objekten mit Informationen zu maximal den letzten fünf Merge-Agentsitzungen zurück. Beachten Sie den <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A>-Wert für alle Sitzungen, die von Interesse sind.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A>: Gibt ein Array von <xref:Microsoft.SqlServer.Replication.MergeSessionSummary>-Objekten mit Informationen zu Merge-Agentsitzungen zurück, die während der Anzahl der als *Stunden*-Parameter übergebenen vergangenen Stunden (maximal der letzten fünf Sitzungen) aufgetreten sind. Beachten Sie den <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A>-Wert für alle Sitzungen, die von Interesse sind.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A>: Gibt ein <xref:Microsoft.SqlServer.Replication.MergeSessionSummary>-Objekt mit Informationen zu der letzten Merge-Agentsitzung zurück. Beachten Sie den <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A>-Wert für diese Sitzung.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt mit Informationen zu maximal den letzten fünf Merge-Agentsitzungen zurück (eines pro Reihe). Beachten Sie den Wert der **Session_id** -Spalte für alle Sitzungen, die von Interesse sind.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A>: Gibt ein <xref:System.Data.DataRow>-Objekt mit Informationen zu den letzten Merge-Agentsitzungen zurück. Beachten Sie den Wert der **Session_id** -Spalte für diese Sitzung.  
  
4.  (Optional) Rufen Sie <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> zum Aktualisieren der Daten für das als *mss* übergebene <xref:Microsoft.SqlServer.Replication.MergeSessionSummary>-Objekt auf, oder rufen Sie <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> zum Aktualisieren der Daten im als *drRefresh* übergebenen <xref:System.Data.DataRow>-Objekt auf.  
  
5.  Rufen Sie mithilfe der in Schritt 3 abgerufenen Sitzungs-ID eine der folgenden Methoden auf, um Informationen zu den Details einer bestimmten Sitzung zurückzugeben:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A>: Gibt ein Array von <xref:Microsoft.SqlServer.Replication.MergeSessionDetail>-Objekten für die angegebene *SessionId* zurück.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt mit Informationen für die angegebene *SessionId* zurück.  
  
#### <a name="to-monitor-replication-properties-for-all-publications-at-a-distributor"></a>So überwachen Sie die Replikationseigenschaften für alle Veröffentlichungen auf einem Verteiler  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationMonitor>-Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf <xref:Microsoft.SqlServer.Management.Common.ServerConnection> fest, die Sie in Schritt 1 erstellt haben.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen.  
  
5.  Führen Sie mindestens eine der folgenden Methoden aus, um Replikationsinformationen für alle Verleger zurückzugeben, die diesen Verteiler verwenden:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu allen Verteilungs-Agents auf diesem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu auf dem Verteiler gespeicherten Fehlern enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu allen Protokolllese-Agents auf dem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu allen Merge-Agents auf dem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu allen anderen Replikations-Agents auf dem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu allen Verlegern auf diesem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das die Verleger, die diesen Verteiler verwenden, zurückgibt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu allen Warteschlangenlese-Agents auf dem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Einzelheiten zu dem angegebenen Warteschlangenlese-Agent und der angegebenen Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Sitzungsinformationen zu dem angegebenen Warteschlangenlese-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu allen Momentaufnahme-Agents auf dem Verteiler enthält.  
  
#### <a name="to-monitor-publication-properties-for-a-specific-publisher-at-the-distributor"></a>So überwachen Sie die Veröffentlichungseigenschaften für einen bestimmten Verleger auf dem Verteiler  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Rufen Sie auf eine der folgenden Arten ein <xref:Microsoft.SqlServer.Replication.PublisherMonitor>-Objekt ab.  
  
    -   Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.PublisherMonitor>-Klasse. Legen Sie die <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A>-Eigenschaft für den Verleger fest, und legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf <xref:Microsoft.SqlServer.Management.Common.ServerConnection> fest, die Sie in Schritt 1 erstellt haben. Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, ist der Verlegername falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
    -   Aus der <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection>, auf die mittels der <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A>-Eigenschaft eines vorhandenen <xref:Microsoft.SqlServer.Replication.ReplicationMonitor>-Objekts zugegriffen wird.  
  
3.  Führen Sie mindestens eine der folgenden Methoden aus, um Replikationsinformationen für alle Veröffentlichungen zurückzugeben, die zu diesem Verleger gehören.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Einzelheiten zu dem angegebenen Verteilungs-Agent und der angegebenen Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Sitzungsinformationen zu dem angegebenen Verteilungs-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Fehlereintragsinformationen zu dem angegebenen Fehler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Einzelheiten zu dem angegebenen Protokolllese-Agent und der angegebenen Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Sitzungsinformationen für den angegebenen Protokolllese-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Einzelheiten zu dem angegebenen Merge-Agent und der angegebenen Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das weitere Einzelheiten zu dem angegebenen Merge-Agent und der angegebenen Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Sitzungsinformationen zu dem angegebenen Merge-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das weitere Sitzungsinformationen zu dem angegebenen Merge-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu allen Veröffentlichungen auf diesem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das weitere Informationen zu allen Veröffentlichungen auf diesem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Einzelheiten zu dem angegebenen Momentaufnahme-Agent und der angegebenen Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Sitzungsinformationen zu dem angegebenen Momentaufnahme-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu allen Abonnements von Veröffentlichungen auf diesem Verteiler enthält.  
  
#### <a name="to-monitor-properties-for-a-specific-publication-at-the-distributor"></a>So überwachen Sie die Eigenschaften für eine bestimmte Veröffentlichung auf dem Verteiler  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Rufen Sie auf eine der folgenden Arten ein <xref:Microsoft.SqlServer.Replication.PublicationMonitor>-Objekt ab.  
  
    -   Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.PublicationMonitor>-Klasse. Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> und <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> für die Veröffentlichung fest, und legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> fest, die Sie in Schritt 1 erstellt haben. Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
    -   Aus der <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection>, auf die mittels der <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A>-Eigenschaft eines vorhandenen <xref:Microsoft.SqlServer.Replication.PublisherMonitor>-Objekts zugegriffen wird.  
  
3.  Führen Sie mindestens eine der folgenden Methoden aus, um Informationen zu dieser Veröffentlichung zurückzugeben.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Fehlereinträge zu dem angegebenen Fehler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu dem Protokolllese-Agent für diese Veröffentlichung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu den Warnungsschwellenwerten für die Überwachung für diese Veröffentlichung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu dem bei dieser Veröffentlichung verwendeten Warteschlangenlese-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu dem Momentaufnahme-Agent für diese Veröffentlichung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu Abonnements für diese Veröffentlichung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das weitere Informationen zu Abonnements für diese Veröffentlichung auf Grundlage der angegebenen <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption> enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Latenzzeitinformationen zu dem angegebenen Überwachungstoken enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A>: Gibt ein <xref:System.Data.DataSet>-Objekt zurück, das Informationen zu allen in diese Veröffentlichung eingefügten Überwachungstoken enthält.  
  
#### <a name="to-monitor-transactional-commands-that-are-waiting-to-be-applied-at-the-subscriber"></a>So überwachen Sie Transaktionsbefehle, die darauf warten, auf dem Abonnenten angewendet zu werden  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Rufen Sie auf eine der folgenden Arten ein <xref:Microsoft.SqlServer.Replication.PublicationMonitor>-Objekt ab.  
  
    -   Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.PublicationMonitor>-Klasse. Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> und <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> für die Veröffentlichung fest, und legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> fest, die Sie in Schritt 1 erstellt haben. Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
    -   Aus der <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection>, auf die mittels der <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A>-Eigenschaft eines vorhandenen <xref:Microsoft.SqlServer.Replication.PublisherMonitor>-Objekts zugegriffen wird.  
  
3.  Führen Sie die <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A>-Methode aus, die ein <xref:Microsoft.SqlServer.Replication.PendingCommandInfo>-Objekt zurückgibt.  
  
4.  Verwenden Sie die Eigenschaften dieses <xref:Microsoft.SqlServer.Replication.PendingCommandInfo>-Objekts, um die geschätzte Anzahl von ausstehenden Befehlen und die Dauer für das Abschließen der Übermittlung dieser Befehle zu bestimmen.  
  
#### <a name="to-set-the-monitor-warning-thresholds-for-a-publication"></a>So legen Sie die Warnungsschwellenwerte für die Überwachung für eine Veröffentlichung fest  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Rufen Sie auf eine der folgenden Arten ein <xref:Microsoft.SqlServer.Replication.PublicationMonitor>-Objekt ab.  
  
    -   Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.PublicationMonitor>-Klasse. Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> und <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> für die Veröffentlichung fest, und legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> fest, die Sie in Schritt 1 erstellt haben. Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
    -   Aus der <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection>, auf die mittels der <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A>-Eigenschaft eines vorhandenen <xref:Microsoft.SqlServer.Replication.PublisherMonitor>-Objekts zugegriffen wird.  
  
3.  Führen Sie die <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A>-Methode aus. Beachten Sie die aktuellen Schwellenwerteinstellungen in der zurückgegebenen <xref:System.Collections.ArrayList> der <xref:Microsoft.SqlServer.Replication.MonitorThreshold>-Objekte.  
  
4.  Führen Sie die <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A>-Methode aus. Übergeben Sie die folgenden Parameter:  
  
    -   *metricID*: <xref:System.Int32>-Wert, der die Schwellenwertmetrik für die Überwachung aus der folgenden Tabelle darstellt:  
  
        |Wert|Beschreibung|  
        |-----------|-----------------|  
        |1|**expiration** - überwacht den bevorstehenden Ablauf von Abonnements für Transaktionsveröffentlichungen.|  
        |2|**latency** - überwacht die Leistung von Abonnements für Transaktionsveröffentlichungen.|  
        |4|**mergeexpiration** - überwacht den bevorstehenden Ablauf von Abonnements für Mergeveröffentlichungen.|  
        |5|**mergeslowrunduration** - überwacht die Dauer von Mergesynchronisierungen über Verbindungen mit niedriger Bandbreite (DFÜ-Verbindungen).|  
        |6|**mergefastrunduration** - überwacht die Dauer von Mergesynchronisierungen über Verbindungen mit niedriger Bandbreite (DFÜ-Verbindungen).|  
        |7|**mergefastrunspeed** - Überwachung der Synchronisierungsgeschwindigkeit von Mergesynchronisierungen über Verbindungen mit hoher Bandbreite (LAN-Verbindungen).|  
        |8|**mergeslowrunspeed** - überwacht die Synchronisierungsgeschwindigkeit von Mergesynchronisierungen über Verbindungen mit niedriger Bandbreite (DFÜ-Verbindungen).|  
  
    -   *enable*: <xref:System.Boolean>-Wert, der angibt, ob die Metrik für die Veröffentlichung aktiviert ist.  
  
    -   *thresholdValue* - ganzzahliger Wert, der den Schwellenwert festlegt.  
  
    -   *shouldAlert* - ganze Zahl, die angibt, ob dieser Schwellenwert eine Warnung generieren soll.  
  
  
