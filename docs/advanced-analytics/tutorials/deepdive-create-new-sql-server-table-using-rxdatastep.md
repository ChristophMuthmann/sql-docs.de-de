---
title: Erstellen Sie neue SQL Server-Tabelle mit RxDataStep | Microsoft Docs
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f276a09ea785da6b31a54693a6f5d758bb77b43
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="create-new-sql-server-table-using-rxdatastep"></a>Erstellen einer neuen SQL Server-Tabelle mit rxDataStep

In dieser Lektion erfahren Sie, wie Sie Daten zwischen In-Memory-Datenrahmen, dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Kontext und lokale Dateien verschieben.

> [!NOTE]
> In dieser Lektion verwenden Sie ein anderes Dataset. Das Fluggesellschaft Verzögerungen-Dataset ist ein öffentlicher Dataset, das häufig für Machine learning-Experimente verwendet wird. Wenn Sie gerade erst mit R beginnen, ist dieses Dataset nützlich, um es für Tests zur Hand zu haben, denn es wird in verschiedenen Produktbeispielen für [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] verwendet, die unter [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]veröffentlicht wurden. Die Datendateien, die Sie für dieses Beispiel benötigen, sind in demselben Verzeichnis wie die anderen Produktbeispiele verfügbar.

## <a name="create-sql-server-table-from-local-data"></a>Erstellen einer SQL Server-Tabelle aus den lokalen Daten

Im ersten Teil dieses Lernprogramms, Sie verwendet die **RxTextData** Funktion, um Daten in R aus einer Textdatei importieren, und dann verwendet der **RxDataStep** Funktion zum Verschieben der Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

In dieser Lektion verwenden Sie eine andere Herangehensweise und rufen Daten aus einer Datei ab, die im [XDF-Format](https://en.wikipedia.org/wiki/Extensible_Data_Format)gespeichert ist. Das XDF-Format ist ein XML-Standard für mehrdimensionale Daten. Dies ist ein binäres Dateiformat mit einer R-Schnittstelle, die die Verarbeitung und Analyse von Zeilen und Spalten optimiert.  Sie können es für das Verschieben von Daten verwenden, um Teilmengen von Daten zu speichern, die für Analysen hilfreich sind.

Nach einigen einfachen Transformationen der Daten mithilfe der XDF-Datei, speichern Sie die transformierten Daten in eine neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle.

> [!NOTE]
> Sie benötigen DDL-Berechtigungen für diesen Schritt.

1. Legen Sie den Computekontext auf die lokale Arbeitsstation fest.
  
    ```R
    rxSetComputeContext("local")
    ```
  
2. Definieren Sie ein neues Datenquellenobjekt mithilfe der **RxXdfData** -Funktion. Für eine XDF-Datenquelle geben Sie einfach den Pfad zur Datendatei an.  Geben Sie den Pfad zur Datei mit einer Textvariablen, aber in diesem Fall besteht eine praktische Kurzform, da die Beispieldatendatei (AirlineDemoSmall.xdf) in das Verzeichnis, das von der RxGetOption-Funktion zurückgegeben wird.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. Aufrufen von RxGetVarInfo auf die Daten im Arbeitsspeicher anzeigen eine Zusammenfassung des Datasets.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**Ergebnisse**

*Var 1: ArrDelay, Typ: ganze Zahl, Min/Max: (-86, 1490)*

*Var 2: CRSDepTime, Typ: numerisch, Speicher: float32, Min/Max: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 Faktorebenen: Montag Dienstag Mittwoch Donnerstag Freitag Samstag Sonntag*

> [!NOTE]
> 
> Haben Sie bemerkt, dass Sie keine weiteren Funktionen zum Laden von Daten in XDF-Datei aufrufen müssen, und von RxGetVarInfo sofort auf die Daten aufrufen? Das liegt daran, dass XDF die Standardmethode für die Zwischenspeicherung für RevoScaleR ist. Weitere Informationen zu XDF-Dateien finden Sie unter [erstellt ein XDF](https://msdn.microsoft.com/microsoft-r/scaler-data-xdf).
  
4. Nun fügen Sie diese Daten in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle, speichern _DayOfWeek_ als ganze Zahl mit Werten von 1 bis 7.
  
    Zu diesem Zweck müssen Sie zunächst eine SQL Server-Datenquelle definieren.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. Überprüfen Sie, ob eine Tabelle mit dem gleichen Namen bereits vorhanden ist und löschen Sie sie gegebenenfalls.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. Tabelle erstellen und Daten laden mithilfe von **rxDataStep**veröffentlicht wurden. Diese Funktion verschiebt Daten zwischen zwei bereits definierten Datenquellen und unterwegs die Serialisierungsdaten transformieren können.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    Da dies eine ziemlich große Tabelle ist, sollten Sie auf die endgültige Statusmeldung warten: *Rows Read: 200000, Total Rows Processed: 600000* (Gelesene Zeilen: 200000, Insgesamt verarbeitete Zeilen: 600000).
     
7. Setzt den Computekontext auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer zurück.

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. Erstellen Sie eine neue SQL Server-Datenquelle mit einer einfachen SQL-Abfrage für die neue Tabelle. Diese Definition fügt Faktorebenen für die *DayOfWeek*-Spalte mithilfe des *colInfo*-Arguments an RxSqlServerData hinzu.
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. Rufen Sie RxSummary einmal, um eine Zusammenfassung der Daten in der Abfrage zu überprüfen.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>Nächster Schritt

[Führen Sie die Segmentierung Analysen mit RxDataStep aus](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Laden von Daten in den Arbeitsspeicher mit rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)


