---
title: "Überprüfen von Daten auf dem Abonnenten | Microsoft-Dokumentation"
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
- Subscribers [SQL Server replication], data validation
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication], SQL Server Management Studio
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fcd9d7f9e729a1d2ebb7cc876ce3807aa839f079
ms.lasthandoff: 04/11/2017

---
# <a name="validate-data-at-the-subscriber"></a>Überprüfen der Daten am Abonnenten
  In diesem Thema wird beschrieben, wie Daten beim Abonnenten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekten (RMO) überprüft werden.  
  
 Der Prozess der Datenüberprüfung besteht aus drei Teilen:  
  
1.  Zunächst müssen die Abonnements für eine Veröffentlichung, die überprüft werden sollen, *gekennzeichnet* werden. Mark subscriptions for validation in the **Validate Subscription**, **Validate Subscriptions**, and **Validate All Subscriptions** dialog boxes, which are available from the **Local Publications** folder and the **Local Subscriptions** folder in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Abonnements können darüber hinaus auch auf der Registerkarte **Alle Abonnements** , auf der Registerkarte **Überwachungsliste für Abonnements** und über den Veröffentlichungsknoten im Replikationsmonitor gekennzeichnet werden. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
2.  Ein Abonnement wird bei der nächsten Synchronisierung durch den Verteilungs-Agent (für Transaktionsreplikationen) oder durch den Merge-Agent (für Mergereplikationen) überprüft. Der Verteilungs-Agent wird in der Regel kontinuierlich ausgeführt. In diesem Fall erfolgt die Überprüfung sofort. Der Merge-Agent wird in der Regel bei Bedarf ausgeführt, und die Überprüfung erfolgt nach der Ausführung des Agents.  
  
3.  Anzeigen der Überprüfungsergebnisse:  
  
    -   In den Detailfenstern im Replikationsmonitor auf der Registerkarte **Verlauf Verteiler zu Abonnent** für die Transaktionsreplikation und auf der Registerkarte **Synchronisierungsverlauf** für die Mergereplikation.  
  
    -   Im Dialogfeld **Synchronisierungsstatus anzeigen** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So prüfen Sie Daten beim Abonnenten mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die Prozeduren für den Replikationsmonitor sind nur für Pushabonnements geeignet, da Pullabonnements im Replikationsmonitor nicht synchronisiert werden können. Sie können ein Abonnement jedoch für die Überprüfung markieren und die Überprüfungsergebnisse für Pullabonnements im Replikationsmonitor anzeigen.  
  
-   In den Überprüfungsergebnissen wird angezeigt, ob die Überprüfung erfolgreich war oder fehlgeschlagen ist, es wird jedoch nicht angegeben, in welchen Zeilen die Überprüfung beim Auftreten eines Fehlers fehlgeschlagen ist. Verwenden Sie das Hilfsprogramm [tablediff Utility](../../tools/tablediff-utility.md), um die Daten auf dem Verleger und auf dem Abonnenten zu vergleichen. Informationen zum Verwenden dieses Hilfsprogramms finden Sie unter [Überprüfen replizierter Tabellen auf Unterschiede &#40;Replikationsprogrammierung&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-validate-data-for-subscriptions-to-a-transactional-publication-management-studio"></a>So überprüfen Sie Daten für Abonnements einer Transaktionsveröffentlichung (Management Studio)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Veröffentlichung, deren Abonnements Sie überprüfen möchten, und klicken Sie dann auf **Abonnements überprüfen**.  
  
4.  Wählen Sie im Dialogfeld **Abonnements überprüfen** die zu überprüfenden Abonnements aus:  
  
    -   Wählen Sie **Alle SQL Server-Abonnements überprüfen**aus.  
  
    -   Wählen Sie **Folgende Abonnements überprüfen**aus, und wählen Sie dann ein oder mehrere Abonnements aus.  
  
5.  Um den Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme) anzugeben, klicken Sie auf **Überprüfungsoptionen**, und geben Sie dann im Dialogfeld **Optionen für die Abonnementüberprüfung** die gewünschten Optionen an.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Zeigen Sie die Überprüfungsergebnisse Im Replikationsmonitor oder im Dialogfeld **Synchronisierungsstatus anzeigen** an: Führen Sie für jedes Abonnement folgende Vorgänge aus:  
  
    1.  Erweitern Sie die Veröffentlichung, klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
    2.  Wenn der Agent nicht ausgeführt wird, klicken Sie im Dialogfeld **Synchronisierungsstatus anzeigen** auf **Start** . Im Dialogfeld werden Meldungen mit Informationen zur Überprüfung angezeigt.  
  
     Wenn keine Meldungen bezüglich der Überprüfung angezeigt werden, hat der Agent bereits eine nachfolgende Meldung protokolliert. Zeigen Sie die Überprüfungsergebnisse in diesem Fall im Replikationsmonitor an. Weitere Informationen finden Sie in den Prozeduren zu den Verfahrensweisen im Replikationsmonitor in diesem Thema.  
  
#### <a name="to-validate-data-for-a-single-subscription-to-a-merge-publication-management-studio"></a>So überprüfen Sie Daten für ein einzelnes Abonnement für eine Mergeveröffentlichung (Management Studio)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die Veröffentlichung, für die Sie Abonnements überprüfen möchten, klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Abonnement überprüfen**.  
  
4.  Wählen Sie im Dialogfeld **Abonnement überprüfen** die Option **Dieses Abonnement überprüfen**aus.  
  
5.  Um den Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme) anzugeben, klicken Sie auf **Optionen**, und geben Sie dann im Dialogfeld **Optionen für die Abonnementüberprüfung** die gewünschten Optionen an.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Zeigen Sie die Überprüfungsergebnisse Im Replikationsmonitor oder im Dialogfeld **Synchronisierungsstatus anzeigen** an:  
  
    1.  Erweitern Sie die Veröffentlichung, klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
    2.  Wenn der Agent nicht ausgeführt wird, klicken Sie im Dialogfeld **Synchronisierungsstatus anzeigen** auf **Start** . Im Dialogfeld werden Meldungen mit Informationen zur Überprüfung angezeigt.  
  
     Wenn keine Meldungen bezüglich der Überprüfung angezeigt werden, hat der Agent bereits eine nachfolgende Meldung protokolliert. Zeigen Sie die Überprüfungsergebnisse in diesem Fall im Replikationsmonitor an. Weitere Informationen finden Sie in den Prozeduren zu den Verfahrensweisen im Replikationsmonitor in diesem Thema.  
  
#### <a name="to-validate-data-for-all-subscriptions-to-a-merge-publication-management-studio"></a>So überprüfen Sie Daten für Abonnements einer Mergeveröffentlichung (Management Studio)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Veröffentlichung, deren Abonnements Sie überprüfen möchten, und klicken Sie dann auf **Alle Abonnements überprüfen**.  
  
4.  Geben Sie im Dialogfeld **Alle Abonnements überprüfen** den Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme) an.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Zeigen Sie die Überprüfungsergebnisse Im Replikationsmonitor oder im Dialogfeld **Synchronisierungsstatus anzeigen** an: Führen Sie für jedes Abonnement folgende Vorgänge aus:  
  
    1.  Erweitern Sie die Veröffentlichung, klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
    2.  Wenn der Agent nicht ausgeführt wird, klicken Sie im Dialogfeld **Synchronisierungsstatus anzeigen** auf **Start** . Im Dialogfeld werden Meldungen mit Informationen zur Überprüfung angezeigt.  
  
     Wenn keine Meldungen bezüglich der Überprüfung angezeigt werden, hat der Agent bereits eine nachfolgende Meldung protokolliert. Zeigen Sie die Überprüfungsergebnisse in diesem Fall im Replikationsmonitor an. Weitere Informationen finden Sie in den Prozeduren zu den Verfahrensweisen im Replikationsmonitor in diesem Thema.  
  
#### <a name="to-validate-data-for-all-push-subscriptions-to-a-transactional-publication-replication-monitor"></a>So überprüfen Sie die Daten aller Pushabonnements einer Transaktionsveröffentlichung (Replikationsüberwachung)  
  
1.  Erweitern Sie im Replikationsmonitor im linken Bereich eine Verlegergruppe, und erweitern Sie dann einen Verleger.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Veröffentlichung, deren Abonnements Sie überprüfen möchten, und klicken Sie dann auf **Abonnements überprüfen**.  
  
3.  Wählen Sie im Dialogfeld **Abonnements überprüfen** die zu überprüfenden Abonnements aus:  
  
    -   Wählen Sie **Alle SQL Server-Abonnements überprüfen**aus.  
  
    -   Wählen Sie **Folgende Abonnements überprüfen**aus, und wählen Sie dann ein oder mehrere Abonnements aus.  
  
4.  Um den Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme) anzugeben, klicken Sie auf **Überprüfungsoptionen**, und geben Sie dann im Dialogfeld **Optionen für die Abonnementüberprüfung** die gewünschten Optionen an.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
7.  Zeigen Sie die Überprüfungsergebnisse an. Führen Sie für jedes Pushabonnement folgende Vorgänge aus:  
  
    1.  Wenn der Agent nicht ausgeführt wird, klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Synchronisierung starten**.  
  
    2.  Klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Details anzeigen**.  
  
    3.  Zeigen Sie die Informationen auf der Registerkarte **Verlauf Verteiler zu Abonnent** im Textbereich **Aktionen in der ausgewählten Sitzung** an.  
  
#### <a name="to-validate-data-for-a-single-push-subscription-to-a-merge-publication-replication-monitor"></a>So überprüfen Sie Daten für ein einzelnes Pushabonnement für eine Mergeveröffentlichung (Replikationsmonitor)  
  
1.  Erweitern Sie im Replikationsmonitor im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
3.  Klicken Sie mit der rechten Maustaste auf das Abonnement, das Sie überprüfen möchten, und klicken Sie dann auf **Abonnement überprüfen**.  
  
4.  Wählen Sie im Dialogfeld **Abonnement überprüfen** die Option **Dieses Abonnement überprüfen**aus.  
  
5.  Um den Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme) anzugeben, klicken Sie auf **Optionen**, und geben Sie dann im Dialogfeld **Optionen für die Abonnementüberprüfung** die gewünschten Optionen an.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
8.  Zeigen Sie die Überprüfungsergebnisse an:  
  
    1.  Wenn der Agent nicht ausgeführt wird, klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Synchronisierung starten**.  
  
    2.  Klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Details anzeigen**.  
  
    3.  Zeigen Sie die Informationen auf der Registerkarte **Synchronisierungsverlauf** im Textbereich **Letzte Meldung der ausgewählten Sitzung** an.  
  
#### <a name="to-validate-data-for-all-push-subscriptions-to-a-merge-publication-replication-monitor"></a>So überprüfen Sie die Daten aller Pushabonnements einer Mergeveröffentlichung (Replikationsüberwachung)  
  
1.  Erweitern Sie im Replikationsmonitor im linken Bereich eine Verlegergruppe, und erweitern Sie dann einen Verleger.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Veröffentlichung, deren Abonnements Sie überprüfen möchten, und klicken Sie dann auf **Alle Abonnements überprüfen**.  
  
3.  Geben Sie im Dialogfeld **Alle Abonnements überprüfen** den Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme) an.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
6.  Zeigen Sie die Überprüfungsergebnisse an. Führen Sie für jedes Pushabonnement folgende Vorgänge aus:  
  
    1.  Wenn der Agent nicht ausgeführt wird, klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Synchronisierung starten**.  
  
    2.  Klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Details anzeigen**.  
  
    3.  Zeigen Sie die Informationen auf der Registerkarte **Synchronisierungsverlauf** im Textbereich **Letzte Meldung der ausgewählten Sitzung** an.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>So überprüfen Sie die Daten für alle Artikel in einer Transaktionsveröffentlichung  
  
1.  Führen Sie beim Verleger für die Veröffentlichungsdatenbank [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md) aus. Geben Sie **@publication** und einen der folgenden Werte für **@rowcount_only**an:  
  
    -   **1** - nur Überprüfung der Zeilenanzahl (Standardeinstellung)  
  
    -   **2** - Zeilenanzahl und binäre Prüfsumme  
  
    > [!NOTE]  
    >  Beim Ausführen von [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md), wird [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) für jeden Artikel in der Publikation ausgeführt. Um [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md) erfolgreich auszuführen, benötigen Sie SELECT-Berechtigungen für alle Spalten in den veröffentlichten Basistabellen.  
  
2.  (Optional) Starten Sie den Verteilungs-Agent für jedes Abonnement, wenn er nicht bereits ausgeführt wird. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Überprüfen Sie die Agentausgabe für das Ergebnis der Überprüfung. Weitere Informationen finden Sie unter [Überprüfen von replizierten Daten](../../relational-databases/replication/validate-replicated-data.md).  
  
#### <a name="to-validate-data-for-a-single-article-in-a-transactional-publication"></a>So überprüfen Sie die Daten für einen einzelnen Artikel in einer Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) aus. Geben Sie **@publication**, den Namen des Artikels für **@article**und einen der folgenden Werte für **@rowcount_only**an:  
  
    -   **1** - nur Überprüfung der Zeilenanzahl (Standardeinstellung)  
  
    -   **2** - Zeilenanzahl und binäre Prüfsumme  
  
    > [!NOTE]  
    >  Um [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) erfolgreich auszuführen, benötigen Sie SELECT-Berechtigungen für alle Spalten in den veröffentlichten Basistabellen.  
  
2.  (Optional) Starten Sie den Verteilungs-Agent für jedes Abonnement, wenn er nicht bereits ausgeführt wird. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Überprüfen Sie die Agentausgabe für das Ergebnis der Überprüfung. Weitere Informationen finden Sie unter [Überprüfen von replizierten Daten](../../relational-databases/replication/validate-replicated-data.md).  
  
#### <a name="to-validate-data-for-a-single-subscriber-to-a-transactional-publication"></a>So überprüfen Sie die Daten für einen einzelnen Abonnenten einer Transaktionsveröffentlichung  
  
1.  Öffnen Sie auf dem Verleger für die Veröffentlichungsdatenbank eine explizite Transaktion mit [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md).  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_marksubscriptionvalidation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md) aus. Geben Sie die Veröffentlichung für **@publication**, den Namen des Abonnenten für **@subscriber**und den Namen der Abonnementdatenbank für **@destination_db**verfügbar sind.  
  
3.  (Optional) Wiederholen Sie Schritt 2 für jedes zu überprüfende Abonnement.  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) aus. Geben Sie **@publication**, den Namen des Artikels für **@article**und einen der folgenden Werte für **@rowcount_only**an:  
  
    -   **1** - nur Überprüfung der Zeilenanzahl (Standardeinstellung)  
  
    -   **2** - Zeilenanzahl und binäre Prüfsumme  
  
    > [!NOTE]  
    >  Um [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) erfolgreich auszuführen, benötigen Sie SELECT-Berechtigungen für alle Spalten in den veröffentlichten Basistabellen.  
  
5.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank mit [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md) einen Commit für die Transaktion aus.  
  
6.  (Optional) Wiederholen Sie die Schritte 1 bis 5 für jeden zu überprüfenden Artikel.  
  
7.  (Optional) Starten Sie den Verteilungs-Agent, wenn er nicht bereits ausgeführt wird. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
8.  Überprüfen Sie die Agentausgabe für das Ergebnis der Überprüfung. Weitere Informationen finden Sie unter [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>So überprüfen Sie die Daten in allen Abonnements für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_validatemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md) aus. Geben Sie **@publication** und einen der folgenden Werte für **@level**an:  
  
    -   **1** - Nur Überprüfung der Zeilenzählung  
  
    -   **3** - Überprüfung der Zeilenzählung und binären Prüfsumme  
  
     Dadurch werden alle Abonnements zur Überprüfung gekennzeichnet.  
  
2.  Starten Sie den Merge-Agent für jedes Abonnement. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Überprüfen Sie die Agentausgabe für das Ergebnis der Überprüfung. Weitere Informationen finden Sie unter [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
#### <a name="to-validate-data-in-selected-subscriptions-to-a-merge-publication"></a>So überprüfen Sie die Daten in ausgewählten Abonnements für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_validatemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md) aus. Geben Sie **@publication**, den Namen des Abonnenten für **@subscriber**, den Namen der Abonnementdatenbank für **@subscriber_db**und einen der folgenden Werte für **@level**an:  
  
    -   **1** - Nur Überprüfung der Zeilenzählung  
  
    -   **3** - Überprüfung der Zeilenzählung und binären Prüfsumme  
  
     Dadurch wird das ausgewählte Abonnement zur Überprüfung gekennzeichnet.  
  
2.  Starten Sie den Merge-Agent für jedes Abonnement. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Überprüfen Sie die Agentausgabe für das Ergebnis der Überprüfung.  
  
4.  Wiederholen Sie die Schritte 1 bis 3 für jedes zu überprüfende Abonnement.  
  
> [!NOTE]  
>  Ein Abonnement für eine Mergeveröffentlichung kann auch am Ende einer Synchronisierung überprüft werden. Dazu geben Sie den **-Validate** -Parameter an, wenn der [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)ausgeführt wird.  
  
#### <a name="to-validate-data-in-a-subscription-using-merge-agent-parameters"></a>So überprüfen Sie die Daten in einem Abonnement mithilfe von Merge-Agentparametern  
  
1.  Starten Sie auf eine der folgenden Arten den Merge-Agent auf dem Abonnenten (Pullabonnement) oder auf dem Verteiler (Pushabonnement) von der Befehlszeile.  
  
    -   Durch Angeben eines Werts von **1** (Zeilenanzahl) oder **3** (Zeilenanzahl und binäre Prüfsumme) für den **-Validate** -Parameter.  
  
    -   Durch Angeben von **Zeilenanzahlüberprüfung** oder **Überprüfung der Zeilenanzahl und Prüfsumme** für den **-ProfileName** -Parameter.  
  
     Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) oder [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Die Replikation ermöglicht Ihnen mithilfe von Replikationsverwaltungsobjekten (RMO), programmgesteuert zu überprüfen, ob die Daten auf dem Abonnenten mit den Daten auf dem Verleger übereinstimmen. Welche Objekte Sie verwenden, hängt vom Typ der Replikationstopologie ab. Für die Transaktionsreplikation ist eine Überprüfung aller Abonnements für eine Veröffentlichung erforderlich.  
  
> [!NOTE]  
>  Ein Beispiel hierzu finden Sie unter [Beispiel (RMO)](#RMOExample)weiter unten in diesem Abschnitt.  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>So überprüfen Sie die Daten für alle Artikel in einer Transaktionsveröffentlichung  
  
1.  Stellen Sie eine Verbindung mit dem Verleger her, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPublication>-Klasse. Legen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> und die <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>-Eigenschaften für die Veröffentlichung fest. Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf die in Schritt 1 erstellte Verbindung fest.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die restlichen Objekteigenschaften abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften in Schritt 2 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A>-Methode auf. Übergeben Sie die folgenden Werte:  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   Ein boolescher Wert, der angibt, ob der Verteilungs-Agent nach Abschluss der Überprüfung beendet werden soll.  
  
     Dadurch werden die Artikel zur Überprüfung gekennzeichnet.  
  
5.  Starten Sie den Verteilungs-Agent, falls er noch nicht ausgeführt wird, um alle Abonnements zu synchronisieren. Weitere Informationen finden Sie unter [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) oder [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md). Das Ergebnis der Überprüfung wird in den Agentverlauf geschrieben. Weitere Informationen finden Sie unter [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>So überprüfen Sie die Daten in allen Abonnements für eine Mergeveröffentlichung  
  
1.  Stellen Sie eine Verbindung mit dem Verleger her, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication>-Klasse. Legen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> und die <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>-Eigenschaften für die Veröffentlichung fest. Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf die in Schritt 1 erstellte Verbindung fest.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die restlichen Objekteigenschaften abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften in Schritt 2 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A>-Methode auf. Übergeben Sie die gewünschte <xref:Microsoft.SqlServer.Replication.ValidationOption>.  
  
5.  Führen Sie für jedes Abonnement den Merge-Agent aus, um die Überprüfung zu starten, oder warten Sie die nächste geplante Ausführung des Agents ab. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md). Das Ergebnis der Überprüfung wird in den Agentverlauf geschrieben. Diesen können Sie mithilfe des Replikationsmonitors anzeigen. Weitere Informationen finden Sie unter [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
#### <a name="to-validate-data-in-a-single-subscription-to-a-merge-publication"></a>So überprüfen Sie die Daten in einem einzelnen Abonnement für eine Mergeveröffentlichung  
  
1.  Stellen Sie eine Verbindung mit dem Verleger her, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication>-Klasse. Legen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> und die <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>-Eigenschaften für die Veröffentlichung fest. Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>-Eigenschaft auf die in Schritt 1 erstellte Verbindung fest.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>-Methode auf, um die restlichen Objekteigenschaften abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften in Schritt 2 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A>-Methode auf. Übergeben Sie den Namen des Abonnenten und der Abonnementdatenbank, der bzw. die überprüft wird, und die gewünschte <xref:Microsoft.SqlServer.Replication.ValidationOption>.  
  
5.  Führen Sie für das Abonnement den Merge-Agent aus, um die Überprüfung zu starten, oder warten Sie die nächste geplante Ausführung des Agents ab. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md). Das Ergebnis der Überprüfung wird in den Agentverlauf geschrieben. Diesen können Sie mithilfe des Replikationsmonitors anzeigen. Weitere Informationen finden Sie unter [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
###  <a name="RMOExample"></a> Beispiel (RMO)  
 In diesem Beispiel werden alle Abonnements für eine Transaktionsveröffentlichung für die Zeilenanzahlüberprüfung gekennzeichnet.  
  
 [!code-cs[HowTo#rmo_ValidateTranPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 In diesem Beispiel wird ein bestimmtes Abonnement für eine Mergeveröffentlichung für die Zeilenanzahlüberprüfung gekennzeichnet.  
  
 [!code-cs[HowTo#rmo_ValidateMergeSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
  
