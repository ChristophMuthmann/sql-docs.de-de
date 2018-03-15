---
title: PREDICT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/25/2018
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
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
manager: craigg
ms.openlocfilehash: c4d6b3967807c83db75dd3171313e9a5869336a1
ms.sourcegitcommit: 6e819406554efbd17bbf84cf210d8ebeddcf772d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="predict-transact-sql"></a>PREDICT (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Generiert einen vorhergesagten Wert oder Bewertungen auf Grundlage eines gespeicherten Modells.  

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

Der Parameter `MODEL` wird verwendet, um das Modell anzugeben, das für die Bewertung oder Vorhersage verwendet wird. Das Modell wird als Variable, Literal oder Skalarausdruck angegeben.

Das Modellobjekt kann mithilfe von R, Python oder eines anderen Tools erstellt werden.

**data**

Der DATA-Parameter wird verwendet, um die Daten anzugeben, die für die Bewertung oder Vorhersage verwendet werden. Daten werden in Form einer Tabellenquelle in der Abfrage angegeben. Die Tabellenquelle kann eine Tabelle, ein Tabellenalias, CTE-Alias, eine sicht oder Tabellenwertfunktion sein.

**parameters**

Der Parameter PARAMETERS wird verwendet, um optionale benutzerdefinierte Parameter anzugeben, die für die Bewertung oder die Vorhersage verwendet werden.

Der Name jedes Parameters bezieht sich auf den Typ des Modells. Die Funktion [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) in RevoScaleR unterstützt z.B. den Parameter `@computeResiduals`, der angibt, ob Restwerte beim Bewerten eines logistischen Regressionsmodells berechnet werden sollen. Wenn Sie ein kompatibles Modell aufrufen, können Sie diesen Parameternamen und einen TRUE- oder FALSE-Wert an die `PREDICT`-Funktion übergeben.

> [!NOTE]
> Diese Option funktioniert nicht in Vorabversionen von SQL Server-2017.

**WITH ( <result_set_definition> )**

Die WITH-Klausel wird verwendet, um das Schema der Ausgabe anzugeben, die von der `PREDICT`-Funktion zurückgegeben wird.

Zusätzlich zu den Spalten, die von der `PREDICT`-Funktion selbst zurückgegeben werden, stehen alle Spalten, die Teil der Dateneingabe sind, während der Abfrage zur Verfügung.

### <a name="return-values"></a>Rückgabewerte

Es steht kein vordefiniertes Schema zur Verfügung. SQL Server überprüft die Inhalte des Modells und der zurückgegebenen Spaltenwerte nicht.

- Die `PREDICT`-Funktion durchläuft die Spalten als Eingabe.
- Die `PREDICT`-Funktion generiert auch neue Spalten, allerdings hängen die Anzahl der Spalten und deren Datentypen vom Typ des Modells ab, das für die Vorhersage verwendet wurde.

Fehlermeldungen im Zusammenhang mit den Daten, dem Modell oder dem Spaltenformat werden von der zugrunde liegenden Vorhersagefunktion zurückgegeben, die dem Modell zugeordnet ist.

- Bei RevoScaleR lautet die entsprechende Funktion [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict).  
- Bei MicrosoftML lautet die entsprechende Funktion [rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict).  

Es ist nicht möglich, die interne Modellstruktur mithilfe von `PREDICT` anzuzeigen. Wenn Sie sich mit dem Inhalt des Modells vertraut machen möchten, müssen Sie das Modellobjekt laden, es deserialisieren und entsprechenden R-Code verwenden, um das Modell zu analysieren.

## <a name="remarks"></a>Remarks

Die `PREDICT`-Funktion wird in allen Editionen von SQL Server, einschließlich Linux, und in Azure SQL-Datenbank unterstützt, unabhängig davon, ob andere Machine Learning-Features aktiviert sind. Allerdings ist SQL Server 2017 oder höher erforderlich. 

Es ist nicht notwendig, dass R, Python oder eine andere Machine Learning-Sprache auf dem Server installiert ist, um die `PREDICT`-Funktion zu verwenden. Sie können das Modell in einer anderen Umgebung trainieren und in einer SQL Server-Tabelle für die Verwendung mit `PREDICT` speichern, oder das Modell aus einer anderen Instanz von SQL Server aufrufen, die das gespeicherte Modell enthält.

### <a name="supported-algorithms"></a>Unterstützte Algorithmen

Das Modell, das Sie verwenden, muss mithilfe eines der unterstützen Algorithmen aus dem RevoScaleR-Paket erstellt worden sein. Eine Liste der derzeit unterstützten Modelle finden Sie unter [Real-time scoring (Echtzeitbewertung)](../../advanced-analytics/real-time-scoring.md).

### <a name="permissions"></a>Berechtigungen

Es sind zwar keine Berechtigungen für `PREDICT` erforderlich, jedoch benötigt der Benutzer `EXECUTE`-Berechtigungen für die Datenbank und Berechtigungen zum Abfragen von Daten, die als Eingaben verwendet werden. Der Benutzer muss außerdem das Modell aus einer Tabelle heraus lesen können, wenn das Modell in einer Tabelle gespeichert wurde.

## <a name="examples"></a>Beispiele

Die folgenden Beispiele veranschaulichen die Syntax zum Aufrufen von `PREDICT`.

### <a name="call-a-stored-model-and-use-it-for-prediction"></a>Aufrufen eines gespeicherten Modells zur Verwendung für eine Vorhersage

Dieses Beispiel ruft ein vorhandenes logistisches Regressionsmodell auf, dass in der Tabelle [models_table] gespeichert ist. Es ruft das aktuellste trainierte Modell mithilfe einer SELECT-Anweisung ab, und übergibt das binäre Modell an die PREDICT-Funktion. Die Eingabewerte stellen Features dar. Die Ausgabe stellt die vom Modell zugewiesene Klassifizierung dar.

```sql
DECLARE @logit_model varbinary(max) = "SELECT TOP 1 [model_binary] from [models_table] ORDER BY [trained_date] DESC";
DECLARE @input_qry = "SELECT ID, [Gender], [Income] from NewCustomers";

SELECT PREDICT [class]
FROM PREDICT( MODEL = @logit_model,  DATA = @input_qry
WITH (class string);
```

### <a name="using-predict-in-a-from-clause"></a>Verwenden von PREDICT in einer FROM-Klausel

In diesem Beispiel wird auf die `PREDICT`-Funktion in der `FROM`-Klausel einer `SELECT`-Anweisung verwiesen:

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

Der Alias **d**, der für die Tabellenquelle im `DATA`-Parameter angegeben ist, wird verwendet, um auf die Spalten zu verweisen, die zu dbo.mytable gehören. Der Alias **p**, der für die **PREDICT**-Funktion angegeben ist, wird verwendet, um auf die Spalten zu verweisen, die von der PREDICT-Funktion zurückgegeben werden.

### <a name="combining-predict-with-an-insert-statement"></a>Kombinieren von PREDICT mit einer INSERT-Anweisung

Einer der gängigsten Anwendungsfälle für die Vorhersage ist das Generieren einer Bewertung für Eingabedaten und das anschließende Einfügen der vorhergesagten Werte in eine Tabelle. Im folgenden Beispiel wird davon ausgegangen, dass die aufrufende Anwendung eine gespeicherte Prozedur verwendet, um eine Zeile mit dem vorhergesagten Wert in eine Tabelle einzufügen:

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

Wenn die Prozedur mehrere Zeilen über einen Tabellenwertparameter aufnimmt, kann sie wie folgt geschrieben werden:

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

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>Erstellen eines R-Modells und Generieren von Bewertungen mithilfe optionaler Modellparameter

> [!NOTE]
> Das Verwenden des Parameterarguments wird in Release Candidate 1 nicht unterstützt.

In diesem Beispiel wird davon ausgegangen, dass Sie ein logistisches Regressionsmodell mit eingebauter Kovarianzmatrix erstellt haben und einen ähnlichen Aufruf von RevoScaleR verwendet haben:

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

Wenn Sie das Modell in SQL Server im Binärformat speichern, können Sie die PREDICT-Funktion verwenden, um nicht nur Vorhersagen, sondern auch zusätzliche Funktionen zu erstellen, die vom Modelltyp unterstützt werden, z.B. Fehler- oder Vertrauensintervalle.

Der folgende Code zeigt den entsprechenden Aufruf von R zu [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict):

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

Der äquivalente Aufruf mithilfe der `PREDICT`-Funktion bietet ebenso die Bewertung (vorhergesagter Wert), Fehler- und Vertrauensintervalle:

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```
