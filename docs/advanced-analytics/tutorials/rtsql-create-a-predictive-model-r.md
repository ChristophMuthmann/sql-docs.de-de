---
title: Erstellen ein Vorhersagemodells (R in SQL-Schnellstart) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
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
ms.assetid: 6eb78a80-5791-438f-9ca6-d142ab5d9bb1
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c6f0117198cd7a548b9e56d228c14231b39ec35a
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="create-a-predictive-model-r-in-sql-quickstart"></a>Erstellen eines Vorhersagemodells (R in SQL-Schnellstart)

In diesem Schritt erfahren Sie, wie Sie ein Modell mithilfe von R trainieren und das Modell später in einer Tabelle in SQL Server speichern. Beim Modell handelt es sich um ein einfaches Regressionsmodell, das den Bremsweg eines Autos basierend auf dessen Geschwindigkeit vorhersagt. Verwenden Sie die `cars` Dataset mit R, eingeschlossen werden, da sie klein und einfach zu verstehen ist.

## <a name="create-the-source-data"></a>Erstellen der Quelldaten

Erstellen Sie zuerst eine Tabelle zum Speichern der Trainingsdaten.

```sql
CREATE TABLE CarSpeed ([speed] int not null, [distance] int not null)
INSERT INTO CarSpeed
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'car_speed <- cars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'car_speed'
```

+ Einige Benutzer möchten gern temporäre Tabellen verwenden, aber beachten Sie, dass einige Clients R Sitzungen zwischen Batches getrennt werden.

+ Viele kleine und große Datasets sind in der R-Laufzeit enthalten. Geben Sie aus einer R-Eingabeaufforderung heraus `library(help="datasets")` ein, um eine Liste der mit R installierten Datasets anzuzeigen.

## <a name="create-a-regression-model"></a>Erstellen eines Regressionsmodells

Die Daten der Autogeschwindigkeit enthalten zwei numerische Spalten, `dist` und `speed`. Es gibt mehrere Beobachtungen einiger Geschwindigkeiten. Aus diesen Daten erstellen Sie ein lineares Regressionsmodell, das den Zusammenhang zwischen der Geschwindigkeit eines Autos und der benötigen Entfernung zum Anhalten beschreibt.

Die Anforderungen eines linearen Modells sind einfach:

+ Definieren Sie eine Formel, die die Beziehung zwischen der abhängigen Variable `speed` und der unabhängigen Variable `distance` beschreibt.

+ Bereitstellen von Eingabedaten zur Verwendung während des Trainings des Modells

> [!TIP]
> Wenn Sie auf der linearen Modellen aufzufrischen benötigen, sollten Sie dieses Lernprogramm, das beschreibt den Prozess der Anpassen eines Modells mit RxLinMod: [Linear Models anpassen](https://docs.microsoft.com/r-server/r/how-to-revoscaler-linear-model)

Sie müssen zum tatsächlichen Erstellen des Modells die Formel in Ihrem R-Code definieren und die Daten als Eingabeparameter weitergeben.

```sql
DROP PROCEDURE IF EXISTS generate_linear_model;
GO
CREATE PROCEDURE generate_linear_model
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'lrmodel <- rxLinMod(formula = distance ~ speed, data = CarsData);
        trained_model <- data.frame(payload = as.raw(serialize(lrmodel, connection=NULL)));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model varbinary(max)));
END;
GO
```

+ Das erste Argument für rxLinMod ist der *formula*-Parameter, der die Distanz abhängig von der Geschwindigkeit definiert.
+ Die Eingabedaten werden in der Variable `CarsData` gespeichert, die durch die SQL-Abfrage aufgefüllt wird. Wenn Sie Ihren Eingabedaten keinen spezifischen Namen zuweisen, ist der Standardvariablenname _InputDataSet_.

## <a name="create-a-table-for-storing-the-model"></a>Erstellen einer Tabelle zum Speichern des Modells

Als Nächstes speichern Sie das Modell, damit Sie erneut trainieren können oder für Vorhersagen verwenden können. Die Ausgabe eines R-Pakets, das ein Modell erstellt, ist normalerweise ein **binäres Objekt**. Daher muss die Tabelle, in der Sie das Modell erstellen, eine Spalte vom Typ **varbinary** bereitstellen.

```sql
CREATE TABLE stopping_distance_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null);
```

## <a name="save-the-model"></a>Speichern des Modells

Führen Sie zum Speichern des Modells die folgende Transact-SQL-Anweisung aus, um die gespeicherte Prozedur aufzurufen, das Modell zu generieren und es in einer Tabelle zu speichern.

```sql
INSERT INTO stopping_distance_models (model)
EXEC generate_linear_model;
```

Beachten Sie, dass wenn Sie diesen Code ein zweites Mal ausführen, Sie diesen Fehler erhalten:

```
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

Eine Möglichkeit zur Vermeidung dieses Fehlers besteht darin, den Namen für jedes neue Modell zu aktualisieren. Sie können den Namen z.B. in einen aussagekräftigeren Namen ändern und den Modelltyp, den Erstellungstag usw. mit aufnehmen.

```sql
UPDATE stopping_distance_models
SET model_name = 'rxLinMod ' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="output-additional-variables"></a>Ausgabe zusätzlicher Variablen

Generell ist die Ausgabe von R aus der gespeicherten Prozedur [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) auf einen einzelnen Datenrahmen beschränkt. (Diese Einschränkung wird möglicherweise in Zukunft entfernt.)

Sie können allerdings zusätzlich zum Datenrahmen Ausgaben für andere Typen, z.B. Skalare, zurückgeben.

Angenommen, Sie möchten ein Modell trainieren, aber sofort eine Tabelle von Koeffizienten des Models anzeigen. Sie können die Tabelle der Koeffizienten als Hauptresultset erstellen, und das trainierte Modell in einer SQL-Variable ausgeben. Sofort erneut können Sie das Modell durch Aufrufen der Variablen, oder Sie können das Modell in einer Tabelle speichern, wie hier gezeigt.

```sql
DECLARE @model varbinary(max), @modelname varchar(30)
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
        speedmodel <- rxLinMod(distance ~ speed, CarsData)
        modelbin <- serialize(speedmodel, NULL)
        OutputDataSet <- data.frame(coefficients(speedmodel));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @params = N'@modelbin varbinary(max) OUTPUT'
    , @modelbin = @model OUTPUT
    WITH RESULT SETS (([Coefficient] float not null));

-- Save the generated model
INSERT INTO [dbo].[stopping_distance_models] (model_name, model)
VALUES (' latest model', @model)
```

**Ergebnisse**

![rslq_basictut_coefficients](media/rslq-basictut-coefficients.PNG)

### <a name="summary"></a>Zusammenfassung

Beachten Sie diese Regeln für die Arbeit mit SQL-Parametern und Variablen von R in `sp_execute_external_script`:

+ Alle R-Skript zugeordnete SQL-Parameter müssen aufgelistet sein, namentlich in der  _@params_  Argument.
+ Fügen Sie zur Ausgabe eines dieser Parameter das OUTPUT-Schlüsselwort in die Liste _@params_ ein.
+ Stellen Sie nach Auflistung der zugeordneten Parameter die Zuordnung bereit: zeilenweise, von SQL-Parametern zu R-Variablen und sofort nach der Liste _@params_.

## <a name="next-lesson"></a>Nächste Lektion

Da Sie nun über ein Modell verfügen, lernen Sie im letzten Schritt, wie man darauf basierende Vorhersagen trifft und die Ergebnisse darstellt.

[Vorhersagen und Zeichnen ausgehend vom Modell](../tutorials/rtsql-predict-and-plot-from-model.md)


