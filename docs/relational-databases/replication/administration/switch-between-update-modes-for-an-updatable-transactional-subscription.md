---
title: "Umschalten zwischen Updatemodi f&#252;r ein aktualisierbares Transaktionsabonnement | Microsoft Docs"
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
  - "Transaktionsreplikation, aktualisierbare Abonnements"
  - "Aktualisierbare Abonnements, Updatemodi"
  - "Abonnements [SQL Server-Replikation], aktualisierbar"
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Umschalten zwischen Updatemodi f&#252;r ein aktualisierbares Transaktionsabonnement
  In diesem Thema wird beschrieben, wie zwischen Updatemodi für ein aktualisierbares Transaktionsabonnement in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]umgeschaltet wird. Geben Sie im Assistenten für neue Abonnements den Modus für aktualisierbare Abonnements an. Informationen zum Festlegen des Modus bei der Verwendung dieses Assistenten finden Sie unter [anzeigen und ändern Sie Eigenschaften von Pullabonnement](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
-   **So schalten Sie zwischen Updatemodi für ein aktualisierbares Transaktionsabonnement um mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Sie können jederzeit ein Failover vom sofortigen Aktualisieren zum verzögerten Aktualisieren ausführen. Danach können Sie erst wieder zum sofortigen Aktualisieren wechseln, wenn der Abonnent und der Verleger verbunden sind und der Warteschlangenlese-Agent alle ausstehenden Nachrichten in der Warteschlange auf den Verleger angewendet hat.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wenn ein Abonnement mit Aktualisierung mit einer Transaktionsveröffentlichung ein Failover von einem Aktualisierungsmodus zu einem anderen unterstützt, können Sie programmgesteuert den Aktualisierungsmodus wechseln, um Situationen zu bewältigen, in denen sich die Verbindung für eine kurze Zeitdauer ändert. Der Updatemodus kann mithilfe gespeicherter Replikationsprozeduren programm- und bedarfsgesteuert festgelegt werden. Weitere Informationen finden Sie unter [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
> [!NOTE]  
>  Den Aktualisierungsmodus zu ändern, nachdem das Abonnement erstellt wird, die **Update_mode** Eigenschaft muss festgelegt werden, um **Failover** (wodurch Umschalten vom sofortigen Aktualisieren zum verzögerte Update) oder **in der Warteschlange Failover** (ermöglicht das Umschalten vom verzögerten Aktualisieren zum sofortigen Aktualisieren) Wenn das Abonnement erstellt wird. Diese Eigenschaften werden im Assistenten für neue Abonnements automatisch festgelegt.  
  
#### So legen Sie den Update für ein Pushabonnement fest  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Abonnements** .  
  
3.  Mit der rechten Maustaste des Abonnements für die Sie den Updatemodus festlegen, und klicken Sie dann auf möchten **Updatemethode festlegen**.  
  
4.  In der **Aktualisierungsmethode festlegen - \< Abonnent>: \< SubscriptionDatabase>** Wählen Sie im Dialogfeld **sofortigem** oder **Verzögertes Aktualisieren**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### So legen Sie den Updatemodus für ein Pullabonnement fest  
  
1.  In der **Abonnementeigenschaften - \< Publisher>: \< PublicationDatabase>** Wert wählen Sie im Dialogfeld **sofort replizieren** oder **ändert sich in die Warteschlange** für die **Aktualisierungsmethode für Abonnent** Option.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Weitere Informationen zum Zugreifen auf die **Abonnementeigenschaften - \< Publisher>: \< PublicationDatabase>** Dialogfeld finden Sie unter [anzeigen und ändern Sie Eigenschaften von Pullabonnement](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So wechseln Sie den Updatemodus  
  
1.  Stellen Sie sicher, dass das Abonnement Failover, indem unterstützt [Sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) für ein Pullabonnement oder [Sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) für ein Pushabonnement. Wenn der Wert des **Updatemodus** im Resultset **3** oder **4**ist, wird das Failover unterstützt.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md). Geben Sie **@publisher**, **@publisher_db**, **@publication**, und einen der folgenden Werte für **@failover_mode**:  
  
    -   **in der Warteschlange** -Failover zum verzögerten Aktualisieren, wenn die Verbindung vorübergehend unterbrochen wurde.  
  
    -   **sofortige** -Failover zum sofortigen Aktualisieren, wenn die Verbindung wiederhergestellt wurde.  
  
## Siehe auch  
 [Aktualisierbare Abonnements für die Transaktionsreplikation](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  