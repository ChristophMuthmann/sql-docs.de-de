---
title: 'Vorgehensweise: Erstellen einer gespeicherten Prozedur mithilfe von sqlrutils| Microsoft-Dokumentation'
ms.custom: 
ms.date: 12/16/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 5ba99b49-481e-4b30-967a-a429b855b1bd
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: ad0cf99c59bcd3295acf0e1c29b14c8523f6f925
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="create-a-stored-procedure-using-sqlrutils"></a>Erstellen einer gespeicherten Prozedur mithilfe von sqlrutils
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Thema werden die Schritte beschrieben, in denen Sie R-Code so konvertieren, dass er als gespeicherte T-SQL-Prozedur ausgeführt werden kann. Zum Erzielen bestmöglicher Ergebnisse kann es erforderlich sein, dass Ihr Code ein wenig geändert wird, damit sichergestellt ist, dass alle Eingaben parametrisiert werden können.

## <a name="bkmk_rewrite"></a>Schritt 1: Schreiben Sie R-Skript

Schreiben Sie die besten Ergebnisse erzielen Sie den R-Code, um es als einzelne Funktion gekapselt.

Alle Variablen, die von der Funktion verwendeten sollte innerhalb der Funktion definiert werden, oder als Eingabeparameter definiert werden soll. Siehe [Beispielcode](#samples) in diesem Thema.

Außerdem wird, da die Eingabeparameter für die R-Funktion werden die Eingabeparameter des SQL-Prozedur enthält, müssen Sie sicherstellen, dass Ihre Eingaben und Ausgaben zu folgendem Typ entsprechen:

### <a name="inputs"></a>Eingaben

In den Eingabeparametern darf es höchstens einen Datenrahmen geben.

Der Objekte in dem Datenrahmen müssen, so wie alle anderen Eingabeparameter der Funktion, die folgenden R-Datentypen haben:
- POSIXct
- numeric
- character
- integer
- Logisch
- raw

Ist ein Eingabetyp keiner der hier genannten Typen, muss es serialisiert und als *raw*an die Funktion übergeben werden. In diesem Fall muss die Funktion auch Code enthalten, in dem die Eingabe deserialisiert wird.

### <a name="outputs"></a>Ausgaben

Die Ausgabe der Funktion kann eines der folgenden Objekte sein:

- Ein Datenrahmen, der die unterstützten Datentypen enthält. Jedes Objekt im Datenrahmen muss einen der unterstützten Datentypen haben.
- Eine benannte Liste, die höchstens einen Datenrahmen enthält. Jedes Element der Liste muss einen der unterstützten Datentypen haben.
- NULL, wenn die Funktion kein Ergebnis zurückgibt.

## <a name="step-2-generate-required-objects"></a>Schritt 2: Generieren der benötigten Objekte

Nachdem Ihre R-Code bereinigt wurden und als einzelne Funktion aufgerufen werden kann, verwenden Sie die Funktionen in der **Sqlrutils** Paket So bereiten Sie vor der Eingaben und Ausgaben in ein Formular, das an den Konstruktor übergeben werden kann, die tatsächlich erstellt die gespeicherte Prozedur.

**Sqlrutils** bietet Funktionen, die definieren, die Eingabedaten Schema und den Typ und die Ausgabe Datenschema und den Typ zu definieren. Darüber hinaus Funktionen, die R-Objekte in der gewünschten Ausgabetyp konvertieren können. Möglicherweise stellen Sie mehrere Funktionsaufrufe der benötigten Objekte, abhängig von den Datentypen zu erstellen, die im Code verwendet wird.

### <a name="inputs"></a>Eingaben

Wenn Ihre Funktion Eingaben akzeptiert für jeden Eingabe-, rufen Sie die folgenden Funktionen ein:

- `setInputData`Wenn die Eingabe eine Datenrahmen ist.
- `setInputParameter`Bei allen anderen Eingabetypen

Wenn Sie jeden Funktionsaufruf vornehmen, wird ein R-Objekt erstellt, wenn Sie später als Argument übergeben werden `StoredProcedure`, um die vollständige gespeicherte Prozedur zu erstellen.

### <a name="outputs"></a>Ausgaben

**Sqlrutils** stellt mehrere Funktionen bereit, für das Konvertieren von R Objekte wie z. B. die SQL Server erforderlichen data.frame Listen.
Gibt Ihre Funktion direkt einen Datenrahmen aus, ohne diesen erst in eine Liste einzuschließen, können Sie diesen Schritt überspringen.
Sie können auch der Konvertierung diesen Schritt überspringen, wenn die Funktion NULL zurück.

Beim Konvertieren einer Liste oder für das Abrufen eines bestimmten Artikels aus einer Liste Wählen Sie auf diese Funktionen:

- `setOutputData`Wenn die Variable für die abzurufenden aus der Liste einen Datenrahmen
- `setOutputParameter`für alle anderen Elemente der Liste

Wenn Sie jeden Funktionsaufruf vornehmen, wird ein R-Objekt erstellt, wenn Sie später als Argument übergeben werden `StoredProcedure`, um die vollständige gespeicherte Prozedur zu erstellen.

## <a name="step-3-generate-the-stored-procedure"></a>Schritt 3: Generieren Sie die gespeicherte Prozedur

Wenn alle Parameter für Eingabe- und bereit sind, stellen Sie einen Aufruf der `StoredProcedure` Konstruktor.

**Verwendung**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

Um zu veranschaulichen, wird davon ausgegangen, dass Sie eine gespeicherte Prozedur namens erstellen möchten **Sp_rsample** mit diesen Parametern:

- Verwendet eine vorhandene Funktion **Foosql**. Die Funktion wurde basierend auf vorhandenem Code im R-Funktion **Foo**, aber Sie geändert, dass die Funktion, um den Anforderungen entsprechen, wie in beschrieben [in diesem Abschnitt](#bkmk_rewrite), und mit dem Namen der aktualisierten-Funktion als  **Foosql**.
- Verwendet die Datenrahmen **Queryinput** als Eingabe
- Generiert als Ausgabe einen Datenrahmen mit dem R-Variablennamen **Sqloutput**
- Den T-SQL-Code als in-Datei erstellt werden soll die `C:\Temp` Ordner, damit Sie später mithilfe von SQL Server Management Studio ausführen können

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> Da Sie die Datei im Dateisystem schreiben, können Sie die Argumente auslassen, die Verbindung mit der Datenbank zu definieren.

Die Ausgabe der Funktion wird eine T-SQL-Prozedur, die auf einer Instanz von SQL Server 2016 (erfordert R Services) oder SQL Server-2017 (erfordert Machine Learning-Dienste mit R) ausgeführt werden können. 

Weitere Beispiele finden Sie in der Hilfe Paket durch Aufrufen von `help(StoredProcedure)` aus einer R-Umgebung.

## <a name="step-4-register-and-run-the-stored-procedure"></a>Schritt 4. Registrieren und Ausführen der gespeicherten Prozedur

Es gibt zwei Möglichkeiten, dass die gespeicherte Prozedur ausgeführt werden kann:

- Verwenden von T-SQL, von jedem beliebigen Client, die Verbindungen mit der SQL Server 2016 oder 2017 von SQL Server-Instanz unterstützt
- Aus einer R-Umgebung

Beide Methoden erfordern, dass die gespeicherte Prozedur registriert werden, in der Datenbank, in dem Sie die gespeicherte Prozedur verwenden möchten.

### <a name="register-the-stored-procedure"></a>Registrieren Sie die gespeicherte Prozedur

Sie können die gespeicherte Prozedur mithilfe von R registrieren, oder führen Sie die CREATE PROCEDURE-Anweisung, in T-SQL.

- Verwenden von T-SQL.  Wenn Sie mehr mit T-SQL vertraut sind, öffnen Sie SQl Server Management Studio (oder einem beliebigen anderen Client, der SQL-DDL Befehle ausführen kann), und führen Sie die CREATE PROCEDURE-Anweisung, die mit dem Code vorbereitet, indem die `StoredProcedure` Funktion.
- Mithilfe von r Während Sie sich noch in der R-Umgebung befinden, können Sie die `registerStoredProcedure` -Funktion in **Sqlrutils** die gespeicherte Prozedur mit der Datenbank zu registrieren.

  Sie konnten z. B. die gespeicherte Prozedur registrieren **Sp_rsample** in der Instanz und die Datenbank, die in definierten *SqlConnStr*, durch Aufruf dieser R:

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> Unabhängig davon, ob Sie R oder SQL verwenden müssen Sie die Anweisung mit einem Konto mit Berechtigungen zum Erstellen von neuen Datenbankobjekten ausführen.

### <a name="run-using-sql"></a>Führen Sie mit SQL

Nachdem die gespeicherte Prozedur erstellt wurde, öffnen Sie eine Verbindung mit der SQL-Datenbank, die mit einem beliebigen Client, der T-SQL unterstützt, und übergeben Sie Werte für alle Parameter, die von der gespeicherten Prozedur erforderlich.

### <a name="run-using-r"></a>Führen Sie mithilfe von R

Einige zusätzliche Vorbereitung ist erforderlich, wenn die gespeicherte Prozedur aus R-Code, sondern ab SQL Server ausgeführt werden soll. Z. B. wenn die gespeicherte Prozedur Eingabewerte erfordert, müssen Sie die Eingabeparameter festlegen, bevor die Funktion ausgeführt werden kann, und diese Objekte dann an die gespeicherte Prozedur in Ihrem R-Code übergeben.

Der Gesamtprozess des Aufrufs der vorbereiteten SQL-Prozedur lautet wie folgt:

1. Rufen Sie `getInputParameters` auf, um eine Liste der Eingabeparameterobjekte abzurufen.
2. Definieren Sie eine Abfrage ( `$query` ) für jeden Parameter, oder legen Sie einen Wert ( `$value` ) für jeden Parameter fest.
3. Verwenden Sie `executeStoredProcedure` , um die gespeicherte Prozedur aus der R-Entwicklungsumgebung auszuführen. Übergeben Sie dazu die Liste der Eingabeparameterobjekte, die Sie festgelegt haben.

## <a name = "samples"></a>Beispiel

In diesem Beispiel wird gezeigt, die vor und nach Versionen eines R-Skripts, die führt einige Transformationen auf die Daten, ruft Daten aus einer SQL Server-Datenbank ab und speichert sie in einer anderen Datenbank.

Dieses einfache Beispiel dient nur zu veranschaulichen, wie Sie R-Code zum Konvertieren in eine gespeicherte Prozedur zu vereinfachen, neu anordnen können.

### <a name="before-code-preparation"></a>Bevor Sie Code zur Vorbereitung


```R
sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineSrc;Trusted_Connection=Yes;"
  
sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineTest;Trusted_Connection=Yes;"
  
sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"
  
dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
xFunc <- function(data) {
    data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
    return(data)
    }
  
xVars <- c("CRSDepTime")
  
sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
rxOpen(dsSqlFrom)
rxOpen(dsSqlTo)
  
if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo))   {
    rxSqlServerDropTable("cleanData")}
  
rxDataStep(inData = dsSqlFrom, 
     outFile = dsSqlTo,
     transformFunc = xFunc,
     transformVars = xVars,
     overwrite = TRUE)
```

> [!NOTE]
> 
> Bei Verwendung eine ODBC-Verbindung statt Aufrufen der *RxSqlServerData* -Funktion, müssen Sie die Verbindung mit öffnen *RxOpen* vor dem Ausführen von Vorgängen in der Datenbank.


### <a name="after-code-preparation"></a>Nach der Vorbereitung von code

In der aktualisierten Version definiert die erste Zeile den Namen der Funktion. Der übrige Code von der ursprünglichen R-Lösung wird ein Teil dieser Funktion.

```R
myetl1function <- function() { 
   sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=Airline01;Trusted_Connection=Yes;"
   sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer02;Database=Airline02;Trusted_Connection=Yes;"
    
   sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"

   dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
   dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
   xFunc <- function(data) {
     data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
     return(data)}
  
   xVars <- c("CRSDepTime")
  
   sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
   if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo)) {rxSqlServerDropTable("cleanData")}
  
   rxDataStep(inData = dsSqlFrom, 
        outFile = dsSqlTo,
        transformFunc = xFunc,
        transformVars = xVars,
        overwrite = TRUE)
   return(NULL)
}
```

> [!NOTE]
> 
> Obwohl Sie die ODBC-Verbindung nicht explizit in Ihrem Code öffnen müssen, ist weiterhin eine ODBC-Verbindung erforderlich, um **sqlrutils**zu verwenden.

## <a name="see-also"></a>Siehe auch

[Generieren einer gespeicherten Prozedur mithilfe von sqlrutils](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)


