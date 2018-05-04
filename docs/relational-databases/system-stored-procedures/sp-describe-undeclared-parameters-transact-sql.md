---
title: Sp_describe_undeclared_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_undeclared_parameters
- sp_describe_undeclared_parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_undeclared_parameters
ms.assetid: 6f016da6-dfee-4228-8b0d-7cd8e7d5a354
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a455bfe51ac57408c075a20128054574b86962f8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdescribeundeclaredparameters-transact-sql"></a>sp_describe_undeclared_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt ein Resultset, das Metadaten zu nicht deklarierten Parametern in enthält eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Batch. Berücksichtigt jeden Parameter, der verwendet wird die **@tsql** batch, aber nicht im deklariert **@params**. Ein Resultset wird zurückgegeben, das für jeden dieser Parameter eine Zeile mit den abgeleiteten Typinformationen für diesen Parameter enthält. Die Prozedur gibt ein leeres Resultset, wenn die **@tsql** eingabebatch hat keine Parameter mit Ausnahme derjenigen, die in deklariert **@params**.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_describe_undeclared_parameters   
    [ @tsql = ] 'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' data type ] [, ...n]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@tsql =** ] **'***Transact-SQL_batch***'**  
 Eine oder mehrere [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen. *Transact-SQL_batch* möglicherweise **Nvarchar (***n***)** oder **nvarchar(max)**.  
  
 [  **@params =** ] **N'***Parameter***"**  
 @params Stellt eine deklarationszeichenfolge für Parameter für die [!INCLUDE[tsql](../../includes/tsql-md.md)] Batch, ähnlich wie mit der Funktionsweise von Sp_executesql funktioniert. *Parameter* möglicherweise **Nvarchar (***n***)** oder **nvarchar(max)**.  
  
 Eine Zeichenfolge, die die Definitionen aller Parameter enthält, die eingebetteten *Transact SQL_batch*. Die Zeichenfolge muss eine Unicode-Konstante oder eine Unicode-Variable sein. Jede Parameterdefinition besteht aus einem Parameternamen und einem Datentyp. Dabei ist n ein Platzhalter für zusätzlicher Parameterdefinitionen. Wenn die Transact-SQL-Anweisung oder den Batch in der Anweisung keine Parameter enthält @params ist nicht erforderlich. Der Standardwert für diesen Parameter ist NULL.  
  
 Datatype  
 Der Datentyp des Parameters.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **Sp_describe_undeclared_parameters** immer gibt den Rückgabestatus 0 bei Erfolg. Wenn die Prozedur löst einen Fehler aus, und die Prozedur als RPC aufgerufen wird, wird der Rückgabestatus mit Fehlertyp aufgefüllt, wie in der Error_type-Spalte der Sys. dm_exec_describe_first_result_set beschrieben. Wenn die Prozedur von [!INCLUDE[tsql](../../includes/tsql-md.md)] aufgerufen wird, ist der Rückgabewert immer 0, auch bei Fehlern.  
  
## <a name="result-sets"></a>Resultsets  
 **Sp_describe_undeclared_parameters** gibt das folgende Resultset zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**Int NOT NULL**|Enthält die Ordnungsposition des Parameters im Resultset. Die Position des ersten Parameters wird mit 1 angegeben.|  
|**name**|**Sysname NOT NULL**|Enthält den Namen des Parameters.|  
|**suggested_system_type_id**|**Int NOT NULL**|Enthält die **System_type_id** des Datentyps des Parameters als im angegebenen sys.types.<br /><br /> Bei CLR-Typen, obwohl die **System_type_name** Spalte gibt NULL zurück, die in dieser Spalte wird der Wert 240 zurückgegeben.|  
|**suggested_system_type_name**|**Nvarchar (256) NULL**|Enthält den Namen des Datentyps. Enthält für den Datentyp des Parameters angegebene Argumente (z. B. Länge, Genauigkeit, Skala). Wenn der Datentyp ein benutzerdefinierter Aliastyp ist, wird der zugrunde liegende Systemtyp hier angegeben. Wenn es sich um einen benutzerdefinierten CLR-Datentyp handelt, wird in dieser Spalte NULL zurückgegeben. Wenn der Typ des Parameters nicht abgeleitet werden kann, wird NULL zurückgegeben.|  
|**suggested_max_length**|**Smallint nicht NULL**|Finden Sie unter sys.columns. für **Max_length** spaltenbeschreibung.|  
|**suggested_precision**|**"tinyint" NOT NULL**|Finden Sie unter sys.columns. enthält eine Beschreibung der Genauigkeitsspalte.|  
|**suggested_scale**|**"tinyint" NOT NULL**|Finden Sie unter sys.columns. enthält eine Beschreibung der Skalierungsspalte.|  
|**suggested_user_type_id**|**Int NULL**|Enthält bei CLR- und Aliastypen die user_type_id des Datentyps der Spalte, wie in sys.types angegeben. Andernfalls NULL.|  
|**suggested_user_type_database**|**Sysname NULL**|Enthält bei CLR- und Aliastypen den Namen der Datenbank, in der der Typ definiert wurde. Andernfalls NULL.|  
|**suggested_user_type_schema**|**Sysname NULL**|Enthält bei CLR- und Aliastypen den Namen des Schemas, in dem der Typ definiert wurde. Andernfalls NULL.|  
|**suggested_user_type_name**|**Sysname NULL**|Enthält bei CLR- und Aliastypen den Namen des Typs. Andernfalls NULL.|  
|**suggested_assembly_qualified_type_name**|**Nvarchar (4000) NULL**|Bei CLR-Typen gibt den Namen der Assembly und Klasse, die den Typ definiert. Andernfalls NULL.|  
|**suggested_xml_collection_id**|**Int NULL**|Enthält die Xml_collection_id des Datentyps des Parameters, wie in sys.columns angegeben. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML Schema Collection zugeordnet ist.|  
|**suggested_xml_collection_database**|**Sysname NULL**|Enthält die Datenbank, in der die XML-Schemaauflistung definiert ist, die diesem Typ zugeordnet wurde. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML Schema Collection zugeordnet ist.|  
|**suggested_xml_collection_schema**|**Sysname NULL**|Enthält das Schema, in dem die XML-Schemaauflistung definiert ist, die diesem Typ zugeordnet wurde. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML Schema Collection zugeordnet ist.|  
|**suggested_xml_collection_name**|**Sysname NULL**|Enthält den Namen der XML-Schemaauflistung, die diesem Typ zugeordnet wurde. Diese Spalte gibt NULL zurück, wenn der zurückgegebene Typ keiner XML Schema Collection zugeordnet ist.|  
|**suggested_is_xml_document**|**Bit NOT NULL**|Gibt 1 zurück, wenn als Typ XML zurückgegeben wird und sichergestellt ist, dass es sich um ein XML-Dokument handelt. Andernfalls wird 0 zurückgegeben.|  
|**suggested_is_case_sensitive**|**Bit NOT NULL**|Gibt 1 zurück, wenn die Spalte von einem Zeichenfolgentyp ist, bei dem die Groß-/Kleinschreibung beachtet wird, andernfalls 0.|  
|**suggested_is_fixed_length_clr_type**|**Bit NOT NULL**|Gibt 1 zurück, wenn die Spalte von einem CLR-Typ mit fester Länge ist, andernfalls 0.|  
|**suggested_is_input**|**Bit NOT NULL**|Gibt 1 zurück, wenn der Parameter an anderer Stelle verwendet wird als links einer Zuweisung. Andernfalls wird 0 zurückgegeben.|  
|**suggested_is_output**|**Bit NOT NULL**|Gibt 1 zurück, wenn der Parameter auf der linken Seite einer Zuweisung verwendet wird oder an einen Ausgabeparameter einer gespeicherten Prozedur übergeben wird. Andernfalls wird 0 zurückgegeben.|  
|**formal_parameter_name**|**Sysname NULL**|Wenn es sich bei dem Parameter um ein Argument für eine gespeicherte Prozedur oder eine benutzerdefinierte Funktion handelt, wird der Name des entsprechenden formalen Parameters zurückgegeben. Andernfalls wird NULL zurückgegeben.|  
|**suggested_tds_type_id**|**Int NOT NULL**|Für die interne Verwendung.|  
|**suggested_tds_length**|**Int NOT NULL**|Für die interne Verwendung.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_describe_undeclared_parameters** immer gibt den Rückgabestatus 0 (null).  
  
 Die häufigste Verwendung besteht darin, dass für eine Anwendung eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung ausgeführt wird, die möglicherweise Parameter enthält und von dieser verarbeitet werden muss. Ein Beispiel ist eine Benutzeroberfläche (z. B. ODBCTest oder RowsetViewer), in denen der Benutzer eine Abfrage mit ODBC-Parametersyntax eingibt. Die Anwendung muss die Anzahl der Parameter dynamisch ermitteln und bei jedem den Benutzer auffordern.  
  
 Ein weiteres Beispiel liegt vor, wenn eine Anwendung ohne Benutzereingabe eine Schleife in den Parametern ausführen und die Daten für diese von einem anderen Speicherort (z. B. einer Tabelle) abrufen muss. In diesem Fall muss die Anwendung nicht alle Parameterinformationen zusammen übergeben. Stattdessen kann die Anwendung alle Parameterinformationen vom Anbieter und die Daten selbst aus der Tabelle abrufen. Code mit **Sp_describe_undeclared_parameters** mehr generisch ist und weniger wahrscheinlich geändert werden müssen, wenn die Datenstruktur später geändert wird.  
  
 **Sp_describe_undeclared_parameters** in den folgenden Fällen einen Fehler zurück.  
  
-   Wenn die Eingabe @tsql ist kein gültiger [!INCLUDE[tsql](../../includes/tsql-md.md)] Batch. Gültigkeit wird bestimmt durch Analysieren der [!INCLUDE[tsql](../../includes/tsql-md.md)] Batch. Alle Fehler, die durch den Batch verursacht während der abfrageoptimierung oder-Ausführung nicht berücksichtigt, wenn festlegen, ob die [!INCLUDE[tsql](../../includes/tsql-md.md)] Batch ist gültig.  
  
-   Wenn @params ist nicht NULL und enthält eine Zeichenfolge, die sich keine syntaktisch gültige deklarationszeichenfolge für Parameter, oder wenn es sich um eine Zeichenfolge enthält, deklariert einen Parameter mehr als einmal.  
  
-   Wenn die Eingabe [!INCLUDE[tsql](../../includes/tsql-md.md)] eingabebatch deklariert eine lokale Variable mit demselben Namen gemäß der Deklaration eines Parameters in @params.  
  
-   Die Anweisung erstellt temporäre Tabellen.  
  
 Wenn @tsql hat keine Parameter, als die im deklarierten @params, die Prozedur gibt ein leeres Resultset zurück.  
  
## <a name="parameter-selection-algorithm"></a>Algorithmus für die Parameterauswahl  
 Bei einer Abfrage mit nicht deklarierten Parametern erfolgt die Datentypableitung für nicht deklarierte Parameter in drei Schritten.  
  
 **Schritt 1**  
  
 Der erste Schritt der Datentypableitung für eine Abfrage mit nicht deklarierten Parametern besteht darin, die Datentypen aller Teilausdrücke zu ermitteln, deren Datentypen nicht von den nicht deklarierten Parametern abhängen. Der Typ kann für die folgenden Ausdrücke ermittelt werden:  
  
-   Spalten, Konstanten, Variablen und deklarierte Parameter.  
  
-   Ergebnisse eines Aufrufs einer benutzerdefinierten Funktion (User-Defined Function, UDF).  
  
-   Ein Ausdruck mit Datentypen, die nicht für alle Eingaben von den nicht deklarierten Parametern abhängen.  
  
 Betrachten Sie beispielsweise die folgende Abfrage: `SELECT dbo.tbl(@p1) + c1 FROM t1 WHERE c2 = @p2 + 2`. Die Ausdrücke dbo.tbl (@p1) + c1 und c2 haben Datentypen und Ausdruck @p1 und @p2 + 2 jedoch nicht.  
  
 Wenn nach diesem Schritt ein anderer Ausdruck als ein UDF-Aufruf über zwei Argumente ohne Datentypen verfügt, tritt bei der Typableitung ein Fehler auf. Beispielsweise führen alle folgenden Ausdrücke zu Fehlern:  
  
```  
SELECT * FROM t1 WHERE @p1 = @p2  
SELECT * FROM t1 WHERE c1 = @p1 + @p2  
SELECT * FROM t1 WHERE @p1 = SUBSTRING(@p2, 2, 3)  
```  
  
 Im folgenden Beispiel wird kein Fehler erzeugt:  
  
```  
SELECT * FROM t1 WHERE @p1 = dbo.tbl(c1, @p2, @p3)  
```  
  
 **Schritt 2**  
  
 Für einen bestimmten nicht deklarierten Parameter @p, der typableitungsalgorithmus sucht nach den innersten Ausdruck E (@p), enthält @p und ist eines der folgenden:  
  
-   Ein Argument für einen Vergleich oder ein Zuweisungsoperator.  
  
-   Ein Argument für eine benutzerdefinierte Funktion (einschließlich Tabellenwert-UDFs), Prozedur oder Methode.  
  
-   Ein Argument an einen **Werte** -Klausel eine **einfügen** Anweisung.  
  
-   Ein Argument an einen **Umwandlung** oder **konvertieren**.  
  
 Der typableitungsalgorithmus sucht nach den Zieldatentyp TT (@p) für "E" (@p). Für die vorherigen Beispiele sind die folgenden Zieldatentypen möglich:  
  
-   Der Datentyp der anderen Seite des Vergleichs oder der Zuweisung.  
  
-   Der deklarierte Datentyp des Parameters, an den dieses Argument übergeben wird.  
  
-   Der Datentyp der Spalte, in der dieser Wert eingefügt wird.  
  
-   Der Datentyp, in den die Anweisung umgewandelt oder konvertiert wird.  
  
 Betrachten Sie beispielsweise die folgende Abfrage: `SELECT * FROM t WHERE @p1 = dbo.tbl(@p2 + c1)`. Klicken Sie dann E (@p1) = @p1, E (@p2) = @p2 + c1, TT (@p1) ist der deklarierte Rückgabedatentyp von dbo.tbl und TT (@p2) ist der deklarierte Parameterdatentyp für dbo.tbl.  
  
 Wenn @p befindet sich nicht in einem beliebigen Ausdruck am Anfang des Schritts 2, ermittelt der typableitungsalgorithmus aufgelistet, E (@p) ist der größte Skalarausdruck, der enthält @p, und der typableitungsalgorithmus keine Berechnen Sie den Zieldatentyp TT (@p) für "E" (@p). Die Abfrage beispielsweise wählen `@p + 2` dann E (@p) = @p + 2, und es gibt keine TT (@p).  
  
 **Schritt 3**  
  
 Jetzt, E (@p) und TT (@p) werden identifiziert, leitet der typableitungsalgorithmus einen Datentyp für @p in einem der beiden folgenden Methoden:  
  
-   Einfache Ableitung  
  
     Wenn E (@p) = @p und TT (@p) vorhanden ist, d. h. wenn @p ist direkt ein Argument an einen der Ausdrücke aufgeführt, die am Anfang des in Schritt 2, und der typableitungsalgorithmus den Datentyp der leitet @p TT (sein.@p). Beispiel:  
  
    ```  
    SELECT * FROM t WHERE c1 = @p1 AND @p2 = dbo.tbl(@p3)  
    ```  
  
     Der Datentyp für @p1, @p2, und @p3 werden der Datentyp von c1, der Rückgabedatentyp von dbo.tbl und den Parameterdatentyp für dbo.tbl bzw.  
  
     Ein Sonderfall Wenn @p ist ein Argument an einen \<, >, \<= oder > =-Operator, einfache Ableitung Regeln nicht gelten. Der Typableitungsalgorithmus verwendet die allgemeinen, im nächsten Abschnitt erklärten Ableitungsregeln. Betrachten Sie beispielsweise die folgenden beiden Abfragen für Fälle, in denen c1 eine Spalte vom Datentyp char(30) ist:  
  
    ```  
    SELECT * FROM t WHERE c1 = @p  
    SELECT * FROM t WHERE c1 > @p  
    ```  
  
     Im ersten Fall leitet der typableitungsalgorithmus **char(30)** wie für den Datentyp @p gemäß den Regeln weiter oben in diesem Thema. Im zweiten Fall leitet der typableitungsalgorithmus **vom Datentyp varchar(8000)** gemäß der allgemeinen Ableitungsregeln im nächsten Abschnitt.  
  
-   Allgemeine Ableitung  
  
     Wenn keine einfache Ableitung möglich ist, kommen für nicht deklarierte Parameter die folgenden Datentypen infrage:  
  
    -   Integer-Datentypen (**Bit**, **"tinyint"**, **"smallint"**, **Int**, **"bigint"**)  
  
    -   Money-Datentypen (**Smallmoney**, **Money**)  
  
    -   Gleitkomma-Datentypen (**"float"**, **real**)  
  
    -   **Numeric (38, 19)** – andere numerische oder dezimale Datentypen werden nicht berücksichtigt.  
  
    -   **vom Datentyp varchar(8000)**, **varchar(max)**, **nvarchar(4000)**, und **nvarchar(max)** – andere string-Datentypen (z. B. **Text**, **char(8000)**, **nvarchar(30)** usw.) werden nicht berücksichtigt.  
  
    -   **varbinary(8000)** und **varbinary(max)** – andere binäre Datentypen werden nicht berücksichtigt (z. B. **Image**, **binary(8000)**, **Varbinary (30)** usw.).  
  
    -   **Datum**, **time(7)**, **Smalldatetime**, **"DateTime"**, **datetime2(7)**, **datetimeoffset(7)**  – Andere Daten- und Uhrzeittypen, z. B. **time(4)**, werden nicht berücksichtigt.  
  
    -   **sql_variant**  
  
    -   **xml**  
  
    -   Systemdefinierte CLR-Typen (**Hierarchyid**, **Geometrie**, **Geography**)  
  
    -   Benutzerdefinierte CLR-Typen  
  
### <a name="selection-criteria"></a>Auswahlkriterien  
 Von den infrage kommenden Datentypen wird jeder Datentyp abgelehnt, durch den die Abfrage ungültig gemacht würde. Von den verbleibenden infrage kommenden Datentypen wählt der Typableitungsalgorithmus anhand der folgenden Regeln einen aus.  
  
1.  Der Datentyp, der die kleinste Anzahl impliziter Konvertierungen in E erzeugt (@p) ausgewählt ist. Wenn ein bestimmter Datentyp einen Datentyp für "E" erzeugt (@p) unterscheidet sich vom TT (@p), der typableitungsalgorithmus betrachtet diese als zusätzliche implizite Konvertierung vom Datentyp des E (@p) in das TT (@p).  
  
     Beispiel:  
  
    ```  
    SELECT * FROM t WHERE Col_Int = Col_Int + @p  
    ```  
  
     In diesem Fall E (@p) ist Col_Int + @p und TT (@p) ist **Int**. **Int** ist für die ausgewählten @p , da es keine impliziten Konvertierungen erzeugt. Jeder andere ausgewählte Datentyp erzeugt mindestens eine implizite Konvertierung.  
  
2.  Wenn mehrere Datentypen gleich wenige Konvertierungen erzeugen, wird der Datentyp mit dem höheren Rang verwendet. Beispiel:  
  
    ```  
    SELECT * FROM t WHERE Col_Int = Col_smallint + @p  
    ```  
  
     In diesem Fall **Int** und **"smallint"** erzeugen eine Konvertierung. Jeder andere Datentyp erzeugt mehr als eine Konvertierung. Da **Int** hat Vorrang vor **"smallint"**, **Int** wird zum @p. Weitere Informationen zur Rangfolge von Datentypen finden Sie unter [Datentyppriorität &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
     Diese Regel gilt nur, wenn zwischen jedem Datentyp, der nach Regel 1 genauso wenige Konvertierungen wie ein anderer erzeugt, und dem Datentyp mit dem höchsten Rang eine implizite Konvertierung erfolgt. Wenn keine implizite Konvertierung erfolgt, tritt bei der Datentypableitung ein Fehler auf. In der Abfrage z. B. `SELECT @p FROM t`,-Datentyp Abzug schlägt fehl, da ein beliebiger für Datentyp @p gut wäre. Beispielsweise besteht keine implizite Konvertierung von **Int** auf **Xml**.  
  
3.  Wenn zwei ähnliche Datentypen unter Regel 1, z. B. tie **vom Datentyp varchar(8000)** und **varchar(max)**, wird der kleinere Datentyp (**vom Datentyp varchar(8000)**) ausgewählt ist. Das gleiche Prinzip gilt für **Nvarchar** und **Varbinary** Datentypen.  
  
4.  Für die Zwecke der Regel 1 bevorzugt der Typableitungsalgorithmus bestimmte Konvertierungen gegenüber anderen. Die Konvertierungen werden in der folgenden Reihenfolge bevorzugt (beste bis schlechteste):  
  
    1.  Konvertierung zwischen gleichem Basisdatentyp mit unterschiedlicher Länge.  
  
    2.  Konvertierung zwischen fester und variabler Länge, die Version der gleichen Datentypen (z. B. **Char** auf **Varchar**).  
  
    3.  Konvertierung zwischen **NULL** und **Int**.  
  
    4.  Jede andere Konvertierung.  
  
 Für die Abfrage beispielsweise `SELECT * FROM t WHERE [Col_varchar(30)] > @p`, **vom Datentyp varchar(8000)** ausgewählt, da die Konvertierung (a) am besten geeignet ist. Für die Abfrage `SELECT * FROM t WHERE [Col_char(30)] > @p`, **vom Datentyp varchar(8000)** wird immer noch ausgewählt werden, da er bewirkt, dass eine Konvertierung vom Typ (b) und eine andere Auswahl (z. B. **varchar(4000)**) würde dazu führen, dass eine Konvertierung vom Typ (d).  
  
 Als ein letztes Beispiel erhält eine Abfrage `SELECT NULL + @p`, **Int** ist für die ausgewählten @p da eine Konvertierung vom Typ (c) werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigung zum Ausführen der @tsql Argument.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden bestimmte Informationen zurückgegeben, z. B. der erwartete Datentyp für den nicht deklarierten `@id`-Parameter und den nicht deklarierten `@name`-Parameter.  
  
```  
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR name = @name'  
  
```  
  
 Wenn der `@id`-Parameter als `@params`-Verweis bereitgestellt wird, wird der `@id`-Parameter im Resultset ausgelassen, und nur der `@name`-Parameter wird beschrieben.  
  
```  
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR NAME = @name',  
@params = N'@id int'  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
  
  
