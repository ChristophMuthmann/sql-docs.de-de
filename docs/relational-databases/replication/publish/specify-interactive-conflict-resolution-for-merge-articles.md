---
title: "Angeben von interaktiver Konfliktauflösung von Mergeartikeln | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], interactive resolvers
- interactive conflict resolution [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d488371a34cefb0ecf73824e362137243c115926
ms.lasthandoff: 04/11/2017

---
# <a name="specify-interactive-conflict-resolution-for-merge-articles"></a>Angeben von interaktiver Konfliktauflösung von Mergeartikeln
  In diesem Thema wird beschrieben, wie die interaktive Konfliktauflösung von Mergeartikeln in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]angegeben wird.  
  
 In der[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Replikation steht ein interaktiver Konfliktlöser zur Verfügung, mit dem Sie Konflikte bei einer bedarfsgesteuerten Synchronisierung in der Synchronisierungsverwaltung von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows manuell lösen können. Wenn Sie die interaktive Konfliktlösung aktiviert haben, können Sie Konflikte mithilfe des interaktiven Konfliktlösers interaktiv lösen. Der interaktive Konfliktlöser ist über die Synchronisierungsverwaltung von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows verfügbar. Weitere Informationen finden Sie unter [Synchronisieren eines Abonnements mithilfe der Synchronisierungsverwaltung von Windows &#40;Synchronisierungsverwaltung von Windows&#41;](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
-   **So geben Sie die interaktive Konfliktauflösung von Mergeartikeln an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wenn die Synchronisierung nicht im Rahmen der Synchronisierungsverwaltung von Windows erfolgt (sondern als geplante Synchronisierung oder als bedarfsgesteuerte Synchronisierung in SQL Server Management Studio oder im Replikationsmonitor), werden Konflikte ohne Benutzereingriff automatisch entsprechend der Standardkonfliktlösung gelöst, die für den Artikel angegeben ist. Weitere Informationen finden Sie unter [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-enable-interactive-conflict-resolution-for-an-article"></a>So aktivieren Sie die interaktive Konfliktlösung für einen Artikel  
  
1.  Wählen Sie auf der Seite **Artikel** des Assistenten für neue Veröffentlichung bzw. des Dialogfelds **Veröffentlichungseigenschaften - \<Veröffentlichung>** eine Tabelle aus. Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
2.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Tabellenartikels festlegen** bzw. **Eigenschaften aller Tabellenartikel festlegen**.  
  
3.  Klicken Sie auf der Seite **Artikeleigenschaften - \<Article>** bzw. **Artikeleigenschaften - \<ArticleType>** auf die Registerkarte **Konfliktlöser**.  
  
4.  Aktivieren Sie die Option **Zulassen, dass der Abonnent Konflikte während bedarfsgesteuerter Synchronisierungen interaktiv löst**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Wenn Sie sich im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** befinden, klicken Sie auf **OK**, um eine Speicherung vorzunehmen und das Dialogfeld zu schließen.  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>So geben Sie an, dass ein Abonnement die interaktive Konfliktlösung verwendet  
  
1.  Geben Sie im Dialogfeld **Abonnementeigenschaften - \<Subscriber>: \<SubscriptionDatabase>** für die Option **Konflikte interaktiv lösen** den Wert **Wahr** an. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) und [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können programmgesteuert angeben, dass ein Abonnent diese grafische Benutzeroberfläche zur Auflösung von Artikelkonflikten verwendet, wenn ein Pullabonnement für eine Mergeveröffentlichung erstellt wird. Im interaktiven Konfliktlöser werden nur Konflikte in Artikeln, die diese Option unterstützen, angezeigt.  
  
#### <a name="to-create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>So erstellen Sie ein Mergepullabonnement, das den interaktiven Konfliktlöser verwendet  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)unter Angabe von **@publication**angegeben wird. Betrachten Sie den Wert von **allow_interactive_resolver** für jeden Artikel im Resultset, für das der interaktive Konfliktlöser verwendet wird.  
  
    -   Wenn dieser Wert **1**lautet, wird der Interaktive Konfliktlöser verwendet.  
  
    -   Wenn dieser Wert **0**lautet, müssen Sie zuerst den interaktiven Konfliktlöser für jeden Artikel aktivieren. Hierzu führen Sie [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)unter Angabe von **@publication**, **@article**, dem Wert **allow_interactive_resolver** für **@property**und dem Wert **true** für **@value**angegeben wird.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)aus. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  Führen Sie auf dem Abonnenten für die Abonnentendatenbank [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)aus, und geben Sie die folgenden Parameter an:  
  
    -   **@publisher**, **@publisher_db** (die veröffentlichte Datenbank) und **@publication**angegeben wird.  
  
    -   Den Wert **true** für **@enabled_for_syncmgr**angegeben wird.  
  
    -   Den Wert **true** für **@use_interactive_resolver**angegeben wird.  
  
    -   Die für den Merge-Agent erforderlichen Sicherheitskontoinformationen. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)aus.  
  
#### <a name="to-define-an-article-that-supports-the-interactive-resolver"></a>So definieren Sie einen Artikel, der den interaktiven Konfliktlöser unterstützt  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication**, den Namen des Artikels für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**und dem Wert **true** für **@allow_interactive_resolver**angegeben wird. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Lösen von Datenkonflikten für Mergeveröffentlichungen &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
  
