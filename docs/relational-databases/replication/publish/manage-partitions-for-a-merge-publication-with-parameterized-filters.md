---
title: "Verwalten von Partitionen für eine Mergeveröffentlichung mit parametrisierten Filtern | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitions [SQL Server replication]
- merge replication partitions [SQL Server replication], SQL Server Management Studio
- parameterized filters [SQL Server replication], partition management
ms.assetid: fb5566fe-58c5-48f7-8464-814ea78e6221
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5718198b2cbfc99a1658a703199bb943fcd73aeb
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="manage-partitions-for-a-merge-publication-with-parameterized-filters"></a>Verwalten von Partitionen für eine Mergeveröffentlichung mit parametrisierten Filtern
  In diesem Thema wird beschrieben, wie Partitionen für eine Mergeveröffentlichung mit parametrisierten Filtern in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekten (RMO) verwaltet werden. Mithilfe parametrisierter Zeilenfilter können nicht überlappende Partitionen generiert werden. Diese Partitionen können eingeschränkt werden, sodass nur ein Abonnement eine bestimmte Partition erhält. In solchen Fällen führt eine große Anzahl von Abonnenten zu einer großen Anzahl von Partitionen, was wiederum eine gleiche Anzahl von partitionierten Momentaufnahmen erforderlich macht. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
-   **So verwalten Sie Partitionen für eine Mergeveröffentlichung mit parametrisierten Filtern mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wenn Sie, wie empfohlen, ein Skript für eine Replikationstopologie erstellen, enthalten die Veröffentlichungsskripts die Aufrufe der gespeicherten Prozedur zum Erstellen von Datenpartitionen. Die Skripts stellen einen Verweis für die erstellten Partitionen bereit und ermöglichen das erneute Erstellen von Partitionen, falls dies erforderlich wird. Weitere Informationen finden Sie unter [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
-   Wenn eine Veröffentlichung parametrisierte Filter aufweist, die Abonnements mit nicht überlappenden Partitionen ergeben, und ein bestimmtes Abonnement verloren gegangen ist und neu erstellt werden muss, müssen Sie wie folgt vorgehen: Entfernen Sie die Partition, die abonniert wurde, erstellen Sie das Abonnement neu, und erstellen Sie dann die Partition neu. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md). Durch Replikation werden Erstellungsskripts für vorhandene Abonnentenpartitionen generiert, wenn ein Erstellungsskript für eine Veröffentlichung generiert wird. Weitere Informationen finden Sie unter [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Zum Verwalten von Partitionen steht Ihnen die Seite **Datenpartitionen** des Dialogfelds **Veröffentlichungseigenschaften – \<Veröffentlichung>** zur Verfügung. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Auf dieser Seite können Sie Partitionen erstellen und löschen, Abonnenten ermöglichen, die Momentaufnahmegenerierung und -bereitstellung zu initialisieren, Momentaufnahmen für eine oder mehrere Partitionen generieren und einen Cleanup von Momentaufnahmen ausführen.  
  
#### <a name="to-create-a-partition"></a>So erstellen Sie eine Partition  
  
1.  Klicken Sie auf der Seite **Datenpartitionen** des Dialogfelds **Veröffentlichungseigenschaften – \<Veröffentlichung>** auf **Hinzufügen**.  
  
2.  Geben Sie im Dialogfeld **Datenpartition hinzufügen** einen Wert für den **HOST_NAME()** - und/oder **SUSER_SNAME()** -Parameter für die Partition ein, die Sie erstellen möchten.  
  
3.  Optional können Sie einen Zeitplan für das Aktualisieren von Momentaufnahmen angeben:  
  
    1.  Aktivieren Sie die Option **Ausführung des Momentaufnahme-Agents für diese Partition zu folgenden Zeitpunkten planen**.  
  
    2.  Akzeptieren Sie den Standardzeitplan für die Aktualisierung von Momentaufnahmen, oder klicken Sie auf **Ändern** , um einen anderen Zeitplan anzugeben.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-partition"></a>So löschen Sie eine Partition  
  
1.  Wählen Sie in der Tabelle auf der Seite **Datenpartitionen** die gewünschte Partition aus.  
  
2.  Klicken Sie auf **Löschen**.  
  
#### <a name="to-allow-subscribers-to-initiate-snapshot-generation-and-delivery"></a>So lassen Sie zu, dass Abonnenten die Momentaufnahmegenerierung und -übermittlung starten  
  
1.  Aktivieren Sie auf der Seite **Datenpartitionen** die Option **Bei Bedarf automatisch eine Partition definieren und eine Momentaufnahme generieren, wenn ein neuer Abonnent zu synchronisieren versucht**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-generate-a-snapshot-for-a-partition"></a>So generieren Sie eine Momentaufnahme für eine Partition  
  
1.  Wählen Sie in der Tabelle auf der Seite **Datenpartitionen** die gewünschte Partition aus.  
  
2.  Klicken Sie auf **Die ausgewählten Momentaufnahmen jetzt generieren**.  
  
#### <a name="to-clean-up-a-snapshot-for-a-partition"></a>So führen Sie einen Cleanup einer Momentaufnahme für eine Partition aus  
  
1.  Wählen Sie in der Tabelle auf der Seite **Datenpartitionen** die gewünschte Partition aus.  
  
2.  Klicken Sie auf **Cleanup der vorhandenen Momentaufnahmen ausführen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können die vorhandenen Partitionen mithilfe gespeicherter Replikationsprozeduren programmgesteuert aufzählen, um eine Veröffentlichung mit parametrisierten Filtern besser verwalten zu können. Zudem können Sie Partitionen erstellen und vorhandene Partitionen löschen. Die folgenden Informationen zu vorhandenen Partitionen können abgerufen werden:  
  
-   Filterung einer Partition (mit [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) oder [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md)).  
  
-   Der Name des Auftrags, der eine partitionierte Momentaufnahme generiert.  
  
-   Das Datum der letzten Ausführung eines Auftrags für eine partitionierte Momentaufnahme.  
  
 Während der zweite Teil der zweiteiligen Momentaufnahme bedarfsgerecht generiert werden kann, wenn ein neues Abonnement initialisiert wird, können Sie mithilfe der nachfolgenden Anweisungen die Generierung dieser Momentaufnahme steuern und die Momentaufnahme im Voraus zu einem beliebigen Zeitpunkt erstellen. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
#### <a name="to-view-information-on-existing-partitions"></a>So zeigen Sie Informationen zu vorhandenen Partitionen an  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_helpmergepartition &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md) aus. Geben Sie den Namen der Veröffentlichung für **@publication**. (Optional) Geben Sie **@suser_sname** oder **@host_name** an, damit nur Informationen basierend auf einem einzelnen Filterkriterium zurückgegeben werden.  
  
#### <a name="to-define-a-new-partition-and-generate-a-new-partitioned-snapshot"></a>So können Sie eine neue Partition definieren und eine neue partitionierte Momentaufnahme generieren  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergepartition &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md) aus. Geben Sie den Namen der Veröffentlichung für **@publication**und den parametrisierten Wert an, der die Partition für eines der folgenden Elemente definiert:  
  
    -   **@suser_sname** – wenn der parametrisierte Filter durch den von [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) zurückgegebenen Wert definiert wird.  
  
    -   **@host_name** – wenn der parametrisierte Filter durch den von [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md) zurückgegebenen Wert definiert wird.  
  
2.  Erstellen und initialisieren Sie die parametrisierte Momentaufnahme für diese neue Partition. Weitere Informationen finden Sie unter [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
#### <a name="to-delete-a-partition"></a>So löschen Sie eine Partition  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_dropmergepartition &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md) aus. Geben Sie den Namen der Veröffentlichung für **@publication** und den parametrisierten Wert an, der die Partition für eines der folgenden Elemente definiert:  
  
    -   **@suser_sname** – wenn der parametrisierte Filter durch den von [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) zurückgegebenen Wert definiert wird.  
  
    -   **@host_name** – wenn der parametrisierte Filter durch den von [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md) zurückgegebenen Wert definiert wird.  
  
     Dadurch werden zudem der Momentaufnahmeauftrag und alle Momentaufnahmedateien für die Partition entfernt.  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Um eine Veröffentlichung mit parametrisierten Filtern besser verwalten zu können, können Sie programmgesteuert neue Abonnentenpartitionen erstellen, die vorhandenen Abonnentenpartitionen aufzählen und Abonnentenpartitionen mithilfe von Replikationsverwaltungsobjekten (RMO) entfernen. Informationen zum Erstellen von Abonnentenpartitionen finden Sie unter [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). Die folgenden Informationen zu vorhandenen Partitionen können abgerufen werden:  
  
-   Der Wert und die Filterfunktion, auf dem bzw. der die Partition basiert.  
  
-   Der Name des Auftrags, der eine parametrisierte Momentaufnahme für den Abonnenten generiert.  
  
-   Das Datum der letzten Ausführung eines Auftrags für eine parametrisierte Momentaufnahme.  
  
#### <a name="to-view-information-on-existing-partitions"></a>So zeigen Sie Informationen zu vorhandenen Partitionen an  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication>-Klasse. Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>- und <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>-Eigenschaften für die Veröffentlichung und legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf die in Schritt 1 erstellte <xref:Microsoft.SqlServer.Management.Common.ServerConnection> fest.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften in Schritt 2 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A>-Methode auf, und übergeben Sie das Ergebnis an ein Array von <xref:Microsoft.SqlServer.Replication.MergePartition>-Objekten.  
  
5.  Rufen Sie für jedes <xref:Microsoft.SqlServer.Replication.MergePartition>-Objekt im Array alle gewünschten Eigenschaften ab.  
  
#### <a name="to-delete-existing-partitions"></a>So löschen Sie vorhandene Partitionen  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication>-Klasse. Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>- und <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>-Eigenschaften für die Veröffentlichung und legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf die in Schritt 1 erstellte <xref:Microsoft.SqlServer.Management.Common.ServerConnection> fest.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften in Schritt 2 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A>-Methode auf, und übergeben Sie das Ergebnis an ein Array von <xref:Microsoft.SqlServer.Replication.MergePartition>-Objekten.  
  
5.  Bestimmen Sie für jedes <xref:Microsoft.SqlServer.Replication.MergePartition>-Objekt im Array, ob die Partition gelöscht werden soll. Diese Entscheidung basiert normalerweise auf dem Wert der <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A>- oder der <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A>-Eigenschaft.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergePublication.RemoveMergePartition%2A>-Methode auf dem <xref:Microsoft.SqlServer.Replication.MergePublication>-Objekt aus Schritt 2 auf. Übergeben Sie das <xref:Microsoft.SqlServer.Replication.MergePartition>-Objekt aus Schritt 5.  
  
7.  Wiederholen Sie Schritt 6 für jede zu löschende Partition.  
  
## <a name="see-also"></a>Siehe auch  
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
