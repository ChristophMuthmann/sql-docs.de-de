---
title: Erstellen Sie neue SQL Server-Tabelle, die mit RxDataStep (SQL und R deep Dive) | Microsoft Docs
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 5a414c590f72a1b1cfef9a3dbd8082a500592140
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-and-r-deep-dive"></a>Erstellen Sie neue SQL Server-Tabelle, die mit RxDataStep (SQL und R deep Dive)

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

In dieser Lektion erfahren Sie, wie zum Verschieben von Daten zwischen in-Memory Data Frames, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Kontext und lokale Dateien.

> [!NOTE]
> In dieser Lektion wird ein anderes DataSet verwendet. Das Fluggesellschaft Verzögerungen-Dataset ist ein öffentlicher Dataset, das häufig für Machine learning-Experimente verwendet wird. In diesem Beispiel verwendeten Datendateien sind im selben Verzeichnis wie andere Produktbeispiele verfügbar.

## <a name="create-sql-server-table-from-local-data"></a>Erstellen von SQL Server-Tabelle aus den lokalen Daten

In der ersten Hälfte dieses Lernprogramms, Sie verwendet die **RxTextData** Funktion, um Daten in R aus einer Textdatei importieren, und dann verwendet der **RxDataStep** Funktion zum Verschieben der Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

In dieser Lektion akzeptiert einen anderen Ansatz, und verwendet Daten aus einer Datei gespeichert, der [XDF-Format](https://en.wikipedia.org/wiki/Extensible_Data_Format). Nach der Durchführung einige einfachen Transformations auf die Daten mithilfe der XDF-Datei, speichern Sie die transformierten Daten in eine neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle.

**Was ist XDF?**

Das XDF-Format ist ein XML-Standard für hochdimensionalen Daten entwickelt und wird durch das systemeigene Dateiformat verwendet [Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Dies ist ein binäres Dateiformat mit einer R-Schnittstelle, die die Verarbeitung und Analyse von Zeilen und Spalten optimiert.  Sie können es für das Verschieben von Daten verwenden, um Teilmengen von Daten zu speichern, die für Analysen hilfreich sind.

1. Legen Sie den Computekontext auf die lokale Arbeitsstation fest. **DDL-Berechtigungen sind für diesen Schritt erforderlich.**

  
    ```R
    rxSetComputeContext("local")
    ```
  
2. Definieren Sie ein neues Datenquellenobjekt mithilfe der **RxXdfData** -Funktion. Um eine XDF-Datenquelle zu definieren, geben Sie den Pfad zu der Datendatei.  

    Sie können den Pfad zur Datei mit einer Textvariablen angeben. In diesem Fall besteht jedoch eine praktische Kurzform, d. h. Verwenden der **RxGetOption** Funktion, und rufen Sie die Datei (AirlineDemoSmall.xdf) aus dem Datenverzeichnis Beispiel.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. Rufen Sie [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) für die Daten im Arbeitsspeicher auf, um eine Zusammenfassung des Datasets anzuzeigen.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**Ergebnisse**

*Var 1: ArrDelay, Typ: ganze Zahl, Min/Max: (-86, 1490)*

*Var 2: CRSDepTime, Typ: numerisch, Speicher: float32, Min/Max: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 Faktorebenen: Montag Dienstag Mittwoch Donnerstag Freitag Samstag Sonntag*

> [!NOTE]
> 
> Haben Sie bemerkt, dass Sie keine anderen Funktionen aufrufen mussten, um die Daten in die XDF-Datei zu laden, und die Funktion **rxGetVarInfo** sofort auf die Daten anwenden konnten? Das liegt daran, dass XDF die Standardmethode für die Zwischenspeicherung für RevoScaleR ist. Zusätzlich zu XDF-Dateien die **von RxGetVarInfo** -Funktion unterstützt jetzt mehrere Datenquellentypen.
  
4. Setzen diese Daten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle speichern _DayOfWeek_ als ganze Zahl mit Werten von 1 bis 7.
  
    Zu diesem Zweck müssen Sie zunächst eine SQL Server-Datenquelle definieren.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. Überprüfen Sie, ob eine Tabelle mit dem gleichen Namen bereits vorhanden ist und löschen Sie sie gegebenenfalls.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. Tabelle erstellen und Daten laden mithilfe von **rxDataStep**veröffentlicht wurden. Diese Funktion verschiebt Daten zwischen zwei bereits definierten Datenquellen und können optional Datentransformation route.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    Dies ist eine relativ große Tabelle, so warten Sie, bis eine Endstatus Meldung wie die folgende angezeigt: *Gelesene Zeilen: 200000, insgesamt Zeilen verarbeitet: 600000*.
     
7. Setzt den Computekontext auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer zurück.

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. Erstellen Sie eine neue SQL Server-Datenquelle mit einer einfachen SQL-Abfrage für die neue Tabelle. Diese Definition fügt Faktor Ebenen für die *DayOfWeek* Spalte mithilfe der *ColInfo* Argument **RxSqlServerData**.
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. Rufen Sie **RxSummary** einmal, um eine Zusammenfassung der Daten in der Abfrage zu überprüfen.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>Nächster Schritt

[Blockweises Analysieren mithilfe von rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Laden von Daten in den Arbeitsspeicher mit rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
