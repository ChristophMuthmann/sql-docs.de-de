---
title: Erstellen Sie ein lokales Paket-Repository mit MiniCRAN | Microsoft Docs
titleSuffix: SQL Server
ms.custom: 
ms.date: 02/20/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9d0a234b0b1112ee01f6eb6c67979ae84d72fd92
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
# <a name="create-a-local-package-repository-using-minicran"></a>Erstellen Sie ein lokales Paket-Repository mit miniCRAN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Die [MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) Paket wurde erstellt, indem Andre de Vries auf die folgenden allgemeinen Szenarien zu unterstützen: 

+ Analysieren von paketabhängigkeiten für eine einzelnes Paket oder eine Gruppe von Paketen
+ Vorbereiten der einen Satz von R-Pakete für die Installation auf einem Server ohne Internetzugriff.

Der Benutzer gibt einen Satz von gewünschten Pakete und MiniCRAN rekursiv liest die Abhängigkeitsstruktur für diese Pakete, und nur die aufgelisteten Pakete und ihre Abhängigkeiten von CRAN oder ähnliche Repositorys herunterlädt.

Als Ausgabe verwenden erstellt MiniCRAN eine intern konsistent Repository bestehend aus der ausgewählten Pakete und alle erforderlichen Abhängigkeiten. Sie können dieses lokale Repository auf den Server verschoben, und fahren Sie mit der Pakete zu installieren, ohne über das Internet.

Erfahrene Benutzer von R werden häufig für die Liste der abhängigen Pakete in der DESCRIPTION-Datei für das heruntergeladene Paket suchen. Allerdings Pakete aufgeführt, **Importe** möglicherweise Abhängigkeiten der zweiten Ebene. Aus diesem Grund empfehlen die Verwendung von der **MiniCRAN** Methode.

## <a name="what-is-a-package-repository"></a>Was ist ein paketrepository

Das Ziel zum Erstellen einer lokalen paketrepository ist an einen zentralen Ort zu bieten, den ein Serveradministrator oder anderen Benutzern in der Organisation verwenden können, um neue R-Pakete auf einem Server installieren, die über keinen Zugriff auf das Internet. Nach dem Erstellen des Repositorys an, können Sie es durch Hinzufügen von neuen Paketen oder aktualisieren die Version der vorhandenen Pakete ändern.

Die [MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) -Paket für R vom geschrieben wurde [Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html) verwaltete Satz von R-Pakete für eine Organisation erstellen Sie eine konsistente erleichtern. 

Paket-Repositorys sind in diesen Szenarien nützlich:

- **Sicherheit**: viele R-Benutzer sind daran gewöhnt, zum Herunterladen und installieren neue R-Pakete werden, vom CRAN oder von einem Spiegel Standorte. Jedoch aus Sicherheitsgründen Produktionsservern ausgeführt [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] haben für gewöhnlich keine Internetverbindung.

- **Einfacher Offlineinstallation**: beim Installieren des Pakets mit einem offline-Server erfordert, dass Sie auch alle paketabhängigkeiten herunterladen, mit MiniCRAN erleichtert es, rufen Sie alle Abhängigkeiten im richtigen Format ab.

    Mithilfe von MiniCRAN können Sie Paket Abhängigkeit Fehler vermeiden, bei der Vorbereitung der Pakete für die Installation mit den [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) Anweisung.

- **Verbesserte versionsverwaltung**: In einer mehrbenutzerumgebung, es gibt gute Gründe für die uneingeschränkte Paketversionen auf dem Server-Installation zu verhindern. Verwenden Sie ein lokales Repository, um ein konsistenter Satz von Paketen für die Verwendung durch Ihre Analytiker bereitzustellen. 

> [!TIP]
> Sie können auch MiniCRAN Vorbereiten von Paketen für die Verwendung in Azure Machine Learning verwenden. Weitere Informationen finden Sie in diesem Blog: [MiniCRAN in Azure ML von Michele Usuelli verwenden](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="prepare-packages-using-minicran"></a>Vorbereiten von Paketen mit miniCRAN

Die **MiniCRAN** Paket selbst 18 CRAN-Paketen abhängig ist zwischen also die **RCurl** Paket, das von einem System abhängig ist auf die **Curl entwickl** Paket. Auf ähnliche Weise Paket **XML** abhängt **libxml2 entwickl**. 

Aus diesen Gründen empfohlen, dass Sie Ihr lokale Repository anfangs auf einem Computer mit vollständigen Zugriff auf das Internet zu erstellen, damit Sie problemlos alle diese Abhängigkeiten erfüllen können. 

Nachdem das Repository erstellt wurde, können Sie das Repository an einen anderen Speicherort verschieben.

### <a name="step-1-install-the-minicran-package"></a>Schritt 1: Installieren Sie das Paket miniCRAN

Zunächst erstellen Sie eine **MiniCRAN** Repository, das als Quelle verwendet. Sie sollten dieses Repository auf einem Computer erstellen, die Zugang zum Internet hat.

1. Installieren der **MiniCRAN** Paket und das erforderliche **Igraph** Paket. In diesem Beispiel wird überprüft, ob das Paket bereits installiert ist, können Sie die If umgeht jedoch Anweisungen und Installieren der Pakete direkt.

    ```R
    if(!require("miniCRAN")) install.packages("miniCRAN") 
    if(!require("igraph")) install.packages("igraph") 
    library("miniCRAN")
    ```

### <a name="step-2-define-a-package-source-a-cran-mirror-or-an-mran-snapshot"></a>Schritt 2: Definieren Sie eine Paketquelle: einen CRAN-Spiegel oder eine Momentaufnahme MRAN

1. Geben Sie eine gespiegelte Site beim Abrufen der Pakete verwenden. Z. B. können die MRAN-Website, oder einen anderen Standort in Ihrer Region Sie, die die Pakete enthält, die Sie benötigen. Wenn der Downloadvorgang abgebrochen, versuchen Sie eine andere gespiegelte Site aus.

    ```R
    CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
    CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
    ```

2. Geben Sie den Namen von einem lokalen Ordner, in dem Sie die gesammelten Pakete zu speichern. 

    Achten Sie darauf, dass Sie den Ordner im Voraus erstellen. Ein Fehler wird ausgelöst, wenn die `local_repo` Ordner ist nicht vorhanden, wenn Sie später den R-Code ausführen.

    Der Ordner sollte es sich um einen beschreibenden Namen verfügen. Hier haben wir "MiniCRAN" verwendet, aber wenn Sie dies oft wiederholen, verwenden Sie wahrscheinlich einen aussagekräftigeren Namen, z. B. "MiniCRANZooPackages" oder "miniCRANMyRPackagev2".

    ```R
    local_repo <- "~/miniCRAN"
    ```

    Erweiterung Tilde-Operator gibt eine Umgebungsvariable mit Ergebnissen entspricht `Sys.getenv("R_USER")`.

### <a name="step-3-add-packages-to-the-repository"></a>Schritt 3: Hinzufügen von Paketen in das repository

1. Nach dem **MiniCRAN** ist installiert, erstellen Sie eine Liste, der angibt, die weitere Pakete heruntergeladen werden soll.

    Führen Sie **nicht** Abhängigkeiten zu dieser anfänglichen Liste hinzufügen. Die **Igraph** Paket, die von **MiniCRAN** die Liste der Abhängigkeiten für Sie generiert. Weitere Informationen zur Verwendung der generierten Abhängigkeitsdiagramm finden Sie unter [MiniCRAN zum Identifizieren von paketabhängigkeiten verwendet](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

    Der folgende R-Skript fügt die Ziel-Pakete, "Zoo" und "Planung", um eine Variable hinzu.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```
2. Es ist nicht erforderlich, dass Sie das Abhängigkeitsdiagramm zeichnen, aber es kann sehr informativ sein.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Erstellen Sie das lokale Repository. Achten Sie darauf, dass Sie die R-Version bei Bedarf ändern.

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

    Aus diesen Informationen erstellt das MiniCRAN-Paket die Ordnerstruktur, die Sie benötigen, kopieren Sie die Pakete für die [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] später erneut.

4. An diesem Punkt sollten Sie einen Ordner, in dem Sie Pakete haben, und alle zusätzlichen Pakete, die erforderlich waren.

    Sie können den folgenden Code zum Auflisten von im Repository MiniCRAN enthaltenen Pakete ausführen.

    ```R
    pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
    head(pdb);
    pdb$Package;
    pdb[, c("Package", "Version", "License")]
    ```

### <a name="step-4-use-the-repository-to-add-r-packages-to-the-instance-library"></a>Schritt 4. Verwenden Sie das Repository zum Hinzufügen von R-Pakete in der Instanz-Bibliothek

Nachdem Sie das Repository erstellt und die benötigten Pakete hinzugefügt haben, müssen Sie den paketrepository verschieben, auf dem Server-Computer und stellen Sie sicher, dass die R-Pakete in die richtige Bibliothek für die Verwendung von SQL Server installiert sind.

Das folgende Verfahren beschreibt, wie die Pakete mithilfe von R-Tools zu installieren.

1. Kopieren Sie den Ordner mit dem Repository MiniCRAN in seiner Gesamtheit, mit dem Server, auf dem die Pakete installiert werden sollen. Der Ordner ist in der Regel für diese Struktur: MiniCRAN-Stamm > -> "bin" -> Windows -> für die Altersvorsorge nicht-Version > -> alle Pakete.

2. Öffnen Sie eine R-Eingabeaufforderung mit dem R-Tool, das der Instanz zugeordnet.

    - Für SQL Server 2017 der Standardordner ist `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`.

    - Für SQL Server 2016 ist der Standardordner `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`.

    - Für eine benannte Instanz der Standardpfad wäre etwa: `<instance_path>.RTEST/R_SERVICES/library`.

    -  Wenn Sie SQL Server auf einem anderen Laufwerk installiert haben, oder andere Änderungen im Installationspfad vorgenommen haben, achten Sie darauf, dass Sie auch diese Änderungen übernehmen.

3. Rufen Sie den Pfad für die Instanz-Bibliothek, und fügen Sie es der Liste der Library-Pfade.

    ```R
    .libPaths()[1];
    lib <- .libPaths()[1]
    ```

    Dieser Befehl sollte auf SQL Server, den Pfad der Bibliothek, die der Instanz zugeordnet sind, z. B. zurück: "c: / Program Programme/Microsoft SQL Server/MSSQL14. MSSQLSERVER/R_SERVICES/Library"

4. Geben Sie den neuen Speicherort auf dem Server, in denen Sie kopiert, die **MiniCRAN** -Repository als `server_repo`.

    In diesem Beispiel wird davon ausgegangen, dass Sie das Repository in einen temporären Ordner auf dem Server kopiert haben.

    ```R
    source_repo <- "C:\\temp\\miniCRAN"
    ```

5. Da Sie in einem neuen R-Arbeitsbereich auf dem Server arbeiten, müssen Sie auch die Liste der Pakete zu installieren sind.

    ```R
    tspackages <- c("zoo", "forecast")
    ```

6. Installieren Sie die Pakete, die den Pfad zur lokalen Kopie des Repositorys MiniCRAN bereitstellen.

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath;(source_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE);
    ```

7. Von der Instanz bereitgestellt werden können Sie die installierten Pakete, die mit einem Befehl wie folgt anzeigen:

    ```R
    installed.packages()
    ```

> [!NOTE] 
> Um das Paket in SQL Server verwenden, müssen die Pakete in der Standardbibliothek verwendet wird, von der Instanz installiert werden. 

## <a name="manually-install-a-single-package-from-a-zipped-file"></a>Installieren Sie ein einzelnes Paket manuell aus einem ZIP-Datei

Wenn Sie ein einzelnes Paket, die keine Abhängigkeiten enthält, oder können keine **MiniCRAN**, Sie können das Paket Sie müssen auch manuell herunterladen. Zu diesem Zweck müssen Sie entweder ein Administrator oder der alleinige Besitzer eines Servers sind.

Nach dem Herunterladen der Pakete, installieren Sie die R-Pakete aus dem ZIP-Datei-Speicherort.

1. Laden Sie das Paket als ZIP-Datei, und speichern Sie sie in einem lokalen Ordner

2. Kopieren Sie diesen Ordner auf dem [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] Computer.

3. Installieren Sie die Pakete in der SQL Server-Instanz-Bibliothek mit konventionellen R-Befehle. Wenn das Paket weist Abhängigkeiten, die nicht bereits installiert sind und Sie haben diese nicht enthalten, kann die Installation misslingen. 

Sie können auch einzelne Pakete in eine Instanz von SQL Server 2017 hochladen, mithilfe der [Erstellen externer LIBRARY-Anweisung](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql). Auch erforderte dieser Prozess Administratorzugriff.
