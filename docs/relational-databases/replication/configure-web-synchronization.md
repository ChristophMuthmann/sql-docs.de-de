---
title: Konfigurieren der Websynchronisierung | Microsoft Dokumentation
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL10.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
helpviewer_keywords:
- Web synchronization, security best practices
- Web synchronization, configuring
ms.assetid: 21f8e4d4-cd07-4856-98f0-9c9890ebbc82
caps.latest.revision: "74"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4da5fe724a52ec84a6177db09f58f1cbe97e0b9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-web-synchronization"></a>Konfigurieren der Websynchronisierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Die Websynchronisierungsoption für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Mergereplikation ermöglicht die Datenreplikation mithilfe des HTTPS-Protokolls über das Internet. Um die Websynchronisierung zu verwenden, müssen Sie zuerst die folgenden Konfigurationsaktionen ausführen:  
  
1.  Erstellen Sie neue Domänenkonten und ordnen Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen zu.  
  
2.  Konfigurieren Sie den Computer, auf dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internetinformationsdienste (Internet Information Services, IIS) ausgeführt wird, für die Synchronisierung von Abonnements.  
  
3.  Konfigurieren Sie eine Mergeveröffentlichung für die Websynchronisierung.  
  
4.  Konfigurieren Sie ein oder mehrere Abonnements zur Verwendung der Websynchronisierung.  
  
> [!NOTE]  
>  Wenn Sie große Datenmengen replizieren oder umfangreiche Datentypen wie **varchar(max)**verwenden möchten, lesen Sie den Abschnitt "Replizieren großer Datenmengen" in diesem Thema.  
  
 Um die Websynchronisierung erfolgreich einzurichten, müssen Sie entscheiden, wie die Sicherheit gemäß bestimmter Anforderungen und Richtlinien konfiguriert werden soll. Es wird empfohlen, diese Entscheidungen zu treffen und die notwendigen Konten zu erstellen, bevor Sie IIS, die Veröffentlichung und die Abonnements konfigurieren.  
  
 In den folgenden Schritten wird aus Platzgründen eine vereinfachte Sicherheitskonfiguration mit lokalen Konten beschrieben. Diese vereinfachte Konfiguration ist für Installationen geeignet, bei denen IIS und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verleger und -Verteiler auf dem gleichen Computer ausgeführt werden, obwohl es viel wahrscheinlicher ist (und empfohlen wird), dass eine Multiservertopologie für eine Produktionsinstallation verwendet wird. Sie können in diesen Schritten die lokalen Konten durch Domänenkonten ersetzen.  
  
## <a name="creating-new-accounts-and-mapping-sql-server-logins"></a>Erstellen von neuen Konten und Zuordnen von SQL Server-Anmeldungen  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung (replisapi.dll) stellt eine Verbindung mit dem Verleger durch Identitätswechsel des für den Anwendungspool angegebenen Kontos her, der der Replikationswebsite zugeordnet ist.  
  
 Das für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung verwendete Konto muss über die unter [Merge Agent Security](../../relational-databases/replication/merge-agent-security.md)im Abschnitt "Herstellen einer Verbindung mit dem Verleger oder dem Verteiler" beschriebenen Berechtigungen verfügen. Zusammengefasst muss das Konto folgende Bedingungen erfüllen:  
  
-   Es muss Mitglied der Veröffentlichungszugriffsliste (PAL) sein.  
  
-   Es muss einer mit einem Benutzer in der Veröffentlichungsdatenbank verknüpften Anmeldung zugeordnet sein.  
  
-   Es muss einer mit einem Benutzer in der Verteilungsdatenbank verknüpften Anmeldung zugeordnet sein.  
  
-   Es muss über Leseberechtigungen für die Momentaufnahmefreigabe verfügen.  
  
 Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation das erste Mal verwenden, müssen Sie auch Konten und Anmeldungen für die Replikations-Agents erstellen. Weitere Informationen finden Sie in diesem Thema in den Abschnitten "Konfigurieren der Veröffentlichung" und "Konfigurieren des Abonnements".  
  
 Bevor Sie die Websynchronisierung konfigurieren, sollten Sie den Abschnitt "Bewährte Methoden bezüglich der Sicherheit bei der Websynchronisierung" in diesem Thema lesen. Weitere Informationen zur Sicherheit bei der Websynchronisierung finden Sie unter [Security Architecture for Web Synchronization](../../relational-databases/replication/security/security-architecture-for-web-synchronization.md).  
  
## <a name="configuring-the-computer-that-is-running-iis"></a>Konfigurieren des Computers, auf dem IIS ausgeführt wird  
 Für die Websynchronisierung ist es erforderlich, IIS zu installieren und zu konfigurieren. Sie benötigen die URL zur Replikationswebsite, bevor Sie eine Veröffentlichung zur Verwendung der Websynchronisierung konfigurieren können.  
  
 Die Websynchronisierung wird auf IIS ab Version 5.0 unterstützt. Der Assistent zum Konfigurieren der Websynchronisierung wird auf IIS Version 7.0 nicht unterstützt. Beginnend mit SQL Server 2012, empfiehlt sich für die Nutzung der Web-Sync-Komponente auf dem IIS-Server die Installation des SQL Servers mit Replikation. Dabei kann es sich um die kostenlose SQL Server Express Edition handeln.  
  
 SSL ist für die Websynchronisierung erforderlich. Sie benötigen ein von einer Zertifizierungsstelle ausgestelltes Sicherheitszertifikat. Nur zu Testzwecken können Sie ein selbst ausgestelltes Sicherheitszertifikat verwenden.  
   
  
 **So konfigurieren Sie IIS für die Websynchronisierung**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Konfigurieren von IIS für die Websynchronisierung](../../relational-databases/replication/configure-iis-for-web-synchronization.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Konfigurieren von IIS 7 für die Websynchronisierung](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md)  
  
## <a name="creating-a-web-garden"></a>Erstellen eines Webgartens  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung unterstützt zwei gleichzeitige Synchronisierungsvorgänge pro Thread. Das Überschreiten dieser Grenze kann dazu führen, dass die Replikationsüberwachung nicht mehr antwortet. Die Anzahl der replisapi.dll zugeordneten Threads wird von der Eigenschaft "Maximale Anzahl von Arbeitsprozessen" des Anwendungspools bestimmt. Standardmäßig ist diese Eigenschaft auf 1 festgelegt.  
  
 Erhöhen Sie den Wert der Eigenschaft "Maximale Anzahl von Arbeitsprozessen", um eine größere Anzahl gleichzeitiger Synchronisierungsvorgänge pro CPU zu unterstützen. Das horizontale Skalieren durch Erhöhen der Anzahl von Arbeitsprozessen pro CPU wird als Erstellen eines "Webgartens" bezeichnet.  
  
 Ein Webgarten lässt die gleichzeitige Synchronisierung von mehr als zwei Abonnenten zu. Er erhöht außerdem die CPU-Auslastung durch replisapi.dll, was sich negativ auf die Gesamtleistung des Servers auswirken kann. Diese Überlegungen müssen bei der Auswahl eines Werts für die Eigenschaft "Maximale Anzahl von Arbeitsprozessen" beachtet werden.  
  
#### <a name="to-increase-maximum-worker-processes-in-iis-7"></a>So erhöhen Sie die maximale Anzahl von Arbeitsprozessen in IIS 7  
  
1.  Erweitern Sie im **Internetinformationsdienste-Manager**den Knoten für den lokalen Server, und klicken Sie dann auf den Knoten **Anwendungspool** .  
  
2.  Wählen Sie den der Websynchronisierungswebsite zugeordneten Anwendungspool aus, und klicken Sie dann im Bereich **Aktionen** auf **Erweiterte Einstellungen** .  
  
3.  Klicken Sie im Dialogfeld **Erweiterte Einstellungen** unter der Überschrift **Prozessmodell**auf die Zeile mit der Bezeichnung Maximale Anzahl von Arbeitsprozessen. Ändern Sie den Eigenschaftswert, und klicken Sie dann auf **OK**.  
  
## <a name="configuring-the-publication"></a>Konfigurieren der Veröffentlichung  
 Erstellen Sie eine Veröffentlichung auf dieselbe Weise wie für eine standardmäßige Mergetopologie, um die Websynchronisierung zu verwenden. Weitere Informationen finden Sie unter [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 Nachdem die Veröffentlichung erstellt wurde, aktivieren Sie die Option zur Verwendung der Websynchronisierung mithilfe der Methoden [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]oder Replikationsverwaltungsobjekte (RMO, Replication Management Objects). Um die Websynchronisierung zu aktivieren, müssen Sie die Webserveradresse für Abonnentenverbindungen angeben.  
  
 Wenn Sie einen Verleger zum ersten Mal verwenden, müssen Sie auch einen Verteiler und eine Momentaufnahmefreigabe konfigurieren. Der Merge-Agent bei jedem Abonnenten muss über Leseberechtigungen für die Momentaufnahmefreigabe verfügen. Weitere Informationen finden Sie unter [Verteilung konfigurieren](../../relational-databases/replication/configure-distribution.md) und [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
 **gen** ist ein reserviertes Wort in Websync-Dateien (XML). Versuchen Sie nicht, Tabellen zu veröffentlichen, in denen Spalten mit dem Namen **gen**enthalten sind.  
  
## <a name="configuring-the-subscription"></a>Konfigurieren des Abonnements  
 Nachdem Sie eine Veröffentlichung aktiviert und IIS konfiguriert haben, erstellen Sie ein Pullabonnement und geben an, dass es mithilfe von IIS synchronisiert werden soll. (Die Websynchronisierung wird nur für Pullabonnements unterstützt.)  
  
## <a name="upgrading-from-an-earlier-version-of-sql-server"></a>Aktualisieren von einer früheren Version von SQL Server  
 Wenn eine vorhandene Websynchronisierungstopologie konfiguriert wurde und Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aktualisieren, müssen Sie sicherstellen, dass die neueste Version von Replisapi.dll in das von der Websynchronisierung verwendete virtuelle Verzeichnis kopiert wird. Standardmäßig befindet sich die neueste Version von Replisapi.dll in C:\Programme\Microsoft SQL Server\\<nnn\>\COM.  
  
## <a name="replicating-large-volumes-of-data"></a>Replizieren großer Datenmengen  
 Um Speicherprobleme auf Abonnentencomputern zu vermeiden, verwendet die Websynchronisierung eine maximale Standardgröße von 100 MB für die XML-Datei zur Übertragung von Änderungen. Die Grenze kann in folgendem Registrierungsschlüssel erweitert werden:  
  
 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\Replication**  
  
 **WebSyncMaxXmlSize DWORD 2000000**  
  
 Der Bereich akzeptabler Werte für diesen Schlüssel ist 100 MB bis 4 GB. Der Wert wird in KB angegeben. Das Setzen diese Parameters auf einen hohen Wert bietet keine Garantie, dass Sie diese Datenmenge synchronisieren können. Die effektive Grenze ist davon abhängig, wie viel zusammenhängender Arbeitsspeicher auf dem Abonnentencomputer verfügbar ist. Falls Sie mehr als 100 MB benötigen, sollten Sie den Wert schrittweise erhöhen und den Speicherbedarf bei einer typischen Arbeitsauslastung auf dem Abonnentencomputer testen.  
  
 Die maximale Größe für die XML-Datei beträgt 4 GB, aber die Replikation synchronisiert die Änderungen aus dieser Datei batchweise. Die Batchgröße von Daten und Metadaten beträgt maximal 25 MB. Achten Sie daher darauf, dass die Daten in jedem Batch höchstens 20 MB ausmachen, damit ausreichend Platz für Metadaten und andere Komponenten vorhanden ist. Diese Grenze bringt die folgenden Auswirkungen mit sich:  
  
-   Es können keine Spalten repliziert werden, die bewirken, dass Daten und Metadaten 25 MB überschreiten. Dies stellt möglicherweise ein Problem dar, wenn Sie Zeilen mit umfangreichen Datentypen wie **varchar(max)**replizieren.  
  
-   Wenn Sie große Datenmengen replizieren, müssen Sie ggf. die Batchgröße des Merge-Agents anpassen.  
  
 Die Batchgröße für die Mergereplikation wird in *Generierungen*gemessen, bei denen es sich um Auflistungen von Änderungen pro Artikel handelt. Die Anzahl von Generierungen in einem Batch wird mithilfe der Parameter –**DownloadGenerationsPerBatch** und –**UploadGenerationsPerBatch** des Merge-Agents angegeben. Weitere Informationen finden Sie unter [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
 Geben Sie für große Datenmengen eine kleine Zahl für die einzelnen Batchverarbeitungsparameter an. Es wird empfohlen, mit dem Wert 10 zu beginnen und dann je nach Anwendungsanforderungen und -leistung diesen Wert zu optimieren. Normalerweise werden diese Parameter in einem Agentprofil angegeben. Weitere Informationen zu Profilen finden Sie unter [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="security-best-practices-for-web-synchronization"></a>Bewährte Methoden bezüglich der Sicherheit bei der Websynchronisierung  
 Es gibt verschiedene Auswahlmöglichkeiten für die sicherheitsbezogenen Einstellungen bei der Websynchronisierung. Der folgende Ansatz ist empfehlenswert:  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verteiler und -Verleger können sich auf demselben Computer befinden (eine typische Konfiguration für die Mergereplikation). IIS sollte jedoch auf einem separaten Computer installiert werden.  
  
-   Verwenden Sie SSL (Secure Sockets Layer), um die Verbindung zwischen dem Abonnenten und dem Computer mit IIS zu verschlüsseln. Dies ist für die Websynchronisierung erforderlich.  
  
-   Verwenden Sie die Standardauthentifizierung für Verbindungen zwischen dem Abonnenten und IIS. Mithilfe der Standardauthentifizierung kann IIS Verbindungen zum Verleger/Verteiler im Namen des Abonnenten herstellen, ohne dass eine Delegierung erforderlich ist. Die Delegierung ist erforderlich, wenn Sie die integrierte Authentifizierung verwenden.  
  
    > [!NOTE]  
    >  Die Standardauthentifizierung ist die Methode, mit der Anmeldeinformationen an IIS weitergegeben werden. Die Standardauthentifizierung verhindert nicht die Angabe von Windows-Domänenkonten für zu IIS hergestellte Verbindungen.  
  
-   Geben Sie an, dass der Momentaufnahme-Agent unter einem Windows-Domänenkonto ausgeführt werden soll und dass der Agent als dieses Konto Verbindungen herstellen soll. (Dies ist die Standardkonfiguration.) Geben Sie an, dass jeder Merge-Agent unter dem Domänenkonto des Benutzers ausgeführt werden soll, der den Abonnentencomputer verwendet. Geben Sie zudem an, dass der Agent Verbindungen als dieses Konto herstellen soll.  
  
     Weitere Informationen zu den erforderlichen Berechtigungen für die Agents finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Geben Sie das Domänenkonto an, das auch vom Merge-Agent verwendet wird, wenn Sie auf der Seite **Webserverinformationen** des Assistenten für neue Abonnements ein Konto und ein Kennwort oder wenn Sie Werte für die Parameter **@internet_url** und **@internet_login** von [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Dieses Konto muss über Leseberechtigungen für die Momentaufnahmefreigabe verfügen.  
  
-   Jede Veröffentlichung sollte ein separates virtuelles Verzeichnis für IIS verwenden.  
  
-   Das Konto, unter dem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung (Replisapi.dll) ausgeführt wird, ist auch das Konto, das während der Synchronisierung eine Verbindung mit dem Verleger und dem Verteiler herstellt. Dieses Konto muss einem SQL-Anmeldekonto auf dem Verleger und dem Verteiler zugeordnet werden. Weitere Informationen finden Sie im Abschnitt „Festlegen von Berechtigungen für die SQL-Replikationsüberwachung“ unter [Konfigurieren von IIS für die Websynchronisierung](../../relational-databases/replication/configure-iis-for-web-synchronization.md).  
  
-   Sie können FTP verwenden, um die Momentaufnahme vom Verleger an den Computer mit IIS zu übermitteln. Die Momentaufnahme wird von dem Computer mit IIS immer mithilfe von HTTPS an den Abonnenten übermittelt. Weitere Informationen finden Sie unter [Übertragen von Momentaufnahmen über FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
-   Wenn sich Server in der Replikationstopologie hinter einer Firewall befinden, müssen Sie möglicherweise Ports in der Firewall öffnen, um die Websynchronisierung zu aktivieren.  
  
    -   Der Abonnentencomputer stellt die Verbindung mit dem Computer, auf dem IIS ausgeführt wird, über HTTPS mithilfe von SSL her, das normalerweise für die Verwendung von Port 443 konfiguriert ist. [!INCLUDE[ssEW](../../includes/ssew-md.md)] -Abonnenten können die Verbindung auch über HTTP herstellen, das normalerweise für die Verwendung von Port 80 konfiguriert ist.  
  
    -   Der Computer, auf dem IIS ausgeführt wird, stellt die Verbindung mit dem Verleger oder Verteiler in der Regel über Port 1433 (Standardinstanz) her. Wenn der Verleger oder der Verteiler eine benannte Instanz auf einem Server mit einer anderen Standardinstanz ist, wird normalerweise die Verbindung mit der benannten Instanz über Port 1500 hergestellt.  
  
    -   Wenn der Computer, auf dem ISS ausgeführt wird, vom Verteiler durch eine Firewall getrennt ist und für die Momentaufnahmeübermittlung eine FTP-Freigabe verwendet wird, müssen die für FTP verwendeten Ports geöffnet sein. Weitere Informationen finden Sie unter [Übertragen von Momentaufnahmen über FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
> [!IMPORTANT]  
>  Das Öffnen von Ports in der Firewall kann dazu führen, dass der Server böswilligen Angriffen ausgesetzt ist. Daher sollten Sie Ports grundsätzlich nur dann öffnen, wenn Sie sicher sind, dass Sie das Konzept von Firewallsystemen verstanden haben. Weitere Informationen finden Sie unter [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Websynchronisierung für die Mergereplikation](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
