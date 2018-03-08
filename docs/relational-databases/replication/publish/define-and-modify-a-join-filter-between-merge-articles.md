---
title: "Definieren und Ändern eines Verknüpfungsfilters zwischen Mergeartikeln | Microsoft-Dokumentation"
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
helpviewer_keywords:
- filters [SQL Server replication], join
- merge replication join filters [SQL Server replication]
- modifying filters, join
- join filters
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
caps.latest.revision: "46"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c9046203c32967c53c5b663bda4c64ad4f01003e
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="define-and-modify-a-join-filter-between-merge-articles"></a>Definieren und Ändern eines Verknüpfungsfilters zwischen Mergeartikeln
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Verknüpfungsfilter zwischen Mergeartikeln in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)] definiert und geändert werden. Die Mergereplikation unterstützt Joinfilter, die in der Regel in Verbindung mit parametrisierten Filtern verwendet werden, um die Tabellenpartitionierung auf andere verknüpfte Tabellenartikel auszuweiten.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
-   **So definieren und ändern Sie einen Verknüpfungsfilter zwischen Mergeartikeln mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Um einen Joinfilter zu erstellen, muss eine Veröffentlichung mindestens zwei verknüpfte Tabellen enthalten. Verknüpfungsfilterfilter sind eine Erweiterung von Zeilenfiltern. Daher müssen Sie den Zeilenfilter für eine Tabelle definieren, bevor Sie diesen in einer anderen Tabelle um eine Verknüpfung erweitern können. Nach dem Definieren eines Joinfilters können Sie diesen wiederum um einen anderen Joinfilter erweitern, sofern die Veröffentlichung weitere verknüpfte Tabellen enthält.  
  
-   Wenn Sie einen Verknüpfungsfilter hinzufügen, ändern oder löschen, nachdem Abonnements für die Veröffentlichung initialisiert wurden, müssen Sie eine neue Momentaufnahme generieren und alle Abonnements nach vorgenommener Änderung erneut initialisieren. Weitere Informationen zum Ändern von Eigenschaften finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Joinfilter für Tabellen können sowohl manuell als auch automatisch per Replikation erstellt werden. Die automatische Erstellung erfolgt auf der Basis der für die Tabellen definierten Beziehungen zwischen Fremdschlüsseln und Primärschlüsseln. Weitere Informationen zum automatischen Generieren einer Reihe von Verknüpfungsfiltern finden Sie unter [Automatically Generate a Set of Join Filters Between Merge Articles &#40;SQL Server Management Studio&#41; (Automatischses Generieren einer Reihe von Verküpfungsfiltern zwischen Mergeartikeln &#40;SQL Server Management Studio&#41;)](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md).  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 Definieren, ändern und löschen Sie Verknüpfungsfilter auf der Seite **Tabellenzeilen filtern** des Assistenten für neue Veröffentlichung oder auf der Seite **Filterzeilen** im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>**. Weitere Informationen zum Verwenden des Assistenten sowie zum Zugriff auf das Dialogfeld finden Sie unter [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-define-a-join-filter"></a>So definieren Sie einen Joinfilter  
  
1.  Wählen Sie auf der Seite **Tabellenzeilen filtern** des Assistenten für neue Veröffentlichung oder auf der Seite **Filterzeilen** von **Veröffentlichungseigenschaften - \<Veröffentlichung>** einen vorhandenen Zeilenfilter oder Verknüpfungsfilter im Bereich **Gefilterte Tabellen** aus.  
  
2.  Klicken Sie auf **Hinzufügen**und anschließend auf **Join hinzufügen, um den ausgewählten Filter zu erweitern**.  
  
3.  Erstellen Sie die Joinanweisung: Aktivieren Sie dazu entweder **Anweisung mit dem Generator erstellen** oder **Joinanweisung manuell schreiben**.  
  
    -   Wenn Sie auswählen, dass der Generator verwendet werden soll, verwenden Sie die Spalten im Raster (**Konjunktion**, **Gefilterte Tabellenspalte**, **Operator**und **Verknüpfte Tabellenspalte**), um eine Joinanweisung zu erstellen.  
  
         Die Spalten in der Tabelle enthalten jeweils ein Dropdown-Kombinationsfeld, in dem Sie zwei Spalten und einen Operator (**=**, **<>**, **<=**, **\<**, **>=**, **>**und **like**) auswählen können. Die Ergebnisse werden im Textbereich **Vorschau** angezeigt. Wenn sich der Join auf mehr als ein Spaltenpaar bezieht, wählen Sie in der **Konjunktion** -Spalte eine Konjunktion aus (AND oder OR), und geben Sie dann zwei weitere Spalten und einen Operator ein.  
  
    -   Wenn Sie ausgewählt haben, dass die Anweisung manuell geschrieben wird, schreiben Sie die Joinanweisung im Textbereich **Joinanweisung** . Ziehen Sie die gewünschten Spalten aus den Listenfeldern **Spalten der gefilterten Tabelle** und **Spalten der verknüpften Tabelle** in den Textbereich **Joinanweisung** .  
  
    -   Die vollständige Joinanweisung würde wie folgt aussehen:  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         Die JOIN-Klausel muss zweiteilige Benennungen verwenden. Drei- und vierteilige Benennungen werden nicht unterstützt.  
  
4.  Geben Sie die Joinoptionen an:  
  
    -   Falls die Spalte, die mit der gefilterten Tabelle (der übergeordneten Tabelle) verknüpft wird, eindeutig ist, aktivieren Sie die Option **Unique key**.  
  
        > [!CAUTION]  
        >  Durch Auswahl dieser Option kennzeichnen Sie, ob es sich bei der Beziehung zwischen der untergeordneten und der übergeordneten Tabelle in einem Joinfilter um eine 1:1- oder eine 1:n-Beziehung handelt. Verwenden Sie diese Option nur, wenn für die verknüpfte Spalte in der untergeordneten Tabelle eine Einschränkung vorhanden ist, die die Eindeutigkeit sicherstellt. Wenn die Option nicht richtig festgelegt wird, kann eine mangelnde Konvergenz der Daten die Folge sein.  
  
    -   Standardmäßig werden Änderungen durch die Mergereplikation während der Synchronisierung zeilenweise verarbeitet. Wenn Änderungen in Zeilen sowohl in der gefilterten Tabelle als auch in der verknüpften Tabelle als eine Einheit verarbeitet werden sollen, aktivieren Sie die Option **Logischer Datensatz** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen verfügbar). Diese Option ist nur verfügbar, wenn die Anforderungen für die Verwendung logischer Datensätze durch den Artikel und die Veröffentlichung erfüllt werden. Weitere Informationen finden Sie im Abschnitt „Überlegungen zum Verwenden logischer Datensätze“ unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Wenn Sie sich im Dialogfeld **Veröffentlichungseigenschaften.-.\<Veröffentlichung>** befinden, klicken Sie auf **OK**, um zu speichern und das Dialogfeld zu schließen.  
  
#### <a name="to-modify-a-join-filter"></a>So ändern Sie einen Joinfilter  
  
1.  Wählen Sie auf der Seite **Tabellenzeilen filtern** des Assistenten für neue Veröffentlichung oder auf der Seite **Filterzeilen** von **Veröffentlichungseigenschaften - \<Veröffentlichung>** einen Filter im Bereich **gefilterte Tabellen**, und klicken Sie dann auf **Bearbeiten**.  
  
2.  Ändern Sie den Filter im Dialogfeld **Join bearbeiten** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-join-filter"></a>So löschen Sie einen Joinfilter  
  
1.  Wählen Sie auf der Seite **Tabellenzeilen filtern** des Assistenten für neue Veröffentlichung oder der Seite **Filterzeilen** von **Veröffentlichungseigenschaften - \<Veröffentlichung>** einen Filter im Bereich **gefilterte Tabellen**, und klicken Sie dann auf **Löschen**. Wenn der Joinfilter, den Sie löschen möchten, mit anderen Joins erweitert ist, werden diese Joins beim Löschen des Filters selbst ebenfalls gelöscht.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 In diesen Prozeduren wird ein parametrisierter Filter für einen übergeordneten Artikel mit Verknüpfungsfiltern zwischen diesem Artikel und zugehörigen untergeordneten Artikeln gezeigt. Joinfilter können mithilfe gespeicherter Replikationsprozeduren programmgesteuert definiert und geändert werden.  
  
#### <a name="to-define-a-join-filter-to-extend-an-article-filter-to-related-articles-in-a-merge-publication"></a>So definieren Sie einen Joinfilter, um einen Artikelfilter auf zugehörige Artikel in einer Mergeveröffentlichung zu erweitern  
  
1.  Definieren Sie die Filterung für den Artikel, zu dem ein Join hergestellt werden soll. Dieser Artikel wird auch als übergeordneter Artikel bezeichnet.  
  
    -   Informationen zu einem Artikel, der mit einem parametrisierten Zeilenfilter gefiltert wurde, finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
    -   Informationen zu einem Artikel, der mit einem statischen Zeilenfilter gefiltert wurde, finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank, [Sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) aus um einen oder mehrere ähnliche Artikel, auch bekannt als untergeordnete Artikel, für die Veröffentlichung zu definieren. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)aus. Geben Sie **@publication**, einen eindeutigen Namen für diesen Filter für **@filtername**, den Namen des in Schritt 2 erstellten untergeordneten Artikels für **@article**, den Namen des übergeordneten Artikels, mit dem ein Join hergestellt wird, für **@join_articlename**und einen der folgenden Werte für **@join_unique_key**an:  
  
    -   **0** &ndash; gibt einen n:1- oder einen n:n-Join zwischen den übergeordneten und den untergeordneten Artikeln an.  
  
    -   **1** &ndash; gibt einen 1:1- oder einen 1:n-Join zwischen den übergeordneten und den untergeordneten Artikeln an.  
  
     Damit wird ein Joinfilter zwischen den beiden Artikeln definiert.  
  
    > [!CAUTION]  
    >  Legen Sie **@join_unique_key** nur dann auf **1** fest, wenn eine Einschränkung für die verknüpfte Spalte in der zugrunde liegenden Tabelle für den übergeordneten Artikel vorliegt, die die Eindeutigkeit sicherstellt. Wird **@join_unique_key** fälschlicherweise auf **1** festgelegt, kann dies zu mangelnder Konvergenz der Daten führen.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel wird ein Artikel für eine Mergeveröffentlichung definiert, bei der der `SalesOrderDetail` -Tabellenartikel anhand der `SalesOrderHeader` -Tabelle gefiltert wird, dies selbst mithilfe eines statischen Zeilenfilters gefiltert wird. Weitere Informationen finden Sie unter [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_1.sql)]  
  
 In diesem Beispiel wird eine Gruppe von Artikeln in einer Mergeveröffentlichung definiert, bei der die Artikel mit einer Reihe von Verknüpfungsfiltern anhand der `Employee` -Tabelle gefiltert werden, die selbst mithilfe eines parametrisierten Zeilenfilters für den Wert [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) in der **LoginID** -Spalte gefiltert wird. Weitere Informationen finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_2.sql)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verknüpfungsfilter](../../../relational-databases/replication/merge/join-filters.md)   
 [Parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtern von veröffentlichten Daten für die Mergereplikation](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [So wird`s gemacht: definieren und ändern Sie einen Verknüpfungsfilter zwischen Mergeartikeln (SQL Server Management Studio)](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Definieren einer logische Datensatzbeziehung zwischen Mergetabellenartikeln](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Definieren und Ändern eines parametrisierten Zeilenfilters für einen Mergeartikel](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  
