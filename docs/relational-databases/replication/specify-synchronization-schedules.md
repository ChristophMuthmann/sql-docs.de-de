---
title: "Angeben von Synchronisierungszeitplänen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication], synchronizing
- scheduling synchronization [SQL Server replication]
- synchronization [SQL Server replication], schedules
- replication [SQL Server], synchronization
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1d131e8e7aee66186245b0d69acb1b5c10285cf3
ms.lasthandoff: 04/11/2017

---
# <a name="specify-synchronization-schedules"></a>Angeben von Synchronisierungszeitplänen
  In diesem Thema wird beschrieben, wie Synchronisierungszeitpläne in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekten (RMO) angegeben werden. Während der Erstellung eines Abonnements kann ein Synchronisierungszeitplan definiert werden, der steuert, wann der Replikations-Agent für das Abonnement ausgeführt wird. Wenn Sie keine Zeitplanungsparameter angeben, wird der Standardzeitplan für das Abonnement verwendet.  
  
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
|Merge-Agent für Pullabonnements|**\<Verleger>-\<Veröffentlichungsdatenbank>-\<Veröffentlichung>-\<Abonnent>-\<Abonnementdatenbank>-\<Integer>**|  
|Merge-Agent für Pushabonnements|**\<Verleger>-\<Veröffentlichungsdatenbank>-\<Veröffentlichung>-\<Abonnent>-\<Integer>**|  
|Verteilungs-Agent für Pushabonnements|**\<Verleger>-\<Veröffentlichungsdatenbank>-\<Veröffentlichung>-\<Abonnent>-\<Integer>** <sup>1</sup>|  
|Verteilungs-Agent für Pullabonnements|**\<Verleger>-\<Veröffentlichungsdatenbank>-\<Veröffentlichung>-\<Abonnent>-\<Abonnementdatenbank>-\<GUID>** <sup>2</sup>|  
|Verteilungs-Agent für Pushabonnements für Nicht-SQL Server-Abonnenten|**\<Verleger>-\<Veröffentlichungsdatenbank>-\<Veröffentlichung>-\<Abonnent>-\<Integer>**|  
  
 <sup>1</sup> Bei Pushabonnements für Oracle-Veröffentlichungen heißt es **\<Verleger>-\<Verleger**> anstatt **\<Verleger>-\<Veröffentlichungsdatenbank>**.  
  
 <sup>2</sup> Bei Pullabonnements für Oracle-Veröffentlichungen heißt es **\<Verleger>-\<Verteilungsdatenbank**> anstatt **\<Verleger>-\<Veröffentlichungsdatenbank>**.  
  
#### <a name="to-specify-synchronization-schedules"></a>So geben Sie Synchronisierungszeitpläne an  
  
1.  Wählen Sie im Assistenten für neue Abonnements auf der Seite **Synchronisierungszeitplan** für jedes Abonnement, das Sie erstellen, einen der folgenden Werte aus der Dropdownliste **Agentzeitplan** aus:  
  
    -   **Fortlaufend ausführen**  
  
    -   **Nur bedarfsgesteuert ausführen**  
  
    -   **\<Zeitplan definieren…>**  
  
2.  Geben Sie bei der Auswahl von **\<Zeitplan definieren…>** im Dialogfeld **Eigenschaften des Auftragszeitplans** einen Zeitplan an, und klicken Sie dann auf **OK**.  
  
3.  Schließen Sie den Assistenten ab.  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-replication-monitor"></a>So ändern Sie einen Synchronisierungszeitplan für ein Pushabonnement im Replikationsmonitor  
  
1.  Erweitern Sie im linken Bereich des Replikationsmonitors eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
3.  Klicken Sie mit der rechten Maustaste auf ein Abonnement, und klicken Sie dann auf **Details anzeigen**.  
  
4.  Klicken Sie im Fenster **Abonnement <Abonnementname>** auf **Aktion**, und klicken Sie dann auf **\<AgentName> Auftragseigenschaften**.  
  
5.  Klicken Sie im Dialogfeld **Auftragseigenschaften - \<JobName>** auf der Seite **Zeitpläne** auf **Bearbeiten**.  
  
6.  Wählen Sie im Dialogfeld **Eigenschaften des Auftragszeitplans** einen Wert aus der Dropdownliste **Zeitplantyp** aus:  
  
    -   Um eine fortlaufende Ausführung des Agents anzugeben, wählen Sie **Automatisch starten, wenn der SQL Server-Agent startet**aus.  
  
    -   Um eine Ausführung des Agents nach einem Zeitplan anzugeben, wählen Sie **Wiederholt**aus.  
  
    -   Um eine bedarfsgesteuerte Ausführung des Agents anzugeben, wählen Sie **Einmal**aus.  
  
7.  Geben Sie bei der Auswahl von **Wiederholt**einen Zeitplan für den Agent an.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-management-studio"></a>So ändern Sie einen Synchronisierungszeitplan für ein Pushabonnement in Management Studio  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verteiler her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **SQL Server-Agent** und anschließend den Ordner **Aufträge** .  
  
3.  Klicken Sie mit der rechten Maustaste auf den Auftrag für den Verteilungs-Agent oder Merge-Agent, der dem Abonnement zugeordnet ist, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie im Dialogfeld **Auftragseigenschaften - \<JobName>** auf der Seite **Zeitpläne** auf **Bearbeiten**.  
  
5.  Wählen Sie im Dialogfeld **Eigenschaften des Auftragszeitplans** einen Wert aus der Dropdownliste **Zeitplantyp** aus:  
  
    -   Um eine fortlaufende Ausführung des Agents anzugeben, wählen Sie **Automatisch starten, wenn der SQL Server-Agent startet**aus.  
  
    -   Um eine Ausführung des Agents nach einem Zeitplan anzugeben, wählen Sie **Wiederholt**aus.  
  
    -   Um eine bedarfsgesteuerte Ausführung des Agents anzugeben, wählen Sie **Einmal**aus.  
  
6.  Geben Sie bei der Auswahl von **Wiederholt**einen Zeitplan für den Agent an.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-pull-subscription-in-management-studio"></a>So ändern Sie einen Synchronisierungszeitplan für ein Pullabonnement in Management Studio  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **SQL Server-Agent** und anschließend den Ordner **Aufträge** .  
  
3.  Klicken Sie mit der rechten Maustaste auf den Auftrag für den Verteilungs-Agent oder Merge-Agent, der dem Abonnement zugeordnet ist, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie im Dialogfeld **Auftragseigenschaften - \<JobName>** auf der Seite **Zeitpläne** auf **Bearbeiten**.  
  
5.  Wählen Sie im Dialogfeld **Eigenschaften des Auftragszeitplans** einen Wert aus der Dropdownliste **Zeitplantyp** aus:  
  
    -   Um eine fortlaufende Ausführung des Agents anzugeben, wählen Sie **Automatisch starten, wenn der SQL Server-Agent startet**aus.  
  
    -   Um eine Ausführung des Agents nach einem Zeitplan anzugeben, wählen Sie **Wiederholt**aus.  
  
    -   Um eine bedarfsgesteuerte Ausführung des Agents anzugeben, wählen Sie **Einmal**aus.  
  
6.  Geben Sie bei der Auswahl von **Wiederholt**einen Zeitplan für den Agent an.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können Synchronisierungszeitpläne mit gespeicherten Replikationsprozeduren programmgesteuert definieren. Welche gespeicherten Prozeduren Sie verwenden, hängt vom Typ der Replikation und vom Typ des Abonnements (Pull oder Push) ab.  
  
 Ein Zeitplan wird durch die folgenden Zeitplanungsparameter definiert, deren Verhalten von [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md) geerbt wird:  
  
-   **@frequency_type** &ndash; der Typ der Frequenz, der bei der Planung des Agents verwendet wird.  
  
-   **@frequency_interval** &ndash; der Tag der Woche, an dem ein Agent ausgeführt wird.  
  
-   **@frequency_relative_interval** &ndash; die Woche eines gegebenen Monats, in der der Agent einmal monatlich ausgeführt wird.  
  
-   **@frequency_recurrence_factor** &ndash; die Anzahl der Einheiten für die Frequenz, die zwischen den einzelnen Synchronisierungen liegen.  
  
-   **@frequency_subday** &ndash; die Einheit für die Frequenz, wenn der Agent täglich mehrmals ausgeführt wird.  
  
-   **@frequency_subday_interval** &ndash; die Anzahl der Einheiten für die Frequenz, die zwischen den einzelnen Ausführungen liegen, wenn der Agent mehrmals täglich ausgeführt wird.  
  
-   **@active_start_time_of_day** &ndash; die früheste Uhrzeit an einem gegebenen Tag, zu der eine Agent-Ausführung gestartet wird.  
  
-   **@active_end_time_of_day** &ndash; die späteste Uhrzeit an einem gegebenen Tag, zu der eine Agent-Ausführung gestartet wird.  
  
-   **@active_start_date** &ndash; der erste Tag, an dem der Agentzeitplan gültig ist.  
  
-   **@active_end_date** &ndash; der letzte Tag, an dem der Agentzeitplan gültig ist.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-transactional-publication"></a>So definieren Sie den Synchronisierungszeitplan für ein Pullabonnement für eine Transaktionsveröffentlichung  
  
1.  Erstellen Sie ein neues Pullabonnement für eine Transaktionsveröffentlichung. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Führen Sie auf dem Abonnenten [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) aus. Geben Sie **@publisher**, **@publisher_db**, **@publication**und die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen, unter denen der Verteilungs-Agent auf dem Abonnenten ausgeführt wird, für **@job_name** und **@password**. Geben Sie die oben beschriebenen Synchronisierungsparameter an, mit denen der Zeitplan für den Verteilungs-Agentauftrag zur Synchronisierung des Abonnements definiert wird.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-transactional-publication"></a>So definieren Sie den Synchronisierungszeitplan für ein Pushabonnement für eine Transaktionsveröffentlichung  
  
1.  Erstellen Sie ein neues Pushabonnement für eine Transaktionsveröffentlichung. Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Führen Sie auf dem Abonnenten [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) aus. Geben Sie **@subscriber**, **@subscriber_db**, **@publication**und die Windows-Anmeldeinformationen, unter denen der Verteilungs-Agent auf dem Abonnenten ausgeführt wird, für **@job_name** und **@password**. Geben Sie die oben beschriebenen Synchronisierungsparameter an, mit denen der Zeitplan für den Verteilungs-Agentauftrag zur Synchronisierung des Abonnements definiert wird.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-merge-publication"></a>So definieren Sie den Synchronisierungszeitplan für ein Pullabonnement für eine Mergeveröffentlichung  
  
1.  Erstellen Sie ein neues Pullabonnement für eine Mergeveröffentlichung. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Führen Sie auf dem Abonnenten [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)aus. Geben Sie **@publisher**, **@publisher_db**, **@publication**und die Windows-Anmeldeinformationen, unter denen der Merge-Agent auf dem Abonnenten ausgeführt wird, für **@job_name** und **@password**. Geben Sie die oben beschriebenen Synchronisierungsparameter an, mit denen der Zeitplan für den Merge-Agentauftrag zur Synchronisierung des Abonnements definiert wird.  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-merge-publication"></a>So definieren Sie den Synchronisierungszeitplan für ein Pushabonnement für eine Mergeveröffentlichung  
  
1.  Erstellen Sie ein neues Pushabonnement für eine Mergeveröffentlichung. Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Führen Sie auf dem Abonnenten [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)aus. Geben Sie **@subscriber**, **@subscriber_db**, **@publication**und die Windows-Anmeldeinformationen, unter denen der Merge-Agent auf dem Abonnenten ausgeführt wird, für **@job_name** und **@password**. Geben Sie die oben beschriebenen Synchronisierungsparameter an, mit denen der Zeitplan für den Merge-Agentauftrag zur Synchronisierung des Abonnements definiert wird.  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Die Replikation verwendet den SQL Server-Agent, um Aufträge für regelmäßig auftretende Aktivitäten wie die Momentaufnahmegenerierung und die Abonnementsynchronisierung zu planen. Sie können Replikationsverwaltungsobjekte (RMO) programmgesteuert verwenden, um Zeitpläne für Replikations-Agentaufträge anzugeben.  
  
> [!NOTE]  
>  Wenn Sie ein Abonnement erstellen und den Wert **false** für **CreateSyncAgentByDefault** (das Standardverhalten für Pullabonnements) angeben, wird der Agentauftrag nicht erstellt und die Zeitplanungseigenschaften werden ignoriert. In diesem Fall muss der Synchronisierungszeitplan von der Anwendung bestimmt werden. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) und [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-transactional-publication"></a>So definieren Sie einen Zeitplan des Replikations-Agents, wenn Sie ein Pushabonnement für eine Transaktionsveröffentlichung erstellen  
  
1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransSubscription>-Klasse für das Abonnement, das Sie erstellen. Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Bevor Sie <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> aufrufen, legen Sie mindestens eines der folgenden Felder der <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A>-Eigenschaft fest:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> – der Typ der Frequenz (z.B. täglich oder wöchentlich), den Sie beim Planen des Agents verwenden.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> – der Tag der Woche, an dem ein Agent ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> – die Woche eines bestimmten Monats, wenn der Agent monatlich ausgeführt werden soll.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> – die Anzahl der Einheiten für die Frequenz, die zwischen den einzelnen Synchronisierungen liegen.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> – die Einheit für die Frequenz, wenn der Agent öfter als täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> – die Anzahl der Einheiten für die Frequenz, die zwischen den einzelnen Ausführungen liegen, wenn der Agent öfter als täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A – der früheste Zeitpunkt an einem bestimmten Tag, zu dem eine Agentausführung gestartet wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> – der späteste Zeitpunkt an einem bestimmten Tag, zu dem eine Agentausführung gestartet wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> – der erste Tag, an dem der Agentzeitplan in Kraft ist.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> – der letzte Tag, an dem der Agentzeitplan in Kraft ist.  
  
    > [!NOTE]  
    >  Wenn Sie keine dieser Eigenschaften angeben, wird ein Standardwert festgelegt.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>-Methode auf, um das Abonnement zu erstellen.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-transactional-publication"></a>So definieren Sie einen Zeitplan des Replikations-Agents, wenn Sie ein Pullabonnement für eine Transaktionsveröffentlichung erstellen  
  
1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPullSubscription>-Klasse für das Abonnement, das Sie erstellen. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Bevor Sie <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> aufrufen, legen Sie mindestens eines der folgenden Felder der <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A>-Eigenschaft fest:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> – der Typ der Frequenz (z.B. täglich oder wöchentlich), den Sie beim Planen des Agents verwenden.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> – der Tag der Woche, an dem ein Agent ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> – die Woche eines bestimmten Monats, in der der Agent monatlich ausgeführt werden soll.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> – die Anzahl der Einheiten für die Frequenz, die zwischen den einzelnen Synchronisierungen liegen.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> – die Einheit für die Frequenz, wenn der Agent öfter als täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> – die Anzahl der Einheiten für die Frequenz, die zwischen den einzelnen Ausführungen liegen, wenn der Agent öfter als täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A – der früheste Zeitpunkt an einem bestimmten Tag, zu dem eine Agentausführung gestartet wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> – der späteste Zeitpunkt an einem bestimmten Tag, zu dem eine Agentausführung gestartet wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> – der erste Tag, an dem der Agentzeitplan in Kraft ist.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> – der letzte Tag, an dem der Agentzeitplan in Kraft ist.  
  
    > [!NOTE]  
    >  Wenn Sie keine dieser Eigenschaften angeben, wird ein Standardwert festgelegt.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>-Methode auf, um das Abonnement zu erstellen.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-merge-publication"></a>So definieren Sie einen Zeitplan des Replikations-Agents, wenn Sie ein Pullabonnement für eine Mergeveröffentlichung erstellen  
  
1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePullSubscription>-Klasse für das Abonnement, das Sie erstellen. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Bevor Sie <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> aufrufen, legen Sie mindestens eines der folgenden Felder der <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A>-Eigenschaft fest:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> – der Typ der Frequenz (z.B. täglich oder wöchentlich), den Sie beim Planen des Agents verwenden.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> – der Tag der Woche, an dem ein Agent ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> – die Woche eines bestimmten Monats, in der der Agent monatlich ausgeführt werden soll.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> – die Anzahl der Einheiten für die Frequenz, die zwischen den einzelnen Synchronisierungen liegen.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> – die Einheit für die Frequenz, wenn der Agent öfter als täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> – die Anzahl der Einheiten für die Frequenz, die zwischen den einzelnen Ausführungen liegen, wenn der Agent öfter als täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A – der früheste Zeitpunkt an einem bestimmten Tag, zu dem eine Agentausführung gestartet wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> – der späteste Zeitpunkt an einem bestimmten Tag, zu dem eine Agentausführung gestartet wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> – der erste Tag, an dem der Agentzeitplan in Kraft ist.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> – der letzte Tag, an dem der Agentzeitplan in Kraft ist.  
  
    > [!NOTE]  
    >  Wenn Sie keine dieser Eigenschaften angeben, wird ein Standardwert festgelegt.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>-Methode auf, um das Abonnement zu erstellen.  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-merge-publication"></a>So definieren Sie einen Zeitplan des Replikations-Agents, wenn Sie ein Pushabonnement für eine Mergeveröffentlichung erstellen  
  
1.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSubscription>-Klasse für das Abonnement, das Sie erstellen. Weitere Informationen finden Sie unter [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Bevor Sie <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> aufrufen, legen Sie mindestens eines der folgenden Felder der <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A>-Eigenschaft fest:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> – der Typ der Frequenz (z.B. täglich oder wöchentlich), den Sie beim Planen des Agents verwenden.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> – der Tag der Woche, an dem ein Agent ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> – die Woche eines bestimmten Monats, in der der Agent monatlich ausgeführt werden soll.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> – die Anzahl der Einheiten für die Frequenz, die zwischen den einzelnen Synchronisierungen liegen.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> – die Einheit für die Frequenz, wenn der Agent öfter als täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> – die Anzahl der Einheiten für die Frequenz, die zwischen den einzelnen Ausführungen liegen, wenn der Agent öfter als täglich ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A – der früheste Zeitpunkt an einem bestimmten Tag, zu dem eine Agentausführung gestartet wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> – der späteste Zeitpunkt an einem bestimmten Tag, zu dem eine Agentausführung gestartet wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> – der erste Tag, an dem der Agentzeitplan in Kraft ist.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> – der letzte Tag, an dem der Agentzeitplan in Kraft ist.  
  
    > [!NOTE]  
    >  Wenn Sie keine dieser Eigenschaften angeben, wird ein Standardwert festgelegt.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>-Methode auf, um das Abonnement zu erstellen.  
  
###  <a name="PShellExample"></a> Beispiel (RMO)  
 In diesem Beispiel werden ein Pushabonnement für eine Mergeveröffentlichung erstellt und der Zeitplan angegeben, mit dem das Abonnement synchronisiert wird.  
  
 [!code-cs[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>Siehe auch  
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [Synchronisieren eines Pushabonnements](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [Synchronisieren eines Pullabonnements](../../relational-databases/replication/synchronize-a-pull-subscription.md)   
 [Synchronisieren von Daten](../../relational-databases/replication/synchronize-data.md)  
  
  

