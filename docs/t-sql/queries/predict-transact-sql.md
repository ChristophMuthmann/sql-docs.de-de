---
title: VORHERSAGEN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 529cb229b6658085d0f2122604a4ed638f66a84c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="predict-transact-sql"></a>VORHERSAGEN Sie (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Generiert einen vorhergesagten Wert oder die Ergebnisse auf Grundlage eines gespeicherten Modells.  

## <a name="syntax"></a>Syntax

```
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>  
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

MODEL = @model | model_literal  
```

### <a name="arguments"></a>Argumente

**model**

Die `MODEL` Parameter wird verwendet, um das Modell für die Bewertung oder für Vorhersagen verwendet anzugeben. Das Modell wird als eine Variable oder ein Literal oder ein skalarer Ausdruck angegeben.

Das Modellobjekt kann mithilfe von R oder Python oder ein anderes Tool erstellt werden.

**Daten**

DATA-Parameter dient zum Angeben der Daten für die Bewertung oder die Vorhersage verwendet. Daten in Form einer Tabellenquelle in der Abfrage angegeben. Tabellenquelle kann es sich um eine Tabelle, Tabellenalias, CTE-Alias, Sicht oder Tabellenwertfunktion handeln.

**Parameter**

Der Parameter-Parameter wird verwendet, an die optionale benutzerdefinierte Parameter für die Bewertung oder die Vorhersage verwendet.

Der Name jedes Parameters bezieht sich auf den Typ des Modells. Die RxPredict-Funktion in "revoscaler" unterstützt z. B. den Parameter  _@computeResiduals Bit_ zur Berechnung des Restwerte Unterstützung bei der Bewertung eines logistischen Regressionsmodells. Übergeben Sie, dass der Parametername und Wert der `PREDICT` Funktion.

> [HINWEIS] Diese Option wird nicht unterstützt, in der Vorabversion von SQL Server-2017 und dienen lediglich der Forward-Kompatibilität enthalten ist.

**MIT ( \<Result_set_definition >)**

Die WITH-Klausel wird verwendet, um das Schema für die zurückgegebene Ausgabe angeben der `PREDICT` Funktion.

Zusätzlich zu den Spalten, die zurückgegeben werden, indem Sie die `PREDICT` Funktion selbst, alle Spalten, die Teil der Daten sind Eingabe stehen zur Verwendung in der Abfrage.

### <a name="return-values"></a>Rückgabewerte

Es steht keine vordefinierten Schema; SQL Server überprüft nicht den Inhalt des Modells und überprüft nicht die Werte der zurückgegebenen Spalte.  
- Die `PREDICT` Funktion durchläuft die Spalten als Eingabe  
- Die `PREDICT` Funktion generiert auch neue Spalten, aber die Anzahl der Spalten und deren Datentypen hängt vom Typ des Modells, die für die Vorhersage verwendet wurde.  

Fehlermeldungen mit den Daten verknüpft, werden die zugrunde liegenden Vorhersagefunktion, die dem Modell zugeordnet das Modell oder des Spaltenformats von zurückgegeben.  
- Für "revoscaler", wird die entsprechende Funktion [RxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)  
- Für MicrosoftML, wird die entsprechende Funktion [rxPredict.mlModel](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxpredict)  

Es ist nicht möglich, die Struktur mit internen Modellen anzeigen `PREDICT`. Wenn Sie den Inhalt des Modells selbst verstehen möchten, müssen Sie das Modellobjekt laden, deserialisieren Sie ihn und entsprechenden R-Code verwenden, um das Modell zu analysieren.

## <a name="remarks"></a>Hinweise

Die `PREDICT` Funktion wird in allen Editionen von SQL Server, einschließlich Linux unterstützt.

Es ist nicht notwendig, R, Python oder einer anderen Machine learning-Sprache installiert sein, auf dem Server verwendet die `PREDICT` Funktion. Sie können Trainieren des Modells in einer anderen Umgebung und speichern Sie sie in einer SQL Server-Tabelle für die Verwendung mit `PREDICT`, oder rufen Sie das Modell aus einer anderen Instanz von SQL Server, der das gespeicherte Modell verfügt.

### <a name="supported-algorithms"></a>Algorithmen unterstützt:

Das Modell, mit denen Sie muss mit einem der unterstützten Algorithmen aus dem "revoscaler"-Paket erstellt worden sein. Eine Liste der derzeit unterstützten Modellen, finden Sie unter [Echtzeit Bewertung](../../advanced-analytics/real-time-scoring.md).

### <a name="permissions"></a>Berechtigungen

Es sind keine Berechtigungen erforderlich, damit `PREDICT`, aber die Bedürfnisse der Benutzer `EXECUTE` -Berechtigung für die Datenbank und über die Berechtigung zum Abfragen von Daten, die als Eingaben verwendet wird. Der Benutzer muss auch das Modell aus einer Tabelle zu lesen sein, wenn Sie das Modell in einer Tabelle gespeichert wurde.

## <a name="examples"></a>Beispiele

Die folgenden Beispiele veranschaulichen die Syntax für den Aufruf von `PREDICT`.

### <a name="call-a-stored-model-and-use-it-for-prediction"></a>Rufen Sie eine gespeicherte Modell und zur Vorhersage zu verwenden

Dieses Beispiel ruft ein vorhandenes logistic Regressionsmodell in Tabelle [Models_table] gespeichert. Es ruft trainierten Modell enthält, mithilfe einer SELECT-Anweisung ab und übergibt dann die Vorhersagefunktion binäre Modell. Die Eingabewerte stellen Funktionen dar. die Ausgabe darstellt, die Klassifizierung, die vom Modell zugewiesen wird.

```sql
DECLARE @logit_model varbinary(max) = "SELECT TOP 1 @model from [models_table]";
DECLARE @input_qry = "SELECT ID, [Gender], [Income] from NewCustomers";

SELECT PREDICT [class]
FROM PREDICT( MODEL = @logit_model,  DATA = @input_qry
WITH (class string);
```

### <a name="using-predict-in-a-from-clause"></a>Verwenden von VORHERSAGEN in einer FROM-Klausel

In diesem Beispiel verweist auf die `PREDICT` -Funktion in der `FROM` -Klausel eine `SELECT` Anweisung:

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

Der Alias **d** angegeben, für die Quelltabelle in der _Daten_ Parameter wird verwendet, um die Spalten, die zu dbo.mytable gehören verweisen. Der Alias **p** angegeben für die **PREDICT** Funktion wird verwendet, um die von der PREDICT-Funktion zurückgegebenen Spalten verweisen.

### <a name="combining-predict-with-an-insert-statement"></a>Kombinieren von VORHERSAGEN mit einer INSERT-Anweisung

Eine gängige Einsatzgebiete für die Vorhersage ist für die Eingabedaten eine Bewertung zu generieren, und klicken Sie dann die vorhergesagten Werte in eine Tabelle einzufügen. Im folgende Beispiel wird davon ausgegangen, dass die aufrufende Anwendung eine gespeicherte Prozedur verwendet, um eine Zeile mit den vorhergesagten Wert in eine Tabelle einzufügen:

```sql
CREATE PROCEDURE InsertLoanApplication
(@p1 varchar(100), @p2 varchar(200), @p3 money, @p4 int)
AS
BEGIN
  DECLARE @model varbinary(max) = (select model
  FROM scoring_model
  WHERE model_name = 'ScoringModelV1');
  WITH d as ( SELECT * FROM (values(@p1, @p2, @p3, @p4)) as t(c1, c2, c3, c4) )

  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = d) WITH(score float) as p;
END;
```

Wenn mehrere Zeilen über einen Tabellenwertparameter in die Prozedur ausgeführt wird, kann er wie folgt geschrieben:

```sql
CREATE PROCEDURE InsertLoanApplications (@new_applications dbo.loan_application_type)
AS
BEGIN
  DECLARE @model varbinary(max) = (SELECT model_bin FROM scoring_models WHERE model_name = 'ScoringModelV1');
  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = @new_applications as d)
  WITH (score float) as p;
END;
```

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>Erstellen ein R-Modell und Generieren von Bewertungen mit optionalen Parametern zu modellieren

> [!NOTE]
> Verwenden des Arguments Parameter wird nicht im Release Candidate 1 unterstützt.

In diesem Beispiel wird davon ausgegangen, dass Sie ein logistischen Regressionsmodells mit einem kovarianzmatrix eingebaut erstellt haben, über einen Aufruf an "revoscaler", wie diese:

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

Wenn Sie das Modell im Binärformat in SQL Server speichern, können Sie die Vorhersagefunktion, nicht nur Vorhersagen, sondern zusätzliche Informationen, die durch den Modelltyp, z. B. Fehler oder Vertrauensbereiche unterstützt generiert.

Der folgende Code zeigt die entsprechenden Aufruf von R RxPredict:

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

Die entsprechenden Aufruf mit der `PREDICT` Funktion bietet außerdem die Bewertung (vorhergesagten Wert), Fehler- und Vertrauensbereiche:

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```



