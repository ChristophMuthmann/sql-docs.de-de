---
title: "Anzeigen und Ändern von Replikationssicherheitseinstellungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying replication security settings
- replication [SQL Server], security
- security [SQL Server replication], viewing settings
- viewing replication security settings
- security [SQL Server replication], modifying settings
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
caps.latest.revision: "47"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 673d8fdcdda983dd111b6c2297f2303882b8bd66
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="view-and-modify-replication-security-settings"></a>Anzeigen und Ändern von Replikationssicherheitseinstellungen
  In diesem Thema wird beschrieben, wie die Replikationssicherheitseinstellungen in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekten (RMO) angezeigt und geändert werden. Die Verbindung des Protokolllese-Agents mit dem Verleger ist beispielsweise als SQL Server-Authentifizierung festgelegt, und Sie möchten Sie zu Integrierte Windows-Authentifizierung ändern, oder Sie müssen die zum Ausführen eines Agentauftrags verwendeten Anmeldeinformationen ändern, weil sich das Kennwort eines Windows-Kontos geändert hat. Informationen zu den für die jeweiligen Agents erforderlichen Berechtigungen finden Sie unter [Sicherheitsmodell des Replikations-Agents](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So zeigen Sie Replikationssicherheitseinstellungen an und ändern sie mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Ändern der Replikationssicherheitseinstellungen](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Welche gespeicherten Prozeduren Sie verwenden, hängt vom Typ des Agents und vom Typ der Serververbindung ab.  
  
-   Welche RMO-Klassen und -Eigenschaften verwendet werden, hängt vom Agenttyp und vom Typ der Serververbindung ab.  
  
###  <a name="Security"></a> Sicherheit  
 Aus Sicherheitsgründen werden die eigentlichen Werte der Kennwörter in Resultsets maskiert, die von den gespeicherten Replikationsprozeduren zurückgegeben werden.  
  
####  <a name="Permissions"></a> Berechtigungen  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Sie können die Sicherheitseinstellungen in den folgenden Dialogfeldern anzeigen und ändern:  
  
1.  Im Dialogfeld **Replikationskennwörter aktualisieren** , das über den Ordner **Replikation** von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]verfügbar ist. Wenn Sie das Kennwort eines [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] - oder Windows-Kontos auf einem Server der Replikationstopologie ändern, verwenden Sie am besten dieses Dialogfeld, anstatt die Kennwörter jedes Agents, der dieses Konto verwendet, einzeln zu aktualisieren. Wenn jedoch Agents dasselbe Konto auf mehreren Servern verwenden, müssen Sie mit jedem Server eine Verbindung herstellen und das Kennwort ändern. Das Kennwort wird überall aktualisiert, wo es die Replikation verwendet. Das Kennwort wird nicht an anderen Orten, wie z. B. auf Verbindungsservern, aktualisiert.  
  
2.  Auf der Seite **Agentsicherheit** des Dialogfelds **Veröffentlichungseigenschaften - \<Veröffentlichung>**. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
3.  Im Dialogfeld **Abonnementeigenschaften - \<Subscription>**. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) und [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
4.  In den Dialogfeldern **Verteilereigenschaften - \<Distributor>** und **Eigenschaften der Verteilungsdatenbank - \<Database>**. Weitere Informationen zum Zugreifen auf diese Dialogfelder finden Sie unter [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
5.  Im Dialogfeld **Verlegereigenschaften - \<Verleger>**. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
#### <a name="to-change-the-password-for-an-account-used-by-one-or-more-agents"></a>So ändern Sie das Kennwort für ein Konto, das von einem oder mehreren Agent(s) verwendet wird  
  
1.  Wenn es sich um ein SQL Server-Konto handelt, wird über dieses Dialogfeld auch das Kennwort für das SQL Server-Konto geändert. Wenn es sich um ein Windows-Konto handelt, müssen Sie zuerst das Kennwort in Windows ändern. Weitere Informationen finden Sie in der Windows-Dokumentation.  
  
    > [!NOTE]  
    >  Nachdem Sie ein Replikationskennwort geändert haben, müssen Sie jeden Agent, der dieses Kennwort verwendet, beenden und neu starten, damit die Änderung für diesen Agent in Kraft tritt.  
  
2.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Server her, und erweitern Sie dann den Serverknoten.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Replikation** , und klicken Sie dann auf **Replikationskennwörter aktualisieren**.  
  
4.  Geben Sie im Dialogfeld **Replikationskennwörter aktualisieren** das Konto und das neue Kennwort an.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>So ändern Sie die Sicherheitseinstellungen für den Momentaufnahme-Agent  
  
1.  Klicken Sie auf der Seite **Agentsicherheit** des Dialogfelds **Veröffentlichungseigenschaften - \<Veröffentlichung>** auf die Schaltfläche **Sicherheitseinstellungen** neben dem Textfeld **Momentaufnahme-Agent**.  
  
2.  Geben Sie im Dialogfeld **Sicherheit für den Momentaufnahme-Agent** das Konto an, unter dem der Agent ausgeführt werden soll.  
  
    -   Geben Sie im Textfeld **Agent-Konto** ein neues Windows-Konto ein.  
  
    -   Geben Sie in den Textfeldern **Kennwort** und **Kennwort bestätigen** ein neues, sicheres Kennwort ein.  
  
3.  Geben Sie den Kontext an, in dem der Agent vom Verteiler aus eine Verbindung mit dem Verleger herstellen soll. Wenn Sie **Folgende SQL Server-Anmeldung verwenden**auswählen, müssen Sie auch einen Anmeldenamen angeben:  
  
    -   Geben Sie einen Anmeldenamen in das Textfeld **Anmeldung** ein.  
  
    -   Geben Sie in den Textfeldern **Kennwort** und **Kennwort bestätigen** ein neues, sicheres Kennwort ein.  
  
    > [!NOTE]  
    >  Wenn es sich beim Verleger um einen Oracle-Verleger handelt, wird der Verbindungskontext im Dialogfeld **Verteilereigenschaften - \<Distributor>** angegeben. Die Prozedur zum Ändern des Kontexts finden Sie weiter unten in diesem Thema.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>So ändern Sie die Sicherheitseinstellungen für den Protokolllese-Agent  
  
1.  Klicken Sie auf der Seite **Agentsicherheit** des Dialogfelds **Veröffentlichungseigenschaften - \<Veröffentlichung>** auf die Schaltfläche **Sicherheitseinstellungen** neben dem Textfeld **Protokolllese-Agent**.  
  
2.  Geben Sie im Dialogfeld **Sicherheit für den Protokolllese-Agent** das Konto an, unter dem der Agent ausgeführt werden soll.  
  
    -   Geben Sie im Textfeld **Agent-Konto** ein neues Windows-Konto ein.  
  
    -   Geben Sie in den Textfeldern **Kennwort** und **Kennwort bestätigen** ein neues, sicheres Kennwort ein.  
  
3.  Geben Sie den Kontext an, in dem der Agent vom Verteiler aus eine Verbindung mit dem Verleger herstellen soll. Wenn Sie **Folgende SQL Server-Anmeldung verwenden**auswählen, müssen Sie auch einen Anmeldenamen angeben:  
  
    -   Geben Sie einen Anmeldenamen in das Textfeld **Anmeldung** ein.  
  
    -   Geben Sie in den Textfeldern **Kennwort** und **Kennwort bestätigen** ein neues, sicheres Kennwort ein.  
  
    > [!NOTE]  
    >  Wenn es sich beim Verleger um einen Oracle-Verleger handelt, wird der Verbindungskontext im Dialogfeld **Verteilereigenschaften - \<Distributor>** angegeben. Ändern Sie den Kontext wie in der nächsten Prozedur beschrieben.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Für jede veröffentlichte Datenbank gibt es einen Protokolllese-Agent. Wenn Sie die Sicherheitseinstellungen eines Agents einer Veröffentlichung ändern, wirkt sich dies auf alle Veröffentlichungen der Veröffentlichungsdatenbank aus.  
  
#### <a name="to-change-the-context-under-which-the-snapshot-agent-and-log-reader-agent-for-an-oracle-publication-make-connections-to-the-publisher"></a>So ändern Sie den Kontext, in dem der Momentaufnahme-Agent und der Protokolllese-Agent einer Oracle-Veröffentlichung Verbindungen zum Verleger herstellen  
  
1.  Klicken Sie auf der Seite **Verleger** des Dialogfelds **Verteilereigenschaften - \<Distributor>** auf die Schaltfläche mit den drei Punkten (**…**) neben einem Verleger.  
  
2.  Geben Sie im Abschnitt **Agentverbindung mit dem Verleger** den Anmeldenamen und das Kennwort an, die das von Ihnen konfigurierte Schema für den administrativen Replikationsbenutzer verwendet. Weitere Informationen finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>So ändern Sie die Sicherheitseinstellungen für den Verteilungs-Agent eines Pushabonnements  
  
1.  Im Dialogfeld **Abonnementeigenschaften - \<Subscription>** auf dem Verleger können Sie folgende Änderungen vornehmen:  
  
    -   Um das Konto zu ändern, unter dem der Verteilungs-Agent ausgeführt wird und Verbindungen zum Verteiler herstellt, klicken Sie auf die Zeile **Agentprozesskonto** , und klicken Sie dann in der Zeile auf die Schaltfläche mit den drei Punkten (**…**). Geben Sie im Dialogfeld **Sicherheit für den Verteilungs-Agent** einen Anmeldenamen und ein Kennwort an.  
  
    -   Um den Kontext zu ändern, in dem der Verteilungs-Agent Verbindungen zum Abonnenten herstellt, klicken Sie auf die Zeile **Abonnentenverbindung** , und klicken Sie dann in der Zeile auf die Schaltfläche mit den drei Punkten (**…**). Geben Sie den Kontext im Dialogfeld **Verbindungsinformationen eingeben** an.  
  
         Wenn Sie Abonnements mit verzögertem Update über eine Warteschlange verwenden, verwendet auch der Warteschlangenlese-Agent den hier angegebenen Kontext für Verbindungen zum Abonnenten.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>So ändern Sie die Sicherheitseinstellungen für den Verteilungs-Agent eines Pullabonnements  
  
1.  Im Dialogfeld **Abonnementeigenschaften - \<Subscription>** auf dem Abonnenten können Sie folgende Änderungen vornehmen:  
  
    -   Um das Konto zu ändern, unter dem der Verteilungs-Agent ausgeführt wird und Verbindungen zum Abonnenten herstellt, klicken Sie auf die Zeile **Agentprozesskonto** , und klicken Sie dann in der Zeile auf die Schaltfläche mit den drei Punkten (**…**). Geben Sie im Dialogfeld **Sicherheit für den Verteilungs-Agent** einen Anmeldenamen und ein Kennwort an.  
  
         Wenn Sie Abonnements mit verzögertem Update über eine Warteschlange verwenden, verwendet auch der Warteschlangenlese-Agent den hier angegebenen Kontext für Verbindungen zum Abonnenten.  
  
    -   Um den Kontext zu ändern, in dem der Verteilungs-Agent Verbindungen zum Verteiler herstellt, klicken Sie auf die Zeile **Verteilerverbindung** , und klicken Sie dann in der Zeile auf die Schaltfläche mit den drei Punkten (**…**). Geben Sie den Kontext im Dialogfeld **Verbindungsinformationen eingeben** an.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>So ändern Sie die Sicherheitseinstellungen für den Merge-Agent eines Pushabonnements  
  
1.  Im Dialogfeld **Abonnementeigenschaften - \<Subscription>** auf dem Verleger können Sie folgende Änderungen vornehmen:  
  
    -   Um das Konto zu ändern, unter dem der Merge-Agent ausgeführt wird und Verbindungen zum Verleger und zum Verteiler herstellt, klicken Sie auf die Zeile **Agentprozesskonto** , und klicken Sie dann in der Zeile auf die Schaltfläche mit den drei Punkten (**…**). Geben Sie im Dialogfeld **Sicherheit für den Merge-Agent** einen Anmeldenamen und ein Kennwort an.  
  
    -   Um den Kontext zu ändern, in dem der Merge-Agent Verbindungen zum Abonnenten herstellt, klicken Sie auf die Zeile **Abonnentenverbindung** , und klicken Sie dann in der Zeile auf die Schaltfläche mit den drei Punkten (**…**). Geben Sie den Kontext im Dialogfeld **Verbindungsinformationen eingeben** an.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>So ändern Sie die Sicherheitseinstellungen für den Merge-Agent eines Pullabonnements  
  
1.  Im Dialogfeld **Abonnementeigenschaften - \<Subscription>** auf dem Abonnenten können Sie folgende Änderungen vornehmen:  
  
    -   Um das Konto zu ändern, unter dem der Merge-Agent ausgeführt wird und Verbindungen zum Abonnenten herstellt, klicken Sie auf die Zeile **Agentprozesskonto** , und klicken Sie dann in der Zeile auf die Schaltfläche mit den drei Punkten (**…**). Geben Sie im Dialogfeld **Sicherheit für den Merge-Agent** einen Anmeldenamen und ein Kennwort an.  
  
    -   Um den Kontext zu ändern, in dem der Merge-Agent Verbindungen zum Verleger und zum Verteiler herstellt, klicken Sie auf die Zeile **Verlegerverbindung** , und klicken Sie dann in der Zeile auf die Schaltfläche mit den drei Punkten (**…**). Geben Sie den Kontext im Dialogfeld **Verbindungsinformationen eingeben** an.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-the-account-under-which-the-queue-reader-agent-runs"></a>So ändern Sie das Konto, unter dem der Warteschlangenlese-Agent ausgeführt wird  
  
1.  Klicken Sie auf der Seite **Allgemein** des Dialogfelds **Verteilereigenschaften - \<Distributor>** auf die Schaltfläche mit den drei Punkten (**…**) neben der Verteilungsdatenbank.  
  
2.  Klicken Sie im Dialogfeld **Eigenschaften der Verteilungsdatenbank - \<Database>** auf die Schaltfläche **Sicherheitseinstellungen** neben dem Textfeld **Agentprozesskonto**.  
  
3.  Geben Sie im Dialogfeld **Sicherheit für den Warteschlangenlese-Agent** das Konto an, unter dem der Agent ausgeführt werden und Verbindungen zum Verteiler herstellen soll.  
  
    -   Geben Sie im Textfeld **Prozesskonto** ein neues Windows-Konto ein.  
  
    -   Geben Sie in den Textfeldern **Kennwort** und **Kennwort bestätigen** ein neues, sicheres Kennwort ein.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Es gibt einen Warteschlangenlese-Agent für jede Verteilungsdatenbank. Wenn Sie die Sicherheitseinstellungen eines Agents ändern, wirkt sich dies auf alle Veröffentlichungen auf allen Verlegern aus, die diese Verteilungsdatenbank verwenden.  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-publisher"></a>So ändern Sie den Kontext, in dem der Warteschlangenlese-Agent Verbindungen zum Verleger herstellt  
  
1.  Klicken Sie auf der Seite **Verleger** des Dialogfelds **Verteilereigenschaften - \<Distributor>** auf die Schaltfläche mit den drei Punkten (**…**) neben dem Verleger.  
  
2.  Geben Sie im Abschnitt **Agentverbindung mit dem Verleger** den Wert **Identität des Agentprozesskontos annehmen** oder **SQL Server-Authentifizierung** für die Option **Agentverbindungsmodus** an. Wenn Sie **SQL Server-Authentifizierung**angeben, müssen Sie auch Werte für **Anmeldung** und **Kennwort**eingeben.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Es gibt einen Warteschlangenlese-Agent für jede Verteilungsdatenbank. Wenn Sie die Sicherheitseinstellungen eines Agents ändern, wirkt sich dies auf alle Veröffentlichungen auf allen Verlegern aus, die diese Verteilungsdatenbank verwenden.  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-subscriber"></a>So ändern Sie den Kontext, in dem der Warteschlangenlese-Agent Verbindungen zum Abonnenten herstellt  
  
-   Der Warteschlangenlese-Agent verwendet denselben Verbindungskontext wie der Verteilungs-Agent für das Abonnement. Weitere Informationen finden Sie in der oben stehenden Prozedur zum Verteilungs-Agent.  
  
#### <a name="to-change-security-settings-for-an-immediate-updating-pull-subscription"></a>So ändern Sie die Sicherheitseinstellungen für ein Pullabonnement mit sofortigem Update  
  
1.  Klicken Sie im Dialogfeld **Abonnementeigenschaften - \<Subscription>** auf dem Abonnenten auf die Zeile **Verlegerverbindung**, und klicken Sie dann in der Zeile auf die Schaltfläche mit den drei Punkten (**…**).  
  
2.  Wählen Sie im Dialogfeld **Verbindungsinformationen eingeben** eine der folgenden Optionen aus:  
  
    -   **Anmeldung von einem Verbindungsserver oder Remoteserver verwenden**. Wählen Sie diese Option aus, wenn Sie einen Remoteserver oder Verbindungsserver zwischen dem Abonnenten und dem Verleger mithilfe von [sp_addserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder einer anderen Methode definiert haben.  
  
    -   **SQL Server-Authentifizierung mit dem folgenden Anmeldenamen und Kennwort verwenden**. Wählen Sie diese Option aus, wenn Sie keinen Remoteserver oder Verbindungsserver für die Verbindungen zwischen dem Abonnenten und dem Verleger definiert haben. Die Replikation erstellt dann einen Verbindungsserver für Sie. Das Konto, das Sie angeben, muss bereits auf dem Verleger vorhanden sein.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  In dieser Prozedur wird beschrieben, wie die Methode geändert werden kann, die Replikationstrigger verwenden, um eine Verbindung zwischen dem Abonnenten und dem Verleger herzustellen, wenn auf dem Abonnenten Änderungen vorgenommen wurden. Sie können auch auf den Verteilungs-Agent für Abonnements mit sofortigem Update bezogene Einstellungen ändern. Weitere Informationen finden Sie in den Prozeduren weiter oben in diesem Thema.  
>   
>  Diese Prozedur gilt nur für Pullabonnements. Verwenden Sie bei Pushabonnements die gespeicherte Prozedur [sp_link_publication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md).  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>So ändern Sie das Kennwort für die Verwaltungsverbindung zwischen dem Verleger und dem Verteiler  
  
1.  Geben Sie auf der Seite **Verleger** des Dialogfelds **Verteilereigenschaften - \<Distributor>** in die Textfelder **Kennwort** und **Kennwort bestätigen** ein sicheres Kennwort ein.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  Geben Sie auf der Seite **Allgemein** des Dialogfelds **Verlegereigenschaften - \<Verleger>** in die Textfelder **Kennwort** und **Kennwort bestätigen** ein sicheres Kennwort ein.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
> [!IMPORTANT]  
>  In allen der folgenden Prozeduren sollte der Benutzer nach Möglichkeit aufgefordert werden, zur Laufzeit Sicherheitsanmeldeinformationen einzugeben. Wenn Sie Anmeldeinformationen in einer Skriptdatei speichern, müssen Sie die Datei schützen, um unberechtigtem Zugriff vorzubeugen.  
  
#### <a name="to-change-all-instances-of-a-stored-password-at-a-replication-server"></a>So ändern Sie alle Instanzen eines gespeicherten Kennworts auf einem Replikationsserver  
  
1.  Führen Sie auf einem Server in einer Replikationstopologie für die Masterdatenbank [sp_changereplicationserverpasswords](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md)aus. Geben Sie das [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Konto oder den [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldenamen, dessen Kennwort geändert wird, für **@login** sowie das neue Kennwort für das Konto oder den Anmeldenamen für **@password**. Damit wird jede Instanz des Kennworts geändert, die von allen Agents auf dem Server beim Herstellen einer Verbindung mit anderen Servern in der Topologie verwendet wird.  
  
    > [!NOTE]  
    >  Wenn nur der Anmeldename und das Kennwort für eine Verbindung mit einem bestimmten Server in der Topologie geändert werden soll (z. B. der Verteiler oder der Abonnent), geben Sie den Namen dieses Servers für **@server**.  
  
2.  Wiederholen Sie Schritt 1 für jeden Server in der Replikationstopologie, für den das Kennwort aktualisiert werden muss.  
  
    > [!NOTE]  
    >  Nachdem Sie ein Replikationskennwort geändert haben, müssen Sie jeden Agent, der dieses Kennwort verwendet, beenden und neu starten, damit die Änderung für diesen Agent in Kraft tritt.  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>So ändern Sie die Sicherheitseinstellungen für den Momentaufnahme-Agent  
  
1.  Führen Sie [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md)auf dem Verleger unter Angabe von **@publication**. Damit werden die aktuellen Sicherheitseinstellungen für den Momentaufnahme-Agent zurückgegeben.  
  
2.  Führen Sie [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)auf dem Verleger unter Angabe von **@publication** und einer oder mehrerer der folgenden zu ändernden Sicherheitseinstellungen aus:  
  
    -   Geben Sie **@job_login** und **@job_password**.  
  
    -   Zum Ändern des Sicherheitsmodus, der beim Herstellen einer Verbindung mit dem Verleger verwendet wird, geben Sie den Wert **1** oder **0** für **@publisher_security_mode**.  
  
    -   Wenn Sie den beim Herstellen einer Verbindung mit dem Verleger verwendeten Sicherheitsmodus von **1** in **0** oder einen für diese Verbindung verwendeten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldenamen ändern, geben Sie **@publisher_login** und **@publisher_password**.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Parameter, einschließlich *job_login* und *job_password*, bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>So ändern Sie die Sicherheitseinstellungen für den Protokolllese-Agent  
  
1.  Führen Sie [sp_helplogreader_agent](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)auf dem Verleger unter Angabe von **@publisher**. Damit werden die aktuellen Sicherheitseinstellungen für den Protokolllese-Agent zurückgegeben.  
  
2.  Führen Sie [sp_changelogreader_agent](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)auf dem Verleger unter Angabe von **@publication** und einer oder mehrerer der folgenden zu ändernden Sicherheitseinstellungen aus:  
  
    -   Geben Sie **@job_login** und **@job_password**.  
  
    -   Zum Ändern des Sicherheitsmodus, der beim Herstellen einer Verbindung mit dem Verleger verwendet wird, geben Sie den Wert **1** oder **0** für **@publisher_security_mode**.  
  
    -   Wenn Sie den beim Herstellen einer Verbindung mit dem Verleger verwendeten Sicherheitsmodus von **1** in **0** oder einen für diese Verbindung verwendeten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldenamen ändern, geben Sie **@publisher_login** und **@publisher_password**.  
  
    > [!NOTE]  
    >  Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Parameter, einschließlich *job_login* und *job_password*, bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>So ändern Sie die Sicherheitseinstellungen für den Verteilungs-Agent eines Pushabonnements  
  
1.  Führen Sie [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)auf dem Verleger unter Angabe von **@publication** und **@subscriber**. Damit werden die Abonnementeigenschaften zurückgegeben, einschließlich der Sicherheitseinstellungen für den Verteilungs-Agent, der auf dem Verteiler ausgeführt wird.  
  
2.  Führen Sie [sp_changesubscription](../../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)auf dem Verleger unter Angabe von **@publication**, **@subscriber**, **@subscriber_db**, den Wert **all** für **@article**, den Namen der Sicherheitseigenschaft für **@property**und den neuen Wert der Eigenschaft für **@value**.  
  
3.  Wiederholen Sie Schritt 2 für jede der folgenden Sicherheitseigenschaften, die geändert wird:  
  
    -   Geben Sie den Wert **distrib_job_password** für **@property** und ein neues Kennwort für **@value**. Wenn Sie das Konto ändern, wiederholen Sie Schritt 2, und geben Sie den Wert **distrib_job_login** für **@property** und das neue Windows-Konto für **@value**.  
  
    -   Um den zum Herstellen der Verbindung mit dem Abonnenten verwendeten Sicherheitsmodus zu ändern, geben Sie den Wert **subscriber_security_mode** für **@property** und den Wert **1** (integrierte Windows-Authentifizierung) oder **0** (SQL Server-Authentifizierung) für **@value**.  
  
    -   Wenn Sie den Sicherheitsmodus für den Abonnenten in die SQL Server-Authentifizierung oder die Anmeldeinformationen für die SQL Server-Authentifizierung ändern, geben Sie den Wert **subscriber_password** für **@property** und das neue Kennwort für **@value**. Wiederholen Sie Schritt 2, und geben Sie dabei den Wert **subscriber_login** für **@property** und den neuen Anmeldenamen für **@value**.  
  
    > [!NOTE]  
    >  Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Eigenschaften einschließlich **distrib_job_login** und **distrib_job_password**bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>So ändern Sie die Sicherheitseinstellungen für den Verteilungs-Agent eines Pullabonnements  
  
1.  Führen Sie auf dem Abonnenten [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)auf dem Verleger unter Angabe von **@publication**. Damit werden die Abonnementeigenschaften zurückgegeben, einschließlich der Sicherheitseinstellungen für den Verteilungs-Agent, der auf dem Abonnenten ausgeführt wird.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)auf dem Verleger unter Angabe von **@publisher**, **@publisher_db**, **@publication**, den Namen der Sicherheitseigenschaft für **@property**und den neuen Wert der Eigenschaft für **@value**.  
  
3.  Wiederholen Sie Schritt 2 für jede der folgenden Sicherheitseigenschaften, die geändert wird:  
  
    -   Geben Sie den Wert **distrib_job_password** für **@property** und ein neues Kennwort für **@value**. Wenn Sie das Konto ändern, wiederholen Sie Schritt 2, und geben Sie den Wert **distrib_job_login** für **@property** und das neue Windows-Konto für **@value**.  
  
    -   Um den zum Herstellen der Verbindung mit dem Verteiler verwendeten Sicherheitsmodus zu ändern, geben Sie den Wert **distributor_security_mode** für **@property** und den Wert **1** (integrierte Windows-Authentifizierung) oder **0** (SQL Server-Authentifizierung) für **@value**.  
  
    -   Wenn Sie den Sicherheitsmodus für den Verteiler in die SQL Server-Authentifizierung oder die Anmeldeinformationen für die SQL Server-Authentifizierung ändern, geben Sie den Wert **distributor_password** für **@property** und das neue Kennwort für **@value**. Wiederholen Sie Schritt 2, und geben Sie dabei den Wert **distributor_login** für **@property** und den neuen Anmeldenamen für **@value**.  
  
    > [!NOTE]  
    >  Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>So ändern Sie die Sicherheitseinstellungen für den Merge-Agent eines Pushabonnements  
  
1.  Führen Sie [sp_helpmergesubscription](../../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)auf dem Verleger unter Angabe von **@publication**, **@subscriber**und **@subscriber_db**. Damit werden die Abonnementeigenschaften zurückgegeben, einschließlich der Sicherheitseinstellungen für den Merge-Agent, der auf dem Verteiler ausgeführt wird.  
  
2.  Führen Sie [sp_changemergesubscription](../../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)auf dem Verleger unter Angabe von **@publication**, **@subscriber**, **@subscriber_db**, den Namen der Sicherheitseigenschaft für **@property**und den neuen Wert der Eigenschaft für **@value**.  
  
3.  Wiederholen Sie Schritt 2 für jede der folgenden Sicherheitseigenschaften, die geändert wird:  
  
    -   Geben Sie den Wert **merge_job_password** für **@property** und ein neues Kennwort für **@value**. Wenn Sie das Konto ändern, wiederholen Sie Schritt 2, und geben Sie den Wert **merge_job_login** für **@property** und das neue Windows-Konto für **@value**.  
  
    -   Um den zum Herstellen der Verbindung mit dem Abonnenten verwendeten Sicherheitsmodus zu ändern, geben Sie den Wert **subscriber_security_mode** für **@property** und den Wert **1** (integrierte Windows-Authentifizierung) oder **0** (SQL Server-Authentifizierung) für **@value**.  
  
    -   Wenn Sie den Sicherheitsmodus für den Abonnenten in die SQL Server-Authentifizierung oder die Anmeldeinformationen für die SQL Server-Authentifizierung ändern, geben Sie den Wert **subscriber_password** für **@property** und das neue Kennwort für **@value**. Wiederholen Sie Schritt 2, und geben Sie dabei den Wert **subscriber_login** für **@property** und den neuen Anmeldenamen für **@value**.  
  
    -   Zum Ändern des Sicherheitsmodus, der beim Herstellen einer Verbindung mit dem Verleger verwendet wird, geben Sie den Wert **publisher_security_mode** für **@property** und den Wert **1** (integrierte Windows-Authentifizierung) oder **0** (SQL Server-Authentifizierung) für **@value**.  
  
    -   Wenn Sie den Sicherheitsmodus für den Verleger in die SQL Server-Authentifizierung oder die Anmeldeinformationen für die SQL Server-Authentifizierung ändern, geben Sie den Wert **publisher_password** für **@property** und das neue Kennwort für **@value**. Wiederholen Sie Schritt 2, und geben Sie dabei den Wert **publisher_login** für **@property** und den neuen Anmeldenamen für **@value**.  
  
    > [!NOTE]  
    >  Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Eigenschaften einschließlich **merge_job_login** und **merge_job_password**bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>So ändern Sie die Sicherheitseinstellungen für den Merge-Agent eines Pullabonnements  
  
1.  Führen Sie auf dem Abonnenten [sp_helpmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)auf dem Verleger unter Angabe von **@publication**. Damit werden die Abonnementeigenschaften zurückgegeben, einschließlich der Sicherheitseinstellungen für den Merge-Agent, der auf dem Abonnenten ausgeführt wird.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)auf dem Verleger unter Angabe von **@publisher**, **@publisher_db**, **@publication**, den Namen der Sicherheitseigenschaft für **@property**und den neuen Wert der Eigenschaft für **@value**.  
  
3.  Wiederholen Sie Schritt 2 für jede der folgenden Sicherheitseigenschaften, die geändert wird:  
  
    -   Geben Sie den Wert **merge_job_password** für **@property** und ein neues Kennwort für **@value**. When changing the account itself, repeat Step 2 specifying a value of **merge_job_login** für **@property** und das neue Windows-Konto für **@value**.  
  
    -   Um den zum Herstellen der Verbindung mit dem Verteiler verwendeten Sicherheitsmodus zu ändern, geben Sie den Wert **distributor_security_mode** für **@property** und den Wert **1** (integrierte Windows-Authentifizierung) oder **0** (SQL Server-Authentifizierung) für **@value**.  
  
    -   Wenn Sie den Sicherheitsmodus für den Verteiler in die SQL Server-Authentifizierung oder die Anmeldeinformationen für die SQL Server-Authentifizierung ändern, geben Sie den Wert **distributor_password** für **@property** und das neue Kennwort für **@value**. Wiederholen Sie Schritt 2, und geben Sie dabei den Wert **distributor_login** für **@property** und den neuen Anmeldenamen für **@value**.  
  
    -   Zum Ändern des Sicherheitsmodus, der beim Herstellen einer Verbindung mit dem Verleger verwendet wird, geben Sie den Wert **publisher_security_mode** für **@property** und den Wert **1** (integrierte Windows-Authentifizierung) oder **0** (SQL Server-Authentifizierung) für **@value**.  
  
    -   Wenn Sie den Sicherheitsmodus für den Verleger in die SQL Server-Authentifizierung oder die Anmeldeinformationen für die SQL Server-Authentifizierung ändern, geben Sie den Wert **publisher_password** für **@property** und das neue Kennwort für **@value**. Wiederholen Sie Schritt 2, und geben Sie dabei den Wert **publisher_login** für **@property** und den neuen Anmeldenamen für **@value**.  
  
    > [!NOTE]  
    >  Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent-to-generate-a-filtered-snapshot-for-a-subscriber"></a>So ändern Sie die Sicherheitseinstellungen für den Momentaufnahme-Agent zum Generieren einer gefilterten Momentaufnahme für einen Abonnenten  
  
1.  Führen Sie [sp_helpdynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)auf dem Verleger unter Angabe von **@publication**. Notieren Sie den Wert **job_name** im Resultset für die zu ändernde Partition des Abonnenten.  
  
2.  Führen Sie [sp_changedynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md)auf dem Verleger unter Angabe von **@publication**, den in Schritt 1 abgerufenen Wert für **@dynamic_snapshot_jobname**und ein neues Kennwort für **@job_password** oder den Anmeldenamen und das Kennwort für das Windows-Konto, unter dem der Agent ausgeführt wird, für **@job_login** und **@job_password**.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Parameter, einschließlich *job_login* und *job_password*, bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-queue-reader-agent"></a>So ändern Sie die Sicherheitseinstellungen für den Warteschlangenlese-Agent  
  
1.  Führen Sie auf dem Verteiler [sp_helpqreader_agent](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)aus. Damit wird das aktuelle Windows-Konto zurückgegeben, unter dem der Warteschlangenlese-Agent ausgeführt wird.  
  
    -   Führen Sie auf dem Verteiler [sp_changeqreader_agent](../../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md)aus, und geben Sie dabei die Einstellungen des Windows-Kontos für **@job_login** und **@job_passwsord**.  
  
    > [!NOTE]  
    >  Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten. Es gibt einen Warteschlangenlese-Agent für jede Verteilungsdatenbank. Wenn Sie die Sicherheitseinstellungen eines Agents ändern, wirkt sich dies auf alle Veröffentlichungen auf allen Verlegern aus, die diese Verteilungsdatenbank verwenden.  
  
2.  Der Warteschlangenlese-Agent verwendet zum Herstellen von Verbindungen mit dem Abonnenten denselben Verbindungskontext wie der Verteilungs-Agent für das Abonnement.  
  
#### <a name="to-change-security-mode-used-by-an-immediate-updating-subscriber-when-connecting-to-the-publisher"></a>So ändern Sie den Sicherheitsmodus, der von einem Abonnenten mit sofortigem Update beim Herstellen einer Verbindung mit dem Verleger verwendet wird  
  
1.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)aus. Geben Sie **@publisher**, **@publication**, den Namen der Veröffentlichungsdatenbank für **@publisher_db**und einen der folgenden Werte für **@security_mode**an:  
  
    -   **0** zum Verwenden der SQL Server-Authentifizierung, wenn Updates beim Verleger vorgenommen werden. Diese Option erfordert auf dem Verleger die Angabe gültiger Anmeldeinformationen für **@login** und **@password**.  
  
    -   **1** , um den Sicherheitskontext des Benutzers zu verwenden, der Änderungen am Abonnenten vornimmt, wenn eine Verbindung mit dem Verleger hergestellt wird. Weitere Informationen zu den in Verbindung mit diesem Sicherheitsmodus geltenden Beschränkungen finden Sie unter [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) .  
  
    -   **2** Verwenden Sie einen vorhandenen benutzerdefinierten Anmeldenamen für den Verbindungsserver, der mit [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)erstellt wurde.  
  
#### <a name="to-change-the-password-for-a-remote-distributor"></a>So ändern Sie das Kennwort für einen Remoteverteiler  
  
1.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md)aus, und geben Sie dabei das neue Kennwort dieses Anmeldenamens für **@password**.  
  
    > [!IMPORTANT]  
    >  Ändern Sie das Kennwort für **distributor_admin** nicht direkt.  
  
2.  Führen Sie auf jedem Verteiler, der diesen Remoteverteiler verwendet, [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md)aus, und geben Sie dabei das Kennwort aus Schritt 1 für **@password**.  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen speichern müssen, verwenden Sie die [Kryptografiedienste](http://go.microsoft.com/fwlink/?LinkId=34733) von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows .NET Framework.  
  
#### <a name="to-change-all-instances-of-a-password-stored-on-a-replication-server"></a>So ändern Sie alle Instanzen eines auf einem Replikationsserver gespeicherten Kennworts  
  
1.  Erstellen Sie mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse eine Verbindung mit dem Replikationsserver.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationServer> -Klasse, und verwenden Sie hierzu die Verbindung aus Schritt 1.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> -Methode auf. Geben Sie die folgenden Parameter an:  
  
    -   *security_mode* &ndash; Ein <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> -Wert, der den Typ der Authentifizierung angibt, für die alle Instanzen des Kennworts geändert werden.  
  
    -   *login* &ndash; Die Anmeldung, für die alle Instanzen des Kennworts geändert werden.  
  
    -   *password* &ndash; Der neue Kennwortwert.  
  
        > [!IMPORTANT]  
        >  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen speichern müssen, verwenden Sie die [Kryptografiedienste](http://go.microsoft.com/fwlink/?LinkId=34733) von Windows .NET Framework.  
  
        > [!NOTE]  
        >  Nur ein Mitglied der festen Serverrolle **sysadmin** kann diese Methode aufrufen.  
  
4.  Wiederholen Sie Schritte 1 bis 3 für jeden Server in der Replikationstopologie, in der das Kennwort aktualisiert werden muss.  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription-to-a-transactional-publication"></a>So ändern Sie die Sicherheitseinstellungen für den Verteilungs-Agent für ein Pushabonnement einer Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransSubscription> -Klasse.  
  
3.  Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>und <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> für das Abonnement und die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft fest.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, wurden entweder die Abonnementeigenschaften in Schritt 3 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
5.  Legen Sie eine oder mehrere der folgenden Sicherheitseigenschaften für die Instanz von <xref:Microsoft.SqlServer.Replication.TransSubscription>fest:  
  
    -   Um die Anmeldeinformationen für das Windows-Konto zu ändern, unter dem der Agent ausgeführt wird, legen Sie das <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> -Feld und das <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> -Feld von <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>fest.  
  
    -   Zur Angabe der integrierten Windows-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Abonnenten verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> -Eigenschaft auf **true**.  
  
    -   Zur Angabe der integrierten SQL Server-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Abonnenten verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> -Eigenschaft auf **false**fest, und geben Sie die Anmeldeinformationen des Abonnenten in den Feldern <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> an.  
  
        > [!NOTE]  
        >  Die Agent-Verbindung zum Verteiler wird immer mit den durch <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>angegebenen Windows-Anmeldeinformationen hergestellt. Dieses Konto wird auch verwendet, um Remoteverbindungen unter Verwendung der Windows-Authentifizierung herzustellen.  
  
6.  (Optional) Wenn Sie den Wert **true** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>angegeben haben, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> -Methode auf, um die Änderungen auf dem Server einzutragen. Wenn Sie den Wert **false** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (die Standardeinstellung) angegeben haben, werden die Änderungen sofort an den Server gesendet.  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription-to-a-transactional-publication"></a>So ändern Sie die Sicherheitseinstellungen für den Verteilungs-Agent für ein Pullabonnement einer Transaktionsveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransPullSubscription> -Klasse.  
  
3.  Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>und <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> für das Abonnement und die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft fest.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, wurden entweder die Abonnementeigenschaften in Schritt 3 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
5.  Legen Sie eine oder mehrere der folgenden Sicherheitseigenschaften für die Instanz von <xref:Microsoft.SqlServer.Replication.TransPullSubscription>fest:  
  
    -   Um die Anmeldeinformationen für das Windows-Konto zu ändern, unter dem der Agent ausgeführt wird, legen Sie das <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> -Feld und das <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> -Feld von <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>fest.  
  
    -   Zur Angabe der integrierten Windows-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Verteiler verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> -Eigenschaft auf **true**.  
  
    -   Zur Angabe der SQL Server-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Verteiler verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> -Eigenschaft auf **false**fest, und geben Sie die Anmeldeinformationen des Verteilers in den Feldern <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> an.  
  
        > [!NOTE]  
        >  Die Agent-Verbindung zum Abonnenten wird immer mit den durch <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>angegebenen Windows-Anmeldeinformationen hergestellt. Dieses Konto wird auch verwendet, um Remoteverbindungen unter Verwendung der Windows-Authentifizierung herzustellen.  
  
6.  (Optional) Wenn Sie den Wert **true** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>angegeben haben, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> -Methode auf, um die Änderungen auf dem Server einzutragen. Wenn Sie den Wert **false** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (die Standardeinstellung) angegeben haben, werden die Änderungen sofort an den Server gesendet.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription-to-a-merge-publication"></a>So ändern Sie die Sicherheitseinstellungen für den Merge-Agent für ein Pullabonnement einer Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePullSubscription> -Klasse.  
  
3.  Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>und <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> für das Abonnement und die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft fest.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, wurden entweder die Abonnementeigenschaften in Schritt 3 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
5.  Legen Sie eine oder mehrere der folgenden Sicherheitseigenschaften für die Instanz von <xref:Microsoft.SqlServer.Replication.MergePullSubscription>fest:  
  
    -   Um die Anmeldeinformationen für das Windows-Konto zu ändern, unter dem der Agent ausgeführt wird, legen Sie das <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> -Feld und das <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> -Feld von <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>fest.  
  
    -   Zur Angabe der integrierten Windows-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Verteiler verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> -Eigenschaft auf **true**.  
  
    -   Zur Angabe der SQL Server-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Verteiler verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> -Eigenschaft auf **false**fest, und geben Sie die Anmeldeinformationen des Verteilers in den Feldern <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> an.  
  
    -   Zur Angabe der integrierten Windows-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Verleger verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> -Eigenschaft auf **true**.  
  
    -   Zur Angabe der integrierten SQL Server-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Verleger verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> -Eigenschaft auf **false**fest, und geben Sie die Anmeldeinformationen des Verlegers in den Feldern <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> an.  
  
        > [!NOTE]  
        >  Die Agent-Verbindung zum Abonnenten wird immer mit den durch <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>angegebenen Windows-Anmeldeinformationen hergestellt. Dieses Konto wird auch verwendet, um Remoteverbindungen unter Verwendung der Windows-Authentifizierung herzustellen.  
  
6.  (Optional) Wenn Sie den Wert **true** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>angegeben haben, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> -Methode auf, um die Änderungen auf dem Server einzutragen. Wenn Sie den Wert **false** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (die Standardeinstellung) angegeben haben, werden die Änderungen sofort an den Server gesendet.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription-to-a-merge-publication"></a>So ändern Sie die Sicherheitseinstellungen für den Merge-Agent für ein Pushabonnement einer Mergeveröffentlichung  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeSubscription> -Klasse.  
  
3.  Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>und <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> für das Abonnement und die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft fest.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, wurden entweder die Abonnementeigenschaften in Schritt 3 falsch definiert, oder das Abonnement ist nicht vorhanden.  
  
5.  Legen Sie eine oder mehrere der folgenden Sicherheitseigenschaften für die Instanz von <xref:Microsoft.SqlServer.Replication.MergeSubscription>fest:  
  
    -   Um die Anmeldeinformationen für das Windows-Konto zu ändern, unter dem der Agent ausgeführt wird, legen Sie das <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> -Feld und das <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> -Feld von <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>fest.  
  
    -   Zur Angabe der integrierten Windows-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Abonnenten verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> -Eigenschaft auf **true**.  
  
    -   Zur Angabe der integrierten SQL Server-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Abonnenten verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> -Eigenschaft auf **false**fest, und geben Sie die Anmeldeinformationen des Abonnenten in den Feldern <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> an.  
  
    -   Zur Angabe der integrierten Windows-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Verleger verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> -Eigenschaft auf **true**.  
  
    -   Zur Angabe der integrierten SQL Server-Authentifizierung als Authentifizierungstyp, der vom Agent zum Verbindungsaufbau mit dem Verleger verwendet wird, legen Sie das <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> -Feld der <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> -Eigenschaft auf **false**fest, und geben Sie die Anmeldeinformationen des Verlegers in den Feldern <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A> und <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> an.  
  
        > [!NOTE]  
        >  Die Agent-Verbindung zum Verteiler wird immer mit den durch <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>angegebenen Windows-Anmeldeinformationen hergestellt. Dieses Konto wird auch verwendet, um Remoteverbindungen unter Verwendung der Windows-Authentifizierung herzustellen.  
  
6.  (Optional) Wenn Sie den Wert **true** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>angegeben haben, rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> -Methode auf, um die Änderungen auf dem Server einzutragen. Wenn Sie den Wert **false** für <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (die Standardeinstellung) angegeben haben, werden die Änderungen sofort an den Server gesendet.  
  
#### <a name="to-change-the-login-information-used-by-an-immediate-updating-subscriber-when-it-connects-to-the-transactional-publisher"></a>So ändern Sie die Anmeldeinformationen, die von einem sofort aktualisierbaren Abonnenten beim Herstellen einer Verbindung mit dem Transaktionsverleger verwendet werden  
  
1.  Erstellen Sie eine Verbindung mit dem Abonnenten, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> -Klasse für die Abonnementdatenbank. Geben Sie <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> und die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>an.  
  
3.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> -Methode auf, um die Eigenschaften des Objekts abzurufen. Wenn diese Methode **false**zurückgibt, wurden entweder die Datenbankeigenschaften in Schritt 2 falsch definiert, oder das Abonnementdatenbank ist nicht vorhanden.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> -Methode auf, und übergeben Sie hierbei die folgenden Parameter:  
  
    -   *Publisher* &ndash; Den Namen des Verlegers.  
  
    -   *PublisherDB* &ndash; Den Namen der Veröffentlichungsdatenbank.  
  
    -   *Publication* &ndash; Den Name der Veröffentlichung, die der sofort aktualisierbare Abonnent abonniert hat.  
  
    -   *Distributor* &ndash; Den Namen des Verteilers.  
  
    -   *PublisherSecurity* - A <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> -Objekt, das den Typ des Sicherheitsmodus, der vom sofort aktualisierbaren Abonnenten beim Verbindungsaufbau mit dem Verleger verwendet wird, und die Anmeldeinformationen für die Verbindung angibt.  
  
###  <a name="PShellExample"></a> Beispiel (RMO)  
 In diesem Beispiel werden der für die Anmeldung angegebene Wert überprüft und alle auf dem Server für die Replikation gespeicherten Kennwörter für die angegebene Windows-Anmeldung bzw. SQL Server-Anwendung geändert.  
  
 [!code-cs[HowTo#rmo_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Ändern der Replikationssicherheitseinstellungen  
 Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
## <a name="see-also"></a>Siehe auch  
 [Konzepte für Replikationsverwaltungsobjekte (RMO)](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Aktualisieren von Replikationsskripts &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Sicherheitsmodell des Replikations-Agents](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicherheit und Schutz &#40;Replikation&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
