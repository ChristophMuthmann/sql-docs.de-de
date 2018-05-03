---
title: 'Tutorial: Konfigurieren der Replikation zwischen einem Server und mobilen Clients (Mergereplikation) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d9751b7adc3d2cd4169bcd6b3a174de720c05eb9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-configure-replication-between-a-server-and-mobile-clients-merge"></a>Tutorial: Konfigurieren der Replikation zwischen einem Server und mobilen Clients (Mergereplikation)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Die Mergereplikation stellt eine geeignete Lösung für das Problem des Verschiebens von Daten zwischen einem zentralen Server und mobilen Clients dar, die nur gelegentlich miteinander verbunden sind. Mithilfe des Replikationsassistenten können Sie eine Mergereplikationstopologie auf einfache Weise konfigurieren und verwalten. In diesem Lernprogramm wird die Konfiguration einer Replikationstopologie für mobile Clients erläutert.  Weitere Informationen zur Mergereplikation finden Sie unter [Mergereplikation](https://docs.microsoft.com/en-us/sql/relational-databases/replication/merge/merge-replication).
  
## <a name="what-you-will-learn"></a>Lernziele  
In diesem Tutorial werden mithilfe einer Mergereplikation Daten aus einer zentralen Datenbank für mindestens einen mobilen Benutzer veröffentlicht, sodass jeder Benutzer eine eindeutig gefilterte Teilmenge von Daten erhält. 

In diesem Tutorial lernen Sie Folgendes:
> [!div class="checklist"]
> * Konfigurieren eines Verlegers für die Mergereplikation
> * Hinzufügen eines mobilen Abonnenten für die Mergeveröffentlichung
> * Synchronisieren des Abonnements für die Mergeveröffentlichung
  
## <a name="prerequisites"></a>Voraussetzungen  
Dieses Tutorial ist für Benutzer vorgesehen, die mit grundlegenden Datenbankvorgängen vertraut sind, aber nur über begrenzte Kenntnisse in Bezug auf die Replikation verfügen. Bevor Sie mit diesem Tutorial starten, müssen Sie das [Tutorial: Preparing the Server for Replication (Tutorial: Vorbereiten des Servers auf die Replikation)](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md) abschließen.  
  
Auf Ihrem System müssen SQL Server Management Studio sowie die folgenden Komponenten installiert sein, damit Sie mit diesem Tutorial arbeiten können:  
  
-   Auf dem Verlegerserver (Quelle):  
  
    -   Eine beliebige Version von SQL Server (SQL Server Express und SQL Server Compact ausgeschlossen) Diese Editionen können nicht als Replikationsverleger fungieren.   
    -   Die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank Aus Sicherheitsgründen werden die Beispieldatenbanken standardmäßig nicht installiert.  
  
-   Abonnentenserver (Ziel):  
  
    -   Eine beliebige Version von SQL Server ([!INCLUDE[ssEW](../../includes/ssew-md.md)] ausgenommen). [!INCLUDE[ssEW](../../includes/ssew-md.md)] wird nicht von der in diesem Lernprogramm erstellten Veröffentlichung unterstützt. 

- Installieren Sie [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Installieren Sie die [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Laden Sie eine [AdventureWorks-Beispieldatenbank](https://github.com/Microsoft/sql-server-samples/releases) herunter. Weitere Informationen zum Wiederherstellen einer Datenbank in SSMS finden Sie unter [Restoring a Database (Wiederherstellen einer Datenbank)](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).  
 
  
>[!NOTE]
> - Die Replikation wird für SQL Server-Versionen, zwischen denen mehr als zwei Versionen liegen, nicht unterstützt. Weitere Informationen finden Sie unter [In der Replikationstopologie unterstützte SQL-Versionen](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/).
> - In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]muss eine Verbindung mit dem Verleger und dem Abonnenten hergestellt werden. Dazu wird ein Anmeldename verwendet, der Mitglied der festen Serverrolle **sysadmin** ist. Weitere Informationen zur Rolle „sysadmin“ finden Sie unter [Rollen auf Serverebene](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles).  
  
  
**Geschätzte Zeit zum Bearbeiten dieses Tutorials: 60 Minuten**  
  
## <a name="configure-a-publisher-for-merge-replication"></a>Konfigurieren eines Verlegers für die Mergereplikation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In diesem Abschnitt erfahren Sie, wie Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Mergeveröffentlichung erstellen, um eine Teilmenge der Tabellen **Employee**, **SalesOrderHeader** und **SalesOrderDetail** in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank zu veröffentlichen. Diese Tabellen werden mit parametrisierten Zeilenfiltern gefiltert, sodass in den einzelnen Abonnements jeweils eine eindeutige Teilmenge der Daten enthalten ist. Außerdem fügen Sie der Veröffentlichungszugriffsliste (Publication Access List, PAL) die vom Merge-Agent verwendete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung hinzu.  
  
### <a name="create-merge-publication-and-define-articles"></a>Erstellen einer Mergeveröffentlichung und Definieren von Artikeln  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2. Starten Sie den **SQL Server-Agent**, indem Sie im **Objekt-Explorer** erst mit der rechten Maustaste auf den Agent und anschließend mit der linken auf **Starten** klicken. Wenn der Agent danach nicht gestartet wird, müssen Sie ihn manuell über den **SQL Server-Konfigurations-Manager** starten.  
3. Erweitern Sie den Ordner **Replikation**, und klicken Sie mit der rechten Maustaste auf **Lokale Veröffentlichungen**. Klicken Sie anschließend auf **Neue Veröffentlichung**.  Der Veröffentlichungsassistent wird gestartet:  

    ![Starten des Assistenten für neue Veröffentlichungen](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
3.  Wählen Sie auf der Seite „Veröffentlichungsdatenbank“ [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] aus, und klicken Sie anschließend auf **Weiter**. 

      
4.  Wählen Sie auf der Seite „Veröffentlichungstyp“ die Option **Mergeveröffentlichung** aus, und klicken Sie anschließend auf **Weiter**.  
    A. Stellen Sie auf der Seite „Abonnententypen“ sicher, dass [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher ausgewählt ist, und klicken Sie anschließend auf **Weiter**: 

    ![Mergereplikation](media/tutorial-replicating-data-with-mobile-clients/mergerpl.png)
  
   
6.  Erweitern Sie auf der Seite „Artikel“ den Knoten **Tabellen**, und wählen Sie die folgenden drei Tabellen aus: **Employee**, **SalesOrderHeader** und **SalesOrderDetail**. Klicken Sie auf **Weiter**:  

    ![Mergeartikel](media/tutorial-replicating-data-with-mobile-clients/mergearticles.png)

    >[!NOTE]
    > Die Employee-Tabelle enthält eine OrganizationNode-Spalte vom Datentyp hierarchyid, die nur für die Replikation in SQL 2017 unterstützt wird. Wenn Sie einen Build verwenden, der niedriger als SQL 2017 ist, wird unten auf dem Bildschirm eine Meldung angezeigt, in der Sie darüber informiert werden, dass möglicherweise Daten verloren gehen können, wenn Sie diese Spalte in einer bidirektionalen Replikation verwenden. Diese Meldung kann für dieses Tutorial ignoriert werden. Trotzdem sollte dieser Datentyp nur in einer Produktionsumgebung repliziert werden, wenn Sie den unterstützten Build verwenden. Weitere Informationen zum Replizieren des hierarchyid-Datentyps finden Sie unter [Verwenden von hierarchyid-Spalten in replizierten Tabellen](https://docs.microsoft.com/en-us/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables).
    
  
7.  Klicken Sie auf der Seite „Tabellenzeilen filtern“ auf **Hinzufügen**, und klicken Sie anschließend auf **Filter hinzufügen**.  
  
8.  Klicken Sie im Dialogfeld **Filter hinzufügen** auf **Employee (HumanResources)** unter **Wählen Sie die zu filternde Tabelle aus**. Klicken Sie erst auf die Spalte **LoginID** und dann auf den Pfeil nach rechts, um der WHERE-Klausel der Filterabfrage die Spalte hinzuzufügen, und ändern Sie die WHERE-Klausel wie folgt:  
  
    ```sql 
    WHERE [LoginID] = HOST_NAME()  
    ```  
  
    A. Klicken Sie erst auf **Eine Zeile aus dieser Tabelle wird nur an ein Abonnement gesendet** und anschließend auf **OK**:  
 
    ![Hinzufügen eines Filters](media/tutorial-replicating-data-with-mobile-clients/mergeaddfilter.png)

    
  
10. Klicken Sie erst auf der Seite **Tabellenzeilen filtern** auf **Employee (Human Resources)** (Mitarbeiter (Personalabteilung)), dann auf **Hinzufügen** und anschließend auf **Add Join to Extend the Selected Filter** (Join hinzufügen, um den ausgewählten Filter zu erweitern).  
  
    A. Wählen Sie im Dialogfeld **Join hinzufügen** unter **Verknüpfte Tabelle** den Eintrag **Sales.SalesOrderDetail** aus. Klicken Sie auf **Write the join statement manually** (Joinanweisung manuell schreiben), und schließen Sie den Vorgang wie folgt ab:  
  
    ```sql  
    ON [Employee].[BusinessEntityID] =  [SalesOrderHeader].[SalesPersonID] 
    ```  
  
    B. Klicken Sie unter **Geben Sie Joinoptionen an** auf die Option **Eindeutiger Schlüssel**, und klicken Sie anschließend auf **OK**:

    ![Hinzufügen von Join zum Filter](media/tutorial-replicating-data-with-mobile-clients/mergeaddjoin.png)

  
13. Klicken Sie erst auf der Seite „Tabellenzeilen filtern“ auf **SalesOrderHeader**, dann auf **Hinzufügen** und anschließend auf **Add Join to Extend the Selected Filter** (Join hinzufügen, um den ausgewählten Filter zu erweitern).  
  
    A. Wählen Sie im Dialogfeld **Join hinzufügen** unter **Verknüpfte Tabelle** den Eintrag **Sales.SalesOrderDetail**aus.    
    B. Klicken Sie auf **Anweisung mit dem Generator erstellen**.  
    c. Überprüfen Sie im Feld **Vorschau**, dass die Joinanweisung wie folgt lautet:  
  
    ```sql  
    ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID] 
    ```  
  
    d. Klicken Sie unter **Geben Sie Joinoptionen an** auf die Option **Eindeutiger Schlüssel**, und klicken Sie anschließend auf **OK**. Klicken Sie auf **Weiter**: 

       ![Jointabellen für Verkaufsaufträge](media/tutorial-replicating-data-with-mobile-clients/joinsalestables.png)
  
21. Klicken Sie auf **Momentaufnahme sofort erstellen**, deaktivieren Sie **Ausführung des Momentaufnahme-Agents zu folgenden Zeitpunkten planen**, und klicken Sie auf **Weiter**:  

    ![Momentaufnahme sofort erstellen](media/tutorial-replicating-data-with-mobile-clients/snapshotagent.png)
  
22. Klicken Sie auf der Seite „Agentsicherheit“ auf **Sicherheitseinstellungen**, geben Sie im Feld **Prozesskonto** das Konto <*Name_des_Verlegercomputers>***\repl_snapshot** sowie das Kennwort für das Konto ein, und klicken Sie anschließend auf **OK**. Klicken Sie auf **Weiter**:  

    ![Sicherheit für den Momentaufnahme-Agent](media/tutorial-replicating-data-with-mobile-clients/snapshotagentsecurity.png)
  
23. Geben Sie auf der Seite **Assistenten abschließen** im Feld **Veröffentlichungsname** den Namen **AdvWorksSalesOrdersMerge** ein, und klicken Sie auf **Fertig stellen**:  

    ![Name der Mergereplikation](media/tutorial-replicating-data-with-mobile-clients/namemergerepl.png)
  
24. Klicken Sie auf **Schließen**, nachdem die Veröffentlichung erstellt wurde. Klicken Sie unter dem Knoten **Replikation** im **Objekt-Explorer** mit der rechten Maustaste auf **Lokale Veröffentlichungen** und **Aktualisieren**, um Ihre neue Mergereplikation anzuzeigen.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>So zeigen Sie den Status der Momentaufnahmegenerierung an  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner „Lokale Veröffentlichungen“ erst mit der rechten Maustaste auf **AdvWorksSalesOrdersMerge** und anschließend mit der linken auf **Status des Momentaufnahme-Agents anzeigen**:  

    ![Status des Momentaufnahme-Agents anzeigen](media/tutorial-replicating-data-with-mobile-clients/viewsnapshotagentstatus.png)
  
3.  Der aktuelle Status des Auftrags des Momentaufnahme-Agents für die Veröffentlichung wird angezeigt. Stellen Sie sicher, dass der Momentaufnahmeauftrag erfolgreich war, bevor Sie zur nächsten Lektion wechseln.  
  
### <a name="to-add-the-merge-agent-login-to-the-pal"></a>So fügen Sie der PAL die Anmeldung des Merge-Agents hinzu  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner „Lokale Veröffentlichungen“ erst mit der rechten Maustaste auf **AdvWorksSalesOrdersMerge** und anschließend mit der linken auf **Eigenschaften**.  
  
    A. Klicken Sie erst auf die Seite **Veröffentlichungszugriffsliste** und dann auf **Hinzufügen**. 
  
    B. Klicken Sie im Dialogfeld „Veröffentlichungszugriff hinzufügen“ auf <*Name_des_Verlegercomputers>***\repl_merge** und anschließend auf **OK**. Klicken Sie auf **OK**: 

    ![PAL zusammenführen](media/tutorial-replicating-data-with-mobile-clients/mergepal.png) 

  
**Weitere Informationen finden Sie unter:**  
[Filtern von veröffentlichten Daten](../../relational-databases/replication/publish/filter-published-data.md)  
[Parametrisierte Zeilenfilter](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
[Definieren eines Artikels](../../relational-databases/replication/publish/define-an-article.md)  
  
  
## <a name="creating-a-subscription-to-the-merge-publication"></a>Erstellen eines Abonnements für die Mergeveröffentlichung
In diesem Abschnitt erfahren Sie, wie Sie zu der Mergeveröffentlichung, die Sie zuvor erstellt haben, ein Abonnement hinzufügen. In diesem Tutorial wird der Remoteabonnent (NODE2\SQL2016) verwendet. Anschließend erstellen Sie Berechtigungen für die Abonnementdatenbank und generieren die gefilterte Datenmomentaufnahme für das neue Abonnement manuell.   
  
### <a name="add-a-subscriber-for-merge-publication"></a>Hinzufügen eines Abonnenten für die Mergereplikation
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Verbindung mit dem Abonnenten her, und erweitern Sie den Serverknoten. Erweitern Sie den Ordner **Replikation**, klicken Sie erst mit der rechten Maustaste auf den Ordner **Lokale Abonnements** und dann mit der linken auf **Neue Abonnements**. Der Assistent für neue Abonnements wird gestartet:

    ![Neues Abonnement](media/tutorial-replicating-data-with-mobile-clients/newsub.png)
  
2.  Klicken Sie auf der Seite **Veröffentlichung** in der Liste **Verleger** auf **SQL Server-Verleger** suchen.  
  
    A. Geben Sie im Dialogfeld **Verbindung mit Server herstellen** im Feld **Servername** den Namen der Verlegerinstanz ein, und klicken Sie auf **Verbinden**: 

    ![Verleger zu Veröffentlichung hinzufügen](media/tutorial-replicating-data-with-mobile-clients/publication.png)
  
4.  Klicken Sie erst auf **AdvWorksSalesOrdersMerge** und dann auf **Weiter**.  
  
5.  Klicken Sie auf der Seite „Speicherort des Merge-Agents“ auf **Run each agent at its Subscriber** (Jeden Agent auf seinem Abonnenten ausführen), und klicken Sie anschließend auf **Weiter**:  

    ![Pullabonnement](media/tutorial-replicating-data-with-mobile-clients/pullsub.png)
  
6.  Wählen Sie auf der Seite „Abonnenten“ den Instanznamen des Abonnentenservers aus, und klicken Sie unter **Abonnementdatenbank** in der Liste auf die Option **Neue Datenbank**.  
  
    A. Geben Sie im Dialogfeld **Neue Datenbank** den Namen **SalesOrdersReplica** in das Feld **Datenbankname** ein, klicken Sie auf **OK**, und klicken Sie anschließend auf **Weiter**: 

    ![Datenbank zu Abonnent hinzufügen](media/tutorial-replicating-data-with-mobile-clients/addsubdb.png)
  
8.  Klicken Sie auf der Seite „Sicherheit für den Merge-Agent“ auf die Schaltfläche mit den Auslassungspunkten (**…**), geben Sie im Feld **Prozesskonto** das Konto <*Name_des_Abonnentencomputers*>***\repl_merge* ein, und geben Sie das Kennwort für dieses Konto ein. Klicken Sie erst auf **OK** und anschließend zweimal auf **Weiter**:  

    ![Sicherheit für den Merge-Agent](media/tutorial-replicating-data-with-mobile-clients/mergeagentsecurity.png)

9. Legen Sie für den **Synchronisierungszeitplan** den **Agentzeitplan** auf **Nur bedarfsgesteuert ausführen** fest. Klicken Sie auf **Weiter**:  

    ![Synchronisierungszeitplan](media/tutorial-replicating-data-with-mobile-clients/mergesyncschedule.png)
  
9. Wählen Sie auf der Seite „Abonnements initialisieren“ aus der Liste **Initialisierungszeitpunkt** die Option **Bei der ersten Synchronisierung** aus, und klicken Sie anschließend zweimal auf **Weiter**: 

    ![Erste Synchronisierung](media/tutorial-replicating-data-with-mobile-clients/firstsync.png)

10. Geben Sie auf der Seite „HOST_NAME-Werte“ im Feld **HOST_NAME-Wert** den Wert **adventure-works\pamela0** ein, und klicken Sie anschließend auf **Fertig stellen**:  

    ![Hostname](media/tutorial-replicating-data-with-mobile-clients/hostname.png)
  
11. Klicken Sie erneut auf **Fertig stellen**, und klicken Sie nachdem das Abonnement erstellt wurde auf **Schließen**.  

### <a name="setting-server-permissions-at-the-subscriber"></a>Festlegen der Datenbankberechtigungen auf dem Abonnenten  
  
1.  Stellen Sie eine Verbindung mit dem Abonnenten in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] her, erweitern Sie **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Anmeldungen**, und wählen Sie anschließend **Neue Anmeldung** aus.  
  
    A. Klicken Sie auf der Seite **Allgemein** auf **Suchen**, geben Sie dann in das Feld **Geben Sie den Objektnamen ein** <*Name_des-Abonnentencomputers>***\repl_merge** ein, klicken Sie auf **Namen überprüfen** und klicken Sie anschließend auf **OK**: 
    
    ![Auf Abonnenten anmelden](media/tutorial-replicating-data-with-mobile-clients/sublogin.png)
  
1. Wählen Sie auf der Seite **Benutzerzuordnung** die Datenbank **SalesOrdersReplica** und die Rolle **db_owner** aus.  Erteilen Sie auf der Seite **Sicherungsfähige Elemente** die Berechtigung „Explizit“ für **Ablaufverfolgung ändern**. Klicken Sie auf **OK**:

    ![Anmeldung als DBO auf Abonnenten festlegen](media/tutorial-replicating-data-with-mobile-clients/setdbo.png)
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>So erstellen Sie die gefilterte Datenmomentaufnahme für das Abonnement  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner **Lokale Veröffentlichungen** erst mit der rechten Maustaste auf die **AdvWorksSalesOrdersMerge**-Veröffentlichung und anschließend mit der linken auf **Eigenschaften**.  
   
    A. Klicken Sie erst auf die Seite **Datenpartitionen** und dann auf **Hinzufügen**.   
    B. Geben Sie im Dialogfeld **Datenpartition hinzufügen** im Feld **HOST_NAME-Wert** den Wert **adventure-works\pamela0** ein, und klicken Sie anschließend auf **OK**.  
    c. Wählen Sie die neu hinzugefügte Partition aus, klicken Sie erst auf **Die ausgewählten Momentaufnahmen jetzt generieren** und anschließend auf **OK**: 

    ![Partition hinzufügen](media/tutorial-replicating-data-with-mobile-clients/partition.png)
  
  
**Weitere Informationen finden Sie unter:**  
[Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
[Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)  
[Momentaufnahmen für Mergeveröffentlichungen mit parametrisierten Filtern](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  

## <a name="synchronize-the-subscription-to-the-merge-publication"></a>Synchronisieren des Abonnements für die Mergeveröffentlichung

In diesem Abschnitt erfahren Sie, wie Sie den Merge-Agent starten können, um das Abonnement mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zu initialisieren. Mithilfe dieser Prozedur können Sie außerdem eine Synchronisierung mit dem Verleger ausführen.   
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>So starten Sie die Synchronisierung und initialisieren das Abonnement  
  
1.  Stellen Sie eine Verbindung mit dem Abonnenten in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] her.  
2. Stellen Sie sicher, dass der **SQL Server-Agent** ausgeführt wird. Starten Sie den **SQL Server-Agent**, indem Sie im **Objekt-Explorer** erst mit der rechten Maustaste auf diesen und anschließend mit der linken auf **Starten** klicken. Wenn der Agent danach nicht gestartet wird, müssen Sie ihn manuell über den **SQL Server-Konfigurations-Manager** starten. 
  
2.  Erweitern Sie den Knoten **Replikation**. Klicken Sie im Ordner **Lokale Abonnements** mit der rechten Maustaste auf das Abonnement in der Datenbank **SalesOrdersReplica**, und klicken Sie anschließend auf **Synchronisierungsstatus anzeigen**.  
  
    A. Klicken Sie auf **Start**, um das Abonnement zu initialisieren: 

    ![Synchronisierungsstatus](media/tutorial-replicating-data-with-mobile-clients/mergesyncstatus.png)
    
  
  
### <a name="next-steps"></a>Next Steps  
Nun wissen Sie, wie Sie ihren Verleger und Ihren Abonnenten erfolgreich für Ihre Mergereplikation konfigurieren können.  Sie können auch Daten in der **SalesOrderHeader** -Tabelle oder der **SalesOrderDetail** -Tabelle auf dem Verleger oder dem Abonnenten einfügen, aktualisieren oder löschen, diese Schrittfolge wiederholen, wenn eine Netzwerkverbindung verfügbar ist, um Daten zwischen dem Verleger und dem Abonnenten zu synchronisieren, und anschließend können Sie die **SalesOrderHeader** -Tabelle oder die **SalesOrderDetail** -Tabelle auf dem anderen Server abfragen, um die replizierten Änderungen anzuzeigen.  
  
**Weitere Informationen finden Sie unter:**   
[Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Synchronisieren von Daten](../../relational-databases/replication/synchronize-data.md)  
[Synchronisieren eines Pullabonnements](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
  
