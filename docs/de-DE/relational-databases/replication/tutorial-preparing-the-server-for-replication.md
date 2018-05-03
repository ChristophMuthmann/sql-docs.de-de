---
title: 'Tutorial: Vorbereiten von SQL Server auf die Replikation (Verleger, Verteiler und Abonnent) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 04/02/2018
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
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1468095ba959f7baf383b68cfaab65dab2591af6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-prepare-sql-server-for-replication---publisher-distributor-subscriber"></a>Tutorial: Vorbereiten von SQL Server auf die Replikation (Verleger, Verteiler und Abonnent)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Es ist wichtig, einen Sicherheitsplan zu erstellen, bevor Sie die Replikationstopologie konfigurieren. In diesem Lernprogramm erfahren Sie, wie Sie eine Replikationstopologie besser sichern und die Verteilung konfigurieren können. Dieser Vorgang stellt den ersten Schritt für die Replikation von Daten dar. Es ist erforderlich, dieses Lernprogramm vor allen anderen Lernprogrammen abzuschließen.  
  
> [!NOTE]  
> Für das sichere Replizieren von Daten zwischen Servern empfiehlt es sich, alle Empfehlungen unter [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)zu implementieren.  
  
## <a name="what-you-will-learn"></a>Lernziele  
In diesem Tutorial erfahren Sie, wie Sie einen Server vorbereiten, sodass die Replikation sicher und mit den niedrigsten Berechtigungen ausgeführt werden kann.  

In diesem Tutorial lernen Sie Folgendes:
> [!div class="checklist"]
> * Erstellen von Windows-Konten für die Replikation
> * Vorbereiten des Momentaufnahmeordners
> * Konfigurieren der Verteilung

## <a name="prerequisites"></a>Voraussetzungen
Dieses Tutorial ist für Benutzer vorgesehen, die mit grundlegenden Datenbankvorgängen vertraut sind, aber nur über begrenzte Erfahrungen in Bezug auf die Replikation verfügen. 

Für dieses Tutorial müssen auf Ihrem System SQL Server Management Studio (SSMS) sowie die folgenden Komponenten installiert sein:  
  
-   Auf dem Verlegerserver (Quelle):  
  
    -   Jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version, außer SQL Server Express oder SQL Compact. Diese Editionen können nicht als Verleger für Replikationen verwendet werden.   
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] -Beispieldatenbank Aus Sicherheitsgründen werden die Beispieldatenbanken standardmäßig nicht installiert.  
  
-   Abonnentenserver (Ziel):  
  
    -   Eine beliebige Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mit Ausnahme von [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] kann nicht als Abonnent einer Transaktionsreplikation fungieren.  
  
- Installieren Sie [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Installieren Sie die [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Laden Sie eine [AdventureWorks-Beispieldatenbank](https://github.com/Microsoft/sql-server-samples/releases) herunter. Weitere Informationen zum Wiederherstellen einer Datenbank in SSMS finden Sie unter [Restoring a Database (Wiederherstellen einer Datenbank)](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 
    
>[!NOTE]
> - Die Replikation wird für SQL Server-Versionen, zwischen denen mehr als zwei Versionen liegen, nicht unterstützt. Weitere Informationen finden Sie unter [In der Replikationstopologie unterstützte SQL-Versionen](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/).
> - In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]muss eine Verbindung mit dem Verleger und dem Abonnenten hergestellt werden. Dazu wird ein Anmeldename verwendet, der Mitglied der festen Serverrolle **sysadmin** ist. Weitere Informationen zur Rolle „sysadmin“ finden Sie unter [Rollen auf Serverebene](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles).  


**Geschätzte Dauer: 30 Minuten**
  
## <a name="create-windows-accounts-for-replication"></a>Erstellen von Windows-Konten für die Replikation
In diesem Abschnitt erstellen Sie Windows-Konten zum Ausführen von Replikations-Agents. Sie erstellen für die folgenden Agents ein separates Windows-Konto auf dem lokalen Server:  
  
|Agent|Speicherort|Kontoname|  
|---------|------------|----------------|  
|Momentaufnahme-Agent|Verleger|<*machine_name*>\repl_snapshot|  
|Protokolllese-Agent|Verleger|<*machine_name*>\repl_logreader|  
|Verteilungs-Agent|Verleger und Abonnent|<*machine_name*>\repl_distribution|  
|Merge-Agent|Verleger und Abonnent|<*machine_name*>\repl_merge|  
  
> [!NOTE]  
> In den Tutorials zur Replikation nutzen der Verleger und der Verteiler dieselbe Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (NODE1\SQL2016), während die Abonnenteninstanz (NODE2\SQL2016) remote ist. Verleger und Abonnent können dieselbe Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gemeinsam verwenden; dies ist jedoch keine Anforderung. Wenn der Verleger und Abonnent dieselbe Instanz verwenden, sind die Schritte zum Erstellen von Konten auf dem Verleger nicht erforderlich.  

### <a name="create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>Erstellen lokaler Windows-Konten für Replikations-Agents auf dem Verleger
  
1.  Öffnen Sie auf dem Verleger in der Systemsteuerung in **Verwaltung** das Tool **Computerverwaltung** .  
  
2.  Erweitern Sie unter **System**den Eintrag **Lokale Benutzer und Gruppen**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Benutzer**, und klicken Sie dann auf **Neuer Benutzer**.  
     
4.  Geben Sie **repl_snapshot** im Feld **Benutzername** ein, geben Sie das Kennwort und weitere relevante Informationen an, und klicken Sie anschließend auf **Erstellen**, um das Konto „repl_snapshot“ zu erstellen: 

       ![Neuer Benutzer](media/tutorial-preparing-the-server-for-replication/newuser.png)
  
5.  Wiederholen Sie den letzten Schritt, um die Konten „repl_logreader“, „repl_distribution“ und „repl_merge“ zu erstellen:  
 
    ![Replikationsbenutzer](media/tutorial-preparing-the-server-for-replication/replusers.png)
  
6.  Klicken Sie auf **Schließen**.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>So erstellen Sie lokale Windows-Konten für Replikations-Agents auf dem Abonnenten  
  
1.  Öffnen Sie auf dem Abonnenten in der Systemsteuerung in **Verwaltung** das Tool **Computerverwaltung** .  
  
2.  Erweitern Sie unter **System**den Eintrag **Lokale Benutzer und Gruppen**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Benutzer**, und klicken Sie dann auf **Neuer Benutzer**.  
  
4.  Geben Sie **repl_distribution** im Feld **Benutzername** ein, geben Sie das Kennwort und weitere relevante Informationen an, und klicken Sie anschließend auf **Erstellen**, um das Konto „repl_distribution“ zu erstellen.  
  
5.  Wiederholen Sie den letzten Schritt, um das Konto repl_merge zu erstellen.  
  
6.  Klicken Sie auf **Schließen**.  

**Siehe auch:** [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)  

## <a name="prepare-the-snapshot-folder"></a>Vorbereiten des Momentaufnahmeordners
In diesem Abschnitt erfahren Sie, wie Sie den Momentaufnahmeordner konfigurieren, in dem die Veröffentlichungsmomentaufnahme erstellt und gespeichert wird. 

### <a name="create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>Erstellen einer Freigabe für den Momentaufnahmeordner und Zuweisen von Berechtigungen  
  
1.  Navigieren Sie im Windows-Explorer zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenordner. Der Standardspeicherort lautet C:\Programme\Microsoft SQL Server\MSSQL.X\MSSQL\Data.  
  
2.  Erstellen Sie einen neuen Ordner mit dem Namen **repldata**.  
  
3.  Klicken Sie mit der rechten Maustaste auf diesen Ordner, und wählen Sie **Eigenschaften** aus.  
  
    A. Klicken Sie auf der Registerkarte **Freigabe** im Dialogfeld **repldata Properties** (Eigenschaften von repldata) auf **Erweiterte Freigabe**.  
  
    B. Klicken Sie im Dialogfeld **Erweiterte Freigabe** auf **Diesen Ordner freigeben**, und klicken Sie dann auf **Berechtigungen**:  

       ![Freigabe von Replikationsdaten](media/tutorial-preparing-the-server-for-replication/repldata.png)

6.  Klicken Sie im Dialogfeld **Berechtigungen für repldata** auf **Hinzufügen**. Geben Sie im Textfeld **Select User, Computers, Service Account, or Groups** (Benutzer, Computer, Dienstkonten oder Gruppen auswählen) den Namen des zuvor erstellten Momentaufnahme-Agent-Kontos ein: <*Name_des_Verlegercomputers>***\repl_snapshot**. Klicken Sie auf **Namen überprüfen** und dann auf **OK**:  

    ![Freigabeberechtigungen hinzufügen](media/tutorial-preparing-the-server-for-replication/addshareperms.png)

7. Wiederholen Sie Schritt 6, um die anderen beiden Konten hinzuzufügen, die zuvor erstellt wurden: <*Name_des_Verlegercomputers>***\repl_merge** und <*Name_des_Verlegercomputers>***\repl_distribution**.

8. Sobald diese drei Konten hinzugefügt wurden, weisen Sie die folgenden Berechtigungen zu:      
    - repl_distribution - Lesezugriff  
    - repl_merge - Lesezugriff  
    - repl_snapshot - Vollzugriff    

  ![Freigabeberechtigungen](media/tutorial-preparing-the-server-for-replication/sharedpermissions.png)

9. Sobald die Freigabeberechtigungen ordnungsgemäß konfiguriert sind, klicken Sie auf **OK**, um das Dialogfeld **Permissions for repldata** (Berechtigungen für repldata) zu schließen. Klicken Sie auf **OK**, um das Dialogfeld **Erweiterte Freigabe** zu schließen. 

10.  Klicken Sie unter **repldata Properties** auf die Registerkarte **Sicherheit**, und wählen Sie **Bearbeiten** aus:  

       ![Sicherheit bearbeiten](media/tutorial-preparing-the-server-for-replication/editsecurity.png)   

11. Klicken Sie im Dialogfeld **Permissions for repldata** auf **Hinzufügen...**. Geben Sie im Textfeld **Select User, Computers, Service Account, or Groups** (Benutzer, Computer, Dienstkonten oder Gruppen auswählen) den Namen des zuvor erstellten Momentaufnahme-Agent-Kontos ein: <*Name_des_Verlegercomputers>***\repl_snapshot**. Klicken Sie auf **Namen überprüfen** und dann auf **OK**:  

    ![Sicherheitsberechtigungen hinzufügen](media/tutorial-preparing-the-server-for-replication/addsecuritypermissions.png)

  
12.  Wiederholen Sie den vorherigen Schritt, um Berechtigungen für den Verteilungs-Agent (*Name_des_Verlegercomputers>***\repl_distribution**) und für den Merge-Agent (* Name_des_verlegercomputers>***\repl_merge**) hinzuzufügen.  
    
  
13. Überprüfen Sie, ob die folgenden Berechtigungen gewährt wurden.  
  
    - repl_distribution - Lesezugriff
    - repl_merge - Lesezugriff
    - repl_snapshot - Vollzugriff   
 
    ![Benutzerberechtigungen für Replikationsdaten](media/tutorial-preparing-the-server-for-replication/replpermissions.png) 

14. Klicken Sie erneut auf die Registerkarte **Freigabe**, und notieren Sie sich den **Netzwerkpfad** für die Freigabe. Sie benötigen diesen Pfad später, wenn Sie den **Momentaufnahmeordner** konfigurieren:  

    ![Netzwerkpfad](media/tutorial-replicating-data-between-continuously-connected-servers/networkpath.png)

15. Klicken Sie auf **OK**, um das Dialogfeld **repldata Properties** zu schließen. 
 
**Weitere Informationen finden Sie unter:**  
[Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  

## <a name="configure-distribution"></a>Konfigurieren der Verteilung
In diesem Abschnitt konfigurieren Sie die Verteilung auf dem Verleger und legen die erforderlichen Berechtigungen für die Verteilungs- und Veröffentlichungsdatenbanken fest. Wenn der Verteiler bereits konfiguriert wurde, müssen zuerst die Veröffentlichung und die Verteilung deaktiviert werden, bevor Sie mit diesem Abschnitt beginnen. Tun Sie dies nicht, falls Sie eine vorhandene Replikationstopologie beibehalten müssen, vor allem in der Produktion.   
  
Das Konfigurieren eines Verlegers mit einem Remoteverteiler wird in diesem Lernprogramm nicht behandelt.  

### <a name="configure-distribution-at-the-publisher"></a>Konfigurieren der Verteilung auf dem Verleger  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Replikation**, und klicken Sie anschließend auf **Verteilung konfigurieren**:  

    ![Konfigurieren der Verteilung](media/tutorial-preparing-the-server-for-replication/configuredistribution.png)
  
    > [!NOTE]  
    > Wenn Sie **localhost[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anstelle des tatsächlichen Servernamens verwendet haben, um eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herzustellen, werden Sie in einer Warnmeldung darauf hingewiesen, dass**  nicht in der Lage ist, eine Verbindung mit dem Server **"localhost"** herzustellen. Klicken Sie im Warnungsdialogfeld auf **OK**. Ändern Sie im Dialogfeld **Verbindung mit Server herstellen** die Angabe für **Servername** von **localhost** in den Namen des Servers. Wählen Sie **Verbinden**.  
  
    Der Verteilungskonfigurations-Assistent wird gestartet.  
  
3.  Wählen Sie auf der Seite **Verteiler** die Option **'ServerName' will act as its own Distributor; SQL Server will create a distribution database and log** („ServerName“ agiert als eigener Verteiler. SQL Server erstellt eine Verteilungsdatenbank und ein Verteilungsprotokoll) aus, und klicken Sie anschließend auf **Weiter**:  

    ![Server agiert als eigener Verteiler](media/tutorial-preparing-the-server-for-replication/serverdistributor.png)
  
4.  Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent nicht ausgeführt wird, klicken Sie auf der Seite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-**Agent-Start** auf **Ja**, und konfigurieren Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Dienst, sodass er automatisch startet. Wählen Sie **Weiter**aus.  

     
5.  Geben Sie den Pfad \\\\<*Name_des_Verlegercomputers>***\repldata** im Textfeld **Momentaufnahmeordner** ein, und klicken Sie dann auf **Weiter**. Dieser Pfad sollte mit dem übereinstimmen, was zuvor im Eigenschaftenordner von „repldata“ unter **Netzwerkpfad** nach dem Konfigurieren der Freigabeeigenschaften angezeigt wurde: 

    ![Momentaufnahmeordner für Replikationsdaten](media/tutorial-preparing-the-server-for-replication/repldatasnapshot.png)
  
6.  Übernehmen Sie die Standardwerte auf den restlichen Seiten des Assistenten:  
    
    ![Standardwerte des Verteilungs-Assistenten](media/tutorial-preparing-the-server-for-replication/distributionwizarddefaults.png)
  
7.  Klicken Sie auf **Fertig stellen**, um die Verteilung zu aktivieren. 

    Beim Konfigurieren des Verteilers kann dieser Fehler angezeigt werden. Es weist darauf hin, dass das Konto, mit dem das SQL Server-Agent-Konto gestartet wird, kein Administrator im System ist. Sie müssen den SQL Server-Agent daher entweder manuell starten und dem bestehenden Konto diese Berechtigungen gewähren oder das Konto ändern, das der SQL Server-Agent nutzt: 

     ![Fehler beim Starten des Agents](media/tutorial-preparing-the-server-for-replication/startingagenterror.png)

    Wenn SQL Server Management Studio mit Administratorrechten ausgeführt wird, können Sie den SQL-Agent manuell innerhalb von SSMS starten:  
        ![Agent in SSMS starten](media/tutorial-preparing-the-server-for-replication/ssmsstartagent.png) 

    >[!NOTE]
    > Wenn der SQL-Agent nicht sichtbar gestartet wird, klicken Sie in SSMS mit der rechten Maustaste auf den SQL Server-Agent und dann auf **Aktualisieren**.  Wenn er weiterhin beendet bleibt, müssen Sie ihn manuell über den **SQL Server-Konfigurations-Manager** starten.    
  
### <a name="setting-database-permissions-at-the-publisher"></a>Festlegen der Datenbankberechtigungen auf dem Verleger  
  
1.  Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] den Knoten **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Anmeldungen**, und wählen Sie anschließend **Neue Anmeldung** aus:  

    ![Neue Anmeldung](media/tutorial-preparing-the-server-for-replication/newlogin.png)
  
2.  Klicken Sie auf der Seite **Allgemein** auf **Suchen**, geben Sie in das Feld **Enter the object name to select** (Namen des auszuwählenden Objekts eingeben) <*Name_des_Verlegercomputers>***\repl_snapshot** ein, und klicken Sie auf **Namen überprüfen** sowie **OK**:  

    ![Replikationsmomentaufnahmeanmeldung hinzufügen](media/tutorial-preparing-the-server-for-replication/addsnapshotlogin.png)
  
3.  Wählen Sie auf der Seite **Benutzerzuordnung** in der Liste **Benutzer, die dieser Anmeldung zugeordnet sind** sowohl die **Verteilungs** - als auch die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank aus.  
  
    Wählen Sie in der Liste „Mitgliedschaft in Datenbankrolle für“ die Rolle **db_owner** für die Anmeldung bei beiden Datenbanken aus:  

    ![Replikationsmomentaufnahme „db_owner“](media/tutorial-preparing-the-server-for-replication/dbowner.png)
  
4.  Klicken Sie auf **OK**, um die Anmeldung zu erstellen.  
  
5.  Wiederholen Sie die Schritte 1 bis 4, um eine Anmeldung für die anderen lokalen Konten (repl_distribution, repl_logreader und repl_merge) zu erstellen. Diese Anmeldungen müssen Benutzern zugeordnet werden, die Mitglieder der festen Datenbankrolle **db_owner** in den Datenbanken **distribution** und **AdventureWorks** sind:  

    ![Replikationsbenutzer in SSMS](media/tutorial-preparing-the-server-for-replication/usersinssms.png)
  
  
**Weitere Informationen finden Sie unter:**  
[Verteilung konfigurieren](../../relational-databases/replication/configure-distribution.md)  
[Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md)  

## <a name="next-steps"></a>Nächste Schritte
Sie haben Ihren Server jetzt erfolgreich für die Replikation vorbereitet. Im nächsten Artikel erfahren Sie, wie Sie die Transaktionsreplikation konfigurieren. 

Für weitere Informationen zum nächsten Artikel blättern
> [!div class="nextstepaction"]
> [Nächste Schritte](tutorial-replicating-data-between-continuously-connected-servers.md)

  
  
