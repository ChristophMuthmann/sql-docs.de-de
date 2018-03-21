---
title: "Einrichten einer Data Science-Client für die Verwendung mit SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 160dae2d84c84aeaecaa07ec16be681fabde5534
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="set-up-a-data-science-client-for-use-with-sql-server"></a>Einrichten eines Data Science-Clients für die Verwendung mit SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Nach der Konfiguration einer Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] um Machine Learning unterstützen, sollten Sie Einrichten einer Entwicklungsumgebung, die der Verbindung mit dem Server für die Remoteausführung und Bereitstellung kann.

Dieser Artikel beschreibt einige typische Clientszenarien, einschließlich der Konfiguration der kostenlosen Visual Studio Community Edition, R-Code in SQL Server ausgeführt wird.

## <a name="install-r-libraries-on-the-client"></a>Installieren von R-Bibliotheken auf dem client

Ihre Clientumgebung sollte Microsoft R Open sowie zusätzliche RevoScaleR-Pakete enthalten, die eine verteilte Ausführung von R auf SQL Server unterstützt. Standard-Distributionen von R müssen sich nicht auf die Pakete aus, die remote rechenkontexte oder parallele Ausführung von R-Aufgaben unterstützen.

Um diese Bibliotheken zu erhalten, installieren Sie eine der folgenden:
  
+ [Microsoft R Client](http://aka.ms/rclient/download)

+ Microsoft R Server (für SQLServer 2016)

    - Zur Installation von SQL Server-Setup finden Sie unter [Installieren von SQL Server 2016 R Server (eigenständig)](../install/sql-r-standalone-windows-install.md)

    - Um separate Windows-basierten Installationsprogramm verwenden zu können, finden Sie unter [Machine Learning-Server für Windows installieren](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ Machine Learning-Server (für SQLServer 2017)

    - Zur Installation von SQL Server-Setup finden Sie unter [installieren Sie SQL Server 2017 Machine Learning-Server (eigenständig)](../install/sql-machine-learning-standalone-windows-install.md)

    - Um separate Windows-basierten Installationsprogramm verwenden zu können, finden Sie unter [Installieren von R Server 9.1 für Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="install-a-development-environment"></a>Installieren Sie eine Entwicklungsumgebung

Wenn Sie eine bevorzugte R-Entwicklungsumgebung noch nicht haben, empfehlen wir eine der folgenden:

+ R-Tools für Visual Studio

    Funktioniert mit Visual Studio 2015.

    Informationen zum Setup finden Sie unter [zum Installieren von R-Tools für Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).
 
    Um RTVS Verwendung Ihrer Microsoft-R-Clientbibliotheken zu konfigurieren, finden Sie unter [zu Microsoft R-Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ Visual Studio-2017

    Die kostenlose Community-Edition enthält die Data Science arbeitsauslastung aus, die Projektvorlagen für R, Python und f# installiert wird.

    Herunterladen von Visual Studio aus [Websiteansicht](https://www.visualstudio.com/vs/). 

+ RStudio

    Wenn Sie RStudio verwenden möchten, sind einige zusätzliche Schritte erforderlich, um die RevoScaleR-Bibliotheken zu verwenden:

    - Installieren Sie Microsoft R-Client, um die erforderlichen Pakete und Bibliotheken zu erhalten.
    - Aktualisieren Sie Ihre R-Pfad zum Verwenden der Microsoft-R-Laufzeit.

    Weitere Informationen finden Sie unter [R-Client - konfigurieren die IDE](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide).

## <a name="configure-your-ide"></a>Konfigurieren der IDE

+ R-Tools für Visual Studio

    Finden Sie unter [Websiteansicht](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r) für einige Beispiele zum Erstellen und Debuggen von R mit R-Tools für Visual Studio-Projekte. 

+ Visual Studio-2017

    Bei der Installation von Microsoft R Client- oder R **vor** Sie Visual Studio installieren, die R-Server-Bibliotheken automatisch erkannt und beim Bibliothekspfad verwendet. Wenn Sie die RevoScaleR-Bibliotheken aus nicht installiert haben die **R-Tools** klicken Sie im Menü **R-Client installieren**.

## <a name="run-r-in-sql-server"></a>Ausführen von R in SQLServer

Dieses Beispiel verwendet Visual Studio 2017 Community Edition, mit der Data Science-Arbeitslast installiert.

1. Aus der **Datei** klicken Sie im Menü **neu** und wählen Sie dann **Projekt**.

2. Das - Handsymbol Bereich enthält eine Liste der vorinstallierten Vorlagen. Klicken Sie auf **R**, und wählen Sie **R Project**. In der **Namen** geben `dbtest` , und klicken Sie auf **OK**.

3. Visual Studio erstellt eine neue Projektordner und einer Standard-Skriptdatei `Script.R`. 

4. Typ `.libPaths()` in der ersten Zeile des Skripts Datei, und drücken Sie STRG + EINGABETASTE.

5. Der Pfad der aktuellen R sollte angezeigt werden, der **R interaktive** Fenster. 

6. Klicken Sie auf die **R-Tools** Menü **Windows** um eine Liste von anderen R-spezifische Windows anzuzeigen, die Sie in Ihrem Arbeitsbereich anzeigen können.
 
    + Anzeigen von Hilfe für die Pakete in der aktuellen Bibliothek durch Drücken von STRG + 3.
    + Finden Sie unter R-Variablen in der **Variable Explorer**, durch Drücken von STRG + 8.

7. Erstellen Sie eine Verbindungszeichenfolge zu einer SQL Server-Instanz, und verwenden Sie die Verbindungszeichenfolge im Konstruktor RxInSqlServer, um ein SQL Server-Datenquellenobjekt zu erstellen. 

    ```r
    connStr <- "Driver=SQL Server;Server=MyServer;Database=MyTestDB;Uid=;Pwd="
    sqlShareDir <- paste("C:\\AllShare\\", Sys.getenv("USERNAME"), sep = "")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    cc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    sampleDataQuery <- "SELECT TOP 100 * from [dbo].[MyTestTable]"
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, connectionString = connStr, rowsPerRead = 500)
    ```

    > [!TIP]
    > Um einen Batch auszuführen, wählen Sie die Zeilen, die Sie verwenden möchten, führen Sie aus, und drücken STRG + EINGABETASTE.

8. Festlegen Sie des computekontexts an den Server, und führen Sie einige einfache R-Code auf die Daten.

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    Ergebnisse werden zurückgegeben, der **R interaktive** Fenster.
    
    Wenn Sie möchten sicherstellen, dass der Code für die SQL Server-Instanz ausgeführt wird, können Sie Profiler verwenden, zum Erstellen einer Ablaufverfolgung.