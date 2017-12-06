---
title: Erstellen mehrere Modelle mit RxExecBy | Microsoft Docs
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: abde4e0ab342f126b73321b66e93fa7b31433222
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="creating-multiple-models-using-rxexecby"></a>Erstellen mehrere Modelle mit rxExecBy

SQL Server 2017 CTP 2.0 umfasst eine neue Funktion **RxExecBy**, die parallele Verarbeitung mehrerer verwandter Modelle unterstützt. Anstatt Train eine sehr umfangreiches Modell auf der Grundlage von Daten aus mehreren ähnlich wie Entitäten, der Data Scientist kann sehr schnell erstellen viele Verwandte Modelle, von denen jeder Daten, die spezifisch für eine einzelne Entität.

Angenommen Sie, Sie sind Geräteausfällen überwachen und Sammeln von Daten für viele verschiedene Arten von Geräten. Mithilfe von RxExecBy können Sie ein einzelnes großen Dataset als Eingabe bereitstellen, geben Sie eine Spalte zum Dataset, z. B. Gerätetyp stratify und erstellen Sie mehrere Modelle Modelle für die einzelnen Geräte.

Dieser Prozess hat nennt man auch wurde "pleasingly" parallelverarbeitung, da eine Aufgabe ausgeführt wird, die etwas sehr aufwändig, für die Datenanalysten oder bestenfalls mühsam war und einen schnellen, einfachen Vorgang vereinfacht.

In vielen Anwendungen dieses Ansatzes sind für einzelne Haushalt intelligenten Meter zu prognostizieren, basierenden Projektionen bewährt für separate Produktlinien erstellen oder Erstellen von Modellen für Loan Genehmigungen, die für die einzelnen Bank Verzweigungen zugeschnitten sind.

## <a name="how-rxexec-works"></a>Funktionsweise von rxExec

Die RxExecBy-Funktion in "revoscaler" für hohes Volumen parallele Verarbeitung über eine große Anzahl von kleinen Datasets dient.

1. Sie rufen Sie die RxExecBy-Funktion als Teil der R-Code, und übergeben ein Dataset mit nicht sortierte Daten.
2. Geben Sie die Partition mit der die Daten gruppiert und sortiert werden soll.
3. Definieren einer Transformation oder Modellierung von Funktion, die auf jede Datenpartition angewendet werden soll
4. Wenn die Funktion ausgeführt wird, werden die Datenabfragen parallel verarbeitet, wenn Ihre Umgebung unterstützt. Darüber hinaus sind die Aufgaben Modellierung oder Transformation auf Kerne verteilt und parallel ausgeführt. Unterstützte computekontext für drei Vorgänge umfassen RxSpark und RxInSQLServer.
5. Es sind mehrere Ergebnisse zurückgegeben.

## <a name="rxexecby-syntax-and-examples"></a>RxExecBy Syntax und Beispiele

**RxExecBy** nimmt vier eingegeben werden, eine der Eingaben wird eine Datasets oder eines Quellobjekts, das partitioniert werden kann für ein bestimmtes **Schlüssel** Spalte. Die Funktion gibt eine Ausgabe für jede Partition an. Das Format der Ausgabe hängt von der Funktion, die als Argument übergeben wird, z. B. Wenn Sie eine Modellierung-Funktion, z. B. RxLinMod übergeben, Sie zurückgeben eines separaten trainierten Modells für jede Partition des Datasets.

### <a name="supported-functions"></a>Unterstützte Funktionen

Modeling: `rxLinMod`, `rxLogit`, `rxGlm`,`rxDtree`

Bewertung: `rxPredict`,

Transformation oder Analyse:`rxCovCor`

## <a name="example"></a>Beispiel

Das folgende Beispiel veranschaulicht das Erstellen mehrerer Modelle, die mit dem Dataset Airline-Aktivität, die für die Spalte [DayOfWeek] partitioniert ist. Die benutzerdefinierte Funktion `delayFunc`, auf die einzelnen Partitionen aufrufenden RxExecBy angewendet wird. Die Funktion erstellt separate Modelle für jeden zweiten Montag, Dienstag, und so weiter.

```SQL
EXEC sp_execute_external_script
@language = N'R'
, @script = N'
delayFunc <- function(key, data, params) { 
    df <- rxImport(inData = airlineData) 
    rxLinMod(ArrDelay ~ CRSDepTime, data = df) 
} 
OutputDataSet <- rxExecBy(airlineData, c("DayOfWeek"), delayFunc)
'
, @input_data_1 = N'select ArrDelay, DayOfWeek, CRSDepTime from AirlineDemoSmall]'
, @input_data_1_name = N'airlineData'

```

Wenn Sie die Fehlermeldung erhalten, `varsToPartition is invalid`, überprüfen Sie, ob der Name der Schlüsselspalte oder Spalten richtig geschrieben ist. Die Sprache "R" wird die Groß-/Kleinschreibung beachtet.

Beachten Sie, die in diesem Beispiel wird für SQL Server nicht optimiert, und in vielen Fällen können Sie erzielen eine bessere Leistung zum Gruppieren der Daten mithilfe von SQL. Allerdings können mit RxExecBy, parallele Aufträge aus r ein. erstellen

Das folgende Beispiel veranschaulicht den Prozess in R, SQL Server als computekontext verwenden:

```R
sqlServerConnString <- "SERVER=hostname;DATABASE=TestDB;UID=DBUser;PWD=Password;"
inTable <- paste("airlinedemosmall")
sqlServerDataDS <- RxSqlServerData(table = inTable, connectionString = sqlServerConnString)

# user function
".Count" <- function(keys, data, params)
{
  myDF <- rxImport(inData = data)
  return (nrow(myDF))
}

# Set SQL Server compute context with level of parallelism = 2
sqlServerCC <- RxInSqlServer(connectionString = sqlServerConnString, numTasks = 4)
rxSetComputeContext(sqlServerCC)

# Execute rxExecBy in SQL Server compute context
sqlServerCCResults <- rxExecBy(inData = sqlServerDataDS, keys = c("DayOfWeek"), func = .Count)
```


