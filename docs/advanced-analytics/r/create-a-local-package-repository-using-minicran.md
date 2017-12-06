---
title: Erstellen Sie ein lokales Paket-Repository mit MiniCRAN | Microsoft Docs
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: "4"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34be243d2f812ddb825f2e74afcde72d9420308d
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="create-a-local-package-repository-using-minicran"></a>Erstellen Sie ein lokales Paket-Repository mit miniCRAN

Es gibt zwei Möglichkeiten, die Sie R-Pakete für die Installation auf einem Server ohne Internetzugriff vorbereiten können.

-   [Verwenden des MiniCRAN-Pakets für eine einzelne lokale Repository erstellt werden.](#bkmk_miniCRAN)

    Die [MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) erstellt eine intern konsistent Repository bestehend aus ausgewählten Pakete aus CRAN-ähnliche Repositorys. Der Benutzer gibt einen Satz von gewünschten Pakete und MiniCRAN rekursiv liest die Abhängigkeitsstruktur für diese Pakete und lädt nur die aufgelisteten Pakete und deren Abhängigkeiten.

    Sie können dieses lokale Repository auf den Server verschoben, und fahren Sie mit der Pakete zu installieren, ohne über das Internet.

-   [Manuell herunter, und kopieren Sie die Pakete nacheinander](#bkmk_manual)

Dieser Artikel beschreibt, wie Sie ein R-Paket-Repository über beide Methoden erstellen können, und empfiehlt zu verwenden, der die **MiniCRAN** Paket.

## <a name="prepare-packages-using-minicran"></a>Vorbereiten von Paketen mit miniCRAN

Das Ziel zum Erstellen einer lokalen paketrepository ist an einen zentralen Ort zu bieten, den ein Serveradministrator oder anderen Benutzern in der Organisation verwenden können, um neue R-Pakete auf einem Server installieren, die über keinen Zugriff auf das Internet.

Die [MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) -Paket für R vom geschrieben wurde [Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html) verwaltete Satz von R-Pakete für eine Organisation erstellen Sie eine konsistente erleichtern. 

Es gibt viele Vorteile gegenüber der Verwendung von MiniCRAN Repository zu erstellen:

-   **Sicherheit**: viele R-Benutzer sind daran gewöhnt, zum Herunterladen und installieren neue R-Pakete werden, vom CRAN oder von einem Spiegel Standorte. Jedoch aus Sicherheitsgründen Produktionsservern ausgeführt [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] haben für gewöhnlich keine Internetverbindung.

-   **Einfacher Offlineinstallation**: beim Installieren des Pakets mit einem offline-Server erfordert, dass Sie auch alle paketabhängigkeiten herunterladen, mit MiniCRAN erleichtert es, rufen Sie alle Abhängigkeiten im richtigen Format ab.

-   **Verbesserte versionsverwaltung**: In einer mehrbenutzerumgebung, es gibt gute Gründe für die uneingeschränkte Paketversionen auf dem Server-Installation zu verhindern.

Nach dem Erstellen des Repositorys an, können Sie es durch Hinzufügen von neuen Paketen oder aktualisieren die Version der vorhandenen Pakete ändern.

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

2.  Geben Sie an einen lokalen Ordner, in dem Sie die gesammelten Pakete zu speichern. Needn't benennen Sie den Ordner MiniCRAN; Es könnte einen aussagekräftigeren Namen wie "GeneticsPackages" oder "ClientRPackages1.0.2" sein.

    Achten Sie auf den Ordner im Voraus erstellen. Ein Fehler wird ausgelöst, wenn die `local_repo` Ordner ist nicht vorhanden, wenn Sie später den R-Code ausführen.

    ```R
    local_repo <- "~/miniCRAN"
    ```

    Erweiterung Tilde-Operator gibt eine Umgebungsvariable mit Ergebnissen entspricht `Sys.getenv("R_USER")`.

### <a name="step-3-add-packages-to-the-repository"></a>Schritt 3: Hinzufügen von Paketen in das repository

1.  Nachdem MiniCRAN installiert ist, erstellen Sie eine Liste der zusätzlichen Pakete, die Sie herunterladen möchten.

    Dieser anfängliche Liste keine Abhängigkeiten hinzu; die **Igraph** Paket von MiniCRAN verwendet die Liste der Abhängigkeiten für Sie generiert. Weitere Informationen zur Verwendung dieses Diagramm finden Sie unter [MiniCRAN zum Identifizieren von paketabhängigkeiten verwendet](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

    Der folgende R-Skript wird das Abrufen von Ziel-Pakete, "Zoo" und "Planung" veranschaulicht.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```
2. Zeichnen Sie optional das Abhängigkeitsdiagramm, kann sehr informativ sein und kalte sucht.
    
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

-   Installieren Sie die Instanz-Bibliothek, die mit dem MiniCRAN Repository und R-Tools.

-   Hochladen Sie Pakete mit einer SQL­Datenbank, und installieren Sie Pakete auf der Grundlage einer pro Datenbank mit der Anweisung externe Bibliothek erstellen. Finden Sie unter [Installieren zusätzlicher R-Pakete unter SQL Server](install-additional-r-packages-on-sql-server.md).

Das folgende Verfahren beschreibt, wie die Pakete mithilfe von R-Tools zu installieren.

1.  Kopieren Sie den Ordner mit MiniCRAN Repository, in seiner Gesamtheit, mit dem Server, auf dem die Pakete installiert werden.

2.  Öffnen Sie eine R-Eingabeaufforderung mit dem R-Tool, das der Instanz zugeordnet.

    - Für SQL Server 2017 der Standardordner ist `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`.

    - Für SQL Server 2016 ist der Standardordner `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`.

    - Für eine benannte Instanz der Standardpfad wäre etwa: `<instance_path>.RTEST/R_SERVICES/library`.

    -  Wenn Sie SQL Server auf einem anderen Laufwerk installiert haben, oder andere Änderungen im Installationspfad vorgenommen haben, achten Sie darauf, dass Sie auch diese Änderungen übernehmen.

3.  Rufen Sie den Pfad für die Instanz-Bibliothek (in Fällen, die Sie in einem Benutzerverzeichnis), und fügen Sie es der Liste der Library-Pfade.

    ```R
    .libPaths()[1]  
    lib \<- .libPaths()[1]
    ```

    Dies sollte der instanzpfad "c: / Program Programme/Microsoft SQL Server/MSSQL14. zurückgeben. MSSQLSERVER/R_SERVICES/Library"

2.  Geben Sie den Speicherort auf dem Server, die Sie kopiert, in dem das Repository MininCRAN im haben `server_repo`.

    In diesem Beispiel wird davon ausgegangen, dass Sie das Repository Ordner "Benutzer" auf dem Server kopiert haben.

    ```R
    R server_repo <- "C:\\Users\\MyUserName\\miniCRAN"
    ```

3.  Da Sie in einem neuen R-Arbeitsbereich auf dem Server arbeiten, müssen Sie auch die Liste der Pakete zu installieren sind.

    ```R
    tspackages <- c("zoo", "forecast")
    ```

4.  Installieren Sie die Pakete, mit dem Pfad zur lokalen Kopie des Repositorys MiniCRAN.

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath(server_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE)
    ```

5.  Zeigen Sie die installierten Pakete jetzt an.

    ```R
    installed.packages()
    ```

> [!NOTE] 
> 
> In SQL Server 2017 werden zusätzliche Datenbankrollen und T-SQL-Anweisungen bereitgestellt, mit dem Serveradministratoren Berechtigungen über-Pakete verwalten können. Der Datenbankadministrator kann die Aufgabe der Installation von Paketen, besitzen mithilfe von R oder T-SQL, bei Bedarf. Allerdings kann der Datenbankadministrator auch Rollen verwenden, Benutzern die Möglichkeit, ihre eigenen Pakete installieren gewähren. Weitere Informationen finden Sie unter [paketverwaltung für SQL Server R](r-package-management-for-sql-server-r-services.md).
> 
> In SQL Server 2016 muss ein Serveradministrator die Pakete aus dem Repository MiniCRAN in die Standardbibliothek, die von der Instanz verwendeten installieren. Zu diesem Zweck verwenden Sie die R-Tools, wie in beschrieben die [vorangehenden Abschnitt](#bkmk_Rtools).

## <a name="manually-download-single-packages"></a>Manuelles Herunterladen von einzelnen Pakete

Wenn Sie nicht MiniCRAN verwenden möchten, können Sie die Pakete, die Sie benötigen, und ihre Abhängigkeiten auch manuell herunterladen. Zu diesem Zweck müssen Sie entweder ein Administrator oder der alleinige Besitzer eines Servers sind.

Nach dem Herunterladen der Pakete, installieren Sie die R-Pakete aus dem ZIP-Datei-Speicherort.

1.  Herunterladen Sie die Pakete Zip-Dateien und in einem lokalen Ordner zu speichern.

2.  Kopieren Sie diesen Ordner auf dem [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] Computer.

3.  Installieren Sie die Pakete in der Bibliothek der SQL Server-Instanz.

> [!NOTE]
> Wenn Sie R-Tools verwenden, um Pakete zu installieren, werden sie als Ganzes für die Instanz installiert. 
> 
> Wenn Sie installieren das Paket in eine Datenbank und das Paket für Benutzer, die mithilfe von Datenbankrollen freigeben möchten, müssen Sie die Bibliothek, die mit der Anweisung externe Bibliothek erstellen hochladen. Finden Sie unter [Installieren zusätzlicher R-Pakete in SQL Server](install-additional-r-packages-on-sql-server.md)
