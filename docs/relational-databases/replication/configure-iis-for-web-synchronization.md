---
title: "Konfigurieren von IIS für die Websynchronisierung | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/14/2017
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
- IIS server configuration [SQL Server replication]
- websync.log
- Web synchronization, IIS servers
ms.assetid: d651186e-c9ca-4864-a444-2cd6943b8e35
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9046b8e56a18c9393faa6807ac3f0b4d2bfc6f25
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="configure-iis-for-web-synchronization"></a>Konfigurieren von IIS für die Websynchronisierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die Verfahren in diesem Thema sind der zweite Schritt zur Konfiguration der Websynchronisierung für die Mergereplikation. Sie führen diesen Schritt aus, nachdem Sie die Websynchronisierung für eine Veröffentlichung aktiviert haben. Eine Übersicht über den Konfigurationsprozess bietet [Websynchronisierung konfigurieren](../../relational-databases/replication/configure-web-synchronization.md). Nachdem Sie die Verfahren in diesem Thema ausgeführt haben, fahren Sie mit dem dritten Schritt fort, in dem Sie die Websynchronisierung für ein Abonnement konfigurieren. Dieser dritte Schritt wird in den folgenden Themen beschrieben:  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Vorgehensweise: Konfigurieren eines Abonnements für die Websynchronisierung \(SQL Server Management Studio\)](http://msdn.microsoft.com/library/ms345214.aspx)  
  
-   Replikationsprogrammierung [!INCLUDE[tsql](../../includes/tsql-md.md)] : [Vorgehensweise: Konfigurieren eines Abonnements für die Verwendung der Websynchronisierung (Replikationsprogrammierung mit Transact-SQL)](http://msdn.microsoft.com/library/ms345206.aspx)  
  
-   RMO: [Vorgehensweise: Konfigurieren eines Abonnements für die Websynchronisierung (RMO-Programmierung)](http://msdn.microsoft.com/library/ms345207.aspx)  
  
 Die Websynchronisierung verwendet einen Computer mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] IIS (Internet Information Services), um Pullabonnements mit Mergeveröffentlichungen zu synchronisieren. Die IIS-Versionen 5.0 und 6.0 sowie [!INCLUDE[iisver](../../includes/iisver-md.md)] werden unterstützt. Der Assistent zum Konfigurieren der Websynchronisierung wird auf [!INCLUDE[iisver](../../includes/iisver-md.md)]nicht unterstützt.  
  
> [!IMPORTANT]  
>  Stellen Sie sicher, dass in Ihrer Anwendung nur [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] oder höhere Versionen verwendet werden und dass keine früheren Versionen von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] auf dem IIS-Server installiert sind. Frühere Versionen von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] können zu Fehlern führen. Dazu zählen folgende Fehler: "Das Format einer Nachricht war während der Websynchronisierung ungültig. Stellen Sie sicher, dass die Replikationskomponenten auf dem Webserver ordnungsgemäß konfiguriert sind."  
  
> [!CAUTION]  
>  Verwenden Sie WebSync und alternative Ordnerspeicherorte für Momentaufnahmen nicht gleichzeitig.  
  
 Zur Verwendung der Websynchronisierung müssen Sie IIS mithilfe der folgenden Schritte konfigurieren. Jeder Schritt wird in diesem Thema im Detail beschrieben.  
  
1.  Konfigurieren Sie SSL (Secure Sockets Layer). SSL wird für die Kommunikation zwischen IIS und allen Abonnenten benötigt.  
  
2.  Installieren Sie mithilfe des Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konnektivitätskomponenten auf dem Computer mit IIS. Wenn Sie den in Schritt 3 erwähnten Assistenten zum Konfigurieren der Websynchronisierung verwenden möchten, müssen Sie auch [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] auf dem Computer mit IIS installieren.  
  
3.  Konfigurieren Sie den Computer mit IIS für die Websynchronisierung. Sie können den Computer manuell oder mithilfe des Assistenten zum Konfigurieren der Websynchronisierung konfigurieren. Es empfiehlt sich, den Assistenten zu verwenden.  
  
    > [!NOTE]  
    >  Wenn der Computer mit IIS unter einer 64-Bit-Version von Windows ausgeführt wird, müssen Sie den folgenden Befehl ausführen, um sicherzustellen, dass der Server ordnungsgemäß für die Ausführung von ISAPI-Anwendungen (Internet Server API) konfiguriert ist. Weitere Informationen finden Sie in der IIS-Dokumentation.  
  
    ```  
    cscript %SystemDrive%\inetpub\AdminScripts\adsutil.vbs set w3svc/AppPools/Enable32bitAppOnWin64 1  
    ```  
  
4.  Legen Sie die entsprechenden Berechtigungen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung fest.  
  
5.  Führen Sie die Websynchronisierung im Diagnosemodus aus, um die Verbindung mit dem Computer mit IIS zu testen und um sicherzustellen, dass das SSL-Zertifikat ordnungsgemäß installiert ist.  
  
## <a name="configuring-secure-sockets-layer"></a>Konfigurieren von SSL (Secure Sockets Layer)  
 Geben Sie zum Konfigurieren von SSL ein Zertifikat an, das der Computer mit IIS verwenden soll. Die Websynchronisierung für die Mergereplikation unterstützt lediglich Serverzertifikate, nicht aber Clientzertifikate. Zum Konfigurieren von IIS für die Bereitstellung müssen Sie zunächst ein Zertifikat von einer Zertifizierungsstelle erwerben. Zertifizierungsstellen sind Einrichtungen, die für das Erstellen öffentlicher Verschlüsselungsschlüssel für Benutzer, Computer oder andere Zertifizierungsstellen zuständig sind und deren Echtheit sicherstellen. Weitere Informationen zu Zertifikaten finden Sie in der IIS-Dokumentation. Nach dem Installieren des Zertifikats müssen Sie dieses Zertifikat der für die Websynchronisierung verwendeten Website zuordnen.  
  
#### <a name="to-specify-a-certificate-for-deployment"></a>So geben Sie ein Zertifikat für die Bereitstellung an  
  
1.  Melden Sie sich an dem Computer mit IIS als Administrator an.  
  
2.  Starten Sie **Internetinformationsdienste-Manager**:  
  
    1.  Klicken Sie im **Startmenü**auf **Ausführen**.  
  
    2.  Geben Sie **inetmgr** im Feld **Öffnen**ein, und klicken Sie dann auf **OK**.  
  
3.  Führen Sie den IIS-Zertifikat-Assistenten aus:  
  
    1.  Erweitern Sie in **Internetinformationsdienste-Manager**den Knoten **Lokaler Computer** , und erweitern Sie dann den Ordner **Websites** .  
  
    2.  Klicken Sie mit der rechten Maustaste auf **Standardwebsite**, und klicken Sie dann auf **Eigenschaften**.  
  
    3.  Klicken Sie auf der Registerkarte **Verzeichnissicherheit** des Dialogfelds **Eigenschaften von Standardwebsite** auf **Serverzertifikat**.  
  
    4.  Schließen Sie den Assistenten für Webserverzertifikate ab.  
  
4.  Klicken Sie auf **OK**.  
  
 Wenn Sie kein Serverzertifikat von einer Zertifizierungsstelle erhalten können, können Sie ein Zertifikat zum Testen angeben. Installieren Sie ein Zertifikat mithilfe des Hilfsprogramms SelfSSL, um IIS 6.0 zum Testen zu konfigurieren. Dieses Hilfsprogramm ist im IIS 6.0 Resource Kit verfügbar. Sie können die Tools auch vom [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=30958)herunterladen. Für IIS&#160;5.0 wechseln Sie zum [Microsoft Hilfe- und Supportcenter](http://go.microsoft.com/fwlink/?LinkId=46229).  
  
> [!NOTE]  
>  Ein Zertifikat muss einer Website zugeordnet werden, damit die betreffende Website SSL verwenden kann. SelfSSL ordnet das Zertifikat automatisch der Standardwebsite zu. Wenn Sie bereits über ein Zertifikat verfügen oder später ein Zertifikat von einer Zertifizierungsstelle installieren, müssen Sie dieses Zertifikat explizit der Website zuordnen, die von der Websynchronisierung verwendet wird. Stellen Sie sicher, dass der Website, die zum Synchronisieren von Abonnements verwendet wird, nur ein Zertifikat zugeordnet ist. Wenn mehrere Zertifikate vorhanden sind, verwendet der Abonnent die erste verfügbare Website.  
  
#### <a name="to-specify-a-certificate-for-testing-in-iis-60"></a>So geben Sie ein Zertifikat für das Testen in IIS 6.0 an  
  
1.  Melden Sie sich an dem Computer mit IIS als Administrator an.  
  
2.  Laden Sie SelfSSL herunter, und installieren Sie es. Standardmäßig wird die Anwendung im Verzeichnis \<*Laufwerk*>:\Programme\IIS Resources\SelfSSL installiert. Anwendungs- und Dokumentationsverknüpfungen werden in das Verzeichnis \<*Laufwerk*>:\Dokumente und Einstellungen\Alle Benutzer\Startmenü\Programme\IIS Resources\SelfSSL kopiert.  
  
3.  Führen Sie SelfSSL aus:  
  
    -   Wenn Sie SelfSSL mit den Standardwerten für alle Parameter ausführen möchten, suchen Sie das Installationsverzeichnis für die Anwendung, und doppelklicken Sie dort auf SelfSSL.exe.  
  
        > [!NOTE]  
        >  Das von SelfSSL installierte Zertifikat ist standardmäßig sieben Tage gültig.  
  
    -   Klicken Sie zum Angeben von Werten für einen oder mehrere Parameter im Menü **Start**auf **Ausführen**. Geben Sie **cmd** im Feld **Öffnen**ein, und klicken Sie dann auf **OK**. Suchen Sie das SelfSSL-Installationsverzeichnis, geben Sie `SelfSSL`ein, und geben Sie dann Werte für einen oder mehrere Parameter an. Eine Liste der Parameter erhalten Sie durch Eingabe von `SelfSSL -?`.  
  
## <a name="installing-connectivity-components-and-sql-server-management-studio"></a>Installieren der Konnektivitätskomponenten und von SQL Server Management Studio  
  
#### <a name="to-install-sql-server-connectivity-components-and-sql-server-management-studio"></a>So installieren Sie die SQL Server-Konnektivitätskomponenten und SQL Server Management Studio  
  
1.  Melden Sie sich an dem Computer mit IIS als Administrator an.  
  
2.  Starten Sie den Installations-Assistenten für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installationsdatenträger. Weitere Informationen zur Verwendung dieses Assistenten finden Sie unter [Installieren von SQL Server 2016 vom Installations-Assistenten &#40;Setup&#41](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
3.  Wählen Sie auf der Seite **Funktionsauswahl** **Konnektivität der Clienttools**aus.  
  
4.  Wenn Sie den Assistenten zum Konfigurieren der Websynchronisierung verwenden möchten, wählen Sie **Verwaltungstools - Einfach**aus.  
  
5.  Schließen Sie den Assistenten ab, und starten Sie dann den Computer neu.  
  
    > [!NOTE]  
    >  Sie können auch weitere Komponenten installieren, für die Websynchronisierung sind aber lediglich die Konnektivitätskomponenten erforderlich.  
  
## <a name="configuring-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>Konfigurieren des Computers mit IIS mithilfe des Assistenten zum Konfigurieren der Websynchronisierung  
 Konfigurieren Sie den IIS-Server mithilfe des Assistenten zum Konfigurieren der Websynchronisierung oder manuell. Es empfiehlt sich, den Assistenten zu verwenden, Sie finden jedoch auch Schritte für die manuelle Konfiguration im nächsten Abschnitt. Der Assistent zum Konfigurieren der Websynchronisierung, der in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] verfügbar ist, kann nur für Veröffentlichungen verwendet werden, die auf einem Verleger mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]oder einem Verleger, der auf [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]aktualisiert wurde, erstellt wurden. Der Assistent kann nicht für Veröffentlichungen unter [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]verwendet werden. Der Assistent kann mit Abonnements unter [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen sowie unter [!INCLUDE[ssEWnoversion](../../includes/ssewnoversion-md.md)] 3.0 und höheren Versionen verwendet werden.  
  
 Die Konfiguration weist die folgenden Merkmale auf:  
  
-   Sie verwendet die Standardwebsite in IIS. Sie können jedoch auch eine andere Website verwenden. Weitere Informationen zum Erstellen von Websites finden Sie in der IIS-Dokumentation.  
  
    > [!NOTE]  
    >  Die von Ihnen angegebene Website bietet Zugriff auf die von der Websynchronisierung verwendeten Komponenten. Die Website bietet nur dann Zugriff auf andere Daten oder Webseiten, wenn Sie dies entsprechend konfigurieren.  
  
-   Erstellt ein virtuelles Verzeichnis und den zugeordneten Alias. Der Alias wird für den Zugriff auf die Websynchronisierungskomponenten verwendet. Wenn die IIS-Adresse z.B. `https://server.domain.com` heißt und Sie als Alias „websync1“ angeben, lautet die Adresse, über die auf die Komponente replisapi.dll zugegriffen wird, `https://server.domain.com/websync1/replisapi.dll`.  
  
-   Sie verwendet die Standardauthentifizierung. Es empfiehlt sich die Verwendung der Standardauthentifizierung, weil sie es ermöglicht, IIS und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verleger/Verteiler auf separaten Computern (empfohlene Konfiguration) auszuführen, ohne dass eine Kerberos-Delegierung erforderlich ist. Die Verwendung von SSL in Verbindung mit der Standardauthentifizierung stellt sicher, dass Anmeldenamen, Kennwörter und alle Daten bei der Übertragung verschlüsselt werden. (SSL ist in jedem Fall und unabhängig vom verwendeten Authentifizierungstyp erforderlich.) Weitere Informationen zu den bewährten Methoden im Zusammenhang mit der Websynchronisierung finden Sie im entsprechenden Abschnitt im Thema [Websynchronisierung konfigurieren](../../relational-databases/replication/configure-web-synchronization.md).  
  
#### <a name="to-configure-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>So konfigurieren Sie den Computer mit IIS mithilfe des Assistenten zum Konfigurieren der Websynchronisierung  
  
1.  Starten Sie auf dem Computer mit IIS [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Stellen Sie eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
3.  Erweitern Sie den Ordner **Lokale Veröffentlichungen** , klicken Sie mit der rechten Maustaste auf die Veröffentlichung, und klicken Sie dann auf **Websynchronisierung konfigurieren**.  
  
4.  Wählen Sie auf der Seite **Abonnententyp** im Assistenten zum Konfigurieren der Websynchronisierung die Option **SQL Server**aus.  
  
5.  Gehen Sie auf der Seite **Webserver** wie folgt vor:  
  
    1.  Wählen Sie die IIS-Instanz aus, die die Abonnements synchronisieren soll.  
  
    2.  Aktivieren Sie die Option **Neues virtuelles Verzeichnis erstellen**.  
  
    3.  Erweitern Sie auf der Seite unten die IIS-Instanz, erweitern Sie **Websites**, und klicken Sie dann auf **Standardwebsite**.  
  
6.  Gehen Sie auf der Seite **Informationen zum virtuellen Verzeichnis** wie folgt vor:  
  
    1.  Geben Sie im Feld **Alias** einen Alias für das virtuelle Verzeichnis ein.  
  
    2.  Geben Sie im Feld **Pfad** einen Pfad für das virtuelle Verzeichnis ein. Wenn Sie beispielsweise **websync1** in das Feld **Alias** eingegeben haben, geben Sie **C:\Inetpub\wwwroot\websync1** in das Feld **Pfad** ein. Klicken Sie auf **Weiter**.  
  
    3.  Klicken Sie in beiden Dialogfeldern auf **Ja**. Damit geben Sie an, dass Sie einen neuen Ordner erstellen und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -ISAPI-DLL-Datei kopieren möchten. zugreifen.  
  
7.  Gehen Sie auf der Seite **Authentifizierter Zugriff** wie folgt vor:  
  
    1.  Stellen Sie sicher, dass die Optionen **Integrierte Windows-Authentifizierung** und **Digest-Authentifizierung für Windows-Domänenserver** deaktiviert sind.  
  
    2.  Aktivieren Sie die Option **Standardauthentifizierung**.  
  
    3.  Geben Sie in den Feldern **Standarddomäne** und **Bereich** die Domäne des Computers mit IIS ein.  
  
8.  Gehen Sie auf der Seite **Verzeichniszugriff** wie folgt vor:  
  
    1.  Klicken Sie auf **Hinzufügen**, und fügen Sie dann im Dialogfeld **Benutzer oder Gruppen auswählen** die Konten hinzu, über die die Abonnenten die Verbindungen zu IIS herstellen werden. Es handelt sich dabei um die Konten, die Sie auf der Seite **Webserverinformationen** des Assistenten für neue Abonnements oder als Wert für den [-Parameter von](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)*@internet_login* eingeben.  
  
9. Geben Sie auf der Seite **Zugriff auf Momentaufnahmefreigabe** die Momentaufnahmefreigabe ein. Die entsprechenden Berechtigungen für diese Freigabe werden so erteilt, dass die Abonnenten auf die Momentaufnahmedateien zugreifen können. Weitere Informationen zu den Berechtigungen für die Freigabe finden Sie unter [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
10. Klicken Sie auf der Seite **Assistenten abschließen** auf **Fertig stellen**.  
  
     Wenn es beim Konfigurieren eines Remotecomputers mit IIS zu einem Fehler, wie z. B. einem Netzwerkfehler, kommt, findet ein Rollback aller abgeschlossenen Aktionen statt, und die verbleibenden Aktionen werden abgebrochen. Wenn für abgeschlossene Aktionen kein Rollback möglich ist, wird als Status auf der letzten Seite des Assistenten **Erfolg** angezeigt, und die abgeschlossenen Aktionen verbleiben im aktuellen Status.  
  
11. Wenn auf dem Computer mit IIS eine 64-Bit-Version von Windows ausgeführt wird, muss replisapi.dll in das entsprechende Verzeichnis kopiert werden:  
  
    1.  Klicken Sie im **Startmenü**auf **Ausführen**. Geben Sie **iisreset** im Feld **Öffnen**ein, und klicken Sie dann auf **OK**.  
  
    2.  IIS wird beendet und neu gestartet. Kopieren Sie anschließend replisapi.dll aus [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]\COM\replisapi in das in Schritt 6b angegebene Verzeichnis.  
  
    3.  Klicken Sie im **Startmenü**auf **Ausführen**. Geben Sie **cmd** im Feld **Öffnen**ein, und klicken Sie dann auf **OK**.  
  
    4.  Führen Sie in dem Verzeichnis, das Sie in Schritt 6b angegeben haben, den folgenden Befehl aus:  
  
         **regsvr32 replisapi.dll**  
  
## <a name="manually-configuring-the-computer-that-is-running-iis"></a>Manuelles Konfigurieren des Computers, auf dem IIS ausgeführt wird  
 Zum manuellen Konfigurieren des Computers mit IIS müssen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung installieren und konfigurieren, und anschließend müssen Sie die Authentifizierung für Abonnenten konfigurieren, die eine Verbindung zu IIS herstellen.  
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>So installieren und konfigurieren Sie die SQL Server-Replikationsüberwachung  
  
1.  Erstellen Sie ein Dateiverzeichnis auf dem Computer mit IIS, in dem die Datei replisapi.dll enthalten sein soll. Dieses Verzeichnis kann an einem beliebigen Ort erstellt werden, es wird jedoch die Erstellung im Verzeichnis \<*Laufwerk*>:\Inetpub empfohlen. Erstellen Sie beispielsweise das Verzeichnis \<*Laufwerk*>:\Inetpub\SQLReplication\\.  
  
    > [!IMPORTANT]  
    >  Es empfiehlt sich unbedingt, dieses Verzeichnis in einer Partition mit dem NTFS-Dateisystem und nicht dem FAT-Dateisystem zu erstellen. Bei Verwendung des NTFS-Dateisystems können Sie mithilfe der NTFS-Dateisystemberechtigungen genau steuern, welche Benutzer auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation zugreifen dürfen.  
  
2.  Kopieren Sie die Datei replisapi.dll aus dem Verzeichnis [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]\com\ in das Dateiverzeichnis, das Sie in Schritt&#160;1 erstellt haben.  
  
3.  Registrieren Sie replisapi.dll:  
  
    1.  Klicken Sie im **Startmenü**auf **Ausführen**. Geben Sie **cmd** im Feld **Öffnen**ein, und klicken Sie dann auf **OK**.  
  
    2.  Führen Sie in dem Verzeichnis, das Sie in Schritt 1 erstellt haben, den folgenden Befehl aus:  
  
         **regsvr32 replisapi.dll**  
  
4.  Erstellen Sie eine neue Website für die Replikation, oder verwenden Sie eine bereits vorhandene Website. Auf diese Website wird während der Synchronisierung von den Replikationskomponenten zugegriffen. Weitere Informationen zum Erstellen von Websites finden Sie in der IIS-Dokumentation.  
  
5.  Erstellen Sie ein virtuelles Verzeichnis in IIS. Dieses virtuelle Verzeichnis sollte unter der Website angelegt werden, die Sie in Schritt&#160;4 erstellt haben, und es sollte dem in Schritt&#160;1 erstellten Verzeichnis zugeordnet werden. Weitere Informationen zum Erstellen virtueller Verzeichnisse finden Sie in der IIS-Dokumentation. Bei der Zuweisung von Berechtigungen für dieses Verzeichnis sollte möglichst restriktiv vorgegangen werden. Während die Berechtigungen **Lesen** und **Ausführen** erteilt werden müssen, können die Berechtigungen **Skripts ausführen**, **Schreiben**und **Durchsuchen** deaktiviert werden.  
  
6.  Konfigurieren Sie IIS für die Ausführung von replisapi.dll. Die in Schritt 4 zugewiesenen Berechtigungen sind zwar für frühere IIS-Versionen ausreichend, für IIS 6.0 ist aber die Aktivierung der ISAPI-Erweiterungen (Internet Server API) erforderlich. Weitere Informationen finden Sie in der IIS 6.0-Dokumentation in den Abschnitten, die sich mit dem Konfigurieren der ISAPI-Erweiterungen und dem Aktivieren bzw. Deaktivieren von dynamischem Inhalt beschäftigen.  
  
#### <a name="to-configure-iis-authentication"></a>So konfigurieren Sie die IIS-Authentifizierung  
  
-   Wenn Abonnenten eine Verbindung mit IIS herstellen, muss IIS die Abonnenten authentifizieren, damit sie auf Ressourcen und Prozesse zugreifen können. IIS bietet drei Authentifizierungsarten: Anonym, Standard und Integriert. Die Authentifizierung kann sowohl auf die gesamte Website als auch nur auf das von Ihnen erstellte virtuelle Verzeichnis angewendet werden.  
  
     Sie sollten die Standardauthentifizierung mit SSL verwenden. SSL ist in jedem Fall und unabhängig vom verwendeten Authentifizierungstyp erforderlich. Weitere Informationen zum Konfigurieren der Authentifizierung finden Sie in der IIS-Dokumentation.  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>Festlegen von Berechtigungen für die SQL Server-Replikationsüberwachung  
 Wenn ein Abonnent eine Verbindung zum Computer mit IIS herstellt, wird er mithilfe der Authentifizierungsart authentifiziert, die bei der Konfiguration von IIS angegeben wurde. Nach dem Authentifizieren des Abonnenten durch IIS prüft IIS, ob der Abonnent berechtigt ist, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation aufzurufen. Wer die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation aufrufen darf, legen Sie mit den Berechtigungen für replisapi.dll fest. Die ordnungsgemäße Konfiguration der Berechtigungen ist notwendig, damit kein unberechtigter Zugriff auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation erfolgt.  
  
 Führen Sie die folgenden Schritte aus, um die minimalen Berechtigungen für das Konto, unter dem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikationsüberwachung ausgeführt wird, zu konfigurieren. Die Schritte in diesem Verfahren beziehen sich auf [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] mit IIS 6.0.  
  
 Führen Sie die unten genannten Schritte aus, und stellen Sie zusätzlich sicher, dass die Veröffentlichungszugriffsliste die erforderlichen Anmeldenamen enthält. Weitere Informationen zur PAL finden Sie unter [Sichern des Verlegers](../../relational-databases/replication/security/secure-the-publisher.md).  
  
#### <a name="to-configure-the-account-and-permissions"></a>So konfigurieren Sie das Konto und die Berechtigungen  
  
1.  Erstellen Sie ein lokales Konto auf dem Computer mit IIS:  
  
    1.  Klicken Sie mit der rechten Maustaste auf **Arbeitsplatz**, und klicken Sie dann auf **Verwalten**.  
  
    2.  Erweitern Sie unter **Computerverwaltung**den Eintrag **Lokale Benutzer und Gruppen**.  
  
    3.  Klicken Sie mit der rechten Maustaste auf **Benutzer**, und klicken Sie dann auf **Neuer Benutzer**.  
  
    4.  Geben Sie einen Benutzernamen und ein sicheres Kennwort ein.  
  
    5.  Klicken Sie auf **Erstellen**und dann auf **Schließen**.  
  
2.  Fügen Sie das Konto der IIS_WPG-Gruppe hinzu:  
  
    1.  Erweitern Sie unter **Computerverwaltung**den Eintrag **Lokale Benutzer und Gruppen**, und klicken Sie dann auf **Gruppen**.  
  
    2.  Klicken Sie mit der rechten Maustaste auf **IIS_WPG**, und klicken Sie dann auf **Zur Gruppe hinzufügen**.  
  
    3.  Klicken Sie im Dialogfeld **Eigenschaften von IIS_WPG** auf **Hinzufügen**.  
  
    4.  Fügen Sie im Dialogfeld **Benutzer, Computer oder Gruppen auswählen** das in Schritt 1 erstellte Konto hinzu.  
  
    5.  Stellen Sie sicher, dass im Feld **Suchpfad** der Name des lokalen Computers und nicht der Name einer Domäne angezeigt wird. Wenn nicht der Name eines lokalen Computers angezeigt wird, klicken Sie auf **Speicherorte**. Wählen Sie im Dialogfeld **Speicherorte** den lokalen Computer aus, und klicken Sie dann auf **OK**.  
  
    6.  Klicken Sie in den Dialogfeldern **Benutzer, Computer oder Gruppen auswählen** und **Eigenschaften von IIS_WPG** jeweils auf **OK**.  
  
3.  Erteilen Sie dem Konto die mindestens erforderlichen Berechtigungen für den Ordner, der die Datei replisapi.dll enthält:  
  
    1.  Suchen Sie den Ordner, den Sie für die Datei replisapi.dll erstellt haben. Klicken Sie mit der rechten Maustaste auf den Ordner, und klicken Sie dann auf **Freigabe und Sicherheit**.  
  
    2.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Hinzufügen**.  
  
    3.  Fügen Sie im Dialogfeld **Benutzer, Computer oder Gruppen auswählen** das in Schritt 1 erstellte Konto hinzu.  
  
    4.  Stellen Sie sicher, dass im Feld **Suchpfad** der Name des lokalen Computers und nicht der Name einer Domäne angezeigt wird. Wenn nicht der Name eines lokalen Computers angezeigt wird, klicken Sie auf **Speicherorte**. Wählen Sie im Dialogfeld **Speicherorte** den lokalen Computer aus, und klicken Sie dann auf **OK**.  
  
    5.  Stellen Sie sicher, dass dem Konto nur die Berechtigungen **Lesen**, **Lesen & Ausführen** und **Ordnerinhalt auflisten** erteilt werden.  
  
    6.  Wählen Sie alle Benutzer oder Gruppen aus, die keinen Zugriff auf das Verzeichnis benötigen, und klicken Sie dann auf **Entfernen**.  
  
    7.  Klicken Sie auf **OK**.  
  
4.  Erstellen Sie im **Internetinformationsdienste-Manager**einen Anwendungspool:  
  
    1.  Klicken Sie im **Startmenü**auf **Ausführen**.  
  
    2.  Geben Sie **inetmgr** im Feld **Öffnen**ein, und klicken Sie dann auf **OK**.  
  
    3.  Erweitern Sie im **Internetinformationsdienste-Manager**den Knoten **Lokaler Computer** .  
  
    4.  Klicken Sie mit der rechten Maustaste auf **Anwendungspools**, zeigen Sie auf **Neu** , und klicken Sie dann auf **Anwendungspool**.  
  
    5.  Geben Sie im Feld **Anwendungspool-ID** einen Namen für den Pool ein, und klicken Sie dann auf **OK**.  
  
5.  Ordnen Sie das Konto dem Anwendungspool zu:  
  
    1.  Erweitern Sie im **Internetinformationsdienste-Manager**den Knoten **Lokaler Computer** , und erweitern Sie dann **Anwendungspools**.  
  
    2.  Klicken Sie mit der rechten Maustaste auf den von Ihnen erstellten Anwendungspool, und klicken Sie dann auf **Eigenschaften**.  
  
    3.  Klicken Sie auf der Registerkarte **Identität** des Dialogfelds **\<ApplicationPoolName>-Eigenschaften** auf **Konfigurierbar**.  
  
    4.  Geben Sie in den Feldern **Benutzername** und **Kennwort** das Konto und das Kennwort aus Schritt 1 ein.  
  
    5.  Klicken Sie auf **OK**.  
  
6.  Ordnen Sie den Anwendungspool dem virtuellen Verzeichnis zu, das für die Websynchronisierung verwendet wird:  
  
    1.  Erweitern Sie im **Internetinformationsdienste-Manager**den Knoten **Lokaler Computer** , und erweitern Sie dann **Websites**.  
  
    2.  Erweitern Sie die Website, die Sie für die Websynchronisierung verwenden, klicken Sie mit der rechten Maustaste auf das für die Websynchronisierung erstellte virtuelle Verzeichnis, und klicken Sie dann auf **Eigenschaften**.  
  
    3.  Wählen Sie auf der Registerkarte **Virtuelles Verzeichnis** des Dialogfelds **\<VirtualDirectoryName>-Eigenschaften** in der Dropdownliste Anwendungspool den in Schritt 5 erstellten **Anwendungspool** aus.  
  
    4.  Klicken Sie auf **OK**.  
  
## <a name="testing-the-connection-to-replisapidll"></a>Testen der Verbindung mit replisapi.dll  
 Führen Sie die Websynchronisierung im Diagnosemodus aus, um die Verbindung mit dem Computer mit IIS zu testen und um sicherzustellen, dass das SSL-Zertifikat (Secure Sockets Layer) ordnungsgemäß installiert ist. Wenn Sie die Websynchronisierung im Diagnosemodus ausführen möchten, müssen Sie auf dem Computer mit IIS als Administrator angemeldet sein.  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>So testen Sie die Verbindung mit replisapi.dll  
  
1.  Stellen Sie sicher, dass die Netzwerkeinstellungen auf dem Abonnenten ordnungsgemäß eingerichtet wurden:  
  
    1.  Klicken Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer im Menü **Extras** auf **Internetoptionen**.  
  
    2.  Klicken Sie auf der Registerkarte **Verbindungen** auf **Einstellungen**.  
  
    3.  Wenn im lokalen Netzwerk kein Proxyserver verwendet wird, deaktivieren Sie die Optionen **Automatische Suche der Einstellungen** und **Proxyserver für LAN verwenden**.  
  
    4.  Wird ein Proxyserver verwendet, aktivieren Sie die Optionen **Proxyserver für LAN verwenden** und **Proxyserver für lokale Adressen umgehen**.  
  
    5.  Klicken Sie auf **OK**.  
  
2.  Stellen Sie auf dem Abonnenten in Internet Explorer eine Verbindung mit dem Server im Diagnosemodus her, indem Sie an die Adresse für replisapi.dll `?diag` anhängen. Beispiel: `https://server.domain.com/directory/replisapi.dll?diag`.  
  
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
  
5.  Überprüfen Sie im Internet Explorer-Fenster mit **Diagnoseinformationen zur SQL-Websynchronisierung**, ob der Wert in jeder **Status** -Spalte der Seite **Erfolg**lautet.  
  
6.  Stellen Sie sicher, dass das Zertifikat ordnungsgemäß auf dem Abonnenten installiert ist:  
  
    1.  Schließen Sie Internet Explorer, und öffnen Sie das Programm anschließend erneut.  
  
    2.  Stellen Sie eine Verbindung mit dem Server im Diagnosemodus her. Wenn das Zertifikat ordnungsgemäß installiert ist, wird das Dialogfeld **Sicherheitshinweis** nicht angezeigt. Wenn das Dialogfeld angezeigt wird, ist der Merge-Agent nicht in der Lage, eine Verbindung mit dem Computer mit IIS herzustellen. Sie müssen daher sicherstellen, dass das Zertifikat für den Server, auf den Sie zugreifen, dem Zertifikatsspeicher auf dem Abonnenten als vertrauenswürdiges Zertifikat hinzugefügt wurde. Weitere Informationen zum Exportieren von Zertifikaten finden Sie in der IIS-Dokumentation.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Websynchronisierung konfigurieren](../../relational-databases/replication/configure-web-synchronization.md)  
  
  
