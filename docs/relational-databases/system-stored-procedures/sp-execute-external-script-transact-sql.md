---
title: Sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/22/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1c1a69ce5647abb9b0b75dce96f755db0dbf6721
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spexecuteexternalscript-transact-sql"></a>Sp_execute_external_script (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Führt das Skript, das als Argument an einen externen Speicherort bereitgestellt. Das Skript muss in einer unterstützten und registrierten Sprache geschrieben werden. Auszuführende **Sp_execute_external_script**, Sie müssen zunächst aktivieren externer Skripts, die mit der Anweisung `sp_configure 'external scripts enabled', 1;`.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]   
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```

## <a name="arguments"></a>Argumente
 @language = N'*Sprache*"  
 Gibt die Skriptsprache an. *Sprache* ist **Sysname**.  

 Gültige Werte sind `Python` oder `R`. 
  
 @script = N'*Skript*"  
 Externe sprachschrift Domänenmodells ein literal oder eine Variable angegeben. *Skript* ist **nvarchar(max)**.  
  
 [ @input_data_1_name = N'*input_data_1_name*"]  
 Gibt den Namen der Variablen, die zur Darstellung von definierten Abfrage @input_data_1. Der Datentyp der Variablen im externen Skript hängt von der Sprache ab. Im Falle von R wird die Eingabevariable einem Datenrahmen. Im Fall von Python muss die Eingabe tabellarische sein. *input_data_1_name* ist **Sysname**.  
  
 Standardwert ist `InputDataSet`.  
  
 [ @input_data_1 = N'*input_data_1*"]  
 Gibt an, die Eingabedaten unter Verwendung des Skripts in Form von externen verwendet eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Abfrage. Der Datentyp des *input_data_1* ist **nvarchar(max)**.
  
 [ @output_data_1_name = N'*output_data_1_name*"]  
 Gibt den Namen der Variablen in externen Skripts mit den Daten zu zurückzugebenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach Abschluss des Aufrufs der gespeicherten Prozedur. Der Datentyp der Variablen im externen Skript hängt von der Sprache ab. Für R muss die Ausgabe einem Datenrahmen. Für Python muss die Ausgabe einem Datenrahmen Pandas sein. *output_data_1_name* ist **Sysname**.  
  
 Standardwert ist "OutputDataSet".  
  
 [ @parallel = 0 | 1] ermöglichen parallele Ausführung von R-Skripts durch Festlegen der `@parallel` -Parameter auf 1 fest. Der Standardwert für diesen Parameter ist 0 (keine Parallelität).  
  
 Für R-Skripts, die nicht mithilfe von RevoScaleR-Funktionen verwenden die `@parallel` Parameter kann für die Verarbeitung großer Datasets, vorausgesetzt, das Skript im Grunde parallelisiert werden kann nützlich sein. Beispielsweise, wenn von der R `predict` Funktion mit einem Modell, um neue Vorhersagen generieren, legen Sie `@parallel = 1` als Hinweis für das Abfragemodul. Wenn die Abfrage parallelisiert werden kann, werden Zeilen gemäß verteilt die **MAXDOP** Einstellung.  
  
 Wenn `@parallel = 1` und die Ausgabe wird direkt auf den Clientcomputer gestreamt wird und dann die `WITH RESULTS SETS` -Klausel ist erforderlich und einem Ausgabeschema muss angegeben werden.  
  
 Für R-Skripts, die RevoScaleR-Funktionen verwenden, paralleler Verarbeitung erfolgt automatisch und sollte nicht angegeben werden `@parallel = 1` auf die **Sp_execute_external_script** aufrufen.  
  
 [ @params = N' *@parameter_name Data_type* [OUT | Ausgabe] [,... ...n] "]  
 Eine Liste der Eingabeparameter-Deklarationen, die in der externen Skript verwendet werden.  
  
 [ @parameter1 = "*value1*' [| Ausgabe] [,... ...n]]  
 Eine Liste von Werten für die Eingabeparameter, die vom externen Skript verwendet werden soll.  

## <a name="remarks"></a>Hinweise

Verwendung **Sp_execute_external_script** zum Ausführen von Skripts, die in einer unterstützten Sprache geschrieben. Aktuell sind die unterstützte Sprachen für SQL Server 2016 und Python R und R für SQL Server-2017. 

> [!IMPORTANT]
> Die Abfragestruktur wird gesteuert, indem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Benutzer beliebige Vorgänge für die Abfrage ausführen können. 

Standardmäßig werden von dieser gespeicherten Prozedur zurückgegebenen Resultsets Ausgabe mit unbenannten Spalten. Spaltennamen, die in einem Skript verwendet gelten lokal in der skriptumgebung und werden nicht im ausgegebenen Resultset wiedergegeben. Verwenden Sie die Resultset-Spalten Name, der `WITH RESULTS SET` -Klausel der [ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md).
  
 Sie können zusätzlich zum Zurückgeben eines Resultsets, Skalare Werte zurückgeben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe von OUTPUT-Parameter. Das folgende Beispiel zeigt die Verwendung des OUTPUT-Parameters, um das serialisierte R-Modell zurückzugeben, das als Eingabe für das Skript verwendet wurde:  

In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] besteht aus einer Serverkomponente, die mit installierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und einen Satz von arbeitsstationstools und verbindungsbibliotheken, die Verbindung mit der hochleistungsumgebung von der Data Scientist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Müssen Sie installieren, Machine learning Komponenten während der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup, um die Ausführung externer Skripts ermöglichen. Weitere Informationen finden Sie unter [Einrichten von SQL Server-Machine Learning-Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).  
  
Sie können Ressourcen von externer Skripts, die durch einen externen Ressourcenpool konfigurieren steuern. Weitere Informationen finden Sie unter [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Informationen über die arbeitsauslastung können aus den Katalogsichten der Ressourcenkontrolle, die DMVS und die Leistungsindikatoren abgerufen werden. Weitere Informationen finden Sie unter [Katalogsichten der Ressourcenkontrolle &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Resource Governor verwandte dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md), und [ SQLServer, externe Skripts Objekt](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

Monitor-skriptausführung mit [dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) und [dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

## <a name="streaming-execution-for-r-and-python-scripts"></a>Streaming-Ausführung von R und Python-Skripts  

Streaming ermöglicht das R oder Python-Skript zum Arbeiten mit mehr Daten als in den Arbeitsspeicher passen können. Um zu steuern, die Anzahl der Zeilen, die während der streaming übergeben, geben Sie einen ganzzahligen Wert für den Parameter `@r_rowsPerRead` in der `@params` Auflistung.  Zum Beispiel wenn Sie ein Modell, die sehr viele Daten verwendet trainieren, konnte Sie anpassen, den Wert zum Lesen von weniger Zeilen, um sicherzustellen, dass alle Zeilen in einem Datenblock gesendet werden können. Dieser Parameter können auch die Anzahl der Zeilen gelesen und gleichzeitig verarbeitet werden, um das Minimieren von Leistungsproblemen Server verwalten. 
  
Sowohl die `@r_rowsPerRead` Parameter für das streaming und die `@parallel` Argument sollte Hinweise berücksichtigt werden. Für den Hinweis, angewendet werden soll muss es möglich, einen SQL-Abfrageplan zu generieren, der parallelen Verarbeitung enthält. Wenn dies nicht möglich ist, kann die paralleler Verarbeitung nicht aktiviert werden.  
  
> [!NOTE]  
>  Streaming und parallele Verarbeitung werden nur in Enterprise Edition unterstützt. Sie können die Parameter in Ihren Abfragen in der Standard Edition einschließen, ohne ein Fehler ausgelöst wird, jedoch Parameter haben keine Auswirkung und R-Skripts, die in einem einzelnen Prozess ausführen.  
  
## <a name="restrictions"></a>Einschränkungen  


### <a name="data-types"></a>Datentypen

Die folgenden Datentypen werden nicht unterstützt, bei der Verwendung in der Eingabeabfrage oder die Parameter des `sp_execute_external_script` Prozedur, und der Rückgabewert ein nicht unterstützter Typ-Fehler.  

Dieses Problem zu umgehen **Umwandlung** die Spalte oder den Wert in einen unterstützten Typ in [!INCLUDE[tsql](../../includes/tsql-md.md)] vor dem Senden an das externe Skript.  
  
-   **Cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **"DateTimeOffset"**, **Zeit**  
  
-   **sql_variant**  
  
-   **Text**, **Bild**  
  
-   **xml**  
  
-   **Hierarchyid**, **Geometrie**, **Geography**  
  
-   Benutzerdefinierte CLR-Typen

Im Allgemeinen einer Gruppe, die zugeordnet werden kann, führt eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Datentyp, wird die Ausgabe als NULL.  

### <a name="restrictions-specific-to-r"></a>Einschränkungen für R spezifisch

Wenn die Eingabe enthält **"DateTime"** Werte, die nicht den zulässigen Wertebereich R groß genug ist, werden Werte in konvertiert **NA**. Dies ist erforderlich, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht eine größere Anzahl von Werten als in der Sprache "R" unterstützt wird.

Float-Werte (z. B. `+Inf`, `-Inf`, `NaN`) können nicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , obwohl beide Sprachen IEEE 754 verwenden. Aktuelle Verhalten sendet nur die Werte, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] direkt als Ergebnis der SQL-Client in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] löst einen Fehler aus. Daher werden diese Werte konvertiert, um **NULL**.

## <a name="permissions"></a>Berechtigungen

Erfordert **EXECUTE ANY EXTERNAL SCRIPT** -Datenbankberechtigung.  

## <a name="examples"></a>Beispiele

Dieser Abschnitt enthält Beispiele, wie diese gespeicherte Prozedur verwendet werden kann, zum Ausführen von R oder Python-Skripts mit [!INCLUDE[tsql](../../includes/tsql-md.md)].

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. Zurückgeben eines R-Datasets zu SQL Server  

Das folgende Beispiel erstellt eine gespeicherte Prozedur, die verwendet **Sp_execute_external_script** zur Rückgabe des Iris-Datasets enthaltenen R zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

```sql
DROP PROC IF EXISTS get_iris_dataset;  
go  
CREATE PROC get_iris_dataset
AS  
BEGIN  
 EXEC   sp_execute_external_script  
       @language = N'R'  
     , @script = N'iris_data <- iris;'
     , @input_data_1 = N''  
     , @output_data_1_name = N'iris_data'
     WITH RESULT SETS (("Sepal.Length" float not null,   
           "Sepal.Width" float not null,  
        "Petal.Length" float not null,   
        "Petal.Width" float not null, "Species" varchar(100)));  
END;
GO
```

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. Generieren eines R-Modells, basierend auf Daten aus SQL Server  

Das folgende Beispiel erstellt eine gespeicherte Prozedur, die verwendet **Sp_execute_external_script** ein Iris-Modell zu generieren und das Modell zurückgeben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE]
>  Dieses Beispiel benötigen Sie erweiterte Installation des Pakets e1071. Weitere Informationen finden Sie unter [Installieren zusätzlicher R-Pakete unter SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md).

```sql
DROP PROC IF EXISTS generate_iris_model;
GO
CREATE PROC generate_iris_model
AS
BEGIN
 EXEC sp_execute_external_script  
      @language = N'R'  
     , @script = N'  
          library(e1071);  
          irismodel <-naiveBayes(iris_data[,1:4], iris_data[,5]);  
          trained_model <- data.frame(payload = as.raw(serialize(irismodel, connection=NULL)));  
'  
     , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from iris_data'  
     , @input_data_1_name = N'iris_data'  
     , @output_data_1_name = N'trained_model'  
    WITH RESULT SETS ((model varbinary(max)));  
END;
GO
```

Um ein ähnliches Modell mithilfe von Python zu generieren, ändern Sie die Sprachen-ID von `@language=N'R'` zu `@language = N'Python'` und nehmen die notwendigen Änderungen im `@script`-Argument vor. Alle anderen Parameter funktionieren genauso wie bei R.

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Erstellen Sie ein Python-Modell und Generieren von Bewertungen aus

Dieses Beispiel veranschaulicht, wie Sie „sp\_execute\_external\_script“ verwenden, um Bewertungen in einem einfachen Python-Modell zu generieren. 

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

-- Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders'

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

# Get data from input query
customer_data = my_input_data

# Define the model
n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

In Python-Code verwendete Spaltenüberschriften werden nicht an SQL Server ausgegeben; geben Sie daher mit der WITH RESULTS-Anweisung die Spaltennamen und Datentypen an, die SQL verwenden soll.

Zur Bewertung können Sie auch die native [PREDICT](../../t-sql/queries/predict-transact-sql.md)-Funktion verwenden, die in der Regel schneller ist, weil sie die Python- bzw. R-Laufzeit nicht aufrufen muss.

## <a name="see-also"></a>Siehe auch

 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Python-Bibliotheken und Datentypen](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [R-Bibliotheken und R-Datentypen](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
 [Bekannte Probleme bei SQL Server-Machine Learning-Dienste](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
 [CREATE EXTERNAL LIBRARY &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Externe Skripts aktiviert – Serverkonfigurationsoption](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server, Externes Skript-Objekt](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
