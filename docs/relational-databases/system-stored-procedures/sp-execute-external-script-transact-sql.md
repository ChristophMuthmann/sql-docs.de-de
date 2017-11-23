---
title: Sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs: TSQL
helpviewer_keywords: sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d437e6e8d86aa648d9c6ef11a8ca04297cafbaf3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spexecuteexternalscript-transact-sql"></a>Sp_execute_external_script (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Führt das Skript, das als Argument an einen externen Speicherort bereitgestellt. Das Skript muss in einer unterstützten und registrierten Sprache geschrieben werden. Die Abfragestruktur wird gesteuert, indem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Benutzer beliebige Vorgänge für die Abfrage ausführen können. Auszuführende **Sp_execute_external_script**, müssen Sie zunächst aktivieren externer Skripts, die mit der `sp_configure 'external scripts enabled', 1;` Anweisung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_execute_external_script   
    @language = N'language,   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]   
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```  
  
## <a name="arguments"></a>Argumente  
 @language= N'*Sprache*"  
 Gibt die Skriptsprache an. *Sprache* ist **Sysname**.  

 Gültige Werte sind `Python` oder `R`. 
  
 @script= N'*Skript*"  
 Externe sprachschrift Domänenmodells ein literal oder eine Variable angegeben. *Skript* ist **nvarchar(max)**.  
  
 [ @input_data_1_name = N'*input_data_1_name*"]  
 Gibt den Namen der Variablen, die zur Darstellung von definierten Abfrage @input_data_1. Der Datentyp der Variablen im externen Skript hängt von der Sprache ab. Im Falle von R wird die Eingabevariable einem Datenrahmen. Im Fall von Python muss die Eingabe tabellarische sein. *input_data_1_name* ist **Sysname**.  
  
 Standardwert ist "InputDataSet".  
  
 [ @input_data_1 = N'*input_data_1*"]  
 Gibt an, die Eingabedaten unter Verwendung des Skripts in Form von externen verwendet eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Abfrage. *input_data_1* ist **nvarchar(max)**.  
  
 [ @output_data_1_name = N'*output_data_1_name*"]  
 Gibt den Namen der Variablen in externen Skripts mit den Daten zu zurückzugebenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach Abschluss des Aufrufs der gespeicherten Prozedur. Der Datentyp der Variablen im externen Skript hängt von der Sprache ab. Im Fall von R muss die Ausgabe einem Datenrahmen. Im Fall von Python muss die Ausgabe einem Datenrahmen Pandas sein. *output_data_1_name* ist **Sysname**.  
  
 Standardwert ist "OutputDataSet".  
  
 [ @parallel = 0 | 1 ]  
 Aktivieren Sie die parallele Ausführung von R-Skripts durch Festlegen der `@parallel` -Parameter auf 1 fest. Der Standardwert für diesen Parameter ist 0 (keine Parallelität).  
  
 Für R-Skripts, die nicht mithilfe von RevoScaleR-Funktionen verwenden die `@parallel` Parameter kann für die Verarbeitung großer Datasets, vorausgesetzt, das Skript im Grunde parallelisiert werden kann nützlich sein. Beispielsweise, wenn von der R `predict` Funktion mit einem Modell, um neue Vorhersagen generieren, legen Sie `@parallel = 1` als Hinweis für das Abfragemodul. Wenn die Abfrage parallelisiert werden kann, werden Zeilen gemäß verteilt die **MAXDOP** Einstellung.  
  
 Wenn `@parallel = 1` und die Ausgabe wird direkt auf den Clientcomputer gestreamt wird und dann die `WITH RESULTS SETS` -Klausel ist erforderlich und einem Ausgabeschema muss angegeben werden.  
  
 Für R-Skripts, die RevoScaleR-Funktionen verwenden, paralleler Verarbeitung erfolgt automatisch und sollte nicht angegeben werden `@parallel = 1` auf die **Sp_execute_external_script** aufrufen.  
  
 [ @params = N' *@parameter_name Data_type* [OUT | Ausgabe] [,... ...n] "]  
 Eine Liste der Eingabeparameter-Deklarationen, die in der externen Skript verwendet werden.  
  
 [ @parameter1 = "*value1*' [| Ausgabe] [,... ...n]]  
 Eine Liste von Werten für die Eingabeparameter, die vom externen Skript verwendet werden soll.  


## <a name="remarks"></a>Hinweise  
 Führen Sie mit **sp_execute_external_script** Skripts aus, die in einer unterstützten Sprache wie beispielsweise R geschrieben wurden. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]besteht [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] aus einer Serverkomponente, die mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installiert wird, sowie Arbeitsstationstools und Verbindungsbibliotheken, der Datenanalysten mit der Hochleistungsumgebung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verbinden. Installieren von R Services (Datenbankintern) während der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup, um die Ausführung von R-Skripts ermöglichen. Weitere Informationen finden Sie unter [Einrichten von SQL Server R Services &#40; In-Database &#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
 Sie können die Ressourcen, die durch ein externes Skript verwendet werden, indem Sie einen externen Ressourcenpool konfigurieren steuern. Weitere Informationen finden Sie unter [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Informationen über die arbeitsauslastung können aus den Katalogsichten der Ressourcenkontrolle, die DMVS und die Leistungsindikatoren abgerufen werden. Weitere Informationen finden Sie unter [Katalogsichten der Ressourcenkontrolle &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Ressourcenkontrolle bezogene dynamische Verwaltungssichten &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md), und [SQLServer, externe Skripts Objekt](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

Monitor-skriptausführung mit [dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) und [dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

 Standardmäßig werden von dieser gespeicherten Prozedur zurückgegebenen Resultsets Ausgabe mit unbenannten Spalten. Spaltennamen, die in einem Skript verwendet gelten lokal in der skriptumgebung und werden nicht im ausgegebenen Resultset wiedergegeben. Verwenden Sie die Resultset-Spalten Name, der `WITH RESULTS SET` -Klausel der [ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md).
  
 Zusätzlich zum Zurückgeben eines Resultsets, können Sie Skalare Werte zurückgeben, von R-Skript [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit OUTPUT-Parametern. Das folgende Beispiel zeigt die Verwendung der OUTPUT-Parameter:  
  
```  
DECLARE @model varbinary(max);  
EXEC sp_execute_external_script  
        @language = N'R'  
        , @script = N'  
    # build classification model to predict tipped or not  
    logitObj <- glm(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource, family = binomial(link=logit));  
  
    # First, serialize a model and put it into a database table  
    modelbin <- serialize(logitObj, NULL);  
    '  
        , @input_data_1 = N'  
SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance  
  FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)  
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d  
'  
        , @input_data_1_name = N'featureDataSource'  
        , @params = N'@modelbin varbinary(max) OUTPUT'  
        , @modelbin = @model OUTPUT;  
```  


## <a name="streaming-execution-for-r-script"></a>Streaming-Ausführung für R-Skript  
 Streaming-Ausführung von R-Skript wird unterstützt durch Angabe `@r_rowsPerRead int parameter` in `@params` Auflistung.  Streaming ermöglicht das R-Skripts zum Arbeiten mit Daten, die nicht in den Arbeitsspeicher passt. Z. B. wenn es Milliarden Zeilen Bewertung mittels predict-Funktion den neuen `@r_rowsPerRead` Parameter verwendet werden, die Ausführung zu einem Datenstrom zu einem Zeitpunkt geteilt. Dieser Parameter steuert die Anzahl der Zeilen, die an die R-Prozesse gesendet werden können sie auch verwendet werden, für die Beschränkung der Anzahl der Zeilen, die gleichzeitig gelesen werden. Dies kann zu Problemen mit der serverleistung zu minimieren, wenn z. B. ein umfangreiches Modell trainiert wird ist hilfreich sein. Beachten Sie, dass dieser Parameter nur in Fällen verwendet werden kann, in dem die Ausgabe des R-Skript hängen nicht lesen, oder der gesamte Satz von Zeilen ansehen.  
  
 Sowohl die `@r_rowsPerRead` Parameter für das streaming und die `@parallel` Argument sollte Hinweise berücksichtigt werden. Für den Hinweis, angewendet werden soll muss es möglich, einen SQL-Abfrageplan zu generieren, der parallelen Verarbeitung enthält. Wenn dies nicht möglich ist, kann die paralleler Verarbeitung nicht aktiviert werden.  
  
> [!NOTE]  
>  Streaming und parallele Verarbeitung werden nur in Enterprise Edition unterstützt. Sie können die Parameter in Ihren Abfragen in der Standard Edition einschließen, ohne ein Fehler ausgelöst wird, jedoch Parameter haben keine Auswirkung und R-Skripts, die in einem einzelnen Prozess ausführen.  
  
## <a name="restrictions"></a>Einschränkungen  
 **Datentypen:** die folgenden Datentypen werden nicht unterstützt, bei der Verwendung in der Eingabeabfrage oder die Parameter des `sp_execute_external_script` Prozedur, und der Rückgabewert ein nicht unterstützter Typ-Fehler.  
  
 Dieses Problem zu umgehen **Umwandlung** die Spalte oder den Wert in einen unterstützten Typ in [!INCLUDE[tsql](../../includes/tsql-md.md)] und r an  
  
-   **Cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **"DateTimeOffset"**, **Zeit**  
  
-   **sql_variant**  
  
-   **Text**, **Bild**  
  
-   **xml**  
  
-   **Hierarchyid**, **Geometrie**, **Geography**  
  
-   Benutzerdefinierte CLR-Typen  
  
 **"DateTime"** Werte in der Eingabe auf der Seite "R" für Werte, die nicht den zulässigen Wertebereich in r passen, dies erforderlich, ist da, in NA konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht eine größere Anzahl von Werten als in der Sprache "R" unterstützt wird.  
  
 "Float"-Werte (z. B., + Inf -Inf, NaN) werden nicht unterstützt, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , obwohl beide Sprachen IEEE 754 verwenden. Aktuelle Verhalten sendet nur die Werte, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] direkt und als ein Ergebnis Sqlclient in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] löst Fehler aus. Diese Werte zu konvertieren, um **NULL**.  
  
 Alle R-Resultset, das zugeordnet werden kann, eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Datentyp, wird die Ausgabe als NULL.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **EXECUTE ANY EXTERNAL SCRIPT** -Datenbankberechtigung.  
  
## <a name="examples"></a>Beispiele  
 Dieser Abschnitt enthält Beispiele, wie diese gespeicherte Prozedur verwendet werden kann, zum Ausführen von R-Skripts, die mit [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
### <a name="a-return-a-data-set-from-r-to-sql-server"></a>A. Ein Dataset von R mit SQL Server zurück.  
 Das folgende Beispiel erstellt eine gespeicherte Prozedur, die verwendet **Sp_execute_external_script** zurückzugebenden Iris-Dataset von R zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
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
go  
```  
  
### <a name="b-generate-a-model-based-on-data-from-sql-server"></a>B. Generieren eines Modells, basierend auf Daten aus SQL Server  
 Das folgende Beispiel erstellt eine gespeicherte Prozedur, die verwendet **Sp_execute_external_script** ein Iris-Modell zu generieren und das Modell zurückgeben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Dieses Beispiel benötigen Sie das e1071-Paket wird installiert. Weitere Informationen finden Sie unter [Installieren zusätzlicher R-Paketen in SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).  
  
```  
DROP PROC IF EXISTS generate_iris_model;  
go  
  
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
go  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Python-Bibliotheken und Datentypen](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [R-Bibliotheken und R-Datentypen](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Bekannte Probleme bei SQL Server R Services](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [Erstellen Sie externe Bibliothek &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [Sp_prepare &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [externe Skripts aktiviert – Serverkonfigurationsoption](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server, Externes Skript-Objekt](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
  
