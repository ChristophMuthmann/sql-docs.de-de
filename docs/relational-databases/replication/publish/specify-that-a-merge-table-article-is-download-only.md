---
title: "Angeben, dass ein neuer Mergetabellenartikel nur herunterladbar ist | Microsoft Docs"
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
  - "Mergereplikation [SQL Server-Replikation], nur herunterladbare Artikel"
  - "Artikel [SQL Server-Replikation], nur herunterladbare"
  - "Nur herunterladbare Artikel"
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Angeben, dass ein neuer Mergetabellenartikel nur herunterladbar ist
  In diesem Thema wird beschrieben, wie angegeben wird, dass ein Mergetabellenartikel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)] nur heruntergeladen werden kann. Nur herunterladbare Artikel sind für Anwendungen vorgesehen, deren Daten nicht auf den Abonnenten aktualisiert werden. Weitere Informationen finden Sie unter [Merge Replikationsleistung mit Download-Only Artikeln optimieren](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So geben Sie an, dass ein Mergetabellenartikel nur herunterladbar ist, mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie nach der Initialisierung von Abonnements angeben, dass ein Artikel nur herunterladbar sein soll, müssen sämtliche Clientabonnements, die den Artikel erhalten, erneut initialisiert werden. Serverabonnements müssen nicht erneut initialisiert werden. Weitere Informationen zu den Auswirkungen von eigenschaftenänderungen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Angeben, dass ein Artikel nur herunterladbar auf die **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Eigenschaften** Registerkarte der **Artikeleigenschaften - \< Artikel>** (Dialogfeld). Dieses Dialogfeld steht im Assistenten für neue Veröffentlichung und die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So geben Sie auf der Seite Artikel an, dass ein Artikel nur herunterladbar sein soll  
  
-   Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung auswählen eine Tabelle, und wählen Sie dann das Kontrollkästchen **Hervorhebung markierte Tabelle ist nur herunterladbar**.  
  
#### Um anzugeben, dass ein Artikel nur herunterladbar auf der Registerkarte Eigenschaften Artikeleigenschaften - \< Artikel> (Dialogfeld)  
  
1.  Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld Wählen Sie eine Tabelle, und klicken Sie dann auf **Artikeleigenschaften**.  
  
2.  Klicken Sie auf **Eigenschaften des hervorgehobenen Tabelle-Artikels festlegen** oder **Eigenschaften aller Tabellenartikel festlegen**.  
  
3.  In der **Zielobjekt** Teil der **Eigenschaften** auf der Registerkarte der **Artikeleigenschaften - \< Artikel>** Dialogfeld geben die folgenden Werte für **synchronisierungsrichtung**:  
  
    -   **Nur herunterladbar auf Abonnenten, Abonnentenänderungen nicht zulassen**  
  
    -   **Nur herunterladbar auf Abonnenten, Abonnentenänderungen zulassen**  
  
4.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So geben Sie an, dass ein neuer Mergetabellenartikel nur herunterladbar ist  
  
1.  Führen Sie [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), Angabe des Werts **1** oder **2** für den Parameter **@subscriber_upload_options**. Die Werte entsprechen dem folgenden Verhalten:  
  
    -   **0** – keine Einschränkungen (Standard). Auf dem Abonnenten vorgenommene Änderungen werden auf den Verleger hochgeladen.  
  
    -   **1** – Änderungen auf dem Abonnenten sind zulässig, aber nicht an den Verleger hochgeladen.  
  
    -   **2** -Änderungen werden auf dem Abonnenten nicht zulässig.  
  
        > [!NOTE]  
        >  Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung, den Wert des veröffentlicht wurde **@subscriber_upload_options** muss für beide Artikel gleich sein.  
  
#### So ändern Sie einen vorhandenen Mergetabellenartikel dahingehend, dass er nur herunterladbar ist  
  
1.  Um zu bestimmen, ob ein Artikel nur herunterladbar ist, führen Sie [Sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Beachten Sie den Wert der **Upload_options** für den Artikel im Ergebnis festlegen.  
  
2.  Wenn der Rückgabewert in Schritt 1 ist **0**, führen Sie [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), Angabe des Werts **Subscriber_upload_options** für **@property**, Wert **1** für **@force_invalidate_snapshot** und **@force_reinit_subscription**, und den Wert **1** oder **2** für **@value**, zu folgendem Verhalten entspricht:  
  
    -   **1** – Änderungen auf dem Abonnenten sind zulässig, aber nicht an den Verleger hochgeladen.  
  
    -   **2** -Änderungen werden auf dem Abonnenten nicht zulässig.  
  
        > [!NOTE]  
        >  Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung veröffentlicht wurde, muss das Verhalten nur herunterladbarer Artikel gleich sein.  
  
## Siehe auch  
 [Optimieren der Leistung der Mergereplikation durch nur herunterladbare Artikel](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md)   
 [Anzeigen und Ändern von Artikeleigenschaften](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  