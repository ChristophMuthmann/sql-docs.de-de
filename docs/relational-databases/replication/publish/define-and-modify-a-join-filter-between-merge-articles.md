---
title: "Definieren und &#196;ndern eines Verkn&#252;pfungsfilters zwischen Mergeartikeln | Microsoft Docs"
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
  - "Filter [SQL Server-Replikation], verknüpfen"
  - "Joinfilter für die Mergereplikation [SQL Server-Replikation]"
  - "Ändern von Filtern, verknüpfen"
  - "Verknüpfungsfilter"
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
caps.latest.revision: 46
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# Definieren und &#196;ndern eines Verkn&#252;pfungsfilters zwischen Mergeartikeln
  In diesem Thema wird beschrieben, wie Verknüpfungsfilter zwischen Mergeartikeln in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]definiert und geändert werden. Die Mergereplikation unterstützt Joinfilter, die in der Regel in Verbindung mit parametrisierten Filtern verwendet werden, um die Tabellenpartitionierung auf andere verknüpfte Tabellenartikel auszuweiten.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
-   **So definieren und ändern Sie einen Verknüpfungsfilter zwischen Mergeartikeln mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Um einen Joinfilter zu erstellen, muss eine Veröffentlichung mindestens zwei verknüpfte Tabellen enthalten. Verknüpfungsfilterfilter sind eine Erweiterung von Zeilenfiltern. Daher müssen Sie den Zeilenfilter für eine Tabelle definieren, bevor Sie diesen in einer anderen Tabelle um eine Verknüpfung erweitern können. Nach dem Definieren eines Joinfilters können Sie diesen wiederum um einen anderen Joinfilter erweitern, sofern die Veröffentlichung weitere verknüpfte Tabellen enthält.  
  
-   Wenn Sie einen Verknüpfungsfilter hinzufügen, ändern oder löschen, nachdem Abonnements für die Veröffentlichung initialisiert wurden, müssen Sie eine neue Momentaufnahme generieren und alle Abonnements nach vorgenommener Änderung erneut initialisieren. Weitere Informationen zu den Anforderungen für eigenschaftenänderungen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Joinfilter für Tabellen können sowohl manuell als auch automatisch per Replikation erstellt werden. Die automatische Erstellung erfolgt auf der Basis der für die Tabellen definierten Beziehungen zwischen Fremdschlüsseln und Primärschlüsseln. Weitere Informationen zum automatischen Generieren einer Reihe von joinfiltern finden Sie unter [generiert automatisch ein Festlegen der Join Filter zwischen Merge Artikel und #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Definieren, ändern und Löschen von joinfiltern steht die **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So definieren Sie einen Joinfilter  
  
1.  Auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>**, wählen Sie einen vorhandenen Zeilenfilter oder joinfilter der **Gefilterte Tabellen** Bereich.  
  
2.  Klicken Sie auf **Hinzufügen**und anschließend auf **Join hinzufügen, um den ausgewählten Filter zu erweitern**.  
  
3.  Erstellen Sie die Joinanweisung: Aktivieren Sie dazu entweder **Anweisung mit dem Generator erstellen** oder **Joinanweisung manuell schreiben**.  
  
    -   Wenn Sie auswählen, um den Generator verwenden, verwenden Sie die Spalten im Raster (**zusammen**, **gefilterte Tabellenspalte**, **Operator**, und **verknüpfte Tabellenspalte**) zum Erstellen einer joinanweisung.  
  
         Jede Spalte im Raster enthält ein Dropdown-Kombinationsfeld, wodurch Sie zwei Spalten und einen Operator (**=**, **<>**, **<=**, **\<**, **>=**, **>**, und **wie**). Die Ergebnisse werden im Textbereich **Vorschau** angezeigt. Wenn der Join auf mehr als ein Spaltenpaar bezieht, wählen Sie eine Konjunktion (und oder oder) aus der **zusammen** Spalte, und geben Sie dann zwei weitere Spalten und einen Operator.  
  
    -   Wenn Sie ausgewählt haben, dass die Anweisung manuell geschrieben wird, schreiben Sie die Joinanweisung im Textbereich **Joinanweisung** . Ziehen Sie die gewünschten Spalten aus den Listenfeldern **Spalten der gefilterten Tabelle** und **Spalten der verknüpften Tabelle** in den Textbereich **Joinanweisung** .  
  
    -   Die vollständige Joinanweisung würde wie folgt aussehen:  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         Die JOIN-Klausel muss zweiteilige Benennungen verwenden. Drei- und vierteilige Benennungen werden nicht unterstützt.  
  
4.  Geben Sie die Joinoptionen an:  
  
    -   Wenn die Spalte, die Sie in der gefilterten Tabelle (die übergeordnete Tabelle) verknüpfen, eindeutig ist, wählen Sie **Eindeutiger Schlüssel**.  
  
        > [!CAUTION]  
        >  Durch Auswahl dieser Option kennzeichnen Sie, ob es sich bei der Beziehung zwischen der untergeordneten und der übergeordneten Tabelle in einem Joinfilter um eine 1:1- oder eine 1:n-Beziehung handelt. Verwenden Sie diese Option nur, wenn für die verknüpfte Spalte in der untergeordneten Tabelle eine Einschränkung vorhanden ist, die die Eindeutigkeit sicherstellt. Wenn die Option nicht richtig festgelegt wird, kann eine mangelnde Konvergenz der Daten die Folge sein.  
  
    -   Standardmäßig werden Änderungen durch die Mergereplikation während der Synchronisierung zeilenweise verarbeitet. Wenn Änderungen in den Zeilen der gefilterten Tabelle und der verknüpften Tabelle als Einheit verarbeitet haben, wählen Sie **logischen Datensatzes** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und höhere Versionen). Diese Option ist nur verfügbar, wenn die Anforderungen für die Verwendung logischer Datensätze durch den Artikel und die Veröffentlichung erfüllt werden. Weitere Informationen finden Sie im Abschnitt "Überlegungen zum Verwenden logischer Datensätze" unter [Gruppieren Sie Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
#### So ändern Sie einen Joinfilter  
  
1.  Auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>**, wählen Sie einen Filter in der **Gefilterte Tabellen** Bereich, und klicken Sie dann auf **Bearbeiten**.  
  
2.  Ändern Sie den Filter im Dialogfeld **Join bearbeiten** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### So löschen Sie einen Joinfilter  
  
1.  Auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>**, wählen Sie einen Filter in der **Gefilterte Tabellen** Bereich, und klicken Sie dann auf **Löschen**. Wenn der Joinfilter, den Sie löschen möchten, mit anderen Joins erweitert ist, werden diese Joins beim Löschen des Filters selbst ebenfalls gelöscht.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 In diesen Prozeduren wird ein parametrisierter Filter für einen übergeordneten Artikel mit Verknüpfungsfiltern zwischen diesem Artikel und zugehörigen untergeordneten Artikeln gezeigt. Joinfilter können mithilfe gespeicherter Replikationsprozeduren programmgesteuert definiert und geändert werden.  
  
#### So definieren Sie einen Joinfilter, um einen Artikelfilter auf zugehörige Artikel in einer Mergeveröffentlichung zu erweitern  
  
1.  Definieren Sie die Filterung für den Artikel, zu dem ein Join hergestellt werden soll. Dieser Artikel wird auch als übergeordneter Artikel bezeichnet.  
  
    -   Informationen zu einem Artikel, der mit einem parametrisierten Zeilenfilter gefiltert wurde, finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
    -   Informationen zu einem Artikel, der mit einem statischen Zeilenfilter gefiltert wurde, finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Definieren Sie einen oder mehrere Artikel, der auch bekannt als untergeordneter Artikel, für die Veröffentlichung. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergefilter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md). Geben Sie **@publication**, einen eindeutigen Namen für diesen Filter für **@filtername**, der Namen des untergeordneten Artikels in Schritt 2 erstellten **@article**, den Namen des übergeordneten Artikels für die zu verknüpfenden **@join_articlename**, und einen der folgenden Werte für **@join_unique_key**:  
  
    -   **0** -Gibt einen n: 1- oder m: n-Join zwischen den übergeordneten und untergeordneten Artikeln.  
  
    -   **1** -Gibt eine 1: 1- oder 1: n-Join zwischen den übergeordneten und untergeordneten Artikeln an.  
  
     Damit wird ein Joinfilter zwischen den beiden Artikeln definiert.  
  
    > [!CAUTION]  
    >  Nur **@join_unique_key** auf **1** wenn eine Einschränkung für die verknüpfte Spalte in der zugrunde liegenden Tabelle für den übergeordneten Artikel vorliegt, die die Eindeutigkeit sicherstellt. Wenn **@join_unique_key** Wert **1** falsch, mangelnder Konvergenz der Daten auftreten.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel wird ein Artikel für eine Mergeveröffentlichung definiert, bei der der `SalesOrderDetail` -Tabellenartikel anhand der `SalesOrderHeader` -Tabelle gefiltert wird, dies selbst mithilfe eines statischen Zeilenfilters gefiltert wird. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_1.sql)]  
  
 In diesem Beispiel definiert eine Gruppe von Artikeln in einer Mergepublikation, bei der Artikel, mit einer Reihe von Verknüpfungsfiltern anhand gefiltert werden, der `Employee` -Tabelle wird, selbst mithilfe eines parametrisierten Zeilenfilters auf dem Wert gefiltert [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) in der **LoginID** Spalte. Weitere Informationen finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_2.sql)]  
  
## Siehe auch  
 [Joinfilter](../../../relational-databases/replication/merge/join-filters.md)   
 [Parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtern veröffentlichter Daten für die Mergereplikation](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [Vorgehensweise: Definieren und Ändern eines Joinfilters zwischen Mergeartikeln (SQL Server Management Studio)](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Definieren einer logische Datensatzbeziehung zwischen Mergetabellenartikeln](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Definieren und Ändern eines parametrisierten Zeilenfilters für einen Mergeartikel](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  