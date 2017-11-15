---
title: "Festlegen des Ablaufdatums für Abonnements | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication], expiration
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- deactivating subscriptions
ms.assetid: 542f0613-5817-42d0-b841-fb2c94010665
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 92dd01ed14cb2f26f30cdcc2ac19ad8a44f80051
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="set-the-expiration-period-for-subscriptions"></a>Festlegen des Ablaufdatums für Abonnements
  In diesem Thema wird beschrieben, wie der Ablaufzeitraum für Abonnements in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]festgelegt wird. Der Ablaufzeitraum für Abonnements bestimmt den Zeitraum, bevor ein Abonnement abläuft und entfernt wird. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
-   **So legen Sie das Ablaufdatum für Abonnements fest mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Das Abonnementablaufdatum wird auch als *Beibehaltungsdauer*bezeichnet. Der Cleanup von Mergereplikationsmetadaten wird durch diese Einstellung bestimmt:  
  
    -   Die Replikation kann der Cleanup von Metadaten aus den Veröffentlichungs- und Abonnementdatenbanken erst ausführen, wenn das Ablaufdatum erreicht ist. Geben Sie keinen zu hohen Wert für die Beibehaltungsdauer an, da dies zu einer Beeinträchtigung der Replikationsleistung führen kann. Es wird empfohlen, eine niedrigere Einstellung zu verwenden, wenn Sie zuverlässig einschätzen können, dass alle Abonnenten innerhalb dieser Zeitspanne regelmäßig synchronisiert werden.  
  
         Die Beibehaltungsdauer für Mergeveröffentlichungen weist eine 24-stündige Kulanzfrist auf, um Abonnenten in unterschiedlichen Zeitzonen aufzunehmen. Wenn Sie beispielsweise eine Beibehaltungsdauer von einem Tag festgelegt haben, beträgt die tatsächliche Beibehaltungsdauer 48 Stunden.  
  
    -   Es ist möglich, anzugeben, dass Abonnements nie ablaufen. Es wird jedoch nachdrücklich empfohlen, diesen Wert nicht zu verwenden, da sonst kein Cleanup der Metadaten ausgeführt werden kann.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Geben Sie das Ablaufdatum von Abonnements im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** auf der Seite **Allgemein** an. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-set-the-expiration-period-for-subscriptions"></a>So legen Sie das Ablaufdatum für Abonnements fest  
  
1.  Geben Sie im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** auf der Seite **Allgemein** im Bereich **Ablaufdatum für das Abonnement** an, ob Abonnements ablaufen sollen.  
  
2.  Falls dies der Fall ist, geben Sie die Dauer an, nach der Abonnements ablaufen sollen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können gespeicherte Replikationsprozeduren dazu verwenden, diesen Wert festzulegen, wenn eine Veröffentlichung erstellt wird, und diesen Wert zu einem späteren Zeitpunkt zu ändern.  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>So legen Sie den Ablaufzeitraum eines Abonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung fest  
  
1.  Führen Sie auf dem Verleger [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)aus. Geben Sie den gewünschten Ablaufzeitraum für das Abonnement in Stunden für **@retention**festgelegt wird. Der Standardablaufzeitraum beträgt 336 Stunden. Weitere Informationen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>So legen Sie den Ablaufzeitraum eines Abonnements für eine Mergeveröffentlichung fest  
  
1.  Führen Sie auf dem Verleger [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)aus. Geben Sie den gewünschten Wert für den Ablaufzeitraum des Abonnements in Stunden für **@retention**festgelegt wird. Geben Sie die Einheiten, in denen der Ablaufzeitraum ausgedrückt wird, für **@retention_period_unit**an. Es stehen die folgenden Werte zur Auswahl:  
  
    -   **1** = Woche  
  
    -   **2** = Monat  
  
    -   **3** = Jahr  
  
     Der Standardablaufzeitraum beträgt 14 Tage. Weitere Informationen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>So ändern Sie den Ablaufzeitraum eines Abonnements für eine Momentaufnahme- oder eine Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)aus. Geben Sie **retention** für **@property** und den neuen Abonnementablaufzeitraum in Stunden für **@value**festgelegt wird.  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>So ändern Sie den Ablaufzeitraum eines Abonnements für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)aus, und geben Sie dazu **@publication** und **@publisher**festgelegt wird. Der Wert von **retention_period_unit** im Resultset ist einer der folgenden:  
  
    -   **0** = Tag  
  
    -   **1** = Woche  
  
    -   **2** = Monat  
  
    -   **3** = Jahr  
  
2.  Führen Sie auf dem Verleger [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)aus. Geben Sie **retention** für **@property** und den neuen Abonnementablaufzeitraum als Text, der auf der Einheit für die Beibehaltungsdauer aus Schritt 1 basiert, für **@value**festgelegt wird.  
  
3.  (Optional) Führen Sie auf dem Verleger [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)aus. Geben Sie **retention_period_unit** für **@property** und eine neue Einheit für den Abonnementablaufzeitraum für **@value**festgelegt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
