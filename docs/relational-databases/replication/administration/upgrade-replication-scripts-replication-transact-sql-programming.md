---
title: Aktualisieren von Replikationsskripts (Replikationsprogrammierung mit Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- scripts [SQL Server replication], upgrading
- upgrading SQL Server, replicated databases
- upgrading replication applications
- replication [SQL Server], scripting
- replication [SQL Server], upgrading
- upgrading replicated databases
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
caps.latest.revision: "41"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09f8ed7bf8cbd407a8bd9dc706d5e9aadf34ce65
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>Aktualisieren von Replikationsskripts (Replikationsprogrammierung mit Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe von [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Skriptdateien kann eine Replikationstopologie programmgesteuert konfiguriert werden. Weitere Informationen finden Sie unter [Replikationskonzepte für gespeicherte Systemprozeduren](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md).  
  
> [!IMPORTANT]  
>  Skripts, die von Mitgliedern der **sysadmin** -Rolle ausgeführt werden, müssen nicht aktualisiert werden. Dennoch empfiehlt es sich, vorhandene Skripts wie in diesem Thema beschrieben zu ändern. Geben Sie ein Konto mit Mindestberechtigungen für jeden Replikations-Agent an, wie im Abschnitt zu den für die Agents erforderlichen Berechtigungen im Thema [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)beschrieben.  
  
 Diese Sicherheitsverbesserungen, die Ihnen mehr Kontrolle über Berechtigungen bieten, indem Sie explizit die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Konten angeben können, unter denen Replikations-Agentaufträge ausgeführt werden, wirken sich auf die folgenden gespeicherten Prozeduren in vorhandenen Skripts aus:  
  
-   **sp_addpublication_snapshot**:  
  
     Sie sollten nun die Windows-Anmeldeinformationen in Form von **@job_login** und **@job_password** angeben, wenn Sie [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) ausführen, um den Auftrag zu erstellen, unter dem der Momentaufnahme-Agent auf dem Verteiler ausgeführt wird.  
  
-   **sp_addpushsubscription_agent**:  
  
     Sie sollten nun [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) ausführen, um explizit einen Auftrag hinzuzufügen, und die Windows-Anmeldeinformationen (**@job_login** und **@job_password**) anzugeben, unter denen der Auftrag des Verteilungs-Agents auf dem Verteiler ausgeführt wird. In Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]wurde dieser Vorgang automatisch beim Erstellen eines Pushabonnements ausgeführt.  
  
-   **sp_addmergepushsubscription_agent**:  
  
     Sie sollten nun [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) ausführen, um explizit einen Auftrag hinzuzufügen, und die Windows-Anmeldeinformationen (**@job_login** und **@job_password**) angeben, unter denen der Auftrag des Merge-Agents auf dem Verteiler ausgeführt wird. In Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]wurde dieser Vorgang automatisch beim Erstellen eines Pushabonnements ausgeführt.  
  
-   **sp_addpullsubscription_agent**:  
  
     Sie sollten nun die Windows-Anmeldeinformationen in Form von **@job_login** und **@job_password** angeben, wenn Sie [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) ausführen, um den Auftrag zu erstellen, unter dem der Verteilungs-Agent auf dem Abonnenten ausgeführt wird.  
  
-   **sp_addmergepullsubscription_agent**:  
  
     Geben Sie nun die Windows-Anmeldeinformationen als **@job_login** und **@job_password** beim Ausführen von [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) an, um den Auftrag zu erstellen, unter dem der Merge-Agent auf dem Abonnenten ausgeführt wird.  
  
-   **sp_addlogreader_agent**:  
  
     Sie sollten nun [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) ausführen, um den Auftrag manuell hinzuzufügen, und die Windows-Anmeldeinformationen anzugeben, unter denen der Protokolllese-Agent auf dem Verteiler ausgeführt wird. In Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]wurde dieser Vorgang automatisch beim Erstellen einer Transaktionsveröffentlichung ausgeführt.  
  
-   **sp_addqreader_agent**:  
  
     Sie sollten nun [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) ausführen, um den Auftrag manuell hinzuzufügen, und die Windows-Anmeldeinformationen anzugeben, unter denen der Warteschlangenlese-Agent auf dem Verteiler ausgeführt wird. In Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]wurde dieser Vorgang automatisch beim Erstellen einer Transaktionsveröffentlichung mit Unterstützung des verzögerten Aktualisierens ausgeführt.  
  
 In dem in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]eingeführten Sicherheitsmodell stellen Replikations-Agents Verbindungen mit der lokalen Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mit Windows-Authentifizierung immer mithilfe der in **@job_name** und **@job_password**. Informationen zu den Anforderungen für beim Ausführen von Replikations-Agentaufträgen verwendeten Windows-Konten finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden, müssen Sie sicherstellen, dass die Datei geschützt ist.  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>So aktualisieren Sie Skripts, mit denen eine Momentaufnahme- oder eine Transaktionsveröffentlichung konfiguriert werden  
  
1.  Führen Sie im vorhandenen Skript [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) vor [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie die Windows-Anmeldeinformationen, unter denen der Protokolllese-Agent ausgeführt wird, für **@job_name** und **@job_password**. Wenn der Agent zum Herstellen der Verbindung mit dem Verleger die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung verwendet, müssen Sie zudem den Wert **0** für **@publisher_security_mode** und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Protokolllese-Agents für die Veröffentlichungsdatenbank erstellt.  
  
    > [!NOTE]  
    >  Dieser Schritt muss nur bei Transaktionsveröffentlichungen, nicht bei Momentaufnahmeveröffentlichungen ausgeführt werden.  
  
2.  (Optional) Führen Sie [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) vor [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) auf dem Verteiler für die Verteilungsdatenbank aus. Geben Sie die Windows-Anmeldeinformationen, unter denen der Warteschlangenlese-Agent ausgeführt wird, für **@job_name** und **@job_password**. Dadurch wird ein Auftrag des Warteschlangenlese-Agents für den Verteiler erstellt.  
  
    > [!NOTE]  
    >  Dieser Schritt muss nur bei Transaktionsveröffentlichungen ausgeführt werden, die Abonnenten mit verzögertem Update über eine Warteschlange unterstützen.  
  
3.  (Optional) Aktualisieren Sie die Ausführung von [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), um alle Nichtstandardwerte für Parameter festzulegen, die neue Replikationsfunktionen implementieren.  
  
4.  Führen Sie nach [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie **@publication** und die Windows-Anmeldeinformationen, unter denen der Momentaufnahme-Agent ausgeführt wird, für **@job_name** und **@job_password**. Wenn der Agent zum Herstellen der Verbindung mit dem Verleger die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung verwendet, müssen Sie zudem den Wert **0** für **@publisher_security_mode** und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
5.  (Optional) Aktualisieren Sie die Ausführung von [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), um alle Nichtstandardwerte für Parameter festzulegen, die neue Replikationsfunktionen implementieren.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>So aktualisieren Sie Skripts, mit denen einer Momentaufnahme- oder Transaktionsveröffentlichung Abonnements hinzugefügt werden  
  
1.  Nach dem Ausführen der gespeicherten Prozedur, mit der das Abonnement erstellt wird, müssen Sie die gespeicherte Prozedur ausführen, mit der der Auftrag des Verteilungs-Agents erstellt wird, damit das Abonnement synchronisiert wird. Welche gespeicherte Prozedur Sie verwenden, hängt vom Typ des Abonnements ab.  
  
    -   Aktualisieren Sie bei einem Pullabonnement die Ausführung von [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md), um die Windows-Anmeldeinformationen bereitzustellen, unter denen der Verteilungs-Agent auf dem Abonnenten für **@job_name** und **@job_password** ausgeführt wird. Dies geschieht nach der Ausführung von [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Weitere Informationen finden Sie unter [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
    -   Führen Sie [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) für ein Pushabonnement auf dem Verleger aus. Geben Sie **@subscriber**, **@subscriber_db**, **@publication**, und die Windows-Anmeldeinformationen, unter denen der Verteilungs-Agent auf dem Verteiler ausgeführt wird, für **@job_name** und **@job_password**und einen Zeitplan für diesen Agentauftrag an. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md). Dies geschieht nach der Ausführung von [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Weitere Informationen finden Sie unter [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md).  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>So aktualisieren Sie Skripts, mit denen eine Mergeveröffentlichung konfiguriert wird  
  
1.  (Optional) Aktualisieren Sie im vorhandenen Skript die Ausführung von [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), um alle Nichtstandardwerte für Parameter festzulegen, die neue Replikationsfunktionen implementieren.  
  
2.  Führen Sie nach [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie **@publication** und die Windows-Anmeldeinformationen, unter denen der Momentaufnahme-Agent ausgeführt wird, für **@job_name** und **@job_password**. Wenn der Agent zum Herstellen der Verbindung mit dem Verleger die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung verwendet, müssen Sie zudem den Wert **0** für **@publisher_security_mode** und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
3.  (Optional) Aktualisieren Sie die Ausführung von [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), um alle Nichtstandardwerte für Parameter festzulegen, die neue Replikationsfunktionen implementieren.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>So aktualisieren Sie Skripts, mit denen einer Mergeveröffentlichung Abonnements hinzugefügt werden  
  
1.  Nach dem Ausführen der gespeicherten Prozedur, mit der das Abonnement erstellt wird, müssen Sie die gespeicherte Prozedur ausführen, mit der der Auftrag des Merge-Agents erstellt wird, damit das Abonnement synchronisiert wird. Welche gespeicherte Prozedur Sie verwenden, hängt vom Typ des Abonnements ab.  
  
    -   Aktualisieren Sie bei einem Pullabonnement die Ausführung von [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md), um die Windows-Anmeldeinformationen anzugeben, unter denen der Merge-Agent auf dem Abonnenten für **@job_name** und **@job_password** ausgeführt wird. Dies geschieht nach der Ausführung von [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Weitere Informationen finden Sie unter [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
    -   Führen Sie für ein Pushabonnement [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) auf dem Verleger aus. Geben Sie **@subscriber**, **@subscriber_db**, **@publication**, und die Windows-Anmeldeinformationen, unter denen der Merge-Agent auf dem Verteiler ausgeführt wird, für **@job_name** und **@job_password**und einen Zeitplan für diesen Agentauftrag an. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md). Dies geschieht nach der Ausführung von [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Weitere Informationen finden Sie unter [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem eine Transaktionsveröffentlichung für die Product-Tabelle erstellt wird. Diese Veröffentlichung unterstützt sofortige Updates mit Updates über eine Warteschlange als Failover. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_1.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Aktualisierung des vorherigen Skripts dargestellt, mit dem eine Transaktionsveröffentlichung erstellt wird, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Diese Veröffentlichung unterstützt sofortige Updates mit Updates über eine Warteschlange als Failover. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen werden zur Laufzeit mithilfe von **sqlcmd** -Skriptvariablen angegeben.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_2.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem eine Mergeveröffentlichung für die Customers-Tabelle erstellt wird. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_3.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das vorherige Skript dargestellt, mit dem eine Mergeveröffentlichung erstellt wird und das aktualisiert wurde, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen werden zur Laufzeit mithilfe von **sqlcmd** -Skriptvariablen angegeben.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_4.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem ein Pushabonnement für eine Transaktionsveröffentlichung erstellt wird. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_5.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Aktualisierung des vorherigen Skripts dargestellt, mit dem ein Pushabonnement für eine Transaktionsveröffentlichung erstellt wird und das aktualisiert wurde, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen werden zur Laufzeit mithilfe von **sqlcmd** -Skriptvariablen angegeben.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_6.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem ein Pushabonnement für eine Mergeveröffentlichung erstellt wird. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Aktualisierung des vorherigen Skripts dargestellt, mit dem ein Pushabonnement für eine Mergeveröffentlichung erstellt wird und das aktualisiert wurde, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen werden zur Laufzeit mithilfe von **sqlcmd** -Skriptvariablen angegeben.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_8.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem ein Pullabonnement für eine Transaktionsveröffentlichung erstellt wird. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Aktualisierung des vorherigen Skripts dargestellt, mit dem ein Pullabonnement für eine Transaktionsveröffentlichung erstellt wird und das aktualisiert wurde, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen werden zur Laufzeit mithilfe von **sqlcmd** -Skriptvariablen angegeben.  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_9.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem ein Pullabonnement für eine Mergeveröffentlichung erstellt wird. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_10.sql)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Aktualisierung des vorherigen Skripts dargestellt, mit dem ein Pullabonnement für eine Mergeveröffentlichung erstellt wird und das aktualisiert wurde, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen werden zur Laufzeit mithilfe von **sqlcmd** -Skriptvariablen angegeben.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_11.sql)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)   
 [Anzeigen und Ändern von Replikationssicherheitseinstellungen](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../../../relational-databases/replication/mssql-eng021797.md)   
 [MSSQL_ENG021798](../../../relational-databases/replication/mssql-eng021798.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Aktualisieren von replizierten Datenbanken](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
