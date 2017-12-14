---
title: "Erstellen einer Veröffentlichung | Microsoft-Dokumentation"
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
helpviewer_keywords:
- publications [SQL Server replication], creating
- articles [SQL Server replication], defining
- adding articles
- articles [SQL Server replication], adding
ms.assetid: 52ee6de9-1d58-4cb9-8711-372bddbe7154
caps.latest.revision: "44"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f0791f563a019b3d9a6f945f63712b4397ad8df0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-publication"></a>Erstellen einer Veröffentlichung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie eine Veröffentlichung in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (Replication Management Objects, RMO) erstellt wird.  
  
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
  
-   Veröffentlichungs- und Artikelnamen dürfen folgende Zeichen nicht enthalten: % , \* , [ , ] , | , : , " , ? , ' , \ , / , < , >. Wenn Objekte in der Datenbank eines dieser Zeichen enthalten, und Sie die Objekte replizieren möchten, müssen Sie einen Artikelnamen angeben, der sich von dem Objektnamen im Dialogfeld **Artikeleigenschaften - \<Article>** unterscheidet. Dieses Dialogfeld ist im Assistenten auf der Seite **Artikel** verfügbar.  
  
###  <a name="Security"></a> Sicherheit  
 Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen speichern müssen, verwenden Sie die [Kryptografiedienste](http://go.microsoft.com/fwlink/?LinkId=34733) von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows .NET Framework.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Mit dem Assistenten für neue Veröffentlichung erstellen Sie Veröffentlichungen und definieren Artikel. Rufen Sie nach der Erstellung einer Veröffentlichung das Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>** auf, um die Eigenschaften anzuzeigen und zu ändern. Weitere Informationen zum Erstellen von Veröffentlichungen aus einer Oracle-Datenbank finden Sie unter [Erstellen einer Veröffentlichung aus einer Oracle-Datenbank](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
#### <a name="to-create-a-publication-and-define-articles"></a>So erstellen Sie eine Veröffentlichung und definieren Artikel  
  
1.  Stellen Sie in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und klicken Sie dann mit der rechten Maustaste auf den Ordner **Lokale Veröffentlichungen** .  
  
3.  Klicken Sie auf **Neue Veröffentlichung**.  
  
4.  Folgen Sie den Anweisungen auf den Seiten des Assistenten für neue Veröffentlichung, um folgende Vorgänge auszuführen:  
  
    -   Angeben eines Verteilers, falls die Verteilung auf dem Server nicht konfiguriert wurde. Weitere Informationen zum Konfigurieren der Verteilung finden Sie unter [Konfigurieren der Veröffentlichung und der Verteilung](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
         Wenn Sie auf der Seite **Verteiler** angeben, dass der Verleger als eigener Verteiler fungiert (lokaler Verteiler) und der Server nicht als Verteiler konfiguriert ist, erfolgt die Konfiguration des Servers durch den Assistenten für neue Veröffentlichung. Auf der Seite **Momentaufnahmeordner** geben Sie einen Standardmomentaufnahmeordner für den Verteiler an. Der Momentaufnahmeordner ist lediglich ein von Ihnen freigegebenes Verzeichnis. Agents, die aus diesem Ordner lesen bzw. in den Ordner schreiben, benötigen ausreichende Zugriffsberechtigungen. Weitere Informationen zum angemessenen Sichern des Ordners finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
         Wenn Sie angeben, dass ein anderer Server als Verteiler fungieren soll, müssen Sie auf der Seite **Administratorkennwort** ein Kennwort für Verbindungen eingeben, die zwischen dem Verleger und dem Verteiler hergestellt werden. Dieses Kennwort muss mit dem Kennwort übereinstimmen, dass bei der Aktivierung des Verlegers auf dem Remoteverteiler angegeben wurde.  
  
         Weitere Informationen finden Sie unter [Configure Distribution](../../../relational-databases/replication/configure-distribution.md).  
  
    -   Auswählen einer Veröffentlichungsdatenbank.  
  
    -   Auswählen eines Veröffentlichungstyps. Weitere Informationen finden Sie unter [Replikationstypen](../../../relational-databases/replication/types-of-replication.md).  
  
    -   Angeben von Daten und Datenbankobjekten, die veröffentlicht werden sollen. Optional können Sie Spalten aus Tabellenartikeln filtern und Artikeleigenschaften angeben.  
  
    -   Optionales Filtern von Zeilen aus Tabellenartikeln. Weitere Informationen finden Sie unter [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md).  
  
    -   Festlegen des Zeitplans für den Momentaufnahme-Agent.  
  
    -   Angeben der Anmeldeinformationen, unter denen die folgenden Replikations-Agents ausgeführt werden und Verbindungen herstellen:  
  
         \- Momentaufnahme-Agent (für alle Veröffentlichungen)  
  
         \- Protokolllese-Agent (für alle Transaktionsveröffentlichungen)  
  
         \- Warteschlangenlese-Agent für Transaktionsveröffentlichungen, in denen Updates von Abonnements zulässig sind  
  
         Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) und [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
    -   Optionale Erstellung eines Skripts für die Veröffentlichung. Weitere Informationen finden Sie unter [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
    -   Angeben eines Namens für die Veröffentlichung.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Veröffentlichungen können programmgesteuert mit gespeicherten Replikationsprozeduren erstellt werden. Welche gespeicherten Prozeduren Sie verwenden, hängt vom Typ der zu erstellenden Veröffentlichung ab.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication"></a>So erstellen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) aus, um die Veröffentlichung der aktuellen Datenbank mit der Momentaufnahme- oder der Transaktionsreplikation zu aktivieren.  
  
2.  Bestimmen Sie bei einer Transaktionsveröffentlichung, ob ein Auftrag des Protokolllese-Agents für die Veröffentlichungsdatenbank existiert. (Dieser Schritt ist für Momentaufnahmeveröffentlichungen nicht erforderlich.)  
  
    -   Wenn bereits ein Auftrag des Protokolllese-Agents für die Veröffentlichungsdatenbank vorhanden ist, fahren Sie mit Schritt 3 fort.  
  
    -   Wenn Sie sich nicht sicher sind, ob ein Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank vorhanden ist, dann führen Sie [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus.  
  
    -   Wenn das Resultset leer ist, erstellen Sie einen Auftrag des Protokolllese-Agents. Führen Sie auf dem Verleger [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) aus. Geben Sie die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] -Anmeldeinformationen, unter denen der Agent ausgeführt wird, für **@job_name** und **@password**aktiviert wird. Wenn der Agent zum Herstellen der Verbindung mit dem Verleger die SQL Server-Authentifizierung verwendet, müssen Sie zudem den Wert **0** für **@publisher_security_mode** und die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Fahren Sie mit Schritt 3 fort.  
  
3.  Führen Sie auf dem Verleger [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) aus. Geben Sie einen Veröffentlichungsnamen für **@publication**und für den **@repl_freq** -Parameter den Wert **snapshot** (bei einer Momentaufnahmeveröffentlichung) oder den Wert **continuous** (bei einer Transaktionsveröffentlichung) an. Geben Sie eventuell weitere Veröffentlichungsoptionen an. Dadurch wird die Veröffentlichung definiert.  
  
    > [!NOTE]  
    >  Veröffentlichungsnamen dürfen die folgenden Zeichen nicht enthalten:  
    >   
    >  % * [ ] | : " ? \ / < >  
  
4.  Führen Sie auf dem Verleger [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) aus. Geben Sie den in Schritt 3 für **@publication** verwendeten Veröffentlichungsnamen und die Windows-Anmeldeinformationen, unter denen der Momentaufnahme-Agent ausgeführt wird, für **@snapshot_job_name** und **@password**aktiviert wird. Wenn der Agent zum Herstellen der Verbindung mit dem Verleger die SQL Server-Authentifizierung verwendet, müssen Sie zudem den Wert **0** für **@publisher_security_mode** und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für **@publisher_login** und **@publisher_password**aktiviert wird. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Parameter, einschließlich *job_login* und *job_password*, bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
5.  Fügen Sie der Veröffentlichung Artikel hinzu. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  Starten Sie den Auftrag des Momentaufnahme-Agents, um die Anfangsmomentaufnahme für diese Veröffentlichung zu generieren. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
#### <a name="to-create-a-merge-publication"></a>So erstellen Sie eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) aus, um die Veröffentlichung der aktuellen Datenbank mit der Mergereplikation zu aktivieren.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) aus. Geben Sie einen Veröffentlichungsnamen für **@publication** und eventuell weitere Veröffentlichungsoptionen an. Dadurch wird die Veröffentlichung definiert.  
  
    > [!NOTE]  
    >  Veröffentlichungsnamen dürfen die folgenden Zeichen nicht enthalten:  
    >   
    >  % * [ ] | : " ? \ / < >  
  
3.  Führen Sie auf dem Verleger [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) aus. Geben Sie den in Schritt 2 für **@publication** verwendeten Veröffentlichungsnamen und die Windows-Anmeldeinformationen, unter denen der Momentaufnahme-Agent ausgeführt wird, für **@snapshot_job_name** und **@password**aktiviert wird. Wenn der Agent zum Herstellen der Verbindung mit dem Verleger die SQL Server-Authentifizierung verwendet, müssen Sie zudem den Wert **0** für **@publisher_security_mode** und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für **@publisher_login** und **@publisher_password**aktiviert wird. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Parameter, einschließlich *job_login* und *job_password*, bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
4.  Fügen Sie der Veröffentlichung Artikel hinzu. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
5.  Starten Sie den Auftrag des Momentaufnahme-Agents, um die Anfangsmomentaufnahme für diese Veröffentlichung zu generieren. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel wird eine Transaktionsveröffentlichung erstellt. Anhand von Skriptvariablen werden Windows-Anmeldeinformationen übergeben, die zur Erstellung von Aufträgen für den Momentaufnahme-Agent und den Protokolllese-Agent erforderlich sind.  
  
 [!code-sql[HowTo#sp_AddTranPub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_1.sql)]  
  
 In diesem Beispiel wird eine Mergeveröffentlichung erstellt. Anhand von Skriptvariablen werden Windows-Anmeldeinformationen übergeben, die zur Erstellung des Auftrags für den Momentaufnahme-Agent erforderlich sind.  
  
 [!code-sql[HowTo#sp_AddMergePub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Veröffentlichungen mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert erstellen. Welche RMO-Klassen Sie zum Erstellen von Veröffentlichungen verwenden, hängt vom Typ der zu erstellenden Veröffentlichung ab.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication"></a>So erstellen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> -Klasse für die Veröffentlichungsdatenbank, legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die Instanz von <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 fest, und rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf. Wenn <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> den Wert **false**zurückgibt, vergewissern Sie sich, dass die Datenbank vorhanden ist.  
  
3.  Hat die <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> -Eigenschaft den Wert **false**, dann legen Sie ihren Wert auf **true**.  
  
4.  Überprüfen Sie für eine Transaktionsveröffentlichung den Wert der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentExists%2A> -Eigenschaft. Wenn diese Eigenschaft den Wert **true**hat, ist ein Protokolllese-Agentauftrag für diese Datenbank bereits vorhanden. Hat diese Eigenschaft den Wert **false**, gehen Sie wie folgt vor:  
  
    -   Legen Sie die Felder <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> und <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> von <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> fest, um die Anmeldeinformationen für das [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Konto bereitzustellen, unter dem der Protokolllese-Agent auf dem Abonnenten ausgeführt wird.  
  
        > [!NOTE]  
        >  Wenn die Veröffentlichung von einem Mitglied der festen Serverrolle <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> erstellt wird, müssen Sie **P:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity** nicht festlegen. In diesem Fall nimmt der Agent die Identität des SQL Server-Agent-Kontos an. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Optional) Legen Sie die Felder <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> oder <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> von <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentPublisherSecurity%2A> fest, wenn Sie die SQL Server-Authentifizierung zum Herstellen einer Verbindung mit dem Verleger verwenden.  
  
    -   Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.CreateLogReaderAgent%2A> -Methode auf, um den Protokolllese-Agentauftrag für die Datenbank zu erstellen.  
  
5.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPublication> -Klasse, und legen Sie die folgenden Eigenschaften für dieses Objekt fest:  
  
    -   Die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Den Namen der veröffentlichten Datenbank für <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Einen Namen für die Veröffentlichung für <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   Einen <xref:Microsoft.SqlServer.Replication.PublicationType> , entweder <xref:Microsoft.SqlServer.Replication.PublicationType.Transactional> oder <xref:Microsoft.SqlServer.Replication.PublicationType.Snapshot>.  
  
    -   Die Felder <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> und <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> von <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> , um die Anmeldeinformationen für das Windows-Konto bereitzustellen, unter dem der Momentaufnahme-Agent ausgeführt wird. Dieses Konto wird auch verwendet, wenn der Momentaufnahme-Agent Verbindungen mit dem lokalen Verteiler herstellt, sowie für alle Remoteverbindungen mithilfe der Windows-Authentifizierung.  
  
        > [!NOTE]  
        >  Wenn die Veröffentlichung von einem Mitglied der festen Serverrolle <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> erstellt wird, müssen Sie **P:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity** nicht festlegen. In diesem Fall nimmt der Agent die Identität des SQL Server-Agent-Kontos an. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Optional) Legen Sie die Felder <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> oder <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> von <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentPublisherSecurity%2A> fest, wenn Sie die SQL Server-Authentifizierung zum Herstellen einer Verbindung mit dem Verleger verwenden.  
  
    -   (Optional) Verwenden Sie den inklusiven logischen OR-Operator (**|** in Visual C# und **Or** in Visual Basic) und den exklusiven logischen OR-Operator (**^** in Visual C# und **Xor** in Visual Basic), um die <xref:Microsoft.SqlServer.Replication.PublicationAttributes> -Werte für die <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> -Eigenschaft.  
  
    -   (Optional) Den Namen des Verlegers für <xref:Microsoft.SqlServer.Replication.TransPublication.PublisherName%2A> , wenn der Verleger ein Nicht-SQL Server-Verleger ist.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> -Methode auf, um die Veröffentlichung zu erstellen.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Eigenschaften einschließlich <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie die <xref:Microsoft.SqlServer.Replication.Publication.Create%2A>-Methode aufrufen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
7.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A>-Methode auf, um den Momentaufnahme-Agentauftrag für die Veröffentlichung zu erstellen.  
  
#### <a name="to-create-a-merge-publication"></a>So erstellen Sie eine Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> -Klasse für die Veröffentlichungsdatenbank, legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die Instanz von <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 fest, und rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf. Wenn <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> den Wert **false**zurückgibt, vergewissern Sie sich, dass die Datenbank vorhanden ist.  
  
3.  Wenn <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> Property is **false**, dann legen Sie ihren Wert auf **true**fest, und rufen Sie <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>.  
  
4.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication> -Klasse, und legen Sie die folgenden Eigenschaften für dieses Objekt fest:  
  
    -   Die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Den Namen der veröffentlichten Datenbank für <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Einen Namen für die Veröffentlichung für <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   Die Felder <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> und <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> von <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> , um die Anmeldeinformationen für das Windows-Konto bereitzustellen, unter dem der Momentaufnahme-Agent ausgeführt wird. Dieses Konto wird auch verwendet, wenn der Momentaufnahme-Agent Verbindungen mit dem lokalen Verteiler herstellt, sowie für alle Remoteverbindungen mithilfe der Windows-Authentifizierung.  
  
        > [!NOTE]  
        >  Wenn die Veröffentlichung von einem Mitglied der festen Serverrolle <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> erstellt wird, müssen Sie **P:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity** nicht festlegen. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Optional) Verwenden Sie den inklusiven logischen OR-Operator (**|** in Visual C# und **Or** in Visual Basic) und den exklusiven logischen OR-Operator (**^** in Visual C# und **Xor** in Visual Basic), um die <xref:Microsoft.SqlServer.Replication.PublicationAttributes> -Werte für die <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> -Eigenschaft.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> -Methode auf, um die Veröffentlichung zu erstellen.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Eigenschaften einschließlich <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie die <xref:Microsoft.SqlServer.Replication.Publication.Create%2A>-Methode aufrufen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A>-Methode auf, um den Momentaufnahme-Agentauftrag für die Veröffentlichung zu erstellen.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 In diesem Beispiel wird die AdventureWorks-Datenbank für Transaktionsveröffentlichung aktiviert, ein Protokolllese-Agentauftrag definiert und die AdvWorksProductTran-Veröffentlichung erstellt. Für diese Veröffentlichung muss ein Artikel definiert sein. Die Anmeldeinformationen für das Windows-Konto, die für die Erstellung des Protokolllese- und des Momentaufnahme-Agentauftrags erforderlich sind, werden zur Laufzeit übergeben. Informationen darüber, wie RMO verwendet wird, um Momentaufnahme- und Transaktionsartikel zu definieren, finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
 [!code-cs[HowTo#rmo_CreateTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpub)]  
  
 In diesem Beispiel wird die AdventureWorks-Datenbank für Mergepublishing aktiviert und die AdvWorksSalesOrdersMerge-Veröffentlichung erstellt. Für diese Veröffentlichung müssen ebenfalls Artikel definiert sein. Die Anmeldeinformationen für das Windows-Konto, die für die Erstellung des Momentaufnahme-Agentauftrags erforderlich sind, werden zur Laufzeit übergeben. Informationen darüber, wie RMO verwendet wird, um Mergeartikel zu definieren, finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
 [!code-cs[HowTo#rmo_CreateMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von „sqlcmd“ mit Skriptvariablen](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replication Management Objects Concepts](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Verteilung konfigurieren](../../../relational-databases/replication/configure-distribution.md)   
 [Schützen des Verteilers](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [Sichern des Verlegers](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  
