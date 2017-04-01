---
title: "Definieren und &#196;ndern eines Spaltenfilters | Microsoft Docs"
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
  - "Filter [SQL Server-Replikation], Spalte"
  - "Ändern von Filtern, Spalte"
  - "Ändern von Filtern"
  - "Spaltenfilter [SQL Server-Replikation]"
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Definieren und &#196;ndern eines Spaltenfilters
  In diesem Thema wird beschrieben, wie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]Spaltenfilter definiert und geändert werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So definieren und ändern Sie einen Spaltenfilter mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Einige Spalten können nicht gefiltert werden. Weitere Informationen finden Sie unter [veröffentlichten Filterdaten](../../../relational-databases/replication/publish/filter-published-data.md). Wenn Sie einen Spaltenfilter ändern, nachdem Abonnements initialisiert wurden, müssen Sie eine neue Momentaufnahme generieren. Außerdem müssen nach der Änderung alle Abonnements erneut initialisiert werden. Weitere Informationen zu den Anforderungen für eigenschaftenänderungen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Spaltenfilter werden auf der Seite **Artikel** des Assistenten für neue Veröffentlichung definiert. Weitere Informationen zum Verwenden des Assistenten für neue Veröffentlichung finden Sie unter [Erstellen einer Publikation](../../../relational-databases/replication/publish/create-a-publication.md).  
  
 Definieren und Ändern der Spaltenfilter auf die **Artikel** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zu Veröffentlichungs- und Artikeleigenschaften finden Sie unter [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So definieren Sie einen Spaltenfilter  
  
1.  Erweitern Sie im Bereich **Zu veröffentlichende Objekte** auf der Seite **Artikel** des Assistenten für neue Veröffentlichung die zu filternde Tabelle.  
  
2.  Klicken Sie auf die Kontrollkästchen für alle Spalten, die herausgefiltert werden sollen, um deren Markierung aufzuheben.  
  
#### So ändern Sie die Spaltenfilterung  
  
1.  Auf der **Artikel** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld erweitern zu filternde Tabelle die **zu veröffentlichende Objekte** Bereich.  
  
2.  Klicken Sie auf die Kontrollkästchen für alle Spalten, die herausgefiltert werden sollen, um deren Markierung aufzuheben, und stellen Sie sicher, dass die Kontrollkästchen für die Spalten, die im Artikel enthalten sein sollen, markiert sind.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Während der Erstellung von Tabellenartikeln können Sie definieren, welche Spalten in den Artikel aufgenommen werden sollen. Nachdem der Artikel definiert wurde, können Sie die Spalten noch ändern. Gefilterte Spalten können mithilfe gespeicherter Replikationsprozeduren programmgesteuert definiert und geändert werden.  
  
> [!NOTE]  
>  Im Folgenden wird davon ausgegangen, dass sich die zugrunde liegende Tabelle nicht geändert hat. Informationen zur Replikation von Änderungen der Datendefinitionssprache (DDL) an veröffentlichten Tabellen finden Sie unter [vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
#### So definieren Sie einen Spaltenfilter für einen in einer Momentaufnahme- oder einer Transaktionsveröffentlichung veröffentlichten Artikel  
  
1.  Definieren Sie den zu filternden Artikel. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Damit werden die Spalten definiert, die in den Artikel aufgenommen oder daraus entfernt werden sollen.  
  
    -   Wenn nur wenige Spalten aus einer Tabelle mit vielen Spalten zu veröffentlichen, führen Sie [Sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) einmal für jede hinzuzufügende Spalte. Geben Sie den Spaltennamen für **@column** und den Wert **add** für **@operation**an.  
  
    -   Wenn die meisten Spalten in einer Tabelle mit vielen Spalten zu veröffentlichen, führen Sie [Sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), Angabe des Werts **null** für **@column** und einem Wert von **Hinzufügen** für **@operation** um alle Spalten hinzuzufügen. Führen Sie dann [Sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), sobald die Angabe des Werts für die einzelnen Spalten ausgeschlossen, **Löschen** für **@operation** und den Namen der auszuschließenden Spalte für **@column**.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Geben Sie den Namen der Veröffentlichung für **@publication** und den Namen des gefilterten Artikels für **@article**an. Damit werden die Synchronisierungsobjekte für den gefilterten Artikel erstellt.  
  
#### So ändern Sie einen Spaltenfilter, um zusätzliche Spalten in einen Artikel aufzunehmen, der in einer Momentaufnahme- oder Transaktionsveröffentlichung veröffentlicht wurde  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) einmal für jede hinzuzufügende Spalte. Geben Sie den Spaltennamen für **@column** und den Wert **add** für **@operation**an.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Geben Sie den Namen der Veröffentlichung für **@publication** und den Namen des gefilterten Artikels für **@article**an. Wenn die Veröffentlichung Abonnements vorhanden sind, geben Sie den Wert **1** für **@change_active**. Damit werden die Synchronisierungsobjekte für den gefilterten Artikel erneut erstellt.  
  
3.  Führen Sie den Auftrag des Momentaufnahme-Agents für die Veröffentlichung erneut aus, um eine aktualisierte Momentaufnahme zu erstellen.  
  
4.  Erneutes Initialisieren von Abonnements Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### So ändern Sie einen Spaltenfilter, um Spalten aus einem Artikel zu entfernen, der in einer Momentaufnahme- oder Transaktionsveröffentlichung veröffentlicht wurde  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) einmal für jede Spalte, die entfernt wird. Geben Sie den Spaltennamen für **@column** und den Wert **drop** für **@operation**an.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Geben Sie den Namen der Veröffentlichung für **@publication** und den Namen des gefilterten Artikels für **@article**an. Wenn die Veröffentlichung Abonnements vorhanden sind, geben Sie den Wert **1** für **@change_active**. Damit werden die Synchronisierungsobjekte für den gefilterten Artikel erneut erstellt.  
  
3.  Führen Sie den Auftrag des Momentaufnahme-Agents für die Veröffentlichung erneut aus, um eine aktualisierte Momentaufnahme zu erstellen.  
  
4.  Erneutes Initialisieren von Abonnements Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### So definieren Sie einen Spaltenfilter für einen Artikel, der in einer Mergeveröffentlichung veröffentlicht wurde  
  
1.  Definieren Sie den zu filternden Artikel. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md). Damit werden die Spalten definiert, die in den Artikel aufgenommen oder daraus entfernt werden sollen.  
  
    -   Wenn nur wenige Spalten aus einer Tabelle mit vielen Spalten zu veröffentlichen, führen Sie [Sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) einmal für jede hinzuzufügende Spalte. Geben Sie den Spaltennamen für **@column** und den Wert **add** für **@operation**an.  
  
    -   Wenn die meisten Spalten in einer Tabelle mit vielen Spalten zu veröffentlichen, führen Sie [Sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), Angabe des Werts **null** für **@column** und einem Wert von **Hinzufügen** für **@operation** um alle Spalten hinzuzufügen. Führen Sie dann [Sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), sobald die Angabe des Werts für die einzelnen Spalten ausgeschlossen, **Löschen** für **@operation** und den Namen der auszuschließenden Spalte für **@column**.  
  
#### So ändern Sie einen Spaltenfilter, um zusätzliche Spalten in einen Artikel aufzunehmen, der in einer Mergeveröffentlichung veröffentlicht wurde  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) einmal für jede hinzuzufügende Spalte. Geben Sie den Spaltennamen für **@column**, ein Wert von **Hinzufügen** für **@operation** und einem Wert von **1** für beide **@force_invalidate_snapshot** und **@force_reinit_subscription**.  
  
2.  Führen Sie den Auftrag des Momentaufnahme-Agents für die Veröffentlichung erneut aus, um eine aktualisierte Momentaufnahme zu erstellen.  
  
3.  Erneutes Initialisieren von Abonnements Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### So ändern Sie einen Spaltenfilter, um Spalten aus einem Artikel zu entfernen, der in einer Mergeveröffentlichung veröffentlicht wurde  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) einmal für jede Spalte, die entfernt wird. Geben Sie den Spaltennamen für **@column**, den Wert **Löschen** für **@operation** und einem Wert von **1** für beide **@force_invalidate_snapshot** und **@force_reinit_subscription**.  
  
2.  Führen Sie den Auftrag des Momentaufnahme-Agents für die Veröffentlichung erneut aus, um eine aktualisierte Momentaufnahme zu erstellen.  
  
3.  Erneutes Initialisieren von Abonnements Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel für Transaktionsreplikation wird die Spalte `DaysToManufacture` aus einem Artikel entfernt, der auf der Tabelle `Product` basiert.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_1.sql)]  
  
 In diesem Beispiel für eine Mergereplikation wird die Spalte `CreditCardApprovalCode` aus einem Artikel entfernt, der auf der Tabelle `SalesOrderHeader` basiert.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_2.sql)]  
  
## Siehe auch  
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtern veröffentlichter Daten für die Mergereplikation](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  