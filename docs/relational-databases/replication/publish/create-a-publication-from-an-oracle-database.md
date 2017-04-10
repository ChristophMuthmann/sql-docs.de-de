---
title: "Erstellen einer Ver&#246;ffentlichung aus einer Oracle-Datenbank | Microsoft Docs"
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
  - "Veröffentlichungen [SQL Server-Replikation], Oracle-Datenbanken"
  - "Veröffentlichungen mit Oracle [SQL Server-Replikation], konfigurieren"
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Erstellen einer Ver&#246;ffentlichung aus einer Oracle-Datenbank
  In diesem Thema wird beschrieben, wie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]eine Veröffentlichung aus einer Oracle-Datenbank erstellt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
-   **So erstellen Sie eine Veröffentlichung aus einer Oracle-Datenbank mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Voraussetzung für das Erstellen einer Veröffentlichung aus einer Oracle-Datenbank ist, dass die Oracle-Software auf dem [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler installiert ist und die Oracle-Datenbank konfiguriert wurde. Weitere Informationen finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Sie können mithilfe des Assistenten für neue Veröffentlichung eine Momentaufnahme- bzw. eine Transaktionsveröffentlichung aus einer Oracle-Datenbank erstellen.  
  
 Wenn Sie zum ersten Mal eine Veröffentlichung aus einer Oracle-Datenbank erstellen, müssen Sie den Oracle-Verleger auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verteiler identifizieren (für nachfolgende Veröffentlichungen aus derselben Datenbank ist dies nicht mehr erforderlich). Identifizieren den Oracle-Verleger kann erreicht werden, den Assistenten für neue Veröffentlichung oder **Verteilereigenschaften - \< Verteiler>** Dialogfeld; in diesem Thema zeigt die **Verteilereigenschaften - \< Verteiler>** (Dialogfeld).  
  
#### So identifizieren Sie den Oracle-Verleger auf dem SQL Server-Verteiler  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]eine Verbindung mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz her, die der Oracle-Verleger als Verteiler verwenden wird. Erweitern Sie dann den Serverknoten.  
  
2.  Mit der rechten Maustaste die **Replikation** Ordner, und klicken Sie dann auf **Verteilereigenschaften**.  
  
3.  Auf der **Herausgeber** auf der Seite der **Verteilereigenschaften - \< Verteiler>** im Dialogfeld klicken Sie auf **Hinzufügen**, und klicken Sie dann auf **Oracle-Verleger hinzufügen**.  
  
4.  Klicken Sie im Dialogfeld **Verbindung mit Server herstellen** auf die Schaltfläche **Optionen** .  
  
5.  Gehen Sie auf der Registerkarte **Anmeldung** wie folgt vor:  
  
    1.  Geben Sie den Namen der Oracle-Datenbankinstanz ein, oder wählen Sie im Kombinationsfeld **Serverinstanz** den Eintrag **Suche fortsetzen** aus.  
  
    2.  Wählen Sie **Oracle-Standardauthentifizierung** (empfohlen) oder **Windows-Authentifizierung**.  
  
         Bei Auswahl von **Windows-Authentifizierung**: der Oracle-Server muss zum Zulassen von Verbindungen mit Windows-Anmeldeinformationen konfiguriert werden (Weitere Informationen finden Sie in der Oracle-Dokumentation.) und Sie müssen angemeldet sein identisch [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Konto, die Sie für das Schema des administrativen replikationsbenutzers angegeben haben.  
  
    3.  Wenn Sie sich für **Oracle-Standardauthentifizierung**entschieden haben, geben Sie den Anmeldenamen und das Kennwort für das Schema für den administrativen Replikationsbenutzer ein, das Sie beim Konfigurieren auf dem Oracle-Verleger erstellt haben.  
  
6.  Wählen Sie auf der Registerkarte **Verbindungseigenschaften** als Verlegertyp **Gateway** oder **Vollständig**aus.  
  
     Mithilfe der Option **Vollständig** kann für Momentaufnahme- und Transaktionsveröffentlichungen der vollständige Satz an unterstützten Funktionen für Oracle-Veröffentlichungen verfügbar gemacht werden. Die Option **Gateway** bietet spezielle Designoptimierungen, um die Leistung in Fällen zu verbessern, in denen die Replikation als Gateway zwischen Systemen verwendet wird. Sie können die Option **Gateway** nicht verwenden, wenn Sie planen, dieselbe Tabelle in mehreren Transaktionsveröffentlichungen zu veröffentlichen. Wenn Sie **Gateway**auswählen, kann eine Tabelle höchstens in einer Transaktionsveröffentlichung und in einer beliebigen Zahl an Momentaufnahmeveröffentlichungen erscheinen.  
  
7.  Klicken Sie auf **Verbinden**. Es wird eine Verbindung mit dem Oracle-Verleger hergestellt, und die Verbindung wird für die Replikation konfiguriert. Die **mit Server verbinden** Dialogfeld wird geschlossen, und Sie kehren zum der **Verteilereigenschaften - \< Verteiler>** (Dialogfeld).  
  
    > [!NOTE]  
    >  Falls bei der Netzwerkkonfiguration Probleme auftreten, wird jetzt eine Fehlermeldung angezeigt. Wenn Sie Probleme haben, eine Verbindung mit der Oracle-Datenbank herzustellen, finden Sie entsprechende Informationen in dem Abschnitt in [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md), der sich mit Verbindungsproblemen zwischen dem SQL Server-Verteiler und der Oracle-Datenbankinstanz beschäftigt.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### So erstellen Sie eine Veröffentlichung aus einer Oracle-Datenbank  
  
1.  Stellen Sie eine Verbindung mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz her, die der Oracle-Verleger als Verteiler verwenden wird. Erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** .  
  
3.  Mit der rechten Maustaste die **lokale Publikationen** Ordner, und klicken Sie dann auf **Neue Oracle-Veröffentlichung**.  
  
4.  Wählen Sie auf der Seite **Oracle-Verleger** des Assistenten für neue Veröffentlichung den Oracle-Verleger aus. Wenn der Oracle-Verleger nicht angezeigt wird, klicken Sie auf **Oracle-Verleger hinzufügen**. Führen Sie dann die in der vorherigen Prozedur beschriebenen Schritte aus.  
  
5.  Wählen Sie auf der Seite **Veröffentlichungstyp** entweder **Momentaufnahmeveröffentlichung** oder **Transaktionsveröffentlichung**aus.  
  
6.  Wählen Sie auf der Seite **Artikel** die Datenbankobjekte aus, die Sie veröffentlichen möchten.  
  
     Optional können Sie auch Tabellenspalten herausfiltern, indem Sie eine Tabelle erweitern und dann die Kontrollkästchen für die Spalten deaktivieren, die nicht einbezogen werden sollen. Klicken Sie auf **Artikeleigenschaften** , um die Artikeleigenschaften anzuzeigen und zu ändern und um bei Bedarf alternative Datentypzuordnungen anzugeben. Weitere Informationen zu datentypzuordnungen finden Sie unter [Angeben der Datentypzuordnungen für einen Oracle-Verleger](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md).  
  
7.  Wenden Sie bei Bedarf auf der Seite **Tabellenzeilen filtern** Filter an, um nur bestimmte Daten aus einer oder mehreren Tabellen zu veröffentlichen.  
  
8.  Deaktivieren Sie auf der Seite **Momentaufnahme-Agent** nur dann die Option **Momentaufnahme sofort erstellen** , wenn Sie alle Objekte erstellt und alle erforderlichen Daten der Abonnementdatenbank hinzugefügt haben.  
  
9. Auf der **-Agent-Sicherheit** Seite, geben Sie Anmeldeinformationen für den Snapshot-Agent (für alle Veröffentlichungen) und der Protokolllese-Agent (für transaktionsveröffentlichungen). Die Agents werden ausgeführt und stellen mithilfe des von Ihnen angegebenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Windows-Kontos Verbindungen zum [!INCLUDE[msCoName](../../../includes/msconame-md.md)] -Verteiler her. Für die Verbindungen zur Oracle-Datenbank verwenden die Agents den Kontext des Kontos, das Sie als Schema für den administrativen Replikationsbenutzer angegeben haben. Weitere Informationen finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
     Weitere Informationen zu den erforderlichen Berechtigungen für die einzelnen Agents finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) und [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
10. Erstellen Sie optional auf der Seite **Aktionen des Assistenten** ein Skript für die Veröffentlichung. Weitere Informationen finden Sie unter [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
11. Geben Sie auf der Seite **Assistenten abschließen** einen Namen für die Veröffentlichung an.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Nachdem eine Oracle-Datenbank als Verleger konfiguriert wurde, können Sie mit gespeicherten Systemprozeduren auf die gleiche Weise wie bei Verwendung eines [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verlegers eine Transaktions- oder Momentaufnahmeveröffentlichung erstellen.  
  
#### So erstellen Sie eine Oracle-Veröffentlichung  
  
1.  Konfigurieren Sie die Oracle-Datenbank als Verleger. Weitere Informationen finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
2.  Wenn kein Remoteverteiler vorhanden ist, konfigurieren Sie den Remoteverteiler. Weitere Informationen finden Sie unter [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
3.  Führen Sie auf dem Remoteverteiler, der vom Oracle-Verleger verwendet wird, [Sp_adddistpublisher & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md). Geben Sie den Transparent Network Substrate (TNS) Namen der Oracle-Datenbankinstanz für **@publisher** und einem Wert von **ORACLE** oder **ORACLE GATEWAY** für **@publisher_type**. `Specify` : Geben Sie den beim Herstellen der Verbindung vom Oracle-Verleger zum Remote- [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler verwendeten Sicherheitsmodus auf eine der folgenden Arten an:  
  
    -   Geben Sie mithilfe von Oracle-Standardauthentifizierung standardmäßig den Wert **0** für **@security_mode**, den Benutzernamen für das Schema für Administrator Sie auf dem Oracle-Verleger, während der Konfiguration für erstellt **@login**, und das Kennwort für **@password**.  
  
        > [!IMPORTANT]  
        >  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen in einer Skriptdatei speichern, müssen Sie die Datei schützen, um unberechtigtem Zugriff vorzubeugen.  
  
    -   Um Windows-Authentifizierung verwenden, geben Sie den Wert **1** für **@security_mode**.  
  
        > [!NOTE]  
        >  Für die Verwendung der Windows-Authentifizierung muss der Oracle-Server so konfiguriert werden, dass Verbindungen mithilfe von Windows-Anmeldeinformationen möglich sind (weitere Informationen dazu finden Sie in der Oracle-Dokumentation). Darüber hinaus müssen Sie aktuell mit demselben Microsoft Windows-Konto angemeldet sein, das Sie für das Schema für den administrativen Replikationsbenutzer angegeben haben.  
  
4.  Erstellen Sie einen Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank.  
  
    -   Wenn Sie unsicher sind, ob ein Protokolllese-Agent-Auftrag für eine veröffentlichte Datenbank vorhanden ist, führen Sie [Sp_helplogreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) auf dem Verteiler, die vom Oracle-Verleger für die Verteilungsdatenbank verwendet. Geben Sie den Namen des Oracle-Verlegers für **@publisher**an. Wenn das Resultset leer ist, muss ein Protokolllese-Agentauftrag erstellt werden.  
  
    -   Wenn ein Protokolllese-Agentauftrag für die Veröffentlichungsdatenbank bereits vorhanden ist, fahren Sie mit Schritt 5 fort.  
  
    -   Führen Sie auf dem Verteiler verwendet, die vom Oracle-Verleger für die Verteilungsdatenbank [Sp_addlogreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Geben Sie die Windows-Anmeldeinformationen, unter dem der Agent ausgeführt, für wird **@job_login** und **@job_password**.  
  
        > [!NOTE]  
        >  Die **@job_login** Parameter muss mit den in Schritt 3 angegebenen Anmeldeinformationen übereinstimmen. Geben Sie keine Sicherheitsinformationen zum Verleger an. Der Protokolllese-Agent stellt mit den in Schritt 3 bereitgestellten Sicherheitsinformationen eine Verbindung mit dem Verleger her.  
  
5.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_addpublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) um die Veröffentlichung zu erstellen. Weitere Informationen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
6.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Geben Sie den Namen der Veröffentlichung in Schritt 4 verwendet **@publication** und die Windows-Anmeldeinformationen, unter denen der Snapshot-Agent ausgeführt, für die wird **@job_name** und **@password**. Um die Oracle-Standardauthentifizierung beim Verbinden mit dem Verleger zu verwenden, müssen Sie auch den Wert angeben **0** für **@publisher_security_mode** und die Oracle-Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt.  
  
## Siehe auch  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Konfigurieren des Transaktionssatz-Auftrags für einen Oracle-Verleger & #40. Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/administration/configure the transaction set job for an oracle publisher.md)   
 [Veröffentlichungen mit Oracle (Übersicht)](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)   
 [Skript zum Erteilen von Oracle-Berechtigungen](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)  
  
  