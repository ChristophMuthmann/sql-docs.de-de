---
title: "Einrichten von SQL Server R Services (In-Database) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "Installieren von SQL Server R Services"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 30
---
# Einrichten von SQL Server R Services (In-Database)
  In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und späteren Versionen können Sie alle Komponenten, die [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] betreffen, mit dem Setup-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installieren.  
 
 
 Nach Abschluss des Setups sind unter Umständen einige zusätzliche Schritte erforderlich, um R Services zu aktivieren, Konten zu konfigurieren und Benutzern Berechtigungen für bestimmte Datenbanken zu erteilen.   
  
Wenn Sie nach dem Setup Probleme mit dem Zugriff auf die Datenbank haben oder frühere Versionen deinstallieren müssen, finden Sie weitere Informationen unter [Häufig gestellte Fragen zu Upgrade und Installation &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md).  

> [!NOTE]
> Um R Services (In-Database) installieren zu können, muss das Laufwerk, auf dem R Services installiert wird, die Erstellung von kurzen Dateinamen mithilfe der 8.3-Schreibweise unterstützen. Andernfalls können die Prozesse, die R aus SQL Server starten, möglicherweise nicht ausgeführt werden. Aktivieren Sie unbedingt die 8.3-Schreibweise auf dem Laufwerk, bevor Sie R Services installieren. Diese Einschränkung wird in einer späteren Version entfallen.

  
##  <a name="a-namebkmkinstallrservicesindatabasea-step-1-install-r-services-in-database-on-sql-server-2016-or-later"></a><a name="bkmk_installRServicesInDatabase"></a> Schritt 1: Installieren von R Services (In-Database) unter SQL Server 2016 oder später  
   
  
1.  Führen Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup aus.  
  
    Informationen dazu, wie Sie unbeaufsichtigte Installationen durchführen, finden Sie unter [Unattended Installs of SQL Server R Services](../../advanced-analytics/r-services/unattended-installs-of-sql-server-r-services.md).  
  
2.  Klicken Sie auf der Registerkarte **Installation** auf **Neue eigenständige SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.  
  
    > [!NOTE]  
    >  Sie können [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] nicht auf einem Failovercluster installieren. Sie können [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] jedoch auf einem eigenständigen Computer installieren, der „Always On“ verwendet und zu einer Verfügbarkeitsgruppe gehört. Weitere Informationen zur Verwendung von R Services in einer Always On-Verfügbarkeitsgruppe finden Sie unter [Always On-Verfügbarkeitsgruppen: Interoperabilität](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md).  
  
3.  Wählen Sie diese Optionen auf der Seite **Funktionsauswahl** aus:  
  
    -   **Datenbankmoduldienste**  
  
         Für die Verwendung von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]ist mindestens eine Instanz des Datenbankmoduls erforderlich. Sie können entweder eine Standardinstanz oder eine benannten Instanz verwenden.  
  
    -   **R Services (In-Database)**  
  
         Diese Option konfiguriert die Datenbankdienste, die von R-Aufträgen verwendet werden, und installiert die Erweiterungen, die externe Skripts und Vorgänge unterstützen.  
    > [!NOTE]
    > 
    > Um Ihren R-Code unter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführen zu können, müssen Sie **[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]** installieren. 
    > 
    > Microsoft R Server (eigenständig) ist hingegen eine Option, mit der Sie die Scale R-Bibliotheken auf einem Windows-Computer verwenden können, auf dem SQL Server nicht ausgeführt wird. Wir empfehlen die Installation von Microsoft R Server (eigenständig) auf einem Laptop oder einem anderen Computer, der für die R-Entwicklung verwendet wird, um R-Lösungen zu erstellen, die zu einem späteren Zeitpunkt auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellt werden können, auf der R Services (In-Database) ausgeführt wird.
 
  
4.  Klicken Sie auf der Seite **Zustimmung zur Installation von Microsoft R Open** auf **Annehmen**.  
  
     Diese Lizenzbedingungen sind für das Herunterladen von Microsoft R Open erforderlich. Sie betreffen eine Verteilung der Open Source-R-Basispakete und -Tools, einschließlich erweiterter R-Pakete und Konnektivitätsanbieter von Revolution Analytics.  
  
    > [!NOTE]  
    >  Wenn der von Ihnen verwendete Computer keinen Internetzugang hat, können Sie das Setup an dieser Stelle anhalten, um die Installationsprogramme wie hier beschrieben separat herunterzuladen: [Installation von R-Komponenten ohne Internetzugang](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).  
  
     Klicken Sie auf **Annehmen**, warten Sie, bis die Schaltfläche **Weiter** aktiv ist, und klicken Sie dann auf **Weiter**.  
  
5.  Stellen Sie auf der Seite **Installationsbereit** sicher, dass die folgenden Auswahlmöglichkeiten aktiviert sind, und klicken Sie auf **Installieren**.  
  
     **Funktionen**  
  
     Datenbankmoduldienste  
  
     R Services (In-Database)  
  
6.  Nach Abschluss der Installation starten Sie den Computer neu.   
  
  
##  <a name="a-namebkmkenablefeaturea-step-2-enable-r-services-and-verify-that-local-r-script-execution-works"></a><a name="bkmk_enableFeature"></a> Schritt 2: Aktivieren von R Services und Sicherstellen, dass das lokale R-Skript ausgeführt wird  
  
  
1. Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Wenn diese Anwendung noch nicht installiert ist, können Sie den Setup-Assistenten für SQL Server erneut ausführen, um einen Link zum Herunterladen zu öffnen und die Anwendung zu installieren.  
  
2. Stellen Sie eine Verbindung zu der Instanz her, in der Sie R Services (In-Database) installiert haben. Führen Sie den folgenden Befehl aus, um R Services explizit zu aktivieren. Andernfalls ist es nicht möglich, R-Skripts aufrufen, selbst wenn die Funktion von Setup installiert wurde.  
  
   ```    
   Exec sp_configure  'external scripts enabled', 1  
   Reconfigure  with override    
   ```  
  
10. Starten Sie den SQL Server-Dienst für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz. Das startet automatisch den verknüpften [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] -Dienst neu. Sie können den Dienst über den Bereich „Dienste“ in der Systemsteuerung oder mithilfe des SQL Server-Konfigurations-Managers neu starten.  
  
9. Wenn der SQL Server-Dienst verfügbar ist, stellen Sie sicher, dass die R-Funktion aktiviert ist, indem Sie den folgenden Befehl ausführen und überprüfen, ob *run_value* auf 1 gesetzt ist:  
  
    ```    
    Exec sp_configure  'external scripts enabled'    
    ```  
   Öffnen Sie optional den Bereich **Services**, und stellen Sie sicher, dass der Launchpad-Dienst für Ihre Instanz ausgeführt wird. Jede Instanz verfügt über einen eigenen Launchpad-Dienst.
   
10. Nun sollten Sie einfache R-Skripts wie den folgenden in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ausführen können:  
  
    ```  
    exec sp_execute_external_script  @language =N'R',  
    @script=N'OutputDataSet<-InputDataSet',    
    @input_data_1 =N'select 1 as hello'  
    with result sets (([hello] int not null));  
    go  
    ```  
  
    **Ergebnisse**  
  
    *hello*  
    *1*   
  
> [!IMPORTANT]  Wenn Sie auf SQL Server-Daten zugreifen oder R-Befehle von einem fernen Data Science-Client ausführen müssen, sind einige zusätzliche Schritte erforderlich. Die folgenden Schritte beschreiben diese zusätzlichen Anforderungen im Detail.
 
  
##  <a name="a-namebkmkconfigureaccountsa-step-3-enable-implied-authentication-for-launchpad-accounts"></a><a name="bkmk_configureAccounts"></a> Schritt 3: Aktivieren der impliziten Authentifizierung für Launchpad-Konten  
   
  
Beim Setup werden 20 neue Windows-Benutzerkonten angelegt, um Aufgaben unter dem Sicherheitstoken des [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]-Dienstes ausführen zu können. Wenn ein Benutzer ein R-Skript von einem externen Client sendet, aktiviert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein verfügbares Workerkonto, ordnet es der Identität des aufrufenden Benutzers zu und führt das R-Skript im Auftrag des Benutzers aus. Dies ist ein neuer Dienst des Datenbankmoduls, der eine sichere Ausführung externer Skripts unterstützt. Er wird als *implizite Authentifizierung* bezeichnet. 

Sie können diese Konten in der Windows-Benutzergruppe **SQLRUserGroup** anzeigen.  Wenn Sie R-Skripts von einem Data Science-Remoteclient ausführen müssen und die Windows-Authentifizierung verwenden, muss diesen Workerkonten die Berechtigung erteilt werden, sich in Ihrem Namen bei der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz anzumelden.  
  
1. Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] im Objekt-Explorer den Knoten **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Anmeldungen**, und wählen Sie anschließend **Neue Anmeldung**.  
2. Klicken Sie im Dialogfeld **Anmeldung – Neu** auf **Suchen**.  
3. Klicken Sie auf **Objekttypen**, und wählen Sie **Gruppen** aus. Deaktivieren Sie alle anderen Optionen.  
4. Geben Sie unter „Namen des auszuwählenden Objekts eingeben“ *SQLRUserGroup* ein, und klicken Sie auf **Namen überprüfen**.  
5. Der Name der lokalen Gruppe, die zum Launchpad-Dienst der Instanz gehört, sollte in etwa wie folgt aufgelöst werden: *instancename\SQLRUserGroup*. Klicken Sie auf **OK**.  
6. In der Standardeinstellung ist die Anmeldung der **öffentlichen** Rolle zugewiesen und verfügt über die Berechtigung, eine Verbindung zum Datenbankmodul herzustellen. 
7. Klicken Sie auf **OK**.  
  
> [!NOTE] Wenn Sie eine SQL-Anmeldung für das Ausführen von R-Skripts im SQL Compute Context verwenden, ist dieser zusätzliche Schritt nicht erforderlich.
  
  
## <a name="step-4-give-non-admin-users-r-script-permissions"></a>Schritt 4: Erteilen von R-Skriptberechtigungen für Nicht-Admin-Benutzer  
  
Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eigenständig installiert haben und R-Skripts in Ihrer eigenen Instanz ausführen, führen Sie die Skripts in der Regel als Administrator aus und verfügen daher implizit über die Berechtigung für verschiedene Vorgänge und alle Daten in der Datenbank sowie über die Möglichkeit, neue R-Pakete nach Bedarf zu installieren.  
  
Allerdings verfügen in einem Unternehmensszenario die meisten Benutzer, einschließlich derjenigen, die mithilfe von SQL-Benutzernamen auf die Datenbank zugreifen, nicht über diese erhöhten Berechtigungen. Aus diesem Grund müssen Sie jedem Benutzer, der externe Skripts ausführt, Benutzerberechtigungen zum Ausführen von R-Skripts in jeder Datenbank, in der R verwendet wird, erteilen.   
  
  
```  
USE <database_name>  
GO  
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]  
```  

> [!TIP] Benötigen Sie Hilfe beim Setup? Sind Sie unsicher, ob Sie alle Schritte ausgeführt haben?
>
> Verwenden Sie diese benutzerdefinierten Berichte, um den Installationsstatus von R Services zu überprüfen. Weitere Informationen finden Sie unter [Überwachung von R Services mithilfe von benutzerdefinierten Berichten](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md).    
  
##  <a name="a-namebkmkadditionala-optional-modifications"></a><a name="bkmk_Additional"></a> Optionale Änderungen  
  
Dieser Abschnitt beschreibt zusätzliche Änderungen, die Sie an der Konfiguration der Instanz oder an Ihrem Data Science-Client vornehmen können, um die Ausführung von R-Skripts zu unterstützen.
  
### <a name="modify-the-number-of-worker-accounts-used-by-includersqllaunchpadtokenrsqllaunchpadmdmd"></a>Ändern der Anzahl von Workerkonten, die von [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] verwendet werden
  
Wenn Sie erwarten, dass Sie R intensiv verwenden oder dass viele Benutzer gleichzeitig Skripts ausführen werden, können Sie die Anzahl der Workerkonten erhöhen, die dem Launchpad-Dienst zugewiesen sind. Weitere Informationen finden Sie unter [Ändern des Benutzerkontenpools für SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).  
  
  
### <a name="give-your-r-users-or-logins-read-write-or-ddl-permissions-as-needed-in-additional-databases"></a>Erteilen Sie Ihren R-Benutzern oder -Anmeldenamen nach Bedarf Lese-, Schreib- oder DDL-Berechtigungen für weitere Datenbanken  
  
Beim Ausführen von R-Skripts muss das Benutzerkonto unter Umständen Daten aus anderen Datenbanken lesen, neue Tabellen zum Speichern von Ergebnissen erstellen und Daten in Tabellen schreiben. 
     
Für jeden Benutzer, der R-Skripts ausführen wird, sollten Sie sicherstellen, dass das Benutzerkonto über die Berechtigungen **db_datareader**, **db_datawriter** bzw. **db_ddladmin** für die betreffende Datenbank verfügt.   
       
Die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung erteilt beispielsweise der SQL-Anmeldung *MySQLLogin* die Rechte zum Ausführen von T-SQL-Abfragen in der *RSamples*-Datenbank. Um diese Anweisung auszuführen, muss die SQL-Anmeldung bereits im Sicherheitskontext des Servers vorhanden sein.  
  
```  
USE RSamples  
GO  
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'  
```  
  
Weitere Informationen zu den Berechtigungen in den einzelnen Rollen finden Sie unter [Rollen auf Datenbankebene](../../relational-databases/security/authentication-access/database-level-roles.md).  
  
  
### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Erstellen einer ODBC-Datenquelle für die Instanz auf Ihrem Data Science-Client  
  
Wenn Sie eine R-Lösung auf einem Data Science-Clientcomputer erstellen und eine Verbindung zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computer als Rechenkontext herstellen müssen, können Sie eine SQL-Anmeldung oder eine integrierte Windows-Authentifizierung verwenden.  
  
Wenn Sie eine SQL-Anmeldung verwenden, müssen Sie sicherstellen, dass sie über die erforderlichen Berechtigungen für die Datenbank verfügt, in der Sie Daten lesen werden. Sie erreichen dies durch Hinzufügen der Berechtigungen *Connect to* und *SELECT* oder indem Sie den Anmeldenamen zur Rolle **db_datareader** hinzufügen. Wenn Sie Objekte erstellen möchten, benötigen Sie **DDL_admin**-Rechte.  Um Daten in Tabellen zu speichern, fügen Sie den Anmeldenamen zur **db_datawriter**-Rolle hinzu.  
  
Wenn Sie die Windows-Authentifizierung verwenden, müssen Sie eine ODBC-Datenquelle auf dem Data Science-Client konfigurieren, die diesen Instanznamen und andere Verbindungsinformationen angibt.  
  
Weitere Informationen finden Sie unter [Verwenden von ODBC-Datenquellen-Administrator](http://windows.microsoft.com/windows/using-odbc-data-source-administrator).  
  
### <a name="optimize-the-server-for-r"></a>Optimieren des Servers für R  

Die Standardeinstellungen für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup dienen zur Optimierung des Lastenausgleichs des Servers für eine Vielzahl von Diensten, die vom Datenbankmodul unterstützt werden, einschließlich ETL-Prozesse, Reporting, Überwachung und Anwendungen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Daten verwenden. Daher können in den Standardeinstellungen Ressourcen für R-Vorgänge eingeschränkt oder gedrosselt sein, insbesondere für speicherintensive Vorgänge.  
  
 Um sicherzustellen, dass R-Aufgaben über die entsprechende Priorität und die nötigen Ressourcen verfügen, wird empfohlen, dass Sie die Ressourcenkontrolle verwenden, um einen externen Ressourcenpool speziell für R-Vorgänge zu konfigurieren. Eventuell ist es auch sinnvoll, die Größe des Speichers zu ändern, der dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankmodul zugewiesen ist, oder die Anzahl der Konten zu erhöhen, die unter dem [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]-Dienst ausgeführt werden.  
  
-   Konfigurieren Sie einen Ressourcenpool für das Verwalten von externen Ressourcen  
  
     [ERSTELLEN SIE EXTERNEN RESSOURCENPOOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
-   Ändern Sie den Arbeitsspeicherumfang, der für das Datenbankmodul reserviert ist  
  
     [Serverkonfigurationsoptionen für den Serverarbeitsspeicher](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
-   Ändern Sie der Anzahl der R-Konten, die von [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] gestartet werden können  
  
     [Ändern des Benutzerkontenpools für SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  
  
### <a name="get-the-r-source-code-optional"></a>Rufen Sie den R-Quellcode ab (optional)  

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthält eine Verteilung der Open Source-R-Basispakete.  
  
Klicken Sie optional auf einen der folgenden Links, um sofort mit dem Herunterladen des geänderten GPL/LGPL-Quellcodes zu beginnen. Der Quellcode wird gemäß der GNU General Public License zur Verfügung gestellt, ist für die Installation oder Verwendung von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] jedoch nicht erforderlich.  
  
-   Kompatibel mit RC2: Laden Sie das Archiv [rre-gpl-src.8.0.2.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786770) herunter 
  
-   Kompatibel mit RC3: Laden Sie das Archiv [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786771) herunter 

-   Kompatibel mit RTM: Laden Sie das Archiv [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkID=786771) herunter
  
## <a name="troubleshooting"></a>Problembehandlung  
 Sind Probleme aufgetreten? Beachten Sie die folgende Liste häufig auftretender Probleme bei der Installation von Vorabversionen von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]:  
  
 [Häufig gestellte Fragen zu Upgrade und Installation &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Einrichten eines Data Science-Clients](../../advanced-analytics/r-services/set-up-a-data-science-client.md)   
 [Erstellen eines eigenständigen R-Servers](../../advanced-analytics/r-services/create-a-standalone-r-server.md)  
  
  