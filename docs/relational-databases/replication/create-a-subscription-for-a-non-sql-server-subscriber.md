---
title: "Erstellen eines Abonnements f&#252;r einen Nicht-SQL Server-Abonnenten | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Abonnements [SQL Server-Replikation], Nicht-SQL Server-Abonnenten"
  - "Abonnenten [SQL Server-Replikation], Nicht-SQL Server-Abonnenten"
  - "Nicht-SQL Server-Abonnenten, Abonnements"
ms.assetid: 5020ee68-b988-4d57-8066-67d183e61237
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Erstellen eines Abonnements f&#252;r einen Nicht-SQL Server-Abonnenten
  In diesem Thema wird beschrieben, wie ein Abonnement für einen Nicht-SQL Server-Abonnenten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] erstellt wird. Von der Transaktionsreplikation und der Momentaufnahmereplikation wird das Veröffentlichen von Daten auf Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten unterstützt. Informationen zu den unterstützten abonnentenplattformen finden Sie unter [nicht-SQL Server-Abonnenten](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
 **In diesem Thema**  
  
-   **So erstellen Sie ein Abonnement für einen Nicht-SQL Server-Abonnenten mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 So erstellen Sie ein Abonnement für einen Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten  
  
1.  Nehmen Sie die Installation und Konfiguration der entsprechenden Clientsoftware und OLE DB-Anbieter auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verteiler vor. Weitere Informationen finden Sie unter [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) und [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
2.  Erstellen Sie mithilfe des Assistenten für neue Veröffentlichung eine Veröffentlichung. Weitere Informationen zum Erstellen von Veröffentlichungen finden Sie unter [Erstellen Sie eine Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md) und [Erstellen einer Veröffentlichung aus einer Oracle-Datenbank](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md). Geben Sie im Assistenten für neue Veröffentlichung folgende Optionen an:  
  
    -   Wählen Sie auf der Seite **Veröffentlichungstyp** entweder **Momentaufnahmeveröffentlichung** oder **Transaktionsveröffentlichung**aus.  
  
    -   Heben Sie auf der Seite **Momentaufnahme-Agent** die Auswahl von **Momentaufnahme sofort erstellen**auf.  
  
         Die Erstellung der Momentaufnahme erfolgt nach der Aktivierung der Veröffentlichung für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten, um sicherzustellen, dass der Momentaufnahme-Agent eine Momentaufnahme und Initialisierungsskripts generiert, die für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten geeignet sind.  
  
3.  Aktivieren Sie die Veröffentlichung für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten mithilfe der **Veröffentlichungseigenschaften - \< PublicationName>** das Dialogfeld. Weitere Informationen zu diesem Schritt finden Sie unter [Publication Properties, Subscription Options](../../relational-databases/replication/publication-properties-subscription-options.md) .  
  
4.  Erstellen Sie mithilfe des Assistenten für neue Abonnements ein Abonnement. In diesem Thema sind weitere Informationen zu diesem Schritt enthalten.  
  
5.  (Optional) Ändern der **Pre_creation_cmd** Artikeleigenschaft, um Tabellen auf dem Abonnenten beizubehalten. In diesem Thema sind weitere Informationen zu diesem Schritt enthalten.  
  
6.  Generieren Sie eine Momentaufnahme für die Veröffentlichung. In diesem Thema sind weitere Informationen zu diesem Schritt enthalten.  
  
7.  Synchronisieren Sie das Abonnement. Weitere Informationen finden Sie unter [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### So aktivieren Sie eine Veröffentlichung für Nicht-SQL Server-Abonnenten  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Maustaste auf die Publikation, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Auf der **Abonnementoptionen** Seite, wählen Sie einen Wert von **True** für die Option **nicht - SQL Server-Abonnenten zulassen**. Beim Auswählen dieser Option werden eine Reihe von Eigenschaften so geändert, dass die Veröffentlichung mit Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten kompatibel ist.  
  
    > [!NOTE]  
    >  Auswählen von **True** legt den Wert für die **Pre_creation_cmd** Artikeleigenschaft auf 'drop'. Mit dieser Einstellung wird angegeben, dass bei der Replikation auf dem Abonnenten eine Tabelle gelöscht werden soll, wenn sie mit dem Namen der Tabelle in dem Artikel übereinstimmt. Wenn Sie Tabellen auf dem Abonnenten vorhanden sind, die Sie beibehalten möchten, verwenden Sie die [Sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) für jeden Artikel die gespeicherte Prozedur; geben Sie den Wert 'none' für **Pre_creation_cmd**: `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Sie werden zur Erstellung einer neuen Momentaufnahme für die Veröffentlichung aufgefordert. Wenn Sie diesen Vorgang lieber zu einem späteren Vorgang ausführen möchten, verwenden Sie hierzu die nachfolgend aufgeführten schrittweisen Anweisungen.  
  
#### So erstellen Sie ein Abonnement für einen Nicht-SQL Server-Abonnenten  
  
1.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
2.  Mit der rechten Maustaste in der entsprechenden Veröffentlichung, und klicken Sie dann auf **neue Abonnements**.  
  
3.  Vergewissern Sie sich, dass auf der Seite **Speicherort des Verteilungs-Agents** die Option **Alle Agents auf dem Verteiler ausführen** aktiviert ist. Von Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten wird das Ausführen von Agents auf dem Abonnenten nicht unterstützt.  
  
4.  Auf der **Abonnenten** auf **-Abonnenten hinzufügen** und klicken Sie dann auf **nicht-SQL Server-Abonnenten hinzufügen**.  
  
5.  In der **nicht-SQL Server-Abonnenten hinzufügen** Dialogfeld Wählen Sie den Typ des Abonnenten.  
  
6.  Geben Sie im Feld **Datenquellenname**einen Wert ein:  
  
    -   Bei Oracle ist dies der von Ihnen konfigurierte Transparent Network Substrate-(TNS-)Name.  
  
    -   Bei IBM kann dies ein beliebiger Name sein. Im Normalfall wird die Netzwerkadresse des Abonnenten angegeben.  
  
     Der in diesem Schritt eingegebene Datenquellenname und die in Schritt 9 angegebenen Anmeldeinformationen werden von diesem Assistenten nicht überprüft. Sie werden von der Replikation nicht verwendet, bis der Verteilungs-Agent für das Abonnement ausgeführt wird. Stellen Sie sicher, dass alle Werte getestet wurden, über eine Verbindung mit dem Abonnenten über einen Client (z. B. **Sqlplus** für Oracle). Weitere Informationen finden Sie unter [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) und [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Auf der **Abonnenten** Seite des Assistenten der Abonnent wird nun angezeigt, der **Abonnenten** Spalte mit einem nur-Lese- **(Standardziel)** in der **Abonnementdatenbank** Spalte:  
  
    -   Bei Oracle weist ein Server höchstens eine Datenbank auf, deshalb ist die Angabe der Datenbank nicht erforderlich.  
  
    -   Bei IBM DB2 wird die Datenbank in der **Initial Catalog** -Eigenschaft der DB2-Verbindungszeichenfolge angegeben, die in dem nachfolgend erwähnten Feld **Zusätzliche Verbindungsoptionen** eingegeben werden kann.  
  
8.  Auf der **Verteilungs-Agent-Sicherheit** Seite, klicken Sie auf die Eigenschaftenschaltfläche (**...**) neben dem Abonnenten für den Zugriff auf die **Verteilungs-Agent-Sicherheit** (Dialogfeld).  
  
9. Führen Sie im Dialogfeld **Sicherheit für den Verteilungs-Agent** folgende Schritte aus:  
  
    -   Geben Sie in den Feldern **Prozesskonto**, **Kennwort**und **Kennwort bestätigen** das Konto und Kennwort von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows  an, unter dem der Verteilungs-Agent ausgeführt werden soll und unter dem er lokale Verbindungen mit dem Verteiler herstellen soll.  
  
         Das Konto muss folgende Mindestberechtigungen: Mitglied der **Db_owner** festen-Datenbankrolle in der Verteilungsdatenbank, Mitglied der veröffentlichungszugriffsliste (PAL); Leseberechtigungen für die momentaufnahmefreigabe und read-Berechtigung für das Installationsverzeichnis des OLE DB-Anbieters. Weitere Informationen zur PAL finden Sie unter [Sichern des Verlegers](../../relational-databases/replication/security/secure-the-publisher.md).  
  
    -   Geben Sie unter **Verbindung mit dem Abonnenten herstellen**, in den Feldern **Anmeldung**, **Kennwort**und **Kennwort bestätigen** die Anmeldung und das Kennwort ein, die zum Verbindungsaufbau mit dem Abonnenten verwendet werden sollen. Diese Anmeldung sollte bereits konfiguriert sein und für das Erstellen von Objekten in der Abonnementdatenbank ausreichende Berechtigungen aufweisen.  
  
    -   In der **zusätzliche Verbindungsoptionen** geben den Verbindungsoptionen für den Abonnenten in Form einer Verbindungszeichenfolge (Oracle erfordert keine zusätzliche Optionen). Mehrere Optionen müssen durch Semikolons voneinander getrennt werden. Hier ein Beispiel einer DB2-Verbindungszeichenfolge (die Umbrüche dienen der Leserlichkeit):  
  
        ```  
        Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
        PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
        Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
        Persist Security Info=False;Connection Pooling=True;  
        ```  
  
         Die meisten Optionen in der Zeichenfolge hängen von dem DB2-Server ab, den Sie konfigurieren. Allerdings sollte die Option **Process Binary as Character** immer auf **False**festgelegt sein. Zur Identifizierung der Abonnementdatenbank ist ein Wert für die Option **Anfangskatalog** erforderlich.  
  
10. Auf der **Synchronisierungszeitplan** Seite, wählen Sie einen Zeitplan für den Verteilungs-Agent aus der **Agentzeitplan** Menü (der Zeitplan ist in der Regel **fortlaufend ausgeführt,**).  
  
11. Geben Sie auf der Seite **Abonnements initialisieren** an, ob das Abonnement initialisiert werden soll, und wenn ja, wann:  
  
    -   Heben Sie die Auswahl von **Initialisieren** nur dann auf, wenn Sie alle Objekte erstellt und alle erforderlichen Daten in der Abonnementdatenbank hinzugefügt haben.  
  
    -   Wählen Sie **sofort** aus der Dropdown-Liste in der **bei** Spalte der Verteilungsagent übertragen lassen snapshot-Dateien auf den Abonnenten nach dem Abschließen des Assistenten. Wählen Sie **Bei der ersten Synchronisierung** aus, wenn die Dateien bei der nächsten laut Zeitplan festgelegten Ausführung der Momentaufnahme übertragen werden sollen.  
  
12. Erstellen Sie optional auf der Seite **Aktionen des Assistenten** ein Skript für das Abonnement. Weitere Informationen finden Sie unter [Scripting Replication](../../relational-databases/replication/scripting-replication.md).  
  
#### So behalten Sie Tabellen auf dem Abonnenten bei  
  
-   Standardmäßig aktivieren einer Veröffentlichung für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten legt den Wert für die **Pre_creation_cmd** Artikeleigenschaft auf 'drop'. Mit dieser Einstellung wird angegeben, dass bei der Replikation auf dem Abonnenten eine Tabelle gelöscht werden soll, wenn sie mit dem Namen der Tabelle in dem Artikel übereinstimmt. Wenn Sie Tabellen auf dem Abonnenten vorhanden sind, die Sie beibehalten möchten, verwenden Sie die [Sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) für jeden Artikel die gespeicherte Prozedur; geben Sie den Wert 'none' für **Pre_creation_cmd**. `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`.  
  
#### So generieren Sie eine Momentaufnahme für die Veröffentlichung  
  
1.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
2.  Maustaste auf die Publikation, und klicken Sie dann auf **Snapshot-Agent-Anzeigestatus**.  
  
3.  In der **Snapshot-Agent-Status anzeigen - \< Veröffentlichung>** im Dialogfeld klicken Sie auf **Start**.  
  
 Nachdem der Momentaufnahme-Agent die Momentaufnahme generiert hat, wird eine Meldung angezeigt, die beispielsweise wie folgt lautet: "[100%] Es wurde eine Momentaufnahme mit 17 Artikel(n) generiert."  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können Pushabonnements auf Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten mithilfe von gespeicherten Replikationsprozeduren programmgesteuert erstellen.  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
#### So erstellen Sie ein Pushabonnement für eine Transaktions- oder Momentaufnahmeveröffentlichung für einen Nicht-SQL Server-Abonnenten  
  
1.  Installieren Sie den neuesten OLE DB-Anbieter für den Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten sowohl auf dem Verleger als auch auf dem Verteiler. Die replikationsanforderungen für einen OLE DB-Anbieter finden Sie unter [nicht-SQL Server-Abonnenten](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md), [Oracle-Abonnenten](../../relational-databases/replication/non-sql/oracle-subscribers.md), [IBM DB2-Abonnenten](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
2.  Auf dem Verleger für die Veröffentlichungsdatenbank, stellen Sie sicher, dass die Veröffentlichung nicht unterstützt[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten durch Ausführen von [Sp_helppublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md).  
  
    -   Wenn der Wert der **Enabled_for_het_sub** ist 1, nicht[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten unterstützt werden.  
  
    -   Wenn der Wert der **Enabled_for_het_sub** 0 ist, führen Sie [Sp_changepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), wobei **Enabled_for_het_sub** für **@property** und **true** für **@value**.  
  
        > [!NOTE]  
        >  Vor dem Ändern der **Enabled_for_het_sub** auf **true**, müssen Sie alle vorhandenen Abonnements für die Publikation löschen. Kann nicht festgelegt werden **Enabled_for_het_sub** auf **true** Wenn die Veröffentlichung auch Abonnements mit Aktualisierung unterstützt. Ändern der **Enabled_for_het_sub** beeinflusst andere Veröffentlichungseigenschaften. Weitere Informationen finden Sie unter [nicht-SQL Server-Abonnenten](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Geben Sie **@publication**, **@subscriber**, ein Wert von **(Standardziel)** für **@destination_db**, den Wert **Push** für **@subscription_type**, und den Wert 3 für **@subscriber_type** (OLE DB-Anbieter gibt).  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addpushsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Geben Sie Folgendes an:  
  
    -   Die Parameter **@subscriber**und **@publication** .  
  
    -   Der Wert **(Standardziel)** für **@subscriber_db**,  
  
    -   Die Eigenschaften der nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenquelle für **@subscriber_provider**, **@subscriber_datasrc**, **@subscriber_location**, **@subscriber_provider_string**, und **@subscriber_catalog**.  
  
    -   Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen, unter dem der Verteilungsagent auf dem Verteiler ausgeführt, für die wird **@job_login** und **@job_password**.  
  
        > [!NOTE]  
        >  Verbindungen, die immer mit der integrierten Windows-Authentifizierung verwenden, die Windows-Anmeldeinformationen, die durch angegebene **@job_login** und **@job_password**. Der Verteilungs-Agent stellt die lokale Verbindung mit dem Verteiler immer mithilfe der Windows-Authentifizierung her. Standardmäßig stellt der Agent mithilfe der integrierten Windows-Authentifizierung eine Verbindung mit dem Abonnenten her.  
  
    -   Der Wert **0** für **@subscriber_security_mode** und die Anmeldeinformationen des OLE DB-Anbieter für **@subscriber_login** und **@subscriber_password**.  
  
    -   Einen Zeitplan für den Verteilungs-Agentauftrag für dieses Abonnement. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Beim Erstellen eines Pushabonnements auf einem Verleger mit einem Remoteverteiler werden die angegebenen Werte für alle Parameter einschließlich *Job_login* und *Job_password*, werden als nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul & #40; SQL Server-Konfigurations-Manager & #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
## Siehe auch  
 [IBM DB2-Abonnenten](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle-Abonnenten](../../relational-databases/replication/non-sql/oracle-subscribers.md)   
 [Andere Nicht-SQL Server-Abonnenten](../../relational-databases/replication/non-sql/other-non-sql-server-subscribers.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  