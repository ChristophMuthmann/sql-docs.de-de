---
title: "Aktualisieren von Replikationsskripts (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Skripts [SQL Server-Replikation], Upgrades ausführen"
  - "Upgrades von SQL Server ausführen, replizierte Datenbanken"
  - "Aktualisieren von Replikationsanwendungen"
  - "Replikation [SQL Server], Skripterstellung"
  - "Replikation [SQL Server], Ausführen von Upgrades"
  - "Aktualisieren von replizierten Datenbanken"
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Aktualisieren von Replikationsskripts (Replikationsprogrammierung mit Transact-SQL)
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skriptdateien kann eine Replikationstopologie programmgesteuert konfiguriert werden. Weitere Informationen finden Sie unter [Replikationskonzepte für gespeicherte Systemprozeduren](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md).  
  
> [!IMPORTANT]  
>  Skripts, die von Mitgliedern der **sysadmin** -Rolle ausgeführt werden, müssen nicht aktualisiert werden. Dennoch empfiehlt es sich, vorhandene Skripts wie in diesem Thema beschrieben zu ändern. Geben Sie ein Konto mit Mindestberechtigungen für jeden Replikations-Agent an, wie im Abschnitt zu den für die Agents erforderlichen Berechtigungen im Thema [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)beschrieben.  
  
 Diese Sicherheitsverbesserungen, die Ihnen mehr Kontrolle über Berechtigungen bieten, indem Sie explizit die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Konten angeben können, unter denen Replikations-Agentaufträge ausgeführt werden, wirken sich auf die folgenden gespeicherten Prozeduren in vorhandenen Skripts aus:  
  
-   **Sp_addpublication_snapshot**:  
  
     Geben Sie nun die Windows-Anmeldeinformationen als **@job_login** und **@job_password** beim Ausführen von [Sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) um den Auftrag erstellen, unter dem der Snapshot-Agent auf dem Verteiler ausgeführt wird.  
  
-   **Sp_addpushsubscription_agent**:  
  
     Sie sollten nun ausführen [Sp_addpushsubscription_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) um explizit einen Auftrag hinzuzufügen und die Windows-Anmeldeinformationen (**@job_login** und **@job_password**) unter dem der Snapshot-Agent-Auftrag auf dem Verteiler ausgeführt wird. In Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]wurde dieser Vorgang automatisch beim Erstellen eines Pushabonnements ausgeführt.  
  
-   **Sp_addmergepushsubscription_agent**:  
  
     Sie sollten nun ausführen [Sp_addmergepushsubscription_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) um explizit einen Auftrag hinzuzufügen und die Windows-Anmeldeinformationen (**@job_login** und **@job_password**) unter dem der Merge-Agent-Auftrag auf dem Verteiler ausgeführt wird. In Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]wurde dieser Vorgang automatisch beim Erstellen eines Pushabonnements ausgeführt.  
  
-   **Sp_addpullsubscription_agent**:  
  
     Geben Sie nun die Windows-Anmeldeinformationen als **@job_login** und **@job_password** beim Ausführen von [Sp_addpullsubscription_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) um den Auftrag erstellen, unter dem der Verteilungsagent auf dem Abonnenten ausgeführt wird.  
  
-   **Sp_addmergepullsubscription_agent**:  
  
     Geben Sie nun die Windows-Anmeldeinformationen als **@job_login** und **@job_password** beim Ausführen von [Sp_addmergepullsubscription_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) um den Auftrag erstellen, unter dem der Merge-Agent auf dem Abonnenten ausgeführt wird.  
  
-   **Sp_addlogreader_agent**:  
  
     Sie sollten nun ausführen [Sp_addlogreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) manuell Auftrag hinzufügen, und geben Sie die Windows-Anmeldeinformationen, unter denen der Protokolllese-Agent auf dem Verteiler ausgeführt wird. In Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]wurde dieser Vorgang automatisch beim Erstellen einer Transaktionsveröffentlichung ausgeführt.  
  
-   **Sp_addqreader_agent**:  
  
     Sie sollten nun ausführen [Sp_addqreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) manuell Auftrag hinzufügen, und geben Sie die Windows-Anmeldeinformationen, unter denen der Warteschlangenlese-Agent auf dem Verteiler ausgeführt wird. In Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]wurde dieser Vorgang automatisch beim Erstellen einer Transaktionsveröffentlichung mit Unterstützung des verzögerten Aktualisierens ausgeführt.  
  
 Im Sicherheitsmodell eingeführten [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], Replikations-Agents stellen Verbindungen mit der lokalen Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mit Windows-Authentifizierung mit den Anmeldeinformationen, die im angegebenen **@job_name** und **@job_password**. Informationen zu den Anforderungen für beim Ausführen von Replikations-Agentaufträgen verwendeten Windows-Konten finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden, müssen Sie sicherstellen, dass die Datei geschützt ist.  
  
### So aktualisieren Sie Skripts, mit denen eine Momentaufnahme- oder eine Transaktionsveröffentlichung konfiguriert werden  
  
1.  Im vorhandenen Skript vor [Sp_addpublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), führen Sie [Sp_addlogreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie die Windows-Anmeldeinformationen, unter dem der Protokolllese-Agent ausgeführt, für wird **@job_name** und **@job_password**. Wenn der Agent [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierung, wenn eine Verbindung mit dem Verleger herstellen, müssen Sie auch den Wert angeben **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Protokolllese-Agents für die Veröffentlichungsdatenbank erstellt.  
  
    > [!NOTE]  
    >  Dieser Schritt muss nur bei Transaktionsveröffentlichungen, nicht bei Momentaufnahmeveröffentlichungen ausgeführt werden.  
  
2.  (Optional) Vor dem [Sp_addpublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), führen Sie [Sp_addqreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) auf dem Verteiler für die Verteilungsdatenbank. Geben Sie die Windows-Anmeldeinformationen, unter dem der Warteschlangenlese-Agent ausgeführt, für wird **@job_name** und **@job_password**. Dadurch wird ein Auftrag des Warteschlangenlese-Agents für den Verteiler erstellt.  
  
    > [!NOTE]  
    >  Dieser Schritt muss nur bei Transaktionsveröffentlichungen ausgeführt werden, die Abonnenten mit verzögertem Update über eine Warteschlange unterstützen.  
  
3.  (Optional) Aktualisieren Sie die Ausführung von [Sp_addpublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) nicht standardmäßige Werte für Parameter fest, die neue Replikationsfunktionen implementieren.  
  
4.  Nach dem [Sp_addpublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), führen Sie [Sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie **@publication** und die Windows-Anmeldeinformationen, unter denen der Snapshot-Agent ausgeführt, für die wird **@job_name** und **@job_password**. Wenn der Agent [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierung, wenn eine Verbindung mit dem Verleger herstellen, müssen Sie auch den Wert angeben **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
5.  (Optional) Aktualisieren Sie die Ausführung von [Sp_addarticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) nicht standardmäßige Werte für Parameter fest, die neue Replikationsfunktionen implementieren.  
  
### So aktualisieren Sie Skripts, mit denen einer Momentaufnahme- oder Transaktionsveröffentlichung Abonnements hinzugefügt werden  
  
1.  Nach dem Ausführen der gespeicherten Prozedur, mit der das Abonnement erstellt wird, müssen Sie die gespeicherte Prozedur ausführen, mit der der Auftrag des Verteilungs-Agents erstellt wird, damit das Abonnement synchronisiert wird. Welche gespeicherte Prozedur Sie verwenden, hängt vom Typ des Abonnements ab.  
  
    -   Aktualisieren Sie bei einem Pullabonnement die Ausführung von [Sp_addpullsubscription_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) die Windows-Anmeldeinformationen angeben, unter dem der Verteilungsagent ausgeführt, auf dem Abonnenten für wird **@job_name** und **@job_password**. Dies erfolgt nach der Ausführung von [Sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Weitere Informationen finden Sie unter [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
    -   Führen Sie ein Pushabonnement [Sp_addpushsubscription_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) auf dem Verleger. Geben Sie **@subscriber**, **@subscriber_db**, **@publication**, unter dem der Verteilungsagent ausgeführt, auf dem Verteiler für die wird, Windows-Anmeldeinformationen **@job_name** und **@job_password**, und einen Zeitplan für diesen Agentauftrag. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md). Dies erfolgt nach der Ausführung von [Sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Weitere Informationen finden Sie unter [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md).  
  
### So aktualisieren Sie Skripts, mit denen eine Mergeveröffentlichung konfiguriert wird  
  
1.  (Optional) Aktualisieren Sie im vorhandenen Skript die Ausführung von [Sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) nicht standardmäßige Werte für Parameter fest, die neue Replikationsfunktionen implementieren.  
  
2.  Nach dem [Sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), führen Sie [Sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie **@publication** und die Windows-Anmeldeinformationen, unter denen der Snapshot-Agent ausgeführt, für die wird **@job_name** und **@job_password**. Wenn der Agent [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierung, wenn eine Verbindung mit dem Verleger herstellen, müssen Sie auch den Wert angeben **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
3.  (Optional) Aktualisieren Sie die Ausführung von [Sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) nicht standardmäßige Werte für Parameter fest, die neue Replikationsfunktionen implementieren.  
  
### So aktualisieren Sie Skripts, mit denen einer Mergeveröffentlichung Abonnements hinzugefügt werden  
  
1.  Nach dem Ausführen der gespeicherten Prozedur, mit der das Abonnement erstellt wird, müssen Sie die gespeicherte Prozedur ausführen, mit der der Auftrag des Merge-Agents erstellt wird, damit das Abonnement synchronisiert wird. Welche gespeicherte Prozedur Sie verwenden, hängt vom Typ des Abonnements ab.  
  
    -   Aktualisieren Sie bei einem Pullabonnement die Ausführung von [Sp_addmergepullsubscription_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) die Windows-Anmeldeinformationen angeben, unter dem der Merge-Agent ausgeführt, auf dem Abonnenten für wird **@job_name** und **@job_password**. Dies erfolgt nach der Ausführung von [Sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Weitere Informationen finden Sie unter [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
    -   Führen Sie ein Pushabonnement [Sp_addmergepushsubscription_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) auf dem Verleger. Geben Sie **@subscriber**, **@subscriber_db**, **@publication**, unter dem der Merge-Agent auf dem Verteiler ausgeführt, für wird, die Windows-Anmeldeinformationen **@job_name** und **@job_password**, und einen Zeitplan für diesen Agentauftrag. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md). Dies erfolgt nach der Ausführung von [Sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Weitere Informationen finden Sie unter [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md).  
  
## Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem eine Transaktionsveröffentlichung für die Product-Tabelle erstellt wird. Diese Veröffentlichung unterstützt sofortige Updates mit Updates über eine Warteschlange als Failover. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_1.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird die Aktualisierung des vorherigen Skripts dargestellt, mit dem eine Transaktionsveröffentlichung erstellt wird, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Diese Veröffentlichung unterstützt sofortige Updates mit Updates über eine Warteschlange als Failover. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen angegeben werden, zur Laufzeit mithilfe **Sqlcmd** Skriptvariablen.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_2.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem eine Mergeveröffentlichung für die Customers-Tabelle erstellt wird. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_3.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird das vorherige Skript dargestellt, mit dem eine Mergeveröffentlichung erstellt wird und das aktualisiert wurde, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen angegeben werden, zur Laufzeit mithilfe **Sqlcmd** Skriptvariablen.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_4.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem ein Pushabonnement für eine Transaktionsveröffentlichung erstellt wird. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_5.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird die Aktualisierung des vorherigen Skripts dargestellt, mit dem ein Pushabonnement für eine Transaktionsveröffentlichung erstellt wird und das aktualisiert wurde, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen angegeben werden, zur Laufzeit mithilfe **Sqlcmd** Skriptvariablen.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_6.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem ein Pushabonnement für eine Mergeveröffentlichung erstellt wird. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird die Aktualisierung des vorherigen Skripts dargestellt, mit dem ein Pushabonnement für eine Mergeveröffentlichung erstellt wird und das aktualisiert wurde, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen angegeben werden, zur Laufzeit mithilfe **Sqlcmd** Skriptvariablen.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_8.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem ein Pullabonnement für eine Transaktionsveröffentlichung erstellt wird. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird die Aktualisierung des vorherigen Skripts dargestellt, mit dem ein Pullabonnement für eine Transaktionsveröffentlichung erstellt wird und das aktualisiert wurde, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen angegeben werden, zur Laufzeit mithilfe **Sqlcmd** Skriptvariablen.  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_9.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird ein [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Skript dargestellt, mit dem ein Pullabonnement für eine Mergeveröffentlichung erstellt wird. Standardparameter wurden zwecks besserer Lesbarkeit entfernt.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_10.sql)]  
  
## Beispiel  
 Im folgenden Beispiel wird die Aktualisierung des vorherigen Skripts dargestellt, mit dem ein Pullabonnement für eine Mergeveröffentlichung erstellt wird und das aktualisiert wurde, damit es unter [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und späteren Versionen erfolgreich ausgeführt werden kann. Standardwerte für neue Parameter wurden explizit deklariert.  
  
> [!NOTE]  
>  Windows-Anmeldeinformationen angegeben werden, zur Laufzeit mithilfe **Sqlcmd** Skriptvariablen.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_11.sql)]  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Erstellen eines Pushabonnements](../../../relational-databases/replication/create-a-push-subscription.md)   
 [Erstellen eines Pullabonnements](../../../relational-databases/replication/create-a-pull-subscription.md)   
 [Anzeigen und Ändern von Replikationssicherheitseinstellungen](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../../../relational-databases/replication/mssql-eng021797.md)   
 [MSSQL_ENG021798](../../../relational-databases/replication/mssql-eng021798.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Aktualisieren von replizierten Datenbanken](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  