---
title: "Installieren Sie zusätzliche R-Pakete unter SQL Server | Microsoft Docs"
ms.date: 11/15/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: f8d20c5b5b687a6d9d94cd97605f294cead27215
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="install-additional-r-packages-on-sql-server"></a>Installieren Sie zusätzliche R-Pakete unter SQL Server

Dieser Artikel beschreibt, wie neue R-Pakete mit einer Instanz von SQL Server installieren, Machine Learning aktiviert ist.

> [!IMPORTANT]
> Die Vorgehensweise zum Hinzufügen neuer Pakete unterscheidet sich je nach Version von SQL Server ausgeführt wird und die Tools, die Sie verwenden. 

**Gilt für:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] und  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="overview-of-package-installation-process"></a>Übersicht über die Paketinstallation

1.  Bestimmen Sie, ob eine Windows-Version des Pakets vorhanden ist: [abrufen, die richtige Paketversion und Format](#packageVersion)

2.  Wenn der Server nicht über Internetzugriff verfügt, laden Sie die Binärdateien im voraus: [Download Zip-Dateien](#bkmk_zipPreparation)

    Achten Sie darauf, dass zu paketabhängigkeiten suchen und Abrufen aller zugehörigen Pakete, die möglicherweise während der Installation benötigt werden. Um eine Auflistung von Paketen und deren Abhängigkeiten vorzubereiten, empfehlen wir die [MiniCRAN Paket](#bkmk_packageDependencies).

    Wenn Sie Downloads oder der Installation Fehler auftreten, versuchen Sie es einer anderen gespiegelten Site.

3.  Wie Sie das Paket installieren hängt davon ab, ob der Server über Internetzugriff verfügt, und auf Ihre Version von SQL Server. Die empfohlene Prozesse lauten wie folgt:

    **Paketinstallation für SQL Server 2016**
    
    1. Der Data Scientist enthält die Pakete, die für ein Projekt oder Team erforderlich. Verwendung [MiniCRAN](create-a-local-package-repository-using-minicran.md) um Sammlungen von Paketen mit ihren Abhängigkeiten vorzubereiten.

    2. Der Datenbankadministrator installiert die Pakete an die Instanz-Bibliothek, die mithilfe von R-Tools.

    **Paketinstallation für SQL Server-2017**

    1. Der Datenbankadministrator paketverwaltung für die Instanz aktiviert und neue Paket-Verwaltungsrollen Benutzer hinzugefügt.

    2. Der Data Scientist enthält die Pakete, die für ein Projekt oder Team erforderlich. Verwendung [MiniCRAN](create-a-local-package-repository-using-minicran.md) um Sammlungen von Paketen mit ihren Abhängigkeiten vorzubereiten.

    3. Das Paket wird in SQL Server-Instanz, mit der EXTERNEN Bibliothek erstellen-Anweisung hochgeladen.
    
    4. Nachdem das Paket mit der Instanz hinzugefügt wurde, jeder Benutzer mit den entsprechenden Berechtigungen kann installieren die Pakete auf der Datenbank, in dem R-Skripts, ausgeführt werden, durch den Aufruf der R-Code aus `sp_execute_external_script`.
    
    5. Benutzer mit entsprechenden Berechtigungen können auch installiert oder Pakete von einem R-Remoteclient, verwenden neue "revoscaler"-Funktion für paketverwaltung zu suchen.

## <a name="install-new-packages"></a>Installieren Sie neue Pakete

In diesem Abschnitt enthalten detaillierte Verfahren für Schlüsselpaket Installationsszenarien. Wählen Sie die beste Methode, je nach:

- Die Version von SQL Server, die Sie verwenden

- Gibt an, ob Sie der alleinige Besitzer der Instanz, oder versuchen, für die Verwaltung von Paketen für mehrere Personen, die mithilfe von Datenbankrollen.

- Gibt an, ob Sie ein einzelnes Paket oder mehrere Pakete mit Abhängigkeiten installieren

**Verwenden Sie SQL Server-paketverwaltung**

Wenn Ihre Instanz Paket Verwaltungsfunktionen unterstützt, können Sie T-SQL oder konventionellen R-Tools verwenden.

-  Uploadpaket R zu, in denen paketverwaltung und das Paket mit der rollenbasierten Zugriff auf, SQL Server aktiviert ist. Ein Benutzer installiert anschließend das Paket mithilfe des T-SQL.

    [Installieren von Paketen, die mit EXTERNEN Bibliothek erstellen](#bkmk_sqlInstall)

- Verwenden Sie einen R-Remoteclient, um neue Pakete auf einen Server hinzuzufügen. Erfordert SQLServer 2017. Paketverwaltung muss auf dem Server aktiviert worden sein. 

    [Verwenden Sie R, um Pakete auf einem Server installieren, wenn paketverwaltung aktiviert ist](#bkmk_rAddPackage)

- Vorbereiten einer Paket-Bibliothek für die Verwendung mit einer EXTERNEN Bibliothek erstellen, die mehrere Pakete zusammen mit deren Abhängigkeiten enthält.

    [Zum Installieren Sie mehrerer Pakete aus einem Repository miniCRAN](#bkmk_minicran)

**Verwenden Sie herkömmliche R-tools**

Wenn Sie eine frühere Version von SQL Server R Services verwenden, befolgen Sie diese Anweisungen zum Installieren der Pakete mit konventionellen R-Tools aus. Verwenden Sie optional MiniCRAN, um eine Auflistung von Paketen für die Installation vorzubereiten.

-  Installieren Sie ein R-Paket in die standardmäßige Instanz-Bibliothek, die mithilfe von R-Tools. Ist Administratorzugriff erforderlich.

    [Installieren von Paketen in der Instanz-Bibliothek, die mithilfe von R-tools](#bkmk_rInstall)

- Erstellen einer freigegebenen Auflistung von Paketen, um einfache Installation mehrere Pakete und ihrer Abhängigkeiten zu unterstützen.

    [Erstellen Sie ein paketrepository mit miniCRAN](create-a-local-package-repository-using-minicran.md)

### <a name="bkmk_sqlInstall"></a>Installieren von Paketen mithilfe von SQL Server-tools

1. Stellen Sie sicher, dass das externe Bibliothek-Management-Feature in SQL Server-2017 für die Instanz aktiviert wurde.

    [Aktivieren oder Deaktivieren der paketverwaltung](r-package-how-to-enable-or-disable.md)

2. Herstellen einer Verbindung mit dem Server mit einem Konto mit Berechtigungen zum Installieren neuer Pakete, die mithilfe einer der unterstützten Datenbankrollen, die in diesem Thema beschriebenen: [R-paketverwaltung für SQL Server](r-package-management-for-sql-server-r-services.md)

3.  Kopieren Sie die ZIP-Datei mit dem R-Paket, das Sie z. B. in einen Ordner auf dem Server-Computer installieren möchten Ihre **Benutzer** oder **Dokumente** Ordner. Ein Paket kann nicht auf einem Netzlaufwerk oder aus einem Ordner auf dem Clientcomputer hinzufügen werden. Wenn Sie zum Erstellen eines MiniCRAN verwendet haben, kopieren Sie den paketrepository in seiner Gesamtheit in einen lokalen Ordner auf dem Server: d. h. nicht auf ein Netzlaufwerk.

    Wenn Sie keinen Zugriff auf Ordner auf dem Server haben, können Sie den Inhalt im Binärformat übergeben. Finden Sie unter [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) ein Beispiel.

4.  Führen Sie aus der Datenbank, in dem das Paket verwendet werden sollen, die [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) Anweisung.

    In diesem Beispiel wird angenommen, dass Ihr Konto berechtigt ist, neue Pakete an den Server hochladen, und installieren sie **freigegebenen** Bereich in der Datenbank.

    Die folgende Anweisung fügt die endgültigen Produktversion von der ["zoo" folgendermaßen](https://cran.r-project.org/web/packages/zoo/index.html) Paket in der aktuellen Datenbankkontext aus einer lokalen Dateifreigabe.

    ```SQL
    CREATE EXTERNAL LIBRARY zoo
    FROM (CONTENT = 'C:\Temp\RPackages\zoo_1.8-0.zip')
    WITH (LANGUAGE = 'R');
    ```

    Wenn Sie eine Verbindung herstellen, die mit einem Konto an, die ein Datenbankbesitzer (Mitglied der Rolle "Dbo") ist, wird das Paket im zur Verfügung gestellt **freigegebenen** Bereich: d. h. es installiert werden kann jeder Benutzer, der ein Element ist von der `rpkgs-users` Rolle.

    Wenn Sie das Paket mit einem Konto an, die nur zugreifen kann hochladen **private** Bereich, das Paket kann nur von Ihnen installiert werden.

4.  Führen Sie zum Installieren des Pakets in der Standardeinstellung R-Bibliothek von der Instanz verwendeten R `library()` Befehl innerhalb der gespeicherten Prozedur Sp_execute_external_script.

    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # load the binaries in zoo
    library(zoo)'
    ```

    Bei erfolgreicher Ausführung der **Nachrichten** Fenster sollte eine Nachricht melden, z. B. "Paket"Zoo"wurde erfolgreich entpackt und MD5 Summen überprüft." Wenn ein erforderliches Paket bereits installiert ist, wird während des Installationsvorgangs dann angefügt, und lädt das Paket erforderliche.

    > [!NOTE]
    > Wenn ein erforderliches Paket nicht verfügbar ist, wird ein Fehler zurückgegeben: "ist kein Paket aufgerufen \<Required_package\>". 
    > 
    > Um Fehler zu vermeiden, wird empfohlen, dass Sie paketabhängigkeiten im Vorfeld überprüfen oder MiniCRAN verwenden, um alle erforderlichen Pakete in eine einzelne ZIP-Datei vor der Ausführung zu erfassen `CREATE EXTERNAL LIBRARY`.

### <a name="bkmk_rAddPackage"></a>Verwenden Sie R, um Pakete auf einem Server installieren, wenn paketverwaltung aktiviert ist

Wenn Sie bereits paketverwaltung für die Instanz aktiviert haben, können Sie neue R-Pakete von einem R-Remoteclient, der mithilfe von RevoScaleR-Funktionen für die paketverwaltung installieren.

1. Bevor Sie beginnen, stellen Sie sicher, dass diese Bedingungen erfüllt sind:

    + Verwenden Sie die neueste Version von Microsoft R-Client, der Standortdatenbank Updates RevoScale enthält.
    + Paketverwaltung wurde für die Instanz und für die Datenbank aktiviert.
    + Sie über die Berechtigung zu einem der Management-Datenbankrollen.

2. Liste der Pakete, die Sie in eine Zeichenfolgenvariable installieren möchten.

    ```R
    packageList <- c("e1071")
    ```
    
3. Definieren Sie eine Verbindungszeichenfolge für die Instanz und die Datenbank, in dem paketverwaltung aktiviert ist, und verwenden Sie die Verbindungszeichenfolge so erstellen einen SQL Server-computekontext.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

4. Rufen Sie `rxInstallPackages` und übergeben des computekontexts und die Zeichenfolgenvariable, die mit den Paketnamen.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Wenn die abhängigen Programme erforderlich sind, werden sie auch heruntergeladen.
    
    In diesem Beispiel weil der Paketbesitzer und des Bereichs wurde nicht angegeben, das Paket installiert ist, mit den Anmeldeinformationen des Benutzers herstellen der Verbindung, und Pakete installiert sind, verwenden den Standardbereich für diesen Benutzer.

### <a name="bkmk_rInstall"></a>Installieren von Paketen in der Instanz-Bibliothek, die mithilfe von R-tools

R-Tools können Sie um neue Pakete auf SQL Server 2016 und SQL Server-2017 zu installieren. Allerdings müssen Sie ein Administrator dazu sein.

1.  Wenn der Server nicht über Internetzugriff verfügt, laden Sie die Pakete voraus herunter.

    Es wird empfohlen, dass Sie ein paketrepository verwenden, um Sammlungen von offline-Paketen vorzubereiten. Weitere Informationen finden Sie unter [erstellen Sie ein lokales Paket-Repository mit MiniCRAN](create-a-local-package-repository-using-minicran.md).

2.  Navigieren Sie zu dem Ordner auf dem Server, auf dem R-Bibliotheken für die Instanz installiert werden.

    > [!IMPORTANT] 
    > Achten Sie darauf, dass Pakete in der Standardbibliothek installieren, die der aktuellen Instanz zugeordnet ist. Installieren Sie Pakete niemals ein Verzeichnis des Benutzers. Anleitungen zum Suchen der Standardbibliothek finden Sie unter [R-Pakete, die mit SQL Server installierten](installing-and-managing-r-packages.md).

    Installieren Sie für jede Instanz, in dem Sie ein Paket ausführen eine separate Kopie des Pakets. Pakete können nicht über Instanzen freigegeben werden.

4.  Öffnen Sie eine R-Eingabeaufforderung als Administrator an.

    Z. B. bei Verwendung der Windows-Eingabeaufforderung, navigieren Sie zu dem Verzeichnis, in dem die RTerm.Exe "oder" RGui.exe-Dateien gespeichert sind. 

    **Standardinstanz**

    SQLServer 2017:`C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQLServer 2016:`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **Benannte Instanz**

    SQLServer 2017:`C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQLServer 2016:`C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

5.  Führen Sie den Befehl R `install.packages` zum Installieren des Pakets.

    Die Syntax hängt davon ab, ob Sie das Paket aus dem Internet oder aus einer lokalen ZIP-Datei ausgegeben werden. 

    **Installieren des Pakets, die über eine Internetverbindung**

    Die folgende Anweisung installiert z. B. das beliebte e1071-Paket. Doppelte Anführungszeichen müssen immer für den Paketnamen.

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    Wenn Sie nach einer gespiegelten Site gefragt werden, wählen Sie einen Standort, der für Ihren Standort zweckmäßig ist.

    Wenn das Zielpaket von weiteren Paketen abhängig ist, die R-Installationsprogramm automatisch die Abhängigkeiten für herunter und installiert sie Sie.

    **Installieren Sie das Paket manuell oder auf einem Computer ohne Internetzugang**

    Wenn das Paket, das Sie installieren möchten, Abhängigkeiten aufweist, laden Sie die erforderlichen Pakete im Voraus herunter, und fügen Sie sie zum Ordner mit anderen komprimierten Paketdateien hinzu. Finden Sie unter der [Tipps zur Installation](#bkmk_tips) Abschnitt Hilfe zum Vorbereiten der Pakete.

    Geben Sie an der R-Eingabeaufforderung mit dem folgenden Befehl den Pfad und den Namen des zu installierenden Pakets an:

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Dieser Befehl extrahiert ein einzelnes R-Paket aus der lokalen ZIP-Datei, sofern Sie die Kopie im Verzeichnis gespeichert ist `C:\Temp\Downloaded packages`, und das Paket (mit seinen Abhängigkeiten) in der R-Bibliothek auf dem lokalen Computer installiert.

### <a name="bkmk_minicran"></a>Zum Installieren Sie mehrerer Pakete aus einem Repository miniCRAN

Installieren von Paketen aus einem Repository MiniCRAN Gesamtprozesses ähnelt der Installation eines Pakets aus einer einzelnen ZIP-Datei. Allerdings enthält das Repository MiniCRAN anstatt Hochladen eines einzelnen Pakets im ZIP-Format, das Zielpaket sowie alle zugehörigen erforderlichen Pakete.

1.  Bereiten Sie das Repository MiniCRAN vor, und kopieren Sie die ZIP-Datei in einen lokalen Ordner auf dem Server.

2.  Bei Verwendung von T-SQL führt ein Administrator die T-SQL-Anweisung `CREATE EXTERNAL LIBRARY` zum Hochladen von ZIP-Paket-Auflistung in der Datenbank.

    Die folgende Anweisung verweist, beispielsweise ein MiniCRAN-Repository, die die RandomForest-Paket und seine Abhängigkeiten enthält.

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

3. Führen Sie den folgenden Befehl im Rahmen des R-Code in einer gespeicherten Prozedur, um die Pakete für die Verwendung mit SQL Server zu installieren.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    Bei erfolgreicher Ausführung der **Nachrichten** Fenster sollte eine Nachricht melden, z. B. "Paket"RandomForest"wurde erfolgreich entpackt und MD5 Summen überprüft" und "Fertig gestellt Ausführung verkettet".

## <a name="package-installation-tips"></a>Tipps zur Installation des Pakets

Dieser Abschnitt enthält verschiedene Tipps und Beispielcode im Zusammenhang mit der Installation von R-Paket für SQL Server. 

###  <a name="packageVersion"></a>Rufen Sie die richtige Paketversion und format

Es gibt mehrere Quellen für R-Pakete. Die bekannteste Quellen sind CRAN und Bioconductor. Auf der offiziellen Website für die R-Sprache (<https://www.r-project.org/>) sind viele dieser Ressourcen aufgeführt. Viele Pakete werden in GitHub veröffentlicht, in dem Sie den Quellcode erhalten können. Aber können Sie R-Pakete zugewiesen wurde, die von einer Person in Ihrem Unternehmen entwickelt wurden.

Unabhängig von der Quelle müssen Sie sicherstellen, dass das Paket, das Sie installieren möchten, ein binäres Format für die Windows-Plattform verfügt. Andernfalls kann nicht das heruntergeladene Paket in der SQL Server-Umgebung ausgeführt.

Vor dem Herunterladen, sollten Sie auch überprüfen, ob das Paket mit der Version von R kompatibel ist, die in SQL Server ausgeführt wird.

### <a name="bkmk_zipPreparation"></a>Paket als ZIP-Datei herunterladen

Laden Sie eine Kopie des Pakets in das Format einer ZIP-Datei für die Offlineinstallation, für die Installation auf einem Server ohne Internetzugriff. Entzippen Sie das Paket nicht.

Z. B. das folgende Verfahren beschreibt jetzt, um die richtige Version von den [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) Paket von Bioconductor, vorausgesetzt, der Computer über Internetzugriff verfügt.

1.  Suchen Sie in der Liste der **Paketarchive** die **Windows-Binärdateiversion** .

2.  Mit der rechten Maustaste des Links, um die. ZIP-Datei, und wählen **Ziel speichern unter**.

3.  Navigieren Sie zu den lokalen Ordner, in dem komprimierten Pakete gespeichert sind, und klicken Sie auf **speichern**.

Dieser Vorgang erstellt eine lokale Kopie des Pakets. Sie können anschließend installieren Sie das Paket, oder kopieren das ZIP-Paket auf einen Server, die über keinen Zugriff auf das Internet.

Für Weitere Informationen zum Inhalt der Zip-Dateiformats und wie Sie ein R-Paket erstellen, empfehlen wir dieses Lernprogramm, das Sie im PDF-Format aus der R-Projektwebsite herunterladen können: [R-Pakete erstellen](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf).

### <a name="bkmk_packageDependencies"></a>Abrufen von paketabhängigkeiten

R-Pakete hängen häufig mehrere andere Pakete, von die einige möglicherweise nicht verfügbar in der Standardeinstellung R-Bibliothek, die von der Instanz verwendet. Oder manchmal ein Paket erfordert eine andere Version von ein abhängiges Paket, das bereits installiert ist.

Wenn Sie müssen zum Installieren mehrerer Pakete, oder möchten, stellen Sie sicher, dass jeder einzelne in Ihrem Unternehmen die richtigen Pakettyp und Version erhält, wird empfohlen, dass Sie das Paket MiniCRAN verwenden, um ein lokales Repository erstellt, das für mehrere Benutzer oder Computer freigegeben werden können. Weitere Informationen finden Sie unter [erstellen Sie ein lokales Paket-Repository mit MiniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="permissions"></a>Berechtigungen

Wenn Sie ein erfahrener R-Benutzer sind, können Sie beim Installieren von Paketen über die Befehlszeile ohne spezielle Berechtigungen, oder sie zuvor herunterzuladen sein. Allerdings müssen die meisten Server eine Internetverbindung keine. Darüber hinaus den Zugriff auf Dateifreigaben oder Speicher kann eingeschränkt werden.

Dieser Abschnitt beschreibt das verschiedene Maß für die Installation von Paketen in SQL Server 2016 und SQl Server-2017 erforderlichen Berechtigungen. Installation erfolgen kann mithilfe von R-Tools oder SQL Server, jedoch den Prozess und die Berechtigungen unterscheiden sich geringfügig.

-   SQL Server 2016

    In dieser Version kann nur ein Administrator auf dem Computer Pakete an den erforderlichen Speicherort installieren. Sie standard-R-Tools verwenden, um Pakete zu installieren, aber Sie müssen als Administrator ausführen und den R-Tools, die der Instanz zugeordnet.

-   SQL Server 2017

    Diese Version bietet neue Features, mit die einen Datenbankadministrator Paketinstallation für Benutzer zu delegieren können. Der Datenbankadministrator muss Paket-Verwaltungsfunktionen auf Instanzebene zu aktivieren. Nachdem diese Funktion aktiviert ist, kann der DBA Datenbankrollen verwenden, um einzelnen Benutzern die Möglichkeit Pakete installiert, nach Bedarf, oder Teilen Pakete auf einem datenbankbasis.

    Weitere Informationen finden Sie unter [paketverwaltung für SQL Server R](r-package-management-for-sql-server-r-services.md).


> [!IMPORTANT]
> 
> Erfahrene Benutzer von R sind daran gewöhnt, zum Installieren von Paketen in einer Benutzerbibliothek und verweisen auf das Paket in diesem Ordner als Teil der R-Lösung, indem Sie einen Dateipfad angeben. Dieses Vorgehen wird jedoch nicht in SQL Server unterstützt. Weitere Informationen und problemumgehungen finden Sie unter [zum Verwenden von Paketen in benutzerbibliotheken](packages-installed-in-user-libraries.md).

### <a name="comparing-package-management-methods"></a>Vergleichen von Paket-Verwaltungsmethoden

In diesem Abschnitt Vergleich der Methoden der Paket-Installation zur Verfügung, und enthält einige weitere Überlegungen und Tipps, wie Sie eine entsprechende Paket Strategie für die Verwaltung und Installation zu bestimmen.

#### <a name="using-sql-server-package-management-features"></a>Verwaltungsfunktionen für SQL Server-Paket verwenden

Wenn Sie paketverwaltung aktivieren, installieren Sie ein Paket für eine bestimmte Datenbank. Wenn Sie müssen mithilfe eines Pakets in allen Datenbanken, wobei R-Skript aktiviert ist, müssten Sie diese in jeder Datenbank installieren.

Jedoch, da die Informationen von SQL Server verwaltet werden zu den Benutzern die Berechtigung zum Verwenden von Paketen verfügt, ist es einfacher, Informationen zu Benutzern und Pakete zwischen Datenbanken zu kopieren. Es ist auch einfach um eine Reihe von Paketen arbeiten, für einen oder mehrere Benutzer beim Wiederherstellen einer Datenbank oder beim Wechseln zwischen Instanzen neu zu erstellen.

Mithilfe von T-SQL und die Paket-Management-Funktionen in SQL Server-2017 ist die bevorzugte Methode, wenn Sie mehrere Datenbankbenutzer installieren oder Ausführen von R-Pakete haben.

Diese Funktion ist mit SQL Server-2017 ab.

#### <a name="using-r-tools-to-install-packages-for-the-sql-server-instance"></a>Mithilfe von R-Tools zum Installieren der Pakete für SQL Server-Instanz

Wenn Sie diese Methode verwenden, sind für die Instanz installierte Pakete in einer Datenbank verfügbar. Aber da Pakete direkt in das Dateisystem installiert sind, müssen sie außerhalb von SQL Server verwaltet werden. Pakete können nicht gesichert oder wiederhergestellt werden. Darüber hinaus muss der Datenbankadministrator erfahren, wie Sie R-Tools verwenden.

Allerdings ist diese Lösung die einfachste Domänenmodus der alleinige Besitzer der Datenbank.

#### <a name="managing-multiple-packages-and-multiple-versions-of-the-same-package"></a>Verwalten von mehreren Paketen sowie mehrere Versionen des gleichen Pakets

Wenn Sie offline-Installation von R-Pakete ausführen müssen, Einrichten von einem lokalen Repository mit [MiniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) können Sie Pakete freigeben und die Versionen, die zur Verwendung von der Organisation zu verwalten.

#### <a name="establish-a-single-mirror-site-as-standard"></a>Einrichten einer einzelnen gespiegelten Site als standard

Um nicht jedes Mal, wenn Sie ein neues Paket hinzufügen, eine gespiegelte Site auswählen zu müssen, können Sie die R-Entwicklungsumgebung so konfigurieren, dass immer dasselbe Repository verwendet wird. Hierzu bearbeiten Sie die globale R-Einstellungsdatei **. Rprofile**, und fügen Sie die folgende Zeile hinzu:

`options(repos=structure(c(CRAN="<mirror site URL>")))`

Aktueller CRAN-Spiegel werden auch auf [Websiteansicht](https://cran.r-project.org/mirrors.html).

Führen Sie für ausführliche Informationen zu Voreinstellungen und anderen Dateien geladen, wenn die Laufzeit von R startet diesen Befehl aus einer R-Konsole aus:`?Startup`

#### <a name="know-which-library-you-are-using-for-installation"></a>Wissen Sie, welche Bibliothek, die Sie für die Installation verwenden

Wenn Sie vor der Installation von alles zuvor die R-Umgebung auf dem Computer geändert haben, halten Sie einen Moment, und stellen Sie sicher, dass die R-Umgebungsvariable `.libPath` nur ein Pfad verwendet.

Dieser Pfad sollte auf den Ordner R_SERVICES für die Instanz verweisen. Weitere Informationen finden Sie unter [R-Pakete, die mit SQL Server installierten](installing-and-managing-r-packages.md).

#### <a name="side-by-side-installation-with-r-server"></a>Seite-an-Seite-Installation mit R-Server

Wenn Sie Microsoft Machine Learning-Server (eigenständig) zusätzlich zu den SQL Server-Machine Learning-Services installiert haben, sollte Ihre Computer separate Installationen von R für jede zu beiden Duplikate aller R-Tools und Bibliotheken verfügen.

> [!IMPORTANT]
> 
> Pakete, die in der Bibliothek R_SERVER installiert sind, werden nur von Microsoft R Server verwendet und nicht von SQL Server zugegriffen werden.
> 
> Achten Sie darauf, dass Sie verwenden die `R_SERVICES` Bibliothek Installieren von Paketen, die Sie in SQL Server verwenden möchten.
