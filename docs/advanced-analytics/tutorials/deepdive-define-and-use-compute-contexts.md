---
title: Definieren und Verwenden von berechneten Kontexten (Tieferer Einblick in Data Science) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 511738cfce795600bcfa06a95de4cdf3d6b503bb
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="define-and-use-compute-contexts"></a>Definieren und Verwenden von berechneten Kontexten


Angenommen, Sie möchten, dass einige der komplexeren Berechnungen auf dem Server statt auf dem lokalen Computer ausgeführt werden sollen. Zu diesem Zweck können Sie einen berechneten Kontext erstellen, der R-Code auf dem Server ausführt.

Die **RxInSqlServer** -Funktion ist eine der erweiterten R-Funktionen im [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) -Paket. Die Funktion behandelt die Aufgaben bei der Erstellung der Datenbank-Verbindung und das Übergeben von Objekten zwischen dem lokalen Computer und dem Remote-Ausführungskontext.

In diesem Schritt erfahren Sie, wie Sie die **RxInSqlServer** -Funktion zur Definition eines Computekontexts in Ihrem R-Code verwenden.

Um einen Computerkontext zu erstellen, benötigen Sie die folgenden grundlegenden Informationen über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz:

- Die Verbindungszeichenfolge für die Instanz
- Eine Spezifikation für die Verarbeitung der Ausgabe
- Optionale Argumente für das Aktivieren der Ablaufverfolgung oder für die Angabe eines freigegebenen Verzeichnisses

## <a name="create-and-set-a-compute-context"></a>Erstellen und Festlegen eines Computekontexts

1. Geben Sie die Verbindungszeichenfolge für die Instanz an, in der Berechnungen stattfinden sollen.  Dies ist nur eine der vielen Variablen, die Sie der *RxInSqlServer* -Funktion zum Erstellen des Computekontexts übergeben. Sie können die Verbindungszeichenfolge erneut verwenden, die Sie zuvor erstellt haben. Alternativ können Sie auch eine andere Verbindungszeichenfolge erstellen, wenn Sie die Berechnungen auf einen anderen Server verschieben oder eine andere Identität verwenden möchten.

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
  
    Das Argument *wait* für *RxInSqlServer* unterstützt diese Optionen:
  
    -   **TRUE**. Der Auftrag wird blockiert und nicht zurückgegeben, bis er abgeschlossen wurde oder ein Fehler aufgetreten ist.  Weitere Informationen finden Sie unter [verteilt und paralleles computing in Microsoft R](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).
  
    -   **FALSE**. Aufträge werden nicht blockierend und sofort zurückgegeben, sodass Sie weiterhin anderen R-Code ausführen können. Jedoch auch im nicht blockierenden Modus muss die Clientverbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufrechterhalten werden, während der Auftrag ausgeführt wird.

3. Optional können Sie ein lokales Verzeichnis angeben, das für den freigegebenen Gebrauch von der lokale R-Sitzung und vom  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Remotecomputer und dessen Konten gemeinsam genutzt wird.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. Wenn Sie ein bestimmtes Verzeichnis für die Freigabe manuell erstellen möchten, können Sie eine Zeile wie folgt hinzufügen. Um zu bestimmen, welche Ordner für die Freigabe zurzeit verwendet wird, führen `rxGetComputeContext`, womit Informationen zu den aktuellen computekontext. Weitere Informationen finden Sie unter [RxInSqlServer (in englischer Sprache)](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinsqlserver).

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Alle Variablen müssen vorbereitet ermöglichen sie als Argumente an den RxInSqlServer-Konstruktor zum Erstellen der *compute Context-Objekt*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    Möglicherweise bemerken Sie, dass die Syntax für RxInSqlServer * fast identisch mit dem der RxSqlServerData-Funktion, die Sie zuvor verwendet ist, um die Datenquelle zu definieren. Es gibt jedoch auch wichtige Unterschiede.
      
    - Das Datenquellenobjekt definiert, indem Sie die Funktion RxSqlServerData, gibt an, in dem die Daten gespeichert werden.
    
    - Im Gegensatz dazu gibt die computekontext (mithilfe der Funktion RxInSqlServer definiert) an, wo Aggregationen und andere Berechnungen durchgeführt werden.
    
    Das Definieren eines Computekontexts wirkt sich nicht auf andere generische R-Berechnungen aus, die Sie auf Ihrer Arbeitsstation ausführen können, und ändert nicht die Quelle der Daten. Sie können z.B. eine lokale Textdatei als Datenquelle definieren, aber SQL Server als Computekontext verwenden und alle Lesevorgänge und Zusammenfassungen der Daten auf dem SQL Server-Computer ausführen.

## <a name="enable-tracing-on-the-compute-context"></a>Aktivieren der Ablaufverfolgung für den Computekontext

Es kann vorkommen, dass Vorgänge, die in Ihrem lokalen Kontext funktionieren, jedoch Probleme bei der Ausführung in einem Remotecomputekontext haben. Wenn Sie Probleme analysieren möchten oder die Leistung überwachen möchten, können Sie die Ablaufverfolgung im Computekontext aktivieren, um die Problembehandlung der Laufzeit zu unterstützen.

1. Erstellen Sie einen neuen computekontext, die die gleiche Verbindungszeichenfolge verwendet, aber fügen Sie die Argumente *TraceEnabled* und *TraceLevel* auf die *RxInSqlServer* Konstruktor.

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

2. Um computekontext zu ändern, verwenden Sie die RxSetComputeContext-Funktion, und geben Sie den Kontext anhand des Namens.

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > In diesem Tutorial verwenden Sie den Computekontext, bei dem die Ablaufverfolgung nicht aktiviert ist. Ist, dass die Leistung für die Ablaufverfolgung aktivierte Option für alle Vorgänge nicht getestet wurde.
    > 
    > Wenn Sie die Ablaufverfolgung verwenden möchten, Bedenken Sie jedoch, dass Ihre Erfahrung Netzwerkkonnektivität auswirken kann.

Da Sie nun einen Remotecomputekontext erstellt haben, lernen Sie, wie Sie Computerkontexte ändern können, um R-Code lokal auf dem Server auszuführen.

## <a name="next-step"></a>Nächster Schritt

[Erstellen und Ausführen von R-Skripts](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)


## <a name="previous-step"></a>Vorheriger Schritt

[Fragen Sie ab und ändern Sie die SQL Server-Daten](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)



