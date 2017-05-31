---
title: "Festlegen der Propagierungsmethode für Datenänderungen an Transaktionsartikeln | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, propagation methods
- propagating data changes [SQL Server replication]
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2abba76ac65025fe1f2c2d23a9d5b094eafb8980
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="set-the-propagation-method-for-data-changes-to-transactional-articles"></a>Festlegen der Propagierungsmethode für Datenänderungen an Transaktionsartikeln
  In diesem Thema wird beschrieben, wie die Propagierungsmethode für Datenänderungen an Transaktionsartikeln in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]festgelegt wird.  
  
 Standardmäßig werden bei der Transaktionsreplikation an Abonnenten vorgenommene Änderungen mithilfe eines Satzes gespeicherter Prozeduren für den jeweiligen Artikel weitergegeben. Sie können diese Prozeduren durch benutzerdefinierte Prozeduren ersetzen. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So legen Sie die Propagierungsmethode für Datenänderungen an Transaktionsartikeln fest**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Gehen Sie bei der Bearbeitung der bei der Replikation generierten Momentaufnahmedateien mit Bedacht vor. Sie müssen die benutzerdefinierte Logik in den benutzerdefinierten gespeicherten Prozeduren testen und unterstützen. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] bietet keine Unterstützung für benutzerdefinierte Logik.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Geben Sie die Propagierungsmethode im Dialogfeld **Artikeleigenschaften - \<Artikel>** auf der Registerkarte **Eigenschaften** an. Diese Registerkarte steht sowohl im Assistenten für neue Veröffentlichung als auch im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** zur Verfügung. Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-the-propagation-method"></a>So geben Sie die Propagierungsmethode an  
  
1.  Wählen Sie im Assistenten für neue Veröffentlichung auf der Seite **Artikel** bzw. im Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>** eine Tabelle aus, und klicken anschließend auf **Artikeleigenschaften**.  
  
2.  Klicken Sie auf die Option **Eigenschaften des hervorgehobenen Tabelle-Artikels festlegen**.  
  
3.  Geben Sie im Dialogfeld **Artikeleigenschaften - \<Article>** auf der Registerkarte **Eigenschaften** im Abschnitt **Anweisungsübermittlung** die Propagierungsmethode für die einzelnen Vorgänge an. Verwenden Sie hierzu die Menüs **INSERT-Übermittlungsformat**, **UPDATE-Übermittlungsformat** und **DELETE-Übermittlungsformat**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Wenn Sie sich im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** befinden, klicken Sie auf **OK**, um eine Speicherung vorzunehmen und das Dialogfeld zu schließen.  
  
#### <a name="to-generate-and-use-custom-stored-procedures"></a>So generieren und verwenden Sie benutzerdefinierte Prozeduren  
  
1.  Wählen Sie im Assistenten für neue Veröffentlichung auf der Seite **Artikel** bzw. im Dialogfeld **Veröffentlichungseigenschaften – \<Veröffentlichung>** eine Tabelle aus, und klicken anschließend auf **Artikeleigenschaften**.  
  
2.  Klicken Sie auf die Option **Eigenschaften des hervorgehobenen Tabelle-Artikels festlegen**.  
  
     Wählen Sie im Dialogfeld **Artikeleigenschaften - \<Article>** auf der Registerkarte **Eigenschaften** im Abschnitt **Anweisungsübermittlung** die CALL-Syntax im Menü des entsprechenden Übermittlungsformats (**INSERT-Übermittlungsformat**, **UPDATE-Übermittlungsformat** oder **DELETE-Übermittlungsformat**) aus, und geben Sie dann den Namen der Prozedur ein, die in **gespeicherter Prozedur INSERT**, in **gespeicherter Prozedur DELETE** oder **in gespeicherter Prozedur UPDATE** verwendet werden soll. Weitere Informationen zur CALL-Syntax finden Sie im Abschnitt „Aufrufsyntax für gespeicherte Prozeduren“ in [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  Wenn Sie sich im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** befinden, klicken Sie auf **OK**, um eine Speicherung vorzunehmen und das Dialogfeld zu schließen.  
  
5.  Wenn die Momentaufnahme für die Veröffentlichung generiert wird, enthält er die Prozedur, die Sie im vorherigen Schritt angegeben haben. Von den Prozeduren wird die von Ihnen angegebene CALL-Syntax verwendet, die bei der Replikation verwendete Standardlogik ist jedoch enthalten.  
  
     Navigieren Sie nach der Momentaufnahmegenerierung zu dem Momentaufnahmeordner der Veröffentlichung, zu der dieser Artikel gehört, und suchen Sie die **.sch** -Datei, die denselben Namen wie der Artikel trägt. Öffnen Sie diese Datei im Editor oder einem anderen Text-Editor, suchen Sie den CREATE PROCEDURE-Befehl für die gespeicherte Prozedur INSERT, UPDATE oder DELETE, und bearbeiten Sie die Prozedurdefinition, um jegliche benutzerdefinierte Logik für das Propagieren von Datenänderungen bereitzustellen. Wenn die Momentaufnahme erneut generiert wird, muss die benutzerdefinierte Prozedur ebenfalls erneut erstellt werden.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Die Transaktionsreplikation ermöglicht es Ihnen zu steuern, wie Änderungen vom Verleger an die Abonnenten weitergegeben (propagiert) werden. Diese Propagierungsmethode kann bei der Erstellung eines Artikels programmgesteuert festgelegt und später anhand gespeicherter Replikationsprozeduren geändert werden.  
  
> [!NOTE]  
>  Sie können für jeden DML-Vorgangstyp (Data Manipulation Language, Datenbearbeitungssprache), der auf einer Zeile veröffentlichter Daten vorkommt (Einfügen, Aktualisieren oder Löschen), eine andere Propagierungsmethode angeben.  
  
 Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-create-an-article-that-uses-transact-sql-commands-to-propagate-data-changes"></a>So erstellen Sie einen Artikel, der Transact-SQL-Befehle verwendet, um Datenänderungen weiterzugeben  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication**, den Namen des Artikels für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**und den Wert **SQL** für wenigstens einen der folgenden Parameter an:  
  
    -   **@ins_cmd** &ndash; steuert die Replikation von [INSERT](../../../t-sql/statements/insert-transact-sql.md) -Befehlen.  
  
    -   **@upd_cmd** &ndash; steuert die Replikation von [UPDATE](../../../t-sql/queries/update-transact-sql.md) -Befehlen.  
  
    -   **@del_cmd** &ndash; steuert die Replikation von [DELETE](../../../t-sql/statements/delete-transact-sql.md) -Befehlen.  
  
    > [!NOTE]  
    >  Wenn Sie den Wert **SQL** für einen der obigen Parameter angeben, werden die Befehle des betreffenden Typs auf den Abonnenten als entsprechende [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Befehle repliziert.  
  
     Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-create-an-article-that-does-not-propagate-data-changes"></a>So erstellen Sie einen Artikel, der keine Datenänderungen weitergibt  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication**, den Namen des Artikels für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**und den Wert **NONE** für wenigstens einen der folgenden Parameter an:  
  
    -   **@ins_cmd** &ndash; steuert die Replikation von [INSERT](../../../t-sql/statements/insert-transact-sql.md) -Befehlen.  
  
    -   **@upd_cmd** &ndash; steuert die Replikation von [UPDATE](../../../t-sql/queries/update-transact-sql.md) -Befehlen.  
  
    -   **@del_cmd** &ndash; steuert die Replikation von [DELETE](../../../t-sql/statements/delete-transact-sql.md) -Befehlen.  
  
    > [!NOTE]  
    >  Wenn Sie den Wert **NONE** für einen der obigen Parameter angeben, werden die Befehle des betreffenden Typs auf den Abonnenten nicht repliziert.  
  
     Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-create-an-article-with-user-modified-custom-stored-procedures"></a>So erstellen Sie einen Artikel mit benutzerdefinierten gespeicherten Prozeduren  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication**, den Namen des Artikels für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, einen Wert für die **@schema_option** -Bitmaske, der den Wert **0x02** enthält (aktiviert die automatische Erstellung benutzerdefinierter gespeicherter Prozeduren), und wenigstens einen der folgenden Parameter an:  
  
    -   **@ins_cmd**: Geben Sie einen Wert für **CALL sp_MSins_*article_name*** an, wobei ***article_name*** der für **@article** festgelegte Wert ist.  
  
    -   **@del_cmd**: Geben Sie einen Wert für **CALL sp_MSdel_*article_name*** oder **XCALL sp_MSdel_*article_name*** an, wobei ***article_name*** der für **@article** angegebene Wert ist.  
  
    -   **@upd_cmd**: Geben Sie einen Wert für **SCALL sp_MSupd_*article_name***, **CALL sp_MSupd_*article_name***, **XCALL sp_MSupd_*article_name***, oder **MCALL sp_MSupd_*article_name*** an, wobei ***article_name*** der für **@article** angegebene Wert ist.  
  
    > [!NOTE]  
    >  Für jeden der obigen Befehlsparameter gilt: Sie können einen selbst gewählten Namen für die gespeicherten Prozeduren angeben, die von der Replikation generiert werden.  
  
    > [!NOTE]  
    >  Weitere Informationen über die CALL, SCALL, XCALL und MCALL-Syntax finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
     Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Navigieren Sie nach der Momentaufnahmegenerierung zu dem Momentaufnahmeordner der Veröffentlichung, zu der dieser Artikel gehört, und suchen Sie die **.sch** -Datei, die denselben Namen wie der Artikel trägt. Öffnen Sie diese Datei mit Notepad.exe, suchen Sie den CREATE PROCEDURE-Befehl für die gespeicherte Prozedur INSERT, UPDATE oder DELETE, und bearbeiten Sie die Prozedurdefinition, um eine benutzerdefinierte Logik für die Propagierung von Datenänderungen bereitzustellen. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-create-an-article-with-custom-scripting-in-the-custom-stored-procedures-to-propagate-data-changes"></a>So erstellen Sie einen Artikel mit benutzerdefinierter Skriptprozedur in den benutzerdefinierten gespeicherten Prozeduren, um Datenänderungen weiterzugeben  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)aus. Geben Sie den Namen der Veröffentlichung, zu der der Artikel gehört, für **@publication**, den Namen des Artikels für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, einen Wert für die **@schema_option** -Bitmaske, der den Wert **0x02** enthält (aktiviert die automatische Erstellung benutzerdefinierter gespeicherter Prozeduren), und wenigstens einen der folgenden Parameter an:  
  
    -   **@ins_cmd**: Geben Sie einen Wert für **CALL sp_MSins_*article_name*** an, wobei ***article_name*** der für **@article** festgelegte Wert ist.  
  
    -   **@del_cmd**: Geben Sie einen Wert für **CALL sp_MSdel_*article_name*** oder **XCALL sp_MSdel_*article_name*** an, wobei ***article_name*** der für **@article** angegebene Wert ist.  
  
    -   **@upd_cmd**: Geben Sie einen Wert für **SCALL sp_MSupd_*article_name***, **CALL sp_MSupd_*article_name***, **XCALL sp_MSupd_*article_name***, **MCALL sp_MSupd_*article_name*** an, wobei ***article_name*** der für **@article** angegebene Wert ist.  
  
    > [!NOTE]  
    >  Für jeden der obigen Befehlsparameter gilt: Sie können einen selbst gewählten Namen für die gespeicherten Prozeduren angeben, die von der Replikation generiert werden.  
  
    > [!NOTE]  
    >  Weitere Informationen über die CALL, SCALL, XCALL und MCALL-Syntax finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
     Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Verwenden Sie auf dem Verleger für die Veröffentlichungsdatenbank die [ALTER PROCEDURE](../../../t-sql/statements/alter-procedure-transact-sql.md) -Anweisung, um [sp_scriptpublicationcustomprocs](../../../relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql.md) so zu bearbeiten, dass ein [CREATE PROCEDURE](../../../t-sql/statements/create-procedure-transact-sql.md) -Skript für die benutzerdefinierten, gespeicherten Prozeduren INSERT, UPDATE und DELETE zurückgegeben wird. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-change-the-method-of-propagating-changes-for-an-existing-article"></a>So ändern Sie die Methode zur Weitergabe von Änderungen an einen vorhandenen Artikel  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)aus. Geben Sie **@publication**, **@article**, den Wert **ins_cmd**, **upd_cmd**bzw. **del_cmd** für **@property**und die entsprechende Propagierungsmethode für **@value**festgelegt wird.  
  
2.  Wiederholen Sie Schritt 1 für jede Propagierungsmethode, die geändert werden soll.  
  
## <a name="see-also"></a>Siehe auch  
 [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [Erstellen, Ändern und Löschen von Veröffentlichungen und Artikeln &#40;Replikation&#41;](../../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)  
  
  
