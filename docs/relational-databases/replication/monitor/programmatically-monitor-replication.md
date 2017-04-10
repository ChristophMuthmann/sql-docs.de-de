---
title: "Programmgesteuertes &#220;berwachen der Replikation | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_replmonitorhelppublisher"
  - "sp_replmonitorhelpmergesessiondetail"
  - "Überwachen der Leistung [SQL Server-Replikation], Veröffentlichungsstatus"
  - "sp_replmonitorhelpmergesession"
  - "sp_replmonitorhelppublicationthresholds"
  - "Überwachen der Leistung [SQL Server-Replikation], Abonnementstatus"
  - "Überwachen der Leistung [SQL Server-Replikation], Transact-SQL-Programmierung"
  - "sp_replmonitorsubscriptionpendingcmds"
  - "sp_replmonitorchangepublicationthreshold"
  - "Transaktionsreplikation, Überwachung"
  - "sp_replmonitorhelppublication"
  - "sp_replmonitorhelpsubscription"
  - "Überwachen der Leistung [SQL Server-Replikation], Schwellenwerte und Warnungen"
  - "Überwachen der Mergereplikation [SQL Server-Replikation]"
  - "Momentaufnahmereplikation [SQL Server], überwachen"
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Programmgesteuertes &#220;berwachen der Replikation
  Der Replikationsmonitor ist ein grafisches Tool, mit dem Sie eine Replikationstopologie überwachen können. Mithilfe von gespeicherten [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Replikationsprozeduren oder Replikationsverwaltungsobjekten (RMO) können Sie programmgesteuert auf diese Überwachungsdaten zugreifen. Diese Objekte ermöglichen das Programmieren der folgenden Tasks:  
  
-   Überwachen des Status von Verlegern, Veröffentlichungen und Abonnements.  
  
-   Überwachen von Merge-Agentsitzungen auf mindestens einem Abonnenten.  
  
-   Überwachen von Transaktionsbefehlen, die darauf warten, auf mindestens einem Abonnenten angewendet zu werden.  
  
-   Definieren von Schwellenwertmetriken, um bestimmen zu können, wann eine Veröffentlichung einen Eingriff erfordert.  
  
-   Überwachen des Status von Überwachungstoken.  
  
 **In diesem Thema:**  
  
 [Transact-SQL](#Tsql)  
  
 [Replikationsverwaltungsobjekte (RMO)](#RMO)  
  
##  <a name="Tsql"></a> Transact-SQL  
  
#### So überwachen Sie Verleger, Veröffentlichungen und Abonnements auf dem Verteiler  
  
1.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md). Dadurch werden Überwachungsinformationen zu allen Verlegern zurückgegeben, die diesen Verteiler verwenden. Um das Resultset auf nur einen Verleger zu beschränken, geben Sie **@publisher**an.  
  
2.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md). Dadurch werden Überwachungsinformationen zu allen Veröffentlichungen zurückgegeben, die diesen Verteiler verwenden. Um das Resultset auf nur einen Verleger, Veröffentlichung oder einer veröffentlichten Datenbank zu beschränken, geben **@publisher**, **@publication**, oder **@publisher_db**, bzw..  
  
3.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md). Dadurch werden Überwachungsinformationen zu allen Abonnements zurückgegeben, die diesen Verteiler verwenden. Um das Resultset auf Abonnements gehören zu einem Verleger zu beschränken, geben Sie Veröffentlichung oder einer veröffentlichten Datenbank **@publisher**, **@publication**, oder **@publisher_db**, bzw..  
  
#### So überwachen Sie Transaktionsbefehle, die darauf warten, auf dem Abonnenten angewendet zu werden  
  
1.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md). Dadurch werden Überwachungsinformationen zu allen Befehlen zurückgegeben, die für alle Abonnements ausstehen, die diesen Verteiler verwenden. Um das Resultset auf Befehle steht für Abonnements gehören zu einem Verleger zu beschränken, geben Sie Abonnenten, Veröffentlichung oder einer veröffentlichten Datenbank **@publisher**, **@subscriber**, **@publication**, oder **@publisher_db**, bzw..  
  
#### So überwachen Sie Mergeänderungen, die darauf warten, hoch- oder heruntergeladen zu werden  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank, [Sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md). Dadurch wird ein Resultset mit Informationen zu Änderungen zurückgegeben, die darauf warten, auf Abonnenten repliziert zu werden. Um das Resultset auf Änderungen zu beschränken, die nur zu einer Veröffentlichung oder einem Artikel gehören, geben Sie **@publication** bzw. **@article**an.  
  
2.  Führen Sie auf einen Abonnenten für die Abonnementdatenbank [Sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md). Dadurch wird ein Resultset mit Informationen zu Änderungen zurückgegeben, die darauf warten, auf dem Verleger repliziert zu werden. Um das Resultset auf Änderungen zu beschränken, die nur zu einer Veröffentlichung oder einem Artikel gehören, geben Sie **@publication** bzw. **@article**an.  
  
#### So überwachen Sie Merge-Agentsitzungen  
  
1.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md). Dies gibt die Überwachungsinformationen, einschließlich **Session_id**, zu allen Merge-Agent-Sitzungen für alle Abonnements, die diesen Verteiler verwenden. Sie erhalten auch **Session_id** durch Abfragen der [MSmerge_sessions](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) -Systemtabelle.  
  
2.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md). Geben Sie einen **Session_id** Wert aus Schritt 1 für **@session_id**. Dadurch werden ausführliche Überwachungsinformationen zu der Sitzung angezeigt.  
  
3.  Wiederholen Sie Schritt 2 für jede Sitzung, die von Interesse ist.  
  
#### So überwachen Sie Merge-Agentsitzungen für Pullabonnements auf dem Abonnenten  
  
1.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md). Geben Sie für ein bestimmtes Abonnement **@publisher**, **@publication**, und der Name der Veröffentlichungsdatenbank für **@publisher_db**. Dadurch werden Überwachungsinformationen zu den letzten fünf Merge-Agentsitzungen für dieses Abonnement zurückgegeben. Beachten Sie den Wert der **Session_id** für Sitzungen, die von Interesse am Ergebnis festgelegt.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md). Geben Sie einen **Session_id** Wert aus Schritt 1 für **@session_id**. Dadurch werden ausführliche Überwachungsinformationen zu der Sitzung angezeigt.  
  
3.  Wiederholen Sie Schritt 2 für jede Sitzung, die von Interesse ist.  
  
#### So können Sie die Schwellenwertmetriken für die Überwachung für eine Veröffentlichung anzeigen und ändern  
  
1.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md). Dadurch werden Überwachungsschwellenwerte zurückgegeben, die für alle Veröffentlichungen festgelegt wurden, die diesen Verteiler verwenden. Um das Resultset auf Überwachungsschwellenwerte für Veröffentlichungen mit einer veröffentlichten Datenbank oder nur einen Verleger oder eine Publikation gehören zu beschränken, geben **@publisher**, **@publisher_db**, oder **@publication**, bzw.. Beachten Sie den Wert der **Metric_id** für alle Schwellenwerte, die geändert werden müssen. Weitere Informationen finden Sie unter [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
2.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md). Geben Sie bei Bedarf Folgendes an:  
  
    -   Die **Metric_id** Wert, der in Schritt 1 für **@metric_id**.  
  
    -   Einen neuen Wert für die Schwellenwertmetrik für die Überwachung für **@value**.  
  
    -   Einen Wert **1** für **@shouldalert** für eine Warnung, die protokolliert wird, wenn dieser Schwellenwert erreicht wird, oder einen Wert **0** , wenn keine Warnung erforderlich ist.  
  
    -   Der Wert **1** für **@mode** , um die Schwellenwertmetrik für die Überwachung zu aktivieren, oder der Wert **2** , um diese zu deaktivieren.  
  
##  <a name="RMO"></a> Replikationsverwaltungsobjekte (RMO)  
  
#### So überwachen Sie ein Abonnement für eine Mergeveröffentlichung auf dem Abonnenten  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz von der <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> Klasse, und legen die <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> Eigenschaften für das Abonnement, und legen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft, um die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> in Schritt 1 erstellte.  
  
3.  Rufen Sie eine der folgenden Methoden auf, um Informationen zu Merge-Agentsitzungen für dieses Abonnement zurückzugeben:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -Gibt ein Array von <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> -Objekten mit Informationen zu maximal den letzten fünf Sitzungen des Merge-Agent. Beachten Sie die <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> Wert für alle Sitzungen, die von Interesse sind.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -Gibt ein Array von <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> -Objekten mit Informationen zu Merge-Agent-Sitzungen, die während der vergangenen Anzahl von Stunden, die als aufgetreten sind die *Stunden* Parameter (maximal die letzten fünf Sitzungen). Beachten Sie die <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> Wert für alle Sitzungen, die von Interesse sind.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> -Gibt einen <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> -Objekt mit Informationen über die letzte Merge-Agent-Sitzung. Beachten Sie die <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> Wert für diese Sitzung.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt mit Informationen zu maximal die letzten fünf Merge-Agent-Sitzungen, eine in jeder Zeile. Beachten Sie den Wert der **Session_id** Spalte für alle Sitzungen, die von Interesse sind.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> -Gibt einen <xref:System.Data.DataRow> -Objekt mit Informationen zu der letzten Merge-Agent-Sitzung. Beachten Sie den Wert der **Session_id** Spalte für diese Sitzung.  
  
4.  (Optional) Rufen Sie <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> So aktualisieren Sie die Daten für die <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> -Objekt übergeben, als *mss,* oder rufen Sie <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> zum Aktualisieren der Daten in der <xref:System.Data.DataRow> -Objekt übergeben, als *DrRefresh*.  
  
5.  Rufen Sie mithilfe der in Schritt 3 abgerufenen Sitzungs-ID eine der folgenden Methoden auf, um Informationen zu den Details einer bestimmten Sitzung zurückzugeben:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A> -Gibt ein Array von <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> Objekte für die angegebene *SessionId*.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt mit Informationen für den angegebenen *SessionId*.  
  
#### So überwachen Sie die Replikationseigenschaften für alle Veröffentlichungen auf einem Verteiler  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> Klasse.  
  
3.  Festlegen der <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft, um die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> in Schritt 1 erstellt haben.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts.  
  
5.  Führen Sie mindestens eine der folgenden Methoden aus, um Replikationsinformationen für alle Verleger zurückzugeben, die diesen Verteiler verwenden:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu allen Verteilungs-Agents auf diesem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu auf dem Verteiler gespeicherten Fehlern enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu allen Protokolllese-Agents auf dem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu allen Merge-Agents auf dem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu allen anderen Replikations-Agents auf dem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu allen Verlegern auf diesem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das die Verleger zurückgibt, die diesen Verteiler verwenden.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu allen Warteschlangenlese-Agents auf dem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Details zu dem angegebenen Warteschlangenlese-Agent und die Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Sitzungsinformationen zu dem angegebenen Warteschlangenlese-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen über alle Snapshot-Agents auf dem Verteiler enthält.  
  
#### So überwachen Sie die Veröffentlichungseigenschaften für einen bestimmten Verleger auf dem Verteiler  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Abrufen einer <xref:Microsoft.SqlServer.Replication.PublisherMonitor> Objekt in einer der folgenden Methoden.  
  
    -   Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.PublisherMonitor> Klasse. Festlegen der <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> -Eigenschaft für den Verleger, und legen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft, um die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> in Schritt 1 erstellte. Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, ist der Verlegername falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
    -   Aus der <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection> zugegriffen, die von der <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> -Eigenschaft eines vorhandenen <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> Objekt.  
  
3.  Führen Sie mindestens eine der folgenden Methoden aus, um Replikationsinformationen für alle Veröffentlichungen zurückzugeben, die zu diesem Verleger gehören.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Details zu der Snapshot-Agent und die Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Sitzungsinformationen zu dem angegebenen Verteilungs-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das fehlereintragsinformationen zu dem angegebenen Fehler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Details für den angegebenen Protokolllese-Agent und die Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Sitzungsinformationen für den angegebenen Protokolllese-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Details zu der Merge-Agent und die Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das zusätzliche Details zu der Merge-Agent und die Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Sitzungsinformationen für den angegebenen Merge-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das zusätzliche Sitzungsinformationen für den angegebenen Merge-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu allen Veröffentlichungen auf diesem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das zusätzliche Informationen zu allen Veröffentlichungen auf diesem Verteiler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Details zu der Snapshot-Agent und die Sitzung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Sitzungsinformationen für den angegebenen Momentaufnahme-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu allen Abonnements für Veröffentlichungen auf diesem Verteiler enthält.  
  
#### So überwachen Sie die Eigenschaften für eine bestimmte Veröffentlichung auf dem Verteiler  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Abrufen einer <xref:Microsoft.SqlServer.Replication.PublicationMonitor> Objekt in einer der folgenden Methoden.  
  
    -   Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.PublicationMonitor> Klasse. Festlegen der <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, und <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> Eigenschaften für die Veröffentlichung, und legen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> in Schritt 1 erstellt haben. Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
    -   Aus der <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> zugegriffen, die von der <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> -Eigenschaft eines vorhandenen <xref:Microsoft.SqlServer.Replication.PublisherMonitor> Objekt.  
  
3.  Führen Sie mindestens eine der folgenden Methoden aus, um Informationen zu dieser Veröffentlichung zurückzugeben.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Fehlereinträge zu dem angegebenen Fehler enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu der Protokolllese-Agent für diese Veröffentlichung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen über die Schwellenwerte der Warnung enthält für diese Veröffentlichung festgelegt.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu den von dieser Veröffentlichung verwendeten Warteschlangenlese-Agent enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen über den Snapshot-Agent für diese Veröffentlichung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu Abonnements für diese Veröffentlichung enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das zusätzliche Informationen zu Abonnements für diese Veröffentlichung enthält auf der Grundlage des angegebenen <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das latenzzeitinformationen für das angegebene Überwachungstoken enthält.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> -Gibt einen <xref:System.Data.DataSet> -Objekt, das Informationen zu allen in diese Veröffentlichung eingefügten Überwachungstoken enthält.  
  
#### So überwachen Sie Transaktionsbefehle, die darauf warten, auf dem Abonnenten angewendet zu werden  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Abrufen einer <xref:Microsoft.SqlServer.Replication.PublicationMonitor> Objekt in einer der folgenden Methoden.  
  
    -   Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.PublicationMonitor> Klasse. Festlegen der <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, und <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> Eigenschaften für die Veröffentlichung, und legen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> in Schritt 1 erstellt haben. Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
    -   Aus der <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> zugegriffen, die von der <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> -Eigenschaft eines vorhandenen <xref:Microsoft.SqlServer.Replication.PublisherMonitor> Objekt.  
  
3.  Führen Sie die <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> -Methode, die gibt eine <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> Objekt.  
  
4.  Verwenden Sie die Eigenschaften dieses <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> -Objekts bestimmt die geschätzte Anzahl von ausstehenden Befehlen und die Länge der Zeit, die es dauert die Übermittlung dieser Befehle.  
  
#### So legen Sie die Warnungsschwellenwerte für die Überwachung für eine Veröffentlichung fest  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Abrufen einer <xref:Microsoft.SqlServer.Replication.PublicationMonitor> Objekt in einer der folgenden Methoden.  
  
    -   Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.PublicationMonitor> Klasse. Festlegen der <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, und <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> Eigenschaften für die Veröffentlichung, und legen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> in Schritt 1 erstellt haben. Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
    -   Aus der <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> zugegriffen, die von der <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> -Eigenschaft eines vorhandenen <xref:Microsoft.SqlServer.Replication.PublisherMonitor> Objekt.  
  
3.  Führen Sie die <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> Methode. Beachten Sie die aktuellen schwellenwerteinstellungen in der zurückgegebenen <xref:System.Collections.ArrayList> von <xref:Microsoft.SqlServer.Replication.MonitorThreshold> Objekte.  
  
4.  Führen Sie die <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> Methode. Übergeben Sie die folgenden Parameter:  
  
    -   *MetricID* : eine <xref:System.Int32> Wert, der schwellenwertmetrik für die Überwachung aus der folgenden Tabelle darstellt:  
  
        |Wert|Beschreibung|  
        |-----------|-----------------|  
        |1|**Ablauf des** -Monitore für den bevorstehenden Ablauf von Abonnements für transaktionsveröffentlichungen.|  
        |2|**Latenz** -überwacht die Leistung von Abonnements für transaktionsveröffentlichungen.|  
        |4|**Mergeexpiration** -überwacht den bevorstehenden Ablauf von Abonnements für Mergepublikationen.|  
        |5|**Mergeslowrunduration** -überwacht die Dauer von mergesynchronisierungen über Verbindungen mit geringer Bandbreite (DFÜ).|  
        |6|**Mergefastrunduration** -überwacht die Dauer von mergesynchronisierungen über Verbindungen mit hoher Bandbreite (LAN).|  
        |7|**Mergefastrunspeed** -überwacht die synchronisierungsgeschwindigkeit von mergesynchronisierungen über Verbindungen mit hoher Bandbreite (LAN).|  
        |8|**Mergeslowrunspeed** -überwacht die synchronisierungsgeschwindigkeit von mergesynchronisierungen über Verbindungen mit geringer Bandbreite (DFÜ).|  
  
    -   *Aktivieren Sie* - <xref:System.Boolean> -Wert, der angibt, ob die Metrik für die Veröffentlichung aktiviert ist.  
  
    -   *ThresholdValue* -Integer-Wert, der den Schwellenwert festlegt.  
  
    -   *ShouldAlert* -ganze Zahl, die angibt, ob dieser Schwellenwert eine Warnung generieren soll.  
  
  