---
title: "Erstellen von aktualisierbaren Abonnements für eine Transaktionsveröffentlichung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updatable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: df91026bb1204d99d3e34e0d08603beba9c3bfef
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication"></a>Erstellen von aktualisierbaren Abonnements für eine Transaktionsveröffentlichung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
> [!NOTE]  
>  Dieses Feature wird in den Versionen von [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] von 2012 bis 2016 weiterhin unterstützt.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
Zum Konfigurieren aktualisierbarer Abonnements steht Ihnen die Seite **Aktualisierbare Abonnements** des **Assistenten für neue Abonnements** zur Verfügung. Diese Seite ist nur verfügbar, wenn Sie eine Transaktionsveröffentlichung für aktualisierbare Abonnements aktiviert haben. Weitere Informationen zum Aktivieren aktualisierbarer Abonnements finden Sie unter [Aktivieren des Aktualisierens von Abonnements für Transaktionsveröffentlichungen](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).   
  
## <a name="to-configure-an-updatable-subscription-from-the-publisher"></a>So konfigurieren Sie ein aktualisierbares Abonnement vom Verleger aus  

1. Stellen Sie mit dem Verleger in Microsoft SQL Server Management Studio eine Verbindung her, und erweitern Sie dann den Serverknoten.

2. Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .

3. Klicken Sie mit der rechten Maustaste auf eine Transaktionsveröffentlichung, die für aktualisierbare Abonnements aktiviert ist, und klicken Sie dann auf **Neue Abonnements**.

4. Geben Sie auf den folgenden Seiten des Assistenten die Optionen für das Abonnement an. Geben Sie dabei z. B. an, wo der Verteilungs-Agent ausgeführt werden soll.

5. Kontrollieren Sie auf der Seite **Aktualisierbare Abonnements** des **Assistenten für neue Veröffentlichung**, dass die Option **Replizieren** aktiviert ist.

6. Wählen Sie in der Dropdownliste **Commit auf Verleger ausführen** eine Option aus:

    * Wenn Sie Abonnements mit sofortigem Update verwenden möchten, aktivieren Sie die Option **Commit für Änderungen gleichzeitig ausführen**. Wenn Sie diese Option aktivieren und die Veröffentlichung Abonnements mit verzögertem Update über eine Warteschlange zulässt (Standardkonfiguration bei Veröffentlichungen, die im Assistenten für neue Veröffentlichung erstellt wurden), wird für die **update_mode**-Abonnementeigenschaft **failover** festgelegt. Dieser Modus ermöglicht es Ihnen, bei Bedarf später zum Update über eine Warteschlange zu wechseln.

    * Wenn Sie Abonnements mit verzögertem Update über eine Warteschlange verwenden möchten, aktivieren Sie die Option **Änderungen in die Warteschlange einreihen und Commit baldmöglichst ausführen**. Wenn Sie diese Option aktivieren, die Veröffentlichung Abonnements mit sofortigem Update zulässt (Standardkonfiguration bei Veröffentlichungen, die im Assistenten für neue Veröffentlichung erstellt wurden) und auf dem Abonnenten SQL Server 2005 oder eine höhere Version ausgeführt wird, wird für die **update_mode**-Abonnementeigenschaft die Einstellung „queued failover“ festgelegt. Dieser Modus ermöglicht es Ihnen, bei Bedarf später zum sofortigen Update zu wechseln.

    Weitere Informationen zum Umschalten zwischen den Updatemodi finden Sie unter [Umschalten zwischen Updatemodi für ein aktualisierbares Transaktionsabonnement](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

7. Bei Abonnements, die das sofortige Update verwenden oder bei denen für **update_mode** die Einstellung **queued failover** festgelegt ist, wird die Seite **Anmeldename für aktualisierbare Abonnements** angezeigt. Geben Sie auf der Seite **Anmeldename für aktualisierbare Abonnements** einen Verbindungsserver an, über den die Verbindungen mit dem Verleger für Abonnements mit sofortigem Update hergestellt werden sollen. Die Verbindungen werden durch die Trigger verwendet, die auf dem Abonnenten ausgelöst werden und die Änderungen zum Verleger weitergeben. Wählen Sie eine der folgenden Optionen aus:

    * **Verbindungsserver erstellen, der mithilfe der SQL Server-Authentifizierung eine Verbindung herstellt.** Wählen Sie diese Option aus, wenn Sie keinen Remoteserver oder Verbindungsserver für die Verbindungen zwischen dem Abonnenten und dem Verleger definiert haben. Die Replikation erstellt dann einen Verbindungsserver für Sie. Das Konto, das Sie angeben, muss bereits auf dem Verleger vorhanden sein.

    * **Vordefinierten Verbindungsserver oder Remoteserver verwenden** Wählen Sie diese Option aus, wenn Sie einen Remoteserver oder Verbindungsserver zwischen dem Abonnenten und dem Verleger mithilfe von [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio oder einer anderen Methode definiert haben.

    Informationen zu den Berechtigungen, die das Verbindungsserverkonto benötigt, finden Sie unter **Abonnements mit verzögertem Update über eine Warteschlange** unter [Hier Linkbeschreibung eingeben](../../../relational-databases/replication/security/secure-the-subscriber.md).

8. Schließen Sie den Assistenten ab.

## <a name="to-configure-an-updatable-subscription-from-the-subscriber"></a>So konfigurieren Sie ein aktualisierbares Abonnement vom Abonnenten aus


1. Stellen Sie mit dem Abonnenten in SQL Server Management Studio eine Verbindung her, und erweitern Sie dann den Serverknoten.

2. Erweitern Sie den Ordner **Replikation** .

3. Klicken Sie mit der rechten Maustaste auf den Ordner **Lokale Abonnements** , und klicken Sie dann auf **Neue Abonnements**.

4. Aktivieren Sie auf der Seite **Veröffentlichung** des **Assistenten für neue Abonnements** in der Dropdownliste **Verleger** die Option **SQL Server-Verleger suchen**.

5. Stellen Sie im Dialogfeld **Verbindung mit Server herstellen** eine Verbindung mit dem Verleger her.

6. Wählen Sie auf der Seite **Veröffentlichung** eine für aktualisierbare Abonnements aktivierte Transaktionsveröffentlichung aus.

7. Geben Sie auf den folgenden Seiten des Assistenten die Optionen für das Abonnement an. Geben Sie dabei z. B. an, wo der Verteilungs-Agent ausgeführt werden soll.

8. Kontrollieren Sie auf der Seite **Aktualisierbare Abonnements** des Assistenten für neue Veröffentlichung, dass die Option **Replizieren** aktiviert ist.

9. Wählen Sie in der Dropdownliste **Commit auf Verleger ausführen** eine Option aus:

    * Wenn Sie Abonnements mit sofortigem Update verwenden möchten, aktivieren Sie die Option **Commit für Änderungen gleichzeitig ausführen**. Wenn Sie diese Option aktivieren und die Veröffentlichung Abonnements mit verzögertem Update über eine Warteschlange zulässt (Standardkonfiguration bei Veröffentlichungen, die im Assistenten für neue Veröffentlichung erstellt wurden), wird für die **update_mode**-Abonnementeigenschaft **failover** festgelegt. Dieser Modus ermöglicht es Ihnen, bei Bedarf später zum Update über eine Warteschlange zu wechseln.

    * Wenn Sie Abonnements mit verzögertem Update über eine Warteschlange verwenden möchten, aktivieren Sie die Option **Änderungen in die Warteschlange einreihen und Commit baldmöglichst ausführen**. Wenn Sie diese Option aktivieren, die Veröffentlichung Abonnements mit sofortigem Update zulässt (Standardkonfiguration bei Veröffentlichungen, die im Assistenten für neue Veröffentlichung erstellt wurden) und auf dem Abonnenten SQL Server 2005 oder eine höhere Version ausgeführt wird, wird für die **update_mode**-Abonnementeigenschaft die Einstellung queued **failover** festgelegt. Dieser Modus ermöglicht es Ihnen, bei Bedarf später zum sofortigen Update zu wechseln.

    Weitere Informationen zum Umschalten zwischen den Updatemodi finden Sie unter [Umschalten zwischen Updatemodi für ein aktualisierbares Transaktionsabonnement](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

10. Bei Abonnements, die das sofortige Update verwenden oder bei denen für **update_mode** die Einstellung queued **failover** festgelegt ist, wird die Seite **Anmeldename für aktualisierbare Abonnements** angezeigt. Geben Sie auf der Seite **Anmeldename für aktualisierbare Abonnements** einen Verbindungsserver an, über den die Verbindungen mit dem Verleger für Abonnements mit sofortigem Update hergestellt werden sollen. Die Verbindungen werden durch die Trigger verwendet, die auf dem Abonnenten ausgelöst werden und die Änderungen zum Verleger weitergeben. Wählen Sie eine der folgenden Optionen aus:

    * **Verbindungsserver erstellen, der mithilfe der SQL Server-Authentifizierung eine Verbindung herstellt.** Wählen Sie diese Option aus, wenn Sie keinen Remoteserver oder Verbindungsserver für die Verbindungen zwischen dem Abonnenten und dem Verleger definiert haben. Die Replikation erstellt dann einen Verbindungsserver für Sie. Das Konto, das Sie angeben, muss bereits auf dem Verleger vorhanden sein.

    * **Vordefinierten Verbindungsserver oder Remoteserver verwenden** Wählen Sie diese Option aus, wenn Sie einen Remoteserver oder Verbindungsserver zwischen dem Abonnenten und dem Verleger mithilfe von [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio oder einer anderen Methode definiert haben.

    Informationen zu den Berechtigungen, die das Verbindungsserverkonto benötigt, finden Sie unter **Abonnements mit verzögertem Update über eine Warteschlange** unter [Hier Linkbeschreibung eingeben](../../../relational-databases/replication/security/secure-the-subscriber.md).

11. Schließen Sie den Assistenten ab.

## <a name="see-also"></a>Weitere Informationen finden Sie unter

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)

[Erstellen eines aktualisierbaren Abonnements für eine Transaktionsveröffentlichung mit T-SQL](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 

