---
title: Einrichten von SQL Server Machine Learning-Services (Datenbankintern) | Microsoft Docs
ms.custom: 
ms.date: 11/15/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- Installieren von SQL Server R Services
- Installieren von SQL Server-Machine Learning-Services
- Richten Sie R Services
- Installieren Sie SQL Machine learning
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 4d18a45b40c7f80ae2b46514f6c8245b80f6b142
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="set-up-sql-server-machine-learning-services-in-database"></a>Einrichten von SQL Server Machine Learning-Services (Datenbankintern)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Thema wird beschrieben, wie zum Installieren und konfigurieren die folgenden Machine learning-Funktionen, die in der Datenbank Analytics in SQL Server unterstützt werden:

+ **SQL Server 2016 R Services (Datenbankintern)**. Wenn Sie SQL Server 2016 haben, installieren Sie dieses Feature, um die Ausführung von R-Code in SQL Server zu ermöglichen. Erfordert das Datenbankmodul an.

    [Einrichten von Machine Learning in der SQL Server 2016](#bkmk_2016top)

+ **SQL Server 2017 Machine Learning Services (Datenbankintern)**. Wenn Sie SQL Server-2017 verfügen, installieren Sie diese Option, um Code von R (oder Python) in SQL Server ausgeführt. Erfordert das Datenbankmodul an. 

    [Machine Learning in der SQL Server-2017 einrichten](#bkmk_2017top)

+ Ein Machine Learning-Server mit **keine** SQL Server

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup schließt auch die Möglichkeit, eine "eigenständig"-Version des Machine learning-Komponenten zu installieren, die das Datenbankmodul ist nicht erforderlich und wird von SQL Server nicht ausgeführt.  Im Allgemeinen wird empfohlen, dass Sie diese Option auf einem anderen Computer als dem Computer installieren, auf dem SQL Server gehostet.
    
    [Einrichten eines eigenständigen Machine Learning-Servers](create-a-standalone-r-server.md).

Dieser Artikel beschreibt den Prozess der Einrichtung, die verwendet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup-Assistenten. Installation über die Befehlszeile oder Installationsprogramme für die Verwendung in offline-Server herunterladen finden Sie in diesen Artikeln:

+ [Installieren von R für SQL Server über die Befehlszeile](unattended-installs-of-sql-server-r-services.md)
+ [Installieren Sie Python für SQL Server über die Befehlszeile](../python/unattended-installs-of-sql-server-python-services.md)
+ [Installieren Sie einen eigenständigen Machine Learning-Server über die Befehlszeile](install-microsoft-r-server-from-the-command-line.md)
+ [Installieren von Machine Learning-Komponenten auf einem Server mit keine Aces internet](installing-ml-components-without-internet-access.md)

**Gilt für:** SQLServer 2016, SqlServer 2017

## <a name="bkmk_prereqs"></a> Prüfliste vor der Installation

+ Machine Learning in der Datenbank erfordert SQLServer 2016 oder höher. 

+ Unterstützte Sprachen: 

    + SQL Server 2016 unterstützt nur die R. 

    + R ist auch verfügbar als Vorschaufunktion in Azure SQL-Datenbank mit einigen Einschränkungen. Weitere Informationen finden Sie unter [mithilfe von R in Azure SQL-Datenbank](using-r-in-azure-sql-database.md)

    + Verwendung von Python erfordert SQLServer 2017 oder höher.

+ Wenn Sie alle vorherigen Versionen von Revolution Analytics-Entwicklungsumgebung oder dem "revoscaler"-Pakete verwendet oder wenn Sie alle Vorabversionen von SQL Server 2016 installiert haben, müssen Sie sie deinstallieren. Seite-an-Seite-Installation wird nicht unterstützt. Hilfe zum Entfernen früherer Versionen finden Sie [Upgrade und Installation – häufig gestellte Fragen für SQL Server-Machine Learning-Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

+ Sie können keine SQL Server 2016 R Services oder SQL Server 2017 Machine Learning Services auf einem Domänencontroller installieren. Der R-Dienste "oder" Machine Learning-Dienste Teil von Setup schlägt fehl.

+ Sie können keine Machine learning-Funktionen auf einem Failovercluster installieren. Die Sicherheitsmechanismus, der verwendet wird, zur Isolierung von externen Skriptprozesse ist nicht kompatibel mit einer Windows Server Failover Cluster-Umgebung. Dieses Problem zu umgehen können Sie eine der folgenden Aktionen ausführen:
    * Mithilfe der Replikation um erforderlichen Tabellen in einer SQL Server-Instanz mit Machine Learning aktiviert zu kopieren.
    * Installieren Sie Machine Learning auf einem eigenständigen Computer, der AlwaysOn verwendet und ist Teil einer verfügbarkeitsgruppe an.

+ Machine Learning-Framework erfordert zusätzliche Konfigurationsschritte, nachdem Setup abgeschlossen ist. Die genauen Schritte hängen von Ihrer Organisation und die Sicherheitsrichtlinien, die Serverkonfiguration und die vorgesehenen Benutzer ab. Es wird empfohlen, dass Sie überprüfen Sie alle Schritte und zusätzliche Konfigurationsschritte, die erforderlich sein könnten in Ihrer Umgebung bestimmen.

## <a name="bkmk2016top"></a>Installieren von SQL Server 2016 R Services (Datenbankintern)

> [!div class="checklist"]
> * Installieren von Datenbankmodul und Machine learning-Funktionen
> * Erforderliche Schritte nach der Installation: Aktivieren von Machine Learning und neu starten
> * Optionale Schritte der nach der Installation: Firewallregeln hinzufügen, fügen Sie Benutzer hinzu, ändern oder Konfigurieren von Dienstkonten, richten Sie eine remote Data Science-Client

**Mithilfe der SQL Server 2016-Setup-Assistenten**

1. Führen Sie den Setup-Assistenten von SQL Server aus.

2. Auf der **Installation** Registerkarte **eigenständige neue SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.

    
     ![Installieren von R Services (Datenbankintern)](media/2016-setup-installation-rsvcs.png "starten Sie die Installation des Datenbankmoduls mit R-Services")
   
3. Auf der **Funktionsauswahl** Seite, wählen Sie die folgenden Optionen:

   - Wählen Sie **Datenbankmoduldienste**. Das Datenbankmodul ist in jeder Instanz erforderlich, die Machine Learning verwendet.
   - Wählen Sie **R Services (Datenbankintern)**. Installiert die Unterstützung für in der Datenbank mithilfe von r
    
     ![R Services Funktionsauswahl](media/2016setup-rsvcs-features.png "wählen Sie diese Funktionen für R Services In der Datenbank")

    > [!IMPORTANT]
    > Installieren Sie R-Server und R Services nicht zur selben Zeit. Sie würden normalerweise R Server (eigenständig) zum Erstellen einer Umgebung, die ein datenanalyst oder Entwickler verwendet werden, die Verbindung mit SQL Server installieren und Bereitstellen von R-Lösungen. Daher besteht keine Notwendigkeit beide auf demselben Computer zu installieren.

4.  Auf der **stimmen Sie installiert Microsoft R Open** auf **Accept**.
  
    Die Lizenzbedingungen ist erforderlich, um Microsoft R Open, die eine Verteilung der open Source-R-Basispakete und Tools, zusammen mit erweiterten R-Paketen und Konnektivitätsanbietern von Microsoft R-Entwicklungsteam umfasst herunterladen.
  
    Wenn der Computer, die Sie verwenden keinen Zugriff auf das Internet, Sie können Setup an diesem Punkt, um die Installationsprogramme getrennt, wie in beschrieben herunterladen anhalten [Installieren von R-Komponenten ohne Internetzugang](installing-ml-components-without-internet-access.md).
  
5. Nachdem Sie den Lizenzvertrag akzeptiert haben, besteht eine kurze Pause während der Installer vorbereitet wird. Klicken Sie auf **Weiter** Wenn die Schaltfläche wird verfügbar.

6. Auf der **Installationsbereit** Seite, stellen Sie sicher, dass die folgenden Elemente enthalten sind, und Sie dann wählen **installieren**.

   + Datenbankmoduldienste
   + R Services (In-Database)

7. Wenn die Installation abgeschlossen ist, starten Sie den Computer neu.


## <a name="bkmk2017top"></a>Installieren von SQL Server 2017 Machine Learning-Services (Datenbankintern)

> [!div class="checklist"]
> * Installieren von Datenbankmodul und Machine learning-Funktionen
> * Erforderliche Schritte nach der Installation: Aktivieren von Machine Learning und neu starten
> * Optionale Schritte der nach der Installation: Firewallregeln hinzufügen, fügen Sie Benutzer hinzu, ändern oder Konfigurieren von Dienstkonten, richten Sie eine remote Data Science-Client.

**Erste Schritte**

1. Führen Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup aus.
  
2. Auf der **Installation** Registerkarte **eigenständige neue SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.

     ![Installieren von Machine Learning-Services (Datenbankintern)](media/2017setup-installation-page-mlsvcs.png "starten Sie die Installation des Datenbankmoduls mit Machine Learning-Diensten")

3. Auf der **Funktionsauswahl** Seite, wählen Sie die folgenden Optionen:
   
    + Wählen Sie **Datenbankmoduldienste**. Das Datenbankmodul ist in jeder Instanz erforderlich, die Machine Learning verwendet.

    + Wählen Sie **Machine Learning-Services (Datenbankintern)**. Diese Option installiert die Unterstützung für in der Datenbank mithilfe von r Nachdem Sie diese Option ausgewählt haben, können Sie Machine learning Sprache auswählen. Sie können nur R auswählen oder können Sie R und Python hinzufügen.
   
    ![Funktionsauswahl für Machine Learning Services](media/2017setup-features-page-mls-rpy.png "wählen Sie diese Funktionen für R Services In der Datenbank")

    Wenn Sie nicht die R- oder Python Sprachoptionen auswählen, installiert der Setup-Assistent nur die Erweiterbarkeitsframework, die SQL Server vertrauenswürdige Launchpad enthält und sprachspezifische Komponenten nicht installiert.  Im Allgemeinen wird empfohlen, dass Sie mindestens eine Sprache zu installieren. Allerdings können Sie diese Option verwenden, wenn Sie beabsichtigen, das den Bindungsprozess sofort zu verwenden, um Machine learning-Komponenten zu aktualisieren. Weitere Informationen finden Sie unter [verwenden SqlBindR zum Aktualisieren einer Instanz des R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

    Es wird empfohlen, die Sie **nicht** die Funktionen für eigenständige und In der Datenbank auf demselben Computer installieren, und installieren Sie sie nie zur gleichen Zeit. Beim Bereitstellen von Lösungen, würden Sie normalerweise Machine Learning-Server (eigenständig) zum Erstellen einer Umgebung, die ein datenanalyst oder Entwickler verwendet werden, die Verbindung mit SQL Server installiert. Daher besteht keine Notwendigkeit beide auf demselben Computer zu installieren.

4.  Lizenzverträge für Machine Learning: je nachdem welche Sprachen, die Sie installieren, Sie die Lizenzverträge für R, Python oder beides zustimmen müssen.

    + Lizenzbedingungen für R: die Lizenzbedingungen umfasst Microsoft R zu öffnen, die eine Verteilung der open Source-R-Basispakete und Tools, zusammen mit erweiterten R-Paketen und Konnektivitätsanbietern von Microsoft-Entwicklungsteam enthält.
  
    + Lizenzbedingungen für Python. Der Python-open-Source-Lizenzvertrag deckt auch Anaconda und verwandte Tools sowie einige neuen Python-Bibliotheken von Microsoft-Entwicklungsteam.

    Klicken Sie auf **Accept** an, dass Ihr Vertrag. Eine kurze Pause vorhanden ist, während die Komponenten vorbereitet sind, und klicken Sie dann die **Weiter** Schaltfläche ist verfügbar.

    Wenn der Computer, die Sie verwenden keinen Zugriff auf das Internet, Sie können Setup an diesem Punkt, um die Installationsprogramme getrennt, wie hier beschrieben herunterladen anhalten: [Machine Learning-Komponenten ohne Internetzugang installieren](installing-ml-components-without-internet-access.md).

6. Auf der **Installationsbereit** Seite, stellen Sie sicher, dass die folgenden Elemente enthalten sind, und Sie dann wählen **installieren**.

   - Datenbankmoduldienste
   - Machine Learning-Dienste (datenbankintern)
   - R, Python oder beides

7. Wenn die Installation abgeschlossen ist, notieren Sie sich den Speicherort der Setup-Protokoll, und klicken Sie dann starten Sie den Computer neu.

###  <a name="bkmk_enableFeature"></a>Schritt nach der Installation erforderlich

Aus Gründen der Sicherheit wird die Machine Learning-Funktion nicht standardmäßig aktiviert, auch wenn die Funktion installiert wurde. Ein Server-Administrator muss das Feature aktivieren und die Instanz neu gestartet. 

In diesem Abschnitt wird beschrieben, wie die Instanz für Machine Learning neu konfiguriert. Konfiguration richtet externe-Dienstkonten und startet den Launchpad-Dienst.

1. Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Wenn diese Anwendung noch nicht installiert ist, können Sie den Setup-Assistenten für SQL Server erneut ausführen, um einen Link zum Herunterladen zu öffnen und die Anwendung zu installieren.
  
2. Herstellen einer Verbindung mit der Instanz, auf dem Machine Learning installiert, und führen Sie den folgenden Befehl aus:

   ```SQL
   sp_configure
   ```

    Suchen Sie nach dem Wert der **externe Skripts aktiviert** -Eigenschaft, die ausgeführt werden **0**. Ist, dass die Funktion standardmäßig oberflächenreduzierung deaktiviert ist.
     
3. Um die externe Skriptingfunktion zu aktivieren, führen Sie die folgende Anweisung aus:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
4. Starten Sie den SQL Server-Dienst für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz. Startet den zugehörigen neu auch automatischer Neustart des SQL Server-Diensts [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst.

    Sie können den Dienst neu starten, mit der **Services** Bereich in der Systemsteuerung oder mithilfe von SQL Server-Konfigurations-Manager.

5. Um sicherzustellen, dass der externes Skript-Ausführung-Dienst, müssen Sie in SQL Server Management Studio aktiviert ist, öffnen Sie ein neues **Abfrage** Fenster, und führen Sie den folgenden Befehl aus:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```
    Der Wert **Run_value** sollte jetzt auf 1 festgelegt werden.
    
6. Öffnen der **Services** Bereich, und stellen Sie sicher, dass das Launchpad-Dienst für die Instanz ausgeführt wird. Wenn Sie mehrere Instanzen installieren, verfügt jede Instanz über einen eigenen Launchpad-Dienst.

7. Es ist ratsam, führen Sie ein einfaches Skript aus, um sicherzustellen, dass externe Skripts Laufzeiten mit SQL Server kommunizieren können. 

    Öffnen Sie ein neues **Abfrage** Fenster in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und führen Sie ein Skript z. B. Folgendes:
    
    + For R
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + For Python
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    Das Skript kann etwas dauern, während zum ersten Mal ausführen die externes Skript-Laufzeit geladen wird. Die Ergebnisse sollten etwa wie folgt aussehen:

    | Hello |
    |----|
    | 1|


8. Wenn Sie Fehlermeldungen erhalten, fahren Sie mit Abschnitt beschreiben Weitere, optionale Änderungen, die Sie möglicherweise vornehmen, nachdem die Installation abgeschlossen ist, oder finden im Handbuch zur Problembehandlung:

    + [Optionale Schritte der nach der Installation: Konfigurieren von Dienst- und Berechtigungen](#bkmk_FollowUp) 
    + [Problembehandlung bei Machine Learning in der SQL Server](upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="bkmk_FollowUp"></a>Optionale Schritte der nach der installation

Je nach Ihrer Anwendungsfall für maschinelles lernen müssen Sie zusätzliche Änderungen vornehmen, auf dem Server, die Firewall, den Dienst bzw. die Datenbankberechtigungen verwendeten Konten. Die Änderungen, die Sie vornehmen müssen, variieren nach Groß-/Kleinschreibung.

Allgemeine Szenarien, die zusätzliche Änderungen erfordern:

* Ändern die Firewallregeln für eingehende Verbindungen zu SQL Server zu ermöglichen.
* Aktivieren von zusätzlichen Netzwerkprotokollen.
* Sicherstellen, dass der Server Remoteverbindungen unterstützt.
* Aktivieren der *implizite Authentifizierung*, wenn Benutzer Zugriff auf SQL Server-Daten von einem remote Data Science-Client, und führen Sie Code mithilfe des RODBC-Pakets oder andere ODBC-Datenanbieter.
* Benutzer Zugriff auf einzelne Datenbanken gewährt.
* Beheben von Sicherheitsproblemen, die Kommunikation mit dem Launchpad-Dienst zu verhindern.
* Sicherstellen, dass Benutzer über die Berechtigung zum Ausführen von Code oder Pakete zu installieren.

> [!NOTE]
> Nicht alle aufgelisteten Änderungen können erforderlich sein. Allerdings wird empfohlen, dass Sie überprüfen, dass alle Elemente, um festzustellen, ob sie für Ihr Szenario anwendbar sind.

Weitere Tipps zur Problembehandlung finden Sie hier: [häufig gestellte Fragen zu Upgrade und Installation](../r/upgrade-and-installation-faq-sql-server-r-services.md)

### <a name="bkmk_configureAccounts"></a>Aktivieren Sie die implizite Authentifizierung für die Kontogruppe Launchpad

Während des Setups werden einige neue Windows-Benutzerkonten zum Ausführen von Aufgaben unter des Sicherheitstokens des erstellt die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Dienst. Wenn ein Benutzer ein R-Skript von einem externen Client sendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktiviert ein Konto Arbeitsthreads verfügbar, wird es auf die Identität des aufrufenden Benutzers zugeordnet und führt das R-Skript im Namen des Benutzers. Dieser neue Dienst des Datenbankmoduls unterstützt die sichere Ausführung externer Skripts, die aufgerufen *implizite Authentifizierung*.

Sie können diese Konten anzeigen, in der Windows-Benutzergruppe **SQLRUserGroup**. Standardmäßig werden 20 Konten erstellt, ist in der Regel mehr als ausreichend, für die Ausführung von R-Aufträge.

Jedoch, wenn Sie, führen Sie R-Skripts von einem remote Data Science-Client möchten und Windows-Authentifizierung verwenden, Sie müssen erteilen diese Konten über die Berechtigung zum Anmelden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz in Ihrem Namen.

1. Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Objekt-Explorer den Knoten **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Anmeldungen**, und wählen Sie anschließend **Neue Anmeldung**.
2. In der **Anmeldung - neu** wählen Sie im Dialogfeld **Suche**.
3. Wählen Sie die **Objekttypen** und **Gruppen** Kontrollkästchen, und deaktivieren Sie alle anderen Kontrollkästchen.
4. Klicken Sie auf **erweitert**, überprüfen Sie, ob die zu suchende Position der aktuellen Computer, und klicken Sie dann auf **Jetzt suchen**.
5. Führen Sie einen Bildlauf durch die Liste der Gruppenkonten auf dem Server, bis Sie beginnen mit gefunden `SQLRUserGroup`.
    
    + Der Name der Gruppe, die für den Launchpad-Dienst zugeordnet ist die _Standardinstanz_ ist immer nur **SQLRUserGroup**. Wählen Sie dieses Konto nur für die Standardinstanz.
    + Bei Verwendung einer _benannte Instanz_, wird der Instanzname dem Standardnamen angefügt `SQLRUserGroup`. Daher, wenn die Instanz "MLTEST" benannt wird, der Standardbenutzernamen Gruppe für diese Instanz wäre **SQLRUserGroupMLTest**.
5. Klicken Sie auf **OK** , schließen Sie das Dialogfeld "Erweiterte Suche" aus, und stellen Sie sicher, dass Sie das richtige Konto für die Instanz ausgewählt haben. Jede Instanz können eigenen Launchpad-Dienst und die Gruppe für diesen Dienst erstellt haben.
6. Klicken Sie auf **OK** einmal zum Schließen der **Benutzer oder Gruppe auswählen** (Dialogfeld).
7. In der **Anmeldung - neu** (Dialogfeld), klicken Sie auf **OK**. In der Standardeinstellung ist die Anmeldung der **öffentlichen** Rolle zugewiesen und verfügt über die Berechtigung, eine Verbindung zum Datenbankmodul herzustellen.

### <a name="bkmk_AllowLogon"></a>Vergabe von Benutzerberechtigungen für das Ausführen externer Skripts.

> [!NOTE]
> Wenn Sie eine SQL-Anmeldung für die Ausführung von R-Skripts in einer SQL Server-computekontext verwenden, ist dieser Schritt nicht erforderlich.

Wenn Sie installiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Ihrer eigenen Instanz sind Sie in der Regel Skripts als Administrator ausführen oder zumindest ein Datenbankbesitzer und daher verfügen über implizite Berechtigungen für verschiedene Vorgänge, werden alle Daten in der Datenbank und die Möglichkeit zum Installieren der neuen Pakete nach Bedarf.

Allerdings müssen in einem Enterprise-Szenario können die meisten Benutzer, einschließlich Benutzer, die Zugriff auf die Datenbank mithilfe von SQL-Anmeldungen, diese erhöhten Berechtigungen keine. Aus diesem Grund müssen für jeden Benutzer, die R oder Python-Skripts ausgeführt werden, Sie erteilen die Benutzerberechtigungen zum Ausführen von Skripts in jeder Datenbank, in der externen Skripts verwendet werden.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> Benötigen Sie Hilfe beim Setup? Sind Sie unsicher, ob Sie alle Schritte ausgeführt haben? Verwenden Sie diese benutzerdefinierten Berichte, um Installationsstatus überprüfen und zusätzliche Schritte ausführen. 
> 
> [Verwenden von benutzerdefinierten Berichten Machine Learning-Dienste überwachen,](monitor-r-services-using-custom-reports-in-management-studio.md).

### <a name="ensure-that-the-sql-server-computer-supports-remote-connections"></a>Stellen Sie sicher, dass der Computer mit SQL Server Remoteverbindungen unterstützt

Wenn Sie von einem Remotecomputer herstellen können, überprüfen Sie, ob der Server Remoteverbindungen zulässt. Remoteverbindungen werden manchmal standardmäßig deaktiviert.

Überprüfen Sie außerdem, um festzustellen, ob die Firewall den Zugriff auf SQL Server zulässt. Standardmäßig ist der von SQL Server verwendete Port häufig durch die Firewall blockiert. Wenn Sie die Windows-Firewall verwenden, finden Sie unter [Konfigurieren der Windows-Firewall für Datenbankmodulzugriff](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).

### <a name="give-your-users-read-write-or-ddl-permissions-to-the-database"></a>Geben Sie Ihre Benutzer zu lesen, schreiben oder DDL-Berechtigungen für die Datenbank

Das Benutzerkonto, mit dem Ausführen von R oder Python, möglicherweise müssen zum Lesen von Daten von anderen Datenbanken, Erstellen von neuen Tabellen zum Speichern der Ergebnisse und Schreiben von Daten in Tabellen. Daher müssen Sie für jeden Benutzer, das Ausführen von R oder Python-Skripts, sicherstellen, dass der Benutzer die entsprechenden Berechtigungen für die Datenbank verfügt: *"db_datareader"*, *Db_datawriter*, oder *Db_ Ddladmin*.

Die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung erteilt beispielsweise der SQL-Anmeldung *MySQLLogin* die Rechte zum Ausführen von T-SQL-Abfragen in der *RSamples* -Datenbank. Um diese Anweisung auszuführen, muss die SQL-Anmeldung bereits im Sicherheitskontext des Servers vorhanden sein.

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Weitere Informationen zu den Berechtigungen, die in den einzelnen Rollen enthalten, finden Sie unter [Datenbankrollen](../../relational-databases/security/authentication-access/database-level-roles.md).

### <a name="use-machine-learning-in-an-azure-vm"></a>Machine Learning in einer Azure-VM verwenden

Wenn Sie einen virtuellen Computer in Azure Machine Learning-Dienste (oder R Services) installiert haben, müssen Sie möglicherweise einige zusätzlichen Standardeinstellungen zu ändern. Weitere Informationen finden Sie unter [Installieren von SQL Server Machine Learning auf virtuellen Azure-Computer](installing-sql-server-r-services-on-an-azure-virtual-machine.md).

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Erstellen einer ODBC-Datenquelle für die Instanz auf Ihrem Data Science-Client

Wenn Sie R-Lösungen auf einer Data Science-Clientcomputer erstellen und Code mithilfe von SQL Server-Computers als computekontext ausführen müssen, können Sie eine SQL-Anmeldung oder die integrierte Windows-Authentifizierung verwenden.

* Wenn Sie eine SQL-Anmeldung verwenden, müssen Sie sicherstellen, dass sie über die erforderlichen Berechtigungen für die Datenbank verfügt, in der Sie Daten lesen werden. Können Sie dies tun, indem hinzufügen *Herstellen einer Verbindung mit* und *wählen* Berechtigungen, oder indem Sie den Anmeldenamen für die *"db_datareader"* Rolle. Bei Anmeldungen, die zum Erstellen von Objekten müssen hinzufügen *DDL_admin* Rechte. Für Anmeldungen, die Daten speichern müssen, um Tabellen, fügen Sie den Anmeldenamen für die *Db_datawriter* Rolle.

* Für Windows-Authentifizierung: müssen Sie möglicherweise eine ODBC-Datenquelle auf dem Data Science-Client zu konfigurieren, der den Namen der Instanz und andere Verbindungsinformationen angibt. Weitere Informationen finden Sie unter [ODBC-Datenquellenadministrator](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie sichergestellt haben, dass das Feature für die Ausführung von Skripts in SQL Server funktioniert, können Sie R und Python-Befehle ausführen, von SQL Server Management Studio, Visual Studio-Code oder einem anderen Client, der T-SQL-Anweisungen an den Server gesendet werden kann. Bevor Sie dies tun, empfiehlt es sich um nehmen einige Änderungen an der Systemkonfiguration, zur Unterstützung einer starke Nutzung von Machine Learning, oder fügen neue R-Pakete.

Dieser Abschnitt enthält einige allgemeine Optimierungen und Learning Aktivitäten für maschinelles lernen.

### <a name="add-more-worker-accounts"></a>Weitere Konten hinzufügen

Wenn Sie glauben, dass R intensivsten verwendet werden kann oder wenn Sie davon ausgehen, dass viele Benutzer gleichzeitig ausgeführte Skripts werden, können Sie die Anzahl der Worker Konten erhöhen, die mit dem Launchpad-Dienst zugewiesen sind. Weitere Informationen finden Sie unter [Ändern des benutzerkontenpools für SQL Server-Machine Learning-Services](modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="bkmk_optimize"></a>Optimieren des Servers für den externen skriptausführung

Die Standardeinstellungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup das Gleichgewicht des Servers für eine Vielzahl von Diensten zu verbessern, die vom Datenbankmodul, extrahieren, Transformieren und laden (ETL) Prozesse, Berichts-, Überwachung, enthalten möglicherweise unterstützt werden sollen und Anwendungen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten. In den Standardeinstellungen finden Sie möglicherweise daher, dass Ressourcen für Machine Learning sind manchmal eingeschränkt oder, insbesondere in arbeitsspeicherintensive Vorgänge gedrosselt.

Um sicherzustellen, dass die Machine Learning Aufträge priorisiert und Ressourcen entsprechend zugewiesen sind, wird empfohlen, dass Sie SQL Server-Ressourcenkontrolle verwenden, um einen externen Ressourcenpool zu konfigurieren. Sie möchten möglicherweise auch die Größe des Arbeitsspeichers zu ändern, die zugeordnet ist, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmodul, oder erhöhen Sie die Anzahl der Konten, die unter ausgeführt der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst.

- Um einen Ressourcenpool für die Verwaltung von externen Ressourcen zu konfigurieren, finden Sie unter [erstellen Sie einen externen Ressourcenpool](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Um die reservierten Umfang an Arbeitsspeicher für die Datenbank zu ändern, finden Sie unter [Server Speicherkonfigurationsoptionen](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- So ändern Sie die Anzahl der R-Konten, die durch gestartet werden können [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], finden Sie unter [Ändern des benutzerkontenpools für Machine Learning](modify-the-user-account-pool-for-sql-server-r-services.md).

Wenn Sie verfügen nicht über die Ressourcenkontrolle und Standard Edition verwenden, können Sie dynamische Verwaltungssichten (DMVs) und erweiterte Ereignisse als auch Windows-Ereignis überwachen, um die Verwaltung von Serverressourcen, die von r verwendet werden Weitere Informationen finden Sie unter [überwachen und Verwalten von R Services](managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Installieren Sie zusätzliche R-Pakete

Nehmen Sie zusätzliche R-Pakete installieren, die Sie verwenden.

Pakete, die Sie von SQL Server verwenden möchten, müssen in der Standardbibliothek installiert sein, die von der Instanz verwendet wird. Wenn Sie eine separate Installation von R auf dem Computer oder bei Installation von Paketen in benutzerbibliotheken nicht auf diese Pakete von T-SQL verwenden kann.

In SQL Server 2016 und SQL Server-2017 unterscheidet sich die Verfahren zum Installieren und Verwalten von R-Pakete. Z. B. in SQL Server-2017, können Sie Benutzergruppen zur Freigabe von Paketen auf einer Ebene pro Datenbank einrichten oder konfigurieren Datenbankrollen, damit Benutzer ihre eigenen Pakete installieren können. Weitere Informationen finden Sie unter [Paket Management](r-package-management-for-sql-server-r-services.md).

In SQL Server 2016 muss ein Datenbankadministrator R-Pakete installieren, die Benutzer benötigen.

Administratorzugriff ist auch erforderlich, um zusätzliche Python-Pakete in der Bibliothek für die Instanz zu installieren.

### <a name="upgrade-the-machine-learning-components"></a>Aktualisieren Sie den Computer mit dem Erlernen von Komponenten

Wenn Sie Machine Learning-Funktionen in SQL Server installieren, erhalten Sie die Version der R oder Python-Komponenten, die aktuelle war, als die Version oder Service Pack veröffentlicht wurde. Jedes Mal gepatcht oder aktualisieren Sie den Server werden auch die Machine Learning-Komponenten aktualisiert werden.

Allerdings können Sie Machine learning-Komponenten auf einen schnelleren Zeitplan unterstützt Aktualisieren von SQL Server-Versionen mithilfe der genannten _Bindung_. Wenn Sie eine SQL Server-Instanz binden, Sie sowohl R oder Python-Versionen aktualisieren, und ändern Sie in einer anderen Support-Richtlinie, die häufiger Upgrades unterstützt. 

Solche Upgrades können Folgendes umfassen:

* Neue R-Pakete
+ Neue APIs für Microsoft Pakete wie [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).
* [Modelle pretrained](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) für bildanalysen Klassifizierung und Text.

Informationen zum upgrade von SQL Server-Instanz finden Sie unter [Aktualisieren des Machine Learning-Komponenten über Bindung](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).


### <a name="tutorials"></a>Lernprogramme

Zum Einstieg in einige einfache Beispiele, und die Grundlagen der Funktionsweise von R mit SQL Server, finden Sie unter [mithilfe von R-Code in Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Beispiele für Machine Learning, reale Szenarien basieren, finden Sie unter [Machine learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md).

### <a name="troubleshooting"></a>Problembehandlung

Sind Probleme aufgetreten? Möchten Sie aktualisieren? Antworten auf häufig gestellte Fragen und bekannte Probleme finden Sie im folgenden Artikel:

* [Upgrade und Installation häufig gestellte Fragen – Machine Learning-Dienste](upgrade-and-installation-faq-sql-server-r-services.md)

Überprüfen Sie den Installationsstatus der Instanz, und beheben Probleme, wiederholen Sie dann diese benutzerdefinierten Berichte.

* [Benutzerdefinierte Berichte für SQL Server R Services](\r\monitor-r-services-using-custom-reports-in-management-studio.md)
