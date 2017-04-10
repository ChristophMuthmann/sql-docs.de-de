---
title: "Konfigurieren von IIS 7 f&#252;r die Websynchronisierung | Microsoft Docs"
ms.custom: ""
ms.date: "09/12/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "IIS 7-Serverkonfiguration [SQL Server-Replikation]"
  - "Websynchronisierung, IIS 7-Server"
ms.assetid: c201fe2c-0a76-44e5-a233-05e14cd224a6
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# Konfigurieren von IIS 7 f&#252;r die Websynchronisierung
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die Verfahren in diesem Thema führt Sie durch den Prozess für die manuelle Konfiguration [!INCLUDE[msCoName](../../includes/msconame-md.md)] IIS (Internetinformationsdienste) Version 7 und höher für verwenden mit websynchronisierung für die Mergereplikation. 
  
 Konfigurieren von IIS 7 oder höher ist die erste von drei Schritte erforderlich, um die websynchronisierung zu aktivieren.  
  
 Einen Überblick über den gesamten Konfigurationsprozess finden Sie unter [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
> [!IMPORTANT]  
>  Stellen Sie sicher, dass in Ihrer Anwendung nur [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] oder höhere Versionen verwendet werden und dass keine früheren Versionen von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] auf dem IIS-Server installiert sind. Frühere Versionen von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] können Fehler verursachen wie: "Das Format einer Meldung war während der Websynchronisierung ungültig. Stellen Sie sicher, dass die Replikationskomponenten auf dem Webserver ordnungsgemäß konfiguriert sind."  
  
 Zur Verwendung der Websynchronisierung müssen Sie IIS mithilfe der folgenden Schritte konfigurieren. Jeder Schritt wird in diesem Thema im Detail beschrieben.  
  
1.  Installieren und konfigurieren Sie die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung auf dem Computer mit IIS.  
  
2.  Konfigurieren Sie SSL (Secure Sockets Layer). SSL wird für die Kommunikation zwischen IIS und allen Abonnenten benötigt.  
  
3.  Konfigurieren Sie die IIS-Authentifizierung.  
  
4.  Konfigurieren Sie ein Konto, und legen Sie Berechtigungen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung fest.  
  
## Installieren der SQL Server-Replikationsüberwachung  

Synchronisierung von wird in IIS ab Version 5.0, unterstützt. Die konfigurieren Web Synchronization-Assistenten in IIS Version 5 und 6, ist nicht mit IIS, Version 7.0 und höher verfügbar. **Beginnend mit SQL Server 2012, verwenden Sie die Web-Sync-Komponente auf IIS-Server sollten Sie SQL Server mit der Replikation installieren. Dies kann der kostenlosen SQL Server Express Edition sein.**
  
#### So installieren und konfigurieren Sie die SQL Server-Replikationsüberwachung  
  
1.  Installieren Sie SQL Server-Replikation auf dem IIS-Computer.

2. Erstellen Sie ein neues Dateiverzeichnis für die Datei replisapi.dll auf dem Computer mit IIS. Wo sollen, aber es wird empfohlen, dass Sie das Verzeichnis erstellen, erstellen Sie das Verzeichnis kann die \<*Laufwerk*>: \Inetpub-Verzeichnis. Erstellen Sie beispielsweise das Verzeichnis \<*Laufwerk*>: \Inetpub\SQLReplication\\.  
  
3.  Kopieren Sie anschließend replisapi.dll aus dem Verzeichnis [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]\com\ in das Verzeichnis, das Sie in Schritt 1 erstellt haben.  
  
4.  Registrieren Sie replisapi.dll:  
  
    1.  Klicken Sie im **Startmenü**auf **Ausführen**. Geben Sie **cmd** im Feld **Öffnen**ein, und klicken Sie dann auf **OK**.  
  
    2.  Führen Sie in dem in Schritt 1 erstellten Verzeichnis den folgenden Befehl aus:  
  
         **regsvr32 replisapi.dll**  
  
5.  Erstellen Sie eine neue Website für die Replikation, oder verwenden Sie eine bereits vorhandene Website. Auf diese Website wird während der Synchronisierung von den Replikationskomponenten zugegriffen. Für die Vorgehensweisen in diesem Thema wird von der Standardwebsite ausgegangen. Weitere Informationen zum Erstellen von Websites finden Sie in der IIS-Dokumentation.  
  
6.  Erstellen Sie ein virtuelles Verzeichnis in IIS. Dieses virtuelle Verzeichnis sollte unter der Website angelegt werden, die Sie in Schritt 4 erstellt haben, und es sollte dem in Schritt 1 erstellten Verzeichnis zugeordnet werden. Gehen Sie bei der Zuweisung von Berechtigungen für dieses Verzeichnis möglichst restriktiv vor. Sie müssen mindestens die Berechtigungen **Lesen** und **Ausführen** auswählen.  
  
    1.  Im **Internet Information Services (IIS) Manager**, in die **Verbindungen** Bereich mit der rechten Maustaste **Default Web Site**, und wählen Sie dann **virtuelles Verzeichnis hinzufügen**.  
  
    2.  Für **Alias**geben Sie **SQLReplication**ein.  
  
    3.  Für **physischen Pfad**, geben Sie **\< Laufwerk>: \Inetpub\SQLReplication\\**, und klicken Sie dann auf **OK**.  
  
7.  Konfigurieren Sie IIS für die Ausführung von replisapi.dll.  
  
    1.  Im **Internet Information Services (IIS) Manager**, klicken Sie auf **Default Web Site**.  
  
    2.  Klicken Sie im mittleren Bereich auf **Handlerzuordnungen**.  
  
    3.  Klicken Sie im Bereich **Aktionen** auf **Modulzuordnung hinzufügen**.  
  
    4.  Geben Sie **replisapi.dll** für **Anforderungspfad**ein.  
  
    5.  Aus der **Modul** Dropdown-Liste **IsapiModule**.  
  
    6.  Für **ausführbare Datei**, geben Sie **\< Laufwerk>: \Inetpub\SQLReplication\replisapi.dll**.  
  
    7.  Geben Sie **Replisapi**für **Name**ein.  
  
    8.  Klicken Sie auf die Schaltfläche **Einschränkungen** , auf die Registerkarte **Zugriff** und anschließend auf **Ausführen**.  
  
    9. Klicken Sie auf **OK** , um das Dialogfeld **Einschränkungen** zu schließen, und klicken Sie dann erneut auf **OK** , um das Dialogfeld **Modulzuordnung hinzufügen** zu schließen. Wenn Sie aufgefordert werden, die ISAPI-Erweiterung zuzulassen, klicken Sie auf **Ja** , um die Erweiterung hinzuzufügen.  
  
    10. Überprüfen Sie, ob Replisapi.dll unter den Handlerzuordnungen **Aktiviert** aufgeführt wird. Ist in der **deaktiviert** Liste rechten Maustaste auf den Eintrag Replisapi aus, und klicken Sie dann auf **Featureberechtigungen bearbeiten**. Aktivieren Sie das Kontrollkästchen **Ausführen** , und klicken Sie auf **OK**.  
  
## Konfigurieren der IIS-Authentifizierung  
 Wenn Abonnentencomputer eine Verbindung mit IIS herstellen, muss IIS die Abonnenten authentifizieren, damit sie auf Ressourcen und Prozesse zugreifen können. Die Authentifizierung kann sowohl auf die gesamte Website als auch nur auf das von Ihnen erstellte virtuelle Verzeichnis angewendet werden.  
  
 Sie sollten die Standardauthentifizierung mit SSL verwenden. SSL ist in jedem Fall und unabhängig vom verwendeten Authentifizierungstyp erforderlich.  
  
 Sie sollten die Standardauthentifizierung mit SSL verwenden. SSL ist in jedem Fall und unabhängig vom verwendeten Authentifizierungstyp erforderlich.  
  
#### So konfigurieren Sie die IIS-Authentifizierung  
  
1.  Im **Internet Information Services (IIS) Manager**, klicken Sie auf **Default Web Site**.  
  
2.  Doppelklicken Sie im mittleren Bereich auf **Authentifizierung**.  
  
3.  Klicken Sie mit der rechten Maustaste auf "Anonyme Authentifizierung", und wählen Sie dann "Deaktivieren" aus.  
  
4.  Klicken Sie mit der rechten Maustaste auf "Standardauthentifizierung", und wählen Sie dann "Aktivieren" aus.  
  
## Konfigurieren von SSL (Secure Sockets Layer)  
 Geben Sie zum Konfigurieren von SSL ein Zertifikat an, das der Computer mit IIS verwenden soll. Die Websynchronisierung für die Mergereplikation unterstützt lediglich Serverzertifikate, nicht aber Clientzertifikate. Zum Konfigurieren von IIS für die Bereitstellung müssen Sie zunächst ein Zertifikat von einer Zertifizierungsstelle erwerben. Weitere Informationen zu Zertifikaten finden Sie in der IIS-Dokumentation.  
  
 Nach dem Installieren des Zertifikats müssen Sie dieses Zertifikat der für die Websynchronisierung verwendeten Website zuordnen. Zum Entwickeln und Testen können Sie ein selbstsigniertes Zertifikat angeben. Sie können von IIS 7 ein Zertifikat erstellen und auf dem Computer registrieren lassen.  
  
 Der Unterschied zwischen dem Bereitstellen für die Produktion und den hier angeführten Vorgehensweisen besteht darin, dass Sie bei der Produktion und Vorproduktionstests ein von einer Zertifizierungsstelle ausgestelltes Zertifikat statt eines selbstsignierten Zertifikats verwenden würden.  
  
> [!IMPORTANT]  
>  Ein selbstsigniertes Zertifikat wird für eine Produktionsinstallation nicht empfohlen. Selbstsignierte Zertifikate sind nicht sicher. Verwenden Sie selbstsignierte Zertifikate nur zum Entwickeln und Testen.  
  
 Führen Sie zum Konfigurieren von SSL die folgenden Schritte aus:  
  
1.  Konfigurieren Sie die Website so, dass sie SSL erfordert und Clientzertifikate ignoriert.  
  
2.  Rufen Sie ein Zertifikat von einer Zertifizierungsstelle ab, oder erstellen Sie ein selbstsigniertes Zertifikat.  
  
3.  Binden Sie das Zertifikat an die Replikationswebsite.  
  
#### So erfordern Sie SSL-Sicherheit für eine Website  
  
1.  Im **Internet Information Services (IIS) Manager**, erweitern Sie den lokalen Server-Knoten, und klicken Sie dann auf die **Standardwebsite** (oder die websynchronisierungswebsite, wenn sie sich von der Standardwebsite unterscheidet).  
  
2.  Doppelklicken Sie im mittleren Bereich auf **SSL-Einstellungen**.  
  
3.  Aktivieren Sie die Option **SSL erforderlich** . Überprüfen Sie unter **Clientzertifikate**, dass die Schaltfläche **Ignorieren** ausgewählt ist.  
  
#### So erstellen Sie ein selbstsigniertes Zertifikat für Tests  
  
1.  Im **Internet Information Services (IIS) Manager**, klicken Sie auf dem lokalen Server-Knoten, und doppelklicken Sie dann im mittleren Bereich auf **Serverzertifikate**.  
  
2.  In der **Aktionen** Bereich, klicken Sie auf **selbstsigniertes Zertifikat erstellen**.  
  
3.  In der **ein selbstsigniertes Zertifikat erstellen** im Dialogfeld Geben Sie einen Namen für das Zertifikat, und klicken Sie dann auf **OK**.  
  
###### So binden Sie ein Zertifikat an eine Website  
  
1.  In der **Verbindungen** Bereich, klicken Sie auf der **Default Web Site** (oder die websynchronisierungswebsite, wenn sie sich von der Standardwebsite unterscheidet).  
  
2.  Klicken Sie im Bereich **Aktionen** auf **Bindungen**und dann auf **Hinzufügen**. Das Dialogfeld **Sitebindung hinzufügen** wird geöffnet.  
  
3.  Aus der **Typ** Dropdown-Liste **Https**. Behalten Sie die Standardeinstellungen für **IP-Adresse** und **Port**bei.  
  
4.  Aus der **SSL-Zertifikat** Dropdown-Liste Wählen Sie das Zertifikat erstellt, unter "So erstellen ein selbstsigniertes Zertifikat zum Testen" klicken Sie auf **OK**, und klicken Sie dann auf **Schließen**.  
  
###### So testen Sie das Zertifikat  
  
1.  Im **Internet Information Services (IIS) Manager**, klicken Sie auf **Default Web Site.**  
  
2.  Aus der **Aktionen** Bereich, klicken Sie auf **Durchsuchen \*: 443(https)**.  
  
3.  Internet Explorer wird geöffnet und zeigt folgende Meldung an: "Es besteht ein Problem mit dem Sicherheitszertifikat der Website". Diese Warnung besagt, dass das zugeordnete Zertifikat nicht von einer bekannten Zertifizierungsstelle ausgestellt wurde und möglicherweise nicht vertrauenswürdig ist. Dies ist eine erwartete Warnung, klicken Sie auf **Weiter, um diese Website (nicht empfohlen)**.  
  
4.  Wenn die Aufforderung **Mit Localhost verbinden**angezeigt wird, geben Sie einen Benutzernamen und ein Kennwort ein, um fortzufahren. Die Standardseite für die Website sollte angezeigt werden.  
  
## Festlegen von Berechtigungen für die SQL Server-Replikationsüberwachung  
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
  
#### So konfigurieren Sie das Konto und die Berechtigungen  
  
1.  Erstellen Sie ein lokales Konto auf dem Computer mit IIS:  
  
    1.  Öffnen Sie **Server-Manager**. Klicken Sie im Startmenü mit der rechten Maustaste **Computer**, und klicken Sie dann auf **verwalten**.  
  
    2.  Erweitern Sie in **Server-Manager**den Knoten **Konfiguration**, und erweitern Sie dann **Lokale Benutzer und Gruppen**.  
  
    3.  Mit der rechten Maustaste **Benutzer**, und klicken Sie dann auf **Neuer Benutzer**.  
  
    4.  Geben Sie einen Benutzernamen und ein sicheres Kennwort ein. Deaktivieren Sie die Option **Benutzer muss Kennwort bei der nächsten Anmeldung ändern**.  
  
    5.  Klicken Sie auf **Erstellen**und dann auf **Schließen**.  
  
2.  Fügen Sie das Konto der IIS_IUSRS-Gruppe hinzu:  
  
    1.  Erweitern Sie in **Server-Manager**den Knoten **Konfiguration**, erweitern Sie **Lokale Benutzer und Gruppen**, und klicken Sie dann auf **Gruppen**.  
  
    2.  Mit der rechten Maustaste **IIS_IUSRS**, und klicken Sie dann auf **Gruppe hinzufügen**.  
  
    3.  In der **Eigenschaften von IIS_IUSRS** Dialogfeld klicken Sie auf **Hinzufügen**.  
  
    4.  Fügen Sie im Dialogfeld **Benutzer, Computer oder Gruppen auswählen** das in Schritt 1 erstellte Konto hinzu.  
  
    5.  Überprüfen Sie, ob **von diesem Speicherort** zeigt den Namen des lokalen Computers (und keiner Domäne). Wenn der Name des lokalen Computers in diesem Feld nicht anzeigt wird, klicken Sie auf **Speicherorte**. Wählen Sie im Dialogfeld **Speicherorte** den lokalen Computer aus, und klicken Sie dann auf **OK**.  
  
    6.  In der **Benutzer** Dialogfeld und der **Eigenschaften von IIS_IUSRS** im Dialogfeld klicken Sie auf**OK**.  
  
3.  Gewähren Sie die mindestens erforderlichen Kontoberechtigungen für den Ordner, der die Datei replisapi.dll enthält:  
  
    1.  In Windows-Explorer mit der rechten Maustaste in des Ordners, den Sie für die Datei replisapi.dll erstellt haben, und klicken Sie dann auf **Eigenschaften**.  
  
    2.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Bearbeiten**.  
  
    3.  In der **Berechtigungen für \< Ordnername>** im Dialogfeld klicken Sie auf **Hinzufügen** um das Konto hinzuzufügen, die Sie in Schritt 1 erstellt haben.  
  
    4.  Überprüfen Sie, ob **von diesem Speicherort** zeigt den Namen des lokalen Computers (und keiner Domäne). Wenn der Name des lokalen Computers in diesem Feld nicht anzeigt wird, klicken Sie auf **Speicherorte**. Wählen Sie im Dialogfeld **Speicherorte** den lokalen Computer aus, und klicken Sie dann auf **OK**.  
  
    5.  Stellen Sie sicher, dass das Konto nur die Berechtigungen **Lesen**, **Lesen & ausführen**, und **Ordnerinhalt auflisten** Berechtigungen.  
  
    6.  Wählen Sie alle Benutzer oder Gruppen aus, die keinen Zugriff auf das Verzeichnis benötigen, klicken Sie auf **Entfernen**, und klicken Sie dann auf **OK**.  
  
4.  Erstellen eines Anwendungspools in **Internet Information Services (IIS) Manager**:  
  
    1.  Im **Internet Information Services (IIS) Manager**, in die **Verbindungen** Bereich, erweitern Sie den lokalen Server-Knoten.  
  
    2.  Mit der rechten Maustaste **Anwendungspools**, und klicken Sie dann auf **Anwendungspool hinzufügen**.  
  
    3.  Geben Sie einen Namen für den Anwendungspool ein, behalten Sie die Standardwerte für die verbleibenden Felder bei, und klicken Sie dann auf **OK**.  
  
    > [!NOTE]  
    >  Wenn Sie mehr als zwei gleichzeitige Synchronisierungsclients erwarten, sollten Sie einen Webgarten erstellen. Weitere Informationen finden Sie unter "Erstellen eines Webgartens" in [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
5.  Ordnen Sie das Konto dem Anwendungspool zu:  
  
    1.  Im **Internet Information Services (IIS) Manager**, erweitern Sie den lokalen Server-Knoten, und klicken Sie dann auf **Anwendungspools**.  
  
    2.  Mit der rechten Maustaste des Anwendungspools, den Sie erstellt haben, und klicken Sie dann auf **Anwendungspoolstandardwerte festlegen**.  
  
    3.  Führen Sie im Dialogfeld **Anwendungspoolstandardwerte** einen Bildlauf nach unten zum Abschnitt **Prozessmodell** durch, und klicken Sie dann auf das Feld **Identität** .  
  
    4.  Klicken Sie auf der rechten Seite der Zeile **Identität** auf die Schaltfläche mit den Auslassungspunkten.  
  
    5.  Klicken Sie auf das Optionsfeld **Benutzerdefiniertes Konto** und dann auf **Festlegen**.  
  
    6.  Geben Sie in den Feldern **Benutzername** und **Kennwort** das Konto und das Kennwort aus Schritt 1 ein, und klicken Sie anschließend auf **OK**.  
  
    7.  Klicken Sie auf **OK** , um das Dialogfeld **Identität des Anwendungspools** zu schließen, und klicken Sie dann erneut auf **OK** , um das Dialogfeld **Anwendungspoolstandardwerte**zu schließen.  
  
6.  Ordnen Sie den Anwendungspool der Replikationswebsite zu:  
  
    1.  Im **Internet Information Services (IIS) Manager**, erweitern Sie den lokalen Server-Knoten, und klicken Sie dann auf die **Standardwebsite** (oder die websynchronisierungswebsite, wenn sie sich von der Standardwebsite unterscheidet).  
  
    2.  Klicken Sie im Bereich **Aktionen** unter **Website verwalten**auf **Erweiterte Einstellungen**.  
  
    3.  Klicken Sie im Dialogfeld **Erweiterte Einstellungen** rechts von **Anwendungspool**auf die Schaltfläche mit den Auslassungspunkten.  
  
    4.  Aus der **Anwendungspool** Dropdown-Liste, wählen Sie den Anwendungspool, die Sie in Schritt 4 erstellt haben, und klicken Sie dann auf **OK**.  
  
    5.  Klicken Sie erneut auf **OK** , um die erweiterten Einstellungen zu schließen.  
  
## Testen der Verbindung mit replisapi.dll  
 Ausführen der websynchronisierung im Diagnosemodus, um die Verbindung mit dem Computer mit IIS zu testen und um sicherzustellen, dass das Secure Sockets Layer (SSL)-Zertifikat ordnungsgemäß installiert ist. Wenn Sie die Websynchronisierung im Diagnosemodus ausführen möchten, müssen Sie auf dem Computer mit IIS als Administrator angemeldet sein.  
  
#### So testen Sie die Verbindung mit replisapi.dll  
  
1.  Stellen Sie sicher, dass die Netzwerkeinstellungen auf dem Abonnenten ordnungsgemäß eingerichtet wurden:  
  
    1.  Klicken Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer im Menü **Extras** auf **Internetoptionen**.  
  
    2.  Klicken Sie auf der Registerkarte **Verbindungen** auf **Einstellungen**.  
  
    3.  Wenn im lokalen Netzwerk kein Proxyserver verwendet wird, deaktivieren Sie die Optionen **Automatische Suche der Einstellungen** und **Proxyserver für LAN verwenden**.  
  
    4.  Wird ein Proxyserver verwendet, klicken Sie auf **Proxyserver für LAN verwenden** und **Proxyserver für lokale Adressen umgehen**und dann auf **OK**.  
  
2.  Stellen Sie auf dem Abonnenten in Internet Explorer eine Verbindung mit dem Server im Diagnosemodus her, indem Sie an die Adresse für replisapi.dll `?diag` anhängen. Zum Beispiel: **https://server.domain.com/directory/replisapi.dll?diag**.  
  
    > [!NOTE]  
    >  Im obigen Beispiel **server.domain.com** sollte ersetzt werden durch die genaue **ausgestellt für** Name wird unter der **Serverzertifikate** Abschnitt im IIS-Manager.  
  
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
  
4.  In der **Herstellen einer Verbindung mit \< ServerName>** Dialogfeld Feld, geben Sie Benutzername und Kennwort, die der Merge-Agent zum Verbinden mit IIS. Diese Anmeldeinformationen werden auch im Assistenten für neue Abonnements angegeben.  
  
5.  Überprüfen Sie im Internet Explorer-Fenster mit ** **Diagnoseinformationen zur SQL-Websynchronisierung, ob der Wert in jeder **Status** -Spalte der Seite **Erfolg**lautet.  
  
6.  Stellen Sie sicher, dass das Zertifikat ordnungsgemäß auf dem Abonnenten installiert ist:  
  
    1.  Schließen Sie Internet Explorer, und öffnen Sie das Programm anschließend erneut.  
  
    2.  Stellen Sie eine Verbindung mit dem Server im Diagnosemodus her. Wenn das Zertifikat ordnungsgemäß installiert ist, wird das Dialogfeld **Sicherheitshinweis** nicht angezeigt. Wenn das Dialogfeld angezeigt wird, ist der Merge-Agent nicht in der Lage, eine Verbindung mit dem Computer mit IIS herzustellen. Sie müssen daher sicherstellen, dass das Zertifikat für den Server, auf den Sie zugreifen, dem Zertifikatsspeicher auf dem Abonnenten als vertrauenswürdiges Zertifikat hinzugefügt wurde. Weitere Informationen zum Exportieren von Zertifikaten finden Sie in der IIS-Dokumentation.  
  
## Siehe auch  
 [Websynchronisierung für die Mergereplikation](../../relational-databases/replication/web-synchronization-for-merge-replication.md)   
 [Websynchronisierung konfigurieren](../../relational-databases/replication/configure-web-synchronization.md)  
  
  