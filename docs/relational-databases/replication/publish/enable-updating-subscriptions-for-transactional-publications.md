---
title: "Aktivieren des Aktualisierens von Abonnements für Transaktionsveröffentlichungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, enabling
- subscriptions [SQL Server replication], updatable
ms.assetid: 539d5bb0-b808-4d8c-baf4-cb6d32d2c595
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 37269f8738b6020ce6d05501251161f8c40c3c9b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="enable-updating-subscriptions-for-transactional-publications"></a>Aktivieren des Aktualisierens von Abonnements für Transaktionsveröffentlichungen
  In diesem Thema wird beschrieben, wie das Aktualisieren von Abonnements für Transaktionsveröffentlichungen in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]aktiviert wird.  
  
> **HINWEIS!** [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  

##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
 Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Aktivieren Sie aktualisierbare Abonnements für Transaktionsveröffentlichungen auf der Seite **Veröffentlichungstyp** des Assistenten für neue Veröffentlichung.  
  
 Um aktualisierbare Abonnements verwenden zu können, müssen auch im Assistenten für neue Abonnements Optionen konfiguriert werden.  
  
#### <a name="to-enable-updating-subscriptions"></a>So aktivieren Sie aktualisierbare Abonnements  
  
1.  Wählen Sie im Assistenten für neue Veröffentlichung auf der Seite **Veröffentlichungstyp** die Option **Transaktionsveröffentlichung mit aktualisierbaren Abonnements**aus.  
  
2.  Geben Sie auf der Seite **Agentsicherheit** neben den Sicherheitseinstellungen für den Momentaufnahme-Agent und den Protokolllese-Agent auch die Sicherheitseinstellungen für den Warteschlangenlese-Agent an. Weitere Informationen zu den Berechtigungen, die für das Konto erforderlich sind, unter dem der Warteschlangenlese-Agent ausgeführt wird, finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    > **HINWEIS:** Der Warteschlangenlese-Agent wird auch dann konfiguriert, wenn Sie lediglich Abonnements mit sofortigem Update verwenden.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Wenn Sie mithilfe von gespeicherten Replikationsprozeduren programmgesteuert eine Transaktionsveröffentlichung erstellen, können Sie das sofortige oder das verzögerte Aktualisieren der Abonnements aktivieren.  
  
#### <a name="to-create-a-publication-that-supports-immediate-updating-subscriptions"></a>So erstellen Sie eine Veröffentlichung, die Abonnements mit sofortigem Update unterstützt  
  
1.  Erstellen Sie, falls notwendig, einen Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank.  
  
    -   Wenn bereits ein Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank vorhanden ist, fahren Sie mit Schritt 2 fort.  
  
    -   Wenn Sie sich nicht sicher sind, ob ein Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank vorhanden ist, dann führen Sie [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Wenn das Resultset leer ist, muss ein Protokolllese-Agentauftrag erstellt werden.  
  
    -   Führen Sie auf dem Verleger [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) aus. Geben Sie die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] -Anmeldeinformationen, unter denen der Agent ausgeführt wird, für **@job_name** und **@password**aktiviert wird. Wenn der Agent zum Herstellen der Verbindung mit dem Verleger die SQL Server-Authentifizierung verwendet, müssen Sie zudem den Wert **0** für **@publisher_security_mode** und die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für **@publisher_login** und **@publisher_password**aktiviert wird.  
  
2.  Führen Sie [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) aus, und geben Sie den Wert **TRUE** für den Parameter **@allow_sync_tran** an.  
  
3.  Führen Sie auf dem Verleger [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) aus. Geben Sie den in Schritt 2 für **@publication** verwendeten Veröffentlichungsnamen und die Windows-Anmeldeinformationen, unter denen der Momentaufnahme-Agent ausgeführt wird, für **@job_name** und **@password**aktiviert wird. Wenn der Agent zum Herstellen der Verbindung mit dem Verleger die SQL Server-Authentifizierung verwendet, müssen Sie zudem den Wert **0** für **@publisher_security_mode** und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für **@publisher_login** und **@publisher_password**aktiviert wird. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
4.  Fügen Sie der Veröffentlichung Artikel hinzu. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
5.  Erstellen Sie auf dem Abonnenten ein Abonnement mit Update für diese Veröffentlichung.   
  
#### <a name="to-create-a-publication-that-supports-queued-updating-subscriptions"></a>So erstellen Sie eine Veröffentlichung, die Abonnements mit verzögertem Update über eine Warteschlange unterstützt  
  
1.  Erstellen Sie, falls notwendig, einen Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank.  
  
    -   Wenn bereits ein Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank vorhanden ist, fahren Sie mit Schritt 2 fort.  
  
    -   Wenn Sie sich nicht sicher sind, ob ein Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank vorhanden ist, dann führen Sie [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Wenn das Resultset leer ist, muss ein Protokolllese-Agentauftrag erstellt werden.  
  
    -   Führen Sie auf dem Verleger [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) aus. Geben Sie die Windows-Anmeldeinformationen, unter denen der Agent ausgeführt wird, für **@job_name** und **@password**aktiviert wird. Wenn der Agent zum Herstellen der Verbindung mit dem Verleger die SQL Server-Authentifizierung verwendet, müssen Sie zudem den Wert **0** für **@publisher_security_mode** und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für **@publisher_login** und **@publisher_password**aktiviert wird.  
  
2.  Erstellen Sie, falls notwendig, einen Warteschlangenlese-Agentauftrag für den Verteiler.  
  
    -   Wenn bereits ein Warteschlangenlese-Agentauftrag für die Verteilungsdatenbank vorhanden ist, fahren Sie mit Schritt 3 fort.  
  
    -   Wenn Sie sich nicht sicher sind, ob ein Warteschlangenlese-Agentauftrag für die Verteilungsdatenbank vorhanden ist, dann führen Sie [sp_helpqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md) auf dem Verteiler für die Verteilungsdatenbank aus. Wenn das Resultset leer ist, muss ein Warteschlangenlese-Agentauftrag erstellt werden.  
  
    -   Führen Sie auf dem Verteiler [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) aus. Geben Sie die Windows-Anmeldeinformationen, unter denen der Agent ausgeführt wird, für **@job_name** und **@password**aktiviert wird. Diese Anmeldeinformationen werden verwendet, wenn der Warteschlangenlese-Agent eine Verbindung mit dem Verleger und dem Abonnenten herstellt. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
3.  Führen Sie [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) aus, und geben Sie den Wert **TRUE** für den Parameter **@allow_queued_tran** und den Wert **Pub Wins**, **Sub Reinit** oder **Sub Wins** für **@conflict_policy** an.  
  
4.  Führen Sie auf dem Verleger [sp_addpublication_snapshot (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) aus. Geben Sie den in Schritt 3 für **@publication** verwendeten Veröffentlichungsnamen und die Windows-Anmeldeinformationen, unter denen der Momentaufnahme-Agent ausgeführt wird, für **@snapshot_job_name** und **@password**aktiviert wird. Wenn der Agent zum Herstellen der Verbindung mit dem Verleger die SQL Server-Authentifizierung verwendet, müssen Sie zudem den Wert **0** für **@publisher_security_mode** und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für **@publisher_login** und **@publisher_password**aktiviert wird. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
5.  Fügen Sie der Veröffentlichung Artikel hinzu. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  Erstellen Sie auf dem Abonnenten ein Abonnement mit Update für diese Veröffentlichung.  
  
#### <a name="to-change-the-conflict-policy-for-a-publication-that-allows-queued-updating-subscriptions"></a>So ändern Sie die Konfliktrichtlinie für eine Veröffentlichung, die Abonnements mit verzögertem Update über eine Warteschlange zulässt  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) aus. Geben Sie den Wert **conflict_policy** für **@property** sowie für die gewünschte Konfliktrichtlinie einen der Werte **pub wins**, **sub reinit**oder **sub wins** für **@value**aktiviert wird.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel wird eine Veröffentlichung erstellt, die sowohl sofortige als auch verzögerte Updates von Pullabonnements unterstützt.  
  
 [!code-sql[HowTo#sp_createtranupdatingpub](../../../relational-databases/replication/codesnippet/tsql/enable-updating-subscrip_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen der Konfliktlösungsoptionen für verzögerte Updates über eine Warteschlange &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)   
 [Veröffentlichungstypen der Transaktionsreplikation](../../../relational-databases/replication/transactional/publication-types-for-transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](https://msdn.microsoft.com/library/mt740635.aspx)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Verwenden von „sqlcmd“ mit Skriptvariablen](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
