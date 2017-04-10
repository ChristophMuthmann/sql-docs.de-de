---
title: "Angeben von Synchronisierungszeitpl&#228;nen | Microsoft Docs"
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
  - "Abonnements [SQL Server-Replikation], synchronisieren"
  - "Planen der Synchronisierung [SQL Server-Replikation]"
  - "Synchronisierung [SQL Server-Replikation], Zeitpläne"
  - "Replikation [SQL Server-Replikation], Synchronisierung"
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Angeben von Synchronisierungszeitpl&#228;nen
  In diesem Thema wird beschrieben, wie Synchronisierungszeitpläne in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) angegeben werden. Während der Erstellung eines Abonnements kann ein Synchronisierungszeitplan definiert werden, der steuert, wann der Replikations-Agent für das Abonnement ausgeführt wird. Wenn Sie keine Zeitplanungsparameter angeben, wird der Standardzeitplan für das Abonnement verwendet.  
  
 Abonnements werden durch den Verteilungs-Agent (für Momentaufnahme- und Transaktionsveröffentlichungen) oder durch den Merge-Agent (für Mergeveröffentlichungen) synchronisiert. Agents können kontinuierlich, bei Bedarf oder nach einem Zeitplan ausgeführt werden.  
  
 **In diesem Thema**  
  
-   **So geben Sie Synchronisierungszeitpläne an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Geben Sie Synchronisierungszeitpläne im Assistenten für neue Abonnements auf der Seite **Synchronisierungszeitplan** an. Weitere Informationen zum Zugreifen auf diesen Assistenten finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md) und [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
 Ändern Sie die Synchronisierungszeitpläne im Dialogfeld **Eigenschaften des Auftragszeitplans** . Dieses Dialogfeld ist in **über den Ordner** Aufträge [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und im Detailfenster des Agents im Replikationsmonitor verfügbar. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
 Wenn Sie die Zeitpläne über den Ordner **Aufträge** angeben, verwenden Sie die folgende Tabelle, um den Auftragsnamen des Agents zu ermitteln.  
  
|Agent|Auftragsname|  
|-----------|--------------|  
|Merge-Agent für Pullabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< SubscriptionDatabase>-\< Integer>**|  
|Merge-Agent für Pushabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< Integer>**|  
|Verteilungs-Agent für Pushabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< Integer>** <sup>1</sup>|  
|Verteilungs-Agent für Pullabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< SubscriptionDatabase>-\< GUID>** <sup>2</sup>|  
|Verteilungs-Agent für Pushabonnements für Nicht-SQL Server-Abonnenten|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< Integer>**|  
  
 <sup>1</sup> Bei Pushabonnements für Oracle-Veröffentlichungen lautet **\< Publisher>-\< Publisher**> statt **\< Publisher>-\< PublicationDatabase>**  
  
 <sup>2</sup> Bei Pullabonnements für Oracle-Veröffentlichungen lautet **\< Publisher>-\< DistributionDatabase**> statt **\< Publisher>-\< PublicationDatabase>**  
  
#### So geben Sie Synchronisierungszeitpläne an  
  
1.  Auf der **SynchronizationSchedule** Seite des Assistenten für neue Abonnements, wählen Sie einen der folgenden Werte aus der **Agentzeitplan** Dropdown-Liste für jedes Abonnement, das Sie erstellen:  
  
    -   **Fortlaufend ausführen**  
  
    -   **Nur bedarfsgesteuert ausführen**  
  
    -   **\< Zeitplan definieren... >**  
  
2.  Wenn Sie die Option **\< Zeitplan definieren… >**, geben Sie einen Zeitplan in der **Eigenschaften des Auftragszeitplans** (Dialogfeld), und klicken Sie dann auf **OK**.  
  
3.  Schließen Sie den Assistenten ab.  
  
#### So ändern Sie einen Synchronisierungszeitplan für ein Pushabonnement im Replikationsmonitor  
  
1.  Erweitern Sie im linken Bereich des Replikationsmonitors eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
3.  Mit der rechten Maustaste ein Abonnement, und klicken Sie dann auf **Details zum**.  
  
4.  In der **Abonnement \< SubscriptionName >** Fenster, klicken Sie auf **Aktion**, und klicken Sie dann auf **\< AgentName> Auftragseigenschaften**.  
  
5.  Auf der **Zeitpläne** auf der Seite der **Auftragseigenschaften - \< JobName>** im Dialogfeld klicken Sie auf **Bearbeiten.**  
  
6.  In der **Eigenschaften des Auftragszeitplans** Dialogfeld Wählen Sie einen Wert aus der **Zeitplantyp** Dropdown-Liste:  
  
    -   Um eine fortlaufende Ausführung des Agents anzugeben, wählen Sie **Automatisch starten, wenn der SQL Server-Agent startet**aus.  
  
    -   Um eine Ausführung des Agents nach einem Zeitplan anzugeben, wählen Sie **Wiederholt**aus.  
  
    -   Um eine bedarfsgesteuerte Ausführung des Agents anzugeben, wählen Sie **Einmal**aus.  
  
7.  Geben Sie bei der Auswahl von **Wiederholt**einen Zeitplan für den Agent an.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### So ändern Sie einen Synchronisierungszeitplan für ein Pushabonnement in Management Studio  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verteiler her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **SQL Server-Agent** und anschließend den Ordner **Aufträge** .  
  
3.  Mit der rechten Maustaste des Projekts, für das Abonnement Verteilungs-Agent oder Merge-Agent zugeordneten, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Auf der **Zeitpläne** auf der Seite der **Auftragseigenschaften - \< JobName>** im Dialogfeld klicken Sie auf **Bearbeiten.**  
  
5.  In der **Eigenschaften des Auftragszeitplans** Dialogfeld Wählen Sie einen Wert aus der **Zeitplantyp** Dropdown-Liste:  
  
    -   Um eine fortlaufende Ausführung des Agents anzugeben, wählen Sie **Automatisch starten, wenn der SQL Server-Agent startet**aus.  
  
    -   Um eine Ausführung des Agents nach einem Zeitplan anzugeben, wählen Sie **Wiederholt**aus.  
  
    -   Um eine bedarfsgesteuerte Ausführung des Agents anzugeben, wählen Sie **Einmal**aus.  
  
6.  Geben Sie bei der Auswahl von **Wiederholt**einen Zeitplan für den Agent an.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### So ändern Sie einen Synchronisierungszeitplan für ein Pullabonnement in Management Studio  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **SQL Server-Agent** und anschließend den Ordner **Aufträge** .  
  
3.  Mit der rechten Maustaste des Projekts, für das Abonnement Verteilungs-Agent oder Merge-Agent zugeordneten, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Auf der **Zeitpläne** auf der Seite der **Auftragseigenschaften - \< JobName>** im Dialogfeld klicken Sie auf **Bearbeiten.**  
  
5.  In der **Eigenschaften des Auftragszeitplans** Dialogfeld Wählen Sie einen Wert aus der **Zeitplantyp** Dropdown-Liste:  
  
    -   Um eine fortlaufende Ausführung des Agents anzugeben, wählen Sie **Automatisch starten, wenn der SQL Server-Agent startet**aus.  
  
    -   Um eine Ausführung des Agents nach einem Zeitplan anzugeben, wählen Sie **Wiederholt**aus.  
  
    -   Um eine bedarfsgesteuerte Ausführung des Agents anzugeben, wählen Sie **Einmal**aus.  
  
6.  Geben Sie bei der Auswahl von **Wiederholt**einen Zeitplan für den Agent an.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können Synchronisierungszeitpläne mit gespeicherten Replikationsprozeduren programmgesteuert definieren. Welche gespeicherten Prozeduren Sie verwenden, hängt vom Typ der Replikation und vom Typ des Abonnements (Pull oder Push) ab.  
  
 Ein Zeitplan wird definiert durch die folgenden zeitplanungsparameter, deren Verhalten von erbt [Sp_add_schedule & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md):  
  
-   **@frequency_type** -der Typ der Frequenz verwendet, wenn es sich bei der Planung des Agents.  
  
-   **@frequency_interval** – den Tag der Woche, wenn ein Agent ausgeführt wird.  
  
-   **@frequency_relative_interval** – die Woche eines gegebenen Monats, wenn der Agent einmal monatlich ausgeführt geplant ist.  
  
-   **@frequency_recurrence_factor** -die Anzahl der frequenztypeinheiten, die zwischen den Synchronisierungen auftreten.  
  
-   **@frequency_subday** -Frequenz, wenn der Agent häufiger als einmal täglich ausgeführt wird.  
  
-   **@frequency_subday_interval** -die Anzahl der Einheiten für die Frequenz zwischen ausgeführt wird, wenn der Agent häufiger als einmal täglich ausgeführt wird.  
  
-   **@active_start_time_of_day** – den frühesten Zeitpunkt an einem bestimmten Tag, wenn eine Agent-Ausführung gestartet.  
  
-   **@active_end_time_of_day** – die späteste Uhrzeit an einem bestimmten Tag, wenn eine Agent-Ausführung gestartet.  
  
-   **@active_start_date** – den ersten Tag, die der Agentzeitplan aktiviert werden.  
  
-   **@active_end_date** – der letzte Tag, die der Agentzeitplan aktiviert werden.  
  
#### So definieren Sie den Synchronisierungszeitplan für ein Pullabonnement für eine Transaktionsveröffentlichung  
  
1.  Erstellen Sie ein neues Pullabonnement für eine Transaktionsveröffentlichung. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Führen Sie auf dem Abonnenten [Sp_addpullsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Geben Sie **@publisher**, **@publisher_db**, **@publication**, und die [!INCLUDE[msCoName](../../includes/msconame-md.md)] unter dem der Verteilungsagent auf dem Abonnenten ausgeführt, für die wird Windows-Anmeldeinformationen **@job_name** und **@password**. Geben Sie die oben beschriebenen Synchronisierungsparameter an, mit denen der Zeitplan für den Verteilungs-Agentauftrag zur Synchronisierung des Abonnements definiert wird.  
  
#### So definieren Sie den Synchronisierungszeitplan für ein Pushabonnement für eine Transaktionsveröffentlichung  
  
1.  Erstellen Sie ein neues Pushabonnement für eine Transaktionsveröffentlichung. Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Führen Sie auf dem Abonnenten [Sp_addpushsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Geben Sie **@subscriber**, **@subscriber_db**, **@publication**, und die Windows-Anmeldeinformationen, unter dem der Verteilungsagent auf dem Abonnenten ausgeführt, für die wird **@job_name** und **@password**. Geben Sie die oben beschriebenen Synchronisierungsparameter an, mit denen der Zeitplan für den Verteilungs-Agentauftrag zur Synchronisierung des Abonnements definiert wird.  
  
#### So definieren Sie den Synchronisierungszeitplan für ein Pullabonnement für eine Mergeveröffentlichung  
  
1.  Erstellen Sie ein neues Pullabonnement für eine Mergeveröffentlichung. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Führen Sie auf dem Abonnenten [Sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Geben Sie **@publisher**, **@publisher_db**, **@publication**, und die Windows-Anmeldeinformationen, unter dem der Merge-Agent auf dem Abonnenten ausgeführt, für die wird **@job_name** und **@password**. Geben Sie die oben beschriebenen Synchronisierungsparameter an, mit denen der Zeitplan für den Merge-Agentauftrag zur Synchronisierung des Abonnements definiert wird.  
  
#### So definieren Sie den Synchronisierungszeitplan für ein Pushabonnement für eine Mergeveröffentlichung  
  
1.  Erstellen Sie ein neues Pushabonnement für eine Mergeveröffentlichung. Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Führen Sie auf dem Abonnenten [Sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Geben Sie **@subscriber**, **@subscriber_db**, **@publication**, und die Windows-Anmeldeinformationen, unter dem der Merge-Agent auf dem Abonnenten ausgeführt, für die wird **@job_name** und **@password**. Geben Sie die oben beschriebenen Synchronisierungsparameter an, mit denen der Zeitplan für den Merge-Agentauftrag zur Synchronisierung des Abonnements definiert wird.  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Die Replikation verwendet den SQL Server-Agent, um Aufträge für regelmäßig auftretende Aktivitäten wie die Momentaufnahmegenerierung und die Abonnementsynchronisierung zu planen. Sie können Replikationsverwaltungsobjekte (RMO) programmgesteuert verwenden, um Zeitpläne für Replikations-Agentaufträge anzugeben.  
  
> [!NOTE]  
>  Wenn Sie ein Abonnement erstellen, und geben Sie den Wert **false** für **CreateSyncAgentByDefault** (das Standardverhalten für Pullabonnements) der Agentauftrag nicht erstellt und die zeitplanungseigenschaften werden ignoriert. In diesem Fall muss der Synchronisierungszeitplan von der Anwendung bestimmt werden. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) und [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
#### So definieren Sie einen Zeitplan des Replikations-Agents, wenn Sie ein Pushabonnement für eine Transaktionsveröffentlichung erstellen  
  
1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransSubscription> Klasse für das Abonnement, das Sie erstellen. Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Vor dem Aufruf von <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, legen Sie eine oder mehrere der folgenden Felder von der <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> Eigenschaft:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -der Typ der Frequenz (z. B. täglich oder wöchentlich) Sie beim Planen des Agents verwenden.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> – den Tag der Woche, an dem ein Agent ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> – die Woche eines gegebenen Monats, wenn der Agent einmal monatlich ausgeführt geplant ist.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -die Anzahl der frequenztypeinheiten, die zwischen den Synchronisierungen auftreten.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -Frequenz, wenn der Agent häufiger als einmal täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -die Anzahl der Einheiten für die Frequenz zwischen ausgeführt wird, wenn der Agent häufiger als einmal täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - frühesten Zeitpunkt an einem bestimmten Tag, der eine Agent-Ausführung beginnt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - spätesten Zeitpunkt an einem bestimmten Tag, der eine Agent-Ausführung beginnt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> – erste Tag, an dem der Agentzeitplan gültig ist.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> – Letzter Tag, die der Agentzeitplan gültig ist.  
  
    > [!NOTE]  
    >  Wenn Sie keine dieser Eigenschaften angeben, wird ein Standardwert festgelegt.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> Methode, um das Abonnement zu erstellen.  
  
#### So definieren Sie einen Zeitplan des Replikations-Agents, wenn Sie ein Pullabonnement für eine Transaktionsveröffentlichung erstellen  
  
1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPullSubscription> Klasse für das Abonnement, das Sie erstellen. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Vor dem Aufruf von <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, legen Sie eine oder mehrere der folgenden Felder von der <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> Eigenschaft:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -der Typ der Frequenz (z. B. täglich oder wöchentlich), die beim Planen des Agents verwendet.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> – den Tag der Woche, an dem ein Agent ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> – die Woche eines gegebenen Monats, an dem der Agent einmal monatlich ausgeführt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -die Anzahl der frequenztypeinheiten, die zwischen den Synchronisierungen auftreten.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -Frequenz, wenn der Agent häufiger als einmal täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -die Anzahl der Einheiten für die Frequenz zwischen ausgeführt wird, wenn der Agent häufiger als einmal täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - frühesten Zeitpunkt an einem bestimmten Tag, der eine Agent-Ausführung beginnt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - spätesten Zeitpunkt an einem bestimmten Tag, der eine Agent-Ausführung beginnt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> – erste Tag, an dem der Agentzeitplan gültig ist.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> – Letzter Tag, die der Agentzeitplan gültig ist.  
  
    > [!NOTE]  
    >  Wenn Sie keine dieser Eigenschaften angeben, wird ein Standardwert festgelegt.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> Methode, um das Abonnement zu erstellen.  
  
#### So definieren Sie einen Zeitplan des Replikations-Agents, wenn Sie ein Pullabonnement für eine Mergeveröffentlichung erstellen  
  
1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePullSubscription> Klasse für das Abonnement, das Sie erstellen. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Vor dem Aufruf von <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, legen Sie eine oder mehrere der folgenden Felder von der <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> Eigenschaft:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -der Typ der Frequenz (z. B. täglich oder wöchentlich), die beim Planen des Agents verwendet.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> – den Tag der Woche, an dem ein Agent ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> – die Woche eines gegebenen Monats, an dem der Agent einmal monatlich ausgeführt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -die Anzahl der frequenztypeinheiten, die zwischen den Synchronisierungen auftreten.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -Frequenz, wenn der Agent häufiger als einmal täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -die Anzahl der Einheiten für die Frequenz zwischen ausgeführt wird, wenn der Agent häufiger als einmal täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - frühesten Zeitpunkt an einem bestimmten Tag, der eine Agent-Ausführung beginnt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - spätesten Zeitpunkt an einem bestimmten Tag, der eine Agent-Ausführung beginnt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> – erste Tag, an dem der Agentzeitplan gültig ist.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> – Letzter Tag, die der Agentzeitplan gültig ist.  
  
    > [!NOTE]  
    >  Wenn Sie keine dieser Eigenschaften angeben, wird ein Standardwert festgelegt.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> Methode, um das Abonnement zu erstellen.  
  
#### So definieren Sie einen Zeitplan des Replikations-Agents, wenn Sie ein Pushabonnement für eine Mergeveröffentlichung erstellen  
  
1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSubscription> Klasse für das Abonnement, das Sie erstellen. Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Vor dem Aufruf von <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, legen Sie eine oder mehrere der folgenden Felder von der <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> Eigenschaft:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -der Typ der Frequenz (z. B. täglich oder wöchentlich), die beim Planen des Agents verwendet.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> – den Tag der Woche, an dem ein Agent ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> – die Woche eines gegebenen Monats, an dem der Agent einmal monatlich ausgeführt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -die Anzahl der frequenztypeinheiten, die zwischen den Synchronisierungen auftreten.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -Frequenz, wenn der Agent häufiger als einmal täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -die Anzahl der Einheiten für die Frequenz zwischen ausgeführt wird, wenn der Agent häufiger als einmal täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - frühesten Zeitpunkt an einem bestimmten Tag, der eine Agent-Ausführung beginnt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - spätesten Zeitpunkt an einem bestimmten Tag, der eine Agent-Ausführung beginnt.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> – erste Tag, an dem der Agentzeitplan gültig ist.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> – Letzter Tag, die der Agentzeitplan gültig ist.  
  
    > [!NOTE]  
    >  Wenn Sie keine dieser Eigenschaften angeben, wird ein Standardwert festgelegt.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> Methode, um das Abonnement zu erstellen.  
  
###  <a name="PShellExample"></a> Beispiel (RMO)  
 In diesem Beispiel werden ein Pushabonnement für eine Mergeveröffentlichung erstellt und der Zeitplan angegeben, mit dem das Abonnement synchronisiert wird.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## Siehe auch  
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [Synchronisieren eines Pushabonnements](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [Synchronisieren eines Pullabonnements](../../relational-databases/replication/synchronize-a-pull-subscription.md)   
 [Synchronisieren von Daten](../../relational-databases/replication/synchronize-data.md)  
  
  