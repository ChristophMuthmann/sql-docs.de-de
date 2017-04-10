---
title: "Erstellen eines aktualisierbaren Abonnements f&#252;r eine Transaktionsver&#246;ffentlichung (Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "07/21/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "aktualisierbaren Transaktionsabonnements"
  - "aktualisierbaren Transaktionsabonnements SSMS"
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# Erstellen eines aktualisierbaren Abonnements f&#252;r eine Transaktionsver&#246;ffentlichung (Management Studio)

> [!NOTE]  
>  Dieses Feature wird in den Versionen von [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] von 2012 bis 2016 weiterhin unterstützt.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
Konfigurieren von aktualisierbaren Abonnements auf den **aktualisierbare Abonnements** auf der Seite der **Assistenten für neue Abonnements**. Diese Seite ist nur verfügbar, wenn Sie eine Transaktionsveröffentlichung für aktualisierbare Abonnements aktiviert haben. Weitere Informationen zum Aktivieren aktualisierbarer Abonnements finden Sie unter [Aktivieren Sie aktualisierbare Abonnements für Transaktionsveröffentlichungen](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).   
  
## So konfigurieren Sie ein aktualisierbares Abonnement vom Verleger aus  

1. Verbinden mit dem Verleger in Microsoft SQL Server Management Studio, und erweitern Sie dann den Serverknoten.

2. Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .

3. Mit der rechten Maustaste in einer Transaktionspublikation, die für aktualisierbare Abonnements aktiviert, und klicken Sie dann auf **neue Abonnements**.

4. Geben Sie auf den folgenden Seiten des Assistenten die Optionen für das Abonnement an. Geben Sie dabei z. B. an, wo der Verteilungs-Agent ausgeführt werden soll.

5. Auf der **aktualisierbare Abonnements** auf der Seite der **Assistenten für neue Abonnements**, stellen Sie sicher **replizieren** ausgewählt ist.

6. Wählen Sie eine Option aus der **Commit auf Verleger** Dropdown-Liste:

    * Um sofort aktualisierbare Abonnements verwenden möchten, wählen Sie **gleichzeitig Änderungen**. Wenn Sie diese Option auswählen und die Veröffentlichung Abonnements mit verzögerter Aktualisierung (Standard bei Veröffentlichungen mit dem Assistenten für neue Veröffentlichung erstellt wurden), kann die Abonnementeigenschaften **Update_mode** Wert **Failover**. Dieser Modus ermöglicht es Ihnen, bei Bedarf später zum Update über eine Warteschlange zu wechseln.

    * Wählen Sie zum Verwenden von Abonnements mit verzögerter Aktualisierung **Änderungen in die Warteschlange und commit**. Wenn Sie diese Option auswählen und die Veröffentlichung sofort aktualisierbare Abonnements (die Standardeinstellung für Veröffentlichungen, die mit dem Assistenten für neue Veröffentlichung erstellt) zulässt und dem Abonnenten, SQL Server 2005 oder höher wird die Abonnementeigenschaft ausgeführt wird **Update_mode** queued Failover festgelegt ist. Dieser Modus ermöglicht es Ihnen, bei Bedarf später zum sofortigen Update zu wechseln.

    Informationen zum Wechseln des Aktualisierungsmodus finden Sie unter [Switch zwischen aktualisieren-Modi für ein aktualisierbares Transaktionsabonnement](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

7. Die **Anmeldename für aktualisierbare Abonnements** angezeigt wird für Abonnements, die sofortiges Aktualisieren oder **Update_mode** festgelegt **Failover in der Warteschlange**. Auf der **Anmeldename für aktualisierbare Abonnements** Seite Geben Sie einen Verbindungsserver für die Verbindungen mit dem Verleger für sofort aktualisierbare Abonnements hergestellt werden. Die Verbindungen werden durch die Trigger verwendet, die auf dem Abonnenten ausgelöst werden und die Änderungen zum Verleger weitergeben. Wählen Sie eine der folgenden Optionen aus:

    * **Erstellen Sie einen Verbindungsserver, der die Verbindung mit SQL Server-Authentifizierung her.** Wählen Sie diese Option aus, wenn Sie keinen Remoteserver oder Verbindungsserver für die Verbindungen zwischen dem Abonnenten und dem Verleger definiert haben. Die Replikation erstellt dann einen Verbindungsserver für Sie. Das Konto, das Sie angeben, muss bereits auf dem Verleger vorhanden sein.

    * **Vordefinierten Verbindungsserver oder Remoteserver verwenden** Wählen Sie diese Option aus, wenn Sie, ein Remoteserver oder verknüpfter Server zwischen dem Abonnenten und dem Verleger mithilfe festgelegt haben [Sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [Sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio oder einer anderen Methode.

    Informationen zu den durch das verbindungsserverkonto erforderlichen Berechtigungen finden Sie unter der **aktualisierbare Abonnements in der Warteschlange** des [Geben Sie hier die linkbeschreibung](../../../relational-databases/replication/security/secure-the-subscriber.md).

8. Schließen Sie den Assistenten ab.

## So konfigurieren Sie ein aktualisierbares Abonnement vom Abonnenten aus


1. Verbinden mit dem Abonnenten in SQL Server Management Studio, und erweitern Sie dann den Serverknoten.

2. Erweitern Sie den Ordner **Replikation** .

3. Mit der rechten Maustaste die **Lokale Abonnements** Ordner, und klicken Sie dann auf **neue Abonnements**.

4. Auf der **Veröffentlichung** auf der Seite der **Assistenten für neue Abonnements**, Option **SQL Server-Verleger suchen** aus der **Publisher** Dropdown-Liste.

5. Stellen Sie im Dialogfeld **Verbindung mit Server herstellen** eine Verbindung mit dem Verleger her.

6. Wählen Sie eine transaktionsveröffentlichung für aktualisierbare Abonnements für die **Veröffentlichung** Seite.

7. Geben Sie auf den folgenden Seiten des Assistenten die Optionen für das Abonnement an. Geben Sie dabei z. B. an, wo der Verteilungs-Agent ausgeführt werden soll.

8. Auf der **aktualisierbare Abonnements** Seite des Assistenten für neue Abonnements sicher **replizieren** ausgewählt ist.

9. Wählen Sie eine Option aus der **Commit auf Verleger** Dropdown-Liste:

    * Um sofort aktualisierbare Abonnements verwenden möchten, wählen Sie **gleichzeitig Änderungen**. Wenn Sie diese Option auswählen und die Veröffentlichung Abonnements mit verzögerter Aktualisierung (Standard bei Veröffentlichungen mit dem Assistenten für neue Veröffentlichung erstellt wurden), kann die Abonnementeigenschaften **Update_mode** Wert **Failover**. Dieser Modus ermöglicht es Ihnen, bei Bedarf später zum Update über eine Warteschlange zu wechseln.

    * Wählen Sie zum Verwenden von Abonnements mit verzögerter Aktualisierung **Änderungen in die Warteschlange und commit**. Wenn Sie diese Option auswählen und die Veröffentlichung sofort aktualisierbare Abonnements (die Standardeinstellung für Veröffentlichungen, die mit dem Assistenten für neue Veröffentlichung erstellt) zulässt und dem Abonnenten, SQL Server 2005 oder höher wird die Abonnementeigenschaft ausgeführt wird **Update_mode** zu in der Warteschlange festgelegt **Failover**. Dieser Modus ermöglicht es Ihnen, bei Bedarf später zum sofortigen Update zu wechseln.

    Informationen zum Wechseln des Aktualisierungsmodus finden Sie unter [Switch zwischen aktualisieren-Modi für ein aktualisierbares Transaktionsabonnement](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

10. Die **Anmeldename für aktualisierbare Abonnements** angezeigt wird für Abonnements, die sofortiges Aktualisieren oder **Update_mode** Legen Sie in der Warteschlange zu **Failover**. Auf der **Anmeldename für aktualisierbare Abonnements** Seite Geben Sie einen Verbindungsserver für die Verbindungen mit dem Verleger für sofort aktualisierbare Abonnements hergestellt werden. Die Verbindungen werden durch die Trigger verwendet, die auf dem Abonnenten ausgelöst werden und die Änderungen zum Verleger weitergeben. Wählen Sie eine der folgenden Optionen aus:

    * **Erstellen Sie einen Verbindungsserver, der die Verbindung mit SQL Server-Authentifizierung her.** Wählen Sie diese Option aus, wenn Sie keinen Remoteserver oder Verbindungsserver für die Verbindungen zwischen dem Abonnenten und dem Verleger definiert haben. Die Replikation erstellt dann einen Verbindungsserver für Sie. Das Konto, das Sie angeben, muss bereits auf dem Verleger vorhanden sein.

    * **Vordefinierten Verbindungsserver oder Remoteserver verwenden** Wählen Sie diese Option aus, wenn Sie, ein Remoteserver oder verknüpfter Server zwischen dem Abonnenten und dem Verleger mithilfe festgelegt haben [Sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [Sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio oder einer anderen Methode.

    Informationen zu den durch das verbindungsserverkonto erforderlichen Berechtigungen finden Sie unter der **aktualisierbare Abonnements in der Warteschlange** des [Geben Sie hier die linkbeschreibung](../../../relational-databases/replication/security/secure-the-subscriber.md).

11. Schließen Sie den Assistenten ab.

## Siehe auch

[Aktualisierbare Abonnements für die Transaktionsreplikation](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md)

[Erstellen eines aktualisierbaren Abonnements für eine Transaktionsveröffentlichung mit T-SQL](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 
