---
title: "Erstellen von SQL Server-Datenobjekten mithilfe von RxSqlServerData | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: bcf5f7ff-795b-4815-b163-bcddd496efce
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Erstellen von SQL Server-Datenobjekten mithilfe von RxSqlServerData
Sie haben jetzt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank und die erforderlichen Berechtigungen zum Arbeiten mit den Daten erstellt und erstellen nun Objekte in R, mit denen Sie mit den Daten arbeiten können – sowohl auf dem Server und auf Ihrer Arbeitsstation.  
  
## Erstellen der SQL Server-Daten-Objekte  
In diesem Schritt erstellen Sie mit R zwei Tabellen und füllen sie aus. Beide Tabellen enthalten simulierte Kreditkarten-Betrugsdaten. Eine Tabelle wird zum Trainieren der Modelle verwendet, die andere Tabelle für die Bewertung. 

Zum Erstellen von Tabellen auf dem entfernten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer verwenden Sie die `RxSqlServerData` Funktion aus dem **RevoScaleR**-Paket.  

> [!TIP]
> Wenn Sie R-Tools für Visual Studio verwenden, wählen Sie **R-Tools** aus der Symbolleiste aus, und klicken Sie auf **Fenster**, um Optionen zum Debuggen und Anzeigen von R-Variablen anzuzeigen.
  
#### Schulung-Datentabelle erstellen  
  
1.  Geben Sie die Datenbank-Verbindungszeichenfolge in einer R-Variablen an. Hier haben wir zwei Beispiele gültiger ODBC-Verbindungszeichenfolgen für SQL Server bereitgestellt: eine, die eine SQL-Anmeldung verwendet und eine für die integrierte Windows-Authentifizierung (empfohlen).

    **Verwenden einer SQL-Anmeldung**
    ```R  
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"   
    ```

    **Verwenden der integrierten Windows-Authentifizierung**
    ```R  
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
    ```

    Achten Sie darauf, dass der Instanzname, Datenbankname, Benutzername und das Kennwort nach Bedarf geändert werden.  
  
2.  Geben Sie den Namen der Tabelle an, die Sie erstellen möchten, und speichern Sie ihn in einer R-Variablen.  
  
    ```R  
    sqlFraudTable <- "ccFraudSmall"       
    ```  
  
    Da die Instanz- und Datenbanknamen bereits als Teil der Verbindungszeichenfolge beim Kombinieren der zwei Variablen angegeben werden, wird der *vollqualifizierte* Name der neuen Tabelle _instance.database.schema.ccFraudSmall_.  
  
3.  Fügen Sie vor dem Instanziieren des Datenquellenobjekts eine Zeile hinzu, die den zusätzlichen Parameter *rowsPerRead* angibt.  Der *rowsPerRead*-Parameter steuert, wie viele Datenzeilen in jeden Batch eingelesen werden.  
  
    ```R  
    sqlRowsPerRead = 5000   
    ```  
  
    Obwohl dieser Parameter optional ist, ist er wichtig für die Handhabung der Speicherauslastung und für effiziente Berechnungen.  Die meisten analytischen Funktionen in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] verarbeiten Daten in Segmenten und sammeln Zwischenergebnisse an, die die endgültigen Berechnungen zurückgeben, nachdem alle Daten gelesen wurden.  
  
    Wenn der Wert dieses Parameters zu groß ist, könnte der Datenzugriff möglicherweise langsam sein, da Sie nicht über genügen Speicher verfügen, um einen solch großen Datenblock effizient zu verarbeiten.  Wenn der Wert *rowsPerRead* zu niedrig ist, kann sich in einigen Systemen die Leistung verringern.  
  
    In dieser exemplarischen Vorgehensweise verwenden Sie die Batchprozessgröße, definiert von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz, zur Steuerung der Anzahl der Zeilen in jedem Segment, und speichern diesen Wert in der Variablen *sqlRowsPerRead*.  Es wird empfohlen, dass Sie bei der Arbeit mit einem großen Datensatz mit dieser Einstellung auf Ihrem System experimentieren.  
  
4.  Schließlich definieren Sie eine Variable für das neue Datenquellenobjekt, und übergeben Sie die zuvor definierten Argumente an den *RxSqlServerData*-Konstruktor. Beachten Sie, dass dadurch nur das neue Datenquellenobjekt erstellt wird, es jedoch nicht aufgefüllt wird.  
  
    ```R  
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable, 
       rowsPerRead = sqlRowsPerRead)  
    ```  

  
#### Bewertungs-Datentabelle erstellen  

Sie verwenden die gleiche Vorgehensweise, um die Tabelle zu erstellen, in der die Bewertungsdaten erhalten sind.  
  
1.  Erstellen Sie eine neue R-Variable, *sqlScoreTable*, um den Namen der Tabelle für die Bewertung zu speichern.  
  
    ```R  
    sqlScoreTable <- "ccFraudScoreSmall"  
    ```  
  
2.  Geben Sie die Variable als Argument an die Funktion *RxSqlServerData*, um ein zweites Datenquellenobjekt, *sqlScoreDS*, zu definieren.  
  
    ```R   
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead) 
    ```  
  
  
Da Sie bereits die Verbindungszeichenfolge und andere Parameter als Variablen im R-Arbeitsbereich definiert haben, ist es einfach, neue Datenquellen für andere Tabellen, Sichten oder Abfragen zu erstellen. Geben Sie einfach einen anderen Tabellennamen an.  
  
Später in diesem Tutorial erfahren Sie, wie Sie ein Datenquellenobjekt auf Grundlage einer SQL-Abfrage erstellen.  
  
## Laden von Daten in SQL-Tabellen mithilfe von R  
Sie haben die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabellen nun erstellt und können Daten in die Tabellen laden mithilfe der entsprechenden **Rx**-Funktion.  
  
Das **RevoScaleR**-Paket enthält Funktionen, die viele unterschiedliche Datenquellen unterstützen: Hier verwenden Sie *RxTextData*, um das Datenquellenobjekt zu generieren. Es gibt weitere Funktionen zum Erstellen von Datenquellenobjekten von Hadoop-Daten, ODBC-Daten, usw.  
  
> [!NOTE]  
> Für diesen Abschnitt müssen Sie über „DDL ausführen“-Berechtigungen für die Datenbank verfügen.
  
#### Daten in die Schulungstabelle laden  
  
1.  Erstellen Sie eine R-Variable, *ccFraudCsv*, und weisen Sie der Variable den Dateipfad für die CSV-Datei zu, die die Beispieldatei enthält, die in Microsoft R enthalten ist.  
  
    ```R  
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")   
    ```  
  
    Beachten Sie die Hilfsfunktion *rxGetOption*. Diese Funktion wird im **RevoScaleR**-Paket zum Festlegen und Verwalten von Optionen Bezug auf lokale und remote Computekontexte bereitgestellt, z.B. das freigegebene Standardverzeichnis, die verwendete Anzahl der Prozessoren (Kerne) in Berechnungen, usw.  Diese Funktion ist hilfreich, da sie die Beispiele aus der richtigen Bibliothek abruft, unabhängig vom Ausführungsort Ihres Codes. Versuchen Sie z.B. die Funktion auf SQL Server und auf Ihrem Entwicklungscomputer auszuführen, und beachten Sie, wie sich die Pfade unterscheiden.
  
2.  Definieren Sie eine Variable, um die neuen Daten zu speichern, und verwenden Sie die Funktion *RxTextData* zur Angabe der Text-Datenquelle.  
  
    ```R  
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(   
        "custID" = "integer", "gender" = "integer", "state" = "integer",   
        "cardholder" = "integer", "balance" = "integer",    
        "numTrans" = "integer",   
        "numIntlTrans" = "integer", "creditLine" = "integer",    
        "fraudRisk" = "integer"))    
    ```  
  
    Das Argument *colClasses* ist wichtig. Sie verwenden es zur Angabe des Datentyps jeder Spalte von Daten, die aus der Textdatei geladen wird. In diesem Beispiel werden alle Spalten als Text behandelt, mit Ausnahme der benannten Spalten, die als ganze Zahlen verarbeitet werden.  
  
3.  Schauen wir uns jetzt einmal die Datenbank in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] an.  Aktualisieren Sie die Liste der Tabellen in der Datenbank.  
  
    Sie sehen, dass zwar die R-Datenobjekte im lokalen Arbeitsbereich erstellt wurden, die Tabellen aber in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank noch nicht erstellt wurden. Es wurden auch keine Daten aus der Textdatei in die R-Variable geladen. 
  
4.  Rufen Sie nun die Funktion *rxDataStep* auf, um die Daten in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle einzufügen.  
  
    ```R  
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)   
    ```  
  
    Wenn nach einer kurzen Pause keine Probleme mit der Verbindungszeichenfolge auftreten, sollten Sie Ergebnisse wie diese sehen:  
  
      *Total Rows written: 10000, Total time: 0.466*
      *Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.577 seconds*  
  
5.  Aktualisieren Sie die Liste der Tabellen mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Um sicherzustellen, dass jede Variable über die korrekten Datentypen verfügt und erfolgreich importiert wurde, können Sie auch mit der rechten Maustaste in die Tabelle in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] klicken und die Option **Die ersten 1000 Zeilen auswählen** auswählen.  
  
#### Daten in die Bewertungstabelle laden  
  
1.  Führen Sie dieselben Schritte zum Laden des Datasets für die Bewertung in die Datenbank durch.  
  
    Starten Sie über den Pfad zur Quelldatei.  
  
    ```R  
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")   
    ```  
  
2.  Verwenden Sie die Funktion *RxTextData*, um die Daten abzurufen, und speichern Sie sie in der Variablen *inTextData*.  
  
    ```R  
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(   
        "custID" = "integer", "gender" = "integer", "state" = "integer",   
        "cardholder" = "integer", "balance" = "integer",    
        "numTrans" = "integer",   
        "numIntlTrans" = "integer", "creditLine" = "integer"))  
  
    ```  
  
3.  Rufen Sie die Funktion *rxDataStep* auf, um die aktuelle Tabelle mit dem neuen Schema und Daten zu überschreiben.  
  
    ```R  
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)    
    ```  
  
    -   Das *inData*-Argument definiert die zu verwendende Datenquelle.  
  
    -   Das *outFile*-Argument gibt die Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, in der Sie die Daten speichern möchten.  
  
    -   Wenn die Tabelle bereits vorhanden ist und Sie nicht die Option *overwrite* verwenden, werden Ergebnisse ungekürzt eingefügt.  
  
Wenn die Verbindung erfolgreich hergestellt wurde, sollte eine Nachricht angezeigt werden, die den Abschluss und die Zeit anzeigt, die zum Schreiben von Dateien in die Tabelle benötigt wurde: 

*Total Rows written: 10000, Total time: 0.384*
*Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.456 seconds*  
  
## Weitere Informationen zu rxDataStep  
*rxDataStep* ist eine leistungsstarke Funktion im **RevoScaleR**-Paket, die mehrere Transformationen auf einen R-Datenrahmen durchführen kann, um Daten in die erforderliche Ziel-Darstellung zu konvertieren. In diesem Fall ist das Ziel der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Sie können auch Transformationen für die Daten angeben. Sie können z.B. angeben, dass neue Spalten ausgeschlossen werden sollen, Sie können neue Spalten hinzufügen oder die Datentypen ändern, indem Sie R-Funktionen in den Argumenten von *rxDataStep* verwenden. Sehen Sie Beispiele für diese Vorgänge in [Lektion 4](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md).  
  
## Nächster Schritt  
[Abfragen und Ändern der SQL Server-Daten &#40;Tieferer Einblick in Data Science&#41;](../../advanced-analytics/r-services/query-and-modify-the-sql-server-data-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Lektion 1: Work with SQL Server Data using R &#40;Data Science Deep Dive&#41; (Arbeiten mit SQL Server-Daten mithilfe von R (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
