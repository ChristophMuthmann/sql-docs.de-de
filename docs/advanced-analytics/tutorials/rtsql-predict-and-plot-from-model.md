---
title: Vorhersagen und Zeichnen von Modell (R in SQL-Schnellstart) | Microsoft Docs
ms.custom: 
ms.date: 08/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.assetid: 46babd8a-a331-44fc-bbd6-24daf58865e1
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: aa4bb7404e5469dd4331cca865fbd027ea631a8f
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="predict-and-plot-from-model-r-in-sql-quickstart"></a>Vorhersagen und Zeichnen von Modell (R in SQL-Schnellstart)

Zum Ausführen _Bewertung_ mit neuen Daten, eines der trainierten Modelle aus der Tabelle, und rufen Sie dann einen neuen Satz von Daten auf dem Vorhersagen basieren. Bewertung ist ein Begriff, die in Data Science manchmal verwendet werden, um das Generieren von Vorhersagen, Wahrscheinlichkeit oder andere Werte basierend auf neuen Daten, die bzw. der in einem trainierten Modell importiert haben.

## <a name="create-the-table-of-new-speeds"></a>Erstellen der Tabelle mit neuen Geschwindigkeiten

Haben Sie bemerkt, dass die ursprünglichen Trainingsdaten bei einer Geschwindigkeit von 25 Meilen pro Stunde enden? Das liegt daran, dass die ursprünglichen Daten auf einem Experiment von 1920 basierten!

Sie fragen sich vielleicht, wie lange ein Auto aus den 1920ern zum Anhalten brauchte, wenn wir davon ausgehen, dass es bis zu 60 oder sogar 100 Meilen pro Stunde schnell werden konnte? Um diese Frage zu beantworten, müssen Sie einige neue Geschwindigkeitswerte bereitstellen.

```sql
CREATE TABLE [dbo].[NewCarSpeed]([speed] [int] NOT NULL,
    [distance] [int]  NULL) ON [PRIMARY]
GO
INSERT [dbo].[NewCarSpeed] (speed)
VALUES (40),  (50),  (60), (70), (80), (90), (100)
```

## <a name="predict-stopping-distance"></a>Vorhersagen des Anhaltewegs

Mittlerweile enthält Ihre Tabelle möglicherweise mehrere R-Modelle, die alle verschiedene Parameter oder Algorithmen verwenden oder mit verschiedenen Teilmengen von Daten trainiert wurden.

![rsql_basictut_listofmodels](media/rsql-basictut-listofmodels.png)

Um vorhersagen auf Grundlage von einem bestimmten Modell erhalten möchten, müssen Sie ein SQL-Skript schreiben, die Folgendes ausführt:

1. Ruft das gewünschte Modell ab
2. Ruft die neuen Eingabedaten ab
3. Ruft eine R-Vorhersagefunktion auf, die mit dem Modell kompatibel ist

In diesem Beispiel, da das Modell basiert die **RxLinMod** Algorithmus, die als Teil der **"revoscaler"** Paket, rufen Sie die [RxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) -Funktion, statt über das generische R `predict` Funktion.

```sql
DECLARE @speedmodel varbinary(max) = (SELECT model FROM [dbo].[stopping_distance_models] WHERE model_name = 'latest model');
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(speedmodel));
            new <- data.frame(NewCarData);
            predicted.distance <- rxPredict(current_model, new);
            str(predicted.distance);
            OutputDataSet <- cbind(new, ceiling(predicted.distance));
            '
    , @input_data_1 = N' SELECT speed FROM [dbo].[NewCarSpeed] '
    , @input_data_1_name = N'NewCarData'
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ Verwenden Sie eine SELECT-Anweisung, um ein einzelnes Modell aus der Tabelle abzurufen, und übergeben Sie es als Eingabeparameter.
+  Rufen Sie nach dem Abruf des Modells aus der Tabelle die `unserialize`-Funktion auf dem Modell auf.

    > [!TIP] 
    > Außerdem sehen Sie sich die neue [Serialisierungsfunktionen](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) bereitgestellt, das Unterstützung von "revoscaler", [Echtzeit Bewertung](../../advanced-analytics/real-time-scoring.md).
+  Wenden Sie die `rxPredict`-Funktion mit geeigneten Argumenten auf das Modell an, und stellen Sie die neuen Eingabedaten bereit.
+  Im Beispiel die `str` Funktion hinzugefügt wird, während der Testphase, überprüfen Sie das Schema der Daten, die zurückgegeben wird, aus r ein. Entfernen Sie die Anweisung später erneut.
+ In der R-Skript verwendeten Spaltennamen sind nicht unbedingt an die Ausgabe der gespeicherten Prozedur übergeben. Hier haben wir die Ergebnisse von mit-Klausel verwendet, um einige neue Spaltennamen zu definieren.

**Ergebnisse**

![rsql_basictut_scoringresults_smalldata](media/rsql-basictut-scoringresults-smalldata.PNG)

## <a name="perform-scoring-in-parallel"></a>Paralleles Ausführen der Bewertung

Die Vorhersagen für dieses kleine Dataset wurden ziemlich schnell zurückgegeben. Aber was ist, wenn Sie sehr schnell sehr viele Vorhersagen benötigen? Es gibt viele Möglichkeiten, Vorgänge in SQL Server, wichtiger beschleunigt werden, wenn die Vorgänge parallel verarbeitet werden können. Bei der Bewertung ist eine einfache Möglichkeit, den *@parallel*-Parameter zu `sp_execute_external_script` hinzuzufügen und den Wert auf **1** festzulegen.

Nehmen wir an, dass Sie eine viel größere Tabelle möglicher Autogeschwindigkeiten mit Hunderten oder Tausenden von Werten erhalten haben. Es gibt viele T-SQL-Beispielskripts aus der Community, mit deren Hilfe Sie Zahlentabellen generieren können, weshalb wir diese hier nicht wiederholen. Gehen wir einfach davon aus, dass Sie eine Spalte mit vielen Ganzzahlen haben und Sie diese als Eingabe für `speed` im Modell verwenden möchten.

Zu diesem Zweck einfach führen Sie die gleichen Vorhersageabfrage jedoch das größere Dataset ersetzen, und fügen die `@parallel = 1` Argument.

```sql
DECLARE @speedmodel varbinary(max) = (select model from [dbo].[stopping_distance_models] where model_name = 'default model');
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(speedmodel));
            new <- data.frame(NewCarData);
            predicted.distance <- rxPredict(current_model, new);
            OutputDataSet <- cbind(new, ceiling(predicted.distance));
            '
    , @input_data_1 = N' SELECT [speed] FROM [dbo].[HugeTableofCarSpeeds] '
    , @input_data_1_name = N'NewCarData'
    , @parallel = 1
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ Parallele Ausführung bietet Vorteile im Allgemeinen, nur bei der Arbeit mit sehr großen Datenmengen. Das SQL-Datenbankmodul könnten, dass die parallele Ausführung nicht erforderlich ist. Darüber hinaus muss die SQL-Abfrage, die die Daten abruft, einen parallelen Abfrageplan generieren können.

+ Bei Verwendung der Option der parallelen Ausführung **müssen** Sie das Schema der Ausgabeergebnisse im Voraus mit der WITH RESULT SETS-Klausel angeben. Wenn Sie das Ausgabeschema im Voraus angeben, kann SQL Server die Ergebnisse von mehreren parallelen Datasets aggregieren, die andernfalls über unbekannte Schemas verfügen könnten.

+ Wenn Sie sind *Training* eines Modells anstelle von *Bewertung*, dieser Parameter wird nicht häufig Einfluss haben. Je nach Modelltyp kann es bei der Erstellung des Modells erforderlich sein, dass alle Zeilen gelesen werden, bevor Zusammenfassungen erstellt werden können.

+ Um die Vorteile der parallelen Verarbeitung, wenn Sie Ihr Modell trainieren zu erhalten, es wird empfohlen, die Verwendung eines der **"revoscaler"** Algorithmen. Diese Algorithmen dienen zum Verteilen der Verarbeitung automatisch, auch wenn Sie nicht angeben <code>@parallel =1</code> im Aufruf von `sp_execute_external_script`. Anleitungen zum Abrufen der optimale Leistung mit "revoscaler" Algorithmen finden Sie unter [verteilt und die parallele Berechnung mit ScaleR in Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).

## <a name="create-an-r-plot-of-the-model"></a>Erstellen eines R-Diagramms des Modells

Viele Clients einschließlich SQL Server Management Studio können mit [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) erstellte Diagramme nicht direkt anzeigen. Stattdessen werden der allgemeine Prozess zum Generieren von R-Plots des Diagramms als Teil der R-Code erstellen, und klicken Sie dann das Abbild in eine Datei schreiben.

Alternativ können Sie jedoch stattdessen das serialisierte binäre Darstellung für jede Anwendung zurückgeben, die Bilder anzeigen kann.

Im folgenden Beispiel wird veranschaulicht, wie eine einfache Grafik mit einer Zeichenfunktion erstellt wird, die standardmäßig in R enthalten ist. Das Bild wird an die angegebene Datei ausgegeben. Zudem wird es von der gespeicherten Prozedur in eine SQL-Variable ausgegeben.

```sql
 EXECUTE sp_execute_external_script
 @language = N'R'
 , @script = N'
     imageDir <- ''C:\\temp\\plots'';
     image_filename = tempfile(pattern = "plot_", tmpdir = imageDir, fileext = ".jpg")
     print(image_filename);
     jpeg(filename=image_filename,  width=600, height = 800);
     print(plot(distance~speed, data=InputDataSet, xlab="Speed", ylab="Stopping distance", main = "1920 Car Safety"));
     abline(lm(distance~speed, data = InputDataSet));
     dev.off();
     OutputDataSet <- data.frame(data=readBin(file(image_filename, "rb"), what=raw(), n=1e6));
     '
  , @input_data_1 = N'SELECT speed, distance from [dbo].[CarSpeed]'
  WITH RESULT SETS ((plot varbinary(max)));
```

+ Die `tempfile` Funktion gibt eine Zeichenfolge, die als Dateiname verwendet werden kann, aber die Datei noch nicht generiert wurde.
+ Für die Argumente für `tempfile`, können Sie ein Präfix und die Erweiterung als auch das Verzeichnis angeben. Um den vollständigen Namen und den Pfad zu überprüfen, Drucken eine Meldung mit `str()`.
+ Die `jpeg`-Funktion erstellt ein R-Gerät mit den angegebenen Parametern.
+ Nach der Erstellung des Diagramms können Sie weitere visual-Funktionen hinzufügen. In diesem Fall wird eine Regressionsgeraden mit hinzugefügt `abline`.
+ Wenn Sie die Grafikfunktionen hinzugefügt haben, müssen Sie das Grafikgerät mithilfe der `dev.off()`-Funktion schließen.
+ Die `readBin`-Funktion nimmt eine Datei zum Lesen, eine Formatangabe und die Anzahl der Datensätze auf. Die `rb`**'-Schlüsselwort Gibt an, dass die Datei statt Text binär ist.

**Ergebnisse**

![rsql_basictut_plotresult_small](media/rsql-basictut-plotresult-small.png)

Wenn Sie detailreichere Diagramme mit einigen der tollen Grafikpakete für R erstellen möchten, empfehlen wir Ihnen diese Artikel. Für beide ist das beliebte **ggplot2**-Paket erforderlich.

+ [Loan Classification using SQL Server 2016 R Services (Krediteinstufung mit SQL Server 2016 R Services)](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/): End-to-End-Szenario basierend auf Versicherungsdaten. Erfordert die **umformen** Paket.
+ [Erstellen von Diagrammen und mithilfe von R-Plots](../../advanced-analytics/tutorials/walkthrough-create-graphs-and-plots-using-r.md)

## <a name="conclusions"></a>Schlussfolgerungen

Die Integration von R mit SQL Server erleichtert das Bereitstellen skalierbarer R-Lösungen durch Nutzung der besten Funktionen von R und relationalen Datenbanken für Datenverarbeitung mit hoher Leistung und schnelle R-Analysen. 

Finden Sie unter folgenden zusätzlichen Ressourcen für weitere R-Beispiele:

+  [SQL Server-R-Lernprogramme](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    Weiterhin Kennenlernen der Lösungen, die mithilfe von R mit SQL Server, über die End-to-End-Szenarien, die durch die Microsoft Data Science und R Services Entwicklungsteams erstellt.

+ [SQL Server-Python-Lernprogramme](../../advanced-analytics/tutorials/sql-server-python-tutorials.md)

    Verwenden Sie für SQL Server 2017 die Leistungsfähigkeit des remote-computekontext und skalierbare Algorithmus mit der Python-Programmiersprache.

+ [Lernprogramme und Beispieldaten für Microsoft R](https://docs.microsoft.com/r-server/r/tutorial-introduction)

    Erfahren Sie, wie die neuen "revoscaler"-Pakete zum Erstellen von Modellen und Transformieren von Daten verwenden.

+ [Erste Schritte mit MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

    Weitere Informationen über die schnelle, skalierbare Algorithmen für maschinelles lernen von Microsoft Research.
