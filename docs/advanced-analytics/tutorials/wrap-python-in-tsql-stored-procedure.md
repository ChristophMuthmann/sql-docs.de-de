---
title: Python-Code in einer gespeicherten Prozedur umschließen | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b0c32ba91698345adea542ed5929a494b00059e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="wrap-python-code-in-a-stored-procedure"></a>Python-Code in einer gespeicherten Prozedur umschließen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In einem [vorherigen Lektion](run-python-using-t-sql.md), haben Sie gelernt, Python, sprechen Sie mit SQL Server vornehmen. In dieser Lektion erfahren Sie, wie zum Einbetten von Python-Code in einer gespeicherten Prozedur, um Daten aus den Python-Beispiel-Datasets abrufen und Schreiben Sie die Daten in eine SQL Server-Tabelle.

Die gespeicherte Systemprozedur [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) stellt den Wrapper, die SQL-Variablen und SQL-Datasets in Python übergibt. Außerdem behandelt die Ergebnisausgabe von Python und übergibt sie an SQL Server in einem Format mit SQL-Datentypen kompatibel.

Sehen wir, wie dies funktioniert.

## <a name="prepare-the-database-and-tables"></a>Bereiten Sie die Datenbank und die Tabellen vor.

Obwohl es möglich ist, einem Remoteclient einrichten und Ausführen von Python-Code mithilfe von Visual Studio-Code, Visual Studio, PyCharm oder andere Tools, um das Szenario zu vereinfachen, sollte der gesamte Code in dieser Lektion als Teil einer gespeicherten Prozedur ausgeführt werden.

1. Starten Sie SQL Server Management Studio, und öffnen Sie ein neues **Abfrage** Fenster.  

2. Erstellen Sie eine neue Datenbank für dieses Projekt aus, und ändern Sie im Rahmen Ihrer **Abfrage** Fenster, das die neue Datenbank verwendet.

    ```sql
    CREATE DATABASE sqlpy;
    GO;
    USE sqlpy;
    GO;
    ```

    > [!TIP] 
    > Wenn Sie noch nicht mit SQL Server oder auf einem Server, die Sie besitzen arbeiten, ist ein häufiger Fehler melden Sie sich, und starten die Arbeit ohne zu bemerken, die Sie in der **master** Datenbank. Immer um sicherzustellen, dass Sie die richtige Datenbank verwenden, geben Sie den Kontext mithilfe der `USE <database name>` Anweisung.

3. Einige leeren Tabellen hinzufügen: eine zum Speichern der Daten und einen für die Modelle zu speichern, Sie trainieren. Füllen Sie später auf die Tabellen mithilfe von Python.

    Der folgende Code erstellt die Tabelle für die Trainingsdaten.

    ```sql
    DROP TABLE IF EXISTS iris_data;
    GO
    CREATE TABLE iris_data (
      id INT NOT NULL IDENTITY PRIMARY KEY
      , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
      , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
      , "Species" VARCHAR(100) NOT NULL, "SpeciesId" INT NOT NULL
    );
    ```

    Wenn Sie mit T-SQL vertraut sind, lohnt sich merken sich den `DROP...IF` Anweisung. Wenn Sie versuchen, eine Tabelle zu erstellen und bereits eine vorhanden ist, gibt SQL Server einen Fehler zurück: "Es besteht bereits ein Objekt mit dem Namen"Iris_data"in der Datenbank." Eine Möglichkeit, um solche Fehler zu vermeiden, wird so löschen Sie vorhandenen Tabellen oder andere Objekte als Teil des Codes.

4. Führen Sie den folgenden Code zum Erstellen der Tabelle zum Speichern des trainierten Modells verwendet. Um Python (oder R) Modelle in SQL Server zu speichern, sie müssen serialisiert und gespeichert werden in einer Spalte vom Typ **varbinary(max)**. 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    Zusätzlich zum Standardinhalt Modell in der Regel, würden Sie auch Hinzufügen von Spalten für andere nützliche Metadaten, z. B. dem Modellnamen, das Datum, an das es trainiert wurde, das die Quelle Algorithmus und Parameter, Datenquellen, usw. Vorerst wir einfach halten und nur den Name des Modells verwenden.

## <a name="populate-the-table"></a>Füllen Sie die Tabelle

Zum Verschieben von Trainingsdaten aus Python in eine SQL Server ist die Tabelle aus mehreren Schritten:

+ Entwerfen Sie eine gespeicherte Prozedur, die die Daten abruft, die Sie möchten.
+ Sie führen die gespeicherte Prozedur, um die Daten zu erhalten.
+ Sie verwenden eine INSERT-Anweisung, um anzugeben, wo die abgerufenen Daten gespeichert werden soll.

1. Erstellen Sie die folgende gespeicherte Prozedur, die Python-Code enthält. 

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    from sklearn import datasets
    iris = datasets.load_iris()
    iris_data = pandas.DataFrame(iris.data)
    iris_data["Species"] = pandas.Categorical.from_codes(iris.target, iris.target_names)
    iris_data["SpeciesId"] = iris.target
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

    Wenn Sie diesen Code ausführen, sollten Sie die Nachricht abrufen "Befehle wurde erfolgreich abgeschlossen." Dies bedeutet lediglich, dass die gespeicherte Prozedur gemäß Ihren Spezifikationen erstellt wurde.

2. Tatsächlich füllen Sie die Tabelle, führen Sie die gespeicherte Prozedur, und geben Sie die Tabelle, in dem die Daten geschrieben werden soll. Bei der Ausführung führt die gespeicherte Prozedur den Python-Code, der aus den integrierten Python-Beispieldaten Iris-Dataset geladen.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Wenn Sie noch nicht in T-SQL vertraut sind, Bedenken Sie, dass die INSERT-Anweisung nur neue Daten hinzugefügt; Es wird nicht für vorhandene Daten überprüfen oder löschen und Neuerstellen die Tabelle. Um zu vermeiden, mehrere Kopien derselben Daten in einer Tabelle abrufen, können Sie zuerst diese Anweisung ausführen: `TRUNCATE TABLE iris_data`. Die T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) Anweisung löscht die vorhandene Daten, behält jedoch die Struktur der Tabelle intakt.

    > [!TIP]
    > Um die gespeicherte Prozedur ändern später verwenden, müssen Sie löschen und erneut erstellen. Verwenden der [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) Anweisung. 

3. Um sicherzustellen, dass die Daten ordnungsgemäß geladen wurde, können Sie einige einfache Abfragen ausführen:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

In der [nächsten Lektion](../tutorials/train-score-using-python-in-tsql.md), Machine Learning-Modells erstellen und speichern Sie es in einer Tabelle.

### <a name="further-reading-about-stored-procedures"></a>Weitere Informationen zu gespeicherten Prozeduren

Wenn Sie SQL Server vertraut sind, finden Sie möglicherweise gespeicherte Prozeduren, die auf den ersten kompliziert sein muss. Jedoch eine gespeicherte Prozedur ist ein leistungsstarkes und flexibles Schnittstelle für die Übergabe von Daten zwischen Anwendungen und dem Server. Mithilfe einer gespeicherten Prozedur können Sie dynamisch Eingaben definieren, die übergeben in neuen Modellnamen, neue Parameter und neue Daten vereinfacht, ohne den Python-Code zu ändern.

Eine Übersicht dazu, wie gespeicherte Prozeduren arbeiten, finden Sie unter [gespeicherte Prozeduren (Datenbankmodul)](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine), oder dieses Lernprogramms: [Schreiben von Transact-SQL-Anweisungen](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements).

Es gibt auch einige gute Lernprogramme auf Community-Sites wie [SQL Server Central](http://www.sqlservercentral.com/) oder [SQL-Team](http://www.sqlteam.com/).

Ihrer Meinung nach zu, wie Sie am besten Python-Code in T-SQL kapseln können, berücksichtigen Sie auch, mit den folgenden Funktionen:

+ Definieren von Standardwerten für die gespeicherte Prozedur
+ Verwenden das Schlüsselwort OUTPUT Eingabevariablen passieren
+ Erstellen von Schemadefinitionen mit mit Ergebnisse sicherzustellen, dass Daten von Anwendungen genutzt hat, den richtigen Datentypen und Spaltennamen
+ Bereitstellen von Hinweisen zur Verbesserung der Batchverarbeitung
+ Identität eines anderen Benutzers zum Testen von Code mithilfe der EXECUTE AS-Klausel

## <a name="next-lesson"></a>Nächste Lektion

[Ein Python-Modell trainieren und Generieren von Bewertungen in SQL Server](../tutorials/train-score-using-python-in-tsql.md)