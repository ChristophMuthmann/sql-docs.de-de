---
title: 'Tutorial: Konfigurieren der Replikation zwischen zwei Servern mit kontinuierlicher Verbindung (transaktional)| Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de374f4372f62741ff3c49a9433cf339cecf3d26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-configure-replication-between-two-fully-connected-servers-transactional"></a>Tutorial: Konfigurieren der Replikation zwischen zwei Servern mit kontinuierlicher Verbindung (transaktional)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Die Transaktionsreplikation stellt eine bewährte Lösung für das Problem des Verschiebens von Daten zwischen Servern mit kontinuierlicher Verbindung dar. Mithilfe des Replikations-Assistenten können Sie eine Replikationstopologie auf einfache Weise konfigurieren und verwalten. In diesem Tutorial wird die Konfiguration einer Topologie für Transaktionsreplikationen für Server mit kontinuierlicher Verbindung erläutert. Weitere Informationen zur Funktionsweise der Transaktionsreplikation finden Sie unter [Übersicht über die Transaktionsreplikation](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication). 
  
## <a name="what-you-will-learn"></a>Lernziele  
In diesem Lernprogramm erfahren Sie, wie Sie Daten aus einer Datenbank mithilfe der Transaktionsreplikation in einer anderen Datenbank veröffentlichen. 

In diesem Tutorial lernen Sie Folgendes:
> [!div class="checklist"]
> * Erstellen eines Verlegers über die Transaktionsreplikation
> * Erstellen eines Abonnenten für den Verleger der Transaktion
> * Überprüfen des Abonnements und Messen der Latenzzeit
> * Problembehandlungsmethoden
  
  
## <a name="prerequisites"></a>Voraussetzungen  
Dieses Lernprogramm ist für Benutzer vorgesehen, die mit grundlegenden Datenbankvorgängen vertraut sind, aber nur über begrenzte Kenntnisse in Bezug auf die Replikation verfügen. Für dieses Lernprogramm ist es erforderlich, dass Sie das vorherige Lernprogramm ( [Vorbereiten des Servers für die Replikation](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)) abgeschlossen haben.  
  
Für dieses Tutorial müssen auf Ihrem System SQL Server Management Studio (SSMS) sowie die folgenden Komponenten installiert sein:  
  
-   Auf dem Verlegerserver (Quelle):  
  
    -   Sämtliche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen, außer SQL Server Express oder SQL Compact. Diese Editionen können nicht als Verleger für Replikationen verwendet werden.   
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] -Beispieldatenbank Aus Sicherheitsgründen werden die Beispieldatenbanken standardmäßig nicht installiert.  
  
-   Abonnentenserver (Ziel):  
  
    -   Eine beliebige Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mit Ausnahme von [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] kann nicht als Abonnent einer Transaktionsreplikation fungieren.  
  
- Installieren Sie [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Installieren Sie die [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Laden Sie eine [AdventureWorks-Beispieldatenbank](https://github.com/Microsoft/sql-server-samples/releases) herunter. Weitere Informationen zum Wiederherstellen einer Datenbank in SSMS finden Sie unter [Wiederherstellen einer Datenbank](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 
 
>[!NOTE]
> - Die Replikation wird für SQL Server-Versionen, zwischen denen mehr als zwei Versionen liegen, nicht unterstützt. Weitere Informationen finden Sie unter [In der Replikationstopologie unterstützte SQL-Versionen](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/).
> - In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]muss eine Verbindung mit dem Verleger und dem Abonnenten hergestellt werden. Dazu wird ein Anmeldename verwendet, der Mitglied der festen Serverrolle **sysadmin** ist. Weitere Informationen zur Rolle „sysadmin“ finden Sie unter [Rollen auf Serverebene](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles).  
  
  
**Geschätzte Dauer dieses Tutorials: 60 Minuten.**  
  
## <a name="configure-the-publisher-for-transactional-replication"></a>Konfigurieren des Verlegers für die Transaktionsreplikation
In diesem Abschnitt erstellen Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Transaktionsveröffentlichung, um eine gefilterte Teilmenge der **Product**-Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank zu veröffentlichen. Außerdem fügen Sie der Veröffentlichungszugriffsliste (Publication Access List, PAL) die vom Verteilungs-Agent verwendete SQL Server-Anmeldung hinzu. Bevor Sie dieses Tutorial starten, sollten Sie das vorherige Tutorial ( [Vorbereiten des Servers für die Replikation](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)) abgeschlossen haben.


### <a name="create-a-publication-and-define-articles"></a>Erstellen einer Veröffentlichung und Definieren von Artikeln
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2. Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, und wählen Sie **Starten** aus. Der SQL Server-Agent muss ausgeführt werden, bevor Sie die Veröffentlichung erstellen. Wenn der Agent nicht gestartet wird, müssen Sie ihn manuell über den **SQL Server-Konfigurations-Manager** starten. 
3. Erweitern Sie den Ordner **Replikation**, und klicken Sie mit der rechten Maustaste auf den Ordner **Lokale Veröffentlichungen**. Klicken Sie anschließend auf **Neue Veröffentlichung**.  Der Assistent für die Konfiguration der Veröffentlichung wird gestartet:  

    ![Neue Veröffentlichung](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
  
3. Wählen Sie auf der Seite „Veröffentlichungsdatenbank“ [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] aus, und klicken Sie anschließend auf **Weiter**.  
  
4. Wählen Sie auf der Seite „Veröffentlichungstyp“ **Transaktionsveröffentlichung** aus, und klicken Sie anschließend auf **Weiter**:  

    ![Transaktionsreplikation](media/tutorial-replicating-data-between-continuously-connected-servers/tranrepl.png)
  
5. Erweitern Sie auf der Seite „Artikel“ den Knoten **Tabellen**, und aktivieren Sie das Kontrollkästchen **Produkt**. Erweitern Sie anschließend das Kontrollkästchen **Produkt**, und deaktivieren Sie die Kontrollkästchen neben **ListPrice** und **StandardCost**. Klicken Sie auf **Weiter**:  

    ![Zu veröffentlichende Artikel](media/tutorial-replicating-data-between-continuously-connected-servers/replarticles.png)
  
6. Wählen Sie auf der Seite „Tabellenzeilen filtern“ die Option **Hinzufügen** aus.   
  
7. Wählen Sie im Dialogfeld **Filter hinzufügen** die Spalte **SafetyStockLevel** und anschließend den Pfeil nach rechts aus, um die Spalte zur WHERE-Klausel der Filteranweisung in der Filterabfrage hinzuzufügen. Geben Sie anschließend den WHERE-Klauselmodifizierer wie folgt ein:  
  
    ```sql  
    WHERE [SafetyStockLevel] < 500  
    ```
  
    ![Filteranweisung](media/tutorial-replicating-data-between-continuously-connected-servers/filter.png)
  
8. Wählen Sie **OK**, und wählen Sie anschließend **Weiter**aus.  
  
9. Aktivieren Sie das Kontrollkästchen **Momentaufnahme sofort erstellen und zum Initialisieren von Abonnements verfügbar halten**, und wählen Sie **Weiter** aus:  

    ![Momentaufnahme-Agent](media/tutorial-replicating-data-between-continuously-connected-servers/snapshot.png)
  
10. Deaktivieren Sie auf der Seite „Agentsicherheit“ das Kontrollkästchen **Sicherheitseinstellungen des Momentaufnahme-Agents verwenden** .   
  
    A. Wählen Sie bei dem Momentaufnahmen-Agent **Sicherheitseinstellungen** aus, geben Sie <*Publisher_Machine_Name>***\repl_snapshot** in das Feld **Prozesskonto** ein, geben Sie das Kennwort für dieses Konto ein, und wählen Sie anschließend **OK** aus:  

    ![Sicherheit für den Momentaufnahme-Agent](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagentsecurity.png)
  
12. Wiederholen Sie den vorherigen Schritt, um <*Publisher_Machine_Name*>**\repl_logreader** als Prozesskonto für den Protokolllese-Agenten festzulegen, und wählen Sie anschließend **OK** aus:  

    ![Sicherheit für den Protokolllese-Agent](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentsecurity.png)   

  
13. Geben Sie auf der Seite „Assistenten abschließen“ im Feld **Veröffentlichungsname** den Namen **AdvWorksProductTrans** ein, und wählen Sie **Fertig stellen** aus:  

    ![Der Name der Veröffentlichung](media/tutorial-replicating-data-between-continuously-connected-servers/advworksproducttrans.png)
  
14. Klicken Sie nach Erstellung der Veröffentlichung auf **Schließen**, um den Assistenten zu beenden. 

    Wenn Ihr SQL Server-Agent bei dem Versuch, die Veröffentlichung zu erstellen, nicht ausgeführt wird, tritt möglicherweise der folgende Fehler auf. Dies ist ein Hinweis darauf, dass Ihre Veröffentlichung erfolgreich erstellt wurde, Ihr Momentaufnahmen-Agent jedoch nicht gestartet werden konnte. In diesem Fall müssen Sie den SQL Server-Agent starten und den Momentaufnahmen-Agent anschließend manuell starten. Anweisungen hierzu finden Sie im nächsten Abschnitt: 

    ![Momentaufnahmen-Agent kann nicht gestartet werden](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenterror.png)
    
  
### <a name="to-view-the-status-of-snapshot-generation"></a>So zeigen Sie den Status der Momentaufnahmegenerierung an  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner **Lokale Veröffentlichungen** mit der rechten Maustaste auf **AdvWorksProductTrans**, und wählen Sie anschließend **Status des Momentaufnahmen-Agents anzeigen** aus:  

    ![Status des Momentaufnahmen-Agents](media/tutorial-replicating-data-between-continuously-connected-servers/viewsnapshot.png)
  
3.  Der aktuelle Status des Auftrags des Momentaufnahme-Agents für die Veröffentlichung wird angezeigt. Überprüfen Sie, ob der Auftrag für die Momentaufnahme erfolgreich war, bevor Sie mit dem nächsten Abschnitt fortfahren.
          
    Wenn Ihr SQL Server-Agent nicht ausgeführt wurde, als Sie zunächst die Veröffentlichung erstellt haben, können Sie anhand des **Status des Momentaufnahmen-Agents** bei Ihrer Veröffentlichung überprüfen, ob der Momentaufnahmen-Agent jemals ausgeführt wurde. Wurde er niemals ausgeführt, wählen Sie zum Starten Ihres Momentaufnahmen-Agents die Option **Starten** aus: 

       ![Momentaufnahmen-Agent starten](media/tutorial-replicating-data-between-continuously-connected-servers/startsnapshotagent.png)
     
       Wenn Ihnen hier ein Fehler angezeigt wird, finden Sie unter [Fehlerbehebung mit dem Momentaufnahmen-Agent](#troubleshoot-erros-with-snapshot-agent) weitere Informationen. 

  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>So fügen Sie der PAL die Anmeldung des Verteilungs-Agents hinzu  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner **Lokale Veröffentlichungen** mit der rechten Maustaste auf **AdvWorksProductTrans**, und wählen Sie anschließend **Eigenschaften** aus.  Das Dialogfeld **Veröffentlichungseigenschaften** wird angezeigt.    
  
    A. Wählen Sie die Seite **Veröffentlichungszugriffsliste** und anschließend **Hinzufügen** aus.  
    B. Klicken Sie im Dialogfeld **Veröffentlichungszugriff hinzufügen** auf <*Publisher_Machine_Name>***\repl_distribution**, und wählen Sie **OK** aus. Wählen Sie **OK** aus:

   
   ![Anmeldung zur PAL-Liste hinzufügen](media/tutorial-replicating-data-between-continuously-connected-servers/tranreplproperties.png)

**Weitere Informationen finden Sie unter:**  
[Konzepte für die Replikationsprogrammierung](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  

## <a name="create-a-subscription-to-the-transactional-publication"></a>Erstellen eines Abonnements für die Transaktionsveröffentlichung
In diesem Abschnitt erfahren Sie, wie Sie einen Abonnenten zu der zuvor erstellten Veröffentlichung hinzufügen. In diesem Tutorial wird ein Remote-Abonnent (NODE2\SQL2016) verwendet, ein Abonnement kann jedoch auch lokal zum Verleger hinzugefügt werden. 

### <a name="to-create-the-subscription"></a>So erstellen Sie das Abonnement  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner **Lokale Veröffentlichungen** mit der rechten Maustaste auf die Veröffentlichung **AdvWorksProductTrans**, und wählen Sie anschließend **Neue Abonnements** aus.  Der Assistent für neue Abonnements wird gestartet: 
 
    ![Neues Abonnement](media/tutorial-replicating-data-between-continuously-connected-servers/newsub.png)     
  
3.  Wählen Sie auf der Seite „Veröffentlichung“ die Veröffentlichung **AdvWorksProductTrans** und anschließend **Weiter** aus:  

    ![Tran.-Verleger auswählen](media/tutorial-replicating-data-between-continuously-connected-servers/selectpub.png)
  
4.  Wählen Sie auf der Seite „Speicherort des Verteilungs-Agents“ die Option **Alle Agents auf dem Verteiler ausführen** und anschließend **Weiter** aus.  Weitere Informationen zu Push- und Pullabonnements finden Sie unter [Abonnieren von Veröffentlichungen](https://docs.microsoft.com/en-us/sql/relational-databases/replication/subscribe-to-publications):

    ![Agents auf dem Verteiler ausführen](media/tutorial-replicating-data-between-continuously-connected-servers/runagentsatdist.png)
  
5.  Wählen Sie auf der Seite „Abonnenten“ die Option **Abonnent hinzufügen** und anschließend in der Dropdownliste **SQL Server-Abonnent hinzufügen** aus, wenn der Name der Abonnenteninstanz nicht angezeigt wird. Dadurch wird das Dialogfeld **Mit Server verbinden** angezeigt. Geben Sie den Namen der Abonnenteninstanz ein, und wählen Sie anschließend **Verbinden** aus.  
    
    A. Aktivieren Sie das Kontrollkästchen neben dem Namen Ihrer Abonnenteninstanz, sobald der Abonnent hinzugefügt wurde. Wählen Sie anschließend unter **Abonnementdatenbank** die Option **Neue Datenbank** aus:   

  ![Abonnentenserver hinzufügen](media/tutorial-replicating-data-between-continuously-connected-servers/addsub.png)

7. Hierdurch wird das Dialogfeld **Neue Datenbank** angezeigt. Geben Sie **ProductReplica** in das Feld **Datenbankname** ein, und wählen Sie **OK** und anschließend **Weiter** aus: 
  
    ![Datenbank für Produktreplikate](media/tutorial-replicating-data-between-continuously-connected-servers/productreplica.png)
  
8.  Wählen Sie im Dialogfeld **Sicherheit für den Verteilungs-Agent** die Schaltfläche mit den Auslassungspunkten (**…**) aus. Geben Sie <*Publisher_Machine_Name>***\repl_distribution** in das Feld **Prozesskonto** ein und anschließend das Kennwort für dieses Konto. Wählen Sie **OK** und anschließend **Weiter** aus:

    ![Verteilungskonto hinzufügen](media/tutorial-replicating-data-between-continuously-connected-servers/adddistaccount.png)
  
9. Wählen Sie **Fertig stellen** aus, um auf den verbleibenden Seiten die Standardwerte zu übernehmen und den Assistenten abzuschließen.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Festlegen der Datenbankberechtigungen auf dem Abonnenten  
  
1.  Stellen Sie eine Verbindung mit dem Abonnenten in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] her, erweitern Sie **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Anmeldungen**, und wählen Sie anschließend **Neue Anmeldung** aus.     
  
    A. Wählen Sie auf der Seite **Allgemein** unter **Anmeldename** die Option **Suche** aus, und fügen Sie die Anmeldung für <*Subscriber_Machine_Name>***\repl_distribution** hinzu.
    B. Erteilen Sie auf der Seite **Benutzerzuordnungen** **db_owner**-Anmeldezugriff für die Datenbank **ProductReplica**: 

    ![Auf Abonnenten anmelden](media/tutorial-replicating-data-between-continuously-connected-servers/loginforsub.png)

2. Wählen Sie **OK** aus, um das Dialogfeld **Neue Anmeldung** zu schließen. 

  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>So zeigen Sie den Synchronisierungsstatus des Abonnements an  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Erweitern Sie im Ordner **Lokale Veröffentlichungen** die Veröffentlichung **AdvWorksProductTrans**, klicken Sie mit der rechten Maustaste auf das Abonnement in der Datenbank **ProductReplica**, und wählen Sie anschließend **Synchronisierungsstatus anzeigen** aus. Der aktuelle Synchronisierungsstatus des Abonnements wird angezeigt:  
    ![Synchronisierungsstatus anzeigen](media/tutorial-replicating-data-between-continuously-connected-servers/viewsyncstatus.png)
3.  Wenn das Abonnement unter **AdvWorksProductTrans**nicht angezeigt wird, drücken Sie F5, um die Liste zu aktualisieren.  
  
**Weitere Informationen finden Sie unter:**  
[Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Erstellen eines Pushabonnements](../../relational-databases/replication/create-a-push-subscription.md)  
[Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  

## <a name="measuring-replication-latency"></a>Messen der Replikationswartezeit
In diesem Abschnitt verwenden Sie Überwachungstoken, um zu überprüfen, ob die Änderungen auf dem Abonnenten repliziert werden, und um die Latenzzeit zu ermitteln. Latenzzeit ist die benötigte Zeit, bis dem Abonnenten eine am Verleger vorgenommene Änderung angezeigt wird.
  
1. Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Verbindung mit dem Verleger her, erweitern Sie den Serverknoten, klicken Sie mit der rechten Maustaste auf den Ordner **Replikation**, und klicken Sie anschließend auf **Replikationsmonitor starten**:

    ![Replikationsmonitor starten](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)

2. Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie die Verlegerinstanz, und wählen Sie anschließend die Veröffentlichung **AdvWorksProductTrans** aus.  
  
    A. Wählen Sie die Registerkarte **Überwachungstoken** aus.  
    B. Wählen Sie **Überwachung einfügen** aus.    
    c. In den folgenden Spalten sehen Sie die für das Überwachungstoken benötigte Zeit: **Verleger zu Verteiler**, **Verteiler zu Abonnent**, **Gesamtlatenzzeit**. Der Wert **Ausstehend** gibt an, dass das Token einen bestimmten Punkt noch nicht erreicht hat:


   ![Überwachungstoken](media/tutorial-replicating-data-between-continuously-connected-servers/tracertoken.png)


**Siehe auch**   
[Messen der Latenzzeit und Überprüfen der Verbindungen bei Transaktionsreplikationen](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

## <a name="error-troubleshooting-methodology"></a>Problembehandlungsmethoden
In diesem Abschnitt erfahren Sie, wie Sie grundlegende Fehler bei der Replikationssynchronisierung beheben können. Beachten Sie, dass Ihnen in diesem Abschnitt vermittelt werden soll, wie Sie mit dem Ziel der Problembehandlung durch die Replikationskomponenten navigieren können. Die tatsächlichen auftretenden Fehler weichen jedoch möglicherweise von den hier erläuterten Fehlern ab und bedürfen einer anderen Lösung. In einem solchen Fall sind weitere Maßnahmen zur Problembehandlung erforderlich, die nicht Inhalt dieses Tutorials sind. 


### <a name="troubleshoot-errors-with-snapshot-agent"></a>Problembehandlung von Fehlern mit dem Momentaufnahmen-Agent
Der **Momentaufnahmen-Agent** generiert die Momentaufnahme und schreibt diese in den angegebenen Momentaufnahmeordner. 

1. Erweitern Sie bei der Replikation den Knoten **Lokale Veröffentlichung**, und wählen Sie Ihre Veröffentlichung **AdvWorksProductTrans** > **Status des Momentaufnahmen-Agents anzeigen** aus, um den Status Ihres Momentaufnahmen-Agents anzuzeigen. 
2. Wenn im **Status des Momentaufnahmen-Agents** ein Fehler gemeldet wird, können im Auftragsverlauf des **Momentaufnahmen-Agents** weitere Einzelheiten gefunden werden. Erweitern Sie **SQL Server-Agent** im **Objekt-Explorer**, und öffnen Sie den **Auftragsaktivitätsmonitor**, um darauf zuzugreifen. 

    A. Legen Sie eine Sortierung nach **Kategorie** fest, und identifizieren Sie den **Momentaufnahmen-Agent** nach der Kategorie „REPL-Snapshot“. 

    B. Klicken Sie mit der rechten Maustaste auf den **Momentaufnahmen-Agent** und auf **Verlauf anzeigen**: 

   ![Verlauf des Momentaufnahmen-Agents](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenthistory.png)
    
1. Wählen Sie im **Verlauf des Momentaufnahmen-Agents** den relevanten Protokolleintrag aus. Dieser befindet sich in der Regel ein oder zwei Zeilen *vor* dem Eintrag mit der Fehlermeldung (Fehler werden durch ein rotes X angezeigt).  Überprüfen Sie die Meldung in dem Textfeld unter den Protokollen: 

    ![Zugriff auf Momentaufnahmen-Agent verweigert](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotaccessdenied.png)

        The replication agent had encountered an exception.
        Exception Message: Access to path '\\node1\repldata.....' is denied.


  Wenn Ihre Windows-Berechtigungen für Ihren Momentaufnahmeordner nicht ordnungsgemäß konfiguriert wurden, wird Ihnen beim **Momentaufnahmen-Agent** der Fehler „Zugriff verweigert“ angezeigt. Sie müssen die Berechtigungen für das Konto <*Publisher_Machine_Name>***\repl_snapshot** in Ihrem Ordner „repldata“ überprüfen. Weitere Informationen finden Sie unter [Erstellen einer Freigabe für den Momentaufnahmeordner und Zuweisen von Berechtigungen](tutorial-preparing-the-server-for-replication.md#create-a-share-for-the-snapshot-folder-and-assign-permissions).

### <a name="troubleshoot-errors-with-log-reader-agent"></a>Problembehandlung von Fehlern mit dem Protokolllese-Agent
Der **Protokolllese-Agent** stellt eine Verbindung mit Ihrer Verlegerdatenbank her und überprüft das Transaktionsprotokoll auf Transaktionen, die mit „für Replikation“ markiert sind. Anschließend fügt er diese Transaktionen zur **Verteilungsdatenbank** hinzu. 

1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Verbindung mit dem Verleger her, erweitern Sie den Serverknoten, klicken Sie mit der rechten Maustaste auf den Ordner **Replikation**, und klicken Sie anschließend auf **Replikationsmonitor starten**:  

    ![Replikationsmonitor starten](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)
  
    Der Replikationsmonitor wird gestartet: ![Replikationsmonitor](media/tutorial-replicating-data-between-continuously-connected-servers/replmonitor.png) 
   
2. Das rote X deutet darauf hin, dass die Veröffentlichung nicht synchronisiert wurde. Erweitern Sie auf der linken Seite das Kontrollkästchen **Meine Verleger** und anschließend die relevanten Verlegerserver.  
  
3.  Wählen Sie auf der linken Seite die Veröffentlichung **AdvWorksProductTrans** aus, und suchen Sie anschließend zur Problemermittlung auf einer der Registerkarten nach dem roten X. In diesem Fall befindet sich das rote X auf der Registerkarte **Agents**. Dies deutet darauf hin, dass bei einem der Agents ein Fehler aufgetreten ist: 

    ![Agent-Fehler](media/tutorial-replicating-data-between-continuously-connected-servers/agenterror.png)

4. Wählen Sie die Registerkarte **Agents** aus, um zu ermitteln, bei welchem Agent der Fehler aufgetreten ist: 

    ![Fehlschlagen des Protokolllesers](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentfailure.png)


5. In dieser Ansicht werden Ihnen zwei Agents angezeigt: der **Momentaufnahmen-Agent** und der **Protokolllese-Agent**. Der Agent, bei dem der Fehler aufgetreten ist, ist mit einem roten X versehen. In diesem Fall befindet sich das rote X bei dem **Protokolllese-Agent** und deutet darauf hin, dass dort ein Problem vorliegt. Doppelklicken Sie auf die Zeile, in welcher der Fehler gemeldet wird. In diesem Fall ist dies der **Protokolllese-Agent**. Hierdurch wird der **Agent-Verlauf** des von Ihnen ausgewählten Agents gestartet. In diesem Fall ist dies der Verlauf des **Protokolllese-Agents**. Der Verlauf enthält weitere Informationen zu dem Fehler: 
    
    ![Fehler beim Protokolllese-Agent](media/tutorial-replicating-data-between-continuously-connected-servers/logreadererror.png)

       Status: 0, code: 20011, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.
       The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.
       Status: 0, code: 15517, text: 'Cannot execute as the database principal because the principal "dbo" does not exist, this type of principal cannot be impersonated, or you do not have permission.'.
       Status: 0, code: 22037, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.        

6. Der oben angegebene Fehler wird normalerweise dadurch verursacht, dass der Besitzer der Verlegerdatenbank nicht ordnungsgemäß festgelegt wurde. Dies geschieht in der Regel, wenn eine Datenbank wiederhergestellt wurde. Wenn Sie dies überprüfen möchten, erweitern Sie **Datenbanken** in **Objekt-Explorer**, und klicken Sie mit der rechten Maustaste auf **AdventureWorks2012** > **Eigenschaften**. Überprüfen Sie, ob auf der Seite **Dateien** ein Besitzer vorhanden ist. Wenn dieses Feld leer ist, ist dies der wahrscheinliche Grund für Ihr Problem: 

    ![Datenbankeigenschaften](media/tutorial-replicating-data-between-continuously-connected-servers/dbproperties.png)

7. Wenn das Feld „Besitzer“ auf der Seite **Dateien** leer ist, öffnen Sie im Bereich der Datenbank **AdventureWorks2012** ein **Neues Abfragefenster**. Führen Sie folgenden T-SQL-Codeausschnitt aus:

    ```sql
    -- set the owner of the database to 'sa' or a specific user account, without the brackets. 
    EXEC sp_changedbowner '<useraccount>'
    -- example for sa: exec sp_changedbowner 'sa'
    -- example for user account: exec sp_changedbowner 'sqlrepro\administrator' 
    ```

8. Sie müssen den **Protokolllese-Agent** neu starten. Erweitern Sie hierzu den Knoten **SQL Server-Agent** im **Objekt-Explorer**, und öffnen Sie den **Auftragsaktivitätsmonitor**. Legen Sie eine Sortierung nach **Kategorie** fest, und identifizieren Sie den **Protokolllese-Agent** nach der Kategorie **'REPL-LogReader'**. Klicken Sie mit der rechten Maustaste auf den Auftrag des **Protokolllese-Agents** und auf **Auftrag starten bei Schritt...**: 

    ![Protokolllese-Agent neu starten](media/tutorial-replicating-data-between-continuously-connected-servers/startjobatstep.png)

9. Überprüfen Sie, ob Ihre Veröffentlichung jetzt synchronisiert wird, indem Sie den **Replikationsmonitor** erneut öffnen. Wenn er nicht bereits geöffnet ist, können Sie ihn finden, indem Sie im **Objekt-Explorer** mit der rechten Maustaste auf **Replikation** klicken. 
10. Wählen Sie die Veröffentlichung **AdvWorksProductTrans** und anschließend die Registerkarte **Agents** aus. Doppelklicken Sie auf den **Protokolllese-Agent**, um den Agent-Verlauf zu öffnen. Sie müssten jetzt sehen können, dass der **Protokolllese-Agent** ausgeführt wird und entweder Befehle repliziert oder über „Keine replizierten Transaktionen“ verfügt:

    ![Log Reader wird ausgeführt](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderrunning.png)

### <a name="troubleshoot-errors-with-distribution-agent"></a>Problembehandlung von Fehlern mit dem Verteilungs-Agent
Der **Verteilungs-Agent** überträgt gefundene Daten in die **Verteilungsdatenbank** und wendet diese anschließend auf den Abonnenten an. 

1. Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Verbindung mit dem Verleger her, erweitern Sie den Serverknoten, klicken Sie mit der rechten Maustaste auf den Ordner **Replikation**, und wählen Sie anschließend **Replikationsmonitor starten** aus.  
2. Wählen Sie im **Replikationsmonitor** die Veröffentlichung **AdvWorksProductTrans** und anschließend die Registerkarte **Alle Abonnements** aus. Klicken Sie mit der rechten Maustaste auf das Abonnement und anschließend auf **Details anzeigen**:

    ![Verteilerdetails anzeigen](media/tutorial-replicating-data-between-continuously-connected-servers/viewdetails.png)

2. Das Dialogfeld **Distributor to Subscriber History** (Verlauf von Verteiler zu Abonnent) wird geöffnet und zeigt an, welches Problem bei dem Agent aufgetreten ist: 

     ![Fehler im Verlauf von Verteiler zu Abonnent](media/tutorial-replicating-data-between-continuously-connected-servers/disthistoryerror.png)
    
        Error messages:
        Agent 'NODE1\SQL2016-AdventureWorks2012-AdvWorksProductTrans-NODE2\SQL2016-7' is retrying after an error. 89 retries attempted. See agent job history in the Jobs folder for more details.

3. Die Fehlermeldung gibt an, dass der **Verteilungs-Agent** den Vorgang wiederholt. Erweitern Sie den **SQL Server-Agent** im **Objekt-Explorer** > **Auftragsaktivitätsmonitor**, um weitere Informationen hierzu zu erhalten. Sortieren Sie die Aufträge nach **Kategorie**. 

    A. Identifizieren Sie den **Verteilungs-Agent** nach der Kategorie **„REPL-Verteilung“**. Klicken Sie mit der rechten Maustaste auf den Agent und anschließend auf **Verlauf anzeigen**:

    ![Verlauf von Verteiler zu Abonnent anzeigen](media/tutorial-replicating-data-between-continuously-connected-servers/viewdistagenthistory.png)

5. Wählen Sie einen der Fehlereinträge aus, und zeigen Sie die Fehlermeldung im unteren Bereich des Fensters an:  

    ![Falsches Kennwort für den Verteiler-Agent](media/tutorial-replicating-data-between-continuously-connected-servers/distpwwrong.png)
    
        Message:
        Unable to start execution of step 2 (reason: Error authenticating proxy NODE1\repl_distribution, system error: The user name or password is incorrect.)

6. Dieser Fehler deutet darauf hin, dass das vom **Verteilungs-Agent** verwendete Kennwort falsch ist. Erweitern Sie zum Beheben dieses Problems den Knoten **Replikation** im **Objekt-Explorer**, klicken Sie mit der rechten Maustaste auf das Abonnement > **Eigenschaften**. Wählen Sie die Auslassungspunkte (...) neben dem **Agent-Prozesskonto** aus, und ändern Sie das Kennwort:

    ![Kennwort für Verteilungs-Agent ändern](media/tutorial-replicating-data-between-continuously-connected-servers/distagentpwchange.png)

7. Überprüfen Sie erneut Ihren **Replikationsmonitor**. Sie können diesen finden, indem Sie mit der rechten Maustaste auf **Replikation** im **Objekt-Explorer** klicken. Ein rotes X unter **alle Abonnements** gibt an, dass bei dem **Verteilungs-Agent** weiterhin ein Fehler auftritt. Öffnen Sie den **Distributor to Subscriber History** (Verlauf von Verteiler zu Abonnent), indem Sie mit der rechten Maustaste auf das Abonnement in **Replikationsmonitor** > **Details anzeigen** klicken. Hier lautet der Fehler nun anders: 

    ![Verteiler-Agent kann keine Verbindung herstellen](media/tutorial-replicating-data-between-continuously-connected-servers/distagentcantconnect.png)
           
        Connecting to Subscriber 'NODE2\SQL2016'        
        Agent message code 20084. The process could not connect to Subscriber 'NODE2\SQL2016'.
        Number:  18456
        Message: Login failed for user 'NODE2\repl_distribution'.

8. Dieser Fehler gibt an, dass der **Verteiler-Agent** keine Verbindung mit dem Abonnenten herstellen konnte, da die Anmeldung von Benutzer **NODE2\repl_distribution** fehlgeschlagen ist. Sie können dies näher untersuchen, indem Sie eine Verbindung mit dem Abonnenten herstellen und das *aktuelle* **SQL-Fehlerprotokoll** unter dem Knoten **Management** im **Objekt-Explorer** öffnen: 

    ![Fehler bei der Anmeldung des Abonnenten](media/tutorial-replicating-data-between-continuously-connected-servers/loginfailed.png) Wenn Ihnen diese Fehlermeldung angezeigt wird, bedeutet dies, dass die Anmeldung des Abonnenten nicht vorhanden ist. Informationen zur Behebung dieses Problems finden Sie unter [Festlegen von Datenbankberechtigungen für den Abonnenten](#setting-database-permissions-at-the-subscriber).

9. Überprüfen Sie erneut den **Replikationsmonitor**, sobald der Anmeldefehler behoben wurde. Wenn alle Probleme behoben wurden, müssten Ihnen neben dem **Veröffentlichungsnamen** ein grüner Pfeil und unter **Alle Abonnements** der Status **Wird ausgeführt** angezeigt werden. Klicken Sie erneut mit der rechten Maustaste auf **Abonnement**, um **Distributor to Subscriber History** (Verlauf von Verteiler zu Abonnent) zu starten und zu überprüfen, ob die Ausführung erfolgreich war. Wenn der Verteilungs-Agent zum ersten Mal ausgeführt wird, können Sie sehen, dass die Momentaufnahme für den Abonnenten massenkopiert wurde, wie in der nachfolgenden Abbildung veranschaulicht ist: 

     ![Verteilungs-Agent erfolgreich ausgeführt](media/tutorial-replicating-data-between-continuously-connected-servers/distagentsuccess.png)   

  ## <a name="next-steps"></a>Nächste Schritte
Sie haben Ihre Verleger und Ihren Abonnenten erfolgreich für Ihre Transaktionsreplikation konfiguriert.  Nun können Sie in der **Produkt**-Tabelle beim Verleger Daten einfügen, aktualisieren oder löschen. Anschließend können Sie die **Produkt**-Tabelle beim Abonnenten abfragen, um die replizierten Änderungen anzuzeigen. Im nächsten Artikel lernen Sie, wie eine Mergereplikation konfiguriert wird.  

Für weitere Informationen zum nächsten Artikel blättern
> [!div class="nextstepaction"]
> [Nächste Schritte](tutorial-replicating-data-with-mobile-clients.md)

  
