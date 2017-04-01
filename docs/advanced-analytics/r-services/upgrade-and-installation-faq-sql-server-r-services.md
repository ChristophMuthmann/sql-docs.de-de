---
title: "H&#228;ufig gestellte Fragen zu Upgrade und Installation (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 58
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 47
---
# H&#228;ufig gestellte Fragen zu Upgrade und Installation (SQL Server R Services)
  Dieses Thema bietet Antworten auf häufig gestellte Fragen, welche die Installation sowie Aktualisierungen von Preview-Versionen von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] betreffen.  
  
 Beachten Sie, wenn Sie [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] zum ersten Mal installieren, die Vorgehensweisen zum Einrichten von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und der R-Komponenten, die hier beschrieben werden: [Einrichten von SQL Server R Services &#40;In-Database&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  

   
## <a name="important-changes-from-pre-releae-versions"></a>Wichtige Änderungen gegenüber Vorabversionen  
 Wenn Sie eine Vorabversion von SQL Server 2016 installiert haben oder Setupanweisungen verwenden, die vor der Veröffentlichung von SQL Server 2016 herausgegeben wurden, müssen Sie beachten, dass sich der Installationsvorgang von Vorabversion und RTM-Versionen vollständig unterscheidet. Diese Änderungen betreffen sowohl die verfügbaren Optionen im SQL Server-Setup-Assistenten als auch die Schritte nach der Installation. 
   
> [!WARNING] Neue Installationen einer Vorabversion von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] werden nicht mehr unterstützt. Es wird empfohlen, möglichst bald eine Aktualisierung durchzuführen.  
+ Wenn Sie [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] als CTP3, CTP3.1, CTP3.2, RC0 oder RC1 installiert haben, müssen Sie das Skript für die Konfiguration nach der Installation nochmals ausführen, um die vorherigen Versionen der R-Komponenten und von R Services zu deinstallieren. 
+ Das Skript für die Konfiguration nach der Installation dient ausschließlich dazu, Kunden bei der Deinstallation von Vorabversionen zu unterstützen.  Führen Sie das Skript nicht aus, wenn Sie neuere Version installieren.

## <a name="how-to-uninstall-previous-versions-of-r-services"></a>Deinstallieren früherer Versionen von R Services

Es ist wichtig, dass Sie frühere Versionen von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] und die zugehörigen R-Komponenten in der richtigen Reihenfolge deinstallieren.

### <a name="1-run-script-to-deregister-windows-user-group-and-components-before-uninstalling-previous-components"></a>1. Führen Sie das Skript aus, um die Registrierung von Windows-Benutzergruppen und -Komponenten aufzuheben, bevor Sie frühere Komponenten deinstallieren.
Wenn Sie eine Vorabversion von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert haben, müssen Sie zunächst das Skript `RegisteREext.exe` mit dem `/uninstall`-Argument ausführen.

Auf diese Weise heben Sie die Registrierung alter Komponenten auf und entfernen die Windows-Benutzergruppen, die dem Launchpad zugeordnet sind. Wenn Sie dies nicht tun, können Sie nicht die erforderliche Windows-Benutzergruppe für neue von Ihnen installierte Instanzen erstellen.
  
Wenn Sie beispielsweise R Services auf der Standardinstanz installiert haben, führen Sie den folgenden Befehl aus dem Verzeichnis aus, in dem das Skript installiert ist:  
  
~~~~
    RegisterRExt.exe /UNINSTALL  
~~~~ 
  
Wenn Sie R Services auf einer benannten Instanz installiert haben, müssen Sie den Instanznamen nach *INSTANCE* angeben:  
  
~~~~ 
RegisterRExt.exe /UNINSTALL /INSTANCE:<instancename>   
~~~~  

Sie müssen das Skript unter Umständen mehrmals ausführen, um alle Komponenten zu entfernen.

> [!NOTE]
> Der Standardspeicherort für dieses Skript ist unterschiedlich und hängt von der Vorabversion ab, die Sie installiert haben. Wenn Sie versuchen, die falsche Version des Skripts auszuführen, erhalten Sie möglicherweise eine Fehlermeldung. 
> 
>  + Wenn Sie über CTP 3.1, 3.2 oder 3.3 verfügen, müssen Sie eine aktualisierte Version des Skripts für die Konfiguration nach der Installation aus dem [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=723194) herunterladen, bevor Sie Komponenten deinstallieren können. Das aktualisierte Skript unterstützt das Aufheben der Registrierung älterer Komponenten. Klicken Sie auf den Link, und wählen Sie **Speichern unter** aus, um das Skript in einem lokalen Ordner zu speichern. Benennen Sie das vorhandene Skript um, und kopieren Sie das neue Skript dann in den Ordner, in dem das Skript ausgeführt werden soll. 
>  + Für RC0 wurde die richtige Skriptdatei installiert, sie befindet sich in diesem Ordner: `C:\Program Files\Microsoft\MRO-for-RRE\8.0\R-3.2.2\library\RevoScaleR\rxLibs\x64`.  
>  + Für die Releaseversionen (13.0.1601.5 oder höher) ist kein Skript erforderlich, um Komponenten zu installieren oder zu konfigurieren. Das Skript sollte ausschließlich für das Entfernen älterer Komponenten verwendet werden. 


### <a name="2-uninstall-any-older-versions-of-the-revolution-enterprise-tools-including-components-installed-with-ctp-releases"></a>2. Deinstallieren Sie ältere Versionen der Revolution Enterprise-Tools, einschließlich Komponenten, die mit CTP-Versionen installiert wurden.

Die Reihenfolge der Deinstallation der R-Komponenten ist wichtig. Deinstallieren Sie immer zuerst [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. Deinstallieren Sie anschließend [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)].  

 Wenn Sie versehentlich zuerst R Open deinstallieren und dann beim Versuch Revolution R Enterprise zu deinstallieren eine Fehlermeldung erhalten, ist eine Umgehungslösung, Revolution R Open oder Microsoft R Open erneut zu installieren und dann beide Komponenten in der richtigen Reihenfolge zu deinstallieren.  

### <a name="3-uninstall-any-other-version-of-microsoft-r-open"></a>3. Deinstallieren Sie eine etwaige andere Version von Microsoft R Open.

Deinstallieren Sie zum Schluss alle übrigen Versionen von Microsoft R Open.
 
### <a name="4-upgrade-sql-server"></a>4. Aktualisieren von SQL Server  
  
Starten Sie den Computer neu, nachdem alle Komponenten von Vorabversionen deinstalliert wurden. Dies ist eine Voraussetzung für das SQL Server-Setup, und Sie können eine aktualisierte Installation erst dann fortsetzen, wenn der Neustart abgeschlossen ist.     

Führen Sie anschließend das SQL Server-Setup aus, und befolgen Sie die nachstehenden Anweisungen für die Installation von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]: [Einrichten von SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
Es sind keine zusätzlichen Komponenten erforderlich, da die R- und Konnektivitätspakete vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup installiert werden. 


## <a name="upgrading-r-components"></a>Upgraden von R-Komponenten

Hotfixes oder Verbesserungen für SQL Server 2016 werden freigegeben, und R-Komponenten werden ebenfalls aktualisiert, wenn Ihre Instanz bereits die R Services-Funktion enthält. 

Allerdings müssen Sie beim Aktualisieren oder Patchen von Servern, die nicht mit dem Internet verbunden sind, eine aktualisierte Version der R-Komponenten manuell herunterladen, bevor Sie mit der Aktualisierung beginnen. Weitere Informationen finden Sie unter [Installation von R-Komponenten ohne Internetzugang](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).

## <a name="problems-uninstalling-older-versions-of-r"></a>Probleme beim Deinstallieren älterer Versionen von R  
In einigen Fällen werden ältere Versionen von Revolution R Open oder Revolution R Enterprise beim Deinstallationsprozess nicht vollständig entfernt.  
  
 Wenn Sie Probleme beim Entfernen einer älteren Version haben, können Sie auch die Registrierung bearbeiten, um betroffene Schlüssel zu entfernen.  
  
 Öffnen Sie die Windows-Registrierung, und suchen Sie folgenden Schlüssel: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.  
  
 Löschen Sie einen der folgenden Einträge, wenn er vorhanden ist und der Schlüssel nur den Wert `sEstimatedSize2` enthält:  
  
-   E0B2C29E-B8FC-490B-A043-2CAE75634972        (für 8.0.2)  
  
-   46695879-954E-4072-9D32-1CC84D4158F4        (für 8.0.1)  
  
-   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (für 8.0.0)  
  
-   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (für 7.5.0)  


## <a name="new-license-agreement-for-r-components-required-for-unattended-installs"></a>Neue Lizenzvereinbarung für R-Komponenten für unbeaufsichtigte Installation erforderlich  
 Wenn Sie die Befehlszeile für das Upgrade einer Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwenden, auf der bereits [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert ist, müssen Sie die Befehlszeile ändern, damit sie den neuen Lizenzvereinbarungsparameter */IACCEPTROPENLICENSEAGREEMENT* verwendet. 
 
 Wenn das ordnungsgemäße Argument nicht angegeben wird, kann das Setup von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] misslingen.  
  
## <a name="after-running-setup-includersqlproductnametokenrsqlproductnamemdmd-is-still-not-enabled"></a>Nach dem Ausführen von Setup ist [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] noch nicht aktiviert  
 Die Funktion, die die Ausführung externer Skripts unterstützt, ist standardmäßig deaktiviert, selbst wenn sie installiert ist. Dies ist beabsichtigt, um die Oberfläche zu reduzieren.  
  
 Um R-Skripts zu aktivieren, kann ein Administrator die folgende Anweisung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ausführen:  
  
1.  Führen Sie auf der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Instanz, auf der R verwendet werden soll, die folgende Anweisung aus.  
  
    ```  
    sp_configure 'external scripts enabled',1 
    reconfigure with override  
    ```  
  
2.  Starten Sie die Instanz neu.  
  
3.  Öffnen Sie nach dem Neustart der Instanz den **SQL Server-Konfigurations-Manager** oder den Bereich **Services**, und überprüfen Sie, ob der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]-Dienst ausgeführt wird.  

> [!TIP] Um eine vorkonfigurierte Instanz von R Services zu installieren, verwenden Sie das Abbild der unter Azure ausgeführten virtuellen Maschine, welches die Enterprises Edition mit aktivierten R Services enthält. Weitere Informationen finden Sie unter [Installieren von SQL Server R Services auf einem virtuellen Azure-Computer](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md).
 

## <a name="setup-of-includersqlproductnametokenrsqlproductnamemdmd-not-available-in-a-failover-cluster"></a>Setup von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] nicht in Failovercluster verfügbar  
 Derzeit ist es nicht möglich, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] auf einem Failovercluster zu installieren.  
    
 Sie können [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] jedoch auf einem eigenständigen Computer installieren, der „Always On“ verwendet und zu einer Verfügbarkeitsgruppe gehört. Weitere Informationen zur Verwendung von R Services in einer Always On-Verfügbarkeitsgruppe finden Sie unter [Always On-Verfügbarkeitsgruppen: Interoperabilität](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md).  

Eine weitere Möglichkeit besteht darin, für die Ausführung von R-Skripts ein Replikat auf einer anderen SQL Server-Instanz einzurichten. Das Replikat könnte mittels einer Replikation oder mittels Protokollversand erstellt werden.
 
## <a name="launchpad-service-cannot-be-started"></a>Launchpad-Dienst kann nicht gestartet werden  

Es gibt verschiedene Probleme, die verhindern können, dass Launchpad gestartet wird.
+ **8.3-Notation nicht aktiviert**.  Um R Services (In-Database) installieren zu können, muss das Laufwerk, auf dem die Funktion installiert wird, die Erstellung von kurzen Dateinamen mithilfe der **8.3**-Notation unterstützen.  Ein 8.3-Dateiname wird auch als kurzer Dateiname bezeichnet und ermöglicht die Kompatibilität mit älteren Versionen von Microsoft Windows oder die Verwendung als alternativer Dateiname zu langen Dateinamen. 

  Wenn das Volume, auf dem [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert wird, keine kurzen Dateinamen unterstützt, können die Prozesse, die R aus SQL Server starten, möglicherweise nicht die richtige ausführbare Datei finden, und [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] wird nicht gestartet.  
  
   Um dieses Problem zu umgehen, aktivieren Sie die 8.3-Notation auf dem Volume, auf dem SQL Server und R Services installiert sind. Sie müssen dann den kurzen Namen für das Arbeitsverzeichnis in der R Services-Konfigurationsdatei angeben. 

    1. Führen Sie zum Aktivieren der 8.3-Notation das **fsutil**-Hilfsprogramm mit dem *8dot3name*-Argument wie hier beschrieben aus: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).
    2. Nachdem dem Aktivieren der 8.3-Notation öffnen Sie die Datei RLauncher.config. Bei einer Standardinstallation befindet sich die Datei RLauncher.config unter C:\Programme\Microsoft SQL Server\MSSQL13. MSSQLSERVER\MSSQL\Binn.
    3. Notieren Sie sich die Eigenschaft für WORKING_DIRECTORY.
    4. Verwenden Sie das Hilfsprogramm fsutil mit dem Argument *file*, um einen kurzen Dateipfad für den unter WORKING_DIRECTORY angegebenen Ordner anzugeben.
    5. Bearbeiten Sie die Konfigurationsdatei, um den Kurznamen für WORKING_DIRECTORY zu verwenden.   
     
Alternativ können Sie ein anderes Verzeichnis für WORKING_DIRECTORY angeben, dessen Pfad mit der 8.3-Notation kompatibel ist.     
   
   > [!NOTE] Diese Einschränkung wird in einer späteren Version entfallen. 
 
+ **Das Konto, unter dem Launchpad ausgeführt wird, wurde geändert oder erforderliche Berechtigungen wurden entfernt.** In der Standardeinstellung verwendet [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] das folgende Konto beim Start, das vom [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Setup so konfiguriert wird, dass es über alle erforderliche Berechtigungen verfügt: NT Service\MSSQLLaunchpad.

  Wenn Sie dem Launchpad ein anderes Konto zuweisen oder das Recht durch eine Richtlinie auf dem SQL Server-Computer entfernt wird, verfügt das Konto daher möglicherweise nicht über die erforderlichen Berechtigungen, und es kann folgende Fehlermeldung angezeigt werden: *ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 	Anmeldung fehlgeschlagen: Der Benutzer besitzt nicht den benötigten Anmeldetyp auf diesem Computer.*

  Um die erforderlichen Berechtigungen für das neue Service-Konto hinzuzufügen, verwenden Sie die Anwendung **Local Security Policy**, und aktualisieren Sie die Berechtigungen für das Konto dahingehend, dass es die folgenden Berechtigungen umfasst:
  + Anpassen des Arbeitsspeicherkontingents für einen Prozess (SeIncreaseQuotaPrivilege)
  + Umgehen von durchsuchenden Prüfungen (SeChangeNotifyPrivilege)
  + Anmelden als Dienst (SeServiceLogonRight)
  + Ersetzen von Token auf Prozessebene (SeAssignPrimaryTokenPrivilege)

  Weitere Informationen über die Berechtigungen für das Ausführen von SQL Server-Diensten finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](https://msdn.microsoft.com/library/ms143504.aspx#Windows).
  
## <a name="side-by-side-installation-not-supported"></a>Parallele Installation wird nicht unterstützt  
 Erstellen Sie keine parallele Installation mit einer anderen Version von R oder anderen Versionen von Revolution Analytics.  

## <a name="offline-installation-of-r-components-for-localized-version-of-sql-server"></a>Offline-Installation von R-Komponenten für lokalisierte Version von SQL Server 
Wenn Sie R Services auf einem Computer installieren, der nicht über einen Internetzugang verfügt, müssen Sie zwei weitere Schritte ausführen: Sie müssen das Installationsprogramm für R-Komponenten in einen lokalen Ordner herunterladen, bevor Sie SQL Server-Setup ausführen. Und Sie müssen die Installationsprogrammdatei bearbeiten, um sicherzustellen, dass die richtige Sprache installiert wird. 

Die Sprachen-ID, die für die R-Komponenten verwendet wird, muss sich mit der installierten SQL Server-Setupsprache decken. Andernfalls ist die Schaltfläche **Weiter** deaktiviert, und Sie können das Setup nicht abschließen.

Weitere Informationen finden Sie unter [Installation von R-Komponenten ohne Internetzugang](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md). 
  
## <a name="unable-to-launch-runtime-for-r-script"></a>Laufzeit für R-Skript kann nicht gestartet werden
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] erstellt eine Windows-Benutzergruppe, die von [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] verwendet wird, um R-Aufträge auszuführen. Diese Benutzergruppe muss sich bei der Instanz anmelden können, die R Services ausführt, um R im Auftrag von Remotebenutzern auszuführen, die die integrierte Windows-Authentifizierung verwenden.
  
 In einer Umgebung, in der die Windows-Gruppe für Benutzer von R (**SQLRUsers**) nicht über diese Berechtigung verfügt, werden möglicherweise die folgenden Fehlermeldungen angezeigt:  
  
-   Wenn Sie versuchen, R-Skripts auszuführen:  
  
     *Laufzeit für 'R'-Skript kann nicht gestartet werden. Überprüfen Sie die Konfiguration der 'R'-Laufzeit.*  
  
     *Ein externer Skriptfehler ist aufgetreten. Laufzeit kann nicht gestartet werden.*  
  
-   Vom [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] -Dienst generierte Fehlermeldungen:  
  
     *Fehler beim Initialisieren des Startprogramms RLauncher.dll*  
  
     *Keine Startprogramm-DLLs registriert!*  
  
-   Sicherheitsprotokolle weisen darauf hin, dass das Konto NT SERVICE\MSSQLLAUNCHPAD sich nicht anmelden konnte.  
  
Informationen, wie Sie dieser Benutzergruppe die notwendigen Berechtigungen erteilen können, finden Sie unter [Einrichten von SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md). 

> [!NOTE]
> 
> Diese Einschränkung gilt nicht, wenn Sie SQL-Benutzernamen verwenden, um von einer Remotearbeitsstation R-Skripts auszuführen. 

  
## <a name="remote-execution-via-odbc"></a>Remoteausführung über ODBC   
 Wenn Sie eine Data Science-Arbeitsstation verwenden und eine Verbindung zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computer herstellen, um R-Befehle mit den **RevoScaleR**-Funktionen auszuführen, wird möglicherweise eine Fehlermeldung angezeigt, wenn ODBC-Aufrufe verwendet werden, die Daten auf den Server schreiben. 
 
 Der Grund ist derselbe wie im vorherigen Abschnitt: Beim Setup erstellt R Services eine Gruppe von Workerkonten, die zum Ausführen von R-Aufgaben verwendet werden. Können diese Konten keine Verbindung zum Server herstellen, können auch keine ODBC-Aufrufe in Ihrem Auftrag ausgeführt werden. 
 
 Beachten Sie, dass diese Einschränkung nicht gilt, wenn Sie SQL-Benutzernamen verwenden, um R-Skripts von einer Remotearbeitsstation auszuführen, da die SQL-Anmeldeinformationen explizit vom R-Client an die SQL Server-Instanz und dann an ODBC übergeben werden.
  
Um eine implizite Authentifizierung zu aktivieren, müssen Sie der folgenden Gruppe von Workerkonten Berechtigungen erteilen:  
    
1. Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] als Administrator auf der Instanz, auf der Sie R-Code ausführen werden. 

2. Führen Sie das folgende Skript aus: Achten Sie darauf, den Namen der Benutzergruppe zu bearbeiten, wenn Sie die Standardeinstellung geändert haben. Bearbeiten Sie außerdem den Namen des Computers und der Instanz.
    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ```

Weitere Informationen sowie eine Beschreibung der Schritte für diesen Vorgang mithilfe der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]-UI finden Sie unter [Einrichten von SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).

    
## <a name="errors-during-setup-because-r-components-cannot-be-installed"></a>Fehler beim Setup, da R-Komponenten nicht installiert werden können  
 Wenn Sie R Services (In-Database) mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup installieren und auf der Seite mit den Microsoft R Open-Lizenzbedingungen auf **Annehmen** klicken, sollte Setup die Komponenten suchen und mit der Installation beginnen, wenn andere Komponenten installiert sind. Allerdings schlägt in folgenden Fällen das Installieren der Komponenten möglicherweise fehl:  
  
-   Sie führen eine Offline-Installation durch, und die Komponenten können nicht heruntergeladen werden.  
  
     [Installieren von R-Komponenten ohne Internetzugang](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)  
  
-   Sie verwenden die Option zum Prüfen auf Aktualisierungen, und der Aktualisierungsdienst gibt eine Fehlermeldung aus, da er die korrekte Version der Komponente nicht finden kann.  
  
  Dies ist ein bekanntes Problem, das in RC3 behoben wurde.  
  
 
  
## <a name="upgrade-of-r-server-standalone-to-rc3-requires-uninstallation-using-the-rc2-setup-utility"></a>Upgrade von R Server (eigenständig) auf RC3 erfordert Deinstallation mit dem RC2-Setup-Hilfsprogramm
 Microsoft R Server (eigenständig) wurde erstmals in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 verfügbar. Um ein Upgrade auf die RC3-Version von Microsoft R Server durchzuführen, müssen Sie zunächst eine Deinstallation mittels [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2-Setup durchführen und anschließend eine Neuinstallation mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC3-Setup durchführen.  
  
1.  Deinstallieren Sie R-Server (eigenständig) für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup.  
  
2.  Führen Sie ein Upgrade auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC3 durch, und wählen Sie die Option zum Installieren von R Services (In-Database) aus. Hierdurch wird die Instanz von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] auf RC3 aktualisiert; es ist keine zusätzliche Konfiguration erforderlich.  
  
3.  Führen Sie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Setup ein weiteres Mal für RC3 aus, und installieren Sie Microsoft R Server (eigenständig).  

Diese Problemumgehung ist nicht erforderlich, wenn Sie ein Upgrade auf die RTM-Version von Microsoft R Server durchführen.

## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [Erste Schritte mit Microsoft R Server &#40;eigenständig&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  