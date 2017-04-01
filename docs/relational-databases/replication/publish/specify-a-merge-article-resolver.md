---
title: "Angeben eines Mergeartikelkonfliktl&#246;sers | Microsoft Docs"
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
  - "Artikel [SQL Server-Replikation], Konfliktlösung"
  - "Konfliktlösung [SQL Server-Replikation], Mergereplikation "
  - "Konfliktlösung bei der Mergereplikation [SQL Server-Replikation], Mergeartikelkonfliktlöser"
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Angeben eines Mergeartikelkonfliktl&#246;sers
  In diesem Thema wird beschrieben, wie ein Konfliktlöser für Mergeartikel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]angegeben wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
-   **So geben Sie einen Mergeartikelkonfliktlöser an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Die Mergereplikation unterstützt die folgenden Typen von Artikelkonfliktlösern:  
  
    -   Den Standardkonfliktlöser. Das Verhalten des Standardkonfliktlösers hängt davon ab, ob es sich um ein Clientabonnement oder ein Serverabonnement handelt. Weitere Informationen zum Angeben des Abonnementtyps finden Sie unter [Geben Sie den Abonnementtyp zusammenführen und Konfliktlösungspriorität & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/specify a merge subscription type and conflict resolution priority.md).  
  
    -   Von Ihnen geschriebene benutzerdefinierte Konfliktlöser. Dabei kann es sich um einen Geschäftslogikhandler (in verwaltetem Code geschrieben) oder einen benutzerdefinierten COM-basierten Konfliktlöser handeln. Weitere Informationen finden Sie unter [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md). Sollten Sie benutzerdefinierte Logik implementieren, die ausgeführt wird, finden Sie in jede replizierte Zeile und nicht nur für Zeilen, die in Konflikt stehende [Implementieren Sie einen Geschäftslogikhandler für einen Artikel Merge](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Einen COM-basierten Standardkonfliktlöser, der in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Wenn Sie einen anderen als den Standardkonfliktlöser verwenden möchten, müssen Sie den Konfliktlöser auf den Computer kopieren und dort registrieren, auf dem der Merge-Agent ausgeführt wird (ein Geschäftslogikhandler muss auch auf dem Verleger registriert werden). Der Merge-Agent wird auf folgenden Computern ausgeführt:  
  
    -   Dem Verteiler für ein Pushabonnement  
  
    -   Dem Abonnent für ein Pullabonnement  
  
    -   Dem Server mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internetinformationsdienste (IIS) für ein Pullabonnement, das die Websynchronisierung verwendet.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Nachdem der Konfliktlöser registriert wurde, geben Sie, dass ein Artikel den Resolver zu verwenden, sollten die **Konfliktlöser** auf der Registerkarte der **Artikeleigenschaften - \< Artikel>** Dialogfeld, das im Assistenten für neue Veröffentlichung verfügbar ist und die **Veröffentlichungseigenschaften - \< Veröffentlichung>** im Dialogfeld. Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So geben Sie einen Konfliktlöser an  
  
1.  Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld Wählen Sie eine Tabelle aus.  
  
2.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Artikels festlegen**.  
  
3.  Auf der **Artikeleigenschaften - \< Artikel>** auf der **Konfliktlöser** Registerkarte.  
  
4.  Wählen Sie **einen benutzerdefinierten Konfliktlöser verwenden (registriert auf dem Verteiler)**, und klicken Sie dann in der Liste auf den Konfliktlöser.  
  
5.  Der Konfliktlöser Eingaben (z. B. ein Spaltenname) erforderlich, geben Sie es in den **Geben Sie Informationen, die vom Konfliktlöser benötigten** Textfeld.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Wiederholen Sie diesen Vorgang für jeden Artikel, der einen Konfliktlöser erfordert.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So registrieren Sie einen benutzerdefinierten Konfliktlöser  
  
1.  Wenn Sie einen eigenen benutzerdefinierten Konfliktlöser registrieren möchten, erstellen Sie einen der folgenden Typen:  
  
    -   Einen auf verwaltetem Code basierenden Konfliktlöser als Geschäftslogikhandler. Weitere Informationen finden Sie unter [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Konfliktlöser, der auf einer gespeicherten Prozedur und COM basiert. Weitere Informationen finden Sie unter [Implement a Custom Conflict Resolver for a Merge Article](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md).  
  
2.  Um festzustellen, ob der gewünschte Konfliktlöser bereits registriert ist, führen Sie [Sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) auf dem Verleger für jede Datenbank. Daraufhin werden eine Beschreibung des benutzerdefinierten Konfliktlösers sowie der Klassenbezeichner (CLSID) für jeden auf dem Verteiler registrierten COM-basierten Konfliktlöser bzw. Informationen zur verwalteten Assembly für jeden auf dem Verteiler registrierten Geschäftslogikhandler angezeigt.  
  
3.  Wenn der gewünschte benutzerdefinierte Konfliktlöser noch nicht registriert ist, führen Sie [Sp_registercustomresolver & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) auf dem Verteiler. Geben Sie einen Namen für den Konfliktlöser für **@article_resolver**; für einen Geschäftslogikhandler, dies ist der Anzeigename der Assembly. Geben Sie für COM-basierte Konfliktlöser, die CLSID der DLL für **@resolver_clsid**, und geben Sie für einen Geschäftslogikhandler den Wert **true** für **@is_dotnet_assembly**, den Namen der Assembly für **@dotnet_assembly_name**, und den vollqualifizierten Namen der Klasse, die überschreibt <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> für **@dotnet_class_name**.  
  
    > [!NOTE]  
    >  Wenn eine Geschäftslogikhandler-Assembly nicht im selben Verzeichnis wie die ausführbare Datei der Merge-Agent bereitgestellt wird, im gleichen Verzeichnis wie die Anwendung, die der Merge-Agent synchron gestartet oder im globalen Assemblycache (GAC), Sie den vollständigen Pfad mit dem Assemblynamen für angeben müssen **@dotnet_assembly_name**.  
  
4.  Wenn der Konfliktlöser ein COM-basierter Konfliktlöser ist, gehen Sie wie folgt vor:  
  
    -   Kopieren Sie die DLL für den benutzerdefinierten Konfliktlöser auf den Verteiler für Pushabonnements oder auf den Abonnenten von Pullabonnements.  
  
        > [!NOTE]  
        >  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] benutzerdefinierte Konfliktlöser finden Sie in der [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM-Verzeichnis.  
  
    -   Verwenden Sie regsvr32.exe, um die benutzerdefinierte Konfliktlöser-DLL im Betriebssystem zu registrieren. Führen Sie beispielsweise folgenden Befehl an der Eingabeaufforderung aus, um den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konfliktlöser Zusatz zu registrieren:  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  Wenn der Konfliktlöser einen Geschäftslogikhandler handelt, stellen Sie die Assembly im gleichen Ordner wie die ausführbaren Merge-Agent (replmerg.exe), im gleichen Ordner wie eine Anwendung, die der Merge-Agent aufruft, oder der Ordner für die **@dotnet_assembly_name** Parameter in Schritt 3.  
  
    > [!NOTE]  
    >  Der Standardinstallationspfad der ausführbaren Merge-Agent-Datei lautet [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
#### So geben Sie in der Definition eines Mergeartikels einen benutzerdefinierten Konfliktlöser an  
  
1.  Wenn Sie einen eigenen benutzerdefinierten Konfliktlöser verwenden möchten, erstellen und registrieren Sie den Konfliktlöser wie oben beschrieben.  
  
2.  Führen Sie auf dem Verleger [Sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) und notieren Sie den Namen des gewünschten benutzerdefinierten Konfliktlösers in der **Wert** -Feld des Resultsets.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie den Namen des Konfliktlösers aus Schritt 2 für **@article_resolver** und alle erforderlichen Eingaben für den benutzerdefinierten Konfliktlöser der **@resolver_info** Parameter. Gespeicherte Prozeduren basierenden benutzerdefinierten Konfliktlösern **@resolver_info** ist der Name der gespeicherten Prozedur. Weitere Informationen zu erforderlichen Eingaben für bereitgestellte benutzerdefinierte Konfliktlöser [!INCLUDE[msCoName](../../../includes/msconame-md.md)], finden Sie unter [Microsoft COM-basierte Konfliktlöser](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md).  
  
#### So geben Sie einen benutzerdefinierten Konfliktlöser für einen vorhandenen Mergeartikel an oder ändern diesen  
  
1.  Um festzustellen, ob ein benutzerdefinierter Konfliktlöser für einen Artikel definiert wurde, oder um den Namen des Konfliktlösers abzurufen, führen [Sp_helpmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Ist ein benutzerdefinierter Konfliktlöser für den Artikel definiert, der Name erscheint in der **Article_resolver** Feld. Alle dem Konfliktlöser übergegebene Eingaben erscheint in der **Resolver_info** Feld des Resultsets.  
  
2.  Führen Sie auf dem Verleger [Sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) und notieren Sie den Namen des gewünschten benutzerdefinierten Konfliktlösers in der **Wert** Feld des Resultsets.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Geben Sie den Wert **Article_resolver**, einschließlich der vollständigen Pfadangabe für Geschäftslogikhandler, für **@property**, und den Namen des gewünschten benutzerdefinierten Konfliktlösers aus Schritt 2 für **@value**.  
  
4.  Um erforderliche Eingaben für den benutzerdefinierten Konfliktlöser zu ändern, führen [Sp_changemergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) erneut. Geben Sie den Wert **Resolver_info** für **@property** und alle erforderlichen Eingaben für den benutzerdefinierten Konfliktlöser für **@value**. Gespeicherte Prozeduren basierenden benutzerdefinierten Konfliktlösern **@resolver_info** ist der Name der gespeicherten Prozedur. Weitere Informationen zu erforderlichen Eingaben finden Sie unter [Microsoft COM-basierte Konfliktlöser](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md).  
  
#### So heben Sie die Registrierung eines benutzerdefinierten Konfliktlösers auf  
  
1.  Führen Sie auf dem Verleger [Sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) und notieren Sie den Namen des benutzerdefinierten Konfliktlösers entfernen in der **Wert** Feld des Resultsets.  
  
2.  Führen Sie [Sp_unregistercustomresolver & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) auf dem Verteiler. Geben Sie den vollständigen Namen des benutzerdefinierten Konfliktlösers aus Schritt 1 für **@article_resolver**.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel wird ein neuer Artikel erstellt und angegeben, dass der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konfliktlöser "Mittelwerterstellung" zur Berechnung des Mittelwerts der Spalte **UnitPrice** verwendet werden soll, wenn Konflikte auftreten.  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 In diesem Beispiel wird ein Artikel dahingehend geändert, dass der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konfliktlöser "Zusatz" zur Berechnung der Summe der Spalte **UnitsOnOrder** verwendet werden soll, wenn Konflikte auftreten.  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## Siehe auch  
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Implementieren eines Geschäftslogikhandlers für einen Mergeartikel](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  