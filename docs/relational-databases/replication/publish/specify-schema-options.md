---
title: "Angeben von Schemaoptionen | Microsoft Docs"
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
  - "Schemas [SQL Server-Replikation], Optionen"
  - "Artikel [SQL Server-Replikation], Transaktionsreplikationsoptionen"
  - "Artikel [SQL Server-Replikation], Mergereplikationsoptionen"
  - "Artikel [SQL Server-Replikation], Schemaoptionen"
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Angeben von Schemaoptionen
  In diesem Thema wird beschrieben, wie Schemaoptionen in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]festgelegt werden. Beim Veröffentlichen einer Tabelle oder einer Sicht können Sie die Objekterstellungsoptionen steuern, die für das veröffentlichte Objekt repliziert werden. Sie können diesen Option festlegen, wenn der Artikel erstellt wird, und auch zu einem späteren Zeitpunkt ändern. Wenn Sie diese Optionen für einen Artikel nicht explizit festlegen, wird eine Standardgruppe von Optionen definiert.  
  
> [!NOTE]  
>  Die Standardschemaoptionen bei der Verwendung von gespeicherten Replikationsprozeduren können sich von den Standardoptionen unterscheiden, wenn Artikel mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] hinzugefügt werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
-   **So geben Sie Schemaoptionen an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie Schemaoptionen ändern, nachdem eine Veröffentlichung erstellt wurde, müssen Sie eine neue Momentaufnahme generieren.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Die vollständige Liste der Schemaoptionen finden Sie unter der **@schema_option** Parameter [Sp_addarticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) und [Sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Schemaoptionen angeben, z. B., ob Einschränkungen und Trigger auf Abonnenten, kopiert der **Eigenschaften** Registerkarte der **Artikeleigenschaften - \< Artikel>** (Dialogfeld). Diese Registerkarte steht im Assistenten für neue Veröffentlichung und die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So geben Sie Schemaoptionen an  
  
1.  Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld Wählen Sie einen Artikel, und klicken Sie dann auf **Artikeleigenschaften**.  
  
2.  Wählen Sie aus, auf welche Artikel die Änderungen der Schemaoptionen angewendet werden sollen:  
  
    -   Klicken Sie auf **Eigenschaften des hervorgehobenen \< ObjectType> Artikel** zum Starten der **Artikeleigenschaften - \< ObjectName>** das Dialogfeld in diesem Dialogfeld vorgenommene Änderungen gelten nur für das Objekt, das im Objektbereich hervorgehoben ist die **Artikel** Seite.  
  
    -   Klicken Sie auf **Eigenschaften aller \< ObjectType> Artikel** zum Starten der **Eigenschaften für alle \< ObjectType> Artikel** das Dialogfeld in diesem Dialogfeld vorgenommene Änderungen gelten für alle Objekte dieses Typs im Objektbereich auf der **Artikel** Seite, einschließlich Objekten, die noch nicht für die Veröffentlichung ausgewählt.  
  
        > [!NOTE]  
        >  Eigenschaftenänderungen in der **Eigenschaften für alle \< ObjectType> Artikel** Überschreiben Sie alle zuvor im Dialogfeld die **Artikeleigenschaften - \< ObjectName>** (Dialogfeld). Wenn Sie beispielsweise sowohl mehrere Standardwerte für alle Artikel eines Objekttyps als auch bestimmte Eigenschaften für einzelne Objekte festlegen möchten, legen Sie zuerst die Standardwerte für alle Artikel fest. Legen Sie anschließend die Eigenschaften für die einzelnen Objekte fest.  
  
3.  In der **Kopieren von Objekten und Einstellungen auf den Abonnenten** und **Zielobjekt** Abschnitte der **Eigenschaften** Registerkarte der **Artikeleigenschaften - \< Artikel>** Dialogfeld geben Werte für die Optionen.  
  
4.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
5.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Schemaoptionen werden als hexadezimaler Wert, der angegeben, dass die [| (Bitweises OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) Ergebnis der eine oder mehrere Optionen. Weitere Informationen finden Sie unter [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) und [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).  
  
> [!NOTE]  
>  Sie müssen Schemaoptionswerte vor dem Ausführen eines bitweisen Vorgangs von **binary** in **int** konvertieren. Weitere Informationen finden Sie unter [CAST und CONVERT & #40; Transact-SQL & #41;](../../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
#### So geben Sie Schemaoptionen an, wenn Sie einen Artikel für eine Momentaufnahme- oder Transaktionsveröffentlichung definieren  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel, für die gehört **@publication**, einen Namen für den Artikel für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, den Typ des Datenbankobjekts für **@type**, und die [| (Bitweises OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) Ergebnis des einen oder mehrere Schemaoptionen für **@schema_option**. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### So geben Sie Schemaoptionen an, wenn Sie einen Artikel für eine Mergeveröffentlichung definieren  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel, für die gehört **@publication**, einen Namen für den Artikel für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, und die [| (Bitweises OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) Ergebnis des einen oder mehrere Schemaoptionen für **@schema_option**. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### So ändern Sie Schemaoptionen für einen Artikel in einer Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication** und den Namen des Artikels für **@article**an. Beachten Sie den Wert der **Schema_option** Spalte im Resultset.  
  
2.  Führen Sie eine [& (bitweises AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) -Vorgang mit dem Wert aus Schritt 1 und dem gewünschten Schema option Wert bestimmt, ob die Option festgelegt ist.  
  
    -   Wenn das Ergebnis **0**ist, ist die Option nicht festgelegt.  
  
    -   Wenn das Ergebnis der Optionswert ist, ist die Option bereits festgelegt.  
  
3.  Wenn die Option nicht festgelegt ist, führen Sie eine [| (Bitweises OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) der Vorgang mit dem Wert aus Schritt 1 und den Wert der gewünschten Option.  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel, für die gehört **@publication**, den Namen des Artikels für **@article**, ein Wert von **Schema_option** für **@property**, und das hexadezimale Ergebnis aus Schritt 3 für **@value**.  
  
5.  Führen Sie den Momentaufnahme-Agent zum Generieren einer neuen Momentaufnahme aus. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
#### So ändern Sie Schemaoptionen für einen vorhandenen Artikel in einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication** und den Namen des Artikels für **@article**an. Beachten Sie den Wert der **Schema_option** Spalte im Resultset.  
  
2.  Führen Sie eine [& (bitweises AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) -Vorgang mit dem Wert aus Schritt 1 und dem gewünschten Schema option Wert bestimmt, ob die Option festgelegt ist.  
  
    -   Wenn das Ergebnis **0**ist, ist die Option nicht festgelegt.  
  
    -   Wenn das Ergebnis der Optionswert ist, ist die Option bereits festgelegt.  
  
3.  Wenn die Option nicht festgelegt ist, führen Sie eine [| (Bitweises OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) der Vorgang mit dem Wert aus Schritt 1 und den Wert der gewünschten Option.  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel, für die gehört **@publication**, den Namen des Artikels für **@article**, ein Wert von **Schema_option** für **@property**, und das hexadezimale Ergebnis aus Schritt 3 für **@value**.  
  
5.  Führen Sie den Momentaufnahme-Agent zum Generieren einer neuen Momentaufnahme aus. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## Siehe auch  
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Artikeloptionen für die Transaktionsreplikation](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  