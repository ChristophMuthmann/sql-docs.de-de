---
title: "Erstellen einer Ver&#246;ffentlichung | Microsoft Docs"
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
  - "Veröffentlichungen [SQL Server-Replikation], erstellen"
  - "Artikel [SQL Server-Replikation], definieren"
  - "Hinzufügen von Artikeln"
  - "Artikel [SQL Server-Replikation], hinzufügen"
ms.assetid: 52ee6de9-1d58-4cb9-8711-372bddbe7154
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Erstellen einer Ver&#246;ffentlichung
  In diesem Thema wird beschrieben, wie eine Veröffentlichung in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) erstellt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So erstellen Sie eine Veröffentlichung und definieren Artikel mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Veröffentlichung und Artikelnamen dürfen dürfen keines der folgenden Zeichen: %, \* , [,], |,:, ","? , ' , \ , / , \< , >. Wenn Objekte in der Datenbank eines dieser Zeichen enthalten, und Sie sie replizieren möchten, geben Sie einen Artikelnamen, die sich von den Objektnamen in der **Artikeleigenschaften - \< Artikel>** im Dialogfeld aus der **Artikel** Seite im Assistenten.  
  
###  <a name="Security"></a> Sicherheit  
 Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen speichern müssen, verwenden Sie die [Kryptografiedienste](http://go.microsoft.com/fwlink/?LinkId=34733) von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows .NET Framework.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Mit dem Assistenten für neue Veröffentlichung erstellen Sie Veröffentlichungen und definieren Artikel. Nachdem eine Veröffentlichung erstellt wurde, anzeigen und Ändern von Veröffentlichungseigenschaften in die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Informationen zum Erstellen einer Veröffentlichung aus einer Oracle-Datenbank finden Sie unter [Erstellen einer Veröffentlichung aus einer Oracle-Datenbank](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
#### So erstellen Sie eine Veröffentlichung und definieren Artikel  
  
1.  Stellen Sie in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie die **Replikation** Ordner, und klicken Sie dann mit der rechten Maustaste die **lokale Publikationen** Ordner.  
  
3.  Klicken Sie auf **Neue Veröffentlichung**.  
  
4.  Folgen Sie den Anweisungen auf den Seiten des Assistenten für neue Veröffentlichung, um folgende Vorgänge auszuführen:  
  
    -   Angeben eines Verteilers, falls die Verteilung auf dem Server nicht konfiguriert wurde. Weitere Informationen zum Konfigurieren der Verteilung finden Sie unter [Verleger- und Verteilereigenschaften](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
         Wenn Sie an der **Verteiler** Seite, die der Verleger als sein eigener Verteiler (lokaler Verteiler) fungiert, und der Server ist nicht konfiguriert, als Verteiler, Assistenten für neue Veröffentlichung der Server konfiguriert werden kann. Auf der Seite **Momentaufnahmeordner** geben Sie einen Standardmomentaufnahmeordner für den Verteiler an. Der Momentaufnahmeordner ist lediglich ein von Ihnen freigegebenes Verzeichnis. Agents, die aus diesem Ordner lesen bzw. in den Ordner schreiben, benötigen ausreichende Zugriffsberechtigungen. Weitere Informationen zur Absicherung des Ordners finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
         Wenn Sie angeben, dass ein anderer Server als Verteiler fungieren soll, müssen Sie auf der Seite **Administratorkennwort** ein Kennwort für Verbindungen eingeben, die zwischen dem Verleger und dem Verteiler hergestellt werden. Dieses Kennwort muss mit dem Kennwort übereinstimmen, dass bei der Aktivierung des Verlegers auf dem Remoteverteiler angegeben wurde.  
  
         Weitere Informationen finden Sie unter [Verteilung konfigurieren](../../../relational-databases/replication/configure-distribution.md).  
  
    -   Auswählen einer Veröffentlichungsdatenbank.  
  
    -   Auswählen eines Veröffentlichungstyps. Weitere Informationen finden Sie unter [Replikationstypen](../../../relational-databases/replication/types-of-replication.md).  
  
    -   Angeben von Daten und Datenbankobjekten, die veröffentlicht werden sollen. Optional können Sie Spalten aus Tabellenartikeln filtern und Artikeleigenschaften angeben.  
  
    -   Optionales Filtern von Zeilen aus Tabellenartikeln. Weitere Informationen finden Sie unter [veröffentlichten Filterdaten](../../../relational-databases/replication/publish/filter-published-data.md).  
  
    -   Festlegen des Zeitplans für den Momentaufnahme-Agent.  
  
    -   Angeben der Anmeldeinformationen, unter denen die folgenden Replikations-Agents ausgeführt werden und Verbindungen herstellen:  
  
         \- Snapshot-Agent für alle Veröffentlichungen.  
  
         \- Protokollieren Sie Protokolllese-Agent für alle transaktionsveröffentlichungen.  
  
         \- Warteschlangenlese-Agent für Transaktionspublikationen, die aktualisierbare Abonnements zulassen.  
  
         Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) und [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
    -   Optionale Erstellung eines Skripts für die Veröffentlichung. Weitere Informationen finden Sie unter [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
    -   Angeben eines Namens für die Veröffentlichung.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Veröffentlichungen können programmgesteuert mit gespeicherten Replikationsprozeduren erstellt werden. Welche gespeicherten Prozeduren Sie verwenden, hängt vom Typ der zu erstellenden Veröffentlichung ab.  
  
#### So erstellen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) So aktivieren die Veröffentlichung der aktuellen Datenbank mit der Snapshot- oder Transaktionsreplikation.  
  
2.  Bestimmen Sie bei einer Transaktionsveröffentlichung, ob ein Auftrag des Protokolllese-Agents für die Veröffentlichungsdatenbank existiert. (Dieser Schritt ist für Momentaufnahmeveröffentlichungen nicht erforderlich.)  
  
    -   Wenn bereits ein Auftrag des Protokolllese-Agents für die Veröffentlichungsdatenbank vorhanden ist, fahren Sie mit Schritt 3 fort.  
  
    -   Wenn Sie unsicher sind, ob ein Protokolllese-Agent-Auftrag für eine veröffentlichte Datenbank vorhanden ist, führen Sie [Sp_helplogreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank.  
  
    -   Wenn das Resultset leer ist, erstellen Sie einen Auftrag des Protokolllese-Agents. Führen Sie auf dem Verleger [Sp_addlogreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Geben Sie die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] unter dem der Agent ausgeführt, für die wird Windows-Anmeldeinformationen **@job_name** und **@password**. Wenn der Agent beim Verbinden mit dem Verleger SQL Server-Authentifizierung verwendet, müssen Sie auch angeben, auf den Wert **0** für **@publisher_security_mode** und [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Fahren Sie mit Schritt 3 fort.  
  
3.  Führen Sie auf dem Verleger [Sp_addpublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Geben Sie einen Veröffentlichungsnamen für **@publication**, und für die **@repl_freq** Parameter, geben Sie den Wert **Snapshot** für eine Snapshot- oder Wert **fortlaufende** für eine Transaktionspublikation. Geben Sie eventuell weitere Veröffentlichungsoptionen an. Dadurch wird die Veröffentlichung definiert.  
  
    > [!NOTE]  
    >  Veröffentlichungsnamen dürfen die folgenden Zeichen nicht enthalten:  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
4.  Führen Sie auf dem Verleger [Sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Geben Sie den Namen der Veröffentlichung verwendet, die in Schritt 3 für **@publication** und die Windows-Anmeldeinformationen, unter denen der Snapshot-Agent ausgeführt, für die wird **@snapshot_job_name** und **@password**. Wenn der Agent beim Verbinden mit dem Verleger SQL Server-Authentifizierung verwendet, müssen Sie auch angeben, auf den Wert **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die angegebenen Werte für alle Parameter einschließlich *Job_login* und *Job_password*, werden als nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul & #40; SQL Server-Konfigurations-Manager & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
5.  Fügen Sie der Veröffentlichung Artikel hinzu. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  Starten Sie den Auftrag des Momentaufnahme-Agents, um die Anfangsmomentaufnahme für diese Veröffentlichung zu generieren. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
#### So erstellen Sie eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger [Sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) So aktivieren die Veröffentlichung der aktuellen Datenbank mithilfe der Mergereplikation.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Geben Sie einen Veröffentlichungsnamen für **@publication** und eventuell weitere Veröffentlichungsoptionen an. Dadurch wird die Veröffentlichung definiert.  
  
    > [!NOTE]  
    >  Veröffentlichungsnamen dürfen die folgenden Zeichen nicht enthalten:  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
3.  Führen Sie auf dem Verleger [Sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Geben Sie den in Schritt 2 verwendeten Veröffentlichungsnamen **@publication** und die Windows-Anmeldeinformationen, unter denen der Snapshot-Agent ausgeführt, für die wird **@snapshot_job_name** und **@password**. Wenn der Agent beim Verbinden mit dem Verleger SQL Server-Authentifizierung verwendet, müssen Sie auch angeben, auf den Wert **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die angegebenen Werte für alle Parameter einschließlich *Job_login* und *Job_password*, werden als nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul & #40; SQL Server-Konfigurations-Manager & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
4.  Fügen Sie der Veröffentlichung Artikel hinzu. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
5.  Starten Sie den Auftrag des Momentaufnahme-Agents, um die Anfangsmomentaufnahme für diese Veröffentlichung zu generieren. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel wird eine Transaktionsveröffentlichung erstellt. Anhand von Skriptvariablen werden Windows-Anmeldeinformationen übergeben, die zur Erstellung von Aufträgen für den Momentaufnahme-Agent und den Protokolllese-Agent erforderlich sind.  
  
 [!code-sql[HowTo#sp_AddTranPub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_1.sql)]  
  
 In diesem Beispiel wird eine Mergeveröffentlichung erstellt. Anhand von Skriptvariablen werden Windows-Anmeldeinformationen übergeben, die zur Erstellung des Auftrags für den Momentaufnahme-Agent erforderlich sind.  
  
 [!code-sql[HowTo#sp_AddMergePub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Veröffentlichungen mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert erstellen. Welche RMO-Klassen Sie zum Erstellen von Veröffentlichungen verwenden, hängt vom Typ der zu erstellenden Veröffentlichung ab.  
  
#### So erstellen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz von der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> Klasse für die Veröffentlichungsdatenbank, legen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft, um die Instanz von <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1, und rufen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Wenn <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> gibt **false**, stellen Sie sicher, dass die Datenbank vorhanden ist.  
  
3.  Wenn die <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> Eigenschaft **false**, legen Sie es auf **true**.  
  
4.  Überprüfen Sie den Wert der für eine Transaktionspublikation, die <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentExists%2A> Eigenschaft. Wenn diese Eigenschaft den Wert **true**hat, ist ein Protokolllese-Agentauftrag für diese Datenbank bereits vorhanden. Hat diese Eigenschaft den Wert **false**, gehen Sie wie folgt vor:  
  
    -   Legen Sie die <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> und <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> oder <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> Felder <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> für die Anmeldeinformationen für die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Konto, unter dem der Protokolllese-Agent ausgeführt wird.  
  
        > [!NOTE]  
        >  Festlegen von <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> ist nicht erforderlich, beim Erstellen der Veröffentlichung von einem Mitglied der **Sysadmin** festen Serverrolle. In diesem Fall nimmt der Agent die Identität des SQL Server-Agent-Kontos an. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Optional) Legen Sie die <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> oder <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> Felder <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentPublisherSecurity%2A> beim SQL Server-Authentifizierung mit dem Verleger herstellen.  
  
    -   Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.CreateLogReaderAgent%2A> Methode, um den Protokolllese-Agent-Auftrag für die Datenbank zu erstellen.  
  
5.  Erstellen Sie eine Instanz von der <xref:Microsoft.SqlServer.Replication.TransPublication> Klasse, und legen Sie für dieses Objekt die folgenden Eigenschaften:  
  
    -   Die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Der Name der veröffentlichten Datenbank für <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Einen Namen für die Veröffentlichung für <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   Ein <xref:Microsoft.SqlServer.Replication.PublicationType> entweder <xref:Microsoft.SqlServer.Replication.PublicationType.Transactional> oder <xref:Microsoft.SqlServer.Replication.PublicationType.Snapshot>.  
  
    -   Die <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> und <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> Felder <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> für die Anmeldeinformationen für das Windows-Konto unter dem der Snapshot-Agent ausgeführt wird. Dieses Konto wird auch verwendet, wenn der Momentaufnahme-Agent Verbindungen mit dem lokalen Verteiler herstellt, sowie für alle Remoteverbindungen mithilfe der Windows-Authentifizierung.  
  
        > [!NOTE]  
        >  Festlegen von <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> ist nicht erforderlich, beim Erstellen der Veröffentlichung von einem Mitglied der **Sysadmin** festen Serverrolle. In diesem Fall nimmt der Agent die Identität des SQL Server-Agent-Kontos an. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Optional) Die <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> oder <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> Felder <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentPublisherSecurity%2A> beim SQL Server-Authentifizierung mit dem Verleger herstellen.  
  
    -   (Optional) Verwenden Sie den inklusiven logischen OR-Operator (**|** in Visual c# und **oder** in Visual Basic) und den exklusiven logischen OR-Operator (**^** in Visual c# und **Xor** in Visual Basic) Festlegen der <xref:Microsoft.SqlServer.Replication.PublicationAttributes> Werte für die <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> Eigenschaft.  
  
    -   (Optional) Der Name des Verlegers für <xref:Microsoft.SqlServer.Replication.TransPublication.PublisherName%2A> Wenn der Verleger ein nicht - SQL Server-Verleger ist.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> Methode, um die Veröffentlichung zu erstellen.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die angegebenen Werte für alle Eigenschaften, einschließlich <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, werden als nur-Text an den Verteiler gesendet. Verschlüsseln Sie die Verbindung zwischen dem Verleger und die zugehörigen Remoteverteiler vor dem Aufruf der <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> Methode. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul & #40; SQL Server-Konfigurations-Manager & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
7.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> Methode, um den Snapshot-Agent-Auftrag für die Veröffentlichung zu erstellen.  
  
#### So erstellen Sie eine Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz von der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> Klasse für die Veröffentlichungsdatenbank, legen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft, um die Instanz von <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1, und rufen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Wenn <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> gibt **false**, stellen Sie sicher, dass die Datenbank vorhanden ist.  
  
3.  Wenn <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> Eigenschaft **false**, legen Sie es auf **true**, und rufen Sie <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>.  
  
4.  Erstellen Sie eine Instanz von der <xref:Microsoft.SqlServer.Replication.MergePublication> Klasse, und legen Sie für dieses Objekt die folgenden Eigenschaften:  
  
    -   Die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Der Name der veröffentlichten Datenbank für <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Einen Namen für die Veröffentlichung für <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   Die <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> und <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> Felder <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> für die Anmeldeinformationen für das Windows-Konto unter dem der Snapshot-Agent ausgeführt wird. Dieses Konto wird auch verwendet, wenn der Momentaufnahme-Agent Verbindungen mit dem lokalen Verteiler herstellt, sowie für alle Remoteverbindungen mithilfe der Windows-Authentifizierung.  
  
        > [!NOTE]  
        >  Festlegen von <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> ist nicht erforderlich, beim Erstellen der Veröffentlichung von einem Mitglied der **Sysadmin** festen Serverrolle. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Optional) Verwenden Sie den inklusiven logischen OR-Operator (**|** in Visual c# und **oder** in Visual Basic) und den exklusiven logischen OR-Operator (**^** in Visual c# und **Xor** in Visual Basic) Festlegen der <xref:Microsoft.SqlServer.Replication.PublicationAttributes> Werte für die <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> Eigenschaft.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> Methode, um die Veröffentlichung zu erstellen.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die angegebenen Werte für alle Eigenschaften, einschließlich <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, werden als nur-Text an den Verteiler gesendet. Verschlüsseln Sie die Verbindung zwischen dem Verleger und die zugehörigen Remoteverteiler vor dem Aufruf der <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> Methode. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul & #40; SQL Server-Konfigurations-Manager & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> Methode, um den Snapshot-Agent-Auftrag für die Veröffentlichung zu erstellen.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 In diesem Beispiel wird die AdventureWorks-Datenbank für Transaktionsveröffentlichung aktiviert, ein Protokolllese-Agentauftrag definiert und die AdvWorksProductTran-Veröffentlichung erstellt. Für diese Veröffentlichung muss ein Artikel definiert sein. Die Anmeldeinformationen für das Windows-Konto, die für die Erstellung des Protokolllese- und des Momentaufnahme-Agentauftrags erforderlich sind, werden zur Laufzeit übergeben. Informationen darüber, wie RMO verwendet wird, um Momentaufnahme- und Transaktionsartikel zu definieren, finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
 [!code-csharp[HowTo#rmo_CreateTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpub)]  
  
 In diesem Beispiel wird die AdventureWorks-Datenbank für Mergepublishing aktiviert und die AdvWorksSalesOrdersMerge-Veröffentlichung erstellt. Für diese Veröffentlichung müssen ebenfalls Artikel definiert sein. Die Anmeldeinformationen für das Windows-Konto, die für die Erstellung des Momentaufnahme-Agentauftrags erforderlich sind, werden zur Laufzeit übergeben. Informationen darüber, wie RMO verwendet wird, um Mergeartikel zu definieren, finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
## Siehe auch  
 [Verwenden von sqlcmd mit Skriptvariablen](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Konzepte für Replikationsverwaltungsobjekte (RMO)](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Konfigurieren der Verteilung](../../../relational-databases/replication/configure-distribution.md)   
 [Schützen des Verteilers](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [Sichern des Verlegers](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  