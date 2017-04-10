---
title: "Deaktivieren der Ver&#246;ffentlichung und Verteilung | Microsoft Docs"
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
  - "Deaktivieren der Veröffentlichung"
  - "Veröffentlichen [SQL Server-Replikation], deaktivieren"
  - "Verteilungsdeaktivierung [SQL Server-Replikation]"
  - "Entfernen der Replikation"
  - "Replikation [SQL Server], entfernen"
  - "Deaktivieren der Replikation"
  - "Deaktivieren der Verteilung"
ms.assetid: 6d4a1474-4d13-4826-8be2-80050fafa8a5
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Deaktivieren der Ver&#246;ffentlichung und Verteilung
  In diesem Thema wird beschrieben, wie die Veröffentlichung und die Verteilung in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) deaktiviert werden.  
  
 Sie können folgendermaßen vorgehen:  
  
-   Löschen aller Verteilungsdatenbanken auf dem Verteiler.  
  
-   Deaktivieren aller Verleger, die den Verteiler verwenden, und Löschen aller Veröffentlichungen auf diesen Verlegern.  
  
-   Löschen aller Abonnements für die Veröffentlichungen. Daten in den Veröffentlichungs- und Abonnementdatenbanken werden nicht gelöscht. Allerdings geht die Synchronisierungsbeziehung zu allen Veröffentlichungsdatenbanken verloren. Falls Sie die Daten auf dem Abonnenten löschen möchten, müssen Sie diese manuell löschen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
-   **So deaktivieren Sie die Veröffentlichung und Verteilung mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Zum Deaktivieren der Veröffentlichung und Verteilung müssen sämtliche Verteilungs- und Veröffentlichungsdatenbanken online sein. Wenn für Verteilungs- oder Veröffentlichungsdatenbanken *Datenbankmomentaufnahmen* vorhanden sind, müssen diese gelöscht werden, bevor die Veröffentlichung und Verteilung deaktiviert werden kann. Eine Datenbankenmomentaufnahme ist eine schreibgeschützte Offlinekopie einer Datenbank, die in keinem Bezug zu einer Replikationsmomentaufnahme steht. Weitere Informationen finden Sie unter [Datenbanksnapshots & #40; SQL Server & #41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Sie können die Veröffentlichung und die Verteilung mithilfe des Veröffentlichungs- und Verteilungsdeaktivierungs-Assistenten deaktivieren.  
  
#### So deaktivieren Sie die Veröffentlichung und Verteilung  
  
1.  Stellen Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger oder Verteiler her, den Sie deaktivieren möchten, und erweitern Sie dann den Serverknoten.  
  
2.  Mit der rechten Maustaste die **Replikation** Ordner, und klicken Sie dann auf **Veröffentlichung und Verteilung deaktivieren**.  
  
3.  Führen Sie die Schritte des Veröffentlichungs- und Verteilungsdeaktivierungs-Assistenten vollständig aus.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Die Veröffentlichung und die Verteilung können mit gespeicherten Replikationsprozeduren programmgesteuert deaktiviert werden.  
  
#### So deaktivieren Sie die Veröffentlichung und Verteilung  
  
1.  Beenden Sie alle replikationsbezogenen Aufträge. Eine Auflistung der Auftragsnamen finden Sie im Abschnitt "Agentsicherheit mit SQL Server-Agent" unter [Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
2.  Führen Sie auf jeden Abonnenten für die Abonnementdatenbank [Sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) um Replikationsobjekte aus der Datenbank zu entfernen. Diese gespeicherte Prozedur entfernt keine Replikationsaufträge vom Verteiler.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) um Replikationsobjekte aus der Datenbank zu entfernen.  
  
4.  Wenn der Verleger einen Remoteverteiler verwendet, führen Sie [Sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md).  
  
5.  Führen Sie auf dem Verteiler [Sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md). Diese gespeicherte Prozedur sollte für jeden auf dem Verteiler registrierten Verleger einmal ausgeführt werden.  
  
6.  Führen Sie auf dem Verteiler [Sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md) die Verteilungsdatenbank zu löschen. Diese gespeicherte Prozedur sollte für jede Verteilungsdatenbank auf dem Verteiler einmal ausgeführt werden. Dadurch werden außerdem alle der Verteilungsdatenbank zugeordnete Warteschlangenlese-Agentaufträge entfernt.  
  
7.  Führen Sie auf dem Verteiler [Sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) um die verteilerbezeichnung vom Server zu entfernen.  
  
    > [!NOTE]  
    >  Wenn alle Replikationsobjekte Veröffentlichung und Verteilung nicht gelöscht werden, vor dem Ausführen [Sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md) und [Sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md), diese Prozeduren einen Fehler zurück. Alle replikationsbezogenen Objekte gelöscht, wenn ein Verleger oder Verteiler gelöscht wird, die **@no_checks** -Parameter muss festgelegt werden, um **1**. Wenn der Verleger oder Verteiler offline oder nicht erreichbar ist, wird die **@ignore_distributor** -Parameter kann festgelegt werden, dass **1** damit sie gelöscht werden können; jedoch alle Veröffentlichungs- und Verteilungsobjekte müssen manuell entfernt werden.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Dieses Beispielskript entfernt Replikationsobjekte aus der Abonnementdatenbank.  
  
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/disable-publishing-and-d_1.sql)]  
  
 Dieses Beispielskript deaktiviert die Veröffentlichung und die Verteilung auf einem Server, der ein Verleger und Verteiler ist, und löscht die Verteilungsdatenbank.  
  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/disable-publishing-and-d_2.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
  
#### So deaktivieren Sie die Veröffentlichung und Verteilung  
  
1.  Entfernen Sie alle Abonnements von Veröffentlichungen, für die der Verteiler verwendet wird. Weitere Informationen finden Sie unter [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md) und [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md).  
  
2.  Entfernen Sie alle Veröffentlichungen, für die der Verteiler verwendet wird, und deaktivieren Sie die Veröffentlichung für alle Datenbanken, wenn sich Verleger und Verteiler auf dem gleichen Server befinden. Weitere Informationen finden Sie unter [Delete a Publication](../../relational-databases/replication/publish/delete-a-publication.md).  
  
3.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
4.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.DistributionPublisher> Klasse. Geben Sie den <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> -Eigenschaft, und übergeben Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Objekt aus Schritt 3.  
  
5.  (Optional) Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode rufen Sie die Eigenschaften des Objekts, und stellen Sie sicher, dass der Verleger vorhanden ist. Wenn diese Methode **false**zurückgibt, war der in Schritt 4 festgelegte Verlegername falsch, oder der Verleger wird von diesem Verteiler nicht verwendet.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Remove%2A> Methode. Übergeben Sie den Wert **true** für *force* , wenn sich Verleger und Verteiler auf verschiedenen Servern befinden, und wenn der Verleger auf dem Verteiler deinstalliert werden soll, ohne dass zuvor überprüft wurde, ob die Veröffentlichungen auf dem Verleger gelöscht wurden.  
  
7.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer> Klasse. Übergeben Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Objekt aus Schritt 3.  
  
8.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationServer.UninstallDistributor%2A> Methode. Übergeben Sie den Wert **true** für *force* , um alle Replikationsobjekte auf dem Verteiler zu löschen, ohne zuvor zu überprüfen, ob die lokalen Veröffentlichungsdatenbanken deaktiviert und die Verteilerdatenbanken deinstalliert wurden.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 In diesem Beispiel werden die Verlegerregistrierung auf dem Verteiler entfernt, die Verteilungsdatenbank gelöscht und der Verteiler deinstalliert.  
  
 [!code-csharp[HowTo#rmo_DropDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropdistpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropdistpub)]  
  
 In diesem Beispiel wird der Verteiler deinstalliert, ohne dass zuvor die lokalen Veröffentlichungsdatenbanken deaktiviert oder die Verteilungsdatenbank gelöscht wurde.  
  
 [!code-csharp[HowTo#rmo_DropDistPubForce](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropdistpubforce)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPubForce](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropdistpubforce)]  
  
## Siehe auch  
 [Konzepte für Replikationsverwaltungsobjekte (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  