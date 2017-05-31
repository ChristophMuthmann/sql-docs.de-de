---
title: "Anzeigen und Ändern der Verteiler- und Verlegereigenschaften | Microsoft-Dokumentation"
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
- viewing replication properties
- Distributors [SQL Server replication], modifying
- modifying replication properties, Distributors
- Distributors [SQL Server replication], properties
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b0c9adb0d7fa110c08f280706d17706f4af07b07
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="view-and-modify-distributor-and-publisher-properties"></a>Anzeigen und Ändern der Verteiler- und Verlegereigenschaften
  In diesem Thema wird beschrieben, wie die Distributor-Eigenschaft und die Publisher-Eigenschaft in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekten (RMO) angezeigt und geändert werden.  
  
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
  
#### <a name="to-view-and-modify-distributor-properties"></a>So zeigen Sie die Verteilereigenschaften an oder ändern diese  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verteiler her, und erweitern Sie dann den Serverknoten.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Replikation** , und klicken Sie dann auf **Verteilereigenschaften**.  
  
3.  Sie können die Eigenschaften im Dialogfeld **Verteilereigenschaften – \<Verteiler>** anzeigen und ändern.  
  
    -   Um die Eigenschaften einer Verteilungsdatenbank anzuzeigen und zu ändern, klicken Sie auf die Schaltfläche Eigenschaften (**...**) für die Datenbank auf der Seite **Allgemein** des Dialogfelds.  
  
    -   Um die mit dem Verteiler verbundenen Verlegereigenschaften anzuzeigen und zu ändern, klicken Sie auf der Seite**Verleger**des Dialogfelds auf die Schaltfläche Eigenschaften ( **...** ) des Verlegers.  
  
    -   Klicken Sie auf der Seite **Allgemein** des Dialogfelds auf **Profilstandards** , um auf die Profile der Replikations-Agents zuzugreifen. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
    -   Um das Kennwort des zum Ausführen von administrativen gespeicherten Prozeduren auf dem Verleger und Aktualisieren von Informationen auf dem Verteiler verwendeten Kontos zu ändern, geben Sie auf der Seite **Verleger** des Dialogfelds in den Feldern **Kennwort** und **Kennwort bestätigen** ein neues Kennwort ein. Weitere Informationen finden Sie unter [Schützen des Verteilers](../../relational-databases/replication/security/secure-the-distributor.md).  
  
4.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
#### <a name="to-view-and-modify-publisher-properties"></a>So zeigen Sie die Verlegereigenschaften an oder ändern diese  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Replikation** , und klicken Sie dann auf **Verlegereigenschaften**.  
  
3.  Sie können die Eigenschaften im Dialogfeld **Verlegereigenschaften - < Verleger >** anzeigen und ändern.  
  
    -   Ein Benutzer der festen Serverrolle **sysadmin** kann Datenbanken für die Replikation auf der Seite **Veröffentlichungsdatenbanken** aktivieren. Durch das Aktivieren wird eine Datenbank nicht veröffentlicht, sondern Benutzer der festen Datenbankrolle **db_owner** für diese Datenbank können dann eine oder mehrere Veröffentlichungen in der Datenbank erstellen.  
  
4.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Die Verleger- und Verteilereigenschaften können mit gespeicherten Replikationsprozeduren programmgesteuert angezeigt werden.  
  
#### <a name="to-view-distributor-and-distribution-database-properties"></a>So zeigen Sie Verleger- und Verteilerdatenbankeigenschaften an  
  
1.  Führen Sie [sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md) aus, um Informationen über Verteiler, Verteilungsdatenbank und Arbeitsverzeichnis zurückzugeben.  
  
2.  Führen Sie [sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) aus, um die Eigenschaften einer angegebenen Verteilungsdatenbank zurückzugeben.  
  
#### <a name="to-change-distributor-and-distribution-database-properties"></a>So ändern Sie Verleger- und Verteilerdatenbankeigenschaften  
  
1.  Führen Sie auf dem Verteiler [sp_changedistributor_property](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md) aus, um Verteilereigenschaften zu ändern.  
  
2.  Führen Sie auf dem Verteiler [sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md) aus, um Eigenschaften der Verteilerdatenbank zu ändern.  
  
3.  Führen Sie auf dem Verteiler [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) aus, um das Verteilerkennwort zu ändern.  
  
    > [!IMPORTANT]  
    >  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen in einer Skriptdatei speichern müssen, sollten Sie die Datei schützen, um nicht autorisierten Zugriff zu verhindern.  
  
4.  Führen Sie auf dem Verteiler [sp_changedistpublisher](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) aus, um mit dem Verteiler die Eigenschaften eines Verlegers zu ändern.  
  
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
  
#### <a name="to-view-and-modify-distributor-properties"></a>So zeigen Sie die Verteilereigenschaften an oder ändern diese  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.Sqlserver.Management.Common.Serverconnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer>-Klasse. Übergeben Sie <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt aus Schritt 1.  
  
3.  (Optional) überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A>-Eigenschaft, um sich davon zu überzeugen, dass der aktuell verbundene Server ein Verteiler ist.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A>-Methode auf, um die Eigenschaften vom Server abzurufen.  
  
5.  (Optional) Zum Ändern der Eigenschaften legen Sie einen neuen Wert für eine oder mehrere der Verteilereigenschaften fest, die im <xref:Microsoft.SqlServer.Replication.ReplicationServer>-Objekt festgelegt werden können.  
  
6.  (Optional) Wenn die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>-Eigenschaft des <xref:Microsoft.SqlServer.Replication.ReplicationServer>-Objekts auf **true** festgelegt ist, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>-Methode auf, um die Änderungen an den Server zu übertragen.  
  
#### <a name="to-view-and-modify-distribution-database-properties"></a>So zeigen Sie Verteilerdatenbankeigenschaften an oder ändern Sie diese Eigenschaften  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.Sqlserver.Management.Common.Serverconnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.DistributionDatabase>-Klasse. Geben Sie die Namenseigenschaft an, und übergeben Sie das <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt aus Schritt 1.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die Eigenschaften vom Server abzurufen. Wenn diese Methode **false**zurückgibt, ist die Datenbank mit dem angegebenen Namen nicht auf dem Server vorhanden.  
  
4.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eine der definierbaren <xref:Microsoft.SqlServer.Replication.DistributionDatabase>-Eigenschaften fest.  
  
5.  (Optional) Wenn die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>-Eigenschaft des <xref:Microsoft.SqlServer.Replication.ReplicationServer>-Objekts auf **true** festgelegt ist, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>-Methode auf, um die Änderungen an den Server zu übertragen.  
  
#### <a name="to-view-and-modify-publisher-properties"></a>So zeigen Sie die Verlegereigenschaften an oder ändern diese  
  
1.  Stellen Sie eine Verbindung mit dem Verleger her, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.DistributionPublisher>-Klasse. Geben Sie die <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A>-Eigenschaft an, und übergeben Sie das <xref:Microsoft.Sqlserver.Management.Common.ServerConnection>-Objekt aus Schritt 1.  
  
3.  (Optional) Um Eigenschaften zu ändern, legen Sie einen neuen Wert für eine der definierbaren <xref:Microsoft.SqlServer.Replication.DistributionPublisher>-Eigenschaften fest.  
  
4.  (Optional) Wenn die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>-Eigenschaft auf dem <xref:Microsoft.SqlServer.Replication.DistributionPublisher>-Objekt auf **true** festgelegt ist, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>-Methode auf, um die Änderungen an den Server übertragen.  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>So ändern Sie das Kennwort für die Verwaltungsverbindung zwischen dem Verleger und dem Verteiler  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler, indem Sie die <xref:Microsoft.Sqlserver.Management.Common.Serverconnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer>-Klasse.  
  
3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf die in Schritt 1 erstellte Verbindung fest.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A>-Methode auf. Übergeben Sie den neuen Kennwortwert für den *password* -Parameter.  
  
    > [!IMPORTANT]  
    >  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen speichern müssen, verwenden Sie die [Kryptografiedienste](http://go.microsoft.com/fwlink/?LinkId=34733) von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
6.  (Optional) Führen Sie die folgenden Schritte aus, um das Kennwort bei jedem Remoteverleger zu ändern, der diesen Verteiler verwendet:  
  
    1.  Stellen Sie eine Verbindung mit dem Verleger her, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
    2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer>-Klasse.  
  
    3.  Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf die in Schritt 6A erstellte Verbindung fest.  
  
    4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A>-Methode auf, um die Eigenschaften des Objekts abzurufen.  
  
    5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A>-Methode auf. Übergeben Sie den neuen Kennwortwert aus Schritt 5 für den *password* -Parameter.  
  
###  <a name="PShellExample"></a> Beispiel (RMO)  
 In diesem Beispiel wird gezeigt, wie Verteilungs- und Verteilungsdatenbankeigenschaften geändert werden.  
  
> [!IMPORTANT]  
>  Um die Speicherung von Anmeldeinformationen im Code vermeiden, wird das neue Verteilerkennwort zur Laufzeit angegeben.  
  
 [!code-cs[HowTo #rmo_ChangeDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo #rmo_ChangeDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## <a name="see-also"></a>Siehe auch  
 [Konzepte für Replikationsverwaltungsobjekte (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Deaktivieren der Veröffentlichung und Verteilung](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Verteilung konfigurieren](../../relational-databases/replication/configure-distribution.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Informationsskript für Verleger und Verteiler](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für einen Verleger &#40;Replikationsmonitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
  
  

