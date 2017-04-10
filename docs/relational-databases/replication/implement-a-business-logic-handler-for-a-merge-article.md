---
title: "Implementieren eines Gesch&#228;ftslogikhandlers f&#252;r einen Mergeartikel | Microsoft Docs"
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
  - "Konfliktlösung bei der Mergereplikation [SQL Server-Replikation], Geschäftslogikhandler"
  - "Geschäftslogikhandler für die Mergereplikation [SQL Server-Replikation]"
  - "Konfliktlösung [SQL Server-Replikation], Mergereplikation "
  - "Geschäftslogikhandler [SQL Server-Replikation]"
  - "BusinessLogicModule-Klasse"
ms.assetid: ed477595-6d46-4fa2-b0d3-a5358903ec05
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Implementieren eines Gesch&#228;ftslogikhandlers f&#252;r einen Mergeartikel
  In diesem Thema wird beschrieben, wie ein Geschäftslogikhandler für einen Mergeartikel mit Replikationsprogrammierung oder Replikationsverwaltungsobjekten (RMO) in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] implementiert wird.  
  
 Die <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> Namespace implementiert eine Schnittstelle, mit dem Sie komplexe Geschäftslogik zum Verarbeiten von Ereignissen, die auftreten, während der Synchronisierung der Mergereplikation schreiben. Die Methoden im Geschäftslogikhandler können vom Replikationsvorgang für jede geänderte Zeile aufgerufen werden, die während der Synchronisierung repliziert wird.  
  
 Der allgemeine Vorgang zum Implementieren eines Geschäftslogikhandlers ist Folgender:  
  
1.  Erstellen Sie die Geschäftslogikhandler-Assembly.  
  
2.  Registrieren Sie die Assembly beim Verteiler.  
  
3.  Stellen Sie die Assembly auf dem Server bereit, auf dem der Merge-Agent ausgeführt wird. Für ein Pullabonnement wird der Agent auf dem Abonnenten ausgeführt, und für ein Pushabonnement wird der Agent auf dem Verteiler ausgeführt. Wenn Sie die Websynchronisierung verwenden, wird der Agent auf dem Webserver ausgeführt.  
  
4.  Erstellen Sie einen Artikel, der den Geschäftslogikhandler verwendet, oder ändern Sie einen vorhandenen Artikel so, dass er den Geschäftslogikhandler verwendet.  
  
 Der von Ihnen angegebene Geschäftslogikhandler wird für jede Zeile ausgeführt, die synchronisiert wird. Eine komplexe Logik und Aufrufe anderer Anwendungen oder Netzwerkdienste können sich auf die Leistung auswirken. Weitere Informationen zu geschäftslogikhandlern finden Sie unter [führen Business Logic During Merge Synchronization](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
 **In diesem Thema**  
  
-   **So implementieren Sie einen Geschäftslogikhandler für einen Mergeartikel mit:**  
  
     [Replikationsprogrammierung](#ReplProg)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="ReplProg"></a> Verwenden der Replikationsprogrammierung  
  
#### So erstellen Sie einen Geschäftslogikhandler und stellen ihn bereit  
  
1.  Erstellen Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio ein neues Projekt für die .NET-Assembly mit dem Code, der den Geschäftslogikhandler implementiert.  
  
2.  Fügen Sie Verweise auf das Projekt für die folgenden Namespaces hinzu.  
  
    |Assemblyverweis|Location|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM (Standardinstallation)|  
    |<xref:System.Data>|GAC (Komponente von .NET Framework)|  
    |<xref:System.Data.Common>|GAC (Komponente von .NET Framework)|  
  
3.  Fügen Sie eine Klasse, die überschreibt die <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> Klasse.  
  
4.  Implementieren der <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> Eigenschaft, um die Typen von Änderungen anzugeben, die verarbeitet werden.  
  
5.  Überschreiben Sie eine oder mehrere der folgenden Methoden von der <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> Klasse:  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> -wird aufgerufen, wenn eine Änderung während der Synchronisierung ein Commit ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> -wird aufgerufen, wenn ein Fehler auftritt, während eine DELETE-Anweisung ist, hochgeladen oder heruntergeladen wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> -wird aufgerufen, wenn DELETE-Anweisungen hochgeladen oder heruntergeladen.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> -wird aufgerufen, wenn ein Fehler auftritt, während eine INSERT-Anweisung ist, hochgeladen oder heruntergeladen wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> -wird aufgerufen, wenn INSERT-Anweisungen hochgeladen oder heruntergeladen.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> -wird aufgerufen, wenn in Konflikt stehende UPDATE-Anweisungen auf dem Verleger und Abonnenten auftreten.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> -wird aufgerufen, wenn die UPDATE-Anweisungen mit DELETE-Anweisungen auf dem Verleger und Abonnenten in Konflikt stehen.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> -wird aufgerufen, wenn ein Fehler auftritt, während eine UPDATE-Anweisung ist, hochgeladen oder heruntergeladen wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> -wird aufgerufen, wenn die UPDATE-Anweisungen hochgeladen oder heruntergeladen.  
  
6.  Erstellen Sie das Projekt, um die Geschäftslogikhandler-Assembly zu erstellen.  
  
7.  Stellen Sie die Assembly in dem Verzeichnis mit der ausführbaren Datei für den Merge-Agent (replmerg.exe) bereit (bei der Standardinstallation ist dies [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM), oder installieren Sie sie im globalen Assemblycache (GAC) von .NET. Installieren Sie die Assembly nur dann im GAC, wenn andere Anwendungen als der Merge-Agent auf die Assembly zugreifen müssen. Die Assembly im GAC, Global Assembly Cache-Tool mit installiert werden kann (**Gacutil.exe)** in .NET Framework SDK bereitgestellt.  
  
    > [!NOTE]  
    >  Auf jedem Server, auf dem der Merge-Agent ausgeführt wird, muss ein Geschäftslogikhandler bereitgestellt werden. Dazu gehört auch der IIS-Server, der die Datei replisapi.dll hostet, wenn die Websynchronisierung verwendet wird.  
  
#### So registrieren Sie einen Geschäftslogikhandler  
  
1.  Führen Sie auf dem Verleger [Sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) Überprüfen Sie, dass die Assembly noch nicht als Geschäftslogikhandler registriert wurde.  
  
2.  Führen Sie auf dem Verteiler [Sp_registercustomresolver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md), dabei einen Anzeigenamen für den Geschäftslogikhandler für **@article_resolver**, Wert **true** für **@is_dotnet_assembly**, den Namen der Assembly für **@dotnet_assembly_name**, und den vollqualifizierten Namen der Klasse, die überschreibt <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> für **@dotnet_class_name**.  
  
    > [!NOTE]  
    >  Wenn die Assembly nicht im selben Verzeichnis wie die ausführbare Datei der Merge-Agent bereitgestellt wird, im gleichen Verzeichnis wie die Anwendung, die der Merge-Agent synchron gestartet oder in den globalen Assemblycache (GAC), Sie den vollständigen Pfad angeben, mit dem Assemblynamen für müssen **@dotnet_assembly_name**. Wenn Sie die Websynchronisierung verwenden, müssen Sie den Speicherort der Assembly auf dem Webserver angeben.  
  
#### So verwenden Sie einen Geschäftslogikhandler mit einem neuen Tabellenartikel  
  
1.  Führen Sie [Sp_addmergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) zur Definition eines Artikels, dabei den Anzeigenamen des geschäftslogikhandlers für **@article_resolver**. Weitere Informationen finden Sie unter [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### So verwenden Sie einen Geschäftslogikhandler mit einem bestehenden Tabellenartikel  
  
1.  Führen Sie [Sp_changemergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), wobei **@publication**, **@article**, ein Wert von **Article_resolver** für **@property**, und den Anzeigenamen des geschäftslogikhandlers für **@value**.  
  
###  <a name="TsqlExample"></a> Beispiele (Replikationsprogrammierung)  
 In diesem Beispiel wird ein Geschäftslogikhandler gezeigt, der ein Überwachungsprotokoll erstellt.  
  
 [!code-csharp[HowTo#rmo_BusinessLogicCode](../../relational-databases/replication/codesnippet/csharp/rmohowto/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 Das folgende Beispiel registriert eine Geschäftslogikhandler-Assembly auf dem Verteiler und ändert einen bestehenden Mergeartikel so, dass diese benutzerdefinierte Geschäftslogik verwendet wird.  
  
 [!code-sql[HowTo#sp_RegisterBLH_10](../../relational-databases/replication/codesnippet/tsql/implement-a-business-log_3.sql)]  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
  
#### So erstellen Sie einen Geschäftslogikhandler  
  
1.  Erstellen Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio ein neues Projekt für die .NET-Assembly mit dem Code, der den Geschäftslogikhandler implementiert.  
  
2.  Fügen Sie Verweise auf das Projekt für die folgenden Namespaces hinzu.  
  
    |Assemblyverweis|Location|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM (Standardinstallation)|  
    |<xref:System.Data>|GAC (Komponente von .NET Framework)|  
    |<xref:System.Data.Common>|GAC (Komponente von .NET Framework)|  
  
3.  Fügen Sie eine Klasse, die überschreibt die <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> Klasse.  
  
4.  Implementieren der <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> Eigenschaft, um die Typen von Änderungen anzugeben, die verarbeitet werden.  
  
5.  Überschreiben Sie eine oder mehrere der folgenden Methoden von der <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> Klasse:  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> -wird aufgerufen, wenn eine Änderung während der Synchronisierung ein Commit ausgeführt wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> -wird aufgerufen, wenn ein Fehler auftritt, während eine DELETE-Anweisung hochgeladen oder heruntergeladen.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> -wird aufgerufen, wenn DELETE-Anweisungen hochgeladen oder heruntergeladen.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> -wird aufgerufen, wenn ein Fehler auftritt, während eine INSERT-Anweisung, hochgeladen oder heruntergeladen wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> -wird aufgerufen, wenn INSERT-Anweisungen hochgeladen oder heruntergeladen.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> -wird aufgerufen, wenn in Konflikt stehende UPDATE-Anweisungen auf dem Verleger und Abonnenten auftreten.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> -wird aufgerufen, wenn die UPDATE-Anweisungen mit DELETE-Anweisungen auf dem Verleger und Abonnenten in Konflikt stehen.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> -wird aufgerufen, wenn ein Fehler auftritt, während eine UPDATE-Anweisung, hochgeladen oder heruntergeladen wird.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> -wird aufgerufen, wenn die UPDATE-Anweisungen hochgeladen oder heruntergeladen.  
  
    > [!NOTE]  
    >  Alle Artikelkonflikte, die nicht explizit von Ihrem benutzerdefinierten Geschäftslogikhandler verarbeitet werden, werden vom Standardkonfliktlöser für den Artikel bearbeitet.  
  
6.  Erstellen Sie das Projekt, um die Geschäftslogikhandler-Assembly zu erstellen.  
  
#### So registrieren Sie einen Geschäftslogikhandler  
  
1.  Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer> Klasse. Übergeben Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1.  
  
3.  Rufen Sie <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumBusinessLogicHandlers%2A> und überprüfen Sie das zurückgegebene <xref:System.Collections.ArrayList> Objekt, um sicherzustellen, dass die Assembly noch nicht als Geschäftslogikhandler registriert wurde.  
  
4.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler> Klasse. Geben Sie die folgenden Eigenschaften an:  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetAssemblyName%2A> -der Name der .NET-Assembly. Sie müssen den vollständigen Pfad mit dem Assemblynamen angeben, falls die Assembly nicht im gleichen Verzeichnis wie die ausführbare Datei für den Merge-Agent, im gleichen Verzeichnis wie die Anwendung, mit der der Merge-Agent synchron gestartet wird, oder im GAC bereitgestellt wird. Sie müssen den vollständigen Pfad mit dem Assemblynamen angeben, wenn Sie einen Geschäftslogikhandler mit der Websynchronisierung verwenden.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetClassName%2A> -den vollständig qualifizierten Namen der Klasse, die überschreibt <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> und den Geschäftslogikhandler implementiert.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> -einen Anzeigenamen ein, die Sie beim Zugriff auf den Geschäftslogikhandler verwenden.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.IsDotNetAssembly%2A> -Wert **true**.  
  
#### So stellen Sie einen Geschäftslogikhandler bereit  
  
1.  Stellen Sie die Assembly auf dem Server, auf dem der Merge-Agent ausgeführt wird, in dem Dateispeicherort bereit, der angegeben wurde, als der Geschäftslogikhandler beim Verteiler registriert wurde. Für ein Pullabonnement wird der Agent auf dem Abonnenten ausgeführt, und für ein Pushabonnement wird der Agent auf dem Verteiler ausgeführt. Wenn Sie die Websynchronisierung verwenden, wird der Agent auf dem Webserver ausgeführt. Wenn der vollständige Pfad beim Registrieren des Geschäftslogikhandlers nicht zusammen mit dem Assemblynamen angegeben wurde, stellen Sie die Assembly im gleichen Verzeichnis wie die ausführbare Datei für den Merge-Agent, im gleichen Verzeichnis wie die Anwendung, mit der der Merge-Agent synchron gestartet wird, bereit. Sie können die Assembly im GAC installieren, wenn es mehrere Anwendungen gibt, die die gleiche Assembly verwenden.  
  
#### So verwenden Sie einen Geschäftslogikhandler mit einem neuen Tabellenartikel  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeArticle> Klasse. Legen Sie die folgenden Eigenschaften fest:  
  
    -   Der Name des Artikels für <xref:Microsoft.SqlServer.Replication.Article.Name%2A>.  
  
    -   Der Name der Veröffentlichung für <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>.  
  
    -   Der Name der Veröffentlichungsdatenbank für <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A>.  
  
    -   Der Anzeigename des Geschäftslogikhandler (<xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A>) für <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Article.Create%2A> Methode. Weitere Informationen finden Sie unter [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### So verwenden Sie einen Geschäftslogikhandler mit einem bestehenden Tabellenartikel  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeArticle> Klasse.  
  
3.  Legen Sie den <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, und <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Eigenschaften.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode zum Abrufen der Eigenschaften des Objekts. Wenn diese Methode **false**zurückgibt, wurden entweder die Artikeleigenschaften in Schritt 3 falsch definiert, oder der Artikel ist nicht vorhanden. Weitere Informationen finden Sie unter [View and Modify Article Properties](../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
6.  Legen Sie den Anzeigenamen des geschäftslogikhandlers für <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>. Dies ist der Wert, der die <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> Eigenschaft, die beim Registrieren des geschäftslogikhandlers angegeben.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 Dieses Beispiel zeigt einen Geschäftslogikhandler, der Informationen über Einfüge-, Update- und Löschvorgänge auf dem Abonnenten protokolliert.  
  
 [!code-csharp[HowTo#rmo_BusinessLogicCode](../../relational-databases/replication/codesnippet/csharp/rmohowto/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 In diesem Beispiel wird ein Geschäftslogikhandler beim Verteiler registriert.  
  
 [!code-csharp[HowTo#rmo_RegisterBLH_10](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_registerblh_10)]  
  
 [!code-vb[HowTo#rmo_vb_RegisterBLH_10](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_registerblh_10)]  
  
 In diesem Beispiel wird ein vorhandener Artikel geändert, um den Geschäftslogikhandler zu verwenden.  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## Siehe auch  
 [Implementieren eines benutzerdefinierten Konfliktlösers für einen Mergeartikel](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [Debuggen Sie einen Geschäftslogikhandler & #40; Replikationsprogrammierung & #41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Konzepte für Replikationsverwaltungsobjekte (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
  
  