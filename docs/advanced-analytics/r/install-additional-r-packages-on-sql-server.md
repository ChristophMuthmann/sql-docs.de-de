---
title: "Installieren Sie zusätzliche R-Pakete unter SQL Server | Microsoft Docs"
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 530745918dfd4808694b401be55e40bac00f3cce
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>Installieren Sie zusätzliche R-Pakete unter SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel beschreibt, wie neue R-Pakete mit einer Instanz von SQL Server installieren, Machine Learning aktiviert ist.

**Gilt für:** 
+ [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]  [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]
+ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="prerequisites"></a>Erforderliche Komponenten

+ Bestimmen Sie, ob eine Windows-Version des Pakets vorhanden ist: [abrufen, die richtige Paketversion und Format](#packageVersion)

+ Wenn der Server nicht über Internetzugriff verfügt, müssen Sie die Windows-Binärdateien im Voraus herunterladen: [Download Zip-Dateien](#bkmk_zipPreparation)

+ Identifizieren Sie paketabhängigkeiten an. 

    - Wenn der Server über Internetzugriff verfügt, müssen Sie nicht kümmern Abhängigkeiten; alle erforderlichen Pakete können automatisch installiert werden.

    - Wenn der Server nicht **nicht** Zugriff auf das Internet haben, müssen Sie alle Abhängigkeiten identifizieren und die erforderlichen Pakete im Voraus in komprimierten Format herunterladen. Eine einfache Möglichkeit hierzu ist die Verwendung [MiniCRAN](create-a-local-package-repository-using-minicran.md) So bereiten Sie eine Auflistung von Paketen mit alle Abhängigkeiten vor. Dieses Repository kann dann mit dem Servercomputer kopiert werden.

+ Überprüfen Sie die Kompatibilität von Paketen. Das Paket sollte mit der Version von R kompatibel sein, die in SQL Server ausgeführt wird.

    Prüfen Sie außerdem, ob das Paket (oder sämtliche Pakete, die dafür) Funktionen enthält, die von SQL Server oder von der Richtlinie blockiert werden würde. Bestimmte Pakete sind z. B. eine schlechte Anpassung für eine gesicherte SQL Server-Umgebung. Solche Pakete können Pakete, die Zugriff auf das Netzwerk einschließen, die mit Java oder andere Frameworks, die in einer SQL Server-Umgebung oder Pakete, die mit erhöhten Rechten Dateisystemzugriff erfordern normalerweise nicht verwendet.

+ Berechtigungen

    Administratorzugriff auf dem Computer mit SQL Server ist erforderlich.

    Darüber hinaus müssen zum Ausführen in SQL Server Pakete in der Standardbibliothek installiert sein, die der aktuellen Instanz zugeordnet ist. Anleitungen zum Suchen der Standardbibliothek finden Sie unter [R-Pakete, die mit SQL Server installierten](installing-and-managing-r-packages.md).
    
    Wenn Sie ein erfahrener R-Benutzer sind, können Sie beim Installieren von Paketen über die Befehlszeile ohne spezielle Berechtigungen, oder sie zuvor herunterzuladen sein. Diese Methode funktioniert jedoch nicht in SQL Server. In vielen Fällen SQL Server müssen eine Internetverbindung Computer keine. Darüber hinaus den Zugriff auf Dateien oder externer Speicher kann eingeschränkt werden. Pakete, die in einer Benutzerbibliothek installiert, können durch R-Aufträge Runnign in SQL Server zugegriffen werden. 

    Wenn Sie administrativen Zugriff auf die SQL Server-Computer besitzen, finden Sie ein Datenbankadministrator, Paketinstallation verwenden können.

+ Führen Sie für jede Instanz, in dem Sie das Paket verwenden müssen separat Installation.

     Pakete können nicht über Instanzen freigegeben werden. Können Sie zum Installieren des Pakets separate Instanzen der gleichen Quelle für die ZIP-Datei, aber eine separate Kopie des Pakets wird jede Instanz-Bibliothek hinzugefügt.

## <a name="install-packages"></a>Installieren von Paketen

Dieser Abschnitt enthält die Paket-Installationsschritte für die folgenden Szenarien:

+ [Installieren Sie neue Pakete auf einem Server mit Internetzugriff](#bkmk_rInstall)
+ [Führen Sie eine offline-Installation von Paketen auf einem Server mit **keine** Zugang zum Internet](#bkmk_offlineInstall)
+ [Installieren der Pakete in einer SQL Server-computekontext mithilfe von RevoScaleR](#bkmk_rAddPackage)
+ [Installieren von Paketen, die mit der Anweisung externe Bibliothek erstellen](#bkmk_createlibrary) (nur SQL Server-2017; andere Einschränkungen gelten)

### <a name="bkmk_rInstall"></a>Online-Installation mithilfe von R-tools

Standard-R-Tools können Sie um neue Pakete auf einer Instanz von SQL Server 2016 oder 2017 von SQL Server zu installieren. Allerdings müssen Sie ein Administrator dazu sein.

1.  Navigieren Sie zu dem Ordner auf dem Server, auf dem R-Bibliotheken für die Instanz installiert werden.

    > [!IMPORTANT] 
    > Achten Sie darauf, dass Pakete in der Standardbibliothek installieren, die der aktuellen Instanz zugeordnet ist. Installieren Sie Pakete niemals ein Verzeichnis des Benutzers.

    Wenn Sie nicht über die erforderlichen Berechtigungen verfügen, wenden Sie sich an den Datenbankadministrator, und geben Sie eine Liste der Pakete, die Sie benötigen.

2.  Öffnen Sie eine R-Eingabeaufforderung als Administrator an.

    Z. B. bei Verwendung der Windows-Eingabeaufforderung, navigieren Sie in das Verzeichnis, in dem sich RTerm.Exe "oder" RGui.exe befinden. 

    **Standardinstanz**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **Benannte Instanz**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

    Wenn Sie die Bindung so aktualisieren Sie die Machine learning-Komponenten verwendet haben, kann der Pfad geändert. Überprüfen Sie den instanzpfad immer vor der Installation von neuen Paketen. 

3.  Führen Sie den Befehl R `install.packages` zum Installieren des Pakets. Die folgende Anweisung installiert z. B. das beliebte e1071-Paket. 

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    Doppelte Anführungszeichen sind erforderlich, für den Paketnamen.

4. Wenn Sie nach einer gespiegelten Site gefragt werden, wählen Sie einen Standort, der für Ihren Standort zweckmäßig ist.

5. Wenn das Zielpaket von weiteren Paketen abhängig ist, die R-Installationsprogramm automatisch die Abhängigkeiten für herunter und installiert sie Sie.

> [!IMPORTANT]
> Führen Sie für jede Instanz, in dem Sie das Paket verwenden müssen separat Installation. Pakete können nicht über Instanzen freigegeben werden.

### <a name = "bkmk_offlineInstall"></a>Offline-Installation mithilfe von R-tools 

Wenn das Paket, das Sie installieren möchten Abhängigkeiten, Vorbereiten **alle** benötigte Pakete voraus.  Finden Sie unter der [Tipps zur Installation](#bkmk_tips) Abschnitt Hilfe zum Vorbereiten der Pakete.

> [!IMPORTANT]
>  Wenn Sie Pakete auf einem Server, die keinen Zugang zum Internet hat installieren, es ist wichtig, dass Sie vollständige Abhängigkeiten im Voraus analysieren, und stellen Sie sicher, dass Sie alle erforderlichen Pakete heruntergeladen haben **vor** mit der Installation beginnen. Wir empfehlen [MiniCRAN](https://mran.microsoft.com/package/miniCRAN) für diesen Prozess. Diese R-Paket kann es sich um eine Liste der Pakete, die Sie installieren möchten, Abhängigkeiten analysiert und ruft die ZIP-Dateien für Sie. MiniCRAN erstellt dann ein einzelnes Repository, das Sie in Server-Computer kopieren können.
> 
> Weitere Informationen finden Sie unter [erstellen Sie ein lokales Paket-Repository mit MiniCRAN](create-a-local-package-repository-using-minicran.md)

1. Kopieren Sie das Paket oder das Repository im ZIP-Format, in einer lokalen Freigabe, oder einen anderen Speicherort aus, die auf der Server zugreifen kann.

2.  Suchen Sie den Ordner auf dem Server, auf dem R-Bibliotheken für die Instanz installiert werden.

    Z. B. bei Verwendung der Windows-Eingabeaufforderung, navigieren Sie in das Verzeichnis, in dem sich RTerm.Exe "oder" RGui.exe befinden.

    **Standardinstanz**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **Benannte Instanz**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. Öffnen Sie eine R-Eingabeaufforderung als Administrator an.

4.  Führen Sie den Befehl R `install.packages` , und geben Sie das Paket oder Namen und den Speicherort der ZIP-Dateien.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Dieser Befehl extrahiert das R-Paket `mynewpackage` aus der lokalen ZIP-Datei, sofern Sie die Kopie im Verzeichnis gespeichert ist `C:\Temp\Downloaded packages`, und das Paket auf dem lokalen Computer installiert. Wenn das Paket keine Abhängigkeiten enthält, überprüft das Installationsprogramm für vorhandene Pakete in der Bibliothek. Wenn Sie ein Repository, die die Abhängigkeiten enthält erstellt haben, installiert das Installationsprogramm die Requireed-Pakete.

    Wenn alle erforderlichen Pakete in der Bibliothek für die Instanz nicht vorhanden sind und können nicht in die ZIP-Dateien gefunden werden, schlägt fehl, die Installation des Ziel-Pakets.

### <a name="bkmk_rAddPackage"></a>Installieren von R-Pakete auf einem Server von einem Remoteclient von R

Bei neueren Versionen von [R-Server "oder" Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server), "revoscaler" beinhaltet Funktionen, die Installation von neuen R-Pakete in einer SQL Server-computekontext unterstützt. 

1. Bevor Sie beginnen, stellen Sie sicher, dass diese Bedingungen erfüllt sind:

    + Der Client hat RevoScale 9.0.1 oder höher.
    + Eine entsprechende Version von "revoscaler" wurde auf SQL Server-Instanz installiert.
    + Die [Paket Verwaltungsfeature](..\r\r-package-how-to-enable-or-disable.md) für die Instanz aktiviert wurde.
    + Sie sind Mitglied einer Datenbankrolle, die Ihnen ermöglicht, die Pakete in einer gemeinsam genutzten oder Prvate-Kontext für die angegebene Instanz und Ddatabase zu installieren.

2. Über eine Befehlszeile R definieren Sie eine Verbindungszeichenfolge für die Instanz und die Datenbank um, und verwenden Sie die Verbindungszeichenfolge mit den [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) Konstruktor zum Erstellen eines SQL Server-computekontext.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. Erstellen Sie eine Liste der Pakete, die Sie verwenden möchten, installieren, und speichern Sie die Liste in einer Zeichenfolgenvariablen.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. Rufen Sie [RxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) und übergeben des computekontexts und die Zeichenfolgenvariable, die mit den Paketnamen.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Wenn die abhängigen Programme erforderlich sind, werden sie auch installiert, vorausgesetzt, dass eine Internetverbindung verfügbar ist.
    
    In diesem Beispiel weil der Besitzer und der Gültigkeitsbereich wurde nicht angegeben, werden Pakete installiert mit den Anmeldeinformationen des Benutzers vornimmt, die Verbindung in den Standardbereich für diesen Benutzer.

### <a name="bkmk_createlibrary"></a>Verwenden Sie MiniCRAN Repository und externe Bibliothek erstellen, um Pakete zu installieren 

SQL Server-2017 bietet neue Features für die Installation und Verwaltung von R-Pakete, die mithilfe des T-SQL. Dieser Prozess erfordert jedoch, dass ein Paket verfügbar sein, da es sich bei eine lokalen ZIP-Datei, anstatt Sie aus dem Internet herunterzuladen. Die Anweisung schlägt fehl, wenn alle Pakete im Voraus nicht vorbereitet werden.

EXTERNE Bibliothek erstellen, wird unter diesen Umständen unterstützt:

+ Installieren Sie ein einzelnes Paket ohne Abhängigkeiten
+ Sie mehrere Pakete oder Pakete mit Abhängigkeiten installieren und alle Pakete im Voraus vorbereitet haben. 

**Schritte**

1.  Bereiten Sie das Paket im ZIP-Format vor, oder erstellen Sie ein MiniCRAN-Repository, das Paket und seine Abhängigkeiten enthält.  

2. Kopieren Sie die ZIP-Datei oder das Repository in einen lokalen Ordner auf dem Server.

     > [!IMPORTANT]
     > Die Datei, die Sie angeben, wie die Quelle der Zielpaket sowie alle zugehörigen erforderlichen Pakete enthalten muss.

3. Führen Sie als Administrator die T-SQL-Anweisung `CREATE EXTERNAL LIBRARY` zum Hochladen von ZIP-Paket-Auflistung in der Datenbank.

    Die folgende Anweisung verweist, beispielsweise ein MiniCRAN-Repository, die die RandomForest-Paket und seine Abhängigkeiten enthält. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    Sie können einen beliebigen Namen in der CREATE-Anweisung keine; den Namen der externen muss den gleichen Namen haben, den voraussichtlich verwenden, wenn beim Laden oder das Paket aufgerufen.

4. Installieren Sie oder mehrere Pakete für die Verwendung mit SQL Server kann durch Ausführen von Code innerhalb einer gespeicherten Prozedur.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    Bei erfolgreicher Ausführung der **Nachrichten** Fenster sollte eine Nachricht melden, z. B. "Paket"RandomForest"wurde erfolgreich entpackt und MD5 Summen überprüft" und "Fertig gestellt Ausführung verkettet".

    Wenn die Installation fehlschlägt, alle Pakete fehl Installation, und nachfolgende Versuche, Paketinstallation installiert möglicherweise auch mit dieser Nachricht: 

    "Fehler im RxSqlPkgInstallPackages... Fehler beim Installieren der Pakete - Konsolenfehlerprotokoll überprüfen Sie"

## <a name="package-installation-tips-and-frequently-asked-questions-faq"></a>Tipps zur Installation des Pakets und häufig gestellte Fragen (FAQ)

Dieser Abschnitt enthält verschiedene Tipps und häufig gestellte Fragen im Zusammenhang mit der Installation von R-Paket für SQL Server.

###  <a name="packageVersion"></a>Rufen Sie die richtige Paketversion und format

Es gibt mehrere Quellen für R-Pakete. Die bekannteste Quellen sind CRAN und Bioconductor. Auf der offiziellen Website für die R-Sprache (<https://www.r-project.org/>) sind viele dieser Ressourcen aufgeführt. Viele Pakete werden in GitHub veröffentlicht, in dem Sie den Quellcode erhalten können. Aber können Sie R-Pakete zugewiesen wurde, die von einer Person in Ihrem Unternehmen entwickelt wurden.

Unabhängig von der Quelle müssen Sie sicherstellen, dass das Paket, das Sie installieren möchten, ein binäres Format für die Windows-Plattform verfügt. Andernfalls kann nicht das heruntergeladene Paket in der SQL Server-Umgebung ausgeführt.

### <a name="bkmk_zipPreparation"></a>Das Paket als ZIP-Datei herunterladen

Für die Installation auf einem Server ohne Internetzugriff müssen Sie eine Kopie des Pakets in das Format einer ZIP-Datei für die Offlineinstallation herunterladen. Entzippen Sie das Paket nicht.

Z. B. das folgende Verfahren beschreibt jetzt, um die richtige Version von den [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) Paket von Bioconductor, vorausgesetzt, der Computer über Internetzugriff verfügt.

1.  Suchen Sie in der Liste der **Paketarchive** die **Windows-Binärdateiversion** .

2.  Mit der rechten Maustaste des Links, um die. ZIP-Datei, und wählen **Ziel speichern unter**.

3.  Navigieren Sie zu den lokalen Ordner, in dem komprimierten Pakete gespeichert sind, und klicken Sie auf **speichern**.

    Dieser Vorgang erstellt eine lokale Kopie des Pakets. Wenn Sie einen Download-Fehler erhalten, versuchen Sie eine andere gespiegelte Site aus.

4. Nachdem das Archiv Paket heruntergeladen wurde, können Sie installieren Sie das Paket oder kopieren das ZIP-Paket auf einen Server, die über keinen Zugriff auf das Internet.

> [!TIP]
> Wenn versehentlich des Pakets installieren anstelle eines Downloads von Binärdateien wird eine Kopie der heruntergeladene ZIP-Datei auch auf Ihrem Computer gespeichert. Beobachten Sie die statusmeldungen aus, während das Paket installiert wird, um den Dateispeicherort zu bestimmen. Sie können diese ZIP-Datei an den Server kopieren, die über keinen Zugriff auf das Internet.
> Wenn Sie mit dieser Methode Paket heruntergeladen haben, sind die paketabhängigkeiten nicht enthalten. 

Für Weitere Informationen zum Inhalt der Zip-Dateiformats und wie Sie ein R-Paket erstellen, empfehlen wir dieses Lernprogramm, das Sie im PDF-Format aus der R-Projektwebsite herunterladen können: [R-Pakete erstellen](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf).

### <a name="bkmk_packageDependencies"></a>Abrufen von paketabhängigkeiten

R-Pakete hängen häufig mehrere andere Pakete, von die einige möglicherweise nicht verfügbar in der Standardeinstellung R-Bibliothek, die von der Instanz verwendet. In einigen Fällen erfordert ein Paket eine andere Version von ein abhängiges Paket, das bereits installiert ist.

Wenn Sie müssen zum Installieren mehrerer Pakete, oder möchten, stellen Sie sicher, dass jeder einzelne in Ihrem Unternehmen die richtigen Pakettyp und Version erhält, wir empfehlen die Verwendung der [MiniCRAN](https://mran.microsoft.com/package/miniCRAN) Paket auf ein lokales Repository zu erstellen, die gemeinsam genutzt werden kann auf mehrere Benutzer oder Computer. Weitere Informationen finden Sie unter [erstellen Sie ein lokales Paket-Repository mit MiniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="permissions"></a>Berechtigungen

Dieser Abschnitt beschreibt das verschiedene Maß für die Installation von Paketen in SQL Server 2016 und SQL Server-2017 erforderlichen Berechtigungen. Installation erfolgen kann mithilfe von R-Tools oder SQL Server, jedoch den Prozess und die Berechtigungen unterscheiden sich geringfügig.

-   SQL Server 2016

    In dieser Version kann nur ein Administrator auf dem Computer Pakete an den erforderlichen Speicherort installieren. Sie standard-R-Tools verwenden, um Pakete zu installieren, aber Sie müssen als Administrator ausführen und den R-Tools, die der Instanz zugeordnet.

-   SQL Server 2017

    Wenn Sie administrativen Zugriff haben, können Sie Pakete auf einer Instanz serverweit installieren, mithilfe von R-Tools.

    Wenn Sie ein Datenbankbesitzer sind, können Sie R-Pakete von einem Remoteclient aus installieren, wenn Sie eine Verbindung definieren und RxInSqlServer mit der Instanz herstellen.
    
    Diese Version enthält neue Features zur Verwaltung von R oder Python-Pakete von Datenbankadministratoren in zukünftigen Versionen zu unterstützen. Um dieses Feature zu verwenden, muss ein Datenbankadministrator Paket-Verwaltungsfunktionen auf Instanzebene zuerst aktivieren. Nachdem diese Funktion aktiviert ist, können einzelne Benutzer Pakete mit einer bestimmten Datenbank, abhängig von ihrer Datenbankrolle installieren. Weitere Informationen finden Sie unter [aktivieren oder Deaktivieren der Verwaltung von R-Paket für SQL Server](../r/r-package-how-to-enable-or-disable.md).

> [!IMPORTANT]
> 
> Erfahrene Benutzer von R sind daran gewöhnt, zum Installieren von Paketen in einer Benutzerbibliothek und verweisen auf das Paket in diesem Ordner als Teil der R-Lösung, indem Sie einen Dateipfad angeben. Dieses Vorgehen wird jedoch nicht in SQL Server unterstützt. Weitere Informationen und problemumgehungen finden Sie unter [zum Verwenden von Paketen in benutzerbibliotheken](packages-installed-in-user-libraries.md).

### <a name="establish-a-single-mirror-site-as-standard"></a>Einrichten einer einzelnen gespiegelten Site als standard

Um nicht jedes Mal, wenn Sie ein neues Paket hinzufügen, eine gespiegelte Site auswählen zu müssen, können Sie die R-Entwicklungsumgebung so konfigurieren, dass immer dasselbe Repository verwendet wird. Hierzu bearbeiten Sie die globale R-Einstellungsdatei **. Rprofile**, und fügen Sie die folgende Zeile hinzu:

`options(repos=structure(c(CRAN="<mirror site URL>")))`

Aktueller CRAN-Spiegel werden auch auf [Websiteansicht](https://cran.r-project.org/mirrors.html).

Führen Sie für ausführliche Informationen zu Voreinstellungen und anderen Dateien geladen, wenn die Laufzeit von R startet diesen Befehl aus einer R-Konsole aus:`?Startup`

### <a name="know-which-library-you-are-using-for-installation"></a>Wissen Sie, welche Bibliothek, die Sie für die Installation verwenden

Wenn Sie vor der Installation von alles zuvor die R-Umgebung auf dem Computer geändert haben, halten Sie einen Moment, und stellen Sie sicher, dass die R-Umgebungsvariable `.libPath` nur ein Pfad verwendet.

Dieser Pfad sollte auf den Ordner R_SERVICES für die Instanz verweisen. Weitere Informationen finden Sie unter [R-Pakete, die mit SQL Server installierten](installing-and-managing-r-packages.md).

### <a name="side-by-side-installation-with-r-server"></a>Seite-an-Seite-Installation mit R-Server

Wenn Sie Microsoft Machine Learning-Server (eigenständig) zusätzlich zu den SQL Server-Machine Learning-Services installiert haben, sollte Ihre Computer separate Installationen von R für die einzelnen Duplikate aller R-Tools und Bibliotheken verfügen.

> [!IMPORTANT]
> 
> Pakete, die in der Bibliothek R_SERVER installiert sind, werden nur von Microsoft R Server verwendet und nicht von SQL Server zugegriffen werden.
> 
> Achten Sie darauf, dass Sie verwenden die `R_SERVICES` Bibliothek Installieren von Paketen, die Sie in SQL Server verwenden möchten.

### <a name="how-to-determine-which-packages-are-already-installed"></a>Wie Sie ermitteln, welche Pakete bereits installiert sind?

 Finden Sie unter [R-Pakete, die mit SQL Server installiert](installing-and-managing-r-packages.md)