---
title: "Zum Ausführen von Realtime Bewertung oder systemeigenen bewerten in SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 11/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9287a85017df7b05b3b354a855811ea528a3ad79
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="how-to-perform-realtime-scoring-or-native-scoring-in-sql-server"></a>Zum Bewerten von Realtime oder systemeigenen bewerten in SQL Server ausführen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieses Thema enthält Anweisungen und Beispielcode für die Echtzeit-Bewertung ausführen und systemeigenen bewertungs-Funktionen in SQL Server-2017 und SQL Server 2016. Das Ziel von Realtime Bewertung und systemeigene Bewertung ist zum Verbessern der Leistung von bewerteten Vorgängen in kleinen Batches.

Sowohl Echtzeit Bewertung als auch systemeigene Bewertung dienen ein Machine learning-Modell ohne Installation von r verwenden Alles, was Sie tun müssen ist ein vortrainierte Modell in einem kompatiblen Format zu erhalten, und speichern sie in einer SQL Server-Datenbank.

## <a name="choosing-a-scoring-method"></a>Wählen eine Bewertungsmethode

Die folgenden Optionen sind für die schnelle Batch Vorhersage unterstützt:

+ **Bewerten von systemeigenen**: VORHERSAGEN von T-SQL-Funktion in SQL Server-2017
+ **Bewerten von Realtime**: mit der sp\_RxPredict gespeicherte Prozedur in SQL Server 2016 oder SQL Server-2017.

> [!NOTE]
> Verwendung der PREDICT-Funktion wird in SQL Server-2017 empfohlen.
> Verwenden von sp\_RxPredict erfordert, dass Sie die SQLCLR-Integration aktivieren. Beachten Sie die Sicherheitsrisiken, bevor Sie diese Option aktivieren.

Der allgemeine Prozess Vorbereiten des Modells, und klicken Sie dann Generieren von Bewertungen ähnelt:

1. Erstellen Sie ein Modell mit einem unterstützten Algorithmus an.
2. Das Modell mit einer speziellen binary-Format zu serialisieren.
3. Stellen Sie das Modell mit SQL Server zur Verfügung. In der Regel bedeutet dies, speichern serialisierte Modell in einer SQL Server-Tabelle.
4. Rufen Sie die Funktion oder gespeicherten Prozedur, und übergeben Sie das Modell und die Eingabedaten.

### <a name="requirements"></a>Anforderungen

+ Die PREDICT-Funktion ist in allen Editionen von SQL Server-2017 verfügbar und ist standardmäßig aktiviert. Sie müssen sich nicht um R zu installieren oder zusätzliche Funktionen aktivieren.

+ Bei Verwendung von sp\_RxPredict, sind einige zusätzliche Schritte erforderlich. Finden Sie unter [ermöglichen, Echtzeit Bewertung](#bkmk_enableRtScoring).

+ Zu diesem Zeitpunkt kann nur "revoscaler" und MicrosoftML kompatiblen Modelle erstellen. Zusätzliche Modelltypen möglicherweise in Zukunft verfügbar sein. Die Liste der derzeit unterstützten Algorithmen finden Sie [Echtzeit Bewertung](../real-time-scoring.md).

### <a name="serialization-and-storage"></a>Serialisierung und Speicher

Um ein Modell mit der schnellen bewertungs-Optionen verwenden, speichern Sie das Modell mithilfe ein spezielles serialisiertes-Format, das für die Größe optimiert wurde, und Bewerten von Effizienz.

+ Rufen Sie `rxSerializeModel` schreiben Sie unterstützten Modells, um die **unformatierten** Format.
+ Rufen Sie `rxUnserializeModel` wiederherstellen, kann das Modell für die Verwendung in anderen R-Code oder das Modell anzuzeigen.

Weitere Informationen finden Sie unter [RxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel).

**Verwenden von SQL**

Von SQL-Code können Sie trainieren, das Modell mit `sp_execute_external_script`, und fügen Sie direkt die trainierten Modelle in einer Tabelle in einer Spalte vom Typ **varbinary(max)**.

Ein einfaches Beispiel finden Sie unter [dieses Lernprogramms](../tutorials/rtsql-create-a-predictive-model-r.md)

**Mithilfe von R**

Es gibt zwei Möglichkeiten, um das Modell in einer Tabelle zu speichern, aus R-Code:

+ Rufen Sie die `rxWriteObject` Funktion, die RevoScaleR-Paket, um das Modell direkt in die Datenbank geschrieben.

  Die `rxWriteObject()` Funktion R-Objekte aus einer ODBC-Datenquelle wie SQL Server abrufen kann, oder Schreiben von Objekten mit SQL Server. Die API ist eine einfache Schlüssel / Wert-Speicher nachgebildet.
  
  Wenn Sie diese Funktion verwenden, achten Sie darauf, dass Sie das Modell zunächst unter Verwendung der neuen Serialisierungsfunktion zu serialisieren. Schalten Sie dann die *Serialisieren* Argument im `rxWriteObject` auf "false", um zu vermeiden, die Serialisierung Schritt wiederholen.

+ Sie können auch das Modell im raw-Format in eine Datei speichern und dann in SQL Server aus der Datei gelesen. Diese Option kann nützlich sein, wenn Sie verschieben oder Kopieren von Modellen zwischen Umgebungen.

## <a name="native-scoring-with-predict"></a>Systemeigen mit VORHERSAGEN bewerten

In diesem Beispiel erstellen Sie ein Modell, und rufen Sie anschließend die Echtzeit-Vorhersagefunktion aus T-SQL.

### <a name="step-1-prepare-and-save-the-model"></a>Schritt 1: Vorbereiten Sie und speichern Sie das Modell

Führen Sie den folgenden Code zum Erstellen der Beispieldatenbank und die erforderlichen Tabellen.

```SQL
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
  "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

Verwenden Sie die folgende Anweisung zum Auffüllen der Datentabelle mit Daten aus der **Iris** Dataset.

```SQL
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

Erstellen Sie jetzt eine Tabelle zum Speichern von Modellen.

```SQL
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

Der folgende Code erstellt ein Modell auf Grundlage der **Iris** Dataset und speichert sie in der Tabelle mit dem Namen **Modelle**.

```SQL
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE] 
> Achten Sie darauf, dass Sie verwenden die [RxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) Funktion vom "revoscaler", um das Modell zu speichern. Der standard R `serialize` Funktion kann nicht das erforderliche Format generiert werden.

Sie können z. B. Folgendes verwenden, um das gespeicherte Modell im Binärformat anzuzeigen. eine Anweisung ausführen:

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Schritt 2: Führen Sie VORHERSAGEN für das Modell

Die folgende einfache PREDICT-Anweisung ruft eine Klassifizierung ab, von der Entscheidung Tree-Modell unter Verwendung der **native Bewertung** Funktion. Es vorhersagt Iris Arten basierend auf Attribute, die Sie bereitstellen, sodass Länge und Breite.

```SQL
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

Wenn Sie die Fehlermeldung erhalten, Fehler"bei der Ausführung der PREDICT-Funktion. Modell ist beschädigt oder ungültig", es bedeutet normalerweise, dass die Abfrage kein Modell zurückgegeben haben nicht. Überprüfen Sie, ob Sie den Modellnamen richtig eingegeben haben, oder wenn die Modelle Tabelle leer ist.

> [!NOTE]
> Da die Spalten und Werte von zurückgegeben **PREDICT** nach Modelltyp variieren können, definieren Sie das Schema der zurückgegebenen Daten mithilfe einer **WITH** Klausel.

## <a name="realtime-scoring-with-sprxpredict"></a>Echtzeit-batchbewertung mit sp_rxPredict

Dieser Abschnitt beschreibt die erforderlichen Schritte zum Einrichten von **Echtzeit** Vorhersage, und veranschaulicht, wie die Funktion von T-SQL aus aufgerufen.

### <a name ="bkmk_enableRtScoring"></a>Schritt 1. Aktivieren Sie die Bewertung der Prozedur Echtzeit

Sie müssen diese Funktion für jede Datenbank aktivieren, die Sie für die Bewertung verwenden möchten. Der Serveradministrator sollte das Befehlszeile-Hilfsprogramm RegisterRExt.exe, führen Sie die in die RevoScaleR-Paket enthalten ist.

> [!NOTE]
> Damit für Echtzeit-Bewertung zur arbeiten können muss SQL CLR-Funktionalität in der Instanz aktiviert werden; Darüber hinaus muss die Datenbank als vertrauenswürdig markiert werden. Wenn Sie das Skript ausführen, werden diese Aktionen für Sie ausgeführt. Auswirkungen auf die zusätzliche Sicherheit sollten Sie jedoch zuvor!

1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und navigieren Sie zu dem Ordner, in dem RegisterRExt.exe befindet. Der folgende Pfad kann in einer Standardinstallation verwendet werden:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Führen Sie den folgenden Befehl ein, und den Namen der Instanz und die Zieldatenbank, in dem Sie die erweiterten gespeicherten Prozeduren ermöglichen möchten:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Geben Sie z. B. die erweiterte gespeicherte Prozedur um die CLRPredict-Datenbank auf der Standardinstanz hinzuzufügen:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    Der Instanzname ist optional, wenn die Datenbank auf der Standardinstanz befindet. Wenn Sie eine benannte Instanz verwenden, müssen Sie den Instanznamen angeben.

3. RegisterRExt.exe erstellt die folgenden Objekte:

    + Vertrauenswürdige Assemblys
    + Die gespeicherte Prozedur`sp_rxPredict`
    + Eine neue Datenbankrolle `rxpredict_users`. Der Datenbankadministrator kann diese Rolle verwenden, Berechtigung Benutzern erteilen, die Bewertungsprofile Echtzeit-Funktionalität verwenden.

4. Fügen Sie alle Benutzer, die auszuführenden `sp_rxPredict` der neuen Rolle.

> [!NOTE]
> 
> In SQL Server 2017 gelten zusätzliche Sicherheitsmaßnahmen auf Probleme mit CLR-Integration zu verhindern. Diese Measures vorgeben zusätzliche Einschränkungen für die Verwendung dieser gespeicherten Prozedur auch. 

### <a name="step-2-prepare-and-save-the-model"></a>Schritt 2: Vorbereiten Sie und speichern Sie das Modell

Das binäre Format sp erforderlichen\_RxPredict ist identisch mit dem Format erforderlich, um die Vorhersagefunktion verwenden. Daher in Ihrem R-Code enthalten einen Aufruf von [RxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), und geben Sie unbedingt `realtimeScoringOnly = TRUE`, wie in diesem Beispiel:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Schritt 3: Rufen Sie sp_rxPredict

Rufen Sie sp\_RxPredict wie würde jeder andere Prozedur enthält. In der aktuellen Version die gespeicherte Prozedur akzeptiert nur zwei Parameter:  _@model_  für das Modell im binären Format und  _@inputData_  für die Daten zur Verwendung in der Bewertung, definiert als eine gültige SQL-Abfrage .

Da das Binärformat identisch, die von der PREDICT-Funktion verwendet wird ist, können Sie die Modelle und eine Datentabelle aus dem vorherigen Beispiel.

```SQL
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> Der Aufruf von sp\_RxPredict schlägt fehl, wenn die Eingabedaten für die Bewertung keine Spalten enthalten, die die Anforderungen des Modells entsprechen. Derzeit werden nur die folgenden .NET Datentypen unterstützt: double, Float, Short, Ushort, long, ulong-Typ und Zeichenfolge.
> 
> Aus diesem Grund müssen Sie die nicht unterstützten Typen der Eingabedaten herausfiltern, bevor Sie sie für die Bewertung von Realtime verwenden.
> 
> Informationen zur entsprechenden SQL-Datentypen finden Sie unter [SQL-CLR-Typzuordnung](https://msdn.microsoft.com/library/bb386947.aspx) oder [Zuordnen von CLR-Parameterdaten](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-realtime-scoring"></a>Deaktivieren Sie Echtzeit-Bewertung

Um bewerteten Echtzeit-Funktionen zu deaktivieren, öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und führen Sie den folgenden Befehl:`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="realtime-scoring-in-microsoft-r-server-or-machine-learning-server"></a>Echtzeit-Bewertung in Microsoft R Server "oder" Machine Learning-Server

Machine Learning-Server unterstützt verteilte Echtzeit Bewertung von Modellen, die als Webdienst veröffentlicht. Weitere Informationen dazu finden Sie in diesen Artikeln:

+ [Was sind Webdienste in Machine Learning-Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [Was ist operationalisierung?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [Bereitstellen eines Python-Modells als Webdienst mit Azureml-Modell-Management-sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Veröffentlichen Sie ein R-Code-Block oder ein Echtzeit-Modell als ein neuer Webdienst.](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [Mrsdeploy-Paket für R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)
