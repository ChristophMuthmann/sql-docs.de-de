---
title: Verwendung Python-Modell in SQL zum Trainieren und Bewerten von | Microsoft Docs
titleSuffix: SQL Server
ms.custom: 
ms.date: 02/28/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 20ba339a29a62fbcffde31828062bee440042d63
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="use-python-model-in-sql-for-training-and-scoring"></a>Verwenden Sie Python-Modell in SQL zum Trainieren und bewerten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In der [vorherigen Lektion](wrap-python-in-tsql-stored-procedure.md), haben Sie gelernt, das allgemeine Muster für die Verwendung von Python zusammen mit SQL. Sie haben gelernt, dass die Python-Code sollte eine eindeutig definierte data.frame ausgeben und optional kann mehrere Variablen von skalare oder binäre ausgeben. Sie haben gelernt, dass die gespeicherte Prozedur von SQL entworfen werden soll, übergeben den richtigen Typ von Daten in Python und die Ergebnisse zu behandeln.

In diesem Abschnitt verwenden dieses gleiche Muster zum Trainieren eines Modells auf die Daten, die Sie in SQL Server hinzugefügt haben, und speichern Sie das Modell in einer SQL Server-Tabelle:

+ Entwerfen Sie eine gespeicherte Prozedur, die eine Python-Machine learning-Funktion aufruft.
+ Die gespeicherte Prozedur benötigt Daten aus SQL Server zum Trainieren des Modells verwenden.
+ Die gespeicherte Prozedur gibt ein trainiertes Modell als binäre Variable. 
+ Speichern Sie das trainierte Modell durch die Variable Modell in eine Tabelle einzufügen. 

## <a name="create-the-stored-procedure-and-train-a-python-model"></a>Erstellen Sie die gespeicherte Prozedur und Trainieren Sie ein Python-Modell

1. Führen Sie den folgenden Code in SQL Server Management Studio zum Erstellen der gespeicherten Prozedur, in dem ein Modell erstellt.

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]]))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

2. Wenn dieser Befehl ohne Fehler ausgeführt wird, wird eine neue gespeicherte Prozedur erstellt und der Datenbank hinzugefügt. Gespeicherte Prozeduren finden Sie in Management Studio **Objektexplorer**unter **Programmierbarkeit**.

3. Führen Sie nun die gespeicherte Prozedur.

    ```sql
    EXEC generate_iris_model
    ```

    Fehler auftreten, sollten abgerufen werden, da Sie bereitgestellt haben, dass die Eingabe der gespeicherten Prozedur erforderlich ist.

    "Prozedur oder Funktion 'Generate_iris_model' erwartet den Parameter"@trained_model", der nicht bereitgestellt wurde."

4. Zum Generieren des Modells mit den erforderlichen Eingaben, und speichern es in einer Tabelle müssen einige zusätzlichen Anweisungen aus:

    ```sql
    DECLARE @model varbinary(max);
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values('Naive Bayes', @model);
    ```

5. Nun versuchen Sie, den Generierungscode Modell einmal ausgeführt. 

    Erhalten Sie die Fehlermeldung: "Verletzung der PRIMARY KEY-Einschränkung kann nicht doppelten Schlüssel im Objekt"dbo.iris_models"einfügen. Der doppelte Schlüsselwert ist (Naive Bayes-Verfahren) ".

    Ist, dass der Name des Modells bereitgestellt wurde, manuell als Teil der INSERT-Anweisung in "Naive Bayes-Verfahren" eingeben. Angenommen, Sie viele Modelle erstellen möchten, mit anderen Parametern oder verschiedene Algorithmen bei jedem Ausführen, sollten das Einrichten einer Metadaten-Schema Sie, damit Sie Modelle automatisch benennen können und weitere leicht identifizieren.

6. Um diesen Fehler zu umgehen, können Sie einige kleinere Änderungen an den SQL-Wrapper vornehmen. In diesem Beispiel wird ein eindeutiger Modellname durch das aktuelle Datum und die Uhrzeit anfügen generiert:

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes ' + CAST(GETDATE()as varchar)
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    ```

7. Um die Modelle anzuzeigen, führen Sie eine einfache SELECT-Anweisung.

    ```sql
    SELECT * FROM iris_models;
    GO
    ```

    **Ergebnisse**

    |model_name | model |
    |------|------|
    | Naive Bayes | 0x800363736B6C656172... |
    | Naive Bayes-Verfahren Jan 01 2018 9:39:00. | 0x800363736B6C656172... |
    | Naive Bayes-Verfahren Feb 01 2018 10:51 AM | 0x800363736B6C656172... |

## <a name="generate-scores-from-the-model"></a>Generieren von Bewertungen aus dem Modell

Schließlich wir dieses Modell aus der Tabelle in eine Variable laden, und übergibt ihn dann wieder an Python zum Generieren von Bewertungen.

1. Führen Sie den folgenden Code zum Erstellen der gespeicherten Prozedur ausführt, bewerten. 

    ```sql
    CREATE PROCEDURE predict_species (@model varchar(100))
    AS
    BEGIN
    DECLARE @nb_model varbinary(max) = (SELECT model FROM iris_models WHERE model_name = @model);
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    import pickle
    irismodel = pickle.loads(nb_model)
    species_pred = irismodel.predict(iris_data[[1,2,3,4]])
    iris_data["PredictedSpecies"] = species_pred
    OutputDataSet = iris_data.query( ''PredictedSpecies != SpeciesId'' )[[0, 5, 6]]
    print(OutputDataSet)
    '
    , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@nb_model varbinary(max)'
    , @nb_model = @nb_model
    WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));
    END;
    GO
    ```

    Die gespeicherte Prozedur ruft die Naïve Bayes-Modell aus der Tabelle ab und verwendet die Funktionen, die mit dem Modell verknüpft sind, zum Generieren von Bewertungen. In diesem Beispiel ruft die gespeicherte Prozedur das Modell aus der Tabelle mit dem Modellnamen ab. Allerdings je nachdem, welche Art von Metadaten Sie mit dem Modell speichern, können Sie auch das neueste Modell oder das Modell mit der höchsten Genauigkeit abrufen.

2. Führen Sie die folgenden Zeilen ein, um den Modellnamen "Naive Bayes-Verfahren" an die gespeicherte Prozedur übergeben, die Bewertungsprofile Code ausgeführt wird. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    Wenn Sie die gespeicherte Prozedur ausführen, wird eine Python-data.frame zurückgegeben. Diese Zeile von T-SQL-gibt das Schema für die zurückgegebenen Ergebnisse: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`

    Sie können die Ergebnisse in eine neue Tabelle einfügen, oder an eine Anwendung zurückzugeben.

    In diesem Beispiel verfügt über einfache vorgenommen wurden, durch die Daten aus der Python-Iris-Dataset für die Bewertung verwenden. (Finden Sie unter der Zeile `iris_data[[1,2,3,4]])`.) Allerdings in der Regel würden Ausführen eine SQL-Abfrage, um die neuen Daten zu erhalten, und übergeben, die in Python als `InputDataSet`. 

### <a name="remarks"></a>Hinweise

Wenn Sie zum Arbeiten in Python werden verwendet, können Sie beim Laden von Daten, das einige Zusammenfassungen und Diagramme erstellen und dann das Trainieren eines Modells und das Generieren von Bewertungen alle in der gleichen 250 Codezeilen sein.

Wenn Ihr Ziel ist, den Prozess (Modellerstellung, Bewertung, usw.) in SQL Server operationalisieren, ist es jedoch wichtig, die Art und Weise berücksichtigen, dass Sie den Prozess in reproduzierbare Schritte trennen können, die mit Parametern geändert werden können. So weit wie möglich ist, möchten Sie die Python-Code, den Sie, in einer gespeicherten Prozedur eindeutig definiert haben ausführen, Eingaben und Ausgaben, die gespeicherte Prozedur Eingaben und Ausgaben zugeordnet.

Darüber hinaus können Sie Leistung im Allgemeinen verbessern, durch die Trennung von Durchsuchen von Daten von der Prozesse Trainieren eines Modells oder Generieren von Bewertungen. 

Punkte zählen und Trainieren Prozesse können häufig optimiert, durch die Nutzung der Funktionen von SQL Server, wie die parallele Verarbeitung oder mithilfe von Algorithmen in [Revoscalepy](../python/what-is-revoscalepy.md) oder [MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) , streaming-Unterstützung und parallele Ausführung anstelle der Python-Standardbibliotheken verwenden. 

## <a name="next-lesson"></a>Nächste Lektion

In der letzten Lektion führen Sie die Python-Code von einem Remoteclient, mithilfe von SQL Server als computekontext. Dieser Schritt ist optional, wenn Sie keinen Python-Client haben oder nicht beabsichtigen, Python außerhalb einer gespeicherten Prozedur ausgeführt werden können.

+ [Erstellen Sie ein Modell Revoscalepy von einem Python-client](use-python-revoscalepy-to-create-model.md)
