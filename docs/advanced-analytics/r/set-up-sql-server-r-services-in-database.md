---
title: Einrichten von SQL Server Machine Learning-Services (Datenbankintern) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- Installieren von SQL Server R Services
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: f0065068d53517626c7157c9be884549573ae08b
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="set-up-sql-server-machine-learning-services-in-database"></a>Einrichten von SQL Server Machine Learning-Services (Datenbankintern)

In diesem Thema wird beschrieben, wie zum Einrichten von Machine Learning Services in SQL Server mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup-Assistenten.

**Gilt für:** SQL Server 2016-R Services (nur R) SQL Server 2017 Machine Learning Services (R und Python)

## <a name="machine-learning-options-in-sql-server-setup"></a>Machine learning-Optionen in SQL Server-setup

SQL Server-Setup bietet die folgenden Optionen für die Installation von Machine Learning:

* Installieren von Machine Learning mit SQL Server-Datenbank

  Diese Option können Sie R oder Python-Skripts ausführen, mit einer gespeicherten Prozedur. Auch können der SQL Server-Computer als remote computekontext für R oder Python-Skripts, die aus einer externen Verbindung ausgeführt werden.

  So installieren Sie diese Option aus:
  
  * Wählen Sie in SQL Server 2016 **R Services (Datenbankintern)**.
  * Wählen Sie in SQL Server 2017 **Machine Learning-Services (Datenbankintern)**.


* Installieren Sie einen eigenständigen Machine Learning-server

  Diese Option wird eine Entwicklungsumgebung für Machine learning-Lösungen, die nicht erfordern, oder verwenden Sie SQL Server erstellt. Aus diesem Grund empfehlen wir in der Regel, dass Sie diese Option auf einem anderen Computer als eine SQL-Hostserver installieren. Weitere Informationen zu dieser Option finden Sie unter [erstellen a Standalone R Server](../r/create-a-standalone-r-server.md).

Der Installationsvorgang erfordert mehrere Schritte, von die einige optional sind. Die optionale Aspekte hängen sowohl Verwendungsweise von Machine Learning und den Status Ihrer Umgebung Sicherheit verwenden. 

## <a name="bkmk_prereqs"></a> Erforderliche Komponenten

*  Installation von R-Server und R-Dienste zur gleichen Zeit zu vermeiden. Sie würden normalerweise R Server (eigenständig) zum Erstellen einer Umgebung, die ein datenanalyst oder Entwickler verwendet werden, die Verbindung mit SQL Server installieren und Bereitstellen von R-Lösungen. Daher besteht keine Notwendigkeit beide auf demselben Computer zu installieren.

* Wenn Sie alle vorherigen Versionen von Revolution Analytics-Entwicklungsumgebung oder dem "revoscaler"-Pakete verwendet oder wenn Sie alle Vorabversionen von SQL Server 2016 installiert haben, müssen Sie sie deinstallieren. Seite-an-Seite-Installation wird nicht unterstützt. Hilfe zum Entfernen früherer Versionen finden Sie [Upgrade und Installation – häufig gestellte Fragen für SQL Server R Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

* Sie können keine Machine Learning-Dienste auf einem Failovercluster installieren. Der Grund ist, der Sicherheitsmechanismus, der verwendet wird, zur Isolierung von externen Skriptprozesse nicht mit einer Windows Server Failover Cluster-Umgebung kompatibel ist. Dieses Problem zu umgehen können Sie eine der folgenden Aktionen ausführen:
    * Mithilfe der Replikation um erforderlichen Tabellen in eine eigenständige SQL Server-Instanz mit R Services zu kopieren.
    * Installieren Sie [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] auf einem eigenständigen Computer, die AlwaysOn verwendet und ist Teil einer verfügbarkeitsgruppe.

> [!IMPORTANT]
> Nachdem Setup abgeschlossen ist, sind einige zusätzliche Schritte erforderlich, um Machine learning-Funktion zu aktivieren. Sie können auch müssen gewähren Sie Benutzerberechtigungen für bestimmte Datenbanken ändern Konten konfigurieren oder Einrichten einer remote Data Science-Client.

##  <a name="bkmk_installExt"></a>Schritt 1: Installieren Sie die Erweiterbarkeitsfunktionen, und wählen Sie ein Machine learning-Sprache

Um Machine Learning verwenden zu können, müssen Sie SQLServer 2016 oder höher installieren. Mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], mindestens eine Instanz des Datenbankmoduls ist erforderlich. Sie können entweder eine Standardinstanz oder eine benannten Instanz verwenden.

1. Führen Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup aus.
  
    Informationen dazu, wie Sie unbeaufsichtigte Installationen finden Sie unter [unbeaufsichtigt installiert SQL Server R Services](../r/unattended-installs-of-sql-server-r-services.md).
  
2. Auf der **Installation** Registerkarte **eigenständige neue SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.
   
3. Auf der **Funktionsauswahl** Seite, um die Dienste der Datenbank verwendet werden, indem Sie R Installieren von Aufträgen und installiert die Erweiterungen, die externe Skripts und Prozesse zu unterstützen, wählen Sie die folgenden Optionen:
   
   **SQL Server 2016**
   - Wählen Sie **Datenbankmoduldienste**.
   - Wählen Sie **R Services (Datenbankintern)**.

   **SQL Server 2017**
   - Wählen Sie **Datenbankmoduldienste**.
   - Wählen Sie **Machine Learning-Services (Datenbankintern)**.
   - Wählen Sie mindestens ein Machine learning-Sprache zu aktivieren. Sie können nur R auswählen oder können Sie R und Python hinzufügen.
   
   > [!NOTE]
   > Wenn Sie nicht die R- oder Python Sprachoptionen auswählen, der Setup-Assistent installiert nur die Erweiterbarkeitsframework, einschließlich SQL Server vertrauenswürdige Launchpad jedoch sprachspezifische Komponenten nicht installiert ist. Diese Option ist für die R oder Python SQL Server-Instanz als Teil der Microsoft moderne Lifecycle-Richtlinie Bindung. Weitere Informationen finden Sie unter [verwenden SqlBindR zum Aktualisieren einer Instanz des R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

4.  Auf der **stimmen Sie installiert Microsoft R Open** Seite **Accept**.
  
     Die Lizenzbedingungen ist erforderlich, um Microsoft R Open, die eine Verteilung der open Source-R-Basispakete und Tools, zusammen mit erweiterten R-Paketen und Konnektivitätsanbietern von Microsoft R-Entwicklungsteam umfasst herunterladen.
  
    > [!NOTE]
    >  Wenn der Computer, die Sie verwenden keinen Zugriff auf das Internet, Sie können Setup an diesem Punkt, um die Installationsprogramme getrennt, wie in beschrieben herunterladen anhalten [Installieren von R-Komponenten ohne Internetzugang](installing-ml-components-without-internet-access.md).
  
5. Wählen Sie **Weiter**aus.

6. Auf der **Installationsbereit** Seite, stellen Sie sicher, dass die folgenden Elemente enthalten sind, und Sie dann wählen **installieren**.

   **SQL Server 2016**
   - Datenbankmoduldienste
   - R Services (In-Database)

   **SQL Server 2017**
   - Datenbankmoduldienste
   - Machine Learning-Dienste (datenbankintern)
   - R, Python oder beides
    
7. Wenn die Installation abgeschlossen ist, starten Sie den Computer neu.

##  <a name="bkmk_enableFeature"></a>Schritt 2: Aktivieren von externen Skripts services

1. Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Wenn diese Anwendung noch nicht installiert ist, können Sie den Setup-Assistenten für SQL Server erneut ausführen, um einen Link zum Herunterladen zu öffnen und die Anwendung zu installieren.
  
2. Herstellen einer Verbindung mit der Instanz, auf dem Machine Learning installiert, und führen Sie den folgenden Befehl aus:

   ```SQL
   sp_configure
   ```

    Der Wert für die **externe Skripts aktiviert** Eigenschaft sollte jetzt **0**. Grund hierfür das Feature ist standardmäßig deaktiviert, um die Angriffsfläche zu verringern und muss explizit von einem Administrator aktiviert ist.
     
3. Um die externe Skriptingfunktion zu aktivieren, führen Sie die folgende Anweisung aus:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
4. Starten Sie den SQL Server-Dienst für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz. Startet den zugehörigen neu auch automatischer Neustart des SQL Server-Diensts [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst.

    Sie können den Dienst neu starten, mit der **Services** Bereich in der Systemsteuerung oder mithilfe von SQL Server-Konfigurations-Manager.

## <a name="bkmk_TestScript"></a>Schritt 3: Stellen Sie sicher, dass die Ausführung des Skripts lokal funktioniert

Stellen Sie sicher, dass die Ausführung externer Skripts-Dienst aktiviert ist.

1. In SQL Server Management Studio, öffnen Sie ein neues **Abfrage** Fenster, und führen Sie den folgenden Befehl aus:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```
    Der Wert **Run_value** sollte jetzt auf 1 festgelegt werden.
    
2. Öffnen der **Services** Bereich, und stellen Sie sicher, dass das Launchpad-Dienst für die Instanz ausgeführt wird. Wenn Sie mehrere Instanzen installieren, verfügt jede Instanz über einen eigenen Launchpad-Dienst.
   
3. Öffnen Sie ein neues **Abfrage** Fenster in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und führen Sie ein einfaches R-Skript, z. B. die folgenden:
  
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```
  
    **Ergebnisse**
  
    *Hello* *1*
  
   Wenn der Befehl ohne Fehler ausgeführt wird, fahren Sie mit den nächsten Schritten. Wenn Sie eine Liste der einige allgemeine Probleme einen Fehler erhalten, finden Sie unter [häufig gestellte Fragen zu Upgrade und Installation](../r/upgrade-and-installation-faq-sql-server-r-services.md).

## <a name="bkmk_FollowUp"></a>Schritt 4: Zusätzliche Konfiguration

Je nach Ihrer Anwendungsfall für R oder Python müssen Sie zusätzliche Änderungen vornehmen, auf dem Server, die Firewall, den Dienst bzw. die Datenbankberechtigungen verwendeten Konten. Die Änderungen, die Sie vornehmen müssen, variieren nach Groß-/Kleinschreibung.

Allgemeine Szenarien, die zusätzliche Änderungen erfordern:

* Ändern die Firewallregeln für eingehende Verbindungen zu SQL Server zu ermöglichen.
* Aktivieren von zusätzlichen Netzwerkprotokollen.
* Sicherstellen, dass der Server Remoteverbindungen unterstützt.
* Aktivieren der *implizite Authentifizierung*, wenn Benutzer Zugriff auf SQL Server-Daten von einem Remotecomputer aus terminal R zum Entwickeln und Ausführen von R-Code mithilfe des RODBC-Pakets oder andere Anbieter von Microsoft Open Database Connectivity (ODBC).
* Erteilen Benutzerberechtigungen zum Ausführen von R-Skript oder Datenbanken verwenden.
* Beheben von Sicherheitsproblemen, die Kommunikation mit dem Launchpad-Dienst zu verhindern.
* Sicherstellen, dass Benutzer über die Berechtigung zum Ausführen von R-Code oder Pakete installieren.

> [!NOTE]
> Nicht alle aufgelisteten Änderungen können erforderlich sein. Allerdings wird empfohlen, dass Sie überprüfen, dass alle Elemente, um festzustellen, ob sie für Ihr Szenario anwendbar sind.

### <a name="bkmk_configureAccounts"></a>Aktivieren Sie die implizite Authentifizierung für die Kontogruppe Launchpad

Während des Setups werden einige neue Windows-Benutzerkonten zum Ausführen von Aufgaben unter des Sicherheitstokens des erstellt die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Dienst. Wenn ein Benutzer ein R-Skript von einem externen Client sendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktiviert ein Konto Arbeitsthreads verfügbar, wird es auf die Identität des aufrufenden Benutzers zugeordnet und führt das R-Skript im Namen des Benutzers. Dieser neue Dienst des Datenbankmoduls unterstützt die sichere Ausführung externer Skripts, die aufgerufen *implizite Authentifizierung*.

Sie können diese Konten anzeigen, in der Windows-Benutzergruppe **SQLRUserGroup**. Standardmäßig werden 20 Konten erstellt, ist in der Regel mehr als ausreichend, für die Ausführung von R-Aufträge.

Jedoch, wenn Sie, führen Sie R-Skripts von einem remote Data Science-Client möchten und Windows-Authentifizierung verwenden, Sie müssen erteilen diese Konten über die Berechtigung zum Anmelden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz in Ihrem Namen.

1. Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Objekt-Explorer den Knoten **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Anmeldungen**, und wählen Sie anschließend **Neue Anmeldung**.
2. In der **Anmeldung - neu** wählen Sie im Dialogfeld **Suche**.
3. Wählen Sie die **Objekttypen** und **Gruppen** Kontrollkästchen, und deaktivieren Sie alle anderen Kontrollkästchen. 
4. In **Geben Sie die zu verwendenden Objektnamen**, Typ **SQLRUserGroup**, und wählen Sie dann **Namen überprüfen**.  
    Der Name der lokalen Gruppe, dem die Instanz Launchpad-Dienst zugeordnet sind, sollte sich in etwa auflösen *Instancename\SQLRUserGroup*. 
5. Wählen Sie **OK**.
6. In der Standardeinstellung ist die Anmeldung der **öffentlichen** Rolle zugewiesen und verfügt über die Berechtigung, eine Verbindung zum Datenbankmodul herzustellen.
7. Wählen Sie **OK**.

### <a name="bkmk_AllowLogon"></a>Vergabe von Benutzerberechtigungen für das Ausführen externer Skripts.

> [!NOTE]
> Wenn Sie eine SQL-Anmeldung für die Ausführung von R-Skripts in einer SQL Server-computekontext verwenden, ist dieser Schritt nicht erforderlich.

Wenn Sie installiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und R-Skripts in eine eigene Instanz ausgeführt werden, sind in der Regel das Ausführen von Skripts als Administrator, oder zumindest ein Datenbankbesitzer und daher verfügen über implizite Berechtigungen für verschiedene Vorgänge, werden alle Daten in der Datenbank und die Möglichkeit zum Installieren der neuen R-Pakete als erforderlich.

Allerdings müssen in einem Enterprise-Szenario können die meisten Benutzer, einschließlich Benutzer, die Zugriff auf die Datenbank mithilfe von SQL-Anmeldungen, diese erhöhten Berechtigungen keine. Aus diesem Grund müssen für jeden Benutzer, die R oder Python-Skripts ausgeführt werden, Sie erteilen die Benutzerberechtigungen zum Ausführen von Skripts in jeder Datenbank, in der externen Skripts verwendet werden.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> Benötigen Sie Hilfe beim Setup? Sind Sie unsicher, ob Sie alle Schritte ausgeführt haben? Verwenden Sie diese benutzerdefinierten Berichte, um den Installationsstatus von R Services zu überprüfen. Weitere Informationen finden Sie unter [Überwachung von R Services mithilfe von benutzerdefinierten Berichten](monitor-r-services-using-custom-reports-in-management-studio.md).

### <a name="ensure-that-the-sql-server-computer-supports-remote-connections"></a>Stellen Sie sicher, dass der Computer mit SQL Server Remoteverbindungen unterstützt

Wenn Sie von einem Remotecomputer herstellen können, überprüfen Sie, ob der Server Remoteverbindungen zulässt. Remoteverbindungen werden manchmal standardmäßig deaktiviert.

Überprüfen Sie außerdem, um festzustellen, ob die Firewall den Zugriff auf SQL Server zulässt. Standardmäßig ist der von SQL Server verwendete Port häufig durch die Firewall blockiert. Wenn Sie die Windows-Firewall verwenden, finden Sie unter [Konfigurieren der Windows-Firewall für Datenbankmodulzugriff](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).

### <a name="give-your-users-read-write-or-ddl-permissions-to-the-database"></a>Geben Sie Ihre Benutzer zu lesen, schreiben oder DDL-Berechtigungen für die Datenbank

Während der Ausführung R-Skripts, das entsprechende Benutzerkonto oder SQL-Anmeldung möglicherweise müssen zum Lesen von Daten von anderen Datenbanken, Erstellen von neuen Tabellen zum Speichern von Ergebnissen, und Schreiben von Daten in Tabellen.

Für jedes Benutzerkonto oder SQL-Anmeldung, die R-Skripts ausführen, achten Sie darauf, dass das Konto oder den Anmeldenamen für die Datenbank die entsprechenden Berechtigungen verfügt: *"db_datareader"*, *Db_datawriter*, oder  *Db_ddladmin*.

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

Nachdem Sie sichergestellt haben, dass das Feature für die Ausführung von Skripts in SQL Server funktioniert, können Sie R und Python-Befehle ausführen, von SQL Server Management Studio, Visual Studio-Code oder einem anderen Client, der T-SQL-Anweisungen an den Server gesendet werden kann.

Sie möchten jedoch nehmen einige Änderungen an der Systemkonfiguration, zur Unterstützung einer starke Nutzung von Machine Learning, oder fügen neue R-Pakete.

Dieser Abschnitt enthält einige allgemeine Änderungen, die Sie vornehmen können, um Machine Learning unterstützt.

### <a name="add-more-worker-accounts"></a>Weitere Konten hinzufügen

Wenn Sie glauben, dass R intensivsten verwendet werden kann oder wenn Sie davon ausgehen, dass viele Benutzer gleichzeitig ausgeführte Skripts werden, können Sie die Anzahl der Worker Konten erhöhen, die mit dem Launchpad-Dienst zugewiesen sind. Weitere Informationen finden Sie unter [Ändern des benutzerkontenpools für SQL Server R Services](modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="bkmk_optimize"></a>Optimieren des Servers für den externen skriptausführung

Die Standardeinstellungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup das Gleichgewicht des Servers für eine Vielzahl von Diensten zu verbessern, die vom Datenbankmodul, extrahieren, Transformieren und laden (ETL) Prozesse, Berichts-, Überwachung, enthalten möglicherweise unterstützt werden sollen und Anwendungen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten. In den Standardeinstellungen finden Sie möglicherweise daher, dass Ressourcen für Machine Learning sind manchmal eingeschränkt oder, insbesondere in arbeitsspeicherintensive Vorgänge gedrosselt.

Um sicherzustellen, dass die Machine Learning Aufträge priorisiert und Ressourcen entsprechend zugewiesen sind, wird empfohlen, dass Sie SQL Server-Ressourcenkontrolle verwenden, um einen externen Ressourcenpool zu konfigurieren. Sie möchten möglicherweise auch die Größe des Arbeitsspeichers zu ändern, die zugeordnet ist, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmodul, oder erhöhen Sie die Anzahl der Konten, die unter ausgeführt der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst.

- Um einen Ressourcenpool für die Verwaltung von externen Ressourcen zu konfigurieren, finden Sie unter [erstellen Sie einen externen Ressourcenpool](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Um die reservierten Umfang an Arbeitsspeicher für die Datenbank zu ändern, finden Sie unter [Server Speicherkonfigurationsoptionen](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- So ändern Sie die Anzahl der R-Konten, die durch gestartet werden können [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], finden Sie unter [Ändern des benutzerkontenpools für Machine Learning](modify-the-user-account-pool-for-sql-server-r-services.md).

Wenn Sie verfügen nicht über die Ressourcenkontrolle und Standard Edition verwenden, können Sie dynamische Verwaltungssichten (DMVs) und erweiterte Ereignisse als auch Windows-Ereignis überwachen, um die Verwaltung von Serverressourcen, die von r verwendet werden Weitere Informationen finden Sie unter [überwachen und Verwalten von R Services](managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Installieren Sie zusätzliche R-Pakete

Nehmen Sie zusätzliche R-Pakete installieren, die Sie verwenden.

Pakete, die Sie von SQL Server verwenden möchten, müssen in der Standardbibliothek installiert sein, die von der Instanz verwendet wird. Wenn Sie eine separate Installation von R auf dem Computer oder bei Installation von Paketen in benutzerbibliotheken nicht auf diese Pakete von T-SQL verwenden kann. Weitere Informationen finden Sie unter [Installieren zusätzlicher R-Pakete unter SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).

Sie können auch Benutzergruppen zur Freigabe von Paketen auf einer pro-Datenbankebene einrichten oder Konfigurieren von Datenbankrollen, damit Benutzer ihre eigenen Pakete installieren können. Weitere Informationen finden Sie unter [Paket Management](r-package-management-for-sql-server-r-services.md).

### <a name="upgrade-the-machine-learning-components"></a>Aktualisieren Sie den Computer mit dem Erlernen von Komponenten

Wenn Sie R-Services, die Verwendung von SQL Server 2016 installieren, erhalten Sie die Version der R-Komponenten, die auf dem neuesten Stand war, als die Version oder Service Pack veröffentlicht wurde. Jedes Mal gepatcht oder aktualisieren Sie den Server werden auch die Machine Learning-Komponenten aktualisiert werden.

Allerdings können Sie Machine learning-Komponenten auf einen schnelleren Zeitplan unterstützt Aktualisieren von SQL Server-Versionen von Microsoft R Server installieren und binden die Instanz. Wenn Sie ein Upgrade durchführen, finden Sie auch die folgenden neuen Features, die in neueren Versionen von Microsoft R Server unterstützt werden:

* Neue R-Pakete, einschließlich [Sqlrutils](https://docs.microsoft.com/r-server/r-reference/sqlrutils/sqlrutils), [OlapR](https://docs.microsoft.com/r-server/r-reference/olapr/olapr), und [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).
* [Modelle pretrained](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) für bildanalysen Klassifizierung und Text.

Informationen zum upgrade von einer SQL Server 2016-Instanz finden Sie unter [Upgrade R-Komponenten über Bindung](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

Wenn Sie nicht sicher sind, welche Version von R mit der Instanz verknüpft ist, können Sie einen Befehl wie folgt ausführen:

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'
myvar <- version$version.string
OutputDataSet <- as.data.frame(myvar);'
```

> [!NOTE]
> Upgrades über des Bindungsvorgangs werden auch für SQL Server-2017 unterstützt. Upgrades werden zurzeit jedoch nur für SQL Server 2016-Instanzen unterstützt.

### <a name="tutorials"></a>Lernprogramme

Zum Einstieg in einige einfache Beispiele, und die Grundlagen der Funktionsweise von R mit SQL Server, finden Sie unter [mithilfe von R-Code in Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Beispiele für Machine Learning, reale Szenarien basieren, finden Sie unter [Machine learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md).

### <a name="troubleshooting"></a>Problembehandlung

Sind Probleme aufgetreten? Möchten Sie aktualisieren? Antworten auf häufig gestellte Fragen und bekannte Probleme finden Sie im folgenden Artikel:

* [Upgrade und Installation häufig gestellte Fragen – Machine Learning-Dienste](upgrade-and-installation-faq-sql-server-r-services.md)

Überprüfen Sie den Installationsstatus der Instanz, und beheben Probleme, wiederholen Sie dann diese benutzerdefinierten Berichte.

* [Benutzerdefinierte Berichte für SQL Server R Services](monitor-r-services-using-custom-reports-in-management-studio.md)

