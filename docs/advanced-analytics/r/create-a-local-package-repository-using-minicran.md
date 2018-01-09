---
title: Erstellen Sie ein lokales Paket-Repository mit MiniCRAN | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: "4"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 066e09747684ede5837d93736f32792736b8985d
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="create-a-local-package-repository-using-minicran"></a>Erstellen Sie ein lokales Paket-Repository mit miniCRAN

Es gibt zwei Möglichkeiten, die Sie R-Pakete für die Installation auf einem Server ohne Internetzugriff vorbereiten können.

-   [Verwenden des MiniCRAN-Pakets für eine einzelne lokale Repository erstellt werden.](#bkmk_miniCRAN)

    Die [MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) erstellt eine intern konsistent Repository bestehend aus ausgewählten Pakete aus CRAN-ähnliche Repositorys. Der Benutzer gibt einen Satz von gewünschten Pakete und MiniCRAN rekursiv liest die Abhängigkeitsstruktur für diese Pakete und lädt nur die aufgelisteten Pakete und deren Abhängigkeiten.

    Sie können dieses lokale Repository auf den Server verschoben, und fahren Sie mit der Pakete zu installieren, ohne über das Internet.

-   [Manuell herunter, und kopieren Sie die Pakete nacheinander](#bkmk_manual)

    Sie können die Liste der abhängigen Pakete in der DESCRIPTION-Datei für das heruntergeladene Paket gefunden. 
    
    Allerdings Pakete aufgeführt, **Importe** möglicherweise Abhängigkeiten der zweiten Ebene. Aus diesem Grund empfehlen die Verwendung von der **MiniCRAN** Methode.

> [!TIP]
> Wussten Sie, dass Sie zum Vorbereiten von Paketen für die Verwendung in Azure Machine Learning MiniCRAN verwenden können? Weitere Informationen finden Sie in diesem Blog: [MiniCRAN in Azure ML von Michele Usuelli verwenden](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="prepare-packages-using-minicran"></a>Vorbereiten von Paketen mit miniCRAN

Das Ziel zum Erstellen einer lokalen paketrepository ist an einen zentralen Ort zu bieten, den ein Serveradministrator oder anderen Benutzern in der Organisation verwenden können, um neue R-Pakete auf einem Server installieren, die über keinen Zugriff auf das Internet.

Die [MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) -Paket für R vom geschrieben wurde [Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html) verwaltete Satz von R-Pakete für eine Organisation erstellen Sie eine konsistente erleichtern. 

Es gibt viele Vorteile gegenüber der Verwendung von MiniCRAN Repository zu erstellen:

-   **Sicherheit**: viele R-Benutzer sind daran gewöhnt, zum Herunterladen und installieren neue R-Pakete werden, vom CRAN oder von einem Spiegel Standorte. Jedoch aus Sicherheitsgründen Produktionsservern ausgeführt [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] haben für gewöhnlich keine Internetverbindung.

-   **Einfacher Offlineinstallation**: beim Installieren des Pakets mit einem offline-Server erfordert, dass Sie auch alle paketabhängigkeiten herunterladen, mit MiniCRAN erleichtert es, rufen Sie alle Abhängigkeiten im richtigen Format ab.

-   **Verbesserte versionsverwaltung**: In einer mehrbenutzerumgebung, es gibt gute Gründe für die uneingeschränkte Paketversionen auf dem Server-Installation zu verhindern.

Nach dem Erstellen des Repositorys an, können Sie es durch Hinzufügen von neuen Paketen oder aktualisieren die Version der vorhandenen Pakete ändern.

> [!NOTE]
> Das MiniCRAN-Paket selbst ist abhängig von 18 anderen CRAN-Paketen, zwischen denen das Paket RCurl ist eine System-Abhängigkeit für das Paket Curl entwickl verfügt. Auf ähnliche Weise abhängt Paket-XML libxml2 entwickl. Wir empfehlen deshalb, Ihr lokale Repository anfangs auf einem Computer mit vollständigen Zugriff auf das Internet zu erstellen, damit Sie problemlos alle diese Abhängigkeiten erfüllen können. Nachdem Sie erstellt haben, können Sie das Repository an einen anderen Speicherort verschieben.

### <a name="step-1-install-the-minicran-package"></a>Schritt 1: Installieren Sie das Paket miniCRAN

Sie beginnen mit dem Erstellen ein Repository MiniCRAN als Quelle verwenden. Sie sollten dieses Repository auf einem Computer erstellen, die Zugang zum Internet hat.

1.  Installieren Sie das Paket MiniCRAN und die erforderlichen **Igraph** Paket.

    ```R
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
    ```

### <a name="step-2-define-a-package-source-a-cran-mirror-or-an-mran-snapshot"></a>Schritt 2: Definieren Sie eine Paketquelle: einen CRAN-Spiegel oder eine Momentaufnahme MRAN

1. Geben Sie eine gespiegelte Site beim Abrufen der Pakete verwenden.

    ```R
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
    ```

2.  Geben Sie den Namen von einem lokalen Ordner, in dem Sie die gesammelten Pakete zu speichern. 

    Achten Sie darauf, dass Sie den Ordner im Voraus erstellen. Ein Fehler wird ausgelöst, wenn die `local_repo` Ordner ist nicht vorhanden, wenn Sie später den R-Code ausführen.

    Der Ordner sollte es sich um einen beschreibenden Namen verfügen. Vermeiden Sie z. B. die Verwendung von "MiniCRAN", und geben Sie etwas stattdessen wie "GeneticsPackages" oder "TeamRPackages1.0.2".

    ```R
    local_repo <- "~/miniCRAN"
    ```

    Erweiterung Tilde-Operator gibt eine Umgebungsvariable mit Ergebnissen entspricht `Sys.getenv("R_USER")`.

### <a name="step-3-add-packages-to-the-repository"></a>Schritt 3: Hinzufügen von Paketen in das repository

1.  Nachdem MiniCRAN installiert ist, erstellen Sie eine Liste der zusätzlichen Pakete, die Sie herunterladen möchten.

    Dieser anfängliche Liste keine Abhängigkeiten hinzu; die **Igraph** Paket von MiniCRAN verwendet die Liste der Abhängigkeiten für Sie generiert. Weitere Informationen zur Verwendung der generierten Abhängigkeitsdiagramm finden Sie unter [MiniCRAN zum Identifizieren von paketabhängigkeiten verwendet](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

    Der folgende R-Skript wird das Abrufen von Ziel-Pakete, "Zoo" und "Planung" veranschaulicht.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```
2. Es ist nicht erforderlich, dass Sie das Abhängigkeitsdiagramm zeichnen, aber es kann sehr informativ sein.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Erstellen Sie das lokale Repository. Achten Sie darauf, dass Sie die R-Version bei Bedarf ändern.

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror)
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3")
    ```

    Aus diesen Informationen erstellt das MiniCRAN-Paket die Ordnerstruktur, die Sie benötigen, kopieren Sie die Pakete für die [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] später erneut.

4. An diesem Punkt sollten Sie einen Ordner, in dem Sie Pakete haben, und alle zusätzlichen Pakete, die erforderlich waren.

    Sie können den folgenden Code zum Auflisten von im Repository MiniCRAN enthaltenen Pakete ausführen.

    ```R
    pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE)
    head(pdb)
    pdb$Package
    pdb[, c("Package", "Version", "License")]
    ```

### <a name="step-4-use-the-repository-to-add-r-packages-to-the-instance-library"></a>Schritt 4. Verwenden Sie das Repository zum Hinzufügen von R-Pakete in der Instanz-Bibliothek

Nachdem Sie das Repository erstellt und die benötigten Pakete hinzugefügt haben, müssen Sie den paketrepository verschieben, auf dem Server-Computer und stellen Sie sicher, dass die R-Pakete in die richtige Bibliothek für die Verwendung von SQL Server installiert sind.

Abhängig von der Version von SQL Server stehen Ihnen zwei Optionen zum Hinzufügen von neuen Pakete in der SQL Server-Instanz zugeordneten R-Bibliothek:

- Installieren Sie die Instanz-Bibliothek, die mit dem MiniCRAN Repository und R-Tools.

- Hochladen Sie Pakete mit einer SQL Server-Datenbank, und installieren Sie die mit der Anweisung externe Bibliothek erstellen. Diese Option erfordert SQL Server-2017. Finden Sie unter [Installieren zusätzlicher R-Pakete unter SQL Server](install-additional-r-packages-on-sql-server.md).

Das folgende Verfahren beschreibt, wie die Pakete mithilfe von R-Tools zu installieren.

1. Kopieren Sie den Ordner mit dem Repository MiniCRAN in seiner Gesamtheit, mit dem Server, auf dem die Pakete installiert werden sollen.

2. Öffnen Sie eine R-Eingabeaufforderung mit dem R-Tool, das der Instanz zugeordnet.

    - Für SQL Server 2017 der Standardordner ist `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`.

    - Für SQL Server 2016 ist der Standardordner `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`.

    - Für eine benannte Instanz der Standardpfad wäre etwa: `<instance_path>.RTEST/R_SERVICES/library`.

    -  Wenn Sie SQL Server auf einem anderen Laufwerk installiert haben, oder andere Änderungen im Installationspfad vorgenommen haben, achten Sie darauf, dass Sie auch diese Änderungen übernehmen.

3.  Rufen Sie den Pfad für die Instanz-Bibliothek, und fügen Sie es der Liste der Library-Pfade.

    ```R
    .libPaths()[1]  
    lib \<- .libPaths()[1]
    ```

    Dieser Befehl sollte auf SQL Server, den Pfad der Bibliothek, die der Instanz zugeordnet sind, z. B. zurück: "c: / Program Programme/Microsoft SQL Server/MSSQL14. MSSQLSERVER/R_SERVICES/Library"

4.  Geben Sie den Speicherort auf dem Server, die Sie kopiert, in dem das Repository MininCRAN im haben `server_repo`.

    In diesem Beispiel wird davon ausgegangen, dass Sie das Repository Ordner "Benutzer" auf dem Server kopiert haben.

    ```R
    R server_repo <- "C:\\Users\\MyUserName\\miniCRAN"
    ```

5.  Da Sie in einem neuen R-Arbeitsbereich auf dem Server arbeiten, müssen Sie auch die Liste der Pakete zu installieren sind.

    ```R
    tspackages <- c("zoo", "forecast")
    ```

6.  Installieren Sie die Pakete, die den Pfad zur lokalen Kopie des Repositorys MiniCRAN bereitstellen.

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath(server_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE)
    ```

7.  Von der Instanz bereitgestellt werden können Sie die installierten Pakete, die mit einem Befehl wie folgt anzeigen:

    ```R
    installed.packages()
    ```

> [!NOTE] 
> In SQL Server muss ein Serveradministrator die Pakete aus dem Repository MiniCRAN in die Standardbibliothek, die von der Instanz verwendeten installieren. 

## <a name="manually-download-single-packages"></a>Manuelles Herunterladen von einzelnen Pakete

Wenn Sie nicht MiniCRAN verwenden möchten, können Sie die Pakete, die Sie benötigen, und ihre Abhängigkeiten auch manuell herunterladen. Zu diesem Zweck müssen Sie entweder ein Administrator oder der alleinige Besitzer eines Servers sind.

Nach dem Herunterladen der Pakete, installieren Sie die R-Pakete aus dem ZIP-Datei-Speicherort.

1. Herunterladen Sie die Pakete Zip-Dateien und in einem lokalen Ordner zu speichern.

2. Kopieren Sie diesen Ordner auf dem [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] Computer.

3. Installieren Sie die Pakete in der Bibliothek der SQL Server-Instanz.

> [!NOTE]
> Wenn Sie R-Tools verwenden, um Pakete zu installieren, werden sie als Ganzes für die Instanz installiert. 
> 
> Wenn Sie installieren das Paket in eine Datenbank und das Paket für Benutzer, die mithilfe von Datenbankrollen freigeben möchten, müssen Sie die Bibliothek, die mit der Anweisung externe Bibliothek erstellen hochladen. Finden Sie unter [Installieren zusätzlicher R-Pakete in SQL Server](install-additional-r-packages-on-sql-server.md)
