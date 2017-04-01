---
title: "Definieren und &#196;ndern eines parametrisierten Zeilenfilters f&#252;r einen Mergeartikel | Microsoft Docs"
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
  - "Parametrisierte Filter [SQL Server-Replikation], definieren"
  - "Parametrisierte Filter [SQL Server-Replikation], ändern"
  - "Mergereplikation [SQL Server-Replikation], dynamische Filter"
  - "Parametrisierte Filter für die Mergereplikation [SQL Server-Replikation]"
  - "Filter [SQL Server-Replikation], parametrisierte"
  - "Ändern von Filtern, parametrisierte Zeile"
  - "Dynamische Filter [SQL Server-Replikation]"
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Definieren und &#196;ndern eines parametrisierten Zeilenfilters f&#252;r einen Mergeartikel
  In diesem Thema wird beschrieben, wie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]parametrisierte Zeilenfilter definiert und geändert werden.  
  
 Zum Erstellen von Tabellenartikeln können Sie parametrisierte Zeilenfilter verwenden. In diesen Filtern werden mit einer [WHERE-Klausel](../../../t-sql/queries/where-transact-sql.md) die zu veröffentlichenden Daten ausgewählt. Statt in der Klausel einen Literalwert anzugeben, (wie bei einem statischen Zeilenfilter), Sie geben eine oder beide der folgenden Systemfunktionen: [SUSER_SNAME](../../../t-sql/functions/suser-sname-transact-sql.md) und [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md). Weitere Informationen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So definieren oder ändern Sie einen parametrisierten Zeilenfilter mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie einen parametrisierten Zeilenfilter hinzufügen, ändern oder löschen, nachdem Abonnements für die Veröffentlichung initialisiert wurden, müssen Sie eine neue Momentaufnahme generieren und alle Abonnements nach vorgenommener Änderung erneut initialisieren. Weitere Informationen zu den Anforderungen für eigenschaftenänderungen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Aus Leistungsgründen wird empfohlen, keine Funktionen auf Spaltennamen in parametrisierten Zeilenfilterklauseln (beispielsweise `LEFT([MyColumn]) = SUSER_SNAME()`) anzuwenden. Wenn Sie HOST_NAME in einer Filterklausel verwenden und den HOST_NAME-Wert überschreiben, müssen Datentypen eventuell mit CONVERT konvertiert werden. Weitere Informationen zu bewährten Methoden für diesen Fall finden Sie im Abschnitt "Überschreiben des Host_name()-Werts""im Thema [parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Definieren, ändern und Löschen von parametrisierten Zeilenfiltern für die **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So definieren Sie einen parametrisierten Zeilenfilter  
  
1.  Auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>**, klicken Sie auf **Hinzufügen**, und klicken Sie dann auf **Filter hinzufügen**.  
  
2.  In der **Filter hinzufügen** Dialogfeld Wählen Sie eine Tabelle aus dem Dropdown-Listenfeld zu filtern.  
  
3.  Erstellen Sie im Textfeld **Filteranweisung** eine Filteranweisung. Sie können den Text direkt in den Textbereich eingeben, und Sie können Spalten auch mit Drag und Drop aus dem Listenfeld **Spalten** einfügen.  
  
    -   Der Textbereich **Filteranweisung** enthält den Standardtext im folgenden Format:  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   Der Standardtext kann nicht geändert werden. Geben Sie mithilfe der SQL-Standardsyntax im Anschluss an das WHERE-Schlüsselwort die Filterklausel ein. Parametrisierte Filter enthalten einen Aufruf der Systemfunktion **HOST_NAME()** und/oder **SUSER_SNAME()**, oder eine benutzerdefinierte Funktion, die eine oder beide dieser Funktionen verweist. Eine vollständige Filterklausel für einen parametrisierten Zeilenfilter kann z. B. wie folgt aussehen:  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         Verwenden Sie einen zweiteiligen Namen für die WHERE-Klausel, drei- oder vierteilige Namen werden nicht unterstützt.  
  
4.  Wählen Sie die Option aus, mit der angegeben wird, wie Daten für mehrere Abonnenten freigegeben werden:  
  
    -   **Eine Zeile aus dieser Tabelle wird an mehrere Abonnements gesendet**  
  
    -   **Eine Zeile aus dieser Tabelle wird nur an ein Abonnement gesendet**  
  
     Wenn Sie **Eine Zeile aus dieser Tabelle wird nur an ein Abonnement gesendet**auswählen, kann die Mergereplikation die Leistung optimieren, da weniger Metadaten gespeichert und verarbeitet werden. Sie müssen jedoch sicherstellen, dass die Daten so partitioniert werden, dass eine Zeile nicht für mehrere Abonnenten repliziert werden kann. Weitere Informationen finden Sie im Abschnitt zum Festlegen von Partitionsoptionen unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
#### So ändern Sie einen parametrisierten Zeilenfilter  
  
1.  Auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>**, wählen Sie einen Filter in der **Gefilterte Tabellen** Bereich, und klicken Sie dann auf **Bearbeiten**.  
  
2.  Ändern Sie den Filter im Dialogfeld **Filter bearbeiten** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### So löschen Sie einen parametrisierten Zeilenfilter  
  
1.  Auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>**, wählen Sie einen Filter in der **Gefilterte Tabellen** Bereich, und klicken Sie dann auf **Löschen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Parametrisierte Zeilenfilter können mithilfe gespeicherter Replikationsprozeduren programmgesteuert erstellt und geändert werden.  
  
#### So definieren Sie einen parametrisierten Zeilenfilter für einen Artikel in einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie **@publication**, einen Namen für den Artikel für **@article**, in die Tabelle veröffentlicht wird, für **@source_object**, die WHERE-Klausel, die für den parametrisierten Filter definiert **@subset_filterclause** (einschließlich nicht `WHERE`), und einen der folgenden Werte für **@partition_options**, welche beschreibt die Art der Partitionierung, die aus dem parametrisierten Filter wird:  
  
    -   **0** – der Filtervorgang für den Artikel ist entweder statisch oder ergibt keine eindeutige Teilmenge von Daten für jede Partition (eine "überlappende" Partition).  
  
    -   **1** - resultierende Partitionen überlappen, und auf dem Abonnenten vorgenommene Updates können nicht die Partition ändern, eine Zeile gehört.  
  
    -   **2** - Filtern für den Artikel ergibt nicht überlappende Partitionen jedoch mehrere Abonnenten können die gleiche Partition erhalten.  
  
    -   **3** – der Filtervorgang für den Artikel ergibt nicht überlappende Partitionen, die für jedes Abonnement eindeutig sind.  
  
#### So ändern Sie einen parametrisierten Zeilenfilter für einen Artikel in einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Geben Sie **@publication**, **@article**, Wert **Subset_filterclause** für **@property**, der Ausdruck, der für den parametrisierten Filter definiert **@value** (einschließlich nicht `WHERE`), und der Wert **1** für beide **@force_invalidate_snapshot** und **@force_reinit_subscription**.  
  
2.  Wenn diese Änderung partitionierungsverhalten führt, und führen Sie dann [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) erneut. Geben Sie **@publication**, **@article**, Wert **Partition_options** für **@property**, und die am besten geeignete Partitionierungsoption für **@value**, dies kann einer der folgenden sein:  
  
    -   **0** – der Filtervorgang für den Artikel ist entweder statisch oder ergibt keine eindeutige Teilmenge von Daten für jede Partition (eine "überlappende" Partition).  
  
    -   **1** - resultierende Partitionen überlappen, und auf dem Abonnenten vorgenommene Updates können nicht die Partition ändern, eine Zeile gehört.  
  
    -   **2** - Filtern für den Artikel ergibt nicht überlappende Partitionen jedoch mehrere Abonnenten können die gleiche Partition erhalten.  
  
    -   **3** – der Filtervorgang für den Artikel ergibt nicht überlappende Partitionen, die für jedes Abonnement eindeutig sind.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel wird eine Gruppe von Artikeln in einer Mergeveröffentlichung definiert, bei der die Artikel mit einer Reihe von Verknüpfungsfiltern anhand der `Employee` -Tabelle gefiltert werden, die selbst mithilfe eines parametrisierten Zeilenfilters in der **LoginID** -Spalte gefiltert wird. Während der Synchronisierung der Wert zurückgegeben, indem die [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) -Funktion überschrieben. Weitere Informationen finden Sie unter Überschreiben des Host_name()-Werts"im Thema [parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-para_1.sql)]  
  
## Siehe auch  
 [Definieren und Ändern eines Verknüpfungsfilters zwischen Mergeartikeln](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Joinfilter](../../../relational-databases/replication/merge/join-filters.md)   
 [Parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  