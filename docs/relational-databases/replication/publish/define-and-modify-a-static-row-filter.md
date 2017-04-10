---
title: "Definieren oder &#196;ndern eines statischen Zeilenfilters | Microsoft Docs"
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
  - "Ändern von Filtern, statische Zeilen-"
  - "Statische Zeilenfilter"
  - "Filter [SQL Server-Replikation], statische Zeilen-"
ms.assetid: a6ebb026-026f-4c39-b6a9-b9998c3babab
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Definieren oder &#196;ndern eines statischen Zeilenfilters
  In diesem Thema wird beschrieben, wie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]statische Zeilenfilter definiert und geändert werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
-   **So definieren oder ändern Sie einen statischen Zeilenfilter mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie einen statischen Zeilenfilter hinzufügen, ändern oder löschen, nachdem Abonnements für die Veröffentlichung initialisiert wurden, müssen Sie eine neue Momentaufnahme generieren und alle Abonnements nach vorgenommener Änderung erneut initialisieren. Weitere Informationen zu den Anforderungen für eigenschaftenänderungen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
-   Wenn die Veröffentlichung für die Peer-zu-Peer-Transaktionsreplikation aktiviert wird, können Tabellen nicht gefiltert werden.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Da diese Filter statisch sind, erhalten alle Abonnenten die gleiche Teilmenge der Daten. Informationen darüber, wie Sie Zeilen in einem Tabellenartikel, der zu einer Mergeveröffentlichung gehört, dynamisch filtern können, damit jeder Abonnent eine andere Partition der Daten erhält, finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md). Mergereplikation ermöglicht es Ihnen zudem, verknüpfte Zeilen auf Grundlage eines vorhandenen Zeilenfilters zu filtern. Weitere Informationen finden Sie unter [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Definieren, ändern und löschen Sie statische Zeilenfilter auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So definieren Sie einen statischen Zeilenfilter  
  
1.  Auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld die Aktion, die Sie ausführen, hängt vom Typ der Veröffentlichung:  
  
    -   Klicken Sie bei der Momentaufnahme- oder Transaktionsveröffentlichung auf **Hinzufügen**.  
  
    -   Klicken Sie bei der Mergeveröffentlichung auf **Hinzufügen**und dann auf **Filter hinzufügen**.  
  
2.  In der **Filter hinzufügen** Dialogfeld Wählen Sie eine Tabelle aus dem Dropdown-Listenfeld zu filtern.  
  
3.  Erstellen Sie im Textfeld **Filteranweisung** eine Filteranweisung. Sie können den Text direkt in den Textbereich eingeben, und Sie können Spalten auch mit Drag und Drop aus dem Listenfeld **Spalten** einfügen.  
  
    > [!NOTE]  
    >  Verwenden Sie einen zweiteiligen Namen für die WHERE-Klausel, drei- oder vierteilige Namen werden nicht unterstützt. Wenn die Veröffentlichung von einem Oracle-Verleger stammt, muss die WHERE-Klausel mit der Oracle-Syntax kompatibel sein.  
  
    -   Der Textbereich **Filteranweisung** enthält den Standardtext im folgenden Format:  
  
        ```tsql  
        SELECT <published_columns> FROM [schema].[tablename] WHERE  
        ```  
  
    -   Der Standardtext kann nicht geändert werden. Geben Sie mithilfe der SQL-Standardsyntax im Anschluss an das WHERE-Schlüsselwort die Filterklausel ein. Die vollständige Filterklausel würde folgendermaßen lauten:  
  
        ```tsql  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE [LoginID] = 'adventure-works\ranjit0'  
        ```  
  
    -   Ein statischer Zeilenfilter kann eine benutzerdefinierte Funktion einschließen. Die vollständige Filterklausel für einen statischen Zeilenfilter mit einer benutzerdefinierten Funktion würde folgendermaßen lauten:  
  
        ```tsql  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] WHERE MyFunction([Freight]) > 100  
        ```  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
#### So ändern Sie einen statischen Zeilenfilter  
  
1.  Auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld Wählen Sie einen Filter in der **Gefilterte Tabellen** Bereich, und klicken Sie dann auf **Bearbeiten**.  
  
2.  Ändern Sie den Filter im Dialogfeld **Filter bearbeiten** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### So löschen Sie einen statischen Zeilenfilter  
  
1.  Auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld Wählen Sie einen Filter in der **Gefilterte Tabellen** Bereich, und klicken Sie dann auf **Löschen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Wenn Sie Tabellenartikel erstellen, können Sie eine WHERE-Klausel definieren, um Zeilen aus einem Artikel zu filtern. Zudem können Sie einen Zeilenfilter ändern, nachdem er definiert wurde. Statische Zeilenfilter können mithilfe gespeicherter Replikationsprozeduren programmgesteuert erstellt und geändert werden.  
  
#### So definieren Sie einen statischen Zeilenfilter für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Definieren Sie den zu filternden Artikel. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_articlefilter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md). Geben Sie den Namen des Artikels für **@article**, den Namen der Veröffentlichung für **@publication**, einen Namen für den Filter für **@filter_name**, und die Filterklausel für **@filter_clause** (einschließlich nicht `WHERE`).  
  
3.  Wenn außerdem ein Spaltenfilter definiert werden muss, finden Sie Informationen unter [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md). Führen Sie andernfalls [Sp_articleview & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Geben Sie den Namen der Veröffentlichung für **@publication**, den Namen des gefilterten Artikels für **@article**, und die in Schritt 2 angegebene Filterklausel **@filter_clause**. Damit werden die Synchronisierungsobjekte für den gefilterten Artikel erstellt.  
  
#### So ändern Sie einen statischen Zeilenfilter für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_articlefilter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md). Geben Sie den Namen des Artikels für **@article**, den Namen der Veröffentlichung für **@publication**, einen Namen für den neuen Filter für **@filter_name**, und die neue Filterklausel für **@filter_clause** (einschließlich nicht `WHERE`). Da diese Änderung Daten in vorhandenen Abonnements ungültig werden, geben Sie den Wert **1** für **@force_reinit_subscription**.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_articleview & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Geben Sie den Namen der Veröffentlichung für **@publication**, den Namen des gefilterten Artikels für **@article**, und die in Schritt 1 angegebene Filterklausel **@filter_clause**. Dadurch wird die Sicht neu erstellt, die den gefilterten Artikel definiert.  
  
3.  Führen Sie den Auftrag des Momentaufnahme-Agents für die Veröffentlichung erneut aus, um eine aktualisierte Momentaufnahme zu erstellen. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
4.  Erneutes Initialisieren von Abonnements Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### So löschen Sie einen statischen Zeilenfilter für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_articlefilter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md). Geben Sie den Namen des Artikels für **@article**, den Namen der Veröffentlichung für **@publication**, ein Wert von NULL für **@filter_name**, und der Wert NULL für **@filter_clause**. Da diese Änderung Daten in vorhandenen Abonnements ungültig werden, geben Sie den Wert **1** für **@force_reinit_subscription**.  
  
2.  Führen Sie den Auftrag des Momentaufnahme-Agents für die Veröffentlichung erneut aus, um eine aktualisierte Momentaufnahme zu erstellen. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
3.  Erneutes Initialisieren von Abonnements Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### So definieren Sie einen statischen Zeilenfilter für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie die Filterklausel für **@subset_filterclause** (einschließlich nicht `WHERE`). Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Wenn außerdem ein Spaltenfilter definiert werden muss, finden Sie Informationen unter [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
#### So ändern Sie einen statischen Zeilenfilter für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung für **@publication**, den Namen des gefilterten Artikels für **@article**, ein Wert von **Subset_filterclause** für **@property**, und die neue Filterklausel für **@value** (einschließlich nicht `WHERE`). Da diese Änderung Daten in vorhandenen Abonnements ungültig werden, geben Sie den Wert 1 für **@force_reinit_subscription**.  
  
2.  Führen Sie den Auftrag des Momentaufnahme-Agents für die Veröffentlichung erneut aus, um eine aktualisierte Momentaufnahme zu erstellen. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
3.  Erneutes Initialisieren von Abonnements Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel für eine Transaktionsreplikation wird der Artikel horizontal gefiltert, um alle eingestellten Produkte zu entfernen.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_1.sql)]  
  
 In diesem Beispiel für eine Mergereplikation werden die Artikel horizontal gefiltert, und nur die Zeilen zurückgegeben, die auf den angegebenen Vertriebsmitarbeiter entfallen. Außerdem wird ein Joinfilter verwendet. Weitere Informationen finden Sie unter [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_2.sql)]  
  
## Siehe auch  
 [Definieren und Ändern eines parametrisierten Zeilenfilters für einen Mergeartikel](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtern veröffentlichter Daten für die Mergereplikation](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  