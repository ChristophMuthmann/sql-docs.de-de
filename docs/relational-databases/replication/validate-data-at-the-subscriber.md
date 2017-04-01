---
title: "&#220;berpr&#252;fen der Daten am Abonnenten | Microsoft Docs"
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
  - "Abonnenten [SQL Server-Replikation], Datenüberprüfung"
  - "Replikation [SQL Server], Überprüfen von Daten"
  - "Transaktionsreplikation, Überprüfen von Daten"
  - "Überprüfen von Daten"
  - "Datenüberprüfung bei der Mergereplikation [SQL Server-Replikation], SQL Server Management Studio"
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# &#220;berpr&#252;fen der Daten am Abonnenten
  In diesem Thema wird beschrieben, wie Daten beim Abonnenten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) überprüft werden.  
  
 Der Prozess der Datenüberprüfung besteht aus drei Teilen:  
  
1.  Zunächst müssen die Abonnements für eine Veröffentlichung, die überprüft werden sollen, *gekennzeichnet* werden. Die Abonnements, die überprüft werden sollen, können Sie in den Dialogfeldern **Abonnement überprüfen**, **Abonnement überprüfens**und **Alle Abonnements überprüfen** , die über den Ordner **Lokale Veröffentlichungen** und **Lokale Abonnements** in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Abonnements können darüber hinaus auch auf der Registerkarte **Alle Abonnements** , auf der Registerkarte **Überwachungsliste für Abonnements** und über den Veröffentlichungsknoten im Replikationsmonitor gekennzeichnet werden. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
2.  Ein Abonnement wird bei der nächsten Synchronisierung durch den Verteilungs-Agent (für Transaktionsreplikationen) oder durch den Merge-Agent (für Mergereplikationen) überprüft. Der Verteilungs-Agent wird in der Regel kontinuierlich ausgeführt. In diesem Fall erfolgt die Überprüfung sofort. Der Merge-Agent wird in der Regel bei Bedarf ausgeführt, und die Überprüfung erfolgt nach der Ausführung des Agents.  
  
3.  Anzeigen der Überprüfungsergebnisse:  
  
    -   In den Detailfenstern im Replikationsmonitor auf der Registerkarte **Verlauf Verteiler zu Abonnent** für die Transaktionsreplikation und auf der Registerkarte **Synchronisierungsverlauf** für die Mergereplikation.  
  
    -   Im Dialogfeld **Synchronisierungsstatus anzeigen** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   **So prüfen Sie Daten beim Abonnenten mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die Prozeduren für den Replikationsmonitor sind nur für Pushabonnements geeignet, da Pullabonnements im Replikationsmonitor nicht synchronisiert werden können. Sie können ein Abonnement jedoch für die Überprüfung markieren und die Überprüfungsergebnisse für Pullabonnements im Replikationsmonitor anzeigen.  
  
-   In den Überprüfungsergebnissen wird angezeigt, ob die Überprüfung erfolgreich war oder fehlgeschlagen ist, es wird jedoch nicht angegeben, in welchen Zeilen die Überprüfung beim Auftreten eines Fehlers fehlgeschlagen ist. Verwenden Sie das Hilfsprogramm [tablediff Utility](../../tools/tablediff-utility.md), um die Daten auf dem Verleger und auf dem Abonnenten zu vergleichen. Weitere Informationen zum Verwenden dieses Hilfsprogramms für replizierte Daten finden Sie unter [Vergleichen replizierten Tabellen für Unterschiede & #40; Replikationsprogrammierung & #41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So überprüfen Sie Daten für Abonnements einer Transaktionsveröffentlichung (Management Studio)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Mit der rechten Maustaste in der Veröffentlichung, für die Sie Abonnements überprüfen, und klicken Sie dann auf möchten **Abonnements überprüfen**.  
  
4.  Wählen Sie im Dialogfeld **Abonnements überprüfen** die zu überprüfenden Abonnements aus:  
  
    -   Wählen Sie **Alle SQL Server-Abonnements überprüfen**aus.  
  
    -   Wählen Sie **Folgende Abonnements überprüfen**aus, und wählen Sie dann ein oder mehrere Abonnements aus.  
  
5.  Geben Sie der Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme) klicken Sie auf **Validierungsoptionen**, und geben Sie dann in der **Optionen für die Abonnementüberprüfung** (Dialogfeld).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Zeigen Sie die Überprüfungsergebnisse Im Replikationsmonitor oder im Dialogfeld **Synchronisierungsstatus anzeigen** an: Führen Sie für jedes Abonnement folgende Vorgänge aus:  
  
    1.  Erweitern Sie die Veröffentlichung rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
    2.  Wenn der Agent nicht ausgeführt wird, klicken Sie im Dialogfeld **Synchronisierungsstatus anzeigen** auf **Start** . Im Dialogfeld werden Meldungen mit Informationen zur Überprüfung angezeigt.  
  
     Wenn keine Meldungen bezüglich der Überprüfung angezeigt werden, hat der Agent bereits eine nachfolgende Meldung protokolliert. Zeigen Sie die Überprüfungsergebnisse in diesem Fall im Replikationsmonitor an. Weitere Informationen finden Sie in den Prozeduren zu den Verfahrensweisen im Replikationsmonitor in diesem Thema.  
  
#### So überprüfen Sie Daten für ein einzelnes Abonnement für eine Mergeveröffentlichung (Management Studio)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die Veröffentlichung, für die Sie Abonnements überprüfen rechten Maustaste auf das Abonnement, und klicken Sie dann auf möchten **Abonnement überprüfen**.  
  
4.  Wählen Sie im Dialogfeld **Abonnement überprüfen** die Option **Dieses Abonnement überprüfen**aus.  
  
5.  Geben Sie der Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme) klicken Sie auf **Optionen**, und geben Sie dann in der **Optionen für die Abonnementüberprüfung** (Dialogfeld).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Zeigen Sie die Überprüfungsergebnisse Im Replikationsmonitor oder im Dialogfeld **Synchronisierungsstatus anzeigen** an:  
  
    1.  Erweitern Sie die Veröffentlichung rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
    2.  Wenn der Agent nicht ausgeführt wird, klicken Sie im Dialogfeld **Synchronisierungsstatus anzeigen** auf **Start** . Im Dialogfeld werden Meldungen mit Informationen zur Überprüfung angezeigt.  
  
     Wenn keine Meldungen bezüglich der Überprüfung angezeigt werden, hat der Agent bereits eine nachfolgende Meldung protokolliert. Zeigen Sie die Überprüfungsergebnisse in diesem Fall im Replikationsmonitor an. Weitere Informationen finden Sie in den Prozeduren zu den Verfahrensweisen im Replikationsmonitor in diesem Thema.  
  
#### So überprüfen Sie Daten für Abonnements einer Mergeveröffentlichung (Management Studio)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Mit der rechten Maustaste in der Veröffentlichung, für die Sie Abonnements überprüfen, und klicken Sie dann auf möchten **alle Abonnements überprüfen**.  
  
4.  In der **alle Abonnements überprüfen** Dialogfeld geben den Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Zeigen Sie die Überprüfungsergebnisse Im Replikationsmonitor oder im Dialogfeld **Synchronisierungsstatus anzeigen** an: Führen Sie für jedes Abonnement folgende Vorgänge aus:  
  
    1.  Erweitern Sie die Veröffentlichung rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
    2.  Wenn der Agent nicht ausgeführt wird, klicken Sie im Dialogfeld **Synchronisierungsstatus anzeigen** auf **Start** . Im Dialogfeld werden Meldungen mit Informationen zur Überprüfung angezeigt.  
  
     Wenn keine Meldungen bezüglich der Überprüfung angezeigt werden, hat der Agent bereits eine nachfolgende Meldung protokolliert. Zeigen Sie die Überprüfungsergebnisse in diesem Fall im Replikationsmonitor an. Weitere Informationen finden Sie in den Prozeduren zu den Verfahrensweisen im Replikationsmonitor in diesem Thema.  
  
#### So überprüfen Sie die Daten aller Pushabonnements einer Transaktionsveröffentlichung (Replikationsüberwachung)  
  
1.  Erweitern Sie im Replikationsmonitor im linken Bereich eine Verlegergruppe, und erweitern Sie dann einen Verleger.  
  
2.  Mit der rechten Maustaste in der Veröffentlichung, für die Sie Abonnements überprüfen, und klicken Sie dann auf möchten **Abonnements überprüfen**.  
  
3.  Wählen Sie im Dialogfeld **Abonnements überprüfen** die zu überprüfenden Abonnements aus:  
  
    -   Wählen Sie **Alle SQL Server-Abonnements überprüfen**aus.  
  
    -   Wählen Sie **Folgende Abonnements überprüfen**aus, und wählen Sie dann ein oder mehrere Abonnements aus.  
  
4.  Geben Sie der Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme) klicken Sie auf **Validierungsoptionen**, und geben Sie dann in der **Optionen für die Abonnementüberprüfung** (Dialogfeld).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
7.  Zeigen Sie die Überprüfungsergebnisse an. Führen Sie für jedes Pushabonnement folgende Vorgänge aus:  
  
    1.  Wenn der Agent nicht ausgeführt wird, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Synchronisierung starten**.  
  
    2.  Maustaste auf das Abonnement, und klicken Sie dann auf **Details zum**.  
  
    3.  Zeigen Sie die Informationen auf der Registerkarte **Verlauf Verteiler zu Abonnent** im Textbereich **Aktionen in der ausgewählten Sitzung** an.  
  
#### So überprüfen Sie Daten für ein einzelnes Pushabonnement für eine Mergeveröffentlichung (Replikationsmonitor)  
  
1.  Erweitern Sie im Replikationsmonitor im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
3.  Mit der rechten Maustaste des Abonnements zu überprüfen, und klicken Sie dann auf **Abonnement überprüfen**.  
  
4.  Wählen Sie im Dialogfeld **Abonnement überprüfen** die Option **Dieses Abonnement überprüfen**aus.  
  
5.  Geben Sie der Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme) klicken Sie auf **Optionen**, und geben Sie dann in der **Optionen für die Abonnementüberprüfung** (Dialogfeld).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
8.  Zeigen Sie die Überprüfungsergebnisse an:  
  
    1.  Wenn der Agent nicht ausgeführt wird, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Synchronisierung starten**.  
  
    2.  Maustaste auf das Abonnement, und klicken Sie dann auf **Details zum**.  
  
    3.  Zeigen Sie die Informationen auf der Registerkarte **Synchronisierungsverlauf** im Textbereich **Letzte Meldung der ausgewählten Sitzung** an.  
  
#### So überprüfen Sie die Daten aller Pushabonnements einer Mergeveröffentlichung (Replikationsüberwachung)  
  
1.  Erweitern Sie im Replikationsmonitor im linken Bereich eine Verlegergruppe, und erweitern Sie dann einen Verleger.  
  
2.  Mit der rechten Maustaste in der Veröffentlichung, für die Sie Abonnements überprüfen, und klicken Sie dann auf möchten **alle Abonnements überprüfen**.  
  
3.  In der **alle Abonnements überprüfen** Dialogfeld geben den Typ der durchzuführenden Überprüfung (Zeilenanzahl oder Zeilenanzahl und Prüfsumme).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
6.  Zeigen Sie die Überprüfungsergebnisse an. Führen Sie für jedes Pushabonnement folgende Vorgänge aus:  
  
    1.  Wenn der Agent nicht ausgeführt wird, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Synchronisierung starten**.  
  
    2.  Maustaste auf das Abonnement, und klicken Sie dann auf **Details zum**.  
  
    3.  Zeigen Sie die Informationen auf der Registerkarte **Synchronisierungsverlauf** im Textbereich **Letzte Meldung der ausgewählten Sitzung** an.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So überprüfen Sie die Daten für alle Artikel in einer Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_publication_validation & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md). Geben Sie **@publication** und einen der folgenden Werte für **@rowcount_only**:  
  
    -   **1** -nur Überprüfung der Zeilenanzahl (Standardeinstellung)  
  
    -   **2** -Zeilenanzahl und binäre Prüfsumme.  
  
    > [!NOTE]  
    >  Beim Ausführen [Sp_publication_validation & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md), [Sp_article_validation & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) wird für jeden Artikel in der Veröffentlichung ausgeführt werden. Um erfolgreich ausgeführt [Sp_publication_validation & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md), benötigen Sie SELECT-Berechtigungen für alle Spalten in den veröffentlichten Basistabellen.  
  
2.  (Optional) Starten Sie den Verteilungs-Agent für jedes Abonnement, wenn er nicht bereits ausgeführt wird. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Überprüfen Sie die Agentausgabe für das Ergebnis der Überprüfung. Weitere Informationen finden Sie unter [Überprüfen von replizierten Daten](../../relational-databases/replication/validate-replicated-data.md).  
  
#### So überprüfen Sie die Daten für einen einzelnen Artikel in einer Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_article_validation & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md). Geben Sie **@publication**, den Namen des Artikels für **@article**, und einen der folgenden Werte für **@rowcount_only**:  
  
    -   **1** -nur Überprüfung der Zeilenanzahl (Standardeinstellung)  
  
    -   **2** -Zeilenanzahl und binäre Prüfsumme.  
  
    > [!NOTE]  
    >  Um erfolgreich ausgeführt [Sp_article_validation & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md), benötigen Sie SELECT-Berechtigungen für alle Spalten in der veröffentlichten Basistabelle.  
  
2.  (Optional) Starten Sie den Verteilungs-Agent für jedes Abonnement, wenn er nicht bereits ausgeführt wird. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Überprüfen Sie die Agentausgabe für das Ergebnis der Überprüfung. Weitere Informationen finden Sie unter [Überprüfen von replizierten Daten](../../relational-databases/replication/validate-replicated-data.md).  
  
#### So überprüfen Sie die Daten für einen einzelnen Abonnenten einer Transaktionsveröffentlichung  
  
1.  Öffnen Sie auf dem Verleger für die Veröffentlichungsdatenbank eine explizite Transaktion mit [BEGIN TRANSACTION & #40; Transact-SQL & #41;](../../t-sql/language-elements/begin-transaction-transact-sql.md).  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_marksubscriptionvalidation & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md). Geben Sie die Veröffentlichung für **@publication**, den Namen des Abonnenten für **@subscriber**, und den Namen der Abonnementdatenbank für **@destination_db**.  
  
3.  (Optional) Wiederholen Sie Schritt 2 für jedes zu überprüfende Abonnement.  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_article_validation & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md). Geben Sie **@publication**, den Namen des Artikels für **@article**, und einen der folgenden Werte für **@rowcount_only**:  
  
    -   **1** -nur Überprüfung der Zeilenanzahl (Standardeinstellung)  
  
    -   **2** -Zeilenanzahl und binäre Prüfsumme.  
  
    > [!NOTE]  
    >  Um erfolgreich ausgeführt [Sp_article_validation & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md), benötigen Sie SELECT-Berechtigungen für alle Spalten in der veröffentlichten Basistabelle.  
  
5.  Auf dem Verleger für die Veröffentlichungsdatenbank commit der Transaktion mit [COMMIT TRANSACTION & #40; Transact-SQL & #41;](../../t-sql/language-elements/commit-transaction-transact-sql.md).  
  
6.  (Optional) Wiederholen Sie die Schritte 1 bis 5 für jeden zu überprüfenden Artikel.  
  
7.  (Optional) Starten Sie den Verteilungs-Agent, wenn er nicht bereits ausgeführt wird. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
8.  Überprüfen Sie die Agentausgabe für das Ergebnis der Überprüfung. Weitere Informationen finden Sie unter [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
#### So überprüfen Sie die Daten in allen Abonnements für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_validatemergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md). Geben Sie **@publication** und einen der folgenden Werte für **@level**an:  
  
    -   **1** -nur Überprüfung der Zeilenzählung.  
  
    -   **3** -Überprüfung der Zeilenzählung und binären Prüfsumme.  
  
     Dadurch werden alle Abonnements zur Überprüfung gekennzeichnet.  
  
2.  Starten Sie den Merge-Agent für jedes Abonnement. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Überprüfen Sie die Agentausgabe für das Ergebnis der Überprüfung. Weitere Informationen finden Sie unter [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
#### So überprüfen Sie die Daten in ausgewählten Abonnements für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_validatemergesubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md). Geben Sie **@publication**, den Namen des Abonnenten für **@subscriber**, den Namen der Abonnementdatenbank für **@subscriber_db**, und einen der folgenden Werte für **@level**:  
  
    -   **1** -nur Überprüfung der Zeilenzählung.  
  
    -   **3** -Überprüfung der Zeilenzählung und binären Prüfsumme.  
  
     Dadurch wird das ausgewählte Abonnement zur Überprüfung gekennzeichnet.  
  
2.  Starten Sie den Merge-Agent für jedes Abonnement. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Überprüfen Sie die Agentausgabe für das Ergebnis der Überprüfung.  
  
4.  Wiederholen Sie die Schritte 1 bis 3 für jedes zu überprüfende Abonnement.  
  
> [!NOTE]  
>  Ein Abonnement für eine Mergeveröffentlichung kann auch am Ende einer Synchronisierung überprüft werden, durch Angabe der **-überprüfen** Parameter beim Ausführen der [Replikationsmerge-Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
#### So überprüfen Sie die Daten in einem Abonnement mithilfe von Merge-Agentparametern  
  
1.  Starten Sie auf eine der folgenden Arten den Merge-Agent auf dem Abonnenten (Pullabonnement) oder auf dem Verteiler (Pushabonnement) von der Befehlszeile.  
  
    -   Bei Angabe des Werts **1** (Zeilenanzahl) oder **3** (Zeilenanzahl und binäre Prüfsumme) für die **-überprüfen** Parameter.  
  
    -   Angeben von **Überprüfung der Zeilenanzahl** oder **Überprüfung der Zeilenanzahl und Prüfsumme** für die **- ProfileName** Parameter.  
  
     Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) oder [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Die Replikation ermöglicht Ihnen mithilfe von Replikationsverwaltungsobjekten (RMO), programmgesteuert zu überprüfen, ob die Daten auf dem Abonnenten mit den Daten auf dem Verleger übereinstimmen. Welche Objekte Sie verwenden, hängt vom Typ der Replikationstopologie ab. Für die Transaktionsreplikation ist eine Überprüfung aller Abonnements für eine Veröffentlichung erforderlich.  
  
> [!NOTE]  
>  Ein Beispiel finden Sie unter [Beispiel (RMO)](#RMOExample), Weiter unten in diesem Abschnitt.  
  
#### So überprüfen Sie die Daten für alle Artikel in einer Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPublication> Klasse. Legen Sie den <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> und <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Eigenschaften für die Veröffentlichung. Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die in Schritt 1 erstellte Verbindung.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode, um die übrigen Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften in Schritt 2 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A> Methode. Übergeben Sie die folgenden Werte:  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>  
  
    -   Ein boolescher Wert, der angibt, ob der Verteilungs-Agent nach Abschluss der Überprüfung beendet werden soll.  
  
     Dadurch werden die Artikel zur Überprüfung gekennzeichnet.  
  
5.  Starten Sie den Verteilungs-Agent, falls er noch nicht ausgeführt wird, um alle Abonnements zu synchronisieren. Weitere Informationen finden Sie unter [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) oder [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md). Das Ergebnis der Überprüfung wird in den Agentverlauf geschrieben. Weitere Informationen finden Sie unter [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
#### So überprüfen Sie die Daten in allen Abonnements für eine Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication> Klasse. Legen Sie den <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> und <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Eigenschaften für die Veröffentlichung. Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die in Schritt 1 erstellte Verbindung.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode, um die übrigen Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften in Schritt 2 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A> Methode. Übergeben Sie die gewünschte <xref:Microsoft.SqlServer.Replication.ValidationOption>.  
  
5.  Führen Sie für jedes Abonnement den Merge-Agent aus, um die Überprüfung zu starten, oder warten Sie die nächste geplante Ausführung des Agents ab. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md). Das Ergebnis der Überprüfung wird in den Agentverlauf geschrieben. Diesen können Sie mithilfe des Replikationsmonitors anzeigen. Weitere Informationen finden Sie unter [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
#### So überprüfen Sie die Daten in einem einzelnen Abonnement für eine Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication> Klasse. Legen Sie den <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> und <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Eigenschaften für die Veröffentlichung. Legen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft auf die in Schritt 1 erstellte Verbindung.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode, um die übrigen Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, sind die Veröffentlichungseigenschaften in Schritt 2 falsch definiert, oder die Veröffentlichung ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A> Methode. Übergeben Sie den Namen der Abonnent und Abonnement-Datenbank überprüft wird und die gewünschte <xref:Microsoft.SqlServer.Replication.ValidationOption>.  
  
5.  Führen Sie für das Abonnement den Merge-Agent aus, um die Überprüfung zu starten, oder warten Sie die nächste geplante Ausführung des Agents ab. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) und [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md). Das Ergebnis der Überprüfung wird in den Agentverlauf geschrieben. Diesen können Sie mithilfe des Replikationsmonitors anzeigen. Weitere Informationen finden Sie unter [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
###  <a name="RMOExample"></a> Beispiel (RMO)  
 In diesem Beispiel werden alle Abonnements für eine Transaktionsveröffentlichung für die Zeilenanzahlüberprüfung gekennzeichnet.  
  
 [!code-csharp[HowTo#rmo_ValidateTranPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 In diesem Beispiel wird ein bestimmtes Abonnement für eine Mergeveröffentlichung für die Zeilenanzahlüberprüfung gekennzeichnet.  
  
 [!code-csharp[HowTo#rmo_ValidateMergeSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
  