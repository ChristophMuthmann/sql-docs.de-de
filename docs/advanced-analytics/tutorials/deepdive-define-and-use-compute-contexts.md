---
title: Definieren und verwenden Sie rechenkontexte (SQL und R deep Dive) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: e8d5a04733ec11aff3b304d183d99c5c89b3feae
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="define-and-use-compute-contexts-sql-and-r-deep-dive"></a>Definieren Sie und verwenden Sie rechenkontexte (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

In dieser Lektion werden die [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) -Funktion, die können Sie definieren einen computekontext für SQL Server und dann auf dem Server statt von Ihrem lokalen Computer ausführen komplexe Berechnungen. 

"Revoscaler" unterstützt mehrere rechenkontexte, damit R-Code in Hadoop, Spark oder in der Datenbank ausgeführt werden können. Für SQL Server definieren Sie den Server, und die Funktion übernimmt die Aufgaben zum Erstellen der Datenbank Verbindungs- und übergeben von Objekten zwischen dem lokalen Computer und der remote-Ausführungskontext.

Die Funktion, die die SQL Server erstellt berechnen Kontext verwendet die folgende Informationen an:

- Verbindungszeichenfolge für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz
- Angabe der Behandlung der Ausgabe
- Optionale Argumente, die Ablaufverfolgung aktivieren, oder geben Sie die Ablaufverfolgungsebene
- Optionale Spezifikation von einem freigegebenen Verzeichnis

## <a name="create-and-set-a-compute-context"></a>Erstellen Sie, und legen Sie einen computekontext.

1. Geben Sie die Verbindungszeichenfolge für die Instanz, auf dem Berechnungen ausgeführt werden.  Sie können die Verbindungszeichenfolge erneut verwenden, die Sie zuvor erstellt haben. Wenn Sie die Berechnungen auf einen anderen Server verschieben, oder verwenden Sie einen anderen Anmeldenamen einige Aufgaben ausführen möchten, können Sie eine andere Verbindungszeichenfolge erstellen.

    **Verwenden einer SQL-Anmeldung**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>"
      ```

    **Verwenden der Windows-Authentifizierung**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
      ```
2. Geben Sie an, wie die Ausgabe behandelt werden soll. Im folgenden Code geben Sie an, dass die R-Sitzung auf der Arbeitsstation immer auf R-Auftragsergebnisse warten soll, aber keine Konsolenausgaben aus Remoteberechnungen zurückgegeben werden sollen.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    Das Argument *wait* für **RxInSqlServer** unterstützt diese Optionen:
  
    -   **TRUE**. Der Auftrag ist als blockiert konfiguriert und wird nicht zurückgegeben, bis er abgeschlossen wurde oder fehlgeschlagen.  Weitere Informationen finden Sie unter [verteilt und paralleles computing in Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Aufträge sind als nicht blockierend und sofort zurück, sodass Sie weiter ausgeführt wird, andere R-Code. Jedoch auch im nicht blockierenden Modus muss die Clientverbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufrechterhalten werden, während der Auftrag ausgeführt wird.

3. Optional können Sie angeben, den Speicherort eines lokalen Verzeichnisses für die gemeinsame Nutzung von der lokalen R-Sitzung und durch die Remotesteuerung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer und ihre Konten.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. Wenn Sie ein bestimmtes Verzeichnis für die Freigabe manuell erstellen möchten, können Sie eine Zeile wie folgt hinzufügen:

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

    Um zu bestimmen, welche Ordner für die Freigabe zurzeit verwendet wird, führen `rxGetComputeContext()`, womit Informationen zu den aktuellen computekontext. Weitere Informationen finden Sie unter [RxInSqlServer (in englischer Sprache)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/).

4. Alle Variablen müssen vorbereitet Geben Sie diese als Argumente für die **RxInSqlServer** -Konstruktor zum Erstellen der *compute Context-Objekt*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    Die Syntax für **RxInSqlServer** nahezu identisch mit der **RxSqlServerData** -Funktion, die Sie zuvor verwendet, um die Datenquelle zu definieren. Es gibt jedoch auch wichtige Unterschiede.
      
    - Das Datenquellenobjekt (mithilfe der Funktion [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)definiert) gibt an, wo die Daten gespeichert werden.
    
    - Im Gegensatz dazu die computekontext definiert, mit der Funktion [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) gibt an, wo Aggregationen und andere Berechnungen durchgeführt werden.
    
    Das Definieren eines Computekontexts wirkt sich nicht auf andere generische R-Berechnungen aus, die Sie auf Ihrer Arbeitsstation ausführen können, und ändert nicht die Quelle der Daten. Sie können z.B. eine lokale Textdatei als Datenquelle definieren, aber SQL Server als Computekontext verwenden und alle Lesevorgänge und Zusammenfassungen der Daten auf dem SQL Server-Computer ausführen.

## <a name="enable-tracing-on-the-compute-context"></a>Aktivieren der Ablaufverfolgung für die computekontext.

Es kann vorkommen, dass Vorgänge, die in Ihrem lokalen Kontext funktionieren, jedoch Probleme bei der Ausführung in einem Remotecomputekontext haben. Wenn Sie Probleme analysieren möchten oder die Leistung überwachen möchten, können Sie die Ablaufverfolgung im Computekontext aktivieren, um die Problembehandlung der Laufzeit zu unterstützen.

1. Erstellen Sie einen neuen computekontext, die die gleiche Verbindungszeichenfolge verwendet, aber fügen Sie die Argumente *TraceEnabled* und *TraceLevel* auf die **RxInSqlServer** Konstruktor.

    ```R
    sqlComputeTrace <- RxInSqlServer(
        connectionString = sqlConnString,
        #shareDir = sqlShareDir,
        wait = sqlWait,
        consoleOutput = sqlConsoleOutput,
        traceEnabled = TRUE,
        traceLevel = 7)
    ```
  
    In diesem Beispiel ist *traceLevel* auf 7 gesetzt, d.h. „alle Ablaufverfolgungsinformationen anzeigen“.

2. Um diesen Computekontext zu ändern, verwenden Sie die Funktion [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext), und geben Sie den Kontext anhand des Namens an.

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > Verwenden Sie für dieses Lernprogramm des computekontexts, der keine Ablaufverfolgung aktiviert werden. 
    > 
    > Wenn Sie die Ablaufverfolgung verwenden möchten, Bedenken Sie jedoch, dass Ihre Erfahrung Netzwerkkonnektivität auswirken kann. Bewusst sein, da die Leistung für die Ablaufverfolgung aktivierte Option für alle Vorgänge nicht getestet wurde.

Im nächsten Schritt, den Sie erfahren, wie mithilfe von remotecomputekontexten Sie, zum Ausführen von R-Code auf dem Server oder lokal.

## <a name="next-step"></a>Nächster Schritt

[Erstellen und Ausführen von R-Skripts](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Abfragen und Ändern der SQL Server-Daten](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
