---
title: "Optimieren von parametrisierten Zeilenfiltern | Microsoft Docs"
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
  - "Vorausberechnete Partitionen [SQL Server-Replikation]"
  - "Filter [SQL Server-Replikation], parametrisierte"
  - "Vorausberechnete Mergereplikationspartitionen [SQL Server-Replikation], SQL Server Management Studio"
  - "Parametrisierte Filter [SQL Server-Replikation], optimieren"
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Optimieren von parametrisierten Zeilenfiltern
  In diesem Thema wird beschrieben, wie parametrisierte Zeilenfilter in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]optimiert werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
-   **So optimieren Sie parametrisierte Zeilenfilter mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wenn Sie parametrisierte Filter verwenden, können Sie festlegen, wie die Filter durch die Mergereplikation verarbeitet werden, indem Sie bei der Erstellung der Veröffentlichung entweder die Option **use partition groups** oder die Option **keep partition changes** wählen. Diese Optionen verbessern bei Veröffentlichungen mit gefilterten Artikeln die Synchronisierungsleistung, da in der Veröffentlichungsdatenbank zusätzliche Metadaten gespeichert werden. Sie können steuern, wie die Daten auf die einzelnen Abonnenten aufgeteilt werden, indem Sie bei der Erstellung eines Artikels **partition options** festlegen. Weitere Informationen zu diesen Anforderungen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
     Mit [!INCLUDE[ssEW](../../../includes/ssew-md.md)] SQL Server Compact-Abonnenten muss "keep_partition_changes" auf "true" festgelegt werden, um sicherzustellen, dass Löschvorgänge ordnungsgemäß weitergegeben werden. Wenn die Einstellung auf "false" festgelegt ist, erhält der Abonnent möglicherweise mehr Zeilen als erwartet.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Folgende Einstellungen können zur Optimierung von parametrisierten Zeilenfiltern verwendet werden:  
  
 **Partitionsoptionen**  
 Legen Sie diese Option auf der **Eigenschaften** auf der Seite der **Artikeleigenschaften - \< Artikel>** im Dialogfeld oder in der **Filter hinzufügen** Dialogfeld. Beide Dialogfelder stehen im Assistenten für neue Veröffentlichung und die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Die **Artikeleigenschaften - \< Artikel>** im Dialogfeld können Sie weitere Werte für diese Option angeben, die nicht verfügbar sind die **Filter hinzufügen** Dialogfeld.  
  
 **Partitionen im Voraus berechnen**  
 Diese Option wird festgelegt, um **True** standardmäßig, wenn die Artikel in Ihrer Veröffentlichung einem Satz von Anforderungen entsprechen. Weitere Informationen zu diesen Anforderungen finden Sie unter [parametrisierte Filter Leistung mit Vorausberechnete Partitionen optimieren](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md). Ändern Sie diese Option auf der **Abonnementoptionen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld).  
  
 **Synchronisierung optimieren**  
 Diese Option sollte festgelegt werden, um **True** nur, wenn **Partitionen im Voraus berechnen** Wert **False**. Legen Sie diese Option auf der **Abonnementoptionen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld).  
  
 Weitere Informationen zum Verwenden des Assistenten für neue Veröffentlichung und Zugreifen auf die **Veröffentlichungseigenschaften - \< Veröffentlichung>** im Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So legen Sie Partitionsoptionen im Dialogfeld Filter hinzufügen bzw. Filter bearbeiten fest  
  
1.  Auf der **Tabellenzeilen filtern** Seite des Assistenten für neue Veröffentlichung oder **Filterzeilen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** im Dialogfeld klicken Sie auf **Hinzufügen**, und klicken Sie dann auf **Filter hinzufügen**.  
  
2.  Erstellen Sie einen parametrisierten Filter. Weitere Informationen finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
3.  Wählen Sie die Option aus, mit der angegeben wird, wie Daten für mehrere Abonnenten freigegeben werden:  
  
    -   **Eine Zeile aus dieser Tabelle wird an mehrere Abonnements gesendet**  
  
    -   **Eine Zeile aus dieser Tabelle wird nur an ein Abonnement gesendet**  
  
     Wenn Sie **Eine Zeile aus dieser Tabelle wird nur an ein Abonnement gesendet**auswählen, kann die Mergereplikation die Leistung optimieren, da weniger Metadaten gespeichert und verarbeitet werden. Sie müssen jedoch sicherstellen, dass die Daten so partitioniert werden, dass eine Zeile nicht für mehrere Abonnenten repliziert werden kann. Weitere Informationen finden Sie im Abschnitt zum Festlegen von Partitionsoptionen unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
#### Festlegen von Partitionsoptionen im Artikeleigenschaften - \< Artikel> (Dialogfeld)  
  
1.  Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld Wählen Sie eine Tabelle, und klicken Sie dann auf **Artikeleigenschaften**.  
  
2.  Klicken Sie auf **Eigenschaften des hervorgehobenen Tabelle-Artikels festlegen** oder **Eigenschaften aller Tabellenartikel festlegen**.  
  
3.  In der **Zielobjekt** Teil der **Eigenschaften** Registerkarte der **Artikeleigenschaften - \< Artikel>** Dialogfeld geben die folgenden Werte für **Partitionsoptionen**:  
  
    -   **Überlappend**  
  
    -   **Überlappend, Datenänderungen außerhalb der Partition nicht zulassen**  
  
    -   **Nicht überlappend, ein Abonnement**  
  
    -   **Nicht überlappend, für mehrere Abonnements freigegeben**  
  
     Weitere Informationen zu diesen Optionen und dazu, in welcher Beziehung Sie zu den Optionen stehen, die im Dialogfeld **Filter hinzufügen** und **Filter bearbeiten** verfügbar sind, finden Sie im Abschnitt über das Festlegen von Partitionsoptionen unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
#### So legen Sie einen Wert für Partitionen im Voraus berechnen fest  
  
1.  Auf der **Abonnementoptionen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld Wählen Sie einen Wert für die **Partitionen im Voraus berechnen** Option. Die Eigenschaft ist in folgenden Fällen schreibgeschützt:  
  
    -   Die Veröffentlichung erfüllt die Anforderungen für im Voraus berechnete Partitionen nicht.  
  
    -   Es wurde noch keine Momentaufnahme für die Veröffentlichung generiert. In diesem Fall wird für die Option der Wert **Wird automatisch beim Erstellen einer Momentaufnahme festgelegt**angezeigt.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### So legen Sie einen Wert für Synchronisierung optimieren fest  
  
1.  Auf der **Abonnementoptionen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Wert wählen Sie im Dialogfeld **True** für die **Synchronisierung optimieren** Option.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Informationen zur Definition der Filteroptionen für **@keep_partition_changes** und **@use_partition_groups**, finden Sie unter [Sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
#### So geben Sie die Optimierungen für Mergefilter beim Erstellen einer neuen Veröffentlichung an  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Geben Sie **@publication** und den Wert **true** für einen der folgenden Parameter an:  
  
    -   **@use_partition_groups**:-die höchste leistungsoptimierung, vorausgesetzt, dass die Artikel den Anforderungen für Vorausberechnete Partitionen entsprechen. Weitere Informationen finden Sie unter [parametrisierte Filter Leistung mit Vorausberechnete Partitionen optimieren](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md).  
  
    -   **@keep_partition_changes** -Verwenden Sie diese Optimierung, wenn Vorausberechnete Partitionen nicht verwendet werden.  
  
2.  Fügen Sie einen Momentaufnahme-Auftrag für die Veröffentlichung hinzu. Weitere Informationen finden Sie unter [Erstellen einer Publikation](../../../relational-databases/replication/publish/create-a-publication.md).  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), geben Sie die folgenden Parameter:  
  
    -   **@publication** -der Name der Veröffentlichung aus Schritt 1.  
  
    -   **@article** -einen Namen für den Artikel  
  
    -   **@source_object** – das Datenbankobjekt, das veröffentlicht wird.  
  
    -   **@subset_filterclause** -die optionale parametrisierte Filterklausel verwendet, um den Artikel horizontal zu filtern.  
  
    -   **@partition_options** -die Partitionsoptionen für den gefilterten Artikel.  
  
4.  Wiederholen Sie Schritt 3 für jeden Artikel in der Veröffentlichung.  
  
5.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) einen Verknüpfungsfilter zwischen zwei Artikeln zu definieren. Weitere Informationen finden Sie unter [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
#### So zeigen Sie das Verhalten von Mergefiltern für eine vorhandene Veröffentlichung an und ändern es  
  
1.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), wobei **@publication**. Beachten Sie den Wert der **Keep_partition_changes** und **Use_partition_groups** im Ergebnis festlegen.  
  
2.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Geben Sie den Wert **Use_partition_groups** für **@property** und entweder **true** oder **false** für **@value**.  
  
3.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Geben Sie den Wert **Keep_partition_changes** für **@property** und entweder **true** oder **false** für **@value**.  
  
    > [!NOTE]  
    >  Beim Aktivieren der **Keep_partition_changes**, müssen Sie zuerst deaktivieren **Use_partition_groups** und geben Sie den Wert **1** für **@force_reinit_subscription**.  
  
4.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Geben Sie den Wert **Partition_options** für **@property** und den entsprechenden Wert für **@value**. Finden Sie unter [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) zur Definition dieser Filteroptionen.  
  
5.  (Optional) Starten Sie den Momentaufnahme-Agent, um, wenn notwendig, die Momentaufnahme erneut zu generieren. Informationen darüber, welche Änderungen erfordern eine neue Momentaufnahme generiert werden, finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## Siehe auch  
 [Automatisches Generieren einer Reihe von Joinfiltern zwischen Mergeartikeln & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md)   
 [Definieren und Ändern eines parametrisierten Zeilenfilters für einen Mergeartikel](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  