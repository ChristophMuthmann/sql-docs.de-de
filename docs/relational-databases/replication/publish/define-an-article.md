---
title: Definieren eines Artikels | Microsoft-Dokumentation
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
- articles [SQL Server replication], defining
- sp_addmergearticle
- adding articles
- sp_addarticle
- articles [SQL Server replication], adding
ms.assetid: 220584d8-b291-43ae-b036-fbba3cc07a2e
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3e37e75379dc4fd1722dd660b2c6145c9540732e
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="define-an-article"></a>Definieren eines Artikels
  In diesem Thema wird beschrieben, wie ein Artikel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekten (RMO) definiert wird.  
  
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
  
-   Artikelnamen dürfen keines der folgenden Zeichen enthalten: % , * , [ , ] , | , : , " , ? , ' , \ , / , < , >. Wenn Objekte in der Datenbank eines dieser Zeichen enthalten und Sie die Objekte replizieren möchten, müssen Sie einen Artikelnamen angeben, der sich von dem Objektnamen unterscheidet.  
  
##  <a name="Security"></a> Sicherheit  
 Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen speichern müssen, verwenden Sie die [Kryptografiedienste](http://go.microsoft.com/fwlink/?LinkId=34733) von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows .NET Framework.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Mit dem Assistenten für neue Veröffentlichung erstellen Sie Veröffentlichungen und definieren Artikel. Rufen Sie nach der Erstellung einer Veröffentlichung das Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>** auf, um die Eigenschaften anzuzeigen und zu ändern. Weitere Informationen zum Erstellen von Veröffentlichungen aus einer Oracle-Datenbank finden Sie unter [Erstellen einer Veröffentlichung aus einer Oracle-Datenbank](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
#### <a name="to-create-a-publication-and-define-articles"></a>So erstellen Sie eine Veröffentlichung und definieren Artikel  
  
1.  Stellen Sie in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und klicken Sie dann mit der rechten Maustaste auf den Ordner **Lokale Veröffentlichungen** .  
  
3.  Klicken Sie auf **Neue Veröffentlichung**.  
  
4.  Folgen Sie den Anweisungen auf den Seiten des Assistenten für neue Veröffentlichung, um folgende Vorgänge auszuführen:  
  
    -   Angeben eines Verteilers, falls die Verteilung auf dem Server nicht konfiguriert wurde. Weitere Informationen zum Konfigurieren der Verteilung finden Sie unter [Konfigurieren der Veröffentlichung und der Verteilung](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
         Wenn Sie auf der Seite **Verteiler** angeben, dass der Verleger als eigener Verteiler fungiert (lokaler Verteiler) und der Server nicht als Verteiler konfiguriert ist, erfolgt die Konfiguration des Servers durch den Assistenten für neue Veröffentlichung. Auf der Seite **Momentaufnahmeordner** geben Sie einen Standardmomentaufnahmeordner für den Verteiler an. Der Momentaufnahmeordner ist lediglich ein von Ihnen freigegebenes Verzeichnis. Agents, die aus diesem Ordner lesen bzw. in den Ordner schreiben, benötigen ausreichende Zugriffsberechtigungen. Weitere Informationen zum angemessenen Sichern des Ordners finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
         Wenn Sie angeben, dass ein anderer Server als Verteiler fungieren soll, müssen Sie auf der Seite **Administratorkennwort** ein Kennwort für Verbindungen eingeben, die zwischen dem Verleger und dem Verteiler hergestellt werden. Dieses Kennwort muss mit dem Kennwort übereinstimmen, dass bei der Aktivierung des Verlegers auf dem Remoteverteiler angegeben wurde.  
  
         Weitere Informationen finden Sie unter [Konfigurieren der Verteilung](../../../relational-databases/replication/configure-distribution.md).  
  
    -   Auswählen einer Veröffentlichungsdatenbank.  
  
    -   Auswählen eines Veröffentlichungstyps. Weitere Informationen finden Sie unter [Replikationstypen](../../../relational-databases/replication/types-of-replication.md).  
  
    -   Angeben von Daten und Datenbankobjekten, die veröffentlicht werden sollen. Optional können Sie Spalten aus Tabellenartikeln filtern und Artikeleigenschaften angeben.  
  
    -   Optionales Filtern von Zeilen aus Tabellenartikeln. Weitere Informationen finden Sie unter [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md).  
  
    -   Festlegen des Zeitplans für den Momentaufnahme-Agent.  
  
    -   Angeben der Anmeldeinformationen, unter denen die folgenden Replikations-Agents ausgeführt werden und Verbindungen herstellen:  
  
         \- Momentaufnahme-Agent (für alle Veröffentlichungen)  
  
         \- Protokolllese-Agent (für alle Transaktionsveröffentlichungen)  
  
         \- Warteschlangenlese-Agent für Transaktionsveröffentlichungen, in denen Updates von Abonnements zulässig sind  
  
         Weitere Informationen finden Sie unter [Sicherheitsmodell des Replikations-Agents](../../../relational-databases/replication/security/replication-agent-security-model.md) und [Bewährte Methoden für die Replikationssicherheit](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
    -   Optionale Erstellung eines Skripts für die Veröffentlichung. Weitere Informationen finden Sie unter [Scripting Replikation](../../../relational-databases/replication/scripting-replication.md).  
  
    -   Angeben eines Namens für die Veröffentlichung.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Nachdem eine Veröffentlichung erstellt wurde, können Artikel programmgesteuert mithilfe gespeicherter Replikationsprozeduren erstellt werden. Die zur Erstellung eines Artikels verwendeten gespeicherten Prozeduren hängen vom Typ der Veröffentlichung ab, für die der Artikel definiert wird. Weitere Informationen finden Sie unter [Erstellen eines Abonnements](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-define-an-article-for-a-snapshot-or-transactional-publication"></a>So definieren Sie einen Artikel für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication**, den Namen des Artikels für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**und alle weiteren optionalen Parameter an. Verwenden Sie **@source_owner** , um den Schemabesitz am Objekt anzugeben, wenn dies nicht **dbo**. Wenn der Artikel kein protokollbasierter Tabellenartikel ist, geben Sie für **@type** den Artikeltyp an. Weitere Informationen finden Sie unter [Angeben von Artikeltypen &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md).  
  
2.  Um Zeilen eines Tabellen- oder Sichtartikels horizontal zu filtern, verwenden Sie [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) zur Definition der Filterklausel. Weitere Informationen finden Sie unter [Definieren oder Ändern eines statischen Zeilenfilters](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Um Spalten eines Tabellen- oder Sichtartikels vertikal zu filtern, verwenden Sie [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Weitere Informationen finden Sie unter [Definieren und Ändern eines Spaltenfilters](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
4.  Führen Sie [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) aus, wenn der Artikel gefiltert wird.  
  
5.  Wenn die Veröffentlichung über vorhandene Abonnements verfügt und [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) den Wert **0** in der Spalte **immediate_sync** zurückgibt, müssen Sie [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) aufrufen, um den Artikel zu jedem vorhandenen Abonnement hinzuzufügen.  
  
6.  Wenn die Veröffentlichung über vorhandene Pullabonnements verfügt, führen Sie [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) auf dem Verleger aus, um für vorhandene Pullabonnements eine neue Momentaufnahme zu erstellen, die nur den neuen Artikel enthält.  
  
    > [!NOTE]  
    >  Für Abonnements, die nicht mithilfe einer Momentaufnahme initialisiert wurden, müssen Sie [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) nicht ausführen, da diese Prozedur von [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)ausgeführt wird.  
  
#### <a name="to-define-an-article-for-a-merge-publication"></a>So definieren Sie einen Artikel für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)aus. Geben Sie für **@publication**den Namen der Veröffentlichung, für **@article**den Namen des Artikels und für **@source_object**. Um Tabellenzeilen horizontal zu filtern, geben Sie einen Wert für **@subset_filterclause**. Weitere Informationen finden Sie unter [Definieren und Ändern eines parametrisierten Zeilenfilters für einen Mergeartikel](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md) und [Definieren oder Ändern eines statischen Zeilenfilters](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md). Wenn der Artikel kein Tabellenartikel ist, geben Sie für **@type**. Weitere Informationen finden Sie unter [Angeben von Artikeltypen &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md).  
  
2.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) aus, um einen Joinfilter zwischen zwei Artikeln zu definieren. Weitere Informationen finden Sie unter [Definieren und Ändern eines Verknüpfungsfilters zwischen Mergeartikeln](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
3.  (Optional) führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) aus, um Tabellenspalten zu filtern. Weitere Informationen finden Sie unter [Definieren und Ändern eines Spaltenfilters](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel wird ein auf der Tabelle `Product` basierender Artikel für eine Transaktionsveröffentlichung definiert, wobei der Artikel sowohl horizontal als auch vertikal gefiltert wird.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_1.sql)]  
  
 In diesem Beispiel wird ein Artikel für eine Mergeveröffentlichung definiert, bei der der `SalesOrderHeader` -Artikel basierend auf **SalesPersonID**statisch gefiltert wird, und der `SalesOrderDetail` -Artikel mithilfe eines auf `SalesOrderHeader`basierenden Verknüpfungsfilters gefiltert wird.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Artikel mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert definieren. Die zur Definition eines Artikels verwendeten RMO-Klassen hängen vom Typ der Veröffentlichung ab, für die der Artikel definiert wird.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 Im folgenden Beispiel wird ein Artikel mit Zeilen- und Spaltenfiltern einer Transaktionsveröffentlichung hinzugefügt.  
  
 [!code-cs[HowTo#rmo_CreateTranArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranarticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranarticles)]  
  
 Im folgenden Beispiel werden drei Artikel einer Mergeveröffentlichung hinzugefügt. Die Artikel haben Spaltenfilter und zwei Joinfilter, die verwendet werden, um einen parametrisierten Zeilenfilter an andere Artikel weiterzugeben.  
  
 [!code-cs[HowTo#rmo_CreateMergeArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergearticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergeArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergearticles)]  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  

