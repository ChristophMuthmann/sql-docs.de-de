---
title: "Ausführen von Python mit T-SQL | Microsoft Docs"
ms.custom: 
ms.date: 09/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: Python
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 2812e9529a9cdb4dc5fd8019a28ccc060ba68d1a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="run-python-using-t-sql"></a>Ausführen von Python mit T-SQL

In diesem Beispiel wird gezeigt, wie Sie ein einfaches Python-Skript in SQL Server ausführen können, indem Sie mit der gespeicherten Prozedur [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

## <a name="step-1-create-the-test-data-table"></a>Schritt 1: Die Test-Datentabelle erstellen

Zunächst erstellen Sie einige zusätzlichen Daten zu verwenden, wenn die Namen der Tage der Woche eine Zuordnung zu den Quelldaten. Führen Sie die folgenden T-SQL-Anweisung aus, um die Tabelle zu erstellen.

```SQL
CREATE TABLE PythonTest (
    [DayOfWeek] varchar(10) NOT NULL,
    [Amount] float NOT NULL
    )
GO

INSERT INTO PythonTest VALUES
('Sunday', 10.0),
('Monday', 11.1),
('Tuesday', 12.2),
('Wednesday', 13.3),
('Thursday', 14.4),
('Friday', 15.5),
('Saturday', 16.6),
('Friday', 17.7),
('Monday', 18.8),
('Sunday', 19.9)
GO
```

## <a name="step-2-run-the-hello-world-script"></a>Schritt 2: Führen Sie das Skript "Hello World"

Der folgende Code die Python-ausführbare Datei lädt, übergibt die Eingabedaten und für jede Zeile von Eingabedaten, aktualisiert die Tagesnamen in der Tabelle mit einer Zahl, die den Tag der Woche Index darstellt.

Beachten Sie den Parameter  *@RowsPerRead* . Dieser Parameter gibt die Anzahl der Zeilen, die von SQL Server für die Python-Laufzeit übergeben werden.

Der Python-Daten-Analysebibliothek genannt **Pandas**ist erforderlich für die Übergabe von Daten mit SQL Server und ist standardmäßig mit Machine Learning-Diensten enthalten.

```sql
DECLARE @ParamINT INT = 1234567
DECLARE @ParamCharN VARCHAR(6) = 'INPUT '

print '------------------------------------------------------------------------'
print 'Output parameters (before):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)

print 'Dataset (before):'
SELECT * FROM PythonTest

print '------------------------------------------------------------------------'
print 'Dataset (after):'
DECLARE @RowsPerRead INT = 5

execute sp_execute_external_script 
@language = N'Python',
@script = N'
import sys
import os
print("*******************************")
print(sys.version)
print("Hello World")
print(os.getcwd())
print("*******************************")
if ParamINT == 1234567:
       ParamINT = 1
else:
       ParamINT += 1

ParamCharN="OUTPUT"
OutputDataSet = InputDataSet

global daysMap

daysMap = {
       "Monday" : 1,
       "Tuesday" : 2,
       "Wednesday" : 3,
       "Thursday" : 4,
       "Friday" : 5,
       "Saturday" : 6,
       "Sunday" : 7
       }

OutputDataSet["DayOfWeek"] = pandas.Series([daysMap[i] for i in OutputDataSet["DayOfWeek"]], index = OutputDataSet.index, dtype = "int32")
', 
@input_data_1 = N'SELECT * FROM PythonTest', 
@params = N'@r_rowsPerRead INT, @ParamINT INT OUTPUT, @ParamCharN CHAR(6) OUTPUT',
@r_rowsPerRead = @RowsPerRead,
@paramINT = @ParamINT OUTPUT,
@paramCharN = @ParamCharN OUTPUT
with result sets (("DayOfWeek" int null, "Amount" float null))

print 'Output parameters (after):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)
GO
```

> [!TIP]
> Die Parameter für diese gespeicherte Prozedur werden in diesem Schnellstart ausführlicher beschrieben: [mithilfe von R-Code in T-SQL-](rtsql-using-r-code-in-transact-sql-quickstart.md).

## <a name="step-3-view-the-results"></a>Schritt 3: Anzeigen der Ergebnisse

Die gespeicherte Prozedur ruft die ursprünglichen Daten, wendet das Python-Skript und gibt dann die geänderten Daten in der **Ergebnisse** Bereich von Management Studio oder anderen SQL-Abfragetool.


|DayOfWeek (vorher)| Amount|DayOfWeek (nachher) |
|-----|-----|-----|
|Sonntag|10|7|
|Montag|11.1|1|
|Dienstag|12.2|2|
|Mittwoch|13.3|3|
|Donnerstag|14.4|4|
|Freitag|15.5|5|
|Samstag|16.6|6|
|Freitag|17.7|5|
|Montag|18.8|1|
|Sonntag|19.9|7|

Statusmeldungen oder Fehler zurückgegeben, an die Python-Konsole werden zurückgegeben, als Nachrichten in der **Abfrage** Fenster. Hier ist ein Auszug aus der Ausgabe, die möglicherweise angezeigt:

*Beispielergebnisse*

```
Output parameters (before):
ParamINT=1234567
ParamCharN=INPUT 
Dataset (before):

(10 rows affected)

Dataset (after):
STDOUT message(s) from external script: 
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

(10 rows affected)
Output parameters (after):
ParamINT=2
ParamCharN=OUTPUT
```

+ Die **Nachricht** Ausgabe enthält das Arbeitsverzeichnis für die Ausführung des Skripts verwendet. In diesem Beispiel bezieht sich auf das workerkonto, der von SQL Server zum Verwalten des Auftrags "MSSQLSERVER01". 

    Die GUID ist der Name eines temporären Ordners, die während der skriptausführung zum Speichern von Daten und Skript-Artefakten erstellt wird. Diese temporären Ordner durch SQL Server gesichert werden, und werden von der Windows-Auftragsobjekt nach bereinigt Skript beendet wurde.

+ Im Abschnitt mit der Meldung "Hello World" Druckt zweimal. Dies liegt daran, dass der Wert der  *@RowsPerRead*  auf 5 festgelegt wurde und in der Tabelle 10 Zeilen vorhanden sind; daher sind die beiden Aufrufe von Python zum Verarbeiten aller Zeilen in der Tabelle erforderlich.

    In der produktionsumgebung ausgeführt wird wird empfohlen, dass Sie experimentieren mit unterschiedlichen Werten um die maximale Anzahl von Zeilen zu bestimmen, die in jedem Batch übergeben werden sollen. Die optimale Anzahl von Zeilen ist datenabhängig und sowohl die Anzahl der Spalten im Dataset und den Typ der Daten, die Sie weitergeben betroffen ist.

## <a name="resources"></a>Ressourcen

Diese zusätzliche Python-Beispiele und Lernprogramme für erweiterte Tipps und End-to-End-Demos angezeigt.

+ [Verwenden von Python-Revoscalepy zum Erstellen eines Modells](use-python-revoscalepy-to-create-model.md)
+ [In der Datenbank Python für SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md)
+ [Erstellen eines Vorhersagemodells über Python- und SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

## <a name="troubleshooting"></a>Problembehandlung

Wenn Sie die gespeicherte Prozedur nicht finden können `sp_execute_external_script`, bedeutet dies wahrscheinlich noch nicht abgeschlossen konfigurieren die Instanz, um das Ausführen des externen Skripts unterstützen. Nach dem 2017 von SQL Server-Setup ausführen und Python als Machine learning Sprache auswählen, müssen Sie auch ausdrücklich aktivieren die Funktion mit `sp_configure`, und klicken Sie dann die Instanz neu gestartet. Weitere Informationen finden Sie unter [Setup Machine Learning-Dienste mit Python](../python/setup-python-machine-learning-services.md).