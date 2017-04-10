---
title: "Arbeiten mit Replikations-Agent-Profilen | Microsoft Docs"
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
  - "Replikation [SQL Server], Agents und Profile"
  - "Replikations-Agentprofile [SQL Server]"
  - "Agents [SQL Server-Replikation], Profile"
  - "Profile [SQL Server], Replikations-Agents"
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
caps.latest.revision: 49
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 49
---
# Arbeiten mit Replikations-Agent-Profilen
  In diesem Thema wird beschrieben, wie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) mit Replikations-Agentprofilen gearbeitet wird. Das Verhalten der einzelnen Replikations-Agents wird durch eine Reihe von Parametern gesteuert, die über Agentprofile festgelegt werden können. Jeder Agent weist ein Standardprofil auf, und einige Agents besitzen weitere vordefinierte Profile, wobei für einen Agent jeweils immer nur ein Profil aktiv ist.  
  
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
  
-   **Nachverfolgung:**  [Nach dem Ändern der Agentparameter](#FollowUp)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
###  <a name="Access_SSMS"></a> So greifen Sie auf das Dialogfeld Agentprofile in SQL Server Management Studio zu  
  
1.  Auf die **Allgemein** auf der Seite der **Verteilereigenschaften - \< Verteiler>** im Dialogfeld klicken Sie auf **Profilstandards**.  
  
#### So greifen Sie über den Replikationsmonitor auf das Dialogfeld Agentprofile zu  
  
-   Zum Öffnen des Dialogfelds für alle Agents mit der rechten Maustaste eines Verlegers, und klicken Sie dann auf **Agentprofile**.  
  
-   Gehen Sie folgendermaßen vor, um das Dialogfeld für einen Agent zu öffnen:  
  
    1.  Erweitern Sie im linken Bereich des Replikationsmonitors eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
    2.  Snapshot-Agent und Merge-Agent-Profilen, mit der rechten Maustaste ein Abonnement für die **alle Abonnements** Registerkarte, und klicken Sie dann auf **Agentprofil**. Bei anderen Agents mit der rechten Maustaste des Agents auf dem **Agents** Registerkarte, und klicken Sie dann auf **Agentprofil**.  
  
###  <a name="Specify_SSMS"></a> So geben Sie ein Profil für einen Agent an  
  
1.  Wenn im Dialogfeld **Agentprofile** Profile für mehrere Agents angezeigt werden, wählen Sie einen Agent aus.  
  
2.  Wählen Sie im Raster **Agentprofile** in der **Default for new** -Spalte ein Profil aus. Standardmäßig wird das Profil nur auf Agents für neue Veröffentlichungen und Abonnements angewendet.  
  
3.  Wenn Sie angeben möchten, dass dieses Profil von allen Agents des ausgewählten Typs für vorhandene Veröffentlichungen oder Abonnements verwendet werden soll, klicken Sie auf **Vorhandene Agents ändern**.  
  
###  <a name="Modify_SSMS"></a> So zeigen Sie einem Profil zugeordnete Parameter an und bearbeiten Sie die Parameter  
  
1.  Wenn im Dialogfeld **Agentprofile** Profile für mehrere Agents angezeigt werden, wählen Sie einen Agent aus.  
  
2.  Klicken Sie auf die Eigenschaftenschaltfläche (**...**) neben einem Profil.  
  
3.  Zeigen Sie die Parameter und Werte in der **\< ProfileName> Profileigenschaften** Dialogfeld.  
  
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
  
1.  Führen Sie auf dem Verteiler [Sp_add_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md). Geben Sie **@name**, ein Wert von **1** für **@profile_type**, und einen der folgenden Werte für **@agent_type**:  
  
    -   **1** - [Replikationsmomentaufnahme-Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replikationsprotokolllese-Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [replikationsverteilungs-Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replikationsmerge-Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replikation Warteschlangenlese-Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Wenn dieses Profil zum neuen Standardprofil für den zugehörigen Typ von Replikations-Agent wird, geben Sie einen Wert **1** für **@default**an. Der Bezeichner für das neue Profil wird zurückgegeben, mit der **@profile_id** -Ausgabeparameter. Dadurch wird ein neues Profil mit einem Satz von Profilparametern erstellt, das auf dem Standardprofil des bestimmten Agenttyps basiert.  
  
2.  Nach der Erstellung des neuen Profils können Sie Standardparameter hinzufügen, entfernen oder ändern, um das Profil anzupassen.  
  
###  <a name="Modify_tsql"></a> So ändern Sie ein vorhandenes Agentprofil  
  
1.  Führen Sie auf dem Verteiler [Sp_help_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Geben Sie einen der folgenden Werte für **@agent_type**:  
  
    -   **1** - [Replikationsmomentaufnahme-Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replikationsprotokolllese-Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [replikationsverteilungs-Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replikationsmerge-Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replikation Warteschlangenlese-Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Dadurch werden alle Profile für den angegebenen Agenttyp zurückgegeben. Beachten Sie den Wert der **Profile_id** im Resultset für das zu ändernde Profil.  
  
2.  Führen Sie auf dem Verteiler [Sp_help_agent_parameter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md). Geben Sie den Bezeichner des Profils aus Schritt 1 für **@profile_id**. Dadurch werden alle Parameter für das Profil zurückgegeben. Beachten Sie den Namen der zu ändernden Parameter bzw. der aus dem Profil zu entfernenden Parameter.  
  
3.  Um den Wert eines Parameters in einem Profil zu ändern, führen [Sp_change_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md). Geben Sie den Bezeichner des Profils aus Schritt 1 für **@profile_id**, den Namen des Parameters ändern für **@property**, und einen neuen Wert für den Parameter für **@value**.  
  
    > [!NOTE]  
    >  Es ist nicht möglich, ein vorhandenes Agentprofil in das Standardprofil für einen Agent zu ändern. Stattdessen müssen Sie ein neues Profil als Standardprofil erstellen, wie in der vorherigen Prozedur beschrieben.  
  
4.  Um einen Parameter aus einem Profil zu entfernen, führen [Sp_drop_agent_parameter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md). Geben Sie den Bezeichner des Profils aus Schritt 1 für **@profile_id** und den Namen des Parameters, der für entfernen **@parameter_name**.  
  
5.  Sie müssen die folgenden Schritte ausführen, um einem Profil einen neuen Parameter hinzuzufügen:  
  
    -   Abfrage der [MSagentparameterlist & #40; Transact-SQL & #41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) die Tabelle auf dem Verteiler, um zu bestimmen, welche Parameter für die einzelnen Agenttypen festgelegt werden können.  
  
    -   Führen Sie auf dem Verteiler [Sp_add_agent_parameter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md). Geben Sie den Bezeichner des Profils aus Schritt 1 für **@profile_id**, den Namen eines gültigen Parameters zum Hinzufügen für **@parameter_name**, und der Wert des Parameters für **@parameter_value**.  
  
###  <a name="Delete_tsql"></a> So löschen Sie ein Agentprofil  
  
1.  Führen Sie auf dem Verteiler [Sp_help_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Geben Sie einen der folgenden Werte für **@agent_type**:  
  
    -   **1** - [Replikationsmomentaufnahme-Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replikationsprotokolllese-Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [replikationsverteilungs-Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replikationsmerge-Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replikation Warteschlangenlese-Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Dadurch werden alle Profile für den angegebenen Agenttyp zurückgegeben. Beachten Sie den Wert der **Profile_id** im Resultset für das Profil zu entfernen.  
  
2.  Führen Sie auf dem Verteiler [Sp_drop_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md). Geben Sie den Bezeichner des Profils aus Schritt 1 für **@profile_id**.  
  
###  <a name="Synch_tsql"></a> So verwenden Sie während der Synchronisierung Agentprofile  
  
1.  Führen Sie auf dem Verteiler [Sp_help_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Geben Sie einen der folgenden Werte für **@agent_type**:  
  
    -   **1** - [Replikationsmomentaufnahme-Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replikationsprotokolllese-Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [replikationsverteilungs-Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replikationsmerge-Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replikation Warteschlangenlese-Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Dadurch werden alle Profile für den angegebenen Agenttyp zurückgegeben. Beachten Sie den Wert der **Profile_name** im Resultset für das zu verwendende Profil.  
  
2.  Wenn der Agent in einem Agentauftrag gestartet wird, bearbeiten Sie den Auftragsschritt, den Agent zum Angeben des Werts von **Profile_name** die in Schritt 1 nach der **- ProfileName** Befehlszeilenparameter. Weitere Informationen finden Sie unter [anzeigen und ändern Sie Replikations-Agent Befehlszeilenparameter & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md).  
  
3.  Wenn den Agent über die Befehlszeile gestartet wird, geben Sie den Wert von **Profile_name** die in Schritt 1 nach der **- ProfileName** Befehlszeilenparameter.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 Dieses Beispiel erstellt ein benutzerdefiniertes Profil für den Merge-Agent mit dem Namen **Custom_merge**, ändert den Wert der **- UploadReadChangesPerBatch** -Parameter wird ein neues **- ExchangeType** Parameter und gibt Informationen über das Profil, das erstellt wird.  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von RMO  
  
###  <a name="Create_RMO"></a> So erstellen Sie ein neues Agentprofil  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe einer Instanz von der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.AgentProfile> Klasse.  
  
3.  Legen Sie die folgenden Eigenschaften für das Objekt fest:  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> -der Name des Profils.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> : eine <xref:Microsoft.SqlServer.Replication.AgentType> -Wert, der den Typ des Replikations-Agent angibt, für den das Profil erstellt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> – der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> in Schritt 1 erstellt haben.  
  
    -   (Optional) <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A> -eine Beschreibung des Profils.  
  
    -   (Optional) <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A> -Legen Sie diese Eigenschaft auf **true** Wenn alle neuen Agentaufträge für diesen <xref:Microsoft.SqlServer.Replication.AgentType> dieses Profil standardmäßig verwenden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> Methode, um das Profil auf dem Server zu erstellen.  
  
5.  Sobald das Profil auf dem Server vorhanden ist, können Sie es anpassen, indem Sie Werte für die Parameter für Replikations-Agents hinzufügen, entfernen oder ändern.  
  
6.  Das Profil einem vorhandenen Auftrag des Replikations-Agents zuweisen möchten, rufen Sie die <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> Methode. Übergeben Sie den Namen der Verteilungsdatenbank für *distributionDBName* und die ID des Auftrags für *agentID*.  
  
###  <a name="Modify_RMO"></a> So ändern Sie ein vorhandenes Agentprofil  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe einer Instanz von der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer> Klasse. Übergeben Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> in Schritt 1 erstellte Objekt.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Überprüfen Sie, ob der Verteiler vorhanden ist, wenn diese Methode **false**zurückgibt.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> Methode. Übergeben Sie ein <xref:Microsoft.SqlServer.Replication.AgentType> Wert, der die zurückgegebenen Profile für einen bestimmten Typ von Replikations-Agent einzugrenzen.  
  
5.  Rufen Sie das gewünschte <xref:Microsoft.SqlServer.Replication.AgentProfile> -Objekt von der zurückgegebenen <xref:System.Collections.ArrayList>, wobei die <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> -Eigenschaft des Objekts mit dem Profilnamen übereinstimmt.  
  
6.  Rufen Sie eine der folgenden Methoden der <xref:Microsoft.SqlServer.Replication.AgentProfile> Ändern des Profils:  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A> -Profil einen unterstützten Parameter hinzugefügt, in denen *Namen* ist der Name des Parameters der Replikations-Agent und *Wert* ist der angegebene Wert. Rufen Sie zum Auflisten aller unterstützten Agentparameter für einen bestimmten Agenttyp die <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> Methode. Diese Methode gibt ein <xref:System.Collections.ArrayList> von <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> -Objekten, die alle unterstützten Parameter darstellen.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A> -entfernt einen vorhandenen Parameter aus dem Profil, wobei *Namen* ist der Name des Parameters der Replikations-Agent. Rufen Sie zum Auflisten aller aktuellen Agentparameter, die für das Profil definiert die <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> Methode. Diese Methode gibt ein <xref:System.Collections.ArrayList> von <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> Objekte, die den vorhandenen Parameter für dieses Profil darstellen.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A> -ändert die Einstellung eines vorhandenen Parameters im Profil, wobei *Namen* ist der Name des Agentparameters und *NewValue* ist der Wert, der die Parameter geändert wird. Rufen Sie zum Auflisten aller aktuellen Agentparameter, die für das Profil definiert die <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> Methode. Diese Methode gibt ein <xref:System.Collections.ArrayList> von <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> Objekte, die den vorhandenen Parameter für dieses Profil darstellen. Zum Aufzählen aller unterstützten Einstellungen für den Agentparameter, rufen Sie die <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> Methode. Diese Methode gibt ein <xref:System.Collections.ArrayList> von <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> Objekte, die die unterstützten Werte für alle Parameter darstellen.  
  
###  <a name="Delete_RMO"></a> So löschen Sie ein Agentprofil  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe einer Instanz von der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.AgentProfile> Klasse. Legen Sie den Namen des Profils für <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> und <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Wenn diese Methode **false**zurückgibt, wurde ein falscher Name angegeben, oder das Profil ist auf dem Server nicht vorhanden.  
  
4.  Überprüfen Sie, ob die <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> Eigenschaftensatz zu <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User>, womit ein Kundenprofil. Entfernen Sie ein Profil mit dem Wert des <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> für <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A>.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A> Methode, um das benutzerdefinierte Profil durch dieses Objekt dargestellt wird, vom Server zu entfernen.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Ändern der Agentparameter  
 Die Änderungen der Agentparameter treten in Kraft, wenn der Agent das nächste Mal gestartet wird. Wenn der Agent ständig ausgeführt wird, müssen Sie den Agent beenden und neu starten.  
  
## Siehe auch  
 [Replikations-Agent-Profile](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replikationsmomentaufnahme-Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [Replikationsprotokolllese-Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replikationsverteilungs-Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replikationsmerge-Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Warteschlangenlese-Agent der Microsoft SQL Server-Replikation](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  