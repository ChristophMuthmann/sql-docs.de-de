---
title: "Festlegen der Propagierungsmethode f&#252;r Daten&#228;nderungen an Transaktionsartikeln | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Transaktionsreplikation, Propagierungsmethoden"
  - "Propagieren von Datenänderungen [SQL Server-Replikation]"
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Festlegen der Propagierungsmethode f&#252;r Daten&#228;nderungen an Transaktionsartikeln
  In diesem Thema wird beschrieben, wie die Propagierungsmethode für Datenänderungen an Transaktionsartikeln in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]festgelegt wird.  
  
 Standardmäßig werden bei der Transaktionsreplikation an Abonnenten vorgenommene Änderungen mithilfe eines Satzes gespeicherter Prozeduren für den jeweiligen Artikel weitergegeben. Sie können diese Prozeduren durch benutzerdefinierte Prozeduren ersetzen. Weitere Informationen finden Sie unter [angeben, wie Änderungen für Transaktionsartikel weitergegeben werden](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So legen Sie die Propagierungsmethode für Datenänderungen an Transaktionsartikeln fest**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Gehen Sie bei der Bearbeitung der bei der Replikation generierten Momentaufnahmedateien mit Bedacht vor. Sie müssen die benutzerdefinierte Logik in den benutzerdefinierten gespeicherten Prozeduren testen und unterstützen. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] bietet keine Unterstützung für benutzerdefinierte Logik.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Geben Sie die propagierungsmethode für die **Eigenschaften** Registerkarte der **Artikeleigenschaften - \< Artikel>** Dialogfeld, das im Assistenten für neue Veröffentlichung verfügbar ist und die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So geben Sie die Propagierungsmethode an  
  
1.  Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld Wählen Sie eine Tabelle, und klicken Sie dann auf **Artikeleigenschaften**.  
  
2.  Klicken Sie auf die Option **Eigenschaften des hervorgehobenen Tabelle-Artikels festlegen**.  
  
3.  Auf der **Eigenschaften** Registerkarte der **Artikeleigenschaften - \< Artikel>** im Feld der **Anweisungsübermittlung** an, die propagierungsmethode für jeden Vorgang mit der **INSERT-übermittlungsformat**, **UPDATE-übermittlungsformat**, und **DELETE-übermittlungsformat** Menüs.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
#### So generieren und verwenden Sie benutzerdefinierte Prozeduren  
  
1.  Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld Wählen Sie eine Tabelle, und klicken Sie dann auf **Artikeleigenschaften**.  
  
2.  Klicken Sie auf die Option **Eigenschaften des hervorgehobenen Tabelle-Artikels festlegen**.  
  
     Auf der **Eigenschaften** auf der Registerkarte der **Artikeleigenschaften - \< Artikel>** im Feld der **Anweisungsübermittlung** aktivieren die CALL-Syntax im Menü Format die entsprechenden Übermittlung (**INSERT-übermittlungsformat**, **UPDATE-übermittlungsformat**, oder **DELETE-übermittlungsformat**), und geben Sie den Namen der Prozedur zur Verwendung in **Einfügen gespeicherte Prozedur**, **Löschen gespeicherter Prozedur**, oder **UPDATE gespeicherte Prozedur**. Weitere Informationen zur CALL-Syntax finden Sie im Abschnitt "Aufrufsyntax für gespeicherte Prozeduren" in [angeben, wie Änderungen für Transaktionsartikel weitergegeben werden](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
5.  Wenn die Momentaufnahme für die Veröffentlichung generiert wird, enthält er die Prozedur, die Sie im vorherigen Schritt angegeben haben. Von den Prozeduren wird die von Ihnen angegebene CALL-Syntax verwendet, die bei der Replikation verwendete Standardlogik ist jedoch enthalten.  
  
     Navigieren Sie nach der Momentaufnahmegenerierung zu dem Momentaufnahmeordner der Veröffentlichung, zu der dieser Artikel gehört, und suchen Sie die **.sch** -Datei, die denselben Namen wie der Artikel trägt. Öffnen Sie diese Datei im Editor oder einem anderen Text-Editor, suchen Sie den CREATE PROCEDURE-Befehl für die gespeicherte Prozedur INSERT, UPDATE oder DELETE, und bearbeiten Sie die Prozedurdefinition, um jegliche benutzerdefinierte Logik für das Propagieren von Datenänderungen bereitzustellen. Wenn die Momentaufnahme erneut generiert wird, muss die benutzerdefinierte Prozedur ebenfalls erneut erstellt werden.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Die Transaktionsreplikation ermöglicht es Ihnen zu steuern, wie Änderungen vom Verleger an die Abonnenten weitergegeben (propagiert) werden. Diese Propagierungsmethode kann bei der Erstellung eines Artikels programmgesteuert festgelegt und später anhand gespeicherter Replikationsprozeduren geändert werden.  
  
> [!NOTE]  
>  Sie können für jeden DML-Vorgangstyp (Data Manipulation Language, Datenbearbeitungssprache), der auf einer Zeile veröffentlichter Daten vorkommt (Einfügen, Aktualisieren oder Löschen), eine andere Propagierungsmethode angeben.  
  
 Weitere Informationen finden Sie unter [angeben, wie Änderungen für Transaktionsartikel weitergegeben werden](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### So erstellen Sie einen Artikel, der Transact-SQL-Befehle verwendet, um Datenänderungen weiterzugeben  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel, für die gehört **@publication**, einen Namen für den Artikel für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, und der Wert **SQL** für mindestens eine der folgenden Parameter:  
  
    -   **@ins_cmd** -steuert die Replikation von [Einfügen](../../../t-sql/statements/insert-transact-sql.md) Befehle.  
  
    -   **@upd_cmd** -steuert die Replikation von [UPDATE](../../../t-sql/queries/update-transact-sql.md) Befehle.  
  
    -   **@del_cmd** -steuert die Replikation von [Löschen](../../../t-sql/statements/delete-transact-sql.md) Befehle.  
  
    > [!NOTE]  
    >  Bei Angabe des Werts **SQL** für eines der oben genannten Parameter Befehle des betreffenden Typs auf den Abonnenten als entsprechende repliziert [!INCLUDE[tsql](../../../includes/tsql-md.md)] Befehl.  
  
     Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### So erstellen Sie einen Artikel, der keine Datenänderungen weitergibt  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel, für die gehört **@publication**, einen Namen für den Artikel für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, und der Wert **NONE** für mindestens eine der folgenden Parameter:  
  
    -   **@ins_cmd** -steuert die Replikation von [Einfügen](../../../t-sql/statements/insert-transact-sql.md) Befehle.  
  
    -   **@upd_cmd** -steuert die Replikation von [UPDATE](../../../t-sql/queries/update-transact-sql.md) Befehle.  
  
    -   **@del_cmd** -steuert die Replikation von [Löschen](../../../t-sql/statements/delete-transact-sql.md) Befehle.  
  
    > [!NOTE]  
    >  Bei Angabe des Werts **NONE** für eines der oben genannten Parameter werden Befehle des betreffenden Typs nicht auf den Abonnenten repliziert werden.  
  
     Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### So erstellen Sie einen Artikel mit benutzerdefinierten gespeicherten Prozeduren  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel, für die gehört **@publication**, einen Namen für den Artikel für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, einen Wert für die **@schema_option** Bitmaske mit dem Wert **0 x 02** (ermöglicht die automatische Generierung von benutzerdefinierten gespeicherten Prozeduren), und mindestens eine der folgenden Parameter:  
  
    -   **@ins_cmd** -Geben Sie den Wert **CALL Sp_MSins_*Article_name***, wobei ***Article_name*** ist der angegebene Wert für **@article**.  
  
    -   **@del_cmd** -Geben Sie den Wert **CALL Sp_MSdel_*Article_name*** oder **XCALL Sp_MSdel_*Article_name***, wobei ***Article_name*** ist der angegebene Wert für **@article**.  
  
    -   **@upd_cmd** -Geben Sie den Wert **SCALL Sp_MSupd_*Article_name***, **CALL Sp_MSupd_*Article_name***, **XCALL Sp_MSupd_*Article_name***, oder **MCALL Sp_MSupd_*Article_name***, wobei ***Article_name*** ist der angegebene Wert für **@article**.  
  
    > [!NOTE]  
    >  Für jeden der obigen Befehlsparameter gilt: Sie können einen selbst gewählten Namen für die gespeicherten Prozeduren angeben, die von der Replikation generiert werden.  
  
    > [!NOTE]  
    >  Weitere Informationen über die CALL, SCALL, XCALL und MCALL-Syntax finden Sie unter [angeben, wie Änderungen für Transaktionsartikel weitergegeben werden](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
     Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Navigieren Sie nach der Momentaufnahmegenerierung zu dem Momentaufnahmeordner der Veröffentlichung, zu der dieser Artikel gehört, und suchen Sie die **.sch** -Datei, die denselben Namen wie der Artikel trägt. Öffnen Sie diese Datei mit Notepad.exe, suchen Sie den CREATE PROCEDURE-Befehl für die gespeicherte Prozedur INSERT, UPDATE oder DELETE, und bearbeiten Sie die Prozedurdefinition, um eine benutzerdefinierte Logik für die Propagierung von Datenänderungen bereitzustellen. Weitere Informationen finden Sie unter [angeben, wie Änderungen für Transaktionsartikel weitergegeben werden](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### So erstellen Sie einen Artikel mit benutzerdefinierter Skriptprozedur in den benutzerdefinierten gespeicherten Prozeduren, um Datenänderungen weiterzugeben  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie den Namen der Veröffentlichung, zu der der Artikel, für die gehört **@publication**, einen Namen für den Artikel für **@article**, das Datenbankobjekt, das veröffentlicht wird, für **@source_object**, einen Wert für die **@schema_option** Bitmaske mit dem Wert **0 x 02** (ermöglicht die automatische Generierung von benutzerdefinierten gespeicherten Prozeduren), und mindestens eine der folgenden Parameter:  
  
    -   **@ins_cmd** -Geben Sie den Wert **CALL Sp_MSins_*Article_name***, wobei ***Article_name*** ist der angegebene Wert für **@article**.  
  
    -   **@del_cmd** -Geben Sie den Wert **CALL Sp_MSdel_*Article_name*** oder **XCALL Sp_MSdel_*Article_name***, wobei ***Article_name*** ist der angegebene Wert für **@article**.  
  
    -   **@upd_cmd** -Geben Sie den Wert **SCALL Sp_MSupd_*Article_name***, **CALL Sp_MSupd_*Article_name***, **XCALL Sp_MSupd_*Article_name***, **MCALL Sp_MSupd_*Article_name***, wobei ***Article_name*** ist der angegebene Wert für **@article**.  
  
    > [!NOTE]  
    >  Für jeden der obigen Befehlsparameter gilt: Sie können einen selbst gewählten Namen für die gespeicherten Prozeduren angeben, die von der Replikation generiert werden.  
  
    > [!NOTE]  
    >  Weitere Informationen über die CALL, SCALL, XCALL und MCALL-Syntax finden Sie unter [angeben, wie Änderungen für Transaktionsartikel weitergegeben werden](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
     Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Verwenden Sie auf dem Verleger für die Veröffentlichungsdatenbank die [ALTER PROCEDURE](../../../t-sql/statements/alter-procedure-transact-sql.md) -Anweisung bearbeiten [Sp_scriptpublicationcustomprocs](../../../relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql.md) damit es gibt eine [CREATE PROCEDURE](../../../t-sql/statements/create-procedure-transact-sql.md) Skript zum Einfügen, aktualisieren und Löschen von benutzerdefinierten gespeicherten Prozeduren. Weitere Informationen finden Sie unter [angeben, wie Änderungen für Transaktionsartikel weitergegeben werden](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### So ändern Sie die Methode zur Weitergabe von Änderungen an einen vorhandenen Artikel  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Geben Sie **@publication**, **@article**, ein Wert von **Ins_cmd**, **Upd_cmd**, oder **Del_cmd** für **@property**, und die entsprechende propagierungsmethode für **@value**.  
  
2.  Wiederholen Sie Schritt 1 für jede Propagierungsmethode, die geändert werden soll.  
  
## Siehe auch  
 [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [Erstellen, ändern und Löschen von Publikationen und Artikeln & #40; Replikation & #41;](../../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)  
  
  