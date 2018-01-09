---
title: R und SQL-Typen und Daten Datenobjekte (R in SQL-Schnellstart) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.assetid: 1a17fc5b-b8c5-498f-b8b1-3b7b43a567e1
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d3773c56310b3d91b20acd05b40fc00ae5003b43
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="r-and-sql-data-types-and-data-objects-r-in-sql-quickstart"></a>R und SQL-Typen und Daten Datenobjekte (R in SQL-Schnellstart)

In diesem Schritt erfahren Sie mehr über einige häufig auftretende Probleme, die beim Verschieben von Daten zwischen R und SQL Server auftreten:

+ Datentypen stimmen manchmal nicht überein
+ Implizite Konvertierungen möglicherweise stattfinden
+ Cast- und Convert-Vorgänge sind manchmal erforderlich
+ R und SQL verwenden verschiedene Datenobjekte

## <a name="always-return-r-data-as-a-data-frame"></a>Geben Sie R-Daten immer als einen Datenrahmen zurück

Wenn Ihr Skript Ergebnisse von R zum SQL Server zurückgibt, muss es die Daten als **data.frame** zurückgeben. Jede andere Objektart, die Sie in Ihrem Skript generieren –, d.h. eine Liste, ein Faktor, ein Vektor oder binäre Daten – müssen zu einem Datenrahmen konvertiert werden, wenn sie als Teil der gespeicherten Prozedurergebnisse ausgegeben werden sollen. Es gibt mehrere R-Funktionen, um die Änderung anderer Objekte zu einem Datenrahmen zu unterstützen. Sie können auch ein binäres Modell serialisieren und es in einen Datenrahmen zurückgeben. Mehr dazu erfahren Sie später in diesem Lernprogramm.

Zunächst sehen wir experimentieren Sie mit einigen grundlegenden R-R-Objekte – Vektoren, Matrizen und Listen – und beobachten Sie, wie die Konvertierung in einem Datenrahmen die Ausgabe an SQL Server übergeben ändert.

Vergleichen Sie diese beiden "Hello World"-Skripts in R. Suchen Sie die Skripts nahezu identisch, aber das erste gibt eine einzelne Spalte der drei folgenden Werte an, während die zweite gibt drei Spalten mit einem einzelnen Wert jedes.

**Beispiel 1**

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
     , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
     , @input_data_1 = N' ';
```

**Beispiel 2**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'
      , @input_data_1 = N'  ';
```

## <a name="identifying-the-schema-and-data-types-of-r-data"></a>Identifizieren Sie die Schemen- und Datenarten der R-Daten

Warum sind die Ergebnisse so unterschiedlich?

Die Antwort finden Sie in der Regel mithilfe des R-`str()`-Befehls. Fügen Sie die Funktion `str(object_name)` in Ihrem R-Skript hinzu, um das Datenschema des festgelegten R-Objekts als Informationsmeldung zurückzugeben. Nachrichten finden Sie unter **Nachrichten**, im Bereich des Visual Studio-Code oder unter der **Nachrichten**-Registerkarte in SSMS.

Um zu ermitteln, warum Beispiel 1 und Beispiel 2 solch unterschiedliche Ergebnisse haben, fügen Sie die Zeile `str(OutputDataSet)` am Ende der _@script_-Variablendefinition in jeder Anweisung, wie folgt ein:

**Beispiel 1 mit str-Funktion hinzugefügt**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**Beispiel 2 mit str-Funktion hinzugefügt**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet)' , 
  @input_data_1 = N'  ';
```

Überprüfen Sie nun den Text in **Nachrichten**, um festzustellen aus welchem Grund die Ausgabe anders ist.

**Ergebnisse - Beispiel 1**

```
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**Ergebnisse - Beispiel 2**

```
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

Wie Sie sehen können, hatte eine geringfügige Änderung in der R-Syntax einen großen Einfluss auf das Schema der Ergebnisse. Es wird nicht warum besprochen, da Unterschiede in den R-Datentypen von Hadley Wickham gründlicher in diesem Artikel erläutert werden: [R Datenstrukturen](http://adv-r.had.co.nz/Data-structures.html).

Jetzt müssen Sie nur Bedenken, dass Sie die erwarteten Ergebnisse überprüfen müssen, wenn Sie R-Objekte in Datenrahmen umwandeln müssen.

> [!TIP]
> 
> Sie können auch R-Identity-Funktionen verwenden, z. B. `is.matrix`, `is.vector`usw.

## <a name="implicit-conversion-of-data-objects"></a>Implizite Konvertierung von Datenobjekten

Jedes R-Datenobjekt verfügt über seine eigenen Regeln darüber, wie Werte verarbeitet werden, wenn sie mit anderen Datenobjekten kombiniert werden, sofern die beiden Datenobjekte über die gleiche Anzahl an Dimensionen verfügen oder jedes Datenobjekt heterogene Datentypen enthält.

Nehmen wir beispielsweise an, dass Sie die folgende Anweisung zur Matrixmultiplikation mit R ausführen.  Sie vervielfältigen eine einspaltige Matrix mit den drei Werten durch ein Array mit vier Werten und erwarten daher, dass eine 4 x 3-Matrix entsteht.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:15);
    OutputDataSet <- as.data.frame(x %*% y);'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));
```

Im Hintergrund wird die Spalte mit drei Werten in eine einspaltige Matrix konvertiert. Das Array `y` wird implizit in eine einspaltige Matrix umgewandelt, um die beiden Argumente anzupassen, da eine Matrix nur ein Sonderfall eines Arrays in R ist.

**Ergebnisse**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

Beachten Sie jedoch, was geschieht, wenn Sie die Größe des Arrays ändern `y`.

```sql
execute sp_execute_external_script
   @language = N'R'
   , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:14);
   OutputDataSet <- as.data.frame(y %*% x);'
   , @input_data_1 = N' SELECT [Col1]  from RTestData;'
   WITH RESULT SETS (([Col1] int ));
```

Jetzt gibt R einen einzelnen Wert als Ergebnis zurück.

**Ergebnisse**
    
|Col1|
|---|
|1542|

Warum? In diesem Fall, da die beiden Argumente als Vektoren derselben Länge behandelt werden können, gibt R als eine Matrix der inneren Produkt zurück.  Dies ist das erwartete Verhalten gemäß der Regeln der linearen Algebra. Es kann jedoch Probleme verursachen, wenn die Downstream-Anwendung erwartet, dass das Ausgabeschema sich nie ändert!

> [!TIP]
> 
> Abrufen von Fehlern? Diese Beispiele erfordern in der Tabelle **RTestData**. Wenn Sie die Test-Datentabelle erstellt haben, gehen Sie zurück zu diesem Thema: [arbeiten mit Eingaben und Ausgaben](../tutorials/rtsql-working-with-inputs-and-outputs.md).
> 
> Wenn Sie die Tabelle erstellt haben, aber weiterhin eine Fehlermeldung erhalten, stellen Sie sicher, dass Sie die gespeicherte Prozedur ausgeführt werden, im Kontext der Datenbank, die die Tabelle enthält, und nicht im **master** oder einer anderen Datenbank.
> 
> Darüber hinaus wird empfohlen, dass Sie die Verwendung von temporärer Tabellen für diese Beispiele vermeiden. Einige R-Clients beendet eine Verbindung zwischen Batches, löschen temporäre Tabellen.

## <a name="merge-or-multiply-columns-of-different-length"></a>Zusammenführen oder Multiplizieren von Spalten mit unterschiedlicher Länge

R bietet maximale Flexibilität beim für die Arbeit mit Vektoren unterschiedliche Größen haben, und für diese Spalte-ähnliche Strukturen in Datenrahmen kombiniert werden. Vektorenlisten können aussehen wie eine Tabelle, aber sie befolgen nicht alle Regeln, die Datenbanktabellen steuern.

Zum Beispiel legt das folgende Skript ein numerisches Array der Länge 6 fest und speichert es in der R-Variable `df1`. Numerische Array wird dann mit der ganzen Zahlen der RTestData-Tabelle, die drei (3) Werte enthält, stellen einen neue Datenrahmen kombiniert `df2`.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
               df1 <- as.data.frame( array(1:6) );
               df2 <- as.data.frame( c( InputDataSet , df1 ));
               OutputDataSet <- df2'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));
```

Zum Ausfüllen eines Datenrahmens, wiederholt R die Elemente, die aus RTestData aufgerufen wurden, so oft wie erforderlich, um die Anzahl der Elemente im Array `df1` zuzuordnen.

**Ergebnisse**
    
|*Col2*|*Col3*|
|----|----|
|1|1|
|10|2|
|100|3|
|1|4|
|10|5|
|100|6|

Beachten Sie, dass der Datenrahmen nur wie eine Tabelle aussieht, aber eigentlich eine Vektorenliste ist.

## <a name="cast-or-convert-sql-server-data"></a>Cast und Convert von SQL Serverdaten

R und SQL Server verwenden nicht die gleichen Datentypen, sodass Sie eine Abfrage im SQL Server durchführen können, um Daten abzurufen und diese an die R-Laufzeit zu übergeben, erfolgt in der Regel eine Art implizite Konvertierung. Eine weitere Reihe von Konvertierungen findet statt, wenn Sie Daten von R an SQL Server zurückgeben.

- SQL Server überträgt die Daten aus der Abfrage an den R-Prozess, durch den Launchpad-Dienst verwaltet und konvertiert es in einer internen Darstellung für größere Effizienz.
- Die R-Laufzeit lädt die Daten in eine data.frame-Variable und führt ihre eigenen Vorgänge für die Daten aus.
- Das Datenbankmodul gibt die Daten über eine sichere interne Verbindung an den SQL Server zurück und zeigt die Daten in Form von SQL Server-Datentypen.
- Sie rufen Sie Daten über eine Verbindung mit dem SQL Server mithilfe einer Client- oder Netzwerk-Bibliothek auf, die SQL-Abfragen und tabellarische Datensätze verarbeiten kann. Diese Clientanwendung kann die Daten auf andere Weise beeinträchtigen.

Um zu sehen, wie dies funktioniert, führen Sie eine Abfrage, wie diese im Datawarehouse AdventureWorksDW durch. In dieser Ansicht werden Verkaufsdaten zurückgegeben, die zum Erstellen von Prognosen verwendet werden.

```sql
SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
> 
> Sie können eine beliebige Version von AdventureWorks verwenden, oder erstellen eine andere Abfrage unter Verwendung einer Datenbank Ihrer Wahl. Der Punkt ist, um zu versuchen, einige Daten zu behandeln, die Text, "DateTime" und numerische Werte enthält.

Nun versuchen Sie, diese Abfrage als Eingabe für die gespeicherte Prozedur einfügen.

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

Wenn Sie eine Fehlermeldung erhalten, müssen Sie wahrscheinlich einige Änderungen am Abfragetext vornehmen. Zum Beispiel das Zeichenfolgenprädikat in der WHERE-Klausel muss von jeweils zwei einfachen Anführungszeichen umschlossen sein.

Nachdem die Abfrage funktioniert, überprüfen Sie die Ergebnisse der `str`-Funktion, um zu sehen wie R die Eingabedaten behandelt.

**Ergebnisse**

```
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ Die datetime-Spalte wurde als R-Datentyp **POSIXct** verarbeitet.
+ Die Textspalte "ProductSeries" wurde als identifiziert eine **Faktor**, d. h. eine Variable "categorical". Zeichenfolgenwerte werden standardmäßig als Faktoren verarbeitet. Wenn Sie R eine Zeichenfolge übergeben, wird diese in eine ganze Zahl für die interne Verwendung konvertiert und dann zurück in die Ausgabe der Zeichenfolge zugeordnet.

### <a name="summary"></a>Zusammenfassung

Auch diese kurze Beispiele können Sie sehen die Notwendigkeit, überprüfen Sie die Auswirkungen der Datenkonvertierung bei der Übergabe von SQL-Abfragen als Eingabe. Da einige SQL Server-Datentypen von R nicht unterstützt werden, sollten Sie diese Möglichkeiten zur Vermeidung von Fehlern:

+ Testen Sie Ihre Daten im voraus, und überprüfen Sie, Spalten oder die Werte in Ihrem Schema, das ein Problem bei der Verwendung in R-Code übergeben werden.
+ Legen Sie Spalten in der Eingabedatenquelle einzeln fest, anstatt `SELECT *` zu verwenden, und verstehen Sie, wie jede Spalte verarbeitet wird.
+ Führen Sie explizite Umwandlungen nach Bedarf beim Vorbereiten der Eingabedaten durch, um Überraschungen zu vermeiden.
+ Vermeiden Sie übergeben von Spalten mit Daten (z. B. GUIDS oder aktualisieren), die Fehler verursachen und nicht für die Modellierung nützlich sind.

Weitere Informationen zu unterstützten und nicht unterstützten Datentypen finden Sie unter [R-Bibliotheken und Datentypen](../r/r-libraries-and-data-types.md).

Informationen zu Auswirkungen auf die Leistung zur Laufzeit Konvertierung von Zeichenfolgen in numerische Faktoren finden Sie unter [leistungsoptimierung für SQL Server R Services](../r/sql-server-r-services-performance-tuning.md).

## <a name="next-lesson"></a>Nächste Lektion

Im nächsten Schritt erfahren Sie, wie R-Funktionen auf SQL Server-Daten angewendet werden.

[Verwenden von R-Funktionen mit SQL Server-Daten](../../advanced-analytics/tutorials/rtsql-using-r-functions-with-sql-server-data.md)
