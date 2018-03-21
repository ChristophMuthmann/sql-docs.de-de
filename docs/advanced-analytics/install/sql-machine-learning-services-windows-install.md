---
title: Installieren von SQL Server 2017 Machine Learning-Services (Datenbankintern) unter Windows | Microsoft Docs
ms.custom: 
ms.date: 03/20/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 1904517351a23bfa736549a249d77be2932b3c07
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-2017-machine-learning-services-in-database-on-windows"></a>Installieren von SQL Server 2017 Machine Learning-Services (Datenbankintern) unter Windows 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Die Machine Learning-Services-Komponente von SQL Server fügt Vorhersageanalysen in der Datenbank, statistische Analyse, Visualisierung und Machine learning-Algorithmen. Funktionsbibliotheken stehen in R und Python und führen Sie auf eine Datenbankmodulinstanz als externen Skript. 

In diesem Artikel wird erläutert, wie zum Installieren der Machine Learning-Komponente durch Ausführen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup-Assistenten und die folgenden der aufforderungen.

## <a name="bkmk_prereqs"> </a> Prüfliste vor der Installation

+ SQL Server-2017 ist erforderlich. Wenn Sie SQL Server 2016 haben, installieren Sie [SQL Server 2016 R Services (Datenbankintern)](sql-r-services-windows-install.md) stattdessen.

+ Eine Datenbank-Modulinstanz ist erforderlich. Nur R kann nicht installiert oder Python-Funktionen, Athough hinzufügen sie inkrementell zu einer vorhandenen Instanz.

+ Machine Learning Services darf nicht auf einem Failovercluster installiert werden. Zum Isolieren von R und Python-Prozesse Sicherheitsmechanismus ist nicht kompatibel mit einer Windows Server Failover Cluster-Umgebung.

+ Machine Learning Services darf nicht auf einem Domänencontroller installiert werden. Der Machine Learning-Dienste Teil von Setup schlägt fehl.

+ Installieren Sie nicht **gemeinsam genutzte Funktionen** > **Machine Learning-Server (eigenständig)** auf demselben Computer Ausführen einer Instanz in der Datenbank. Ein eigenständiger Server wird für die gleichen Ressourcen, während Sie die Leistung der beiden Installationen untergraben konkurrieren.

+ Seite-an-Seite-Installation mit anderen Versionen von R und Python wird unterstützt, aber nicht empfohlen. Es wird unterstützt, da SQL Server-Instanz eigenen Kopien der Open Source-R und Anaconda Verteilungen verwendet. Aber es wird nicht empfohlen, da das Ausführen von Code, der auf dem SQL Server-Computer außerhalb von SQL Server R und Python verwendet zu verschiedenen Problemen führen kann:
    
  + Sie verwenden eine andere Bibliothek und andere ausführbare Datei, und unterschiedliche Ergebnisse erhalten, als Sie ausführen, wenn Sie in SQL Server ausgeführt werden.
  + R und Python-Skripts, die auf externen Bibliotheken können von SQL Server, um Ressourcenkonflikte führende verwaltet werden.
  
> [!IMPORTANT]
> Nachdem Setup abgeschlossen ist, achten Sie darauf, dass Sie nach der Konfiguration in diesem Artikel beschriebenen Schritte. Diese Schritte umfassen das Aktivieren von SQL Server, um externe Skripts zu verwenden und das Hinzufügen von Konten für SQL Server zum Ausführen von R und Python-Aufträgen in Ihrem Namen erforderlich sind. Konfigurationsänderungen muss in der Regel ein Neustart der Instanz oder einen Neustart des Launchpad-Diensts.

## <a name="get-the-installation-media"></a>Abrufen der Installationsmedien

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Ausführen von 'Setup'

Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat.

1. Starten Sie den Setup-Assistenten für SQL Server-2017. Sie können herunterladen 
  
2. Auf der **Installation** Registerkarte **eigenständige neue SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.

   ![Installieren von Machine Learning-in-Database-Dienste](media/2017setup-installation-page-mlsvcs.PNG)
   
3. Wählen Sie diese Optionen auf der Seite **Funktionsauswahl** aus:
  
    -   **Datenbankmoduldienste**
  
         Um die R und Python mit SQL Server verwenden möchten, müssen Sie eine Instanz des Datenbankmoduls installieren. Sie können entweder eine Standardinstanz oder eine benannte Instanz verwenden.
  
    -   **Machine Learning-Services (Datenbankintern)**
  
         Diese Option installiert die Datenbankdienste, die R zu unterstützen, und Python-skriptausführung.

    -   **R**

        Aktivieren Sie diese Option zum Hinzufügen der Microsoft R-Pakete, Interpreter und Open Source-R. 

    -   **Python**

        Überprüfen Sie diese Option, um die Microsoft-Python-Pakete, die Python-3.5 ausführbare Datei, hinzufügen, und wählen Sie Bibliotheken aus der Anaconda-Verteilung.
        
        ![Optionen für R und Python Feature](media/2017setup-features-page-mls-rpy.png "Setup-Optionen für Python")

        > [!NOTE]
        > 
        > Wählen Sie die Option für nicht **Machine Learning-Server (eigenständig)**. Die Option zum Installieren von Machine Learning-Server unter **gemeinsam genutzte Funktionen** dient zur Verwendung auf einem separaten Computer.

4. Auf der **stimmen Sie R installieren** Seite **Accept**. Die Lizenzbedingungen umfasst Microsoft R zu öffnen, die eine Verteilung der open Source-R-Basispakete und Tools, zusammen mit erweiterten R-Paketen und Konnektivitätsanbietern von Microsoft-Entwicklungsteam enthält.

5. Auf der **Zustimmung zum Installieren von Python** Seite **Accept**. Der Python-open-Source-Lizenzvertrag deckt auch Anaconda und verwandte Tools sowie einige neuen Python-Bibliotheken von Microsoft-Entwicklungsteam.
     
     ![Vereinbarung für den Python-Lizenz](media/2017setup-python-license.png "-Lizenzvertrag für Python")
  
    > [!NOTE]
    >  Wenn der Computer, den Sie verwenden nicht über Internetzugriff verfügt, können Sie Setup aus, an diesem Punkt, um die Installationsprogramme getrennt herunterladen anhalten. Weitere Informationen finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](../install/sql-ml-component-install-without-internet-access.md).
  
     Wählen Sie **Accept**, warten Sie, bis die **Weiter** wird aktiv, und wählen Sie dann die Schaltfläche **Weiter**.
  
6. Auf der **Installationsbereit** Seite, stellen Sie sicher, dass diese Auswahl enthalten ist, und wählen Sie **installieren**.
  
    + Datenbankmoduldienste
    + Machine Learning-Dienste (datenbankintern)
    + R, Python oder beides

    Notieren Sie sich den Speicherort des Ordners, unter dem Pfad `..\Setup Bootstrap\Log` , in dem die Konfigurationsdateien gespeichert werden. Wenn Setup abgeschlossen ist, können Sie die installierten Komponenten in der Statusdatei überprüfen.

## <a name="restart-the-service"></a>Starten Sie den Dienst neu.

Wenn die Installation abgeschlossen ist, starten Sie das Datenbankmodul vor dem Fortfahren mit der nächsten Ausführung des Skripts zu aktivieren.

Die lo auch automatisch Neustart neu gestartet wird den zugehörigen [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst.

Können Sie mit der rechten Maustaste den Dienst neu starten **starten** Befehl für die Instanz in SSMS oder mithilfe der **Services** Bereich in der Systemsteuerung oder mithilfe von [SQL Server-Konfigurations-Manager ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="bkmk_enableFeature"></a>Ausführen des externen Skripts aktivieren

1. Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Sie können auch herunterladen und installieren Sie die entsprechende Version von dieser Seite: [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > Sie können auch versuchen, die Preview-Version von [SQL Operations Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is), das Verwaltungsaufgaben und Abfragen von SQL Server unterstützt.
  
2. Eine Verbindung mit der Instanz, auf dem Sie Machine Learning Services installiert, und auf **neue Abfrage** , öffnen ein Abfragefenster, und führen den folgenden Befehl aus:

   ```SQL
   sp_configure
   ```

    Der Wert für die Eigenschaft `external scripts enabled` sollte an diesem Punkt **0** betragen. Grund hierfür ist die Funktion standardmäßig deaktiviert ist. Die Funktion muss explizit von einem Administrator aktiviert werden, bevor R oder Python-Skripts ausgeführt werden können.
    
3.  Um die externe Skriptingfunktion zu aktivieren, führen Sie die folgende Anweisung aus:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    Wenn Sie bereits die Funktion für die Sprache "R" aktiviert haben, führen Sie kein zweites Mal für Python neu konfigurieren. Die zugrunde liegende Erweiterbarkeitsplattform unterstützt beide Sprachen.

4. Starten Sie den SQL Server-Dienst für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz. Startet den zugehörigen neu auch automatischer Neustart des SQL Server-Diensts [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst.

    Können Sie mit der rechten Maustaste den Dienst neu starten **starten** Befehl für die Instanz in SSMS oder mithilfe der **Services** Bereich in der Systemsteuerung oder mithilfe von [SQL Server-Konfigurations-Manager ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Überprüfen der Installation

Verwenden Sie die folgenden Schritte aus, um sicherzustellen, dass alle Komponenten, die mit dem externes Skript gestartet ausgeführt werden.

1. Öffnen Sie in SQL Server Management Studio ein neues Abfragefenster, und führen Sie den folgenden Befehl:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    Der Wert **Run_value** sollte jetzt auf 1 festgelegt werden.
    
2. Öffnen der **Services** Systemsteuerung oder mithilfe von SQL Server-Konfigurations-Manager, und vergewissern Sie sich **SQL Server Launchpad-Dienst** ausgeführt wird. Sie sollten einen Dienst für jede Datenbankmodulinstanz, die R verfügt oder Python installiert sein. Starten Sie den Dienst aus, wenn nicht ausgeführt wird. Weitere Informationen finden Sie unter [Komponenten zur Unterstützung der Integration von Python](../python/new-components-in-sql-server-to-support-python-integration.md). 
   
3. Wenn Launchpad ausgeführt wird, sollten Sie möglicherweise Ausführen einfacher R und Python-Skripts, um sicherzustellen, dass externe Skripts Laufzeiten mit SQL Server kommunizieren können.

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

 **Ergebnisse**

    Das Skript kann etwas dauern, während zum ersten Mal ausführen die externes Skript-Laufzeit geladen wird. Die Ergebnisse sollten etwa wie folgt aussehen:

    | Hello |
    |----|
    | 1|


> [!NOTE]
> Spalten oder Überschriften im Python-Skript verwendet, werden nicht, entwurfsbedingt zurückgegeben. Um die Spaltennamen für Ihre Ausgabe hinzufügen, müssen Sie das Schema für die zurückgegebenen Daten Menge angeben. Dies erfolgt mithilfe des Parameters mit der Ergebnisse der gespeicherten Prozedur, benennen die Spalten und Angeben des SQL-Datentyps.
> 
> Beispielsweise können Sie die folgende Zeile zum Generieren von einer beliebigen Spaltenname hinzufügen: `WITH RESULT SETS ((Col1 AS int))`

## <a name="additional-configuration"></a>Zusätzliche Konfiguration

Wenn die externen Skript Überprüfungsschritt erfolgreich war, können Sie Python-Befehle ausführen, von SQL Server Management Studio, Visual Studio-Code oder einem anderen Client, der T-SQL-Anweisungen an den Server gesendet werden kann.

Wenn Sie einen Fehler beim Ausführen des Befehls erhalten haben, überprüfen Sie die zusätzlichen Konfigurationsschritte in diesem Abschnitt. Sie müssen möglicherweise zusätzliche entsprechende Konfigurationen an den Dienst oder einer Datenbank vornehmen.

Allgemeine Szenarien, die zusätzliche Änderungen erfordern:

* [Konfigurieren der Windows-Firewall für eingehende Verbindungen](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [Zusätzliche Netzwerkprotokolle aktivieren](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Aktivieren Sie Remoteverbindungen](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Integrierte Berechtigungen für Remotebenutzer erweitern](#bkmk_configureAccounts)
* [Erteilen der Berechtigung zum Ausführen externer Skripts.](#permissions-external-script)
* [Gewähren von Zugriff auf einzelne Datenbanken](#permissions-db)

> [!NOTE]
> Nicht alle aufgelisteten Änderungen erforderlich sind, und keine u. u. notwendig sein. Anforderungen richten sich nach Ihrem Sicherheitsschema, in dem Sie installiert SQL Server, und wie Sie erwarten, dass Benutzer eine Verbindung mit der Datenbank und externe Skripts ausführen. Weitere Tipps zur Problembehandlung finden Sie hier: [häufig gestellte Fragen zu Upgrade und Installation](../r/upgrade-and-installation-faq-sql-server-r-services.md)

###  <a name="bkmk_configureAccounts"></a> Aktivieren Sie die implizite Authentifizierung für die Kontogruppe Launchpad

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

### <a name="permissions-external-script"></a> Vergabe von Benutzerberechtigungen für das Ausführen externer Skripts.

Wenn Sie installiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selbst, und Sie in Ihrer eigenen Instanz R oder Python-Skripts ausgeführt werden, die Sie Skripts in der Regel als Administrator ausführen. Daher müssen Sie die implizite Berechtigung über verschiedene Vorgänge und alle Daten in der Datenbank.

Die meisten Benutzer haben jedoch nicht diese erhöhten Berechtigungen. Beispielsweise müssen Benutzer in einer Organisation, die SQL-Anmeldungen verwenden, für den Datenbankzugriff in der Regel erweiterte Berechtigungen keine. Aus diesem Grund müssen für jeden Benutzer, die mithilfe von R oder Python, Sie Benutzern von Machine Learning Services gewähren die Berechtigung zum Ausführen externer Skripts, die in jeder Datenbank, in denen die Sprache verwendet wird. So sieht wie:

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> Berechtigungen sind nicht spezifisch für die unterstützten Skriptsprache. Das heißt, sind nicht separate Berechtigungsebenen für R-Skript im Vergleich zu den Python-Skript. Wenn Sie unterschiedliche Berechtigungen für diese Sprachen verwalten möchten, installieren Sie R und Python auf separaten Instanzen.

### <a name="permissions-db"></a> Gewähren Sie die Definition der Benutzer Lese-, Schreib- oder Daten Datendefinitionssprache (DDL)-Zugriffsberechtigungen auf Datenbanken.

Während ein Benutzer die Skripts ausgeführt wird, muss der Benutzer möglicherweise zum Lesen von Daten von anderen Datenbanken. Die Benutzer müssen möglicherweise auch zum Erstellen von neuer Tabellen zum Speichern der Ergebnisse und Schreiben von Daten in Tabellen.

Für jede Windows-Benutzerkonto oder SQL-Anmeldung, die R oder Python-Skripts ausgeführt wird, stellen Sie sicher, dass sie die entsprechenden Berechtigungen für die spezielle Datenbank verfügt: `db_datareader`, `db_datawriter`, oder `db_ddladmin`.

Beispielsweise die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung gibt die SQL-Anmeldung *MySQLLogin* die Rechte zum Ausführen von T-SQL-Abfragen der *ML_Samples* Datenbank. Um diese Anweisung auszuführen, muss die SQL-Anmeldung bereits im Sicherheitskontext des Servers vorhanden sein.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Weitere Informationen zu den Berechtigungen, die in den einzelnen Rollen enthalten, finden Sie unter [Datenbankrollen](../../relational-databases/security/authentication-access/database-level-roles.md).


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Erstellen einer ODBC-Datenquelle für die Instanz auf Ihrem Data Science-Client

Sie können ein Machine learning-Lösung auf einem Data Science-Clientcomputer erstellen. Wenn Sie Code mit dem SQL Server-Computer als computekontext ausführen müssen, haben Sie zwei Optionen: Zugriff auf die Instanz mithilfe einer SQL-Anmeldung oder mithilfe einer Windows-Konto.

+ Für SQL-Anmeldungen: Stellen Sie sicher, dass die Anmeldung erforderlichen Berechtigungen für die Datenbank verfügt, in dem Sie Daten lesen. Hierzu können Sie durch Hinzufügen von *Herstellen einer Verbindung mit* und *wählen* Berechtigungen, oder indem Sie den Anmeldenamen für die `db_datareader` Rolle. Um Objekte zu erstellen, weisen `DDL_admin` Rechte. Wenn Sie Daten in Tabellen speichern müssen, zum Hinzufügen der `db_datawriter` Rolle.

+ Für Windows-Authentifizierung: müssen Sie möglicherweise eine ODBC-Datenquelle auf dem Data Science-Client zu erstellen, der den Namen der Instanz und andere Verbindungsinformationen angibt. Weitere Informationen finden Sie unter [ODBC-Datenquellenadministrator](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="suggested-optimizations"></a>Vorgeschlagene Optimierungen

Nun, da Sie alles haben, Sie können auch den Server zur Unterstützung von Machine Learning optimieren möchten, oder installieren pretrained Modelle.

### <a name="add-more-worker-accounts"></a>Weitere Konten hinzufügen

Wenn Sie erwarten, viele Benutzer Skripts gleichzeitig ausgeführt werden dass, können Sie die Anzahl der Worker Konten erhöhen, die mit dem Launchpad-Dienst zugewiesen sind. Weitere Informationen finden Sie unter [Ändern des benutzerkontenpools für SQL Server-Machine Learning-Services](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="optimize-the-server-for-script-execution"></a>Optimieren Sie den Server für die Ausführung des Skripts

Die Standardeinstellungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup das Gleichgewicht des Servers für eine Vielzahl von Diensten zu verbessern, die vom Datenbankmodul, extrahieren, Transformieren und laden (ETL) Prozesse, Berichts-, Überwachung, enthalten möglicherweise unterstützt werden sollen und Anwendungen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten. In den Standardeinstellungen finden Sie möglicherweise daher, dass Ressourcen für Machine Learning sind manchmal eingeschränkt oder, insbesondere in arbeitsspeicherintensive Vorgänge gedrosselt.

Um sicherzustellen, dass die Machine Learning Aufträge priorisiert und Ressourcen entsprechend zugewiesen sind, wird empfohlen, dass Sie SQL Server-Ressourcenkontrolle verwenden, um einen externen Ressourcenpool zu konfigurieren. Sie möchten möglicherweise auch die Größe des Arbeitsspeichers zu ändern, die zugeordnet ist, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmodul, oder erhöhen Sie die Anzahl der Konten, die unter ausgeführt der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst.

- Um einen Ressourcenpool für die Verwaltung von externen Ressourcen zu konfigurieren, finden Sie unter [erstellen Sie einen externen Ressourcenpool](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Um die reservierten Umfang an Arbeitsspeicher für die Datenbank zu ändern, finden Sie unter [Server Speicherkonfigurationsoptionen](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- So ändern Sie die Anzahl der R-Konten, die durch gestartet werden können [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], finden Sie unter [Ändern des benutzerkontenpools für Machine Learning](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

Wenn Sie verfügen nicht über die Ressourcenkontrolle und Standard Edition verwenden, können Sie dynamische Verwaltungssichten (DMVs) und erweiterte Ereignisse als auch Windows-Ereignis überwachen, um die Verwaltung von Serverressourcen. Weitere Informationen finden Sie unter [überwachen und Verwalten von R Services](../r/managing-and-monitoring-r-solutions.md) und [überwachen und Verwalten von Python-Diensten](../python/managing-and-monitoring-python-solutions.md).

### <a name="install-additional-r-packages"></a>Installieren Sie zusätzliche R-Pakete

R-Lösungen, die Sie für SQL Server erstellen, können grundlegende R-Funktionen, Funktionen aus der Properietary Packes mit SQL Server und Drittanbieter-R-Paketen kompatibel mit der Version der Open-Source-R durch SQL Server installierte installiert aufrufen.

Pakete, die Sie von SQL Server verwenden möchten, müssen in der Standardbibliothek installiert sein, die von der Instanz verwendet wird. Wenn Sie eine separate Installation von R auf dem Computer oder bei Installation von Paketen in benutzerbibliotheken nicht auf diese Pakete von T-SQL verwenden kann.

In SQL Server 2016 und SQL Server-2017 unterscheidet sich die Verfahren zum Installieren und Verwalten von R-Pakete. In SQL Server 2016 muss ein Datenbankadministrator R-Pakete installieren, die Benutzer benötigen. In SQL Server 2017 können Sie Benutzergruppen einrichten, Pakete auf einer pro-Datenbankebene freigeben oder Konfigurieren von Datenbankrollen, damit Benutzer ihre eigenen Pakete installieren können. Weitere Informationen finden Sie unter [Paket Management](../r/r-package-management-for-sql-server-r-services.md).


## <a name="get-help"></a>Abrufen von Hilfe

Benötigen Sie Hilfe bei der Installation oder Aktualisierung? Antworten auf häufig gestellte Fragen und bekannte Probleme finden Sie im folgenden Artikel:

* [Upgrade und Installation häufig gestellte Fragen – Machine Learning-Dienste](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Überprüfen Sie den Installationsstatus der Instanz, und beheben Probleme, wiederholen Sie dann diese benutzerdefinierten Berichte.

* [Benutzerdefinierte Berichte für SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Nächste Schritte

R-Entwickler können mit einigen einfachen Beispielen beginnen und die Grundlagen der Funktionsweise von R mit SQL Server. Im nächsten Schritt finden Sie unter den folgenden Links:

+ [Lernprogramm: Ausführen von R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Lernprogramm: In-Database-Analyse für R-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python-Entwickler können zum Verwenden von Python mit SQL Server gemäß diesen Lernprogrammen erfahren:

+ [Lernprogramm: Ausführen von Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Lernprogramm: In-Database-Analyse für Python-Entwickler](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Beispiele für Machine Learning, reale Szenarien basieren, finden Sie unter [Machine learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md).
