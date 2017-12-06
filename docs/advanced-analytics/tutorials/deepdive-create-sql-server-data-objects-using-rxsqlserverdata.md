---
title: Erstellen von SQL Server-Datenobjekten mithilfe von RxSqlServerData | Microsoft-Dokumentation
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
ms.assetid: bcf5f7ff-795b-4815-b163-bcddd496efce
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c6208de7eedf66640ab2b8131a4b73c51e6fbaba
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata"></a>Erstellen von SQL Server-Datenobjekten mithilfe von RxSqlServerData

Sie haben jetzt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank und die erforderlichen Berechtigungen zum Arbeiten mit den Daten erstellt und erstellen nun Objekte in R, mit denen Sie mit den Daten arbeiten können – sowohl auf dem Server und auf Ihrer Arbeitsstation.

## <a name="create-the-sql-server-data-objects"></a>Erstellen der SQL Server-Daten-Objekte

In diesem Schritt erstellen Sie mit R zwei Tabellen und füllen sie aus. Beide Tabellen enthalten simulierte Kreditkarten-Betrugsdaten. Eine Tabelle wird zum Trainieren der Modelle verwendet, die andere Tabelle für die Bewertung.

Zum Erstellen von Tabellen auf dem entfernten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer verwenden Sie die **RxSqlServerData** Funktion aus dem **RevoScaleR** -Paket.

> [!TIP]
> Wenn Sie R-Tools für Visual Studio verwenden, wählen Sie **R-Tools** aus der Symbolleiste aus, und klicken Sie auf **Fenster** , um Optionen zum Debuggen und Anzeigen von R-Variablen anzuzeigen.

### <a name="create-the-training-data-table"></a>Erstellen der Datentabelle training

1. Geben Sie die Datenbank-Verbindungszeichenfolge in einer R-Variablen an. Hier haben wir zwei Beispiele gültiger ODBC-Verbindungszeichenfolgen für SQL Server bereitgestellt: eine, die eine SQL-Anmeldung verwendet und eine für die integrierte Windows-Authentifizierung (empfohlen).

    **Verwenden einer SQL-Anmeldung**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"
    ```

    **Verwenden der Windows-Authentifizierung**
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
  
    Obwohl dieser Parameter optional ist, ist er wichtig für die Handhabung der Speicherauslastung und für effiziente Berechnungen.  Die meisten analytischen Funktionen in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] verarbeiten Daten in Segmenten und sammeln Zwischenergebnisse an, die die endgültigen Berechnungen zurückgeben, nachdem alle Daten gelesen wurden.
  
    Wenn der Wert dieses Parameters zu groß ist, könnte der Datenzugriff möglicherweise langsam sein, da Sie nicht über genügen Speicher verfügen, um einen solch großen Datenblock effizient zu verarbeiten.  Wenn der Wert *rowsPerRead* zu niedrig ist, kann sich in einigen Systemen die Leistung verringern.
  
    In dieser exemplarischen Vorgehensweise verwenden Sie die Batchprozessgröße, definiert von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, zur Steuerung der Anzahl der Zeilen in jedem Segment, und speichern diesen Wert in der Variablen *sqlRowsPerRead*.  Es wird empfohlen, dass Sie bei der Arbeit mit einem großen Datensatz mit dieser Einstellung auf Ihrem System experimentieren.
  
4.  Abschließend definieren Sie eine Variable für das neue Datenquellenobjekt, und übergeben Sie die Argumente, die an den Konstruktor RxSqlServerData zuvor definiert. Beachten Sie, dass dadurch nur das neue Datenquellenobjekt erstellt wird, es jedoch nicht aufgefüllt wird.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

#### <a name="to-create-the-scoring-data-table"></a>Bewertungs-Datentabelle erstellen

Sie verwenden die gleiche Vorgehensweise, um die Tabelle zu erstellen, in der die Bewertungsdaten erhalten sind.

1. Erstellen Sie eine neue R-Variable, *sqlScoreTable*, um den Namen der Tabelle für die Bewertung zu speichern.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Geben Sie diese Variable als Argument an die RxSqlServerData-Funktion, um eine zweite Datenquellenobjekt definieren *SqlScoreDS*.
  
    ```R
    sqlScoreDS \<- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Da Sie bereits die Verbindungszeichenfolge und andere Parameter als Variablen im R-Arbeitsbereich definiert haben, ist es einfach, neue Datenquellen für andere Tabellen, Sichten oder Abfragen zu erstellen. Geben Sie einfach einen anderen Tabellennamen an.

Später in diesem Tutorial erfahren Sie, wie Sie ein Datenquellenobjekt auf Grundlage einer SQL-Abfrage erstellen.

## <a name="load-data-into-sql-tables-using-r"></a>Laden von Daten in SQL-Tabellen mithilfe von R

Sie haben die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen nun erstellt und können Daten in die Tabellen laden mithilfe der entsprechenden **Rx** -Funktion.

Die **"revoscaler"** Paket enthält Funktionen, die Unterstützung von vielen unterschiedlichen Datenquellen: für Textdaten, verwenden Sie RxTextData um das Datenquellenobjekt zu generieren. Es gibt weitere Funktionen zum Erstellen von Datenquellenobjekten von Hadoop-Daten, ODBC-Daten, usw.

> [!NOTE]
> Für diesen Abschnitt müssen Sie über „DDL ausführen“-Berechtigungen für die Datenbank verfügen.

### <a name="load-data-into-the-training-table"></a>Laden Sie Daten in der Tabelle training

1. Erstellen Sie eine Variable R *CcFraudCsv*, und weisen Sie die Variable den Dateipfad für die CSV-Datei, die die Beispieldaten enthält.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Beachten Sie die Hilfsfunktion **rxGetOption**. Diese Funktion wird im **RevoScaleR**-Paket zum Festlegen und Verwalten von Optionen Bezug auf lokale und remote Computekontexte bereitgestellt, z.B. das freigegebene Standardverzeichnis, die verwendete Anzahl der Prozessoren (Kerne) in Berechnungen, usw.  Dieser Aufruf ist hilfreich, da er ruft die Beispiele sind aus der Bibliothek richtig, unabhängig davon, wo Sie Ihren Code ausgeführt werden. Versuchen Sie z.B. die Funktion auf SQL Server und auf Ihrem Entwicklungscomputer auszuführen, und beachten Sie, wie sich die Pfade unterscheiden.
  
2. Definieren Sie eine Variable, um die neuen Daten zu speichern, und verwenden Sie die RxTextData-Funktion, um die Datenquelle für den Text angeben.
  
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
  
    Sie sehen, dass zwar die R-Datenobjekte im lokalen Arbeitsbereich erstellt wurden, die Tabellen aber in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank noch nicht erstellt wurden. Darüber hinaus wurde keine Daten in die R-Variable aus der Textdatei geladen.
  
4. Rufen Sie nun die Funktion **rxDataStep** auf, um die Daten in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle einzufügen.
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
  
    Wenn nach einer kurzen Pause keine Probleme mit der Verbindungszeichenfolge auftreten, sollten Sie Ergebnisse wie diese sehen:
  
      *Total Rows written: 10000, Total time: 0.466*

      *Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.577 seconds*
  
5. Aktualisieren Sie die Liste der Tabellen mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Um sicherzustellen, dass jede Variable verfügt über die korrekten Datentypen und wurde erfolgreich importiert, Sie können auch mit der rechten Maustaste der Tabellenindexes in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , und wählen Sie **oberste 1000 Zeilen auswählen**.

### <a name="load-data-into-the-scoring-table"></a>Laden Sie Daten in der bewertungs-Tabelle

1. Führen Sie dieselben Schritte zum Laden des Datasets für die Bewertung in die Datenbank durch.
  
    Starten Sie über den Pfad zur Quelldatei.
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. Verwenden der RxTextData-Funktion, um die Daten abzurufen, und speichern Sie sie in der Variablen *InTextData*.
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  Rufen Sie die RxDataStep-Funktion, um die aktuelle Tabelle mit dem neuen Schema und Daten zu überschreiben.
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - Das *inData* -Argument definiert die zu verwendende Datenquelle.
  
    - Das *outFile* -Argument gibt die Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, in der Sie die Daten speichern möchten.
  
    - Wenn die Tabelle bereits vorhanden ist und Sie nicht die Option *overwrite* verwenden, werden Ergebnisse ungekürzt eingefügt.
  
Wenn die Verbindung erfolgreich hergestellt wurde, sollte eine Nachricht angezeigt werden, die den Abschluss und die Zeit anzeigt, die zum Schreiben von Dateien in die Tabelle benötigt wurde:

*Total Rows written: 10000, Total time: 0.384*

*Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.456 seconds*

## <a name="more-about-rxdatastep"></a>Weitere Informationen zu rxDataStep

Die **RxDataStep** ist eine leistungsstarke Funktion, die mehrere Transformationen auf ein R-Datenrahmen zum Konvertieren der Daten in der Darstellung, die vom Ziel erforderliche ausführen können. In diesem Fall ist das Ziel der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Sie können auch Transformationen auf die Daten angeben, in den Argumenten um RxDataStep mithilfe von R-Funktionen. Sehen Sie Beispiele für diese Vorgänge zu einem späteren Zeitpunkt ein.

## <a name="next-step"></a>Nächster Schritt

[Fragen Sie ab und ändern Sie die SQL Server-Daten](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Arbeiten Sie mit SQL Server-Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

