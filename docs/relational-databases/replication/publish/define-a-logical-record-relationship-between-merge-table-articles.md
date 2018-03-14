---
title: Definieren einer logischen Datensatzbeziehung zwischen Mergetabellenartikeln | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ff847b3a-c6b0-4eaf-b225-2ffc899c5558
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab8e8998836bc9517a65e652b7bb2ba4d9832449
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="define-a-logical-record-relationship-between-merge-table-articles"></a>Definieren einer logische Datensatzbeziehung zwischen Mergetabellenartikeln
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie eine logische Datensatzbeziehung zwischen Mergetabellenartikeln in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekten (RMO) definiert wird.  
  
 Mergereplikation ermöglicht Ihnen, eine Beziehung zwischen verknüpften Zeilen in verschiedenen Tabellen zu definieren. Diese Zeilen können dann während der Synchronisierung als Transaktionseinheit verarbeitet werden. Eine logische Datensatzbeziehung zwischen zwei Artikeln kann unabhängig davon definiert werden, ob sie über eine Joinfilterbeziehung verfügen oder nicht. Weitere Informationen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So definieren Sie eine logische Datensatzbeziehung zwischen Mergetabellenartikeln mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie einen logischen Datensatz hinzufügen, ändern oder löschen, nachdem Abonnements für die Veröffentlichung initialisiert wurden, müssen Sie eine neue Momentaufnahme generieren und alle Abonnements nach vorgenommener Änderung erneut initialisieren. Weitere Informationen zum Ändern von Eigenschaften finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 Zum Definieren logischer Datensätze steht Ihnen das Dialogfeld **Join hinzufügen** zur Verfügung, das über den Assistenten für neue Veröffentlichung und das Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>** verfügbar ist. Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
 Logische Datensätze können nur dann im Dialogfeld **Join hinzufügen** definiert werden, wenn sie auf einen Joinfilter in einer Mergeveröffentlichung angewendet werden und die Veröffentlichung die Anforderungen für die Verwendung vorausberechneter Partitionen erfüllt. Wenn Sie logische Datensätze definieren möchten, die nicht auf Joinfilter angewendet werden, und die Konflikterkennung und -lösung auf der Ebene des logischen Datensatzes festlegen möchten, müssen Sie gespeicherte Prozeduren verwenden.  
  
#### <a name="to-define-a-logical-record-relationship"></a>So definieren Sie eine logische Datensatzbeziehung  
  
1.  Wählen Sie auf der Seite **Tabellenzeilen filtern** des Assistenten für neue Veröffentlichung oder auf der Seite **Zeilen filtern** des Dialogfelds **Veröffentlichungseigenschaften – \<Veröffentlichung>** im Bereich **Gefilterte Tabellen** einen Zeilenfilter aus.  
  
     Logische Datensatzbeziehungen sind mit einem Joinfilter verknüpft, der wiederum einen Zeilenfilter erweitert. Sie müssen daher zuerst einen Zeilenfilter definieren, bevor Sie den Filter mit einem Join erweitern und eine logische Datensatzbeziehung anwenden können. Nach dem Definieren eines Joinfilters können Sie diesen Joinfilter wiederum um einen anderen Joinfilter erweitern. Weitere Informationen zum Definieren von Joinfiltern finden Sie unter [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
2.  Klicken Sie auf **Hinzufügen**und anschließend auf **Join hinzufügen, um den ausgewählten Filter zu erweitern**.  
  
3.  Definieren Sie im Dialogfeld **Join hinzufügen** einen Joinfilter, und aktivieren Sie dann das Kontrollkästchen **Logischer Datensatz**.  
  
4.  Wenn Sie sich im Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>** befinden, klicken Sie auf **OK**, um eine Speicherung vorzunehmen und das Dialogfeld zu schließen.  
  
#### <a name="to-delete-a-logical-record-relationship"></a>So löschen Sie eine logische Datensatzbeziehung  
  
-   Sie können entweder nur die logische Datensatzbeziehung oder die logische Datensatzbeziehung und den zugeordneten Joinfilter gemeinsam löschen.  
  
     So löschen Sie nur die logische Datensatzbeziehung:  
  
    1.  Wählen Sie im Assistenten für neue Veröffentlichung auf der Seite **Zeilen filtern** oder im Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>** auf der Seite **Zeilen filtern** im Bereich **Gefilterte Tabellen** den der logischen Datensatzbeziehung zugeordneten Joinfilter aus, und klicken Sie dann auf **Bearbeiten**.  
  
    2.  Deaktivieren Sie im Dialogfeld **Join bearbeiten** die Option **Logischer Datensatz**.  
  
    3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     So löschen Sie die logische Datensatzbeziehung und den zugeordneten Joinfilter:  
  
    -   Wählen Sie im Assistenten für neue Veröffentlichung auf der Seite **Zeilen filtern** bzw. im Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>** im Bereich **Gefilterte Tabellen** den betreffenden Filter aus, und klicken Sie dann auf **Löschen**. Wenn der Joinfilter, den Sie löschen möchten, mit anderen Joins erweitert ist, werden diese Joins beim Löschen des Filters selbst ebenfalls gelöscht.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können logische Datensatzbeziehungen zwischen Artikeln programmgesteuert mithilfe gespeicherter Replikationsprozeduren angeben.  
  
#### <a name="to-define-a-logical-record-relationship-without-an-associated-join-filter"></a>So definieren Sie eine logische Datensatzbeziehung ohne einen zugeordneten Joinfilter  
  
1.  Wenn die Veröffentlichung irgendwelche gefilterten Artikel enthält, führen Sie [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)aus, und achten Sie im Resultset auf den Wert von **use_partition_groups** .  
  
    -   Wenn der Wert **1**ist, dann werden bereits vorausberechnete Partitionen verwendet.  
  
    -   Ist der in Schritt 1 ermittelte Wert **0**, führen Sie [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie den Wert **use_partition_groups** für **@property** und den Wert **true** für **@value**.  
  
        > [!NOTE]  
        >  Wenn die Veröffentlichung keine vorausberechneten Partitionen unterstützt, dann können keine logischen Datensätze verwendet werden. Weitere Informationen finden Sie unter „Anforderungen für die Verwendung vorausberechneter Partitionen“ im Thema [Optimieren der Leistung parametrisierter Filter mithilfe vorausberechneter Partitionen](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
    -   Ist der Wert NULL, muss der Momentaufnahme-Agent ausgeführt werden, um die Momentaufnahme für die Veröffentlichung zu generieren.  
  
2.  Wenn die Artikel, die den logischen Datensatz umfassen, nicht vorhanden sind, führen Sie [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie eine der folgenden Konflikterkennungs- und -lösungsoptionen für den logischen Datensatz an:  
  
    -   Damit Konflikte, die innerhalb verknüpfter Zeilen im logischen Datensatz auftreten, erkannt und gelöst werden, geben Sie den Wert **true** für **@logical_record_level_conflict_detection** und **@logical_record_level_conflict_resolution**.  
  
    -   Um die Standard-Konflikterkennung und -lösung auf Zeilen- oder Spaltenebene zu verwenden, geben Sie den Wert **false** für **@logical_record_level_conflict_detection** und **@logical_record_level_conflict_resolution**an.  
  
3.  Wiederholen Sie Schritt 2 für jeden Artikel, der den logischen Datensatz umfasst. Sie müssen für jeden Artikel im logischen Datensatz die gleiche Konflikterkennung und Konfliktlösungsoption verwenden. Weitere Informationen finden Sie unter [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)aus. Geben Sie **@publication**an sowie den Namen des ersten an der Beziehung beteiligten Artikels für **@article**, den Namen des zweiten an der Beziehung beteiligten Artikels für **@join_articlename**, einen Namen für die Beziehung für **@filtername**, eine Klausel zur Definition der Beziehung zwischen den beiden Artikeln für **@join_filterclause**, den Jointyp für **@join_unique_key** und einen der folgenden Werte für **@filter_type**:  
  
    -   **2** &ndash; Definiert eine logische Datensatzbeziehung.  
  
    -   **3** &ndash; Definiert eine logische Beziehung mit einem Joinfilter.  
  
    > [!NOTE]  
    >  Wird kein Joinfilter verwendet, ist die Richtung der Beziehung zwischen den beiden Artikeln nicht wichtig.  
  
5.  Wiederholen Sie Schritt 2 für jede weitere logische Datensatzbeziehung in der Veröffentlichung.  
  
#### <a name="to-change-conflict-detection-and-resolution-for-logical-records"></a>So ändern Sie die Konflikterkennung und -lösung für logische Datensätze  
  
1.  So erkennen und lösen Sie Konflikte, die innerhalb verknüpfter Zeilen im logischen Datensatz auftreten:  
  
    -   Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)aus. Geben Sie den Wert **logical_record_level_conflict_detection** für **@property** und den Wert **true** für **@value**. Geben Sie den Wert **1** für **@force_invalidate_snapshot** und **@force_reinit_subscription**.  
  
    -   Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)aus. Geben Sie den Wert **logical_record_level_conflict_resolution** für **@property** und den Wert **true** für **@value**. Geben Sie den Wert **1** für **@force_invalidate_snapshot** und **@force_reinit_subscription**.  
  
2.  So verwenden Sie die Standard-Konflikterkennung und -lösung auf Zeilen- oder Spaltenebene:  
  
    -   Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)aus. Geben Sie den Wert **logical_record_level_conflict_detection** für **@property** und den Wert **false** für **@value**. Geben Sie den Wert **1** für **@force_invalidate_snapshot** und **@force_reinit_subscription**.  
  
    -   Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)aus. Geben Sie den Wert **logical_record_level_conflict_resolution** für **@property** und den Wert **false** für **@value**. Geben Sie den Wert **1** für **@force_invalidate_snapshot** und **@force_reinit_subscription**.  
  
#### <a name="to-remove-a-logical-record-relationship"></a>So entfernen Sie eine logische Datensatzbeziehung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank die folgende Abfrage aus, um alle Informationen über die für die angegebene Veröffentlichung definierten logischen Datensatzbeziehungen zurückzugeben:  
  
     [!code-sql[HowTo#sp_ReturnMergeLogicalRecords](../../../relational-databases/replication/codesnippet/tsql/define-a-logical-record-_1.sql)]  
  
     Achten Sie auf den Namen der zu entfernenden logischen Datensatzbeziehung in der Spalte **filtername** des Resultsets.  
  
    > [!NOTE]  
    >  Diese Abfrage gibt die gleichen Informationen zurück wie [sp_helpmergefilter](../../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md). Diese gespeicherte Systemprozedur ermittelt jedoch nur Informationen über logische Datensatzbeziehungen, die auch Joinfilter sind.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_dropmergefilter](../../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)aus. Geben Sie **@publication**an sowie den Namen eines der an der Beziehung beteiligten Artikel für **@article**und den Namen der Beziehung aus Schritt 1 für **@filtername**.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 Im folgenden Beispiel werden vorausberechnete Partitionen für eine vorhandene Veröffentlichung aktiviert und ein logischer Datensatz erstellt, der die zwei neuen Artikel für die Tabellen `SalesOrderHeader` und `SalesOrderDetail` umfasst.  
  
 [!code-sql[HowTo#sp_AddMergeLogicalRecord](../../../relational-databases/replication/codesnippet/tsql/define-a-logical-record-_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
  
> [!NOTE]  
>  Bei der Mergereplikation können Sie auch angeben, dass Konflikte auf der Ebene logischer Datensätze nachverfolgt und gelöst werden. Diese Optionen können mit RMO jedoch nicht festgelegt werden.  
  
#### <a name="to-define-a-logical-record-relationship-without-an-associated-join-filter"></a>So definieren Sie eine logische Datensatzbeziehung ohne einen zugeordneten Joinfilter  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication> -Klasse, legen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> -Eigenschaft und die <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> -Eigenschaft der Veröffentlichung fest, und legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die in Schritt 1 erstellte Verbindung fest.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften in Schritt 2 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
4.  Wenn die <xref:Microsoft.SqlServer.Replication.MergePublication.PartitionGroupsOption%2A> -Eigenschaft auf <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.False>festgelegt ist, ändern Sie sie in <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.True>.  
  
5.  Wenn die Artikel, die den logischen Datensatz enthalten sollen, nicht vorhanden sind, erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeArticle> -Klasse, und legen Sie die folgenden Eigenschaften fest:  
  
    -   Den Namen des Artikels für <xref:Microsoft.SqlServer.Replication.Article.Name%2A>  
  
    -   Den Namen der Veröffentlichung für <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>  
  
    -   (Optional) Wenn der Artikel horizontal gefiltert wird, geben Sie die Zeilenfilterklausel für die <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> -Eigenschaft an. Verwenden Sie diese Eigenschaft, um einen statischen oder parametrisierten Zeilenfilter anzugeben. Weitere Informationen zu parametrisierten Zeilenfiltern finden Sie unter [Parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
     Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Article.Create%2A> -Methode auf.  
  
7.  Wiederholen Sie die Schritte 5 und 6 für jeden Artikel, der den logischen Datensatz umfasst.  
  
8.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> -Klasse, um die logische Datensatzbeziehung zwischen Artikeln zu definieren. Legen Sie dann die folgenden Eigenschaften fest:  
  
    -   Den Namen des untergeordneten Artikels in der logischen Datensatzbeziehung für die <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.ArticleName%2A> -Eigenschaft  
  
    -   Den Namen des bestehenden übergeordneten Artikels in der logischen Datensatzbeziehung für die <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinArticleName%2A> -Eigenschaft  
  
    -   Einen Namen für die logische Datensatzbeziehung für die <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterName%2A> -Eigenschaft  
  
    -   Einen Ausdruck, der die Beziehung für die <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinFilterClause%2A> -Eigenschaft definiert  
  
    -   Den Wert <xref:Microsoft.SqlServer.Replication.FilterTypes.LogicalRecordLink> für die <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterTypes%2A> -Eigenschaft. Wenn die logische Datensatzbeziehung auch ein Joinfilter ist, geben Sie den Wert <xref:Microsoft.SqlServer.Replication.FilterTypes.JoinFilterAndLogicalRecordLink> für diese Eigenschaft an. Weitere Informationen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
9. Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergeArticle.AddMergeJoinFilter%2A> -Methode für das Objekt auf, das den untergeordneten Artikel in der Beziehung darstellt. Übergeben Sie das <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> -Objekt aus Schritt 8, um die Beziehung zu definieren.  
  
10. Wiederholen Sie die Schritte 8 und 9 für jede weitere logische Datensatzbeziehung in der Veröffentlichung.  
  
###  <a name="PShellExample"></a> Beispiel (RMO)  
 In diesem Beispiel wird ein logischer Datensatz erstellt, der die zwei neuen Artikel für die Tabellen `SalesOrderHeader` und `SalesOrderDetail` umfasst.  
  
 [!code-cs[HowTo#rmo_CreateLogicalRecord](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createlogicalrecord)]  
  
 [!code-vb[HowTo#rmo_vb_CreateLogicalRecord](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createlogicalrecord)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Definieren und Ändern eines statischen Zeilenfilters](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [Optimieren der Leistung parametrisierter Filter mithilfe vorausberechneter Partitionen](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)   
 [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)  
  
  
