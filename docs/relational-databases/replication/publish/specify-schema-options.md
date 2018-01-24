---
title: Angeben von Schemaoptionen | Microsoft Dokumentation
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
- schemas [SQL Server replication], options
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- articles [SQL Server replication], schema options
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
caps.latest.revision: "39"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e90de846e7d7dddc6ded2eac73f6aea9b1cf8c6
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="specify-schema-options"></a>Angeben von Schemaoptionen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Schemaoptionen in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)] festgelegt werden. Beim Veröffentlichen einer Tabelle oder einer Sicht können Sie die Objekterstellungsoptionen steuern, die für das veröffentlichte Objekt repliziert werden. Sie können diesen Option festlegen, wenn der Artikel erstellt wird, und auch zu einem späteren Zeitpunkt ändern. Wenn Sie diese Optionen für einen Artikel nicht explizit festlegen, wird eine Standardgruppe von Optionen definiert.  
  
> [!NOTE]  
>  Die Standardschemaoptionen bei der Verwendung von gespeicherten Replikationsprozeduren können sich von den Standardoptionen unterscheiden, wenn Artikel mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]hinzugefügt werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
-   **So geben Sie Schemaoptionen an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie Schemaoptionen ändern, nachdem eine Veröffentlichung erstellt wurde, müssen Sie eine neue Momentaufnahme generieren.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Die vollständige Liste der Schemaoptionen finden Sie im Parameter **@schema_option** von [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) und [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 Auf der Registerkarte **Eigenschaften** im Dialogfeld **Artikeleigenschaften - \<Artikel>** können Sie Schemaoptionen angeben, beispielsweise, ob Einschränkungen und Trigger auf Abonnenten kopiert werden sollen. Diese Registerkarte ist im Assistenten für neue Veröffentlichung sowie über das Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** verfügbar. Weitere Informationen zum Verwenden des Assistenten sowie zum Zugriff auf das Dialogfeld finden Sie unter [Eine Veröffentlichung erstellen](../../../relational-databases/replication/publish/create-a-publication.md) und [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-schema-options"></a>So geben Sie Schemaoptionen an  
  
1.  Wählen Sie im Assistenten für neue Veröffentlichung auf der Seite **Artikel** bzw. im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** einen Artikel aus, und klicken anschließend auf **Artikeleigenschaften**.  
  
2.  Wählen Sie aus, auf welche Artikel die Änderungen der Schemaoptionen angewendet werden sollen:  
  
    -   Klicken Sie auf **Eigenschaften des hervorgehobenen \<ObjectType>-Artikels festlegen**, um das Dialogfeld **Artikeleigenschaften - \<ObjectName>** zu starten. Die in diesem Dialogfeld vorgenommenen Änderungen werden nur auf das Objekt angewendet, das im Objektbereich auf der Seite **Artikel** markiert ist.  
  
    -   Klicken Sie auf **Eigenschaften aller \<ObjectType>-Artikel** festlegen, um das Dialogfeld **Eigenschaften für alle \<ObjectType>-Artikel** zu starten. Die in diesem Dialogfeld vorgenommenen Änderungen werden auf alle Objekte dieses Typs angewendet, die im Objektbereich auf der Seite **Artikel** vorhanden sind, einschließlich jener Objekte, die noch nicht für die Veröffentlichung ausgewählt wurden.  
  
        > [!NOTE]  
        >  Durch die Änderungen im Dialogfeld **Eigenschaften für alle \<ObjectType>-Artikel**, werden alle zuvor im Dialogfeld **Artikeleigenschaften - \<ObjectName>** vorgenommenen Änderungen überschrieben. Wenn Sie beispielsweise sowohl mehrere Standardwerte für alle Artikel eines Objekttyps als auch bestimmte Eigenschaften für einzelne Objekte festlegen möchten, legen Sie zuerst die Standardwerte für alle Artikel fest. Legen Sie anschließend die Eigenschaften für die einzelnen Objekte fest.  
  
3.  In den Abschnitten **Objekte und Einstellungen auf den Abonnenten kopieren** und **Zielobjekt** der Registerkarte **Eigenschaften** im Dialogfeld **Artikeleigenschaften - \<Artikel>** können Sie Werte für die Optionen angeben.  
  
4.  Ändern Sie die Eigenschaften nach Bedarf, und klicken Sie dann auf **OK**.  
  
5.  Wenn Sie sich im Dialogfeld **Veröffentlichungseigenschaften.-.\<Veröffentlichung>** befinden, klicken Sie auf **OK**, um zu speichern und das Dialogfeld zu schließen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Schemaoptionen werden als hexadezimaler Wert angegeben, der das [| (Bitweise OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) -Ergebnis einer oder mehrerer Optionen ist. Weitere Informationen finden Sie unter [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) und [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).  
  
> [!NOTE]  
>  Sie müssen Schemaoptionswerte vor dem Ausführen eines bitweisen Vorgangs von **binary** in **int** konvertieren. Weitere Informationen finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>So geben Sie Schemaoptionen an, wenn Sie einen Artikel für eine Momentaufnahme- oder Transaktionsveröffentlichung definieren  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication**, den Namen des Artikels für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, den Typ des Datenbankobjekts für **@type**und das [| (Bitweise OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) -Ergebnis mindestens einer Schemaoption für **@schema_option**festgelegt werden. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>So geben Sie Schemaoptionen an, wenn Sie einen Artikel für eine Mergeveröffentlichung definieren  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication**, den Namen des Artikels für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**und das [| (Bitweise OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) -Ergebnis mindestens einer Schemaoption für **@schema_option**festgelegt werden. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>So ändern Sie Schemaoptionen für einen Artikel in einer Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication** und den Namen des Artikels für **@article**festgelegt werden. Notieren Sie den Wert der **schema_option** -Spalte im Resultset.  
  
2.  Führen Sie einen [& (Bitweise AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md)-Vorgang mit dem Wert aus Schritt 1 und dem gewünschten Wert für die Schemaoption aus, um festzustellen, ob die Option festgelegt ist.  
  
    -   Wenn das Ergebnis **0**ist, ist die Option nicht festgelegt.  
  
    -   Wenn das Ergebnis der Optionswert ist, ist die Option bereits festgelegt.  
  
3.  Wenn die Option nicht festgelegt ist, führen Sie einen [| (Bitweisen OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) -Vorgang mit dem Wert aus Schritt 1 und dem gewünschten Wert für die Schemaoption aus.  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication**, den Namen des Artikels für **@article**, den Wert **schema_option** für **@property**und das hexadezimale Ergebnis aus Schritt 3 für **@value**festgelegt werden.  
  
5.  Führen Sie den Momentaufnahme-Agent zum Generieren einer neuen Momentaufnahme aus. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>So ändern Sie Schemaoptionen für einen vorhandenen Artikel in einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication** und den Namen des Artikels für **@article**festgelegt werden. Notieren Sie den Wert der **schema_option** -Spalte im Resultset.  
  
2.  Führen Sie einen [& (Bitweise AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md)-Vorgang mit dem Wert aus Schritt 1 und dem gewünschten Wert für die Schemaoption aus, um festzustellen, ob die Option festgelegt ist.  
  
    -   Wenn das Ergebnis **0**ist, ist die Option nicht festgelegt.  
  
    -   Wenn das Ergebnis der Optionswert ist, ist die Option bereits festgelegt.  
  
3.  Wenn die Option nicht festgelegt ist, führen Sie einen [| (Bitweisen OR)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) -Vorgang mit dem Wert aus Schritt 1 und dem gewünschten Wert für die Schemaoption aus.  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication**, den Namen des Artikels für **@article**, den Wert **schema_option** für **@property**und das hexadezimale Ergebnis aus Schritt 3 für **@value**festgelegt werden.  
  
5.  Führen Sie den Momentaufnahme-Agent zum Generieren einer neuen Momentaufnahme aus. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Artikeloptionen für die Transaktionsreplikation](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
