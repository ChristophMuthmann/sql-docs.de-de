---
title: "Angeben eines Mergeartikelkonfliktlösers | Microsoft-Dokumentation"
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
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
- merge replication conflict resolution [SQL Server replication], merge article resolvers
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2934cf0580b44b6a496f9dae4d5cd297cd8717d7
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="specify-a-merge-article-resolver"></a>Angeben eines Mergeartikelkonfliktlösers
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
  
    -   Den Standardkonfliktlöser. Das Verhalten des Standardkonfliktlösers hängt davon ab, ob es sich um ein Clientabonnement oder ein Serverabonnement handelt. Informationen zum Angeben eines Abonnementtyps finden Sie unter [Angeben eines Mergerabonnementtyps und einer Konfliktlösungspriorität &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md).  
  
    -   Von Ihnen geschriebene benutzerdefinierte Konfliktlöser. Dabei kann es sich um einen Geschäftslogikhandler (in verwaltetem Code geschrieben) oder einen benutzerdefinierten COM-basierten Konfliktlöser handeln. Weitere Informationen finden Sie unter [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)angegeben wird. Wenn Sie benutzerdefinierte Logik implementieren müssen, die für jede replizierte Zeile und nicht nur für Konfliktzeilen ausgeführt werden muss, finden Sie unter [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)angegeben wird.  
  
    -   Einen COM-basierten Standardkonfliktlöser, der Bestandteil von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ist.  
  
-   Wenn Sie einen anderen als den Standardkonfliktlöser verwenden möchten, müssen Sie den Konfliktlöser auf den Computer kopieren und dort registrieren, auf dem der Merge-Agent ausgeführt wird (ein Geschäftslogikhandler muss auch auf dem Verleger registriert werden). Der Merge-Agent wird auf folgenden Computern ausgeführt:  
  
    -   Dem Verteiler für ein Pushabonnement  
  
    -   Dem Abonnent für ein Pullabonnement  
  
    -   Dem Server mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internetinformationsdienste (IIS) für ein Pullabonnement, das die Websynchronisierung verwendet.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Nach dem Registrieren des Konfliktlösers geben Sie dessen Verwendung durch einen Artikel im Dialogfeld **Artikeleigenschaften - \<Artikel>** auf der Registerkarte **Konfliktlöser** an. Dieses Dialogfeld ist im Assistenten für neue Veröffentlichung über das Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** verfügbar. Weitere Informationen zum Verwenden des Assistenten sowie zum Zugriff auf das Dialogfeld finden Sie unter [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-resolver"></a>So geben Sie einen Konfliktlöser an  
  
1.  Wählen Sie auf der Seite **Artikel** des Assistenten für neue Veröffentlichung bzw. des Dialogfelds **Veröffentlichungseigenschaften - \<Veröffentlichung>** eine Tabelle aus.  
  
2.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Artikels festlegen**.  
  
3.  Klicken Sie auf der Seite **Artikeleigenschaften - \<Artikel>** auf die Registerkarte **Konfliktlöser**.  
  
4.  Wählen Sie **Benutzerdefinierten Konfliktlöser verwenden (registriert auf dem Verteiler)**aus, und klicken Sie dann in der Liste auf den Konfliktlöser.  
  
5.  Sind für den Konfliktlöser Eingaben erforderlich (z. B. ein Spaltenname), geben Sie sie im Textfeld **Geben Sie die vom Konfliktlöser benötigten Informationen ein** an.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Wiederholen Sie diesen Vorgang für jeden Artikel, der einen Konfliktlöser erfordert.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-register-a-custom-conflict-resolver"></a>So registrieren Sie einen benutzerdefinierten Konfliktlöser  
  
1.  Wenn Sie einen eigenen benutzerdefinierten Konfliktlöser registrieren möchten, erstellen Sie einen der folgenden Typen:  
  
    -   Einen auf verwaltetem Code basierenden Konfliktlöser als Geschäftslogikhandler. Weitere Informationen finden Sie unter [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Konfliktlöser, der auf einer gespeicherten Prozedur und COM basiert. Weitere Informationen finden Sie unter [Implement a Custom Conflict Resolver for a Merge Article](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md).  
  
2.  Um zu bestimmen, ob der gewünschte Konfliktlöser bereits registriert ist, führen Sie auf dem Verleger für eine beliebige Datenbank [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) aus. Daraufhin werden eine Beschreibung des benutzerdefinierten Konfliktlösers sowie der Klassenbezeichner (CLSID) für jeden auf dem Verteiler registrierten COM-basierten Konfliktlöser bzw. Informationen zur verwalteten Assembly für jeden auf dem Verteiler registrierten Geschäftslogikhandler angezeigt.  
  
3.  Wenn der gewünschte benutzerdefinierte Konfliktlöser noch nicht registriert ist, führen Sie auf dem Verteiler [sp_registercustomresolver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) aus. Geben Sie den Namen des Konfliktlösers für **@article_resolver**an. Bei Geschäftslogikhandlern ist dies der Anzeigenamen der Assembly. Geben Sie für COM-basierte Konfliktlöser den Klassenbezeichner CLSID der DLL für **@resolver_clsid** an, und für einen Geschäftslogikhandler den Wert **true** für **@is_dotnet_assembly**, den Namen der Assembly für **@dotnet_assembly_name**, und den vollqualifizierten Namen der Klasse, die <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> überschreibt, für **@dotnet_class_name**.  
  
    > [!NOTE]  
    >  Sie müssen den vollständigen Pfad mit dem Assemblynamen für **@dotnet_assembly_name**angegeben wird.  
  
4.  Wenn der Konfliktlöser ein COM-basierter Konfliktlöser ist, gehen Sie wie folgt vor:  
  
    -   Kopieren Sie die DLL für den benutzerdefinierten Konfliktlöser auf den Verteiler für Pushabonnements oder auf den Abonnenten von Pullabonnements.  
  
        > [!NOTE]  
        >  Benutzerdefinierte Konfliktlöser von[!INCLUDE[msCoName](../../../includes/msconame-md.md)] sind im [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM-Verzeichnis enthalten.  
  
    -   Verwenden Sie regsvr32.exe, um die benutzerdefinierte Konfliktlöser-DLL im Betriebssystem zu registrieren. Führen Sie beispielsweise folgenden Befehl an der Eingabeaufforderung aus, um den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konfliktlöser Zusatz zu registrieren:  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  Wenn es sich beim Konfliktlöser um einen Geschäftslogikhandler handelt, stellen Sie die Assembly im gleichen Ordner wie die ausführbare Datei des Merge-Agents (replmerg.exe), im gleichen Ordner wie eine Anwendung, die den Merge-Agent aufruft, oder in dem in Schritt für den **@dotnet_assembly_name** -Parameter angegebenen Ordner bereit.  
  
    > [!NOTE]  
    >  Der Standardinstallationspfad der ausführbaren Merge-Agent-Datei lautet [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
#### <a name="to-specify-a-custom-resolver-when-defining-a-merge-article"></a>So geben Sie in der Definition eines Mergeartikels einen benutzerdefinierten Konfliktlöser an  
  
1.  Wenn Sie einen eigenen benutzerdefinierten Konfliktlöser verwenden möchten, erstellen und registrieren Sie den Konfliktlöser wie oben beschrieben.  
  
2.  Führen Sie auf dem Verleger [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)aus, und notieren Sie den Namen des gewünschten benutzerdefinierten Konfliktlösers im **value**-Feld des Resultsets.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) aus. Geben Sie den Namen des Konfliktlösers aus Schritt 2 für **@article_resolver** und gegebenenfalls alle für den benutzerdefinierten Konfliktlöser erforderlichen Eingaben im Parameter **@resolver_info** an. Bei benutzerdefinierten Konfliktlösern, die auf einer gespeicherten Prozedur basieren, entspricht **@resolver_info** dem Namen der gespeicherten Prozedur. Weitere Informationen zu den für [!INCLUDE[msCoName](../../../includes/msconame-md.md)] erforderlichen Eingaben für Konfliktlöser finden Sie unter [Microsoft COM-Based Resolvers (Microsoft COM-basierte Konfliktlöser)](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
#### <a name="to-specify-or-change-a-custom-resolver-for-an-existing-merge-article"></a>So geben Sie einen benutzerdefinierten Konfliktlöser für einen vorhandenen Mergeartikel an oder ändern diesen  
  
1.  Um zu bestimmen, ob ein benutzerdefinierter Konfliktlöser für einen Artikel definiert wurde, oder um den Namen des Konfliktlösers abzurufen, führen Sie [sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) aus. Wenn ein benutzerdefinierter Konfliktlöser für einen Artikel definiert wurde, wird dessen Namen im Feld **article_resolver** angezeigt. Alle dem Konfliktlöser übergegebene Eingaben werden im Feld **resolver_info** des Resultsets angezeigt.  
  
2.  Führen Sie auf dem Verleger [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) aus, und notieren Sie den Namen des gewünschten benutzerdefinierten Konfliktlösers im **value**-Feld des Resultsets.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) aus. Geben Sie den Wert **article_resolver**, einschließlich der vollständigen Pfadangabe für Geschäftslogikhandler, für **@property**und den Namen des gewünschten benutzerdefinierten Konfliktslösers aus Schritt 2 für **@value**angegeben wird.  
  
4.  Führen Sie nochmals [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) aus, um irgendwelche erforderlichen Eingaben für den benutzerdefinierten Konfliktlöser zu ändern. Geben Sie den Wert **resolver_info** für **@property** und alle erforderlichen Eingaben für den benutzerdefinierten Konfliktlöser für **@value**angegeben wird. Bei benutzerdefinierten Konfliktlösern, die auf einer gespeicherten Prozedur basieren, entspricht **@resolver_info** dem Namen der gespeicherten Prozedur. Weitere Informationen zu den erforderlichen Eingaben finden Sie unter [Microsoft COM-Based Resolvers (Microsoft COM-basierte Konfliktlöser)](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
#### <a name="to-unregister-a-custom-conflict-resolver"></a>So heben Sie die Registrierung eines benutzerdefinierten Konfliktlösers auf  
  
1.  Führen Sie auf dem Verleger [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) aus, und notieren Sie den Namen des zu entfernenden benutzerdefinierten Konfliktlösers im **value**-Feld des Resultsets.  
  
2.  Führen Sie [Sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) auf dem Verteiler aus. Geben Sie den vollständigen Namen des benutzerdefinierten Konfliktlösers aus Schritt 1 für **@article_resolver**angegeben wird.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel wird ein neuer Artikel erstellt und angegeben, dass der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konfliktlöser "Mittelwerterstellung" zur Berechnung des Mittelwerts der Spalte **UnitPrice** verwendet werden soll, wenn Konflikte auftreten.  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 In diesem Beispiel wird ein Artikel dahingehend geändert, dass der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konfliktlöser "Zusatz" zur Berechnung der Summe der Spalte **UnitsOnOrder** verwendet werden soll, wenn Konflikte auftreten.  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
