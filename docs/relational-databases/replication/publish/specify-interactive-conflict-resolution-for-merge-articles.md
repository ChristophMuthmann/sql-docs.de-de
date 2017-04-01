---
title: "Angeben von interaktiver Konfliktaufl&#246;sung von Mergeartikeln | Microsoft Docs"
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
  - "Konfliktlösung bei der Mergereplikation [SQL Server-Replikation], interaktive Konfliktlöser"
  - "Interaktive Konfliktlösung [SQL Server-Replikation]"
  - "Artikel [SQL Server-Replikation], Konfliktlösung"
  - "Konfliktlösung [SQL Server-Replikation], Mergereplikation "
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Angeben von interaktiver Konfliktaufl&#246;sung von Mergeartikeln
  In diesem Thema wird beschrieben, wie die interaktive Konfliktauflösung von Mergeartikeln in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]angegeben wird.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die Replikation bietet eine interaktive Konfliktlöser, können Sie zum manuellen Beheben von Konflikten während der bedarfsgesteuerten Synchronisierung in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Synchronisierungsverwaltung von Windows. Wenn Sie die interaktive Konfliktlösung aktiviert haben, können Sie Konflikte mithilfe des interaktiven Konfliktlösers interaktiv lösen. Der interaktive Konfliktlöser ist über die Synchronisierungsverwaltung von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows verfügbar. Weitere Informationen finden Sie unter [synchronisieren Sie ein Abonnement mithilfe von Windows Synchronization Manager & #40; Windows-Synchronisierungs-Manager & #41;](../../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
-   **So geben Sie die interaktive Konfliktauflösung von Mergeartikeln an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wenn die Synchronisierung nicht im Rahmen der Synchronisierungsverwaltung von Windows erfolgt (sondern als geplante Synchronisierung oder als bedarfsgesteuerte Synchronisierung in SQL Server Management Studio oder im Replikationsmonitor), werden Konflikte ohne Benutzereingriff automatisch entsprechend der Standardkonfliktlösung gelöst, die für den Artikel angegeben ist. Weitere Informationen finden Sie unter [Interactive Conflict Resolution](../../../relational-databases/replication/merge/interactive-conflict-resolution.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So aktivieren Sie die interaktive Konfliktlösung für einen Artikel  
  
1.  Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld Wählen Sie eine Tabelle aus. Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
2.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Tabellenartikels festlegen** bzw. **Eigenschaften aller Tabellenartikel festlegen**.  
  
3.  Auf der **Artikeleigenschaften - \< Artikel>** oder **Artikeleigenschaften - \< ArticleType>** auf der **Konfliktlöser** Registerkarte.  
  
4.  Wählen Sie **Abonnent Konflikte während bedarfsgesteuerter Synchronisierungen interaktiv löst**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
#### So geben Sie an, dass ein Abonnement die interaktive Konfliktlösung verwendet  
  
1.  In der **Abonnementeigenschaften - \< Abonnent>: \< SubscriptionDatabase>** Dialogfeld geben den Wert **True** für die **Konflikte interaktiv lösen** Option. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) und [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können programmgesteuert angeben, dass ein Abonnent diese grafische Benutzeroberfläche zur Auflösung von Artikelkonflikten verwendet, wenn ein Pullabonnement für eine Mergeveröffentlichung erstellt wird. Im interaktiven Konfliktlöser werden nur Konflikte in Artikeln, die diese Option unterstützen, angezeigt.  
  
#### So erstellen Sie ein Mergepullabonnement, das den interaktiven Konfliktlöser verwendet  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), wobei **@publication**. Beachten Sie den Wert der **Allow_interactive_resolver** für jeden Artikel im Resultset für das der interaktive Konfliktlöser verwendet wird.  
  
    -   Wenn dieser Wert **1**lautet, wird der Interaktive Konfliktlöser verwendet.  
  
    -   Wenn dieser Wert **0**lautet, müssen Sie zuerst den interaktiven Konfliktlöser für jeden Artikel aktivieren. Führen Sie hierzu [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), wobei **@publication**, **@article**, Wert **Allow_interactive_resolver** für **@property**, und der Wert **true** für **@value**.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Weitere Informationen finden Sie unter [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md), geben Sie die folgenden Parameter:  
  
    -   **@publisher**, **@publisher_db** (die veröffentlichte Datenbank) und **@publication**.  
  
    -   Der Wert **true** für **@enabled_for_syncmgr**.  
  
    -   Der Wert **true** für **@use_interactive_resolver**.  
  
    -   Die für den Merge-Agent erforderlichen Sicherheitskontoinformationen. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md).  
  
#### So definieren Sie einen Artikel, der den interaktiven Konfliktlöser unterstützt  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel, für die gehört **@publication**, einen Namen für den Artikel für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, und der Wert **true** für **@allow_interactive_resolver**. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## Siehe auch  
 [Anzeigen und Lösen von Datenkonflikten für Mergeveröffentlichungen & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/view and resolve data conflicts for merge publications.md)   
 [Interaktive Konfliktlösung](../../../relational-databases/replication/merge/interactive-conflict-resolution.md)  
  
  