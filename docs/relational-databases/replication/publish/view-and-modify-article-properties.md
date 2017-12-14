---
title: "Anzeigen und Ändern von Artikeleigenschaften | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- sp_changearticle
- sp_helparticle
- viewing replication properties
- sp_changemergearticle
- sp_helpmergearticle
- modifying replication properties, articles
- articles [SQL Server replication], modifying
- articles [SQL Server replication], properties
ms.assetid: e71831fa-3d39-4e4a-9706-4d3a497082cc
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 63dedf143ed8bd1ea568ad5d6b749557249f4b29
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="view-and-modify-article-properties"></a>Anzeigen und Ändern von Artikeleigenschaften
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie die Artikeleigenschaften in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (Replication Management Objects, RMO) angezeigt und geändert werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
-   **So zeigen Sie Artikeleigenschaften an oder ändern sie mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Einige Eigenschaften können nicht geändert werden, nachdem eine Veröffentlichung erstellt wurde. Andere Eigenschaften können nicht geändert werden, wenn Abonnements für die Veröffentlichung vorhanden sind. Eigenschaften, die nicht geändert werden können, werden als schreibgeschützt angezeigt.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Nachdem eine Veröffentlichung erstellt wurde, ist für bestimmte Eigenschaftsänderungen eine neue Momentaufnahme erforderlich. Wenn für eine Veröffentlichung Abonnements erstellt wurden, müssen bei bestimmten Änderungen alle Abonnements erneut initialisiert werden. Weitere Informationen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) und [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Sie können die Eigenschaften von Artikeln im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** anzeigen und ändern. Dieses Dialogfeld ist in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]und im Replikationsmonitor verfügbar. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
-   Die Seite **Allgemein** enthält den Namen und die Beschreibung der Veröffentlichung, den Datenbanknamen, den Typ der Veröffentlichung und die Einstellungen für den Abonnementablauf.  
  
-   Die Seite **Artikel** entspricht der Seite **Artikel** des Assistenten für neue Veröffentlichung. Verwenden Sie diese Seite, um Artikel hinzuzufügen und zu löschen und um Eigenschaften sowie die Spaltenfilterung für Artikel zu ändern.  
  
-   Die Seite **Zeilen filtern** entspricht der Seite **Tabellenzeilen filtern** des Assistenten für neue Veröffentlichung. Mithilfe dieser Seite können Sie statische Zeilenfilter für sämtliche Veröffentlichungstypen hinzufügen, bearbeiten und löschen sowie parametrisierte Zeilenfilter und Joinfilter für Mergeveröffentlichungen hinzufügen, bearbeiten und löschen.  
  
-   Auf der Seite **Momentaufnahme** können Sie das Format und den Speicherort der Momentaufnahme angeben und zudem angeben, ob die Momentaufnahme komprimiert werden soll und ob Skripts ausgeführt werden sollen, bevor und nachdem die Momentaufnahme angewendet wird.  
  
-   Die Seite **FTP-Momentaufnahme** (bei Momentaufnahme- und Transaktionsveröffentlichungen sowie Mergeveröffentlichungen für Verleger, auf denen frühere Versionen als SQL Server 2005 ausgeführt werden) bietet die Möglichkeit anzugeben, ob Abonnenten Momentaufnahmedateien über FTP (File Transfer Protocol) herunterladen können.  
  
-   Auf der Seite **FTP-Momentaufnahme und Internet** (bei Mergeveröffentlichungen von Verlegern, auf denen SQL Server 2005 oder höher ausgeführt wird) können Sie angeben, ob Abonnenten Momentaufnahmedateien per FTP herunterladen können und ob Abonnenten Abonnements über HTTPS synchronisieren können.  
  
-   Auf der Seite **Abonnementoptionen** können Sie eine Reihe von Optionen festlegen, die auf alle Abonnements angewendet werden. Die Optionen hängen vom Veröffentlichungstyp ab.  
  
-   Auf der Seite **Veröffentlichungszugriffsliste** können Sie angeben, welche Anmeldungen und Gruppen auf eine Veröffentlichung zugreifen können.  
  
-   Über die Seite **Agentsicherheit** können Sie auf die Einstellungen für die Konten zugreifen, unter denen folgende Agents ausgeführt werden. Sie können außerdem Verbindungen mit den Computern in einer Replikationstopologie herstellen: Momentaufnahme-Agent für alle Veröffentlichungen, Protokolllese-Agent für alle Transaktionsveröffentlichungen und Warteschlangenlese-Agent für Transaktionsveröffentlichungen, die Abonnements mit verzögertem Update über eine Warteschlange zulassen.  
  
-   Auf der Seite **Datenpartitionen** (für Mergeveröffentlichungen von Verlegern, auf denen SQL Server 2005 oder höher ausgeführt wird) können Sie angeben, ob Abonnenten von Veröffentlichungen mit parametrisierten Filtern eine Momentaufnahme anfordern können, wenn diese nicht verfügbar ist. Sie haben zudem die Möglichkeit, Momentaufnahmen für eine oder mehrere Partitionen entweder einmalig oder wiederkehrend gemäß einem Zeitplan zu generieren.  
  
#### <a name="to-view-and-modify-article-properties"></a>So zeigen Sie Artikeleigenschaften an oder ändern sie  
  
1.  Wählen Sie auf der Seite **Artikel** bzw. im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** einen Artikel aus, und klicken Sie dann auf **Artikeleigenschaften**.  
  
2.  Wählen Sie aus, auf welche Artikel die Eigenschaftsänderungen angewendet werden sollen:  
  
    -   Klicken Sie auf **Eigenschaften des hervorgehobenen \<ObjectType>-Artikels festlegen**, um das Dialogfeld **Artikeleigenschaften - \<ObjectName>** zu starten. Die in diesem Dialogfeld vorgenommenen Änderungen werden nur auf das Objekt angewendet, das im Objektbereich auf der Seite **Artikel** markiert ist.  
  
    -   Klicken Sie auf **Eigenschaften aller \<ObjectType>-Artikel** festlegen, um das Dialogfeld **Eigenschaften für alle \<ObjectType>-Artikel** zu starten. Die in diesem Dialogfeld vorgenommenen Änderungen werden auf alle Objekte dieses Typs angewendet, die im Objektbereich auf der Seite **Artikel** vorhanden sind, einschließlich jener Objekte, die noch nicht für die Veröffentlichung ausgewählt wurden.  
  
        > [!NOTE]  
        >  Durch die Änderungen im Dialogfeld **Eigenschaften für alle \<ObjectType>-Artikel** werden alle zuvor im Dialogfeld **Artikeleigenschaften - \<ObjectName>** vorgenommenen Änderungen überschrieben. Wenn Sie beispielsweise sowohl mehrere Standardwerte für alle Artikel eines Objekttyps als auch bestimmte Eigenschaften für einzelne Objekte festlegen möchten, legen Sie zuerst die Standardwerte für alle Artikel fest. Legen Sie anschließend die Eigenschaften für die einzelnen Objekte fest.  
  
3.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
4.  Klicken Sie im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Artikel können mithilfe gespeicherter Replikationsprozeduren programmgesteuert geändert und ihre Eigenschaften zurückgegeben werden. Die verwendeten gespeicherten Prozeduren hängen vom Typ der Veröffentlichung ab, zu der der Artikel gehört.  
  
#### <a name="to-view-the-properties-of-an-article-belonging-to-a-snapshot-or-transactional-publication"></a>So zeigen Sie die Eigenschaften eines Artikels an, der zu einer Momentaufnahme- oder einer Transaktionsveröffentlichung gehört  
  
1.  Führen Sie [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)aus, und geben Sie dabei den Namen der Veröffentlichung für den **@publication** -Parameter und den Namen des Artikels für den **@article** -Parameter an. Wenn Sie **@article**nicht angeben, werden Informationen zu allen Artikeln in der Veröffentlichung zurückgegeben.  
  
2.  Führen Sie [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) aus, damit die Tabellenartikel alle in der Basistabelle verfügbaren Spalten auflisten.  
  
#### <a name="to-modify-the-properties-of-an-article-belonging-to-a-snapshot-or-transactional-publication"></a>So ändern Sie die Eigenschaften eines Artikels, der zu einer Momentaufnahme- oder einer Transaktionsveröffentlichung gehört  
  
1.  Führen Sie [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)aus, und geben Sie dabei die zu ändernde Artikeleigenschaft im **@property** -Parameter und den neuen Wert dieser Eigenschaft im **@value** -Parameter an.  
  
    > [!NOTE]  
    >  Wenn die Änderung das Generieren einer neuen Momentaufnahme erfordert, müssen Sie zudem den Wert **1** für **@force_invalidate_snapshot**angeben, und wenn die Änderung das erneute Initialisieren der Abonnenten erfordert, müssen Sie auch den Wert **1** für **@force_reinit_subscription**. Weitere Informationen über Eigenschaften, die bei Änderung eine neue Momentaufnahme oder eine erneute Initialisierung erfordern, finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
#### <a name="to-view-the-properties-of-an-article-belonging-to-a-merge-publication"></a>So zeigen Sie die Eigenschaften eines Artikels an, der zu einer Mergeveröffentlichung gehört  
  
1.  Führen Sie [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)aus, und geben Sie dabei den Namen der Veröffentlichung für den **@publication** -Parameter und den Namen des Artikels für den **@article** -Parameter an. Wenn Sie diese Parameter nicht angeben, werden Informationen zu allen Artikeln einer Veröffentlichung oder des Verlegers zurückgegeben.  
  
2.  Führen Sie [sp_helpmergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-helpmergearticlecolumn-transact-sql.md) aus, damit die Tabellenartikel alle in der Basistabelle verfügbaren Spalten auflisten.  
  
#### <a name="to-modify-the-properties-of-an-article-belonging-to-a-merge-publication"></a>So ändern Sie die Eigenschaften eines Artikels, der zu einer Mergeveröffentlichung gehört  
  
1.  Führen Sie [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)aus, und geben Sie dabei die zu ändernde Artikeleigenschaft im **@property** -Parameter und den neuen Wert dieser Eigenschaft im **@value** -Parameter an.  
  
    > [!NOTE]  
    >  Wenn die Änderung das Generieren einer neuen Momentaufnahme erfordert, müssen Sie zudem den Wert **1** für **@force_invalidate_snapshot**angeben, und wenn die Änderung das erneute Initialisieren der Abonnenten erfordert, müssen Sie auch den Wert **1** für **@force_reinit_subscription**. Weitere Informationen über Eigenschaften, die bei Änderung eine neue Momentaufnahme oder eine erneute Initialisierung erfordern, finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel für eine Transaktionsreplikation werden die Eigenschaften des veröffentlichten Artikels zurückgegeben.  
  
 [!code-sql[HowTo#sp_helptranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_1.sql)]  
  
 In diesem Beispiel für eine Transaktionsreplikation werden die Schemaoptionen für den veröffentlichten Artikel geändert.  
  
 [!code-sql[HowTo#sp_changetranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_2.sql)]  
  
 In diesem Beispiel für eine Mergereplikation werden die Eigenschaften des veröffentlichten Artikels zurückgegeben.  
  
 [!code-sql[HowTo#sp_helpmergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_3.sql)]  
  
 In diesem Mergereplikationsbeispiel werden die Konflikterkennungseinstellungen für einen veröffentlichten Artikel geändert.  
  
 [!code-sql[HowTo#sp_changemergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_4.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Artikel ändern und mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert auf ihre Eigenschaften zugreifen. Welche RMO-Klassen Sie zum Anzeigen oder Ändern von Artikeleigenschaften verwenden, hängt vom Typ der Veröffentlichung ab, zu der der Artikel gehört.  
  
#### <a name="to-view-or-modify-properties-of-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>So zeigen Sie die Eigenschaften eines Artikels an, der zu einer Momentaufnahme- oder einer Transaktionsveröffentlichung gehört, oder ändern sie  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransArticle> -Klasse.  
  
3.  Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>und <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> fest.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft fest.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, wurden entweder die Artikeleigenschaften in Schritt 3 falsch definiert, oder der Artikel ist nicht vorhanden.  
  
6.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eine der definierbaren <xref:Microsoft.SqlServer.Replication.TransArticle> -Eigenschaften fest.  
  
7.  (Optional) Wenn Sie den Wert **true** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>angegeben haben, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> -Methode auf, um die Änderungen auf dem Server einzutragen. Wenn Sie den Wert **false** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (die Standardeinstellung) angegeben haben, werden die Änderungen sofort an den Server gesendet.  
  
#### <a name="to-view-or-modify-properties-of-an-article-that-belongs-to-a-merge-publication"></a>So zeigen Sie die Eigenschaften eines Artikels an, der zu einer Mergeveröffentlichung gehört, oder ändern sie  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeArticle> -Klasse.  
  
3.  Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>und <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> fest.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft fest.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, wurden entweder die Artikeleigenschaften in Schritt 3 falsch definiert, oder der Artikel ist nicht vorhanden.  
  
6.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eine der definierbaren <xref:Microsoft.SqlServer.Replication.MergeArticle> -Eigenschaften fest.  
  
7.  (Optional) Wenn Sie den Wert **true** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>angegeben haben, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> -Methode auf, um die Änderungen auf dem Server einzutragen. Wenn Sie den Wert **false** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (die Standardeinstellung) angegeben haben, werden die Änderungen sofort an den Server gesendet.  
  
###  <a name="PShellExample"></a> Beispiel (RMO)  
 In diesem Beispiel wird ein Mergeartikel geändert, um den vom Artikel verwendeten Geschäftslogikhandler anzugeben.  
  
 [!code-cs[HowTo#rmo_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren eines Geschäftslogikhandlers für einen Mergeartikel](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
