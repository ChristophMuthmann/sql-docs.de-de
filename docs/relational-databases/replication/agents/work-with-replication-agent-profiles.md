---
title: Arbeiten mit Replikations-Agent-Profilen | Microsoft-Dokumentation
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
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- agents [SQL Server replication], profiles
- profiles [SQL Server], replication agents
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
caps.latest.revision: 49
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d47140507a42084ddf60fa9c54ef6abe43c6f8b6
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="work-with-replication-agent-profiles"></a>Arbeiten mit Replikations-Agent-Profilen
  In diesem Thema wird beschrieben, wie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekten (RMO) mit Replikations-Agentprofilen gearbeitet wird. Das Verhalten der einzelnen Replikations-Agents wird durch eine Reihe von Parametern gesteuert, die über Agentprofile festgelegt werden können. Jeder Agent weist ein Standardprofil auf, und einige Agents besitzen weitere vordefinierte Profile, wobei für einen Agent jeweils immer nur ein Profil aktiv ist.  
  
 **In diesem Thema**  
  
-   **So arbeiten Sie mit Replikations-Agentprofilen mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
    -   Auf das Dialogfeld Agentprofile zugreifen  
  
    -   Ein Profil für einen Agent angeben  
  
    -   Ein Profil erstellen  
  
    -   Ein Profil ändern  
  
    -   Ein Profil löschen  
  
     [Transact-SQL](#TsqlProcedure)  
  
    -   Ein Profil erstellen  
  
    -   Ein Profil ändern  
  
    -   Ein Profil löschen  
  
    -   Agentprofile während der Synchronisierung verwenden  
  
    -   Beispiel für Transact-SQL  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
    -   Ein Profil erstellen  
  
    -   Ein Profil ändern  
  
    -   Ein Profil löschen  
  
-   **Follow Up:**  [After Changing Agent Parameters](#FollowUp)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
###  <a name="Access_SSMS"></a> So greifen Sie auf das Dialogfeld Agentprofile in SQL Server Management Studio zu  
  
1.  Klicken Sie im Dialogfeld **Verteilereigenschaften - \<Distributor>** auf der Seite **Allgemein** auf **Profilstandards**.  
  
#### <a name="to-access-the-agent-profiles-dialog-box-from-replication-monitor"></a>So greifen Sie über den Replikationsmonitor auf das Dialogfeld Agentprofile zu  
  
-   Um das Dialogfeld für alle Agents zu öffnen, klicken Sie mit der rechten Maustaste auf einen Verleger, und klicken Sie dann auf **Agentprofile**.  
  
-   Gehen Sie folgendermaßen vor, um das Dialogfeld für einen Agent zu öffnen:  
  
    1.  Erweitern Sie im linken Bereich des Replikationsmonitors eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
    2.  Klicken Sie bei Verteilungs-Agent- oder Merge-Agent-Profilen auf der Registerkarte **Alle Abonnements** mit der rechten Maustaste auf ein Abonnement, und klicken Sie dann auf **Agentprofil**. Klicken Sie bei anderen Agents auf der Registerkarte **Agents** mit der rechten Maustaste auf den Agent, und klicken Sie dann auf **Agentprofil**.  
  
###  <a name="Specify_SSMS"></a> So geben Sie ein Profil für einen Agent an  
  
1.  Wenn im Dialogfeld **Agentprofile** Profile für mehrere Agents angezeigt werden, wählen Sie einen Agent aus.  
  
2.  Wählen Sie im Raster **Agentprofile** in der **Default for new** -Spalte ein Profil aus. Standardmäßig wird das Profil nur auf Agents für neue Veröffentlichungen und Abonnements angewendet.  
  
3.  Wenn Sie angeben möchten, dass dieses Profil von allen Agents des ausgewählten Typs für vorhandene Veröffentlichungen oder Abonnements verwendet werden soll, klicken Sie auf **Vorhandene Agents ändern**.  
  
###  <a name="Modify_SSMS"></a> So zeigen Sie einem Profil zugeordnete Parameter an und bearbeiten Sie die Parameter  
  
1.  Wenn im Dialogfeld **Agentprofile** Profile für mehrere Agents angezeigt werden, wählen Sie einen Agent aus.  
  
2.  Klicken Sie auf die Eigenschaftenschaltfläche (**…**) neben einem Profil.  
  
3.  Im Dialogfeld **\<Profilname> Profileigenschaften** werden die Parameter und Werte angezeigt.  
  
    -   Parameter in benutzerdefinierten Profilen können bearbeitet werden; Parameter in vordefinierten Systemprofilen können nicht bearbeitet werden.  
  
    -   Um alle Parameter für einen Agent anzuzeigen, deaktivieren Sie das Kontrollkästchen **Nur die in diesem Profil verwendeten Parameter anzeigen** . Informationen zu den Agentparametern finden Sie unter den Links am Ende dieses Themas.  
  
4.  Klicken Sie auf **Schließen**.  
  
###  <a name="Create_SSMS"></a> So erstellen Sie ein benutzerdefiniertes Profil  
  
1.  Wenn im Dialogfeld **Agentprofile** Profile für mehrere Agents angezeigt werden, wählen Sie einen Agent aus.  
  
2.  Klicken Sie auf **Neu**.  
  
3.  Wählen Sie im Initialisierungsdialogfeld **Neues Agentprofil** ein vorhandenes Profil aus, auf dem das neue Profil basieren soll.  
  
4.  Geben Sie im Dialogfeld **Neues Agentprofil** Werte in die Textfelder **Name** und **Beschreibung** ein.  
  
5.  Ändern Sie die Parameter in dem gewünschten Profil entsprechend. Um alle Parameter für einen Agent anzuzeigen, deaktivieren Sie das Kontrollkästchen **Nur die in diesem Profil verwendeten Parameter anzeigen** . Informationen zu den Agentparametern finden Sie unter den Links am Ende dieses Themas.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="Delete_SSMS"></a> So löschen Sie ein benutzerdefiniertes Profil  
  
1.  Wenn im Dialogfeld **Agentprofile** Profile für mehrere Agents angezeigt werden, wählen Sie einen Agent aus.  
  
2.  Wenn ein Profil einem oder mehreren Agents zugeordnet ist, ändern Sie das Profil für diese Agents:  
  
    1.  Wählen Sie im Raster **Agentprofile** ein anderes Profil aus.  
  
    2.  Klicken Sie auf **Vorhandene Agents ändern**.  
  
        > [!NOTE]  
        >  Dadurch wird das Profil nicht nur für die Agents geändert, deren Profil Sie löschen möchten, sondern für alle Agents des ausgewählten Typs für vorhandene Veröffentlichungen oder Abonnements.  
  
3.  Wählen Sie das zu löschende Profil aus, und klicken Sie dann auf **Löschen**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
###  <a name="Create_tsql"></a> So erstellen Sie ein neues Agentprofil  
  
1.  Führen Sie auf dem Verteiler [sp_add_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md) aus. Geben Sie **@name**, einen Wert **1** für **@profile_type**und einen der folgenden Werte für **@agent_type**an:  
  
    -   **1** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Wenn dieses Profil zum neuen Standardprofil für den zugehörigen Typ von Replikations-Agent wird, geben Sie einen Wert **1** für **@default**. Der Bezeichner für das neue Profil wird mithilfe des **@profile_id** -Ausgabeparameters zurückgegeben. Dadurch wird ein neues Profil mit einem Satz von Profilparametern erstellt, das auf dem Standardprofil des bestimmten Agenttyps basiert.  
  
2.  Nach der Erstellung des neuen Profils können Sie Standardparameter hinzufügen, entfernen oder ändern, um das Profil anzupassen.  
  
###  <a name="Modify_tsql"></a> So ändern Sie ein vorhandenes Agentprofil  
  
1.  Führen Sie auf dem Verteiler [sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md) aus. Geben Sie einen der folgenden Werte für **@agent_type**an:  
  
    -   **1** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Dadurch werden alle Profile für den angegebenen Agenttyp zurückgegeben. Beachten Sie den Wert **profile_id** im Resultset für das zu ändernde Profil.  
  
2.  Führen Sie auf dem Verteiler [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md) aus. Geben Sie den Bezeichner des Profils aus Schritt 1 für **@profile_id**. Dadurch werden alle Parameter für das Profil zurückgegeben. Beachten Sie den Namen der zu ändernden Parameter bzw. der aus dem Profil zu entfernenden Parameter.  
  
3.  Führen Sie [sp_change_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md) aus, um den Wert eines Parameters in einem Profil zu ändern. Geben Sie den Bezeichner des Profils aus Schritt 1 für **@profile_id**, den Namen des zu ändernden Parameters für **@property**und einen neuen Wert für den Parameter für **@value**.  
  
    > [!NOTE]  
    >  Es ist nicht möglich, ein vorhandenes Agentprofil in das Standardprofil für einen Agent zu ändern. Stattdessen müssen Sie ein neues Profil als Standardprofil erstellen, wie in der vorherigen Prozedur beschrieben.  
  
4.  Führen [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md) aus, um einen Parameter von einem Profil zu entfernen. Geben Sie den Bezeichner des Profils aus Schritt 1 für **@profile_id** und den Namen des zu entfernenden Parameters für **@parameter_name**.  
  
5.  Sie müssen die folgenden Schritte ausführen, um einem Profil einen neuen Parameter hinzuzufügen:  
  
    -   Fragen Sie die Tabelle [MSagentparameterlist &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) auf dem Verteiler ab, um die Profilparameter zu bestimmen, die für die einzelnen Agenttypen festgelegt werden können.  
  
    -   Führen Sie auf dem Verteiler [sp_add_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md) aus. Geben Sie den Bezeichner des Profils aus Schritt 1 für **@profile_id**, den Namen eines gültigen Parameters zum Hinzufügen für **@parameter_name**und den Wert des Parameters für **@parameter_value**.  
  
###  <a name="Delete_tsql"></a> So löschen Sie ein Agentprofil  
  
1.  Führen Sie auf dem Verteiler [sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md) aus. Geben Sie einen der folgenden Werte für **@agent_type**an:  
  
    -   **1** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Dadurch werden alle Profile für den angegebenen Agenttyp zurückgegeben. Beachten Sie den Wert **profile_id** im Resultset für das zu entfernende Profil.  
  
2.  Führen Sie auf dem Verteiler [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md) aus. Geben Sie den Bezeichner des Profils aus Schritt 1 für **@profile_id**.  
  
###  <a name="Synch_tsql"></a> So verwenden Sie während der Synchronisierung Agentprofile  
  
1.  Führen Sie auf dem Verteiler [sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md) aus. Geben Sie einen der folgenden Werte für **@agent_type**an:  
  
    -   **1** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Dadurch werden alle Profile für den angegebenen Agenttyp zurückgegeben. Beachten Sie den Wert **profile_name** im Resultset für das zu verwendende Profil.  
  
2.  Wenn der Agent in einem Agentauftrag gestartet wird, bearbeiten Sie den Auftragsschritt, mit dem der Agent gestartet wird, um den in Schritt 1 ermittelten Wert **profile_name** nach dem **-ProfileName** -Befehlszeilenparameter anzugeben. Weitere Informationen finden Sie unter [Anzeigen und Ändern von Befehlszeilenparametern des Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md).  
  
3.  Wenn der Agent von der Eingabeaufforderung gestartet wird, geben Sie den in Schritt 1 ermittelten Wert **profile_name** nach dem **-ProfileName** -Befehlszeilenparameter an.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel werden ein benutzerdefiniertes Profil für den Merge-Agent mit der Bezeichnung **custom_merge**erstellt, der Wert des **-UploadReadChangesPerBatch** -Parameters geändert, ein neuer **-ExchangeType** -Parameter hinzugefügt und Informationen zu dem Profil, das erstellt wird, zurückgegeben.  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von RMO  
  
###  <a name="Create_RMO"></a> So erstellen Sie ein neues Agentprofil  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie eine Instanz der <xref:Microsoft.Sqlserver.Management.Common.Serverconnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.AgentProfile>-Klasse.  
  
3.  Legen Sie die folgenden Eigenschaften für das Objekt fest:  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A>: der Name des Profils.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> : ein <xref:Microsoft.SqlServer.Replication.AgentType>-Wert, der den Typ des Replikations-Agents angibt, für den das Profil erstellt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>: Die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1.  
  
    -   (Optional) <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A>: eine Beschreibung des Profils.  
  
    -   (Optional) <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A>: Legen Sie diese Eigenschaft auf **TRUE** fest, wenn alle neuen Agentaufträge für diesen <xref:Microsoft.SqlServer.Replication.AgentType> dieses Profil standardmäßig verwenden.  
  
4.  Rufen Sie die Methode <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> auf, um das Profil auf dem Server zu erstellen.  
  
5.  Sobald das Profil auf dem Server vorhanden ist, können Sie es anpassen, indem Sie Werte für die Parameter für Replikations-Agents hinzufügen, entfernen oder ändern.  
  
6.  Rufen Sie die Methode <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> auf, um das Profil einem vorhandenen Replikationsmerge-Agentauftrag zuzuweisen. Übergeben Sie den Namen der Verteilungsdatenbank für *distributionDBName* und die ID des Auftrags für *agentID*.  
  
###  <a name="Modify_RMO"></a> So ändern Sie ein vorhandenes Agentprofil  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie eine Instanz der <xref:Microsoft.Sqlserver.Management.Common.Serverconnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer>-Klasse. Übergeben Sie das <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt, das Sie in Schritt 1 erstellt haben.  
  
3.  Rufen Sie die Methode <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> auf. Überprüfen Sie, ob der Verteiler vorhanden ist, wenn diese Methode **false**zurückgibt.  
  
4.  Rufen Sie die Methode <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> auf. Übergeben Sie einen <xref:Microsoft.SqlServer.Replication.AgentType>-Wert, um die zurückgegebenen Profile für einen bestimmten Typ von Replikations-Agent einzugrenzen.  
  
5.  Rufen Sie das gewünschte <xref:Microsoft.SqlServer.Replication.AgentProfile>-Objekt von dem zurückgegebenen <xref:System.Collections.ArrayList>-Objekt auf, wobei die Eigenschaft <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> mit dem Namen des Profils übereinstimmt.  
  
6.  Rufen Sie eine der folgenden Methoden von <xref:Microsoft.SqlServer.Replication.AgentProfile> auf, um das Profil zu ändern:  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A>: fügt dem Profil einen unterstützten Parameter hinzu, wobei es sich bei *name* um den Namen des Replikations-Agent-Parameters und bei *value* um den angegebenen Wert handelt. Rufen Sie zum Aufzählen aller unterstützten Agentparameter für einen bestimmten Agenttyp die Methode <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> auf. Diese Methode gibt ein <xref:System.Collections.ArrayList>-Objekt von <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo>-Objekten zurück, das alle unterstützen Parameter darstellt.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A>: fügt dem Profil einen unterstützen Parameter hinzu, wobei es sich bei *name* um den Namen des Replikations-Agent-Parameters handelt. Rufen Sie zum Aufzählen aller aktuellen Agentparameter, die für das Profil definiert sind, die Methode <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> auf. Diese Methode gibt eine <xref:System.Collections.ArrayList> von <xref:Microsoft.SqlServer.Replication.AgentProfileParameter>-Objekten zurück, die den vorhandenen Parameter für dieses Profil darstellt.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A>: ändert die Einstellung eines vorhandenen Parameters im Profil, wobei *name* der Name des Agentparameters und *newValue* der Wert ist, in den der Parameter geändert wird. Rufen Sie zum Aufzählen aller aktuellen Agentparameter, die für das Profil definiert sind, die Methode <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> auf. Diese Methode gibt eine <xref:System.Collections.ArrayList> von <xref:Microsoft.SqlServer.Replication.AgentProfileParameter>-Objekten zurück, die den vorhandenen Parameter für dieses Profil darstellt. Rufen Sie zum Aufzählen aller unterstützten Einstellungen für den Agentparameter die <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A>-Methode auf. Diese Methode gibt eine <xref:System.Collections.ArrayList> von <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo>-Objekten zurück, die die unterstützen Werte für alle Parameter darstellt.  
  
###  <a name="Delete_RMO"></a> So löschen Sie ein Agentprofil  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie eine Instanz der <xref:Microsoft.Sqlserver.Management.Common.Serverconnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.AgentProfile>-Klasse. Legen Sie den Namen des Profils für <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> und <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> fest.  
  
3.  Rufen Sie die Methode <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> auf. Wenn diese Methode **false**zurückgibt, wurde ein falscher Name angegeben, oder das Profil ist auf dem Server nicht vorhanden.  
  
4.  Stellen Sie sicher, dass die Eigenschaft <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> auf <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User> festgelegt ist, wodurch ein Kundenprofil angegeben wird. Entfernen Sie kein Profil, das einen Wert <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> für <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> aufweist.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A>-Methode auf, um das benutzerdefinierte Profil, das durch dieses Objekt dargestellt wird, vom Server zu entfernen.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Ändern der Agentparameter  
 Die Änderungen der Agentparameter treten in Kraft, wenn der Agent das nächste Mal gestartet wird. Wenn der Agent ständig ausgeführt wird, müssen Sie den Agent beenden und neu starten.  
  
## <a name="see-also"></a>Siehe auch  
 [Replikations-Agent-Profile](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  
