---
title: "Anzeigen und &#196;ndern der Verteiler- und Verlegereigenschaften | Microsoft Docs"
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
  - "Anzeigen von Replikationseigenschaften"
  - "Verteiler [SQL Server-Replikation], ändern"
  - "Ändern von Replikationseigenschaften, Verteiler"
  - "Verteiler [SQL Server-Replikation], Eigenschaften"
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# Anzeigen und &#196;ndern der Verteiler- und Verlegereigenschaften
  In diesem Thema wird beschrieben, wie die Distributor-Eigenschaft und die Publisher-Eigenschaft in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) angezeigt und geändert werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So können Sie Verteiler- und Verlegereigenschaften anzeigen und ändern mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Bei Verlegern, auf denen eine niedrigere Versionen als [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ausgeführt wird, kann ein Benutzer der festen Serverrolle **sysadmin** auf der Seite **Abonnenten** Abonnenten registrieren. Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]müssen Abonnenten für die Replikation nicht mehr explizit registriert werden.  
  
###  <a name="Security"></a> Sicherheit  
 Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So zeigen Sie die Verteilereigenschaften an oder ändern diese  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verteiler her, und erweitern Sie dann den Serverknoten.  
  
2.  Mit der rechten Maustaste die **Replikation** Ordner, und klicken Sie dann auf **Verteilereigenschaften**.  
  
3.  Anzeigen und ändern Sie die Eigenschaften der **Verteilereigenschaften - \< Verteiler>** (Dialogfeld).  
  
    -   Zum Anzeigen und Ändern der Eigenschaften einer Verteilungsdatenbank, klicken Sie auf die Eigenschaftenschaltfläche (**...**) für die Datenbank auf die **Allgemeine** Thedialog im auf der Seite.  
  
    -   Um und ändern mit dem Verteiler verknüpfte Verlegereigenschaften anzuzeigen, klicken Sie auf die Eigenschaftenschaltfläche (**...**) für den Verleger auf den **Herausgeber** Seite des Dialogfelds.  
  
    -   Klicken Sie auf der Seite **Allgemein** des Dialogfelds auf **Profilstandards** , um auf die Profile der Replikations-Agents zuzugreifen. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
    -   Um das Kennwort des zum Ausführen von administrativen gespeicherten Prozeduren auf dem Verleger und Aktualisieren von Informationen auf dem Verteiler verwendeten Kontos zu ändern, geben Sie auf der Seite **Verleger** des Dialogfelds in den Feldern **Kennwort** und **Kennwort bestätigen** ein neues Kennwort ein. Weitere Informationen finden Sie unter [Schützen des Verteilers](../../relational-databases/replication/security/secure-the-distributor.md).  
  
4.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
#### So zeigen Sie die Verlegereigenschaften an oder ändern diese  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Mit der rechten Maustaste die **Replikation** Ordner, und klicken Sie dann auf **Verlegereigenschaften**.  
  
3.  Anzeigen und ändern Sie die Eigenschaften der **Verlegereigenschaften - \< Publisher >** Dialogfeld.  
  
    -   Ein Benutzer der festen Serverrolle **sysadmin** kann Datenbanken für die Replikation auf der Seite **Veröffentlichungsdatenbanken** aktivieren. Aktivieren einer Datenbank werden die Datenbank nicht veröffentlicht werden; Vielmehr ermöglicht dies allen Benutzern in der **Db_owner** festen Datenbankrolle für diese Datenbank eine oder mehrere Veröffentlichungen in der Datenbank zu erstellen.  
  
4.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Die Verleger- und Verteilereigenschaften können mit gespeicherten Replikationsprozeduren programmgesteuert angezeigt werden.  
  
#### So zeigen Sie Verleger- und Verteilerdatenbankeigenschaften an  
  
1.  Führen Sie [Sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md) Informationen über Verteiler, Verteilungsdatenbank und Arbeitsverzeichnis zurückzugeben.  
  
2.  Führen Sie [Sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) um Eigenschaften einer angegebenen Verteilungsdatenbank zurückzugeben.  
  
#### So ändern Sie Verleger- und Verteilerdatenbankeigenschaften  
  
1.  Führen Sie auf dem Verteiler [Sp_changedistributor_property](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md) Verteilereigenschaften ändern.  
  
2.  Führen Sie auf dem Verteiler [Sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md) So ändern Sie die Eigenschaften der Verteilungsdatenbank.  
  
3.  Führen Sie auf dem Verteiler [Sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) So ändern Sie das Kennwort für den Verteiler.  
  
    > [!IMPORTANT]  
    >  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen in einer Skriptdatei speichern müssen, sollten Sie die Datei schützen, um nicht autorisierten Zugriff zu verhindern.  
  
4.  Führen Sie auf dem Verteiler [Sp_changedistpublisher](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) zum Ändern der Eigenschaften eines Verlegers mit dem Verteiler.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Das folgende Beispielskript [!INCLUDE[tsql](../../includes/tsql-md.md)] gibt Informationen über den Verteiler und die Verteilerdatenbank zurück.  
  
 [!code-sql[HowTo#sp_helpdistributor](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_1.sql)]  
  
 [!code-sql[HowTo#sp_helpdistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_2.sql)]  
  
 Im folgenden Beispiel werden die Beibehaltungsdauer für den Verteiler, das Kennwort für den Verbindungsaufbau zum Verteiler und das Intervall geändert, in dem der Verteiler den Status verschiedener Replikations-Agents überprüft (auch Taktintervall genannt).  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen in einer Skriptdatei speichern müssen, sollten Sie die Datei schützen, um nicht autorisierten Zugriff zu verhindern.  
  
 [!code-sql[HowTo#sp_changedistributor_property](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_3.sql)]  
  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_4.sql)]  
  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_5.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
  
#### So zeigen Sie die Verteilereigenschaften an oder ändern diese  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer> Klasse. Übergeben Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Objekt aus Schritt 1.  
  
3.  (Optional) Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A> Eigenschaft zu überprüfen, ob die derzeit verbundene Server ein Verteiler ist.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> Methode, um die Eigenschaften vom Server abzurufen.  
  
5.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eine oder mehrere der Verteilereigenschaften fest, die festgelegt werden können die <xref:Microsoft.SqlServer.Replication.ReplicationServer> Objekt.  
  
6.  (Optional) Wenn die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> Eigenschaft auf die <xref:Microsoft.SqlServer.Replication.ReplicationServer> -Objekts festgelegt, um **true**, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode, um die Änderungen an den Server übertragen.  
  
#### So zeigen Sie Verteilerdatenbankeigenschaften an oder ändern Sie diese Eigenschaften  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.DistributionDatabase> Klasse. Geben Sie die Namenseigenschaft, und übergeben Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Objekt aus Schritt 1.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode, um die Eigenschaften vom Server abzurufen. Wenn diese Methode **false**zurückgibt, ist die Datenbank mit dem angegebenen Namen nicht auf dem Server vorhanden.  
  
4.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eines der <xref:Microsoft.SqlServer.Replication.DistributionDatabase> Eigenschaften festgelegt werden können.  
  
5.  (Optional) Wenn die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> Eigenschaft auf die <xref:Microsoft.SqlServer.Replication.DistributionDatabase> -Objekts festgelegt, um **true**, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode, um die Änderungen an den Server übertragen.  
  
#### So zeigen Sie die Verlegereigenschaften an oder ändern diese  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.DistributionPublisher> Klasse. Geben Sie den <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> -Eigenschaft, und übergeben der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Objekt aus Schritt 1.  
  
3.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eines der <xref:Microsoft.SqlServer.Replication.DistributionPublisher> Eigenschaften festgelegt werden können.  
  
4.  (Optional) Wenn die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> Eigenschaft auf die <xref:Microsoft.SqlServer.Replication.DistributionPublisher> -Objekts festgelegt, um **true**, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> Methode, um die Änderungen an den Server übertragen.  
  
#### So ändern Sie das Kennwort für die Verwaltungsverbindung zwischen dem Verleger und dem Verteiler  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer> Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die in Schritt 1 erstellte Verbindung.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> Methode zum Abrufen der Eigenschaften des Objekts.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> Methode. Übergeben Sie den neuen Kennwortwert für den *password* -Parameter.  
  
    > [!IMPORTANT]  
    >  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen speichern müssen, verwenden Sie die [Kryptografiedienste](http://go.microsoft.com/fwlink/?LinkId=34733) von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
6.  (Optional) Führen Sie die folgenden Schritte aus, um das Kennwort bei jedem Remoteverleger zu ändern, der diesen Verteiler verwendet:  
  
    1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
    2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer> Klasse.  
  
    3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft, um die in Schritt 6a erstellte Verbindung.  
  
    4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> Methode zum Abrufen der Eigenschaften des Objekts.  
  
    5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> Methode. Übergeben Sie den neuen Kennwortwert aus Schritt 5 für den *password* -Parameter.  
  
###  <a name="PShellExample"></a> Beispiel (RMO)  
 In diesem Beispiel wird gezeigt, wie Verteilungs- und Verteilungsdatenbankeigenschaften geändert werden.  
  
> [!IMPORTANT]  
>  Um die Speicherung von Anmeldeinformationen im Code vermeiden, wird das neue Verteilerkennwort zur Laufzeit angegeben.  
  
 [!code-csharp[HowTo#rmo_ChangeDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## Siehe auch  
 [Konzepte für Replikationsverwaltungsobjekte (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Deaktivieren der Veröffentlichung und Verteilung](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md)   
 [Konzepte für Replikationsverwaltungsobjekte (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Informationsskript für Verleger und Verteiler](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für einen Verleger & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
  
  