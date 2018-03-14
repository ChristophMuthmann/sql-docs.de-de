---
title: "Erstellen eines Abonnements für einen Nicht-SQL Server-Abonnenten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication], non-SQL Server Subscribers
- Subscribers [SQL Server replication], non-SQL Server Subscribers
- non-SQL Server Subscribers, subscriptions
ms.assetid: 5020ee68-b988-4d57-8066-67d183e61237
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5abfc62f959e40006a2f25cfc91cc84955831aa
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="create-a-subscription-for-a-non-sql-server-subscriber"></a>Erstellen eines Abonnements für einen Nicht-SQL Server-Abonnenten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie ein Abonnement für einen Nicht-SQL Server-Abonnenten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]erstellt wird. Von der Transaktionsreplikation und der Momentaufnahmereplikation wird das Veröffentlichen von Daten auf Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten unterstützt. Informationen zu den unterstützten Abonnentenplattformen finden Sie unter [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)erstellt wird.  
  
 **In diesem Thema**  
  
-   **So erstellen Sie ein Abonnement für einen Nicht-SQL Server-Abonnenten mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 So erstellen Sie ein Abonnement für einen Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten  
  
1.  Nehmen Sie die Installation und Konfiguration der entsprechenden Clientsoftware und OLE DB-Anbieter auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verteiler vor. Weitere Informationen finden Sie unter [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) und [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
2.  Erstellen Sie mithilfe des Assistenten für neue Veröffentlichung eine Veröffentlichung. Weitere Informationen zum Erstellen von Veröffentlichungen finden Sie unter [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md) und [Erstellen einer Veröffentlichung aus einer Oracle-Datenbank](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md). Geben Sie im Assistenten für neue Veröffentlichung folgende Optionen an:  
  
    -   Wählen Sie auf der Seite **Veröffentlichungstyp** entweder **Momentaufnahmeveröffentlichung** oder **Transaktionsveröffentlichung**aus.  
  
    -   Heben Sie auf der Seite **Momentaufnahme-Agent** die Auswahl von **Momentaufnahme sofort erstellen**auf.  
  
         Die Erstellung der Momentaufnahme erfolgt nach der Aktivierung der Veröffentlichung für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten, um sicherzustellen, dass der Momentaufnahme-Agent eine Momentaufnahme und Initialisierungsskripts generiert, die für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten geeignet sind.  
  
3.  Verwenden Sie zur Aktivierung der Veröffentlichung für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten das Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichungsname>**. Weitere Informationen zu diesem Schritt finden Sie unter [Publication Properties, Subscription Options](../../relational-databases/replication/publication-properties-subscription-options.md) .  
  
4.  Erstellen Sie mithilfe des Assistenten für neue Abonnements ein Abonnement. In diesem Thema sind weitere Informationen zu diesem Schritt enthalten.  
  
5.  (Optional) Ändern Sie die **pre_creation_cmd** -Artikeleigenschaft, um Tabellen auf dem Abonnenten beizubehalten. In diesem Thema sind weitere Informationen zu diesem Schritt enthalten.  
  
6.  Generieren Sie eine Momentaufnahme für die Veröffentlichung. In diesem Thema sind weitere Informationen zu diesem Schritt enthalten.  
  
7.  Synchronisieren Sie das Abonnement. Weitere Informationen finden Sie unter [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### <a name="to-enable-a-publication-for-non-sql-server-subscribers"></a>So aktivieren Sie eine Veröffentlichung für Nicht-SQL Server-Abonnenten  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Veröffentlichung, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Wählen Sie auf der Seite **Abonnementoptionen** den Wert **Wahr** für die Option **Nicht-SQL Server-Abonnenten zulassen**aus. Beim Auswählen dieser Option werden eine Reihe von Eigenschaften so geändert, dass die Veröffentlichung mit Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten kompatibel ist.  
  
    > [!NOTE]  
    >  Durch die Auswahl von **Wahr** wird der Wert der Artikeleigenschaft **pre_creation_cmd** auf 'drop' festgelegt. Mit dieser Einstellung wird angegeben, dass bei der Replikation auf dem Abonnenten eine Tabelle gelöscht werden soll, wenn sie mit dem Namen der Tabelle in dem Artikel übereinstimmt. Wenn auf dem Abonnenten Tabellen vorhanden sind, die Sie aufheben möchten, verwenden Sie für jeden Artikel die gespeicherte Prozedur [sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) . Geben Sie für **pre_creation_cmd**: `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`den Wert 'none' an.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Sie werden zur Erstellung einer neuen Momentaufnahme für die Veröffentlichung aufgefordert. Wenn Sie diesen Vorgang lieber zu einem späteren Vorgang ausführen möchten, verwenden Sie hierzu die nachfolgend aufgeführten schrittweisen Anweisungen.  
  
#### <a name="to-create-a-subscription-for-a-non-sql-server-subscriber"></a>So erstellen Sie ein Abonnement für einen Nicht-SQL Server-Abonnenten  
  
1.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die entsprechende Veröffentlichung, und klicken Sie dann auf **Neue Abonnements**.  
  
3.  Vergewissern Sie sich, dass auf der Seite **Speicherort des Verteilungs-Agents** die Option **Alle Agents auf dem Verteiler ausführen** aktiviert ist. Von Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten wird das Ausführen von Agents auf dem Abonnenten nicht unterstützt.  
  
4.  Klicken Sie auf der Seite **Abonnenten** zunächst auf **Abonnent hinzufügen** und dann auf **Nicht-SQL Server-Abonnenten hinzufügen**.  
  
5.  Wählen Sie im Dialogfeld **Nicht-SQL Server-Abonnenten hinzufügen** den Abonnententyp aus.  
  
6.  Geben Sie im Feld **Datenquellenname**einen Wert ein:  
  
    -   Bei Oracle ist dies der von Ihnen konfigurierte Transparent Network Substrate-(TNS-)Name.  
  
    -   Bei IBM kann dies ein beliebiger Name sein. Im Normalfall wird die Netzwerkadresse des Abonnenten angegeben.  
  
     Der in diesem Schritt eingegebene Datenquellenname und die in Schritt 9 angegebenen Anmeldeinformationen werden von diesem Assistenten nicht überprüft. Sie werden von der Replikation nicht verwendet, bis der Verteilungs-Agent für das Abonnement ausgeführt wird. Vergewissern Sie sich, dass sämtliche Werte getestet wurden, und zwar durch die Verbindungsherstellung mit dem Abonnenten über ein Clienttool (für Oracle z. B. **sqlplus** ). Weitere Informationen finden Sie unter [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) und [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Nun wird auf der Seite **Abonnenten** des Assistenten der Abonnent in der **Abonnent** -Spalte angezeigt; hierbei ist ein schreibgeschütztes **(Standardziel)** in der **Abonnementdatenbank** -Spalte enthalten:  
  
    -   Bei Oracle weist ein Server höchstens eine Datenbank auf, deshalb ist die Angabe der Datenbank nicht erforderlich.  
  
    -   Bei IBM DB2 wird die Datenbank in der **Initial Catalog** -Eigenschaft der DB2-Verbindungszeichenfolge angegeben, die in dem nachfolgend erwähnten Feld **Zusätzliche Verbindungsoptionen** eingegeben werden kann.  
  
8.  Klicken Sie auf der Seite **Sicherheit für den Verteilungs-Agent** neben dem Abonnenten auf die Schaltfläche für die Eigenschaften (**…**), um auf das Dialogfeld **Sicherheit für den Verteilungs-Agent** zuzugreifen.  
  
9. Führen Sie im Dialogfeld **Sicherheit für den Verteilungs-Agent** folgende Schritte aus:  
  
    -   Geben Sie in den Feldern **Prozesskonto**, **Kennwort**und **Kennwort bestätigen** das Konto und Kennwort von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows  an, unter dem der Verteilungs-Agent ausgeführt werden soll und unter dem er lokale Verbindungen mit dem Verteiler herstellen soll.  
  
         Für das Konto müssen folgende Mindestberechtigungen erfüllt werden: Mitglied der festen Datenbankrolle **db_owner** in der Verteilungsdatenbank, Mitglied der Veröffentlichungszugriffsliste (PAL, Publication Access List); Leseberechtigungen für die Momentaufnahmefreigabe sowie Leseberechtigungen für das Installationsverzeichnis des OLE DB-Anbieters. Weitere Informationen zu PAL finden Sie unter [Sichern des Verlegers](../../relational-databases/replication/security/secure-the-publisher.md).  
  
    -   Geben Sie unter **Verbindung mit dem Abonnenten herstellen**, in den Feldern **Anmeldung**, **Kennwort**und **Kennwort bestätigen** die Anmeldung und das Kennwort ein, die zum Verbindungsaufbau mit dem Abonnenten verwendet werden sollen. Diese Anmeldung sollte bereits konfiguriert sein und für das Erstellen von Objekten in der Abonnementdatenbank ausreichende Berechtigungen aufweisen.  
  
    -   Geben Sie im Feld **Zusätzliche Verbindungsoptionen** sämtliche Verbindungsoptionen für den Abonnenten in Form einer Verbindungszeichenfolge an (für Oracle sind keine zusätzlichen Optionen erforderlich). Mehrere Optionen müssen durch Semikolons voneinander getrennt werden. Hier ein Beispiel einer DB2-Verbindungszeichenfolge (die Umbrüche dienen der Leserlichkeit):  
  
        ```  
        Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
        PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
        Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
        Persist Security Info=False;Connection Pooling=True;  
        ```  
  
         Die meisten Optionen in der Zeichenfolge hängen von dem DB2-Server ab, den Sie konfigurieren. Allerdings sollte die Option **Process Binary as Character** immer auf **False**festgelegt sein. Zur Identifizierung der Abonnementdatenbank ist ein Wert für die Option **Anfangskatalog** erforderlich.  
  
10. Wählen Sie auf der Seite **Synchronisierungszeitplan** im Menü **Agentzeitplan** einen Zeitplan für den Verteilungs-Agent aus (der Zeitplan weist normalerweise das Attribut **Fortlaufend ausführen**auf).  
  
11. Geben Sie auf der Seite **Abonnements initialisieren** an, ob das Abonnement initialisiert werden soll, und wenn ja, wann:  
  
    -   Heben Sie die Auswahl von **Initialisieren** nur dann auf, wenn Sie alle Objekte erstellt und alle erforderlichen Daten in der Abonnementdatenbank hinzugefügt haben.  
  
    -   Wenn Sie in der **Initialisierungszeitpunkt** -Spalte auf die Option **Sofort** klicken, überträgt der Verteilungs-Agent Momentaufnahmedateien an den Abonnenten, nachdem alle Vorgänge des Assistenten beendet sind. Wählen Sie **Bei der ersten Synchronisierung** aus, wenn die Dateien bei der nächsten laut Zeitplan festgelegten Ausführung der Momentaufnahme übertragen werden sollen.  
  
12. Erstellen Sie optional auf der Seite **Aktionen des Assistenten** ein Skript für das Abonnement. Weitere Informationen finden Sie unter [Scripting Replication](../../relational-databases/replication/scripting-replication.md).  
  
#### <a name="to-retain-tables-at-the-subscriber"></a>So behalten Sie Tabellen auf dem Abonnenten bei  
  
-   Standardmäßig wird durch das Aktivieren einer Veröffentlichung für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten der Wert der **pre_creation_cmd** -Artikeleigenschaft auf 'drop' festgelegt. Mit dieser Einstellung wird angegeben, dass bei der Replikation auf dem Abonnenten eine Tabelle gelöscht werden soll, wenn sie mit dem Namen der Tabelle in dem Artikel übereinstimmt. Wenn auf dem Abonnenten Tabellen vorhanden sind, die Sie beibehalten möchten, verwenden Sie für jeden Artikel die gespeicherte Prozedur [sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) . Geben Sie für **pre_creation_cmd**den Wert 'none' an. `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`.  
  
#### <a name="to-generate-a-snapshot-for-the-publication"></a>So generieren Sie eine Momentaufnahme für die Veröffentlichung  
  
1.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Veröffentlichung, und klicken Sie dann auf **Status des Momentaufnahme-Agents anzeigen**.  
  
3.  Klicken Sie im Dialogfeld **Status des Momentaufnahme-Agents anzeigen - \<Veröffentlichung>** auf **Start**.  
  
 Nachdem der Momentaufnahme-Agent die Momentaufnahme generiert hat, wird eine Meldung angezeigt, die beispielsweise wie folgt lautet: "[100%] Es wurde eine Momentaufnahme mit 17 Artikel(n) generiert."  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Sie können Pushabonnements auf Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten mithilfe von gespeicherten Replikationsprozeduren programmgesteuert erstellen.  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
#### <a name="to-create-a-push-subscription-for-a-transactional-or-snapshot-publication-to-a-non-sql-server-subscriber"></a>So erstellen Sie ein Pushabonnement für eine Transaktions- oder Momentaufnahmeveröffentlichung für einen Nicht-SQL Server-Abonnenten  
  
1.  Installieren Sie den neuesten OLE DB-Anbieter für den Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten sowohl auf dem Verleger als auch auf dem Verteiler. Informationen zu den Replikationsanforderungen für einen OLE DB-Anbieter finden Sie unter [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md), [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md), [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
2.  Überprüfen Sie für die Veröffentlichungsdatenbank auf dem Verleger, ob die Veröffentlichung Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten unterstützt, indem Sie [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) ausführen.  
  
    -   Der Wert 1 für **enabled_for_het_sub** bedeutet, dass Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten unterstützt werden.  
  
    -   Wenn der Wert für **enabled_for_het_sub** 0 ist, führen Sie [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) aus, wobei Sie **enabled_for_het_sub** für **@property** und **true** für **@value** angeben.  
  
        > [!NOTE]  
        >  Bevor Sie **enabled_for_het_sub** zu **true**ändern, müssen Sie alle vorhandenen Abonnements für die Veröffentlichung löschen. Sie können **enabled_for_het_sub** nicht auf **true** festlegen, wenn die Veröffentlichung auch Abonnements mit Update unterstützt. Die Änderung von **enabled_for_het_sub** beeinflusst andere Veröffentlichungseigenschaften. Weitere Informationen finden Sie unter [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) aus. Geben Sie **@publication**, **@subscriber**, den Wert **(Standardziel)** für **@destination_db**, den Wert **push** für **@subscription_type**und den Wert 3 für **@subscriber_type** (den OLE DB-Anbieter) an.  
  
4.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) aus. Geben Sie Folgendes an:  
  
    -   Die Parameter **@subscriber**und **@publication** .  
  
    -   Den Wert **(Standardziel)** für **@subscriber_db**,  
  
    -   Die Eigenschaften der Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle für **@subscriber_provider**, **@subscriber_datasrc**, **@subscriber_location**, **@subscriber_provider_string**und **@subscriber_catalog**erstellt wird.  
  
    -   Die Parameter [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen, unter denen der Verteilungs-Agent auf dem Verteiler für **@job_login** und **@job_password**erstellt wird.  
  
        > [!NOTE]  
        >  Für Verbindungen, die mit der integrierten Windows-Authentifizierung hergestellt werden, werden immer die mit **@job_login** und **@job_password**erstellt wird. Der Verteilungs-Agent stellt die lokale Verbindung mit dem Verteiler immer mithilfe der Windows-Authentifizierung her. Standardmäßig stellt der Agent mithilfe der integrierten Windows-Authentifizierung eine Verbindung mit dem Abonnenten her.  
  
    -   Den Wert **0** für **@subscriber_security_mode** und die Anmeldeinformationen des OLE DB-Anbieters für **@subscriber_login** und **@subscriber_password**erstellt wird.  
  
    -   Einen Zeitplan für den Verteilungs-Agentauftrag für dieses Abonnement. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Beim Erstellen eines Pushabonnements auf einem Verleger mit einem Remoteverteiler werden die angegebenen Werte für alle Parameter, einschließlich *job_login* und *job_password*, an den Verteiler als Nur-Text gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md)   
 [Andere Nicht-SQL Server-Abonnenten](../../relational-databases/replication/non-sql/other-non-sql-server-subscribers.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
