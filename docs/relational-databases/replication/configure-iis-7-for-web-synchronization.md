---
title: "Konfigurieren von IIS 7 für die Websynchronisierung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/12/2016
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
- IIS 7 server configuration [SQL Server replication]
- Web synchronization, IIS 7 servers
ms.assetid: c201fe2c-0a76-44e5-a233-05e14cd224a6
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: c0e55c0e35039490f0ce4cd8a7fb6d7e232c05aa
ms.openlocfilehash: ecc4752f5bf52931df9c7af62b5828b92f8f0123
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="configure-iis-7-for-web-synchronization"></a>Konfigurieren von IIS 7 für die Websynchronisierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Die Vorgehensweisen in diesem Thema führen Sie durch den Prozess zum manuellen Konfigurieren von [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Internetinformationsdiensten (IIS) Version 7 oder höher zur Verwendung mit der Websynchronisierung für die Mergereplikation. 
  
 Das Konfigurieren von IIS 7 oder höher ist der erste von drei Schritten, die zum Aktivieren der Websynchronisierung erforderlich sind.  
  
 Eine Übersicht über den gesamten Konfigurationsprozess finden Sie unter [Konfigurieren der Websynchronisierung](../../relational-databases/replication/configure-web-synchronization.md).  
  
> [!IMPORTANT]  
>  Stellen Sie sicher, dass in Ihrer Anwendung nur [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] oder höhere Versionen verwendet werden und dass keine früheren Versionen von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] auf dem IIS-Server installiert sind. Frühere Versionen von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] können Fehler verursachen wie: "Das Format einer Meldung war während der Websynchronisierung ungültig. Stellen Sie sicher, dass die Replikationskomponenten auf dem Webserver ordnungsgemäß konfiguriert sind."  
  
 Zur Verwendung der Websynchronisierung müssen Sie IIS mithilfe der folgenden Schritte konfigurieren. Jeder Schritt wird in diesem Thema im Detail beschrieben.  
  
1.  Installieren und konfigurieren Sie die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung auf dem Computer mit IIS.  
  
2.  Konfigurieren Sie SSL (Secure Sockets Layer). SSL wird für die Kommunikation zwischen IIS und allen Abonnenten benötigt.  
  
3.  Konfigurieren Sie die IIS-Authentifizierung.  
  
4.  Konfigurieren Sie ein Konto, und legen Sie Berechtigungen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung fest.  
  
## <a name="installing-the-sql-server-replication-listener"></a>Installieren der SQL Server-Replikationsüberwachung  

Die Websynchronisierung wird auf IIS ab Version 5.0 unterstützt. Der Assistent zum Konfigurieren der Websynchronisierung der IIS-Versionen 5 und 6 ist für IIS-Version 7.0 und höher nicht verfügbar. **Beginnend mit SQL Server 2012 empfiehlt sich für die Nutzung der Web-Sync-Komponente auf dem IIS-Server die Installation des SQL Servers mit Replikation. Dabei kann es sich um die kostenlose SQL Server Express-Edition handeln.**
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>So installieren und konfigurieren Sie die SQL Server-Replikationsüberwachung  
  
1.  Installieren Sie die SQL Server-Replikation auf dem IIS-Computer.

2. Erstellen Sie ein neues Dateiverzeichnis für die Datei replisapi.dll auf dem Computer mit IIS. Dieses Verzeichnis kann an einem beliebigen Ort erstellt werden, es wird jedoch das Erstellen im Verzeichnis \<*Laufwerk*>:\Inetpub empfohlen. Erstellen Sie beispielsweise das Verzeichnis \<*Laufwerk*>:\Inetpub\SQLReplication\\.  
  
3.  Kopieren Sie die Datei replisapi.dll aus dem Verzeichnis [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]\com\ in das Dateiverzeichnis, das Sie in Schritt&#160;1 erstellt haben.  
  
4.  Registrieren Sie replisapi.dll:  
  
    1.  Klicken Sie im **Startmenü**auf **Ausführen**. Geben Sie **cmd** im Feld **Öffnen**ein, und klicken Sie dann auf **OK**.  
  
    2.  Führen Sie in dem in Schritt 1 erstellten Verzeichnis den folgenden Befehl aus:  
  
         **regsvr32 replisapi.dll**  
  
5.  Erstellen Sie eine neue Website für die Replikation, oder verwenden Sie eine bereits vorhandene Website. Auf diese Website wird während der Synchronisierung von den Replikationskomponenten zugegriffen. Für die Vorgehensweisen in diesem Thema wird von der Standardwebsite ausgegangen. Weitere Informationen zum Erstellen von Websites finden Sie in der IIS-Dokumentation.  
  
6.  Erstellen Sie ein virtuelles Verzeichnis in IIS. Dieses virtuelle Verzeichnis sollte unter der Website angelegt werden, die Sie in Schritt 4 erstellt haben, und es sollte dem in Schritt 1 erstellten Verzeichnis zugeordnet werden. Gehen Sie bei der Zuweisung von Berechtigungen für dieses Verzeichnis möglichst restriktiv vor. Sie müssen mindestens die Berechtigungen **Lesen** und **Ausführen** auswählen.  
  
    1.  Klicken Sie im **Internetinformationsdienste-Manager**im Bereich **Verbindungen** mit der rechten Maustaste auf **Standardwebsite**, und wählen Sie dann **Virtuelles Verzeichnis hinzufügen**aus.  
  
    2.  Für **Alias**geben Sie **SQLReplication**ein.  
  
    3.  Geben Sie **\<Laufwerk>:\Inetpub\SQLReplication\\** für **Physischer Pfad** ein, und klicken Sie dann auf **OK**.  
  
7.  Konfigurieren Sie IIS für die Ausführung von replisapi.dll.  
  
    1.  Klicken Sie im **Internetinformationsdienste-Manager**auf **Standardwebsite**.  
  
    2.  Klicken Sie im mittleren Bereich auf **Handlerzuordnungen**.  
  
    3.  Klicken Sie im Bereich **Aktionen** auf **Modulzuordnung hinzufügen**.  
  
    4.  Geben Sie **replisapi.dll** für **Anforderungspfad**ein.  
  
    5.  Wählen Sie in der Dropdownliste **Modul** die Option **IsapiModule**aus.  
  
    6.  Geben Sie **\<Laufwerk>:\Inetpub\SQLReplication\replisapi.dll** für **Ausführbare Datei** ein.  
  
    7.  Geben Sie **Replisapi**für **Name**ein.  
  
    8.  Klicken Sie auf die Schaltfläche **Einschränkungen** , auf die Registerkarte **Zugriff** und anschließend auf **Ausführen**.  
  
    9. Klicken Sie auf **OK** , um das Dialogfeld **Einschränkungen** zu schließen, und klicken Sie dann erneut auf **OK** , um das Dialogfeld **Modulzuordnung hinzufügen** zu schließen. Wenn Sie aufgefordert werden, die ISAPI-Erweiterung zuzulassen, klicken Sie auf **Ja** , um die Erweiterung hinzuzufügen.  
  
    10. Überprüfen Sie, ob Replisapi.dll unter den Handlerzuordnungen **Aktiviert** aufgeführt wird. Befindet sich die Datei in der Liste **Deaktiviert** , klicken Sie mit der rechten Maustaste auf den Eintrag "Replisapi" und dann auf **Funktionsberechtigungen bearbeiten**. Aktivieren Sie das Kontrollkästchen **Ausführen** , und klicken Sie auf **OK**.  
  
## <a name="configuring-iis-authentication"></a>Konfigurieren der IIS-Authentifizierung  
 Wenn Abonnentencomputer eine Verbindung mit IIS herstellen, muss IIS die Abonnenten authentifizieren, damit sie auf Ressourcen und Prozesse zugreifen können. Die Authentifizierung kann sowohl auf die gesamte Website als auch nur auf das von Ihnen erstellte virtuelle Verzeichnis angewendet werden.  
  
 Sie sollten die Standardauthentifizierung mit SSL verwenden. SSL ist in jedem Fall und unabhängig vom verwendeten Authentifizierungstyp erforderlich.  
  
 Sie sollten die Standardauthentifizierung mit SSL verwenden. SSL ist in jedem Fall und unabhängig vom verwendeten Authentifizierungstyp erforderlich.  
  
#### <a name="to-configure-iis-authentication"></a>So konfigurieren Sie die IIS-Authentifizierung  
  
1.  Klicken Sie im **Internetinformationsdienste-Manager**auf **Standardwebsite**.  
  
2.  Doppelklicken Sie im mittleren Bereich auf **Authentifizierung**.  
  
3.  Klicken Sie mit der rechten Maustaste auf "Anonyme Authentifizierung", und wählen Sie dann "Deaktivieren" aus.  
  
4.  Klicken Sie mit der rechten Maustaste auf "Standardauthentifizierung", und wählen Sie dann "Aktivieren" aus.  
  
## <a name="configuring-secure-sockets-layer"></a>Konfigurieren von SSL (Secure Sockets Layer)  
 Geben Sie zum Konfigurieren von SSL ein Zertifikat an, das der Computer mit IIS verwenden soll. Die Websynchronisierung für die Mergereplikation unterstützt lediglich Serverzertifikate, nicht aber Clientzertifikate. Zum Konfigurieren von IIS für die Bereitstellung müssen Sie zunächst ein Zertifikat von einer Zertifizierungsstelle erwerben. Weitere Informationen zu Zertifikaten finden Sie in der IIS-Dokumentation.  
  
 Nach dem Installieren des Zertifikats müssen Sie dieses Zertifikat der für die Websynchronisierung verwendeten Website zuordnen. Zum Entwickeln und Testen können Sie ein selbstsigniertes Zertifikat angeben. Sie können von IIS 7 ein Zertifikat erstellen und auf dem Computer registrieren lassen.  
  
 Der Unterschied zwischen dem Bereitstellen für die Produktion und den hier angeführten Vorgehensweisen besteht darin, dass Sie bei der Produktion und Vorproduktionstests ein von einer Zertifizierungsstelle ausgestelltes Zertifikat statt eines selbstsignierten Zertifikats verwenden würden.  
  
> [!IMPORTANT]  
>  Ein selbstsigniertes Zertifikat wird für eine Produktionsinstallation nicht empfohlen. Selbstsignierte Zertifikate sind nicht sicher. Verwenden Sie selbstsignierte Zertifikate nur zum Entwickeln und Testen.  
  
 Führen Sie zum Konfigurieren von SSL die folgenden Schritte aus:  
  
1.  Konfigurieren Sie die Website so, dass sie SSL erfordert und Clientzertifikate ignoriert.  
  
2.  Rufen Sie ein Zertifikat von einer Zertifizierungsstelle ab, oder erstellen Sie ein selbstsigniertes Zertifikat.  
  
3.  Binden Sie das Zertifikat an die Replikationswebsite.  
  
#### <a name="to-require-ssl-security-for-a-web-site"></a>So erfordern Sie SSL-Sicherheit für eine Website  
  
1.  Erweitern Sie im **Internetinformationsdienste-Manager**den Knoten für den lokalen Server, und klicken Sie dann auf die **Standardwebsite** (oder die Websynchronisierungswebsite, wenn sie sich von der Standardwebsite unterscheidet).  
  
2.  Doppelklicken Sie im mittleren Bereich auf **SSL-Einstellungen**.  
  
3.  Aktivieren Sie die Option **SSL erforderlich** . Überprüfen Sie unter **Clientzertifikate**, dass die Schaltfläche **Ignorieren** ausgewählt ist.  
  
#### <a name="to-create-a-self-signed-certificate-for-testing"></a>So erstellen Sie ein selbstsigniertes Zertifikat für Tests  
  
1.  Klicken Sie im **Internetinformationsdienste-Manager**auf den Knoten für den lokalen Server, und doppelklicken Sie dann im mittleren Bereich auf **Serverzertifikate**.  
  
2.  Klicken Sie im Bereich **Aktionen** auf **Selbstsigniertes Zertifikat erstellen**.  
  
3.  Geben Sie im Dialogfeld **Selbstsigniertes Zertifikat erstellen** einen Namen für das Zertifikat ein, und klicken Sie dann auf **OK**.  
  
###### <a name="to-bind-a-certificate-to-a-web-site"></a>So binden Sie ein Zertifikat an eine Website  
  
1.  Klicken Sie im Bereich **Verbindungen** auf die **Standardwebsite** (oder die Websynchronisierungswebsite, wenn sie sich von der Standardwebsite unterscheidet).  
  
2.  Klicken Sie im Bereich **Aktionen** auf **Bindungen**und dann auf **Hinzufügen**. Das Dialogfeld **Sitebindung hinzufügen** wird geöffnet.  
  
3.  Wählen Sie in der Dropdownliste **Typ** die Option **https**aus. Behalten Sie die Standardeinstellungen für **IP-Adresse** und **Port**bei.  
  
4.  Wählen Sie in der Dropdownliste **SSL-Zertifikat** das unter "So erstellen Sie ein selbstsigniertes Zertifikat für Tests" erstellte Zertifikat, klicken Sie auf **OK**und dann auf **Schließen**.  
  
###### <a name="to-test-the-certificate"></a>So testen Sie das Zertifikat  
  
1.  Klicken Sie im **Klicken Sie imternet Klicken Sie imformation Services (IIS) Manager**auf **Standardwebsite.**  
  
2.  Klicken Sie im Bereich **Aktionen** auf \*:443(https) **durchsuchen**.  
  
3.  Internet Explorer wird geöffnet und zeigt folgende Meldung an: "Es besteht ein Problem mit dem Sicherheitszertifikat der Website". Diese Warnung besagt, dass das zugeordnete Zertifikat nicht von einer bekannten Zertifizierungsstelle ausgestellt wurde und möglicherweise nicht vertrauenswürdig ist. Dies ist eine erwartete Warnung, klicken Sie deshalb auf **Laden dieser Website fortsetzen (nicht empfohlen)**.  
  
4.  Wenn die Aufforderung **Mit Localhost verbinden**angezeigt wird, geben Sie einen Benutzernamen und ein Kennwort ein, um fortzufahren. Die Standardseite für die Website sollte angezeigt werden.  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>Festlegen von Berechtigungen für die SQL Server-Replikationsüberwachung  
 Wenn ein Abonnentencomputer eine Verbindung zum Computer mit IIS herstellt, wird der Abonnent mithilfe der Authentifizierungsart authentifiziert, die bei der Konfiguration von IIS angegeben wurde. Nach dem Authentifizieren des Abonnenten durch IIS prüft IIS, ob der Abonnent berechtigt ist, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation aufzurufen. Wer die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation aufrufen darf, legen Sie mit den Berechtigungen für replisapi.dll fest. Die ordnungsgemäße Konfiguration der Berechtigungen ist notwendig, damit kein unberechtigter Zugriff auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation erfolgt.  
  
 Führen Sie die folgenden Schritte aus, um die minimalen Berechtigungen für das Konto, unter dem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung ausgeführt wird, zu konfigurieren. Die Schritte in der folgenden Vorgehensweise gelten für [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server 2008 mit IIS 7.0.  
  
 Führen Sie die unten genannten Schritte aus, und stellen Sie zusätzlich sicher, dass die Veröffentlichungszugriffsliste die erforderlichen Anmeldenamen enthält. Weitere Informationen zur PAL finden Sie unter [Sichern des Verlegers](../../relational-databases/replication/security/secure-the-publisher.md).  
  
 **Wichtig** Das in diesem Abschnitt erstellte Konto ist das Konto, das während der Synchronisierung eine Verbindung mit dem Verleger und dem Verteiler herstellt. Dieses Konto muss als SQL-Anmeldekonto auf dem Verteilungs- und Veröffentlichungsserver hinzugefügt werden.  
  
 Das für die SQL Server-Replikationsüberwachung verwendete Konto muss über die im Thema "Sicherheit für den Merge-Agent" im Abschnitt "Herstellen einer Verbindung mit dem Verleger oder dem Verteiler" beschriebenen Berechtigungen verfügen.  
  
 Zusammengefasst muss das Konto folgende Bedingungen erfüllen:  
  
-   Es muss Mitglied der Veröffentlichungszugriffsliste (PAL) sein.  
  
-   Es muss einer mit einem Benutzer in der Veröffentlichungsdatenbank verknüpften Anmeldung zugeordnet sein.  
  
-   Es muss einer mit einem Benutzer in der Verteilungsdatenbank verknüpften Anmeldung zugeordnet sein.  
  
-   Es muss über Leseberechtigungen für die Momentaufnahmefreigabe verfügen.  
  
#### <a name="to-configure-the-account-and-permissions"></a>So konfigurieren Sie das Konto und die Berechtigungen  
  
1.  Erstellen Sie ein lokales Konto auf dem Computer mit IIS:  
  
    1.  Öffnen Sie **Server-Manager**. Klicken Sie im Startmenü mit der rechten Maustaste auf **Arbeitsplatz**, und klicken Sie dann auf **Verwalten**.  
  
    2.  Erweitern Sie in **Server-Manager**den Knoten **Konfiguration**, und erweitern Sie dann **Lokale Benutzer und Gruppen**.  
  
    3.  Klicken Sie mit der rechten Maustaste auf **Benutzer**, und klicken Sie dann auf **Neuer Benutzer**.  
  
    4.  Geben Sie einen Benutzernamen und ein sicheres Kennwort ein. Deaktivieren Sie die Option **Benutzer muss Kennwort bei der nächsten Anmeldung ändern**.  
  
    5.  Klicken Sie auf **Erstellen**und dann auf **Schließen**.  
  
2.  Fügen Sie das Konto der IIS_IUSRS-Gruppe hinzu:  
  
    1.  Erweitern Sie in **Server-Manager**den Knoten **Konfiguration**, erweitern Sie **Lokale Benutzer und Gruppen**, und klicken Sie dann auf **Gruppen**.  
  
    2.  Klicken Sie mit der rechten Maustaste auf **IIS_IUSRS**, und klicken Sie dann auf **Zur Gruppe hinzufügen**.  
  
    3.  Klicken Sie im Dialogfeld **Eigenschaften von IIS_IUSRS** auf **Hinzufügen**.  
  
    4.  Fügen Sie im Dialogfeld **Benutzer, Computer oder Gruppen auswählen** das in Schritt 1 erstellte Konto hinzu.  
  
    5.  Stellen Sie sicher, dass unter **Suchpfad** der Name des lokalen Computers und nicht eine Domäne angezeigt wird. Wenn der Name des lokalen Computers in diesem Feld nicht anzeigt wird, klicken Sie auf **Speicherorte**. Wählen Sie im Dialogfeld **Speicherorte** den lokalen Computer aus, und klicken Sie dann auf **OK**.  
  
    6.  Klicken Sie im Dialogfeldern **Benutzer auswählen** und **Eigenschaften von IIS_IUSRS** jeweils auf**OK**.  
  
3.  Gewähren Sie die mindestens erforderlichen Kontoberechtigungen für den Ordner, der die Datei replisapi.dll enthält:  
  
    1.  Klicken Sie in Windows Explorer mit der rechten Maustaste auf den Ordner, den Sie für die Datei replisapi.dll erstellt haben, und klicken Sie dann auf **Eigenschaften**.  
  
    2.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Bearbeiten**.  
  
    3.  Klicken Sie im Dialogfeld **Berechtigungen für \<Ordnername>** auf **Hinzufügen**, um das in Schritt 1 erstellte Konto hinzuzufügen.  
  
    4.  Stellen Sie sicher, dass unter **Suchpfad** der Name des lokalen Computers und nicht eine Domäne angezeigt wird. Wenn der Name des lokalen Computers in diesem Feld nicht anzeigt wird, klicken Sie auf **Speicherorte**. Wählen Sie im Dialogfeld **Speicherorte** den lokalen Computer aus, und klicken Sie dann auf **OK**.  
  
    5.  Stellen Sie sicher, dass dem Konto nur die Berechtigungen **Lesen**, **Lesen & Ausführen** und **Ordnerinhalt auflisten** erteilt werden.  
  
    6.  Wählen Sie alle Benutzer oder Gruppen aus, die keinen Zugriff auf das Verzeichnis benötigen, klicken Sie auf **Entfernen**, und klicken Sie dann auf **OK**.  
  
4.  Erstellen Sie im **Internetinformationsdienste-Manager**einen Anwendungspool:  
  
    1.  Erweitern Sie im **Internetinformationsdienste-Manager**im Bereich **Verbindungen** den Knoten für den lokalen Server.  
  
    2.  Klicken Sie mit der rechten Maustaste auf **Anwendungspools**, und klicken Sie dann auf **Anwendungspool hinzufügen**.  
  
    3.  Geben Sie einen Namen für den Anwendungspool ein, behalten Sie die Standardwerte für die verbleibenden Felder bei, und klicken Sie dann auf **OK**.  
  
    > [!NOTE]  
    >  Wenn Sie mehr als zwei gleichzeitige Synchronisierungsclients erwarten, sollten Sie einen Webgarten erstellen. Weitere Informationen finden Sie unter „Erstellen eines Webgartens“ in [Konfigurieren der Websynchronisierung](../../relational-databases/replication/configure-web-synchronization.md).  
  
5.  Ordnen Sie das Konto dem Anwendungspool zu:  
  
    1.  Erweitern Sie im **Internetinformationsdienste-Manager**den Knoten für den lokalen Server, und klicken Sie dann auf **Anwendungspools**.  
  
    2.  Klicken Sie mit der rechten Maustaste auf den von Ihnen erstellten Anwendungspool, und klicken Sie dann auf **Anwendungspoolstandardwerte festlegen**.  
  
    3.  Führen Sie im Dialogfeld **Anwendungspoolstandardwerte** einen Bildlauf nach unten zum Abschnitt **Prozessmodell** durch, und klicken Sie dann auf das Feld **Identität** .  
  
    4.  Klicken Sie auf der rechten Seite der Zeile **Identität** auf die Schaltfläche mit den Auslassungspunkten.  
  
    5.  Klicken Sie auf das Optionsfeld **Benutzerdefiniertes Konto** und dann auf **Festlegen**.  
  
    6.  Geben Sie in den Feldern **Benutzername** und **Kennwort** das Konto und das Kennwort aus Schritt 1 ein, und klicken Sie anschließend auf **OK**.  
  
    7.  Klicken Sie auf **OK** , um das Dialogfeld **Identität des Anwendungspools** zu schließen, und klicken Sie dann erneut auf **OK** , um das Dialogfeld **Anwendungspoolstandardwerte**zu schließen.  
  
6.  Ordnen Sie den Anwendungspool der Replikationswebsite zu:  
  
    1.  Erweitern Sie im **Internetinformationsdienste-Manager**den Knoten für den lokalen Server, und klicken Sie dann auf die **Standardwebsite** (oder die Websynchronisierungswebsite, wenn sie sich von der Standardwebsite unterscheidet).  
  
    2.  Klicken Sie im Bereich **Aktionen** unter **Website verwalten**auf **Erweiterte Einstellungen**.  
  
    3.  Klicken Sie im Dialogfeld **Erweiterte Einstellungen** rechts von **Anwendungspool**auf die Schaltfläche mit den Auslassungspunkten.  
  
    4.  Wählen Sie in der Dropdownliste **Anwendungspool** den Anwendungspool aus Schritt 4 aus, und klicken Sie dann auf **OK**.  
  
    5.  Klicken Sie erneut auf **OK** , um die erweiterten Einstellungen zu schließen.  
  
## <a name="testing-the-connection-to-replisapidll"></a>Testen der Verbindung mit replisapi.dll  
 Führen Sie die Websynchronisierung im Diagnosemodus aus, um die Verbindung mit dem Computer mit IIS zu testen und um sicherzustellen, dass das SSL-Zertifikat (Secure Sockets Layer) ordnungsgemäß installiert ist. Wenn Sie die Websynchronisierung im Diagnosemodus ausführen möchten, müssen Sie auf dem Computer mit IIS als Administrator angemeldet sein.  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>So testen Sie die Verbindung mit replisapi.dll  
  
1.  Stellen Sie sicher, dass die Netzwerkeinstellungen auf dem Abonnenten ordnungsgemäß eingerichtet wurden:  
  
    1.  Klicken Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer im Menü **Extras** auf **Internetoptionen**.  
  
    2.  Klicken Sie auf der Registerkarte **Verbindungen** auf **Einstellungen**.  
  
    3.  Wenn im lokalen Netzwerk kein Proxyserver verwendet wird, deaktivieren Sie die Optionen **Automatische Suche der Einstellungen** und **Proxyserver für LAN verwenden**.  
  
    4.  Wird ein Proxyserver verwendet, klicken Sie auf **Proxyserver für LAN verwenden** und **Proxyserver für lokale Adressen umgehen**und dann auf **OK**.  
  
2.  Stellen Sie auf dem Abonnenten in Internet Explorer eine Verbindung mit dem Server im Diagnosemodus her, indem Sie an die Adresse für replisapi.dll `?diag` anhängen. Beispiel: `https://server.domain.com/directory/replisapi.dll?diag`.  
  
    > [!NOTE]  
    >  Im oben aufgeführten Beispiel sollte **server.domain.com** durch den im Abschnitt **Serverzertifikate** in IIS-Manager aufgeführten genauen **Ausgestellt an** -Namen ersetzt werden.  
  
3.  Wenn das für IIS angegebene Zertifikat nicht vom Windows-Betriebssystem erkannt wird, wird das Dialogfeld **Sicherheitshinweis** angezeigt. Dieser Hinweis wird möglicherweise angezeigt, weil das Zertifikat ein Testzertifikat ist oder es von einer Zertifizierungsstelle ausgestellt wurde, die von Windows nicht erkannt wird.  
  
    > [!NOTE]  
    >  Wenn dieses Dialogfeld nicht angezeigt wird, stellen Sie sicher, dass das Zertifikat für den Server, auf den Sie zugreifen, dem Zertifikatsspeicher auf dem Abonnenten als vertrauenswürdiges Zertifikat hinzugefügt wurde. Weitere Informationen zum Exportieren von Zertifikaten finden Sie in der IIS-Dokumentation.  
  
    1.  Klicken Sie im Dialogfeld **Sicherheitshinweis** auf **Zertifikat anzeigen**.  
  
    2.  Klicken Sie auf der Registerkarte **Allgemein** des Dialogfelds **Zertifikat** auf **Zertifikat installieren**.  
  
    3.  Schließen Sie den Zertifikatimport-Assistenten ab, und übernehmen Sie dabei die Standardwerte.  
  
    4.  Klicken Sie im Dialogfeld **Sicherheitswarnung** auf **Ja**.  
  
    5.  Klicken Sie im Bestätigungsdialogfeld des Zertifikatimport-Assistenten auf **OK**.  
  
    6.  Schließen Sie das Dialogfeld **Zertifikat** .  
  
    7.  Klicken Sie im Dialogfeld **Sicherheitshinweis** auf **Ja**.  
  
    > [!NOTE]  
    >  Die Zertifikate werden für die Benutzer installiert. Dieser Prozess muss für jeden Benutzer ausgeführt werden, der mit IIS synchronisiert werden soll.  
  
4.  Geben Sie im Dialogfeld **Verbindung mit \<ServerName> herstellen** den Anmeldenamen und das Kennwort an, den bzw. das der Merge-Agent zum Herstellen der Verbindung mit dem IIS verwenden soll. Diese Anmeldeinformationen werden auch im Assistenten für neue Abonnements angegeben.  
  
5.  Überprüfen Sie im Internet Explorer-Fenster mit **** Diagnoseinformationen zur SQL-Websynchronisierung, ob der Wert in jeder **Status** -Spalte der Seite **Erfolg**lautet.  
  
6.  Stellen Sie sicher, dass das Zertifikat ordnungsgemäß auf dem Abonnenten installiert ist:  
  
    1.  Schließen Sie Internet Explorer, und öffnen Sie das Programm anschließend erneut.  
  
    2.  Stellen Sie eine Verbindung mit dem Server im Diagnosemodus her. Wenn das Zertifikat ordnungsgemäß installiert ist, wird das Dialogfeld **Sicherheitshinweis** nicht angezeigt. Wenn das Dialogfeld angezeigt wird, ist der Merge-Agent nicht in der Lage, eine Verbindung mit dem Computer mit IIS herzustellen. Sie müssen daher sicherstellen, dass das Zertifikat für den Server, auf den Sie zugreifen, dem Zertifikatsspeicher auf dem Abonnenten als vertrauenswürdiges Zertifikat hinzugefügt wurde. Weitere Informationen zum Exportieren von Zertifikaten finden Sie in der IIS-Dokumentation.  
  
## <a name="see-also"></a>Siehe auch  
 [Websynchronisierung für die Mergereplikation](../../relational-databases/replication/web-synchronization-for-merge-replication.md)   
 [Konfigurieren der Websynchronisierung](../../relational-databases/replication/configure-web-synchronization.md)  
  
  

