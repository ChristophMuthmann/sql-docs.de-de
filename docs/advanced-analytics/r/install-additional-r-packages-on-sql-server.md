---
title: Installieren Sie zusätzliche R-Pakete unter SQL Server | Microsoft Docs
ms.date: 03/05/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 79f62f394b31349308e9e67b3b0fe45bc57cff78
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>Installieren Sie zusätzliche R-Pakete unter SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel beschreibt, wie neue R-Pakete mit einer Instanz von SQL Server installieren, Machine Learning aktiviert ist.

Es gibt mehrere Methoden zum Installieren von neuen R-Paketen, abhängig von Ihnen installierten Version von SQL Server, und gibt an, ob der Server über Internetzugriff verfügt.

+ [Installieren Sie neuer Pakete mithilfe von R-Tools mit Internetzugriff](#bkmk_rInstall)

    Verwenden Sie herkömmliche R-Befehle, um Pakete aus dem Internet zu installieren. Dies ist die einfachste Methode, jedoch ist Administratorzugriff erforderlich.

    **Gilt für:**[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]. Erforderlich, auch für Instanzen von [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] , in denen paketverwaltung über DDLs nicht aktiviert wurde.

+ [Installieren Sie neue R-Pakete auf einem Server mit **keine** Zugang zum Internet](#bkmk_offlineInstall)

    Wenn der Server nicht über Internetzugriff verfügt, sind einige zusätzliche Schritte erforderlich, um die Pakete vorzubereiten. Dieser Abschnitt beschreibt, wie die erforderlichen Dateien für die Installation des Pakets und seiner Abhängigkeiten vorbereitet.

+ [Installieren von Paketen, die mit der EXTERNEN Bibliothek erstellen-Anweisung](#bkmk_createlibrary) 

    Die [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) Anweisung finden Sie im SQL Server-2017, und es Ihnen ermöglicht, eine Paket-Bibliothek zu erstellen, ohne Ausführen von R oder Python-code direkt. Diese Methode erfordert jedoch, dass Sie alle erforderlichen Pakete im Voraus vorbereiten und zusätzliche Database-Berechtigungen erfordert.

    **Gilt für:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]; andere Einschränkungen gelten

## <a name="bkmk_rInstall"></a> Installieren Sie neue R-Pakete, die über das Internet

Standard-R-Tools können Sie um neue Pakete auf einer Instanz von SQL Server 2016 oder 2017 von SQL Server zu installieren. Dieser Vorgang setzt voraus, dass Sie ein Administrator auf dem Computer sind.

> [!IMPORTANT] 
> Achten Sie darauf, dass Pakete in der Standardbibliothek installieren, die der aktuellen Instanz zugeordnet ist. Installieren Sie Pakete niemals ein Verzeichnis des Benutzers.

Dieses Verfahren wird beschrieben, wie Sie mithilfe von "rgui.exe" Pakete installieren können; Sie können jedoch RTerm oder eine beliebige andere R Befehlszeilentool, die mit erhöhten Rechten Datenzugriff unterstützt.

### <a name="install-a-package-using-rgui-or-rterm"></a>Installieren eines Pakets mithilfe von "rgui.exe" oder RTerm

1. Navigieren Sie zu dem Ordner auf dem Server, auf dem R-Bibliotheken für die Instanz installiert werden.

  **Standardinstanz**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **Benannte Instanz**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

  Wenn Sie die Bindung so aktualisieren Sie die Machine learning-Komponenten verwendet haben, kann der Pfad geändert. Überprüfen Sie den instanzpfad immer vor der Installation von neuen Paketen. 

2. RGui.exe Maustaste, und wählen **als Administrator ausführen**.

    Wenn Sie nicht über die erforderlichen Berechtigungen verfügen, wenden Sie sich an den Datenbankadministrator, und geben Sie eine Liste der Pakete, die Sie benötigen.

3. Über die Befehlszeile, wenn Sie wissen, dass der Paketname können Sie eingeben: `install.packages("the_package-name")` doppelte Anführungszeichen für den Paketnamen erforderlich sind.

4. Wenn Sie nach einer gespiegelten Site gefragt werden, wählen Sie einen Standort, der für Ihren Standort zweckmäßig ist.

5. Wenn das Zielpaket von weiteren Paketen abhängig ist, die R-Installationsprogramm automatisch die Abhängigkeiten für herunter und installiert sie Sie.

6. Führen Sie für jede Instanz, in dem Sie das Paket verwenden müssen separat Installation. Pakete können nicht über Instanzen freigegeben werden.

## <a name = "bkmk_offlineInstall"></a> Offline-Installation mithilfe von R-tools

Um die R-Pakete auf einem Server installieren, die nicht über Internetzugriff verfügt, müssen Sie folgende Aktionen ausführen:

+ Analysieren Sie die Abhängigkeiten im voraus.
+ Das Zielpaket auf einem Computer mit Internetzugriff herunterladen.
+ Herunterladen Sie alle erforderlichen Pakete auf dem gleichen Computer, und fügen Sie alle Pakete in ein einzelnes Paket-Archiv.
+ ZIP-Archiv, ist er nicht bereits im ZIP-Format.
+ Kopieren Sie das Archiv Paket an einen Speicherort auf dem Server.
+ Installieren Sie das Zielpaket, das die Archivdatei als Quelle angeben.

> [!IMPORTANT] 
> > Achten Sie darauf, dass Sie alle Abhängigkeiten analysieren und herunterladen **alle** benötigte Pakete **vor** mit der Installation beginnen. Wir empfehlen [MiniCRAN](https://mran.microsoft.com/package/miniCRAN) für diesen Prozess. Diese R-Paket kann es sich um eine Liste der Pakete, die Sie installieren möchten, Abhängigkeiten analysiert und ruft die ZIP-Dateien für Sie. MiniCRAN erstellt dann ein einzelnes Repository, das Sie in Server-Computer kopieren können.
> 
> Weitere Informationen finden Sie unter [erstellen Sie ein lokales Paket-Repository mit MiniCRAN](create-a-local-package-repository-using-minicran.md)

Dieses Verfahren setzt voraus, dass Sie alle Pakete vorbereitet haben, im ZIP-Format müssen und sind bereit, die sie auf den Server kopiert.

1. Kopieren Sie das Paket ZIP-Datei, oder für mehrere Pakete vollständige Repository, enthält alle Pakete im ZIP-Format an einen Speicherort, den auf der Server zugreifen kann.

2. Öffnen Sie den Ordner auf dem Server, auf dem R-Bibliotheken für die Instanz installiert werden. Z. B. bei Verwendung der Windows-Eingabeaufforderung, navigieren Sie in das Verzeichnis, in dem sich RTerm.Exe "oder" RGui.exe befinden.

  **Standardinstanz**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **Benannte Instanz**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. Mit der rechten Maustaste auf die "rgui.exe" oder der Befehlszeile aus, und wählen Sie **als Administrator ausführen**.

4. Führen Sie den Befehl R `install.packages` , und geben Sie das Paket oder Namen und den Speicherort der ZIP-Dateien.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Dieser Befehl extrahiert das R-Paket `mynewpackage` aus der lokalen ZIP-Datei, sofern Sie die Kopie im Verzeichnis gespeichert ist `C:\Temp\Downloaded packages`, und das Paket auf dem lokalen Computer installiert. Wenn das Paket keine Abhängigkeiten enthält, überprüft das Installationsprogramm für vorhandene Pakete in der Bibliothek. Wenn Sie ein Repository, die die Abhängigkeiten enthält erstellt haben, installiert das Installationsprogramm die erforderlichen Pakete auch an.

    Wenn alle erforderlichen Pakete in der Bibliothek für die Instanz nicht vorhanden sind und können nicht in die ZIP-Dateien gefunden werden, schlägt fehl, die Installation des Ziel-Pakets.

## <a name="bkmk_createlibrary"></a> Verwenden Sie eine DDL-Anweisung, um ein Paket installieren 

In SQL Server-2017, können Sie die [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) Anweisung, um ein Paket oder eine Reihe von Paketen auf einer Instanz oder eine bestimmte Datenbank hinzufügen. Diese DDL-Anweisung und die unterstützenden Rollen dienen zur Vereinfachung Installation und Verwaltung von Paketen durch Datenbankbesitzer ohne R oder Python-Tools verwenden zu müssen.

Dieser Prozess erfordert einige Vorbereitung, im Vergleich zur Installation von Paketen mit konventionellen R oder Python-Methoden.

+ Alle Pakete werden muss als eine lokale ZIP-Datei verfügbar, anstatt aus dem Internet herunterladen.

    Wenn Sie keinen Zugriff auf das Dateisystem auf dem Server haben, können Sie auch ein vollständiges Paket als Variable übergeben mit einem binary-Format. Weitere Informationen finden Sie unter [externe Bibliothek erstellen](../../t-sql/statements/create-external-library-transact-sql.md).

+ Die Anweisung schlägt fehl, falls erforderlich, dass die Pakete nicht verfügbar sind. Sie müssen die Abhängigkeiten des Pakets analysieren, die Sie verwenden möchten, und vergewissern Sie sich, dass die Pakete auf dem Server und Datenbank hochgeladen werden. Es wird empfohlen, **MiniCRAN** oder **Igraph** zum Analysieren von Paketen Abhängigkeiten.

+ Sie müssen die erforderlichen Berechtigungen für die Datenbank verfügen. Weitere Informationen finden Sie unter [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

### <a name="prepare-the-packages-in-archive-format"></a>Vorbereiten der Pakete im Archivformat

1. Wenn Sie ein einzelnes Paket installieren, wird herunterladen Sie das Paket im ZIP-Format. 

2. Wenn das Paket andere Pakete erfordert, müssen Sie sicherstellen, dass die erforderlichen Pakete verfügbar sind. Sie können MiniCRAN analysieren Das Zielpaket und identifizieren alle abhängigen Elemente. 

3. Kopieren Sie die ZIP-Dateien oder MiniCRAN Repository, alle Pakete in einen lokalen Ordner auf dem Server enthält.

4. Öffnen einer **Abfrage** Fenster mit einem Konto mit Administratorrechten aus.

5. Führen Sie die T-SQL-Anweisung `CREATE EXTERNAL LIBRARY` zum Hochladen von ZIP-Paket-Auflistung in der Datenbank.

    Die folgende Anweisung benennt beispielsweise als Paketquelle eine MiniCRAN "Repository" enthält die **RandomForest** -Paket, zusammen mit seiner Abhängigkeiten. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    Sie können keinen beliebigen Namen verwenden. den Namen der externen muss den gleichen Namen haben, den voraussichtlich verwenden, wenn beim Laden oder das Paket aufgerufen.

6. Wenn die Bibliothek erfolgreich erstellt wurde, können Sie das Paket in SQL Server ausführen, indem sie innerhalb einer gespeicherten Prozedur aufgerufen wird.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    library(randomForest)'
    ```

### <a name="known-issues-with-create-external-library"></a>Bekannte Probleme mit der EXTERNEN Bibliothek erstellen

EXTERNE Bibliothek erstellen, wird unter diesen Umständen unterstützt:

+ Installieren Sie ein einzelnes Paket ohne Abhängigkeiten.
+ Sie Pakete mit Abhängigkeiten installieren, und alle Pakete im Voraus vorbereitet haben. 

Die DDL-Anweisung schlägt fehl, wenn bestehende paketabhängigkeiten fehlen. Beispielsweise wird während des Installationsvorgangs bezeichnet, in diesen Fällen fehl:

+ Sie installiert ein Paket, das auf zweiter Ebene Abhängigkeiten aufweist, und die Analyse nicht auf zweiter Ebene Pakete erweitern. Angenommen, Sie installieren möchten **gglot2**, und identifiziert alle Pakete, die im Manifest aufgelisteten; diese Pakete jedoch eine andere Abhängigkeiten, die nicht installiert wurden.
+ Sie installiert einen Satz von Paketen, die andere Versionen eines unterstützenden Pakets erforderlich sind, und der Server hat die falsche Version.

## <a name="package-installation-tips"></a>Tipps zur Installation des Pakets

Dieser Abschnitt enthält verschiedene Tipps und häufig gestellte Fragen im Zusammenhang mit der Installation von R-Paket für SQL Server.

###  <a name="packageVersion"></a> Rufen Sie die richtige Paketversion und format

Es gibt mehrere Quellen für R-Pakete, z. B. CRAN und Bioconductor. Die offizielle Website für die Sprache "R" (<https://www.r-project.org/>) sind viele dieser Ressourcen aufgeführt. Viele Pakete werden in GitHub veröffentlicht, in dem Sie den Quellcode erhalten können. Schließlich, Sie können R-Pakete, die von einer Person in Ihrem Unternehmen entwickelt wurden angegeben wurde, oder Sie haben ein benutzerdefiniertes Paket an dem von das Ihnen geschriebenen.

Stellen Sie unabhängig von der Quelle bevor Sie versuchen, die zum Installieren des Pakets sicher, dass Sie mit das binary-Format für die Windows-Plattform erhalten haben. 

### <a name="bkmk_zipPreparation"></a> Das Paket als ZIP-Datei herunterladen

Für die Installation auf einem Server ohne Internetzugriff müssen Sie eine Kopie des Pakets in das Format einer ZIP-Datei für die Offlineinstallation herunterladen. **Entzippen Sie das Paket nicht.**

Z. B. das folgende Verfahren beschreibt jetzt, um die richtige Version von den [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) Paket von Bioconductor, vorausgesetzt, der Computer über Internetzugriff verfügt.

1.  Suchen Sie in der Liste der **Paketarchive** die **Windows-Binärdateiversion** .

2.  Mit der rechten Maustaste des Links, um die. ZIP-Datei, und wählen **Ziel speichern unter**.

3.  Navigieren Sie zu den lokalen Ordner, in dem komprimierten Pakete gespeichert sind, und klicken Sie auf **speichern**.

    Dieser Vorgang erstellt eine lokale Kopie des Pakets. 

4. Wenn Sie einen Download-Fehler erhalten, versuchen Sie eine andere gespiegelte Site aus.

5. Nachdem das Archiv Paket heruntergeladen wurde, können Sie installieren Sie das Paket oder kopieren das ZIP-Paket auf einen Server, die über keinen Zugriff auf das Internet.

> [!TIP]
> Wenn versehentlich des Pakets installieren anstelle eines Downloads von Binärdateien wird eine Kopie der heruntergeladene ZIP-Datei auch auf Ihrem Computer gespeichert. Beobachten Sie die statusmeldungen aus, während das Paket installiert wird, um den Dateispeicherort zu bestimmen. Sie können diese ZIP-Datei an den Server kopieren, die über keinen Zugriff auf das Internet.
> 
> Wenn Sie Pakete, die mit dieser Methode abgerufen haben, sind die Abhängigkeiten nicht enthalten. 

### <a name="bkmk_packageDependencies"></a> Abrufen der erforderlichen Pakete

R-Pakete hängen häufig mehrere andere Pakete, von die einige möglicherweise nicht verfügbar in der Standardeinstellung R-Bibliothek, die von der Instanz verwendet. In einigen Fällen erfordert ein Paket eine andere Version von ein abhängiges Paket, das bereits installiert ist.

Wenn Sie müssen zum Installieren mehrerer Pakete, oder möchten, stellen Sie sicher, dass jeder einzelne in Ihrem Unternehmen die richtigen Pakettyp und Version erhält, wir empfehlen die Verwendung der [MiniCRAN](https://mran.microsoft.com/package/miniCRAN) Paket, um die vollständige Abhängigkeitskette zu analysieren. MinicRAN erstellt ein lokales Repository, das für mehrere Benutzer oder Computer freigegeben werden kann. Weitere Informationen finden Sie unter [erstellen Sie ein lokales Paket-Repository mit MiniCRAN](create-a-local-package-repository-using-minicran.md).


### <a name="know-which-library-you-are-using-for-installation"></a>Wissen Sie, welche Bibliothek, die Sie für die Installation verwenden

Wenn Sie vor der Installation von alles zuvor die R-Umgebung auf dem Computer geändert haben, halten Sie einen Moment, und stellen Sie sicher, dass die R-Umgebungsvariable `.libPath` nur ein Pfad verwendet.

Dieser Pfad sollte auf den Ordner R_SERVICES für die Instanz verweisen. Weitere Informationen finden Sie unter [R-Pakete, die mit SQL Server installierten](installing-and-managing-r-packages.md).

### <a name="side-by-side-installation-with-r-server"></a>Seite-an-Seite-Installation mit R-Server

Wenn Sie Microsoft Machine Learning-Server (eigenständig) zusätzlich zu den SQL Server-Machine Learning-Services installiert haben, sollte Ihre Computer separate Installationen von R für die einzelnen Duplikate aller R-Tools und Bibliotheken verfügen.

Pakete, die in der Bibliothek R_SERVER installiert sind, werden nur von Microsoft R Server verwendet und nicht von SQL Server zugegriffen werden. Achten Sie darauf, dass Sie verwenden die `R_SERVICES` Bibliothek Installieren von Paketen, die Sie in SQL Server verwenden möchten.

### <a name="how-to-determine-which-packages-are-already-installed"></a>Wie Sie ermitteln, welche Pakete bereits installiert sind?

 Finden Sie unter [R-Pakete, die mit SQL Server installiert](installing-and-managing-r-packages.md)