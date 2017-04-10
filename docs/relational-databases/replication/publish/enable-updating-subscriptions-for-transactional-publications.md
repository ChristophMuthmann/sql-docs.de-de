---
title: "Aktivieren des Aktualisierens von Abonnements f&#252;r Transaktionsver&#246;ffentlichungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Transaktionsreplikation, aktualisierbare Abonnements"
  - "aktualisierbare Abonnements, aktivieren"
  - "Abonnements [SQL Server-Replikation], aktualisierbar"
ms.assetid: 539d5bb0-b808-4d8c-baf4-cb6d32d2c595
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Aktivieren des Aktualisierens von Abonnements f&#252;r Transaktionsver&#246;ffentlichungen
  In diesem Thema wird beschrieben, wie das Aktualisieren von Abonnements für Transaktionsveröffentlichungen in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]aktiviert wird.  
  
> **HINWEIS!** [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  

##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
 Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Aktivieren Sie aktualisierbare Abonnements für Transaktionsveröffentlichungen auf der Seite **Veröffentlichungstyp** des Assistenten für neue Veröffentlichung.  
  
 Um aktualisierbare Abonnements verwenden zu können, müssen auch im Assistenten für neue Abonnements Optionen konfiguriert werden.  
  
#### So aktivieren Sie aktualisierbare Abonnements  
  
1.  Wählen Sie im Assistenten für neue Veröffentlichung auf der Seite **Veröffentlichungstyp** die Option **Transaktionsveröffentlichung mit aktualisierbaren Abonnements**aus.  
  
2.  Geben Sie auf der Seite **Agentsicherheit** neben den Sicherheitseinstellungen für den Momentaufnahme-Agent und den Protokolllese-Agent auch die Sicherheitseinstellungen für den Warteschlangenlese-Agent an. Weitere Informationen zu den Berechtigungen, die für das Konto erforderlich sind, unter dem der Warteschlangenlese-Agent ausgeführt wird, finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    > **Hinweis:** der Warteschlangenlese-Agent wird konfiguriert, auch wenn Sie nur sofort aktualisierbare Abonnements verwenden.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Wenn Sie mithilfe von gespeicherten Replikationsprozeduren programmgesteuert eine Transaktionsveröffentlichung erstellen, können Sie das sofortige oder das verzögerte Aktualisieren der Abonnements aktivieren.  
  
#### So erstellen Sie eine Veröffentlichung, die Abonnements mit sofortigem Update unterstützt  
  
1.  Erstellen Sie, falls notwendig, einen Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank.  
  
    -   Wenn bereits ein Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank vorhanden ist, fahren Sie mit Schritt 2 fort.  
  
    -   Wenn Sie unsicher sind, ob ein Protokolllese-Agent-Auftrag für eine veröffentlichte Datenbank vorhanden ist, führen Sie [Sp_helplogreader_agent &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Wenn das Resultset leer ist, muss ein Protokolllese-Agentauftrag erstellt werden.  
  
    -   Führen Sie auf dem Verleger [Sp_addlogreader_agent &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Geben Sie die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] unter dem der Agent ausgeführt, für die wird Windows-Anmeldeinformationen **@job_name** und **@password**. Wenn der Agent beim Verbinden mit dem Verleger SQL Server-Authentifizierung verwendet, müssen Sie auch angeben, auf den Wert **0** für **@publisher_security_mode** und [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**.  
  
2.  Führen Sie [Sp_addpublication &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), Angabe des Werts **true** für den Parameter **@allow_sync_tran**.  
  
3.  Führen Sie auf dem Verleger [Sp_addpublication_snapshot &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Geben Sie den in Schritt 2 verwendeten Veröffentlichungsnamen **@publication** und die Windows-Anmeldeinformationen, unter denen der Snapshot-Agent ausgeführt, für die wird **@job_name** und **@password**. Wenn der Agent beim Verbinden mit dem Verleger SQL Server-Authentifizierung verwendet, müssen Sie auch angeben, auf den Wert **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
4.  Fügen Sie der Veröffentlichung Artikel hinzu. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
5.  Erstellen Sie auf dem Abonnenten ein Abonnement mit Update für diese Veröffentlichung.   
  
#### So erstellen Sie eine Veröffentlichung, die Abonnements mit verzögertem Update über eine Warteschlange unterstützt  
  
1.  Erstellen Sie, falls notwendig, einen Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank.  
  
    -   Wenn bereits ein Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank vorhanden ist, fahren Sie mit Schritt 2 fort.  
  
    -   Wenn Sie unsicher sind, ob ein Protokolllese-Agent-Auftrag für eine veröffentlichte Datenbank vorhanden ist, führen Sie [Sp_helplogreader_agent &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Wenn das Resultset leer ist, muss ein Protokolllese-Agentauftrag erstellt werden.  
  
    -   Führen Sie auf dem Verleger [Sp_addlogreader_agent &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Geben Sie die Windows-Anmeldeinformationen, unter dem der Agent ausgeführt, für wird **@job_name** und **@password**. Wenn der Agent beim Verbinden mit dem Verleger SQL Server-Authentifizierung verwendet, müssen Sie auch angeben, auf den Wert **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**.  
  
2.  Erstellen Sie, falls notwendig, einen Warteschlangenlese-Agentauftrag für den Verteiler.  
  
    -   Wenn bereits ein Warteschlangenlese-Agentauftrag für die Verteilungsdatenbank vorhanden ist, fahren Sie mit Schritt 3 fort.  
  
    -   Wenn Sie unsicher sind, ob ein Warteschlangenlese-Agent-Auftrag für die Verteilungsdatenbank vorhanden ist, führen Sie [Sp_helpqreader_agent &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md) auf dem Verteiler für die Verteilungsdatenbank. Wenn das Resultset leer ist, muss ein Warteschlangenlese-Agentauftrag erstellt werden.  
  
    -   Führen Sie auf dem Verteiler [Sp_addqreader_agent &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md). Geben Sie die Windows-Anmeldeinformationen, unter dem der Agent ausgeführt, für wird **@job_name** und **@password**. Diese Anmeldeinformationen werden verwendet, wenn der Warteschlangenlese-Agent eine Verbindung mit dem Verleger und dem Abonnenten herstellt. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
3.  Führen Sie [Sp_addpublication &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), Angabe des Werts **true** für den Parameter **@allow_queued_tran** und einem Wert von **Pub Wins**, **sub Reinit**, oder **sub Wins** für **@conflict_policy**.  
  
4.  Führen Sie auf dem Verleger [Sp_addpublication_snapshot (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Geben Sie den Namen der Veröffentlichung verwendet, die in Schritt 3 für **@publication** und die Windows-Anmeldeinformationen, unter denen der Snapshot-Agent ausgeführt, für die wird **@snapshot_job_name** und **@password**. Wenn der Agent beim Verbinden mit dem Verleger SQL Server-Authentifizierung verwendet, müssen Sie auch angeben, auf den Wert **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
5.  Fügen Sie der Veröffentlichung Artikel hinzu. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  Erstellen Sie auf dem Abonnenten ein Abonnement mit Update für diese Veröffentlichung.  
  
#### So ändern Sie die Konfliktrichtlinie für eine Veröffentlichung, die Abonnements mit verzögertem Update über eine Warteschlange zulässt  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changepublication &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Geben Sie den Wert **Conflict_policy** für **@property** und die gewünschte konfliktrichtlinie **Pub Wins**, **sub Reinit**, oder **sub Wins** für **@value**.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel wird eine Veröffentlichung erstellt, die sowohl sofortige als auch verzögerte Updates von Pullabonnements unterstützt.  
  
 [!code-sql[HowTo#sp_createtranupdatingpub](../../../relational-databases/replication/codesnippet/tsql/enable-updating-subscrip_1.sql)]  
  
## Siehe auch  
 [Legen Sie in der Warteschlange aktualisieren Konfliktlösungsoptionen &#40; SQL Server Management Studio &#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)   
 [Veröffentlichungstypen der Transaktionsreplikation](../../../relational-databases/replication/transactional/publication-types-for-transactional-replication.md)   
 [Aktualisierbare Abonnements für die Transaktionsreplikation](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Erstellen von aktualisierbaren Abonnements für eine Transaktionsveröffentlichung](https://msdn.microsoft.com/library/mt740635.aspx)   
 [Aktualisierbare Abonnements für die Transaktionsreplikation](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Verwenden von sqlcmd mit Skriptvariablen](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)  
  
  