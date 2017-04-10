---
title: "Anzeigen und &#196;ndern von Artikeleigenschaften | Microsoft Docs"
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
  - "sp_changearticle"
  - "sp_helparticle"
  - "Anzeigen von Replikationseigenschaften"
  - "sp_changemergearticle"
  - "sp_helpmergearticle"
  - "Ändern von Replikationseigenschaften, Artikel"
  - "Artikel [SQL Server-Replikation], ändern"
  - "Artikel [SQL Server-Replikation], Eigenschaften"
ms.assetid: e71831fa-3d39-4e4a-9706-4d3a497082cc
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Anzeigen und &#196;ndern von Artikeleigenschaften
  In diesem Thema wird beschrieben, wie die Artikeleigenschaften in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) angezeigt und geändert werden.  
  
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
  
-   Nachdem eine Veröffentlichung erstellt wurde, ist für bestimmte Eigenschaftsänderungen eine neue Momentaufnahme erforderlich. Wenn für eine Veröffentlichung Abonnements erstellt wurden, müssen bei bestimmten Änderungen alle Abonnements erneut initialisiert werden. Weitere Informationen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) und [Hinzufügen und löschen Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Anzeigen und Ändern von Artikeleigenschaften in die **Veröffentlichungseigenschaften - \< Veröffentlichung>** verfügbar im Dialogfeld [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] und Replikationsmonitor. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
-   Die Seite **Allgemein** enthält den Namen und die Beschreibung der Veröffentlichung, den Datenbanknamen, den Typ der Veröffentlichung und die Einstellungen für den Abonnementablauf.  
  
-   Die Seite **Artikel** entspricht der Seite **Artikel** des Assistenten für neue Veröffentlichung. Verwenden Sie diese Seite, um Artikel hinzuzufügen und zu löschen und um Eigenschaften sowie die Spaltenfilterung für Artikel zu ändern.  
  
-   Die Seite **Zeilen filtern** entspricht der Seite **Tabellenzeilen filtern** des Assistenten für neue Veröffentlichung. Mithilfe dieser Seite können Sie statische Zeilenfilter für sämtliche Veröffentlichungstypen hinzufügen, bearbeiten und löschen sowie parametrisierte Zeilenfilter und Joinfilter für Mergeveröffentlichungen hinzufügen, bearbeiten und löschen.  
  
-   Auf der Seite **Momentaufnahme** können Sie das Format und den Speicherort der Momentaufnahme angeben und zudem angeben, ob die Momentaufnahme komprimiert werden soll und ob Skripts ausgeführt werden sollen, bevor und nachdem die Momentaufnahme angewendet wird.  
  
-   Die **FTP-Momentaufnahme** auf der Seite (für Momentaufnahme- und transaktionsveröffentlichungen und mergeveröffentlichungen für Verleger, auf denen Versionen vor SQL Server 2005) können Sie angeben, ob Abonnenten momentaufnahmedateien über FTP File Transfer Protocol () herunterladen können.  
  
-   Die **FTP-Momentaufnahme und Internet** (für mergeveröffentlichungen von Verlegern mit SQLServer 2005 oder höher) auf der Seite können Sie angeben, ob Abonnenten momentaufnahmedateien per FTP herunterladen können und ob Abonnenten Abonnements über HTTPS synchronisieren können.  
  
-   Auf der Seite **Abonnementoptionen** können Sie eine Reihe von Optionen festlegen, die auf alle Abonnements angewendet werden. Die Optionen hängen vom Veröffentlichungstyp ab.  
  
-   Auf der Seite **Veröffentlichungszugriffsliste** können Sie angeben, welche Anmeldungen und Gruppen auf eine Veröffentlichung zugreifen können.  
  
-   Über die Seite **Agentsicherheit** können Sie auf die Einstellungen für die Konten zugreifen, unter denen folgende Agents ausgeführt werden. Sie können außerdem Verbindungen mit den Computern in einer Replikationstopologie herstellen: Momentaufnahme-Agent für alle Veröffentlichungen, Protokolllese-Agent für alle Transaktionsveröffentlichungen und Warteschlangenlese-Agent für Transaktionsveröffentlichungen, die Abonnements mit verzögertem Update über eine Warteschlange zulassen.  
  
-   Die **Datenpartitionen** (für mergeveröffentlichungen von Verlegern mit SQLServer 2005 oder höher) auf der Seite können Sie angeben, ob Abonnenten von Veröffentlichungen mit parametrisierten Filtern eine Momentaufnahme anfordern können, wenn eine nicht verfügbar ist. Sie haben zudem die Möglichkeit, Momentaufnahmen für eine oder mehrere Partitionen entweder einmalig oder wiederkehrend gemäß einem Zeitplan zu generieren.  
  
#### So zeigen Sie Artikeleigenschaften an oder ändern sie  
  
1.  Auf der **Artikel** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld Wählen Sie einen Artikel, und klicken Sie dann auf **Artikeleigenschaften**.  
  
2.  Wählen Sie aus, auf welche Artikel die Eigenschaftsänderungen angewendet werden sollen:  
  
    -   Klicken Sie auf **Eigenschaften des hervorgehobenen \< ObjectType> Artikel** zum Starten der **Artikeleigenschaften - \< ObjectName>** das Dialogfeld in diesem Dialogfeld vorgenommene Änderungen gelten nur für das Objekt, das im Objektbereich hervorgehoben ist die **Artikel** Seite.  
  
    -   Klicken Sie auf **Eigenschaften aller \< ObjectType> Artikel**, um die **Eigenschaften für alle \< ObjectType> Artikel** das Dialogfeld in diesem Dialogfeld vorgenommene Änderungen gelten für alle Objekte dieses Typs im Objektbereich auf der **Artikel** Seite, einschließlich Objekten, die noch nicht für die Veröffentlichung ausgewählt.  
  
        > [!NOTE]  
        >  Eigenschaftenänderungen in der **Eigenschaften für alle \< ObjectType> Artikel** Überschreiben Sie alle zuvor im Dialogfeld die **Artikeleigenschaften - \< ObjectName>** (Dialogfeld). Wenn Sie beispielsweise sowohl mehrere Standardwerte für alle Artikel eines Objekttyps als auch bestimmte Eigenschaften für einzelne Objekte festlegen möchten, legen Sie zuerst die Standardwerte für alle Artikel fest. Legen Sie anschließend die Eigenschaften für die einzelnen Objekte fest.  
  
3.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
4.  Klicken Sie auf **OK** auf die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Artikel können mithilfe gespeicherter Replikationsprozeduren programmgesteuert geändert und ihre Eigenschaften zurückgegeben werden. Die verwendeten gespeicherten Prozeduren hängen vom Typ der Veröffentlichung ab, zu der der Artikel gehört.  
  
#### So zeigen Sie die Eigenschaften eines Artikels an, der zu einer Momentaufnahme- oder einer Transaktionsveröffentlichung gehört  
  
1.  Führen Sie [Sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md), gibt den Namen der Veröffentlichung für die **@publication** -Parameter und den Namen des Artikels für die **@article** Parameter. Wenn Sie **@article**nicht angeben, werden Informationen zu allen Artikeln in der Veröffentlichung zurückgegeben.  
  
2.  Führen Sie [Sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) für Tabellenartikel alle in der Basistabelle verfügbaren Spalten auflisten.  
  
#### So ändern Sie die Eigenschaften eines Artikels, der zu einer Momentaufnahme- oder einer Transaktionsveröffentlichung gehört  
  
1.  Führen Sie [Sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md), Angeben der Artikeleigenschaft die **@property** Parameter und den neuen Wert dieser Eigenschaft in der **@value** Parameter.  
  
    > [!NOTE]  
    >  Wenn die Änderung die Generierung einer neuen Momentaufnahme erfordert, müssen Sie auch angeben, auf den Wert **1** für **@force_invalidate_snapshot**, und wenn die Änderung erfordert, dass Abonnenten erneut initialisiert werden, müssen Sie auch angeben, auf den Wert **1** für **@force_reinit_subscription**. Weitere Informationen zu den Eigenschaften, die bei Änderung erfordern eine neue Momentaufnahme oder eine erneute Initialisierung, finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
#### So zeigen Sie die Eigenschaften eines Artikels an, der zu einer Mergeveröffentlichung gehört  
  
1.  Führen Sie [Sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md), gibt den Namen der Veröffentlichung für die **@publication** -Parameter und den Namen des Artikels für die **@article** Parameter. Wenn Sie diese Parameter nicht angeben, werden Informationen zu allen Artikeln einer Veröffentlichung oder des Verlegers zurückgegeben.  
  
2.  Führen Sie [Sp_helpmergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-helpmergearticlecolumn-transact-sql.md) für Tabellenartikel alle in der Basistabelle verfügbaren Spalten auflisten.  
  
#### So ändern Sie die Eigenschaften eines Artikels, der zu einer Mergeveröffentlichung gehört  
  
1.  Führen Sie [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), Angeben der Artikeleigenschaft die **@property** Parameter und den neuen Wert dieser Eigenschaft in der **@value** Parameter.  
  
    > [!NOTE]  
    >  Wenn die Änderung die Generierung einer neuen Momentaufnahme erfordert, müssen Sie auch angeben, auf den Wert **1** für **@force_invalidate_snapshot**, und wenn die Änderung erfordert, dass Abonnenten erneut initialisiert werden, müssen Sie auch angeben, auf den Wert **1** für **@force_reinit_subscription**. Weitere Informationen zu den Eigenschaften, die bei Änderung erfordern eine neue Momentaufnahme oder eine erneute Initialisierung, finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
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
  
#### So zeigen Sie die Eigenschaften eines Artikels an, der zu einer Momentaufnahme- oder einer Transaktionsveröffentlichung gehört, oder ändern sie  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransArticle> Klasse.  
  
3.  Legen Sie den <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, und <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Eigenschaften.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, wurden entweder die Artikeleigenschaften in Schritt 3 falsch definiert, oder der Artikel ist nicht vorhanden.  
  
6.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eines der <xref:Microsoft.SqlServer.Replication.TransArticle> Eigenschaften festgelegt werden können.  
  
7.  (Optional) Wenn Sie einen Wert von angegeben **true** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode, um die Änderungen auf dem Server. Wenn Sie einen Wert von angegeben **false** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (Standard), Änderungen werden an den Server sofort gesendet.  
  
#### So zeigen Sie die Eigenschaften eines Artikels an, der zu einer Mergeveröffentlichung gehört, oder ändern sie  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeArticle> Klasse.  
  
3.  Legen Sie den <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, und <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Eigenschaften.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, wurden entweder die Artikeleigenschaften in Schritt 3 falsch definiert, oder der Artikel ist nicht vorhanden.  
  
6.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eines der <xref:Microsoft.SqlServer.Replication.MergeArticle> Eigenschaften festgelegt werden können.  
  
7.  (Optional) Wenn Sie einen Wert von angegeben **true** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode, um die Änderungen auf dem Server. Wenn Sie einen Wert von angegeben **false** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (Standard), Änderungen werden an den Server sofort gesendet.  
  
###  <a name="PShellExample"></a> Beispiel (RMO)  
 In diesem Beispiel wird ein Mergeartikel geändert, um den vom Artikel verwendeten Geschäftslogikhandler anzugeben.  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## Siehe auch  
 [Implementieren eines Geschäftslogikhandlers für einen Mergeartikel](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  