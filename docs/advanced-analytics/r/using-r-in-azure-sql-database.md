---
title: Verwendung von R in Azure SQL-Datenbank | Microsoft Docs
ms.custom: 
ms.date: 12/08/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: e6376a5b03a272633e876b993c3a67467d7b4637
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="using-r-in-azure-sql-database"></a>Verwendung von R in Azure SQL-Datenbank

Im Oktober 2017 kündigte das SQL Server-Entwicklungsteam Pläne zur Ausführung von R-Code in der Datenbank mithilfe von gespeicherten Prozeduren, ähnlich wie R Services in SQL Server 2016 zu unterstützen. 

Um für die öffentliche releasezeitplan und bevorstehender Ereignisse, aktuell zu halten, finden Sie unter der [SQL Server-Blog](https://blogs.technet.microsoft.com/dataplatforminsider/) oder [Microsoft R Server-Blog](https://blogs.msdn.microsoft.com/rserver/).

> [!IMPORTANT]
> Zurzeit die Vorschau des R-Unterstützung ist nur verfügbar in Azure SQL-Datenbank in West Mitte-NORD und Funktionen sind im Vergleich zu den Funktionen für R eingeschränkt und Python-code die Ausführung in SQL Server 2016 oder 2017.

## <a name="whats-included"></a>Inhalt

Die R-Funktionen in der Datenbank kann für die folgenden Datenbank-Dienstebenen und Leistungsstufen verwendet werden:
 
- Premium-Dienstebene – P1, P2, P4, P6, P11, P15
- Premium-Dienst von RS-Ebene – PRS1, PRS2 PRS4, PRS6
- Premium elastischen Pool – 125 eDTUs oder höher
- Premium RS elastischen Pool – 125 eDTUs oder höher

Die Preview-Version umfasst diese Pakete an:

+   Microsoft R Open mit R Version 3.3.3
+   Base R-Pakete und Funktionen werden vorinstallierte
+   Microsoft R Server 9.2, einschließlich der "revoscaler"-Paket

In der aktuellen Preview-Version können Sie die folgenden Aufgaben ausführen:

+ Trainieren Modelle mit Daten, die in den Arbeitsspeicher passt
+   Bewerten von Modellen mit Daten, die in den Arbeitsspeicher passt
+   Trivial Parallelität für die Ausführung von R-Skript (mithilfe der @parallel Parameter in Sp_execute_external_script)
+   Streaming-Ausführung für die Ausführung von R-Skript (mit @r_RowsPerRead Parameter in Sp_execute_external_script)
+   Führen Sie ein R-Skript auf einmal


Die folgenden Aufgaben werden in der Preview-Version von R in Azure SQL-Datenbank nicht unterstützt:

+ Ausführen von R-Skripts auf bestimmte Datenbanken ist nicht möglich.
+ DMVs überwachen CPU bereitgestellt und speicherauslastung von R-Skripts sind nicht verfügbar.
+ Es können keine Pakete von Drittanbietern installiert werden. Erstellen eines EXTERNEN LIBRARY-Anweisung wird nicht unterstützt.

## <a name="example"></a>Beispiel

In Azure SQL-Datenbank, alle R-Befehle werden ausgeführt von T-SQL, mit der gespeicherten Prozedur [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). 

Im folgenden Beispiel wird veranschaulicht, wie die Vorschaufunktion, verwenden das Iris-DataSet enthaltene Basis r ausprobieren

### <a name="step-1-create-the-data-tables"></a>Schritt 1: Erstellen von Datentabellen

Starten, indem Sie zwei Tabellen erstellen: eine für die Quelldaten aus R extrahiert speichern und einen zum Speichern von das trainierte Modell.

```sql
DROP TABLE IF EXISTS iris_data, iris_models;
GO
CREATE TABLE iris_data (
        id INT NOT NULL IDENTITY PRIMARY KEY
        , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
        , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
        , "Species" VARCHAR(100) NULL
);
CREATE TABLE iris_models (
    model_name VARCHAR(30) NOT NULL PRIMARY KEY,
    model VARBINARY(max) NOT NULL,
    native_model VARBINARY(MAX) NOT NULL
);
GO
```

### <a name="step-2-populate-table-with-data-from-the-iris-dataset"></a>Schritt 2: Füllen Sie Tabelle mit Daten aus dem Iris-dataset

Nachdem die Tabellen erstellt wurden, führen Sie den folgenden Code zum Einfügen von Trainingsdaten in der Tabelle. Die gespeicherte Prozedur Sp_execute_external_script R aufgerufen und gibt Iris-Dataset als einem Datenrahmen mit dem Schema in der INSERT INTO-Anweisung angegeben.

```sql
INSERT INTO iris_data
("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
EXEC sp_execute_external_script @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

### <a name="step-3-create-the-stored-procedure-that-generates-the-model"></a>Schritt 3: Erstellen Sie die gespeicherte Prozedur, die das Modell generiert.

Die folgende gespeicherte Prozedur funktioniert die tatsächlich erstellen und Trainieren des Modells, das in einem der beiden binäre Formate gespeichert werden kann.

```sql
CREATE PROCEDURE generate_iris_model
    @trained_model VARBINARY(MAX) OUTPUT, 
    @native_trained_model VARBINARY(MAX) OUTPUT
AS
BEGIN
  EXEC sp_execute_external_script @language = N'R'
  , @script = N'
    iris_model <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris_rx_data);
    trained_model <- as.raw(serialize(iris_model, connection=NULL));
    native_trained_model <- rxSerializeModel(iris_model, realtimeScoringOnly = TRUE)
    '
  , @input_data_1 = N'SELECT "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@trained_model VARBINARY(MAX) OUTPUT, @native_trained_model VARBINARY(MAX) OUTPUT
    , @trained_model = @trained_model OUTPUT
    , @native_trained_model = @native_trained_model OUTPUT;
End
```

+ Die **Ausgabe** -Schlüsselwort für die Eingabeparameter gibt an, dass die Werte übergeben und für die Ausgabe ebenfalls verwendet werden soll.
+ Der Anfang der Zeile mit `iris_model` Decision Tree-Modell zum Vorhersagen auf Grundlage von Attributen Blume Arten definiert.
+ Der Aufruf von `serialize` speichert das Modell in einem binären Format, für die Speicherung in SQL Server geeignet. 
+ Alternativ können Sie mit Modelle auf Grundlage von "revoscaler"-Algorithmen, können Sie mithilfe der [RxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) -Funktion, die das Modell in einem neuen systemeigenen binären Format gespeichert. In diesem Format gespeicherte Modelle können zum Bewerten von mit der PREDICT-Funktion in SQL Server geladen werden.

### <a name="step-4-train-and-save-the-model"></a>Schritt 4. Trainieren Sie und speichern Sie das Modell

Rufen Sie die Eingabedaten zu verarbeiten, und erstellen Sie ein Modell mit dem Erstellen der gespeicherten Prozedur. Der folgende Code speichert das Modell auch auf die Tabelle **Iris_models**, sodass Sie sie später verwenden können, die Arten von Blume vorherzusagen.

```sql
DECLARE @model VARBINARY(MAX), @native_modelVARBINARY(MAX);
EXEC generate_iris_model @model OUTPUT, @native_model OUTPUT;
DELETE FROM iris_models WHERE model_name = 'iris.dtree';
INSERT INTO iris_models (model_name, model, native_model) VALUES('iris.dtree', @model, @native_model);
SELECT model_name, datalength(model)/1024. AS model_size_kb, datalength(native_model)/1024. AS native_model_size_kb FROM iris_models;
GO
```

### <a name="step-5-create-a-stored-procedure-for-scoring"></a>Schritt 5. Erstellen einer gespeicherten Prozedur für die Bewertung

Als Nächstes erstellen Sie eine gespeicherte Prozedur für die Bewertung. Diese gespeicherte Prozedur lädt ein angegebenes Modell aus der Tabelle und erstellt basierend auf Eingabedaten Ergebnisse.

```sql
CREATE PROCEDURE predict_iris_species (@model varchar(100))
AS
BEGIN
  DECLARE @rx_model VARBINARY(MAX) = (SELECT model FROM iris_models WHERE model_name = @model);
  EXEC sp_execute_external_script @language = N'R'
  , @script = N'
    irismodel<-unserialize(rx_model);
    OutputDataSet <-rxPredict(irismodel, iris_rx_data, extraVarsToWrite = c("Species", "id"));
      '
  , @input_data_1 = N'SELECT "id", "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@rx_model varbinary(max)'
  , @rx_model = @rx_model
  WITH RESULT SETS ( ("setosa_Pred" FLOAT, "versicolor_Pred" FLOAT, "virginica_Pred" FLOAT, "Species.Actual" VARCHAR(100), "id" INT));
END;
GO
```

Diese gespeicherte Prozedur verwendet die [RxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) -Funktion, aber Sie können auch verwenden systemeigene PREDICT-Funktion in T-SQL wie gezeigt [hier](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-general-availability-of-native-scoring-using-predict-function-in-azure-sql-database/). Verwendung der PREDICT-Funktion erfordert die Verwendung einer [ **Rx** Modell](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler) und speichern Sie das Modell mit [RxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel).

### <a name="step-6-use-the-stored-procedure-to-generate-predictions"></a>Schritt 6. Verwenden Sie die gespeicherte Prozedur, um vorhersagen zu generieren.

Führen Sie die gespeicherte Prozedur, um das Generieren von Bewertungen aus dem Modell. Sie können entweder die Werte in einer Tabelle einfügen oder die Vorhersagen an eine aufrufende Anwendung zurückgegeben.

```sql
EXEC predict_iris_species 'iris.dtree';
GO
```

## <a name="related-resources"></a>Verwandte Ressourcen

Azure Marketplace gibt es auch mehrere virtuelle Computer, der SQL Server-2017 enthalten:

+ [Bereitstellen eines virtuellen Computers für Machine Learning in Azure](provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

Außerdem sehen Sie sich diesen virtuellen Computern, die mit einer Vielzahl von gängigen Machine learning-Tools vorkonfigurierten stammen:

+ [Data Science Virtual Machines](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)
+ [Die virtuelle Maschine umfassenden lernen](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)

