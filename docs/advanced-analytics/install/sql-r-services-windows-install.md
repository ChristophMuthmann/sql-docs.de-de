---
title: Installieren von SQL Server 2016 R Services (Datenbankintern) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2018
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
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Active
ms.openlocfilehash: 0012b48101085b7ccb18695fbda1f25c10a6b90b
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-2016-r-services-in-database"></a>Installieren von SQL Server 2016 R Services (datenbankintern) 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Artikel wird erläutert, wie zum Installieren und konfigurieren **SQL Server 2016 R Services (Datenbankintern)**. Wenn Sie SQL Server 2016 haben, installieren Sie dieses Feature, um die Ausführung von R-Code in SQL Server zu ermöglichen.

## <a name="bkmk_prereqs"> </a> Prüfliste vor der Installation

+ SQL Server 2016 ist erforderlich. Wenn Sie SQL Server 2016 haben, installieren Sie [SQL Server 2017 Machine Learning Services (Datenbankintern)](sql-machine-learning-services-windows-install.md) stattdessen.

+ Eine Datenbank-Modulinstanz ist erforderlich. Installation kann nicht nur R, Athough Sie ihn inkrementell zu einer vorhandenen Instanz hinzufügen können.

+ Installieren Sie R Services nicht auf einem Failovercluster. Zum Isolieren von R-Prozesse Sicherheitsmechanismus ist nicht kompatibel mit einer Windows Server Failover Cluster-Umgebung.

+ Installieren Sie R Services nicht auf einem Domänencontroller installiert. Der R-Services-Teil der Installation schlägt fehl.

+ Installieren Sie nicht **gemeinsam genutzte Funktionen** > **R Server (eigenständig)** auf demselben Computer Ausführen einer Instanz in der Datenbank. 

+ Seite-an-Seite-Installation mit anderen Versionen von R und Python sind möglich, da SQL Server-Instanz eigenen Kopien der Open Source-R und Anaconda Verteilungen verwendet. Ausführen von Code, der auf dem SQL Server-Computer außerhalb von SQL Server R und Python verwendet kann jedoch zu verschiedenen Problemen führen:
    
  + Sie verwenden eine andere Bibliothek und andere ausführbare Datei, und unterschiedliche Ergebnisse erhalten, als Sie ausführen, wenn Sie in SQL Server ausgeführt werden.
  + R und Python-Skripts, die auf externen Bibliotheken können von SQL Server, um Ressourcenkonflikte führende verwaltet werden.
  
Wenn Sie alle vorherigen Versionen von Revolution Analytics-Entwicklungsumgebung oder dem "revoscaler"-Pakete verwendet oder wenn Sie alle Vorabversionen von SQL Server 2016 installiert haben, müssen Sie sie deinstallieren. Ältere und neuere Versionen von "revoscaler" und anderen proprietären Pakete ausführen, wird nicht unterstützt. Hilfe zum Entfernen früherer Versionen finden Sie [Upgrade und Installation – häufig gestellte Fragen für SQL Server-Machine Learning-Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Nachdem Setup abgeschlossen ist, achten Sie darauf, dass Sie zusätzliche nach der Konfiguration in diesem Artikel beschriebenen Schritte. Diese Schritte umfassen das Aktivieren von SQL Server, um externe Skripts zu verwenden und das Hinzufügen von Konten für SQL Server zum Ausführen von R-Aufträgen in Ihrem Namen erforderlich sind. Konfigurationsänderungen muss in der Regel ein Neustart der Instanz oder einen Neustart des Launchpad-Diensts.

## <a name="get-the-installation-media"></a>Abrufen der Installationsmedien

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> Installieren einer Patchanforderung 

Microsoft hat ein Problem bei der speziellen Version von Microsoft VC++ 2013 Runtime-Binärdateien erkannt, die von SQL Server als vorausgesetzte Komponenten installiert werden. Wenn dieses Update an den VC++ Runtime-Binärdateien nicht installiert wird, können bei SQL Server in bestimmten Szenarios Stabilitätsprobleme auftreten. Bevor Sie SQL Server installieren, sollten Sie entsprechend den Anweisungen unter [Versionsanmerkungen zu SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) vorgehen, um festzustellen, ob Ihr Computer einen Patch für die VC-Runtime-Binärdateien benötigt.  

## <a name="bkmk2016top"></a>Führen Sie das Setup

Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat.

1. Starten Sie den Setup-Assistenten für SQL Server 2016.

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
  
5. Nachdem Sie den Lizenzvertrag akzeptiert haben, besteht eine kurze Pause während der Installer vorbereitet wird. Klicken Sie auf **Weiter** Wenn die Schaltfläche wird verfügbar.

6. Auf der **Installationsbereit** Seite, stellen Sie sicher, dass die folgenden Elemente enthalten sind, und Sie dann wählen **installieren**.

   + Datenbankmoduldienste
   + R Services (In-Database)

    Notieren Sie sich den Speicherort des Ordners, unter dem Pfad `..\Setup Bootstrap\Log` , in dem die Konfigurationsdateien gespeichert werden. Wenn Setup abgeschlossen ist, können Sie die installierten Komponenten in der Statusdatei überprüfen.

7. Wenn die Installation abgeschlossen ist, starten Sie den Computer neu.

##  <a name="bkmk_enableFeature"></a>Ausführen des externen Skripts aktivieren

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
     
3. Um die externe Skriptingfunktion zu aktivieren, führen Sie die folgende Anweisung aus:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Starten Sie den Dienst neu.

Wenn die Installation abgeschlossen ist, starten Sie das Datenbankmodul vor dem Fortfahren mit der nächsten Ausführung des Skripts zu aktivieren.

Die lo auch automatisch Neustart neu gestartet wird den zugehörigen [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst.

Können Sie mit der rechten Maustaste den Dienst neu starten **starten** Befehl für die Instanz in SSMS oder mithilfe der **Services** Bereich in der Systemsteuerung oder mithilfe von [SQL Server-Konfigurations-Manager ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Überprüfen der Installation

Verwenden Sie die folgenden Schritte aus, um sicherzustellen, dass alle Komponenten, die mit dem externes Skript gestartet ausgeführt werden.

1. Öffnen Sie in SQL Server Management Studio ein neues Abfragefenster, und führen Sie den folgenden Befehl:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    Der Wert **Run_value** sollte jetzt auf 1 festgelegt werden.

2. Öffnen der **Services** Systemsteuerung oder mithilfe von SQL Server-Konfigurations-Manager, und vergewissern Sie sich **SQL Server Launchpad-Dienst** ausgeführt wird. Sie sollten einen Dienst für jede Datenbankmodulinstanz, die R verfügt oder Python installiert sein. Starten Sie den Dienst aus, wenn nicht ausgeführt wird. Weitere Informationen finden Sie unter [Komponenten zur Unterstützung der Integration von Python](../python/new-components-in-sql-server-to-support-python-integration.md).

7. Wenn Launchpad ausgeführt wird, sollten Sie möglicherweise Ausführen einfacher R, um sicherzustellen, dass externe Skripts Laufzeiten mit SQL Server kommunizieren können. 

    Öffnen Sie ein neues **Abfrage** Fenster in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und führen Sie ein Skript z. B. Folgendes:
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    Das Skript kann etwas dauern, während zum ersten Mal ausführen die externes Skript-Laufzeit geladen wird. Die Ergebnisse sollten etwa wie folgt aussehen:

    | Hello |
    |----|
    | 1|

## <a name="bkmk_FollowUp"></a> Zusätzliche Konfiguration

Wenn die externen Skript Überprüfungsschritt erfolgreich war, können Sie Python-Befehle ausführen, von SQL Server Management Studio, Visual Studio-Code oder einem anderen Client, der T-SQL-Anweisungen an den Server gesendet werden kann.

Wenn Sie einen Fehler beim Ausführen des Befehls erhalten haben, überprüfen Sie die zusätzlichen Konfigurationsschritte in diesem Abschnitt. Sie müssen möglicherweise zusätzliche entsprechende Konfigurationen an den Dienst oder einer Datenbank vornehmen.

Allgemeine Szenarien, die zusätzliche Änderungen erfordern:

* [Konfigurieren der Windows-Firewall für eingehende Verbindungen](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [Zusätzliche Netzwerkprotokolle aktivieren](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Aktivieren Sie Remoteverbindungen](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Integrierte Berechtigungen für Remotebenutzer erweitern](#bkmk_configureAccounts)
* [Erteilen der Berechtigung zum Ausführen externer Skripts.](#bkmk_AllowLogon)
* [Gewähren von Zugriff auf einzelne Datenbanken](#permissions-db)

> [!NOTE]
> Nicht alle aufgelisteten Änderungen erforderlich sind, und keine u. u. notwendig sein. Anforderungen richten sich nach Ihrem Sicherheitsschema, in dem Sie installiert SQL Server, und wie Sie erwarten, dass Benutzer eine Verbindung mit der Datenbank und externe Skripts ausführen. Weitere Tipps zur Problembehandlung finden Sie hier: [häufig gestellte Fragen zu Upgrade und Installation](../r/upgrade-and-installation-faq-sql-server-r-services.md)

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

Allerdings müssen in einem Enterprise-Szenario können die meisten Benutzer, einschließlich Benutzer, die Zugriff auf die Datenbank mithilfe von SQL-Anmeldungen, diese erhöhten Berechtigungen keine. Aus diesem Grund müssen für jeden Benutzer, die R-Skripts ausgeführt werden, Sie erteilen die Benutzerberechtigungen zum Ausführen von Skripts in jeder Datenbank, in der externen Skripts verwendet werden.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> Benötigen Sie Hilfe beim Setup? Sind Sie unsicher, ob Sie alle Schritte ausgeführt haben? Verwenden Sie diese benutzerdefinierten Berichte, um Installationsstatus überprüfen und zusätzliche Schritte ausführen. 
> 
> [Verwenden von benutzerdefinierten Berichten Machine Learning-Dienste überwachen,](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

### <a name="permissions-db"></a> Geben Sie Ihre Benutzer zu lesen, schreiben oder DDL-Berechtigungen für die Datenbank

Das Benutzerkonto, das zum Ausführen von R verwendet wird möglicherweise müssen zum Lesen von Daten von anderen Datenbanken, Erstellen von neuen Tabellen zum Speichern von Ergebnissen, und Schreiben von Daten in Tabellen. Daher müssen Sie für jeden Benutzer, das Ausführen von R-Skripts, sicherstellen, dass der Benutzer die entsprechenden Berechtigungen für die Datenbank verfügt: *"db_datareader"*, *Db_datawriter*, oder *Db_ddladmin*.

Die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung erteilt beispielsweise der SQL-Anmeldung *MySQLLogin* die Rechte zum Ausführen von T-SQL-Abfragen in der *RSamples* -Datenbank. Um diese Anweisung auszuführen, muss die SQL-Anmeldung bereits im Sicherheitskontext des Servers vorhanden sein.

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Weitere Informationen zu den Berechtigungen, die in den einzelnen Rollen enthalten, finden Sie unter [Datenbankrollen](../../relational-databases/security/authentication-access/database-level-roles.md).


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Erstellen einer ODBC-Datenquelle für die Instanz auf Ihrem Data Science-Client

Wenn Sie R-Lösungen auf einer Data Science-Clientcomputer erstellen und Code mithilfe von SQL Server-Computers als computekontext ausführen müssen, können Sie eine SQL-Anmeldung oder die integrierte Windows-Authentifizierung verwenden.

* Wenn Sie eine SQL-Anmeldung verwenden, müssen Sie sicherstellen, dass sie über die erforderlichen Berechtigungen für die Datenbank verfügt, in der Sie Daten lesen werden. Können Sie dies tun, indem hinzufügen *Herstellen einer Verbindung mit* und *wählen* Berechtigungen, oder indem Sie den Anmeldenamen für die *"db_datareader"* Rolle. Bei Anmeldungen, die zum Erstellen von Objekten müssen hinzufügen *DDL_admin* Rechte. Für Anmeldungen, die Daten speichern müssen, um Tabellen, fügen Sie den Anmeldenamen für die *Db_datawriter* Rolle.

* Für Windows-Authentifizierung: müssen Sie möglicherweise eine ODBC-Datenquelle auf dem Data Science-Client zu konfigurieren, der den Namen der Instanz und andere Verbindungsinformationen angibt. Weitere Informationen finden Sie unter [ODBC-Datenquellenadministrator](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="suggested-optimizations"></a>Vorgeschlagene Optimierungen

Nun, da Sie alles haben, Sie können auch den Server zur Unterstützung von Machine Learning optimieren möchten, oder installieren pretrained Modelle.

### <a name="add-more-worker-accounts"></a>Weitere Konten hinzufügen

Wenn Sie glauben, dass R intensivsten verwendet werden kann oder wenn Sie davon ausgehen, dass viele Benutzer gleichzeitig ausgeführte Skripts werden, können Sie die Anzahl der Worker Konten erhöhen, die mit dem Launchpad-Dienst zugewiesen sind. Weitere Informationen finden Sie unter [Ändern des benutzerkontenpools für SQL Server-Machine Learning-Services](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="bkmk_optimize"></a>Optimieren des Servers für den externen skriptausführung

Die Standardeinstellungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup das Gleichgewicht des Servers für eine Vielzahl von Diensten zu verbessern, die vom Datenbankmodul, extrahieren, Transformieren und laden (ETL) Prozesse, Berichts-, Überwachung, enthalten möglicherweise unterstützt werden sollen und Anwendungen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten. In den Standardeinstellungen finden Sie möglicherweise daher, dass Ressourcen für Machine Learning sind manchmal eingeschränkt oder, insbesondere in arbeitsspeicherintensive Vorgänge gedrosselt.

Um sicherzustellen, dass die Machine Learning Aufträge priorisiert und Ressourcen entsprechend zugewiesen sind, wird empfohlen, dass Sie SQL Server-Ressourcenkontrolle verwenden, um einen externen Ressourcenpool zu konfigurieren. Sie möchten möglicherweise auch die Größe des Arbeitsspeichers zu ändern, die zugeordnet ist, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmodul, oder erhöhen Sie die Anzahl der Konten, die unter ausgeführt der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Dienst.

- Um einen Ressourcenpool für die Verwaltung von externen Ressourcen zu konfigurieren, finden Sie unter [erstellen Sie einen externen Ressourcenpool](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Um die reservierten Umfang an Arbeitsspeicher für die Datenbank zu ändern, finden Sie unter [Server Speicherkonfigurationsoptionen](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- So ändern Sie die Anzahl der R-Konten, die durch gestartet werden können [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], finden Sie unter [Ändern des benutzerkontenpools für Machine Learning](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

Wenn Sie verfügen nicht über die Ressourcenkontrolle und Standard Edition verwenden, können Sie dynamische Verwaltungssichten (DMVs) und erweiterte Ereignisse als auch Windows-Ereignis überwachen, um die Verwaltung von Serverressourcen, die von r verwendet werden Weitere Informationen finden Sie unter [überwachen und Verwalten von R Services](../r/managing-and-monitoring-r-solutions.md).

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

Beispiele für Machine Learning, reale Szenarien basieren, finden Sie unter [Machine learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md).


