---
title: "Einrichtung und Konfiguration für Python Machine Learning-Dienste | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: bc9cfe7bf885c99ccfe487e10e001ff36f68ee86
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="set-up-python-machine-learning-services-in-database"></a>Einrichten von Python Machine Learning-Services (Datenbankintern)

  Sie installieren die erforderlichen Komponenten für Python durch Ausführen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup-Assistenten und den interaktiven Anweisungen folgen, wie in diesem Thema beschrieben.

## <a name="machine-learning-options-in-sql-server-setup"></a>Machine learning-Optionen in SQL Server-setup

Wählen Sie die **Machine Learning Services** gelten, und wählen Sie **Python** als Sprache.

Die **gemeinsam genutzte Funktionen** Abschnitt enthält eine separate Installationsoption **Machine Learning-Server (eigenständig)**. Diese Option unterstützt operationalisierung von Python-Code auf einem Server, die keine SQL Server oder erfordert, die keine Verwendung von SQL Server-rechenkontexte. Es wird daher empfohlen, die Sie *nicht* installieren Sie diese auf demselben Computer wie SQL Server-Instanz. Installieren Sie stattdessen die Machine Learning-Server (eigenständig) auf einem separaten Computer.

Nachdem die Installation abgeschlossen ist, konfigurieren, dass die Instanz, um die Ausführung von Skripts zu ermöglichen, die eine externe ausführbare Datei verwenden. Sie müssen möglicherweise zusätzliche Änderungen vornehmen, mit dem Server um Machine Learning-arbeitsauslastungen zu unterstützen. Konfigurationsänderungen muss in der Regel ein Neustart der Instanz oder einen Neustart des Launchpad-Diensts.

### <a name="prerequisites"></a>Erforderliche Komponenten

+ SQL Server-2017 ist erforderlich. Python-Integration wird auf früheren Versionen von SQL Server nicht unterstützt.
+ Achten Sie darauf, dass das Datenbankmodul installiert werden. Eine Instanz von SQL Server wird zum Ausführen von Python-Skripts in der Datenbank erforderlich.
+ Erforderliche Komponenten werden als Teil des Setups der Python-Komponente installiert.
+ Sie können keine Machine Learning mit Python-Dienste auf einem Failovercluster installieren. Zum Isolieren von Python-Prozesse Sicherheitsmechanismus ist nicht kompatibel mit einer Windows Server Failover Cluster-Umgebung.
   
  Dieses Problem zu umgehen können Sie die Replikation verwenden, so kopieren Sie die erforderlichen Tabellen in eine eigenständige SQL Server-Instanz, die Python-Dienste verwendet. Alternativ können Sie Machine Learning mit Python-Diensten auf einem eigenständigen Computer installieren, die die AlwaysOn-Einstellung verwendet und ist Teil einer verfügbarkeitsgruppe.

+ Seite-an-Seite-Installation mit anderen Versionen von Python ist möglich, da SQL Server-Instanz eine eigene Kopie der Anaconda-Verteilung verwendet wird. Ausführen von Code, der Python auf dem SQL Server-Computer außerhalb von SQL Server verwendet, kann jedoch zu verschiedenen Problemen führen:
    + Sie verwenden eine andere Bibliothek und andere ausführbare Datei, und unterschiedliche Ergebnisse erhalten, als Sie ausführen, wenn Sie in SQL Server ausgeführt werden.
    + Python-Skripts, die auf externen Bibliotheken können von SQL Server, um Ressourcenkonflikte führende verwaltet werden.
  
> [!IMPORTANT]
> Nachdem Setup abgeschlossen ist, achten Sie darauf, dass Sie zusätzliche nach der Konfiguration in diesem Thema beschriebenen Schritte. Dazu gehören das Aktivieren von SQL Server, um externe Skripts zu verwenden und das Hinzufügen von Konten für SQL Server zum Ausführen von Python-Aufträgen in Ihrem Namen erforderlich sind.

### <a name="unattended-installation"></a>Für die unbeaufsichtigte installation

Zum Ausführen einer unbeaufsichtigten Installations verwenden Sie die Befehlszeilenoptionen für SQL Server-Setup und die Argumente, die spezifisch für Python. Weitere Informationen finden Sie unter [unbeaufsichtigt installiert SQL Server mit Python Machine Learning Services](unattended-installs-of-sql-server-python-services.md).

##  <a name="bkmk_installPythonInDatabase"></a>Schritt 1: Installieren von Machine Learning-Dienste (In-Database) auf dem SQLServer

1. Führen Sie den Setup-Assistenten für SQL Server-2017.
  
2. Auf der **Installation** Registerkarte **eigenständige neue SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.

    ![Installieren Sie Python in Datenbank](media/2017setup-installation-page-mlsvcs.PNG)
   
3. Wählen Sie diese Optionen auf der Seite **Funktionsauswahl** aus:
  
    -   **Datenbankmoduldienste**
  
         Um Python mit SQL Server verwenden, müssen Sie eine Instanz des Datenbankmoduls installieren. Sie können entweder eine Standardinstanz oder eine benannte Instanz verwenden.
  
    -   **Machine Learning-Services (Datenbankintern)**
  
         Diese Option installiert die Datenbankdienste, die Ausführung von Python-Skripts zu unterstützen.

    -   **Python** überprüfen Sie diese Option, um die Python-3.5 ausführbare Datei und wählt Bibliotheken aus Anaconda-Verteilung. Installieren Sie nur eine Sprache pro Instanz.
        
        ![Optionen für Python Feature](media/ml-svcs-features-python-highlight.png "Setup-Optionen für Python")

        > [!NOTE]
        > 
        > Wählen Sie die Option für nicht **Machine Learning-Server (eigenständig)**. Die Option zum Installieren von Machine Learning-Server unter **gemeinsam genutzte Funktionen** dient zur Verwendung auf einem separaten Computer. Sie möchten z. B. die gleiche Version des Machine learning-Komponenten auf einem anderen Computer für die Projektentwicklung, z. B. die Datenanalysten Laptop verwendeten installieren.

4. Auf der **Zustimmung zum Installieren von Python** Seite **Accept**.
  
     Die Lizenzbedingungen ist erforderlich, um die ausführbaren Python Python-Pakete aus Anaconda herunterzuladen.
     
     ![Vereinbarung für den Python-Lizenz](media/ml-svcs-license-python.png "-Lizenzvertrag für Python")
  
    > [!NOTE]
    >  Wenn der Computer, den Sie verwenden nicht über Internetzugriff verfügt, können Sie Setup aus, an diesem Punkt, um die Installationsprogramme getrennt herunterladen anhalten. Weitere Informationen finden Sie unter [Komponenten ohne Internetzugang installieren](../r/installing-ml-components-without-internet-access.md).
  
     Wählen Sie **Accept**, warten Sie, bis die **Weiter** wird aktiv, und wählen Sie dann die Schaltfläche **Weiter**.
  
5. Auf der **Installationsbereit** Seite, stellen Sie sicher, dass diese Auswahl enthalten ist, und wählen Sie **installieren**.
  
     + Datenbankmoduldienste
     + Machine Learning-Dienste (datenbankintern)
     + Python
  
    Diese Auswahl darstellen die Mindestkonfiguration erforderlich, um das Verwenden von Python mit [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)].
    
    ![Bereit zum Installieren von Python](media/ready-to-install-python.png "erforderliche Komponenten für die Python-Installation")

    Optional, notieren Sie sich den Speicherort des Ordners, unter dem Pfad `..\Setup Bootstrap\Log` , in dem die Konfigurationsdateien gespeichert werden. Wenn Setup abgeschlossen ist, können Sie die installierten Komponenten in der Statusdatei überprüfen.

6. Nach Abschluss der Installation starten Sie den Computer neu.

##  <a name="bkmk_enableFeature"></a>Schritt 2: Ausführen von Python-Skripts zu aktivieren

1. Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Wenn es nicht bereits installiert ist, können Sie den SQL Server-Setup-Assistenten erneut aus, um ein Downloadlink zu öffnen, und installieren Sie es ausführen.
  
2. Herstellen einer Verbindung mit der Instanz, auf dem Machine Learning-Dienste installiert, und führen Sie den folgenden Befehl aus:

   ```SQL
   sp_configure
   ```

    Der Wert für die Eigenschaft `external scripts enabled` sollte an diesem Punkt **0** betragen. Grund hierfür ist die Funktion standardmäßig deaktiviert ist. Die Funktion muss explizit von einem Administrator aktiviert werden, bevor R oder Python-Skripts ausgeführt werden können.
    
3.  Führen Sie die folgende Anweisung aus, um externe Skriptingfunktion aktivieren, das Python unterstützt:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    Wenn Sie bereits die Funktion für die Sprache "R" aktiviert haben, müssen Sie nicht ausführen ein zweites Mal für Python neu konfigurieren. Die zugrunde liegende Erweiterbarkeitsplattform unterstützt beide Sprachen.

4. Starten Sie den SQL Server-Dienst für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz. Startet den zugehörigen neu auch automatischer Neustart des SQL Server-Diensts [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst.

    Sie können den Dienst neu starten, mit der **Services** Bereich in der Systemsteuerung oder mithilfe von [SQL Server-Konfigurations-Manager](../../relational-databases/sql-server-configuration-manager.md).

## <a name="step-3-verify-that-the-external-script-execution-feature-is-running"></a>Schritt 3: Stellen Sie sicher, dass der externe Ausführung Skriptfunktion ausgeführt wird

Nehmen Sie einen Moment Zeit, um sicherzustellen, dass alle Komponenten, die mit dem Python-Skript gestartet ausgeführt werden.

1. Öffnen Sie in SQL Server Management Studio ein neues Abfragefenster, und führen Sie den folgenden Befehl:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    Der Wert **Run_value** sollte jetzt auf 1 festgelegt werden.
    
2. Öffnen der **Services** Systemsteuerung oder mithilfe von SQL Server-Konfigurations-Manager, und stellen Sie sicher, dass das Launchpad-Dienst für die Instanz ausgeführt wird. Wenn Sie das Launchpad nicht ausgeführt wird, starten Sie den Dienst an.
  
    Wenn Sie mehrere Instanzen von SQL Server installiert haben, hat jeder Instanz, die entweder R oder Python aktiviert hat eigene Launchpad-Dienst.

    Bei der Installation von R und Python auf eine Einzelinstanz wird nur ein Launchpad installiert. Eine separate, sprachspezifische Startprogramm DLL wird für jede Sprache hinzugefügt. Weitere Informationen finden Sie unter [Komponenten zur Unterstützung der Integration von Python](new-components-in-sql-server-to-support-python-integration.md). 
   
3. Wenn Launchpad ausgeführt wird, sollten Sie wie folgt in einfache Python-Skripts ausgeführt werden [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'OutputDataSet = InputDataSet',
    @input_data_1 = N'SELECT 1 AS col'
    ```
    
    **Ergebnisse**
    
    *<code>&nbsp;&nbsp;</code>* *1*

> [!NOTE]
> Spalten oder Überschriften im Python-Skript verwendet, werden nicht, entwurfsbedingt zurückgegeben. Um die Spaltennamen für Ihre Ausgabe hinzufügen, müssen Sie das Schema für die zurückgegebenen Daten Menge angeben. Dies erfolgt mithilfe des Parameters mit der Ergebnisse der gespeicherten Prozedur, benennen die Spalten und Angeben des SQL-Datentyps.
> 
> Beispielsweise können Sie die folgende Zeile zum Generieren von einer beliebigen Spaltenname hinzufügen:`WITH RESULT SETS ((Col1 AS int))`

## <a name="step-4-additional-configuration"></a>Schritt 4: Zusätzliche Konfiguration

Wenn der vorherige Befehl erfolgreich war, können Sie die Python-Befehle ausführen, von SQL Server Management Studio, Visual Studio-Code oder einem anderen Client, der T-SQL-Anweisungen an den Server gesendet werden kann.

Wenn Sie einen Fehler beim Ausführen des Befehls erhalten haben, überprüfen Sie in der folgenden Liste. Sie müssen möglicherweise zusätzliche entsprechende Konfigurationen an den Dienst oder einer Datenbank vornehmen.

> [!NOTE]
> 
> Nicht alle aufgelisteten Änderungen erforderlich sind, und keine u. u. notwendig sein. Anforderungen richten sich nach Ihrem Sicherheitsschema, in dem Sie installiert SQL Server, und wie Sie erwarten, dass Benutzer eine Verbindung mit der Datenbank und externe Skripts ausführen.

###  <a name="bkmk_configureAccounts"></a>Aktivieren Sie die implizite Authentifizierung für die Kontogruppe Launchpad

Beim Setup werden eine Anzahl neuer Windows-Benutzerkonten angelegt, um Aufgaben unter dem Sicherheitstoken des [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]-Dienstes ausführen zu können. Wenn ein Benutzer ein Python oder R-Skript von einem externen Client sendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktiviert ein Konto Arbeitsthreads verfügbar. Anschließend ordnet er die Identität des aufrufenden Benutzers und führt das Skript im Namen des Benutzers.

Hierbei spricht *implizite Authentifizierung*, und ist ein Dienst des Datenbankmoduls. Dieser Dienst unterstützt die sichere Ausführung externer Skripts in SQL Server 2016 und SQL Server-2017.

Sie können diese Konten in der Windows-Benutzergruppe **SQLRUserGroup**anzeigen. Standardmäßig werden 20 Konten erstellt, ist in der Regel mehr als ausreichend, für die Ausführung externen Skripts Aufträge.

> [!IMPORTANT]
> Die workergruppe heißt **SQLRUserGroup** unabhängig davon, ob Sie R oder Python installiert. Es gibt eine einzelne Gruppe für jede Instanz ein.

Wenn Sie Skripts aus einer remote Data Science-Client ausführen müssen und Sie die Windows-Authentifizierung verwenden, sind weitere Aspekte zu berücksichtigen. Diese Konten müssen über die Berechtigung zum Anmelden, erhalten die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz in Ihrem Namen.

1. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Objekt-Explorer, erweitern Sie dann **Sicherheit**. Klicken Sie dann mit der rechten Maustaste **Anmeldungen**, und wählen Sie **NewLogin**.
2. In der **Anmeldung - neu** wählen Sie im Dialogfeld **Suche**.
3. Wählen Sie **Objekttypen**, und wählen Sie **Gruppen**. Deaktivieren Sie alle anderen aus.
4. In **Geben Sie die zu verwendenden Objektnamen**, Typ *SQLRUserGroup*, und wählen Sie **Namen überprüfen**.
5. Der Name der lokalen Gruppe, die zum Launchpad-Dienst der Instanz gehört, sollte in etwa wie folgt aufgelöst werden: *instancename\SQLRUserGroup*. Wählen Sie **OK**.
6. Standardmäßig die Gruppe zugewiesen, um die **öffentlichen** Rolle, und verfügt über die Berechtigung für die Verbindung mit dem Datenbankmodul.
7. Wählen Sie **OK**.

> [!NOTE]
> Bei Verwendung einer **SQL-Anmeldung** zum Ausführen von Skripts in einer SQL Server-computekontext, dieser zusätzliche Schritt ist nicht erforderlich.

### <a name="give-users-permission-to-run-external-scripts"></a>Vergabe von Benutzerberechtigungen für das Ausführen externer Skripts.

Wenn Sie installiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selbst, und Sie in Ihrer eigenen Instanz Python-Skripts ausgeführt werden, die Sie Skripts in der Regel als Administrator ausführen. Daher müssen Sie die implizite Berechtigung über verschiedene Vorgänge und alle Daten in der Datenbank.

Die meisten Benutzer haben jedoch nicht diese erhöhten Berechtigungen. Beispielsweise müssen Benutzer in einer Organisation, die SQL-Anmeldungen verwenden, für den Datenbankzugriff in der Regel erweiterte Berechtigungen keine. Aus diesem Grund müssen für jeden Benutzer, die mithilfe von Python, Sie Benutzern von Machine Learning Services gewähren die Berechtigung zum Ausführen externer Skripts, die in jeder Datenbank, wo Python verwendet wird. So sieht wie:

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> Berechtigungen sind nicht spezifisch für die unterstützten Skriptsprache. Das heißt, sind nicht separate Berechtigungsebenen für R-Skript im Vergleich zu den Python-Skript. Wenn Sie unterschiedliche Berechtigungen für diese Sprachen verwalten möchten, installieren Sie R und Python auf separaten Instanzen.

### <a name="give-your-users-read-write-or-data-definition-language-ddl-permissions-to-databases"></a>Gewähren Sie die Definition der Benutzer Lese-, Schreib- oder Daten Datendefinitionssprache (DDL)-Zugriffsberechtigungen auf Datenbanken.

Während ein Benutzer die Skripts ausgeführt wird, muss der Benutzer möglicherweise zum Lesen von Daten von anderen Datenbanken. Die Benutzer müssen möglicherweise auch zum Erstellen von neuer Tabellen zum Speichern der Ergebnisse und Schreiben von Daten in Tabellen.

Für jede Windows-Benutzerkonto oder SQL-Anmeldung, die R oder Python-Skripts ausgeführt wird, stellen Sie sicher, dass sie die entsprechenden Berechtigungen für die spezielle Datenbank verfügt: `db_datareader`, `db_datawriter`, oder `db_ddladmin`.

Beispielsweise die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung gibt die SQL-Anmeldung *MySQLLogin* die Rechte zum Ausführen von T-SQL-Abfragen der *ML_Samples* Datenbank. Um diese Anweisung auszuführen, muss die SQL-Anmeldung bereits im Sicherheitskontext des Servers vorhanden sein.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Weitere Informationen zu den Berechtigungen, die in den einzelnen Rollen enthalten, finden Sie unter [Datenbankrollen](../../relational-databases/security/authentication-access/database-level-roles.md).

### <a name="ensure-that-the-sql-server-installation-supports-remote-connections"></a>Stellen Sie sicher, dass die Installation von SQL Server Remoteverbindungen unterstützt

Wenn Sie von einem Remotecomputer herstellen können, überprüfen Sie, ob die Firewall den Zugriff auf SQL Server zulässt. In einer Standardinstallation Remoteverbindungen möglicherweise deaktiviert oder der von SQL Server verwendeten Port durch die Firewall blockiert werden. Weitere Informationen finden Sie unter [Konfigurieren der Windows-Firewall für Datenbankmodulzugriff](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Erstellen einer ODBC-Datenquelle für die Instanz auf Ihrem Data Science-Client

Sie können ein Machine learning-Lösung auf einem Data Science-Clientcomputer erstellen. Wenn Sie Code mit dem SQL Server-Computer als computekontext ausführen müssen, haben Sie zwei Optionen: Zugriff auf die Instanz mithilfe einer SQL-Anmeldung oder mithilfe einer Windows-Konto.

+ Für SQL-Anmeldungen: Stellen Sie sicher, dass die Anmeldung erforderlichen Berechtigungen für die Datenbank verfügt, in dem Sie Daten lesen. Hierzu können Sie durch Hinzufügen von *Herstellen einer Verbindung mit* und *wählen* Berechtigungen, oder indem Sie den Anmeldenamen für die `db_datareader` Rolle. Um Objekte zu erstellen, weisen `DDL_admin` Rechte. Wenn Sie Daten in Tabellen speichern müssen, zum Hinzufügen der `db_datawriter` Rolle.

+ Für Windows-Authentifizierung: müssen Sie möglicherweise eine ODBC-Datenquelle auf dem Data Science-Client zu erstellen, der den Namen der Instanz und andere Verbindungsinformationen angibt. Weitere Informationen finden Sie unter [ODBC-Datenquellenadministrator](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="additional-optimizations"></a>Zusätzliche Optimierungen

Nun, da Sie alles haben, Sie können auch den Server zur Unterstützung von Machine Learning optimieren möchten, oder installieren pretrained Modelle.

### <a name="add-more-worker-accounts"></a>Weitere Konten hinzufügen

Wenn Sie erwarten, viele Benutzer Skripts gleichzeitig ausgeführt werden dass, können Sie die Anzahl der Worker Konten erhöhen, die mit dem Launchpad-Dienst zugewiesen sind. Weitere Informationen finden Sie unter [Ändern des benutzerkontenpools für SQL Server-Machine Learning-Services](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="optimize-the-server-for-script-execution"></a>Optimieren Sie den Server für die Ausführung des Skripts

Die Standardeinstellungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup optimieren den Saldo des Servers für eine Vielzahl von Diensten. Zu diesen Diensten gehören ETL-Prozesse, reporting, Überwachung und Anwendungen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten.

Wenn Sie die Standardeinstellungen verwenden, stellen Sie möglicherweise fest, dass Ressourcen für die Ausführung externer Skripts, insbesondere in arbeitsspeicherintensive Vorgänge gedrosselt oder eingeschränkt werden. Wenn Machine Learning eine Priorität ist, ändern Sie die Standardeinstellungen für die Datenbank um sicherzustellen, dass externe Skripts für Aufträge priorisiert und Ressourcen entsprechend zugewiesen werden. Diese Änderungen können umfassen:

+ Reduziert die Menge des Arbeitsspeichers für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmoduls.
+ Erhöhen der Anzahl von Konten unter ausgeführten der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst. Dies bewirkt keine Erhöhung der Anzahl von Ressourcen, jedoch wird vergrößert die Anzahl von Skripts, die gleichzeitig ausgeführt werden können.

Wenn Sie SQL Server Enterprise Edition verfügen, verwenden Sie die Ressourcenkontrolle so konfigurieren Sie einen externen Ressourcenpool für Python. Weitere Informationen finden Sie in den folgenden Artikeln:

-   Konfigurieren Sie einen Ressourcenpool für das Verwalten von externen Ressourcen
  
     [ERSTELLEN SIE EXTERNEN RESSOURCENPOOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
  
-   Ändern Sie den Arbeitsspeicherumfang, der für das Datenbankmodul reserviert ist
  
     [Serverkonfigurationsoptionen für Arbeitsspeicher-server](../../database-engine/configure-windows/server-memory-server-configuration-options.md)
  
-   Ändern der Anzahl von Worker-Konten, die von gestartet werden kann[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]
  
     [Ändern des benutzerkontenpools für SQL Server R Services](../r/modify-the-user-account-pool-for-sql-server-r-services.md)

Wenn Sie SQL Server Standard Edition verwenden, verfügen nicht über die Ressourcenkontrolle können Sie dynamische Verwaltungssichten und erweiterte Ereignisse verwenden, helfen Ihnen beim Verwalten von Serverressourcen. Sie können auch Windows-ereignisüberwachung für diesen Zweck. Weitere Informationen finden Sie unter [überwachen und Verwalten von R Services](../r/managing-and-monitoring-r-solutions.md).

### <a name="upgrade-the-machine-learning-components"></a>Aktualisieren Sie den Computer mit dem Erlernen von Komponenten

Wenn Sie Machine Learning Services mithilfe von SQL Server-2017 installieren, erhalten Sie die Version der Komponenten, zum Zeitpunkt der Veröffentlichung veröffentlicht wurde. Jedes Mal gepatcht oder aktualisieren Sie die SQL Server-Instanz werden die Machine Learning-Komponenten ebenfalls aktualisiert.

Upgrade Machine learning-Komponenten auf einen schnelleren Zeitplan als unterstützt, wird von SQL Server-Versionen von Microsoft Machine Learning-Server installieren. Wenn Sie dies tun, erhalten Sie auch keine neuen Features, die in der neuesten Version von Machine Learning-Server, z. B. unterstützt:

+ Updates für Python-Pakete für [Revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) und [Microsoftml für Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).
+ [Modelle pretrained](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) für bildanalysen Klassifizierung und Text.

Informationen zum Aktualisieren einer Instanz, finden Sie unter [Upgrade R-Komponenten über Bindung](..\r\use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="tutorials"></a>Lernprogramme

Finden Sie unter den folgenden Lernprogrammen für einige Beispiele für die Verwendung Python mit SQL Server zum Erstellen und Bereitstellen von Machine Learning-Lösungen:

[Verwenden von Python in T-SQL](../tutorials/run-python-using-t-sql.md)

[Erstellen Sie ein Python-Modell mit revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md)
