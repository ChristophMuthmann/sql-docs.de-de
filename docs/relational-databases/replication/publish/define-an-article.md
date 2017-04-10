---
title: "Definieren eines Artikels | Microsoft Docs"
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
  - "Artikel [SQL Server-Replikation], definieren"
  - "sp_addmergearticle"
  - "Hinzufügen von Artikeln"
  - "sp_addarticle"
  - "Artikel [SQL Server-Replikation], hinzufügen"
ms.assetid: 220584d8-b291-43ae-b036-fbba3cc07a2e
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Definieren eines Artikels
  In diesem Thema wird beschrieben, wie ein Artikel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) definiert wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So definieren Sie einen Artikel mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Artikelnamen dürfen keines der folgenden Zeichen enthalten: % , * , [ , ] , | , : , " , ? , ' , \ , / , \< , >. Wenn Objekte in der Datenbank eines dieser Zeichen enthalten und Sie die Objekte replizieren möchten, müssen Sie einen Artikelnamen angeben, der sich von dem Objektnamen unterscheidet.  
  
##  <a name="Security"></a> Sicherheit  
 Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen speichern müssen, verwenden Sie die [Kryptografiedienste](http://go.microsoft.com/fwlink/?LinkId=34733) von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows .NET Framework.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Mit dem Assistenten für neue Veröffentlichung erstellen Sie Veröffentlichungen und definieren Artikel. Nachdem eine Veröffentlichung erstellt wurde, anzeigen und Ändern von Veröffentlichungseigenschaften in die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Informationen zum Erstellen einer Veröffentlichung aus einer Oracle-Datenbank finden Sie unter [Erstellen einer Veröffentlichung aus einer Oracle-Datenbank](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
#### So erstellen Sie eine Veröffentlichung und definieren Artikel  
  
1.  Stellen Sie in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie die **Replikation** Ordner, und klicken Sie dann mit der rechten Maustaste die **lokale Publikationen** Ordner.  
  
3.  Klicken Sie auf **Neue Veröffentlichung**.  
  
4.  Folgen Sie den Anweisungen auf den Seiten des Assistenten für neue Veröffentlichung, um folgende Vorgänge auszuführen:  
  
    -   Angeben eines Verteilers, falls die Verteilung auf dem Server nicht konfiguriert wurde. Weitere Informationen zum Konfigurieren der Verteilung finden Sie unter [Verleger- und Verteilereigenschaften](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
         Wenn Sie an der **Verteiler** Seite, die der Verleger als sein eigener Verteiler (lokaler Verteiler) fungiert, und der Server ist nicht konfiguriert, als Verteiler, Assistenten für neue Veröffentlichung der Server konfiguriert werden kann. Auf der Seite **Momentaufnahmeordner** geben Sie einen Standardmomentaufnahmeordner für den Verteiler an. Der Momentaufnahmeordner ist lediglich ein von Ihnen freigegebenes Verzeichnis. Agents, die aus diesem Ordner lesen bzw. in den Ordner schreiben, benötigen ausreichende Zugriffsberechtigungen. Weitere Informationen zur Absicherung des Ordners finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
         Wenn Sie angeben, dass ein anderer Server als Verteiler fungieren soll, müssen Sie auf der Seite **Administratorkennwort** ein Kennwort für Verbindungen eingeben, die zwischen dem Verleger und dem Verteiler hergestellt werden. Dieses Kennwort muss mit dem Kennwort übereinstimmen, dass bei der Aktivierung des Verlegers auf dem Remoteverteiler angegeben wurde.  
  
         Weitere Informationen finden Sie unter [Verteilung konfigurieren](../../../relational-databases/replication/configure-distribution.md).  
  
    -   Auswählen einer Veröffentlichungsdatenbank.  
  
    -   Auswählen eines Veröffentlichungstyps. Weitere Informationen finden Sie unter [Replikationstypen](../../../relational-databases/replication/types-of-replication.md).  
  
    -   Angeben von Daten und Datenbankobjekten, die veröffentlicht werden sollen. Optional können Sie Spalten aus Tabellenartikeln filtern und Artikeleigenschaften angeben.  
  
    -   Optionales Filtern von Zeilen aus Tabellenartikeln. Weitere Informationen finden Sie unter [veröffentlichten Filterdaten](../../../relational-databases/replication/publish/filter-published-data.md).  
  
    -   Festlegen des Zeitplans für den Momentaufnahme-Agent.  
  
    -   Angeben der Anmeldeinformationen, unter denen die folgenden Replikations-Agents ausgeführt werden und Verbindungen herstellen:  
  
         \- Snapshot-Agent für alle Veröffentlichungen.  
  
         \- Melden Sie sich Protokolllese-Agent für alle transaktionsveröffentlichungen.  
  
         \- Warteschlangenlese-Agent für Transaktionspublikationen, die aktualisierbare Abonnements zulassen.  
  
         Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) und [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
    -   Optionale Erstellung eines Skripts für die Veröffentlichung. Weitere Informationen finden Sie unter [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
    -   Angeben eines Namens für die Veröffentlichung.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Nachdem eine Veröffentlichung erstellt wurde, können Artikel programmgesteuert mithilfe gespeicherter Replikationsprozeduren erstellt werden. Die zur Erstellung eines Artikels verwendeten gespeicherten Prozeduren hängen vom Typ der Veröffentlichung ab, für die der Artikel definiert wird. Weitere Informationen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### So definieren Sie einen Artikel für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel, für die gehört **@publication**, einen Namen für den Artikel für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, und alle weiteren optionalen Parameter. Verwendung **@source_owner** an, den Besitz des Schemas des Objekts, wenn nicht **Dbo**. Wenn der Artikel kein Protokollbasierter Tabellenartikel ist, geben Sie den Artikel für **@type**; Weitere Informationen finden Sie unter [Artikeltypen angeben & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md).  
  
2.  Verwenden Sie zum Filtern von Zeilen in einer Tabelle oder Sichtartikels horizontal, [Sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) zur Definition der Filterklausel. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Verwenden Sie zum Filtern von Spalten in einer Tabelle oder Sichtartikels vertikal, [Sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Weitere Informationen finden Sie unter [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
4.  Führen Sie [Sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) wenn der Artikel gefiltert wird.  
  
5.  Wenn die Veröffentlichung Abonnements vorhanden sind und [Sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) Gibt einen Wert von **0** in die **Immediate_sync** Spalte müssen Sie aufrufen [Sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) Artikel zu jedem vorhandenen Abonnement hinzufügen.  
  
6.  Wenn die Veröffentlichung vorhandenen Pullabonnements stehen, führen [Sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) auf dem Verleger für vorhandene Pullabonnements eine neue Momentaufnahme zu erstellen, die nur den neuen Artikel enthält.  
  
    > [!NOTE]  
    >  Für Abonnements, die nicht mit einer Momentaufnahme initialisiert werden, Sie müssen nicht auszuführende [Sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) wie diese Prozedur ausgeführt wird, indem Sie [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
#### So definieren Sie einen Artikel für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung für **@publication**, einen Namen für den Artikel für **@article**, und das Objekt veröffentlicht wird, für **@source_object**. Um Tabellenzeilen horizontal zu filtern, geben Sie einen Wert für **@subset_filterclause**. Weitere Informationen finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md) und [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md). Wenn der Artikel kein Tabellenartikel ist, geben Sie für **@type**den Artikeltyp an. Weitere Informationen finden Sie unter [Artikeltypen angeben & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md).  
  
2.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) einen Verknüpfungsfilter zwischen zwei Artikeln zu definieren. Weitere Informationen finden Sie unter [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
3.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) um Tabellenspalten zu filtern. Weitere Informationen finden Sie unter [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel wird ein auf der Tabelle `Product` basierender Artikel für eine Transaktionsveröffentlichung definiert, wobei der Artikel sowohl horizontal als auch vertikal gefiltert wird.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_1.sql)]  
  
 In diesem Beispiel wird ein Artikel für eine Mergeveröffentlichung definiert, bei der der `SalesOrderHeader` -Artikel basierend auf **SalesPersonID**statisch gefiltert wird, und der `SalesOrderDetail` -Artikel mithilfe eines auf `SalesOrderHeader`basierenden Verknüpfungsfilters gefiltert wird.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Artikel mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert definieren. Die zur Definition eines Artikels verwendeten RMO-Klassen hängen vom Typ der Veröffentlichung ab, für die der Artikel definiert wird.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 Im folgenden Beispiel wird ein Artikel mit Zeilen- und Spaltenfiltern einer Transaktionsveröffentlichung hinzugefügt.  
  
 [!code-csharp[HowTo#rmo_CreateTranArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranarticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranarticles)]  
  
 Im folgenden Beispiel werden drei Artikel einer Mergeveröffentlichung hinzugefügt. Die Artikel haben Spaltenfilter und zwei Joinfilter, die verwendet werden, um einen parametrisierten Zeilenfilter an andere Artikel weiterzugeben.  
  
 [!code-csharp[HowTo#rmo_CreateMergeArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergearticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergeArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergearticles)]  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  