---
title: "Gewusst wie: Erstellen einer gespeicherten Prozedur mithilfe von sqlrutils | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5ba99b49-481e-4b30-967a-a429b855b1bd
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Gewusst wie: Erstellen einer gespeicherten Prozedur mithilfe von sqlrutils
In diesem Thema werden die Schritte beschrieben, in denen Sie R-Code so konvertieren, dass er als gespeicherte T-SQL-Prozedur ausgeführt werden kann. Zum Erzielen bestmöglicher Ergebnisse kann es erforderlich sein, dass Ihr Code ein wenig geändert wird, damit sichergestellt ist, dass alle Eingaben parametrisiert werden können.

## <a name="step-1-format-your-r-script"></a>Schritt 1: Formatieren Ihres R-Skripts

1. Schließen Sie den gesamten Code in einer einzige Funktion ein.

   Dies bedeutet, dass alle Variablen, die in der Funktion verwendet werden, innerhalb der Funktion oder als Eingabeparameter definiert sein müssen. Siehe [Beispielcode](#samples) in diesem Thema.

## <a name="step-2-standardize-the-inputs-and-outputs"></a>Schritt 2: Standardisieren der Eingaben und Ausgaben

Die Eingabeparameter der Funktion werden die Eingabeparameter der gespeicherten SQL-Prozedur und müssen daher den folgenden Typanforderungen entsprechen:
- In den Eingabeparametern darf es höchstens einen Datenrahmen geben.
- Der Objekte in dem Datenrahmen müssen, so wie alle anderen Eingabeparameter der Funktion, die folgenden R-Datentypen haben:
    - POSIXct
    - numeric
    - character
    - integer
    - Logisch
    - raw

- Ist ein Eingabetyp keiner der hier genannten Typen, muss es serialisiert und als *raw* an die Funktion übergeben werden. In diesem Fall muss die Funktion auch Code enthalten, in dem die Eingabe deserialisiert wird.

Die Ausgabe der Funktion kann eines der folgenden Objekte sein:

- Ein Datenrahmen, der die unterstützten Datentypen enthält. Jedes Objekt im Datenrahmen muss einen der unterstützten Datentypen haben.
- Eine benannte Liste, die höchstens einen Datenrahmen enthält. Jedes Element der Liste muss einen der unterstützten Datentypen haben. 
- NULL, wenn die Funktion kein Ergebnis zurückgibt.

## <a name="step-3-make-calls-to-the-sqlrutils-package-to-generate-the-stored-procedure"></a>Schritt 3: Erstellen von Aufrufen des sqlrutils-Pakets, um die gespeicherte Prozedur zu generieren

Nachdem Sie Ihren R-Code bereinigt haben und dieser als eine einzelne Funktion aufgerufen werden kann, können Sie damit beginnen, den Code mit den Funktionen in **sqlrutils** in eine gespeicherte Prozedur zu konvertieren.

Abhängig von den Datentypen der Parameter verwenden Sie unterschiedliche Funktionen, um die Daten zu erfassen und ein Parameterobjekt zu erstellen.

1. Hat Ihre Funktion Eingabeparameter, erstellen Sie für jeden Parameter eines der folgenden Objekte: 
    - Ist der Eingabeparameter ein Datenrahmen, verwenden Sie `setInputData`.
    - Für alle anderen Eingabeparameter verwenden Sie `setInputParameter`.

2. Gibt Ihre Funktion eine Liste aus, erstellen Sie wie folgt ein Objekt, in dem die gewünschten Daten aus der Liste verarbeitet werden: 
    - Ist die Variable in der Liste ein Datenrahmen, verwenden Sie `setOutputData`.
    - Für alle anderen Elemente der Liste verwenden Sie `setOutputParameter`.
    - Gibt Ihre Funktion direkt einen Datenrahmen aus, ohne diesen erst in eine Liste einzuschließen, können Sie diesen Schritt überspringen. 
    - Überspringen Sie diesen Schritt, wenn die Funktion NULL zurückgibt.

3. Wenn alle Eingabe- und Ausgabeparameter vorbereitet sind, rufen Sie den `StoredProcedure`-Konstruktor auf, um die gespeicherte Prozedur zu erstellen, in der die R-Funktion enthalten ist.
4. Um die gespeicherte Prozedur sofort für die angegebene Datenbank zu registrieren, verwenden Sie `registerStoredProcedure`.

## <a name="step-4-execute-the-stored-procedure"></a>Schritt 4. Ausführen der gespeicherten Prozedur

1. Wenn Sie die gespeicherte Prozedur nicht aus SQL Server, sondern aus R-Code ausführen möchten, und wenn die gespeicherte Prozedur Eingabe erfordert, müssen Sie diese Eingabeparameter festlegen, bevor die Funktion ausgeführt werden kann: 
    - Rufen Sie `getInputParameters` auf, um eine Liste der Eingabeparameterobjekte abzurufen.
    - Definieren Sie eine Abfrage (`$query`) für jeden Parameter, oder legen Sie einen Wert (`$value`) für jeden Parameter fest. 

2. Verwenden Sie `executeStoredProcedure`, um die gespeicherte Prozedur aus der R-Entwicklungsumgebung auszuführen. Übergeben Sie dazu die Liste der Eingabeparameterobjekte, die Sie festgelegt haben.

## <a name="a-name-samplesaexamples-prepare-your-code"></a><a name = "samples"></a>Beispiele: Vorbereiten des Codes 

In diesem Beispiel werden in dem R-Code folgende Schritte ausgeführt: Lesen von Daten aus einer Datenbank, Ausführen einiger Transformationen für die Daten und Speichern dieser Daten in einer anderen Datenbank. Dieses einfache Beispiel wird nur dazu verwendet, zu veranschaulichen, wie Sie Ihren R-Code neu anordnen könnten, um eine einfachere Schnittstelle für die Konvertierung einer gespeicherten Prozedur bereitzustellen.

**Vor dem Formatieren**


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
Wenn Sie eine ODBC-Verbindung verwenden, statt die *RxSqlServerData*-Funktion aufzurufen, müssen Sie die Verbindung mit *rxOpen* öffnen, bevor Sie Vorgänge in der Datenbank ausführen können.



**Nach dem Formatieren**

In der neu formatierten Version ist der Funktionsname in der ersten Zeile definiert.

Der gesamte weitere Code aus Ihrer ursprünglichen R-Lösung wird Teil dieser Funktion. 

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
Obwohl Sie die ODBC-Verbindung nicht explizit in Ihrem Code öffnen müssen, ist weiterhin eine ODBC-Verbindung erforderlich, um **sqlrutils** zu verwenden. 


## <a name="see-also"></a>Siehe auch

[Generieren einer gespeicherten Prozedur mithilfe von sqlrutils](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

