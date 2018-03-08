---
title: SQL Server Data Objekte mithilfe von RxSqlServerData (SQL und R deep Dive) | Microsoft Docs
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: bcf5f7ff-795b-4815-b163-bcddd496efce
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 4690f7bd66b17643d7d58b10663debd4becbdac7
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-and-r-deep-dive"></a>Erstellen Sie SQL Server-Datenobjekte mit RxSqlServerData (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

Sie haben nun erstellt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank und über die erforderlichen Berechtigungen zur mit den Daten arbeiten. In diesem Schritt erstellen Sie einige Objekte in R, mit denen Sie mit den Daten arbeiten können.

## <a name="create-the-sql-server-data-objects"></a>Erstellen Sie die SQL Server Data-Objekte

In diesem Schritt verwenden Sie die Funktionen aus der **"revoscaler"** Paket zum Erstellen und Auffüllen von zwei Tabellen. Eine Tabelle wird zum Trainieren der Modelle verwendet, die andere Tabelle für die Bewertung. Beide Tabellen enthalten simulierte Kreditkarten-Betrugsdaten.

Zum Erstellen von Tabellen auf der Remoteinstanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer, rufen die **RxSqlServerData** Funktion.

> [!TIP]
> Wenn Sie R-Tools für Visual Studio verwenden, wählen Sie **R-Tools** aus der Symbolleiste aus, und klicken Sie auf **Fenster** , um Optionen zum Debuggen und Anzeigen von R-Variablen anzuzeigen.

### <a name="create-the-training-data-table"></a>Erstellen der Datentabelle training

1. Speichern Sie die Datenbankverbindungszeichenfolge in ein R-Variablen. Hier sind zwei Beispiele für gültige ODBC-Verbindungszeichenfolgen für SQL Server: eine, die unter Verwendung einer SQL-Anmeldung und eine für die integrierte Windows-Authentifizierung.

    **SQL-Anmeldename**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"
    ```

    **Windows-Authentifizierung**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
    ```

    Achten Sie darauf, dass der Instanzname, Datenbankname, Benutzername und das Kennwort nach Bedarf geändert werden.
  
2. Geben Sie den Namen der Tabelle an, die Sie erstellen möchten, und speichern Sie ihn in einer R-Variablen.
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    Da die Instanz- und Datenbanknamen bereits als Teil der Verbindungszeichenfolge beim Kombinieren der zwei Variablen angegeben werden, wird der *vollqualifizierte* Name der neuen Tabelle _instance.database.schema.ccFraudSmall_.
  
3.  Fügen Sie vor dem Instanziieren des Datenquellenobjekts eine Zeile hinzu, die den zusätzlichen Parameter *rowsPerRead*angibt.  Der *rowsPerRead* -Parameter steuert, wie viele Datenzeilen in jeden Batch eingelesen werden.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    Obwohl dieser Parameter optional ist, ist er wichtig für die Handhabung der Speicherauslastung und für effiziente Berechnungen.  Der erweiterten analytischen Funktionen in den meisten [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Daten in Segmenten verarbeiten und Speichern von Zwischenergebnissen zurückgeben, die endgültige Berechnungen nachdem alle Daten gelesen wurden.
  
    Wenn der Wert dieses Parameters zu groß ist, könnte der Datenzugriff möglicherweise langsam sein, da Sie nicht über genügen Speicher verfügen, um einen solch großen Datenblock effizient zu verarbeiten.  Wenn der Wert *rowsPerRead* zu niedrig ist, kann sich in einigen Systemen die Leistung verringern. Aus diesem Grund wird empfohlen, dass Sie mit dieser Einstellung auf Ihrem System experimentieren bei der Arbeit mit einem großen DataSet.
  
    In dieser exemplarischen Vorgehensweise verwenden die standardmäßige Batchgröße Prozess definiert, indem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz zum Steuern der Anzahl der Zeilen in jeder Block. Speichern Sie diesen Wert in der Variablen `sqlRowsPerRead`.
  
4.  Abschließend definieren Sie eine Variable für das neue Datenquellenobjekt, und übergeben Sie die Argumente, die an den Konstruktor RxSqlServerData zuvor definiert. Beachten Sie, dass dadurch nur das neue Datenquellenobjekt erstellt wird, es jedoch nicht aufgefüllt wird.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

#### <a name="to-create-the-scoring-data-table"></a>Bewertungs-Datentabelle erstellen

Erstellen Sie die gleichen Schritte mit der Tabelle, die Bewertungsprofile, mit der gleichen Daten enthält.

1. Erstellen Sie eine neue R-Variable, *sqlScoreTable*, um den Namen der Tabelle für die Bewertung zu speichern.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Geben Sie diese Variable als Argument an die RxSqlServerData-Funktion, um eine zweite Datenquellenobjekt definieren *SqlScoreDS*.
  
    ```R
    sqlScoreDS \<- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Da Sie bereits die Verbindungszeichenfolge und andere Parameter als Variablen im Arbeitsbereich "R" definiert haben, ist es leicht, neue Datenquellen zu anderen Tabellen, Sichten oder Abfragen zu erstellen.

> [!NOTE]
> Die Funktion verwendet die anderen Argumente für eine Datenquelle basierend auf einer ganzen Tabelle als für eine Datenquelle basierend auf einer Abfrage definieren. Dies ist, da die SQL Server-Datenbankmodul Abfragen anders vorbereiten muss. Weiter unten in diesem Lernprogramm erfahren Sie, wie ein Datenquellenobjekt, das basierend auf einer SQL-Abfrage zu erstellen.

## <a name="load-data-into-sql-tables-using-r"></a>Laden Sie Daten in SQL-Tabellen, die mithilfe von R

Sie haben die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen nun erstellt und können Daten in die Tabellen laden mithilfe der entsprechenden **Rx** -Funktion.

Die **"revoscaler"** Paket enthält Funktionen, die Unterstützung von vielen unterschiedlichen Datenquellen: für Textdaten verwenden [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) das Datenquellenobjekt zu generieren. Es gibt weitere Funktionen zum Erstellen von Datenquellenobjekten von Hadoop-Daten, ODBC-Daten, usw.

> [!NOTE]
> Für diesen Abschnitt, benötigen Sie **' DDL ausführen '** Berechtigungen für die Datenbank.

### <a name="load-data-into-the-training-table"></a>Laden Sie Daten in der Tabelle training

1. Erstellen Sie eine Variable R *CcFraudCsv*, und weisen Sie die Variable den Dateipfad für die CSV-Datei, die die Beispieldaten enthält.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Beachten Sie den Aufruf von **RxGetOption**, die die GET-Methode zugeordnet ist [RxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) in **"revoscaler"**. Mit diesem Dienstprogramm können festgelegt und Listenoptionen im Zusammenhang mit der lokalen und Remotecomputern rechenkontexte, z. B. das Standardverzeichnis für den freigegebenen oder die Anzahl der Prozessoren (Kerne), die in Berechnungen verwendet.
    
    Dieser bestimmten Aufruf ruft die Beispiele sind von der richtigen bereitgestellt werden, unabhängig davon, wo Sie Ihren Code ausgeführt werden. Versuchen Sie z.B. die Funktion auf SQL Server und auf Ihrem Entwicklungscomputer auszuführen, und beachten Sie, wie sich die Pfade unterscheiden.
  
2. Definieren Sie eine Variable, um die neuen Daten zu speichern, und verwenden Sie die Funktion **RxTextData** zur Angabe der Text-Datenquelle.
  
    ```R
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer",
        "fraudRisk" = "integer"))
    ```
  
    Das Argument *colClasses* ist wichtig. Sie verwenden es zur Angabe des Datentyps jeder Spalte von Daten, die aus der Textdatei geladen wird. In diesem Beispiel werden alle Spalten als Text behandelt, mit Ausnahme der benannten Spalten, die als ganze Zahlen verarbeitet werden.
  
3. An diesem Punkt sollten so halten Sie an einen Moment, und zeigen Sie Ihre Datenbank in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  Aktualisieren Sie die Liste der Tabellen in der Datenbank.
  
    Beachten Sie, dass, obwohl die R-Datenobjekte im lokalen Arbeitsbereich erstellt wurden, die Tabellen nicht in erstellt wurden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank. Darüber hinaus wurde keine Daten in die R-Variable aus der Textdatei geladen.
  
4. Rufen Sie nun die Funktion [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) auf, um die Daten in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle einzufügen.
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
  
    Wenn nach einer kurzen Pause keine Probleme mit der Verbindungszeichenfolge auftreten, sollten Sie Ergebnisse wie diese sehen:
  
      *Total Rows written: 10000, Total time: 0.466*

      *Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.577 seconds*
  
5. Aktualisieren Sie die Liste der Tabellen mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Um sicherzustellen, dass jede Variable verfügt über die korrekten Datentypen und wurde erfolgreich importiert, Sie können auch mit der rechten Maustaste der Tabellenindexes in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , und wählen Sie **oberste 1000 Zeilen auswählen**.

### <a name="load-data-into-the-scoring-table"></a>Laden Sie Daten in der bewertungs-Tabelle

1. Wiederholen Sie die Schritte zum Laden des Datasets für die Bewertung in die Datenbank aus.
  
    Starten Sie über den Pfad zur Quelldatei.
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. Verwenden Sie die Funktion **RxTextData** , um die Daten abzurufen, und speichern Sie sie in der Variablen *inTextData*.
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  Rufen Sie die Funktion **rxDataStep** auf, um die aktuelle Tabelle mit dem neuen Schema und Daten zu überschreiben.
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - Das *inData* -Argument definiert die zu verwendende Datenquelle.
  
    - Das *outFile* -Argument gibt die Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, in der Sie die Daten speichern möchten.
  
    - Wenn die Tabelle bereits vorhanden ist, und verwenden Sie nicht die *überschreiben* Option Ergebnisse ungekürzt eingefügt werden.
  
Wenn die Verbindung erfolgreich hergestellt wurde, sollte eine Nachricht angezeigt werden, die den Abschluss und die Zeit anzeigt, die zum Schreiben von Dateien in die Tabelle benötigt wurde:

*Total Rows written: 10000, Total time: 0.384*

*Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.456 seconds*

## <a name="more-about-rxdatastep"></a>Weitere Informationen zu rxDataStep

[RxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) ist eine leistungsstarke Funktion, die mehrere Transformationen auf ein R-Datenrahmen ausführen können. Sie können auch RxDataStep verwenden, um Daten in der Darstellung, die vom Ziel erforderlich: in diesem Fall [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Sie können optional Transformationen auf die Daten angeben, mithilfe von R-Funktionen in den Argumenten um **RxDataStep**. Beispiele für diese Vorgänge werden weiter unten in diesem Lernprogramm bereitgestellt.

## <a name="next-step"></a>Nächster Schritt

[Abfragen und Ändern der SQL Server-Daten](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Arbeiten Sie mit SQL Server-Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
