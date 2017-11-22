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
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: updateable transactional subscriptions, T-SQL
ms.assetid: a6e80857-0a69-4867-b6b7-f3629d00c312
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 53bef20bb061a75fca42b122278d2c583b65b904
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-updatable-subscription-to-transactional-publication"></a>Erstellen von aktualisierbaren Abonnements für eine Transaktionsveröffentlichung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
> [!NOTE]  
>  Dieses Feature wird in den Versionen von [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] von 2012 bis 2016 weiterhin unterstützt.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
Bei einer Transaktionsreplikation können am Abonnenten vorgenommene Änderungen mithilfe sofort aktualisierbarer Abonnements oder Abonnements mit verzögerter Aktualisierung über eine Warteschlange an den Verleger zurückgegeben werden. Aktualisierbare Abonnements können mithilfe von gespeicherten Replikationsprozeduren programmgesteuert erstellt werden. (Weitere Informationen finden Sie auch unter [Erstellen eines aktualisierbaren Abonnements für eine Transaktionsveröffentlichung (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md).) 

## <a name="to-create-an-immediate-updating-pull-subscription"></a>So erstellen Sie ein sofort aktualisierbares Pullabonnement ##

1. Überprüfen Sie auf dem Verleger, ob die Veröffentlichung Abonnements mit sofortigem Update unterstützt, indem Sie [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)ausführen. 

    * Wenn `allow_sync_tran` im Resultset den Wert `1`hat, unterstützt die Veröffentlichung Abonnements mit sofortigem Update.

    * Wenn `allow_sync_tran` im Resultset den Wert `0`hat, muss die Veröffentlichung erneut erstellt und die Unterstützung von Abonnements mit sofortigem Update aktiviert werden.

2. Überprüfen Sie auf dem Verleger, ob die Veröffentlichung Pullabonnements unterstützt, indem Sie [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)ausführen. 

    * Wenn `allow_pull` im Resultset den Wert `1`hat, unterstützt die Veröffentlichung Pullabonnements.

    * Wenn `allow_pull` den Wert `0`hat, führen Sie [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)aus, wobei Sie `allow_pull` für `@property` und `true` für `@value`angeben. 

3. Führen Sie auf dem Abonnenten [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)aus. Geben Sie `@publisher` und `@publication`und einen der folgenden Werte für `@update_mode`fest:

    * `sync tran` – Ermöglicht sofortige Updates des Abonnements.

    * `failover` – Ermöglicht das sofortige Aktualisieren für das Abonnement, wobei als Failoveroption das verzögerte Aktualisieren über eine Warteschlange verwendet wird.

    > [!NOTE]  
>  `failover` erfordert, dass die Veröffentlichung auch Abonnements mit verzögertem Aktualisieren über eine Warteschlange zulässt. 
 
4. Führen Sie auf dem Abonnenten [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)aus. Geben Sie Folgendes an:

    * Die Parameter `@publisher`, `@publisher_db`und `@publication` . 

    * Die Microsoft Windows-Anmeldeinformationen, unter denen der Verteilungs-Agent auf dem Abonnenten für `@job_login` und `@job_password`ausgeführt wird. 

    > [!NOTE]  
>  Für Verbindungen, die mit der integrierten Windows-Authentifizierung hergestellt werden, werden immer die mit `@job_login` und `@job_password`angegebenen Windows-Anmeldeinformationen verwendet. Der Verteilungs-Agent stellt die lokale Verbindung mit dem Abonnenten immer mithilfe der integrierten Windows-Authentifizierung her. Standardmäßig stellt der Agent mithilfe der integrierten Windows-Authentifizierung eine Verbindung mit dem Verteiler her. 
 
    * (Optional) Ein Wert von `0` für `@distributor_security_mode` und die Microsoft SQL Server-Anmeldeinformationen für `@distributor_login` und `@distributor_password`, wenn Sie beim Herstellen einer Verbindung zum Verteiler die SQL Server-Authentifizierung verwenden müssen. 

    * Einen Zeitplan für den Verteilungs-Agentauftrag für dieses Abonnement. 

5. Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)aus. Geben Sie `@publisher`, `@publication`, den Namen der Veröffentlichungsdatenbank für `@publisher_db`und einen der folgenden Werte für `@security_mode`an: 

    * `0` – Verwenden Sie die SQL Server-Authentifizierung, wenn Updates beim Verleger vorgenommen werden. Diese Option erfordert auf dem Verleger die Angabe gültiger Anmeldeinformationen für `@login` und `@password`.

    * `1` – Verwenden Sie zum Verbindungsaufbau mit dem Verleger den Sicherheitskontext des Benutzers, der Änderungen am Abonnenten vornimmt. Weitere Informationen zu den in Verbindung mit diesem Sicherheitsmodus geltenden Beschränkungen finden Sie unter [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) .

    * `2` – Verwenden Sie einen vorhandenen benutzerdefinierten Anmeldenamen für den Verbindungsserver, der mit [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)erstellt wurde.

6. Führen Sie auf dem Verleger [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) aus, wobei Sie `@publication`, `@subscriber`, `@destination_db`, den Wert „Pull“ für `@subscription_type`und denselben Wert angeben, den Sie in Schritt 3 für `@update_mode`angegeben haben.

Damit wird das Pullabonnement beim Verleger registriert. 


## <a name="to-create-an-immediate-updating-push-subscription"></a>So erstellen Sie ein sofort aktualisierbares Pushabonnement ##

1. Überprüfen Sie auf dem Verleger, ob die Veröffentlichung Abonnements mit sofortigem Update unterstützt, indem Sie [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)ausführen. 

    * Wenn `allow_sync_tran` im Resultset den Wert `1`hat, unterstützt die Veröffentlichung Abonnements mit sofortigem Update.

    * Wenn `allow_sync_tran` im Resultset den Wert `0`hat, muss die Veröffentlichung erneut erstellt und die Unterstützung von Abonnements mit sofortigem Update aktiviert werden.

2. Überprüfen Sie auf dem Verleger, ob die Veröffentlichung Pushabonnements unterstützt, indem Sie [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)ausführen. 

    * Wenn `allow_push` im Resultset den Wert `1`hat, unterstützt die Veröffentlichung Pushabonnements.

    * Wenn `allow_push` den Wert `0`hat, führen Sie [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)aus, wobei Sie `allow_push` für `@property` und `true` für `@value`angeben. 

3. Führen Sie auf dem Verleger [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)aus. Geben Sie `@publication`, `@subscriber`, `@destination_db`und einen der folgenden Werte für `@update_mode`fest:

    * `sync tran` – Aktiviert die Unterstützung für sofortige Updates.

    * `failover` – Aktiviert die Unterstützung für sofortige Updates, wobei verzögerte Updates über eine Warteschlange als Failoveroption verwendet werden.

    > [!NOTE]  
>  `failover` erfordert, dass die Veröffentlichung auch Abonnements mit verzögertem Aktualisieren über eine Warteschlange zulässt. 
 
4. Führen Sie auf dem Verleger [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)aus. Geben Sie die folgenden Parameter an:

    * `@subscriber`, `@subscriber_db`und `@publication`. 

    * Die Windows-Anmeldeinformationen, unter denen der Verteilungs-Agent beim Verteiler für `@job_login` und `@job_password`ausgeführt wird. 

    > [!NOTE]  
>  Für Verbindungen, die mit der integrierten Windows-Authentifizierung hergestellt werden, werden immer die mit `@job_login` und `@job_password`angegebenen Windows-Anmeldeinformationen verwendet. Der Verteilungs-Agent stellt die lokale Verbindung mit dem Verteiler immer mithilfe der Windows-Authentifizierung her. Standardmäßig stellt der Agent mithilfe der integrierten Windows-Authentifizierung eine Verbindung mit dem Abonnenten her. 

    * (Optional) Ein Wert von `0` für `@subscriber_security_mode` und die SQL Server-Anmeldeinformationen für `@subscriber_login` und `@subscriber_password`, wenn Sie beim Herstellen einer Verbindung zum Abonnenten die SQL Server-Authentifizierung verwenden müssen. 

    * Einen Zeitplan für den Verteilungs-Agentauftrag für dieses Abonnement.

5. Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)aus. Geben Sie `@publisher`, `@publication`, den Namen der Veröffentlichungsdatenbank für `@publisher_db`und einen der folgenden Werte für `@security_mode`an: 

     * `0` – Verwenden Sie die SQL Server-Authentifizierung, wenn Updates beim Verleger vorgenommen werden. Diese Option erfordert auf dem Verleger die Angabe gültiger Anmeldeinformationen für `@login` und `@password`.

     * `1` – Verwenden Sie zum Verbindungsaufbau mit dem Verleger den Sicherheitskontext des Benutzers, der Änderungen am Abonnenten vornimmt. Weitere Informationen zu den in Verbindung mit diesem Sicherheitsmodus geltenden Beschränkungen finden Sie unter [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) .

     * `2` – Verwenden Sie einen vorhandenen benutzerdefinierten Anmeldenamen für den Verbindungsserver, der mit [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)erstellt wurde.


## <a name="to-create-a-queued-updating-pull-subscription"></a>So erstellen Sie ein Pullabonnement mit verzögertem Update über eine Warteschlange ##

1. Überprüfen Sie auf dem Verleger, ob die Veröffentlichung Abonnements mit verzögertem Update über eine Warteschlange unterstützt, indem Sie [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)ausführen. 

    * Wenn `allow_queued_tran` im Resultset den Wert `1`hat, unterstützt die Veröffentlichung Abonnements mit sofortigem Update.

    * Wenn `allow_queued_tran` im Resultset den Wert `0`hat, muss die Veröffentlichung erneut erstellt und die Unterstützung von Abonnements mit verzögertem Update über eine Warteschlange aktiviert werden.

2. Überprüfen Sie auf dem Verleger, ob die Veröffentlichung Pullabonnements unterstützt, indem Sie [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)ausführen. 

    * Wenn `allow_pull` im Resultset den Wert `1`hat, unterstützt die Veröffentlichung Pullabonnements.

    * Wenn `allow_pull` den Wert `0`hat, führen Sie [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)aus, wobei Sie `allow_pull` für `@property` und `true` für `@value`angeben. 

3. Führen Sie auf dem Abonnenten [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)aus. Geben Sie `@publisher` und `@publication`und einen der folgenden Werte für `@update_mode`fest:

    * `queued tran` – Aktiviert das verzögerte Update über eine Warteschlange für das Abonnement.

    * `queued failover` – Aktiviert die Unterstützung für verzögerte Updates über eine Warteschlange, wobei sofortige Updates als Failoveroption verwendet werden.

    > [!NOTE]  
>  `queued failover` erfordert, dass die Veröffentlichung auch Abonnements mit sofortigem Update zulässt. Damit im Fehlerfall sofortige Updates durchgeführt werden können, müssen Sie unter Verwendung von [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) die Anmeldeinformationen definieren, unter denen Änderungen am Abonnenten auf dem Verleger repliziert werden sollen.
 
4. Führen Sie auf dem Abonnenten [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)aus. Geben Sie die folgenden Parameter an:

    * @publisher, `@publisher_db`und `@publication`. 

    * Die Windows-Anmeldeinformationen, unter denen der Verteilungs-Agent auf dem Abonnenten für `@job_login` und `@job_password`ausgeführt wird. 

    > [!NOTE]  
>  Für Verbindungen, die mit der integrierten Windows-Authentifizierung hergestellt werden, werden immer die mit `@job_login` und `@job_password`angegebenen Windows-Anmeldeinformationen verwendet. Der Verteilungs-Agent stellt die lokale Verbindung mit dem Abonnenten immer mithilfe der integrierten Windows-Authentifizierung her. Standardmäßig stellt der Agent mithilfe der integrierten Windows-Authentifizierung eine Verbindung mit dem Verteiler her. 
 
    * (Optional) Ein Wert von `0` für `@distributor_security_mode` und die SQL Server-Anmeldeinformationen für `@distributor_login` und `@distributor_password`, wenn Sie beim Herstellen einer Verbindung zum Verteiler die SQL Server-Authentifizierung verwenden müssen. 

    * Einen Zeitplan für den Verteilungs-Agentauftrag für dieses Abonnement.

5. Führen Sie auf dem Verleger [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md) aus, umd den Abonnenten auf dem Verleger zu registrieren, wobei Sie `@publication`, `@subscriber`, `@destination_db`, den Wert „Pull“ für `@subscription_type`und denselben Wert angeben, den Sie in Schritt 3 für `@update_mode`angegeben haben.

Damit wird das Pullabonnement beim Verleger registriert. 


## <a name="to-create-a-queued-updating-push-subscription"></a>So erstellen Sie ein Pushabonnement mit verzögertem Update über eine Warteschlange ##

1. Überprüfen Sie auf dem Verleger, ob die Veröffentlichung Abonnements mit verzögertem Update über eine Warteschlange unterstützt, indem Sie [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)ausführen. 

    * Wenn „allow_queued_tran“ im Resultset den Wert 1 hat, unterstützt die Veröffentlichung Abonnements mit sofortigem Update.

    * Wenn „allow_queued_tran“ im Resultset den Wert 0 hat, muss die Veröffentlichung erneut erstellt und die Unterstützung von Abonnements mit verzögertem Update über eine Warteschlange aktiviert werden. Weitere Informationen finden Sie unter „Gewusst wie: Aktivieren von aktualisierbaren Abonnements für Transaktionsveröffentlichungen (Replikationsprogrammierung mit Transact-SQL)“.

2. Überprüfen Sie auf dem Verleger, ob die Veröffentlichung Pushabonnements unterstützt, indem Sie [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)ausführen. 

    * Wenn `allow_push` im Resultset den Wert `1`hat, unterstützt die Veröffentlichung Pushabonnements.

    * Wenn `allow_push` den Wert `0`hat, führen Sie [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)aus, wobei Sie „allow_push“ für `@property` und `true` für `@value`angeben. 

3. Führen Sie auf dem Verleger [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)aus. Geben Sie `@publication`, `@subscriber`, `@destination_db`und einen der folgenden Werte für `@update_mode`fest:

    * `queued tran` – Aktiviert das verzögerte Update über eine Warteschlange für das Abonnement.

    * `queued failover` – Aktiviert die Unterstützung für verzögerte Updates über eine Warteschlange, wobei sofortige Updates als Failoveroption verwendet werden.

    > [!NOTE]  
>  Die Option „queued failover“ erfordert, dass die Veröffentlichung auch Abonnements mit sofortigem Update zulässt. Damit im Fehlerfall sofortige Updates durchgeführt werden können, müssen Sie unter Verwendung von [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) die Anmeldeinformationen definieren, unter denen Änderungen am Abonnenten auf dem Verleger repliziert werden sollen.

4. Führen Sie auf dem Verleger [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)aus. Geben Sie die folgenden Parameter an:

    * `@subscriber`, `@subscriber_db`und `@publication`. 

    * Die Windows-Anmeldeinformationen, unter denen der Verteilungs-Agent beim Verteiler für `@job_login` und `@job_password`ausgeführt wird. 

    > [!NOTE]  
>  Für Verbindungen, die mit der integrierten Windows-Authentifizierung hergestellt werden, werden immer die mit `@job_login` und `@job_password`angegebenen Windows-Anmeldeinformationen verwendet. Der Verteilungs-Agent stellt die lokale Verbindung mit dem Verteiler immer mithilfe der Windows-Authentifizierung her. Standardmäßig stellt der Agent mithilfe der integrierten Windows-Authentifizierung eine Verbindung mit dem Abonnenten her. 
 
    * (Optional) Ein Wert von `0` für `@subscriber_security_mode` und die SQL Server-Anmeldeinformationen für `@subscriber_login` und `@subscriber_password`, wenn Sie beim Herstellen einer Verbindung zum Abonnenten die SQL Server-Authentifizierung verwenden müssen. 

    * Einen Zeitplan für den Verteilungs-Agentauftrag für dieses Abonnement.


## <a name="example"></a>Beispiel ##

In diesem Beispiel wird ein sofort aktualisierbares Abonnement für eine Veröffentlichung erstellt, die Abonnements mit sofortigem Update unterstützt. Die Werte für den Anmeldenamen und das Kennwort werden zur Laufzeit mithilfe von sqlcmd-Skriptvariablen bereitgestellt.

> [!NOTE]  
>  Dieses Skript verwendet „sqlcmd“-Skriptvariablen. Sie weisen das Format `$(MyVariable)`auf. Informationen zur Verwendung von Skriptvariablen in der Befehlszeile und in SQL Server Management Studio finden Sie im Abschnitt **Ausführen von Replikationsskripts** im Thema [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md).

```
-- Execute this batch at the Subscriber.
DECLARE @publication AS sysname;
DECLARE @publicationDB AS sysname;
DECLARE @publisher AS sysname;
DECLARE @login AS sysname;
DECLARE @password AS nvarchar(512);
SET @publication = N'AdvWorksProductTran';
SET @publicationDB = N'AdventureWorks2008R2';
SET @publisher = $(PubServer);
SET @login = $(Login);
SET @password = $(Password);

-- At the subscription database, create a pull subscription to a transactional 
-- publication using immediate updating with queued updating as a failover.
EXEC sp_addpullsubscription 
    @publisher = @publisher, 
    @publication = @publication, 
    @publisher_db = @publicationDB, 
    @update_mode = N'failover', 
    @subscription_type = N'pull';

-- Add an agent job to synchronize the pull subscription, 
-- which uses Windows Authentication when connecting to the Distributor.
EXEC sp_addpullsubscription_agent 
    @publisher = @publisher, 
    @publisher_db = @publicationDB, 
    @publication = @publication,
    @job_login = @login,
    @job_password = @password; 

-- Add a Windows Authentication-based linked server that enables the 
-- Subscriber-side triggers to make updates at the Publisher. 
EXEC sp_link_publication 
    @publisher = @publisher, 
    @publication = @publication,
    @publisher_db = @publicationDB, 
    @security_mode = 0,
    @login = @login,
    @password = @password;
GO

USE AdventureWorks2008R2;
GO

-- Execute this batch at the Publisher.
DECLARE @publication AS sysname;
DECLARE @subscriptionDB AS sysname;
DECLARE @subscriber AS sysname;
SET @publication = N'AdvWorksProductTran'; 
SET @subscriptionDB = N'AdventureWorks2008R2Replica'; 
SET @subscriber = $(SubServer);

-- At the Publisher, register the subscription, using the defaults.
USE [AdventureWorks2008R2]
EXEC sp_addsubscription 
    @publication = @publication, 
    @subscriber = @subscriber, 
    @destination_db = @subscriptionDB, 
    @subscription_type = N'pull', 
    @update_mode = N'failover';
GO
```

## <a name="see-also"></a>Siehe auch ##

[Aktualisierbare Abonnements für die Transaktionsreplikation](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Verwenden von sqlcmd mit Skriptvariablen](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)

[Erstellen eines aktualisierbaren Abonnements für eine Transaktionsveröffentlichung (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)

