---
title: CREATE FUNCTION (SQL Data Warehouse) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cad1b2c-5ea0-4001-9060-2f6832ccd057
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 1d57e08169e2d637a954546a8f2f1e728e8f67a5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-function-sql-data-warehouse"></a>CREATE FUNCTION (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Erstellt eine benutzerdefinierte Funktion in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Eine benutzerdefinierte Funktion ist eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Routine, die Parameter annimmt, eine Aktion ausführt (z.B. eine komplexe Berechnung) und das Ergebnis dieser Aktion als Wert zurückgeben kann. Der Rückgabewert muss ein Skalarwert (Einzelwert) sein. Verwenden Sie diese Anweisung zum Erstellen einer wiederverwendbaren Routine, die auf folgende Weise verwendet werden kann:  
  
-   In [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, wie z. B. SELECT  
  
-   In Anwendungen, die die Funktion aufrufen  
  
-   Bei der Definition einer anderen benutzerdefinierten Funktion  
  
-   Zum Definieren einer CHECK-Einschränkung für eine Spalte  
  
-   Zum Ersetzen einer gespeicherten Prozedur  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
--Transact-SQL Scalar Function Syntax  
CREATE FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]  
  
<function_option>::=   
{  
    [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
}  
  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name des Schemas, zu dem die benutzerdefinierte Funktion gehört.  
  
 *function_name*  
 Der Name der benutzerdefinierten Funktion. Funktionsnamen müssen den Regeln für Bezeichner entsprechen und innerhalb der Datenbank und für jedes Schema eindeutig sein.  
  
> [!NOTE]  
>  Auf den Funktionsnamen müssen Klammern folgen, selbst wenn kein Parameter angegeben ist.  
  
 @*parameter_name*  
 Ein Parameter in der benutzerdefinierten Funktion. Ein oder mehrere Parameter können deklariert werden.  
  
 Eine Funktion kann maximal 2.100 Parameter haben. Der Benutzer muss beim Ausführen einer Funktion den Wert jedes deklarierten Parameters angeben (sofern kein Standardwert für den betreffenden Parameter definiert ist).  
  
 Geben Sie einen Parameternamen an, der mit dem Zeichen (@) beginnt. Der Parametername muss den Regeln für Bezeichner entsprechen. Parameter gelten lokal in der jeweiligen Funktion. Dieselben Parameternamen können in anderen Funktionen verwendet werden. Parameter können nur den Platz von Konstanten einnehmen. Sie können nicht anstelle von Tabellennamen, Spaltennamen oder Namen anderer Datenbankobjekte verwendet werden.  
  
> [!NOTE]  
>  ANSI_WARNINGS wird bei der Übergabe von Parametern in einer gespeicherten Prozedur oder in einer benutzerdefinierten Funktion oder beim Deklarieren und Festlegen von Variablen in einer Batchanweisung nicht berücksichtigt. Wird beispielsweise eine Variable als **char(3)** definiert und dann auf einen Wert festgelegt, der länger als drei Zeichen ist, werden die Daten auf die definierte Größe abgeschnitten, und die Anweisung INSERT oder UPDATE wird erfolgreich ausgeführt.  
  
 *parameter_data_type*  
 Der Parameterdatentyp. Für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen sind alle skalaren Datentypen zulässig, die in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] unterstützt werden. Der Datentyp timestamp (rowversion) wird nicht unterstützt.  
  
 [ =*default* ]  
 Ein Standardwert für den Parameter. Wenn ein *default*-Wert definiert ist, kann die Funktion ausgeführt werden, ohne dass ein Wert für diesen Parameter angegeben werden muss.  
  
 Wenn ein Parameter der Funktion über einen Standardwert verfügt, muss beim Aufrufen der Funktion das DEFAULT-Schlüsselwort angegeben werden, um den Standardwert abzurufen. In diesem Punkt gibt es einen Unterschied zum Verwenden von Parametern in einer gespeicherten Prozedur. Fehlt im Aufruf einer gespeicherten Prozedur ein Parameter, der einen Standardwert hat, wird automatisch dieser Standardwert verwendet.  
  
 *return_data_type*  
 Der Rückgabewert einer benutzerdefinierten Skalarfunktion. Für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen sind alle skalaren Datentypen zulässig, die in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] unterstützt werden. Der Datentyp timestamp (rowversion) wird nicht unterstützt. Der Cursor und die Tabelle von nicht skalaren Typen sind nicht zulässig.  
  
 *function_body*  
 Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen.  function_body kann keine SELECT-Anweisung enthalten und kann nicht auf Datenbankdaten verweisen.  function_body kann nicht auf Tabellen oder Sichten verweisen. function_body kann andere deterministische Funktionen aufrufen, jedoch keine nicht deterministischen Funktionen aufrufen. 
  
 In Skalarfunktionen entspricht *function_body* einer Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die zusammen einen Skalarwert ergeben.  
  
 *scalar_expression*  
 Gibt den skalaren Wert an, den die Skalarfunktion zurückgibt.  
  
 **\<function_option>::=** 
  
 Gibt an, dass die Funktion mindestens über eine der folgenden Optionen verfügen wird.  
  
 SCHEMABINDING  
 Gibt an, dass die Funktion an die Datenbankobjekte gebunden ist, auf die sie verweist. Wenn SCHEMABINDING angegeben ist, können an Basisobjekten keine Änderungen vorgenommen werden, die die Funktionsdefinition betreffen können. Zunächst muss die Funktionsdefinition selbst geändert oder gelöscht werden, um Abhängigkeiten in dem zu ändernden Objekt zu entfernen.  
  
 Die Bindung der Funktion an die Objekte, auf die sie verweist, wird nur bei einer der folgenden Aktionen entfernt:  
  
-   Die Funktion wird gelöscht.  
  
-   Die Funktion wird mithilfe der ALTER-Anweisung geändert, wobei die Option SCHEMABINDING nicht angegeben ist.  
  
 Eine Funktion kann nur dann schemagebunden sein, wenn die folgenden Bedingungen erfüllt sind:  
  
-   Alle benutzerdefinierten Funktionen, auf die die Funktion verweist, sind ebenfalls schemagebunden.  
  
-   Auf die Funktionen und die anderen benutzerdefinierten Funktionen, auf die die Funktion verweist, wird unter Verwendung eines einteiligen oder zweiteiligen Namens verwiesen.  
  
-   Nur auf integrierte Funktionen und andere benutzerdefinierte Funktionen in der gleichen Datenbank kann im Text der benutzerdefinierten Funktionen verwiesen werden.  
  
-   Der Benutzer, der die CREATE FUNCTION-Anweisung ausgeführt hat, besitzt REFERENCES-Berechtigungen für die Datenbankobjekte, auf die die Funktion verweist.  
  
 Zum Entfernen von SCHEMABINDING verwenden Sie ALTER  
  
 RETURNS NULL ON NULL INPUT | **CALLED ON NULL INPUT**  
 Gibt das **OnNULLCall**-Attribut einer Skalarwertfunktion an. Wenn das Attribut nicht angegeben ist, wird standardmäßig CALLED ON NULL INPUT verwendet. Dies bedeutet, dass der Hauptteil der Funktion ausgeführt wird, selbst wenn NULL als ein Argument übergeben wird.  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Wenn eine benutzerdefinierte Funktion nicht mit der SCHEMABINDING-Klausel erstellt wurde, können sich die an zugrunde liegenden Objekten vorgenommenen Änderungen auf die Definition der Funktion auswirken und bei Aufruf der Funktion zu unerwarteten Ergebnissen führen. Es wird empfohlen, eine der folgenden Methoden zu implementieren, damit die Funktion aufgrund von Änderungen an den zugrunde liegenden Objekten nicht veraltet ist:  
  
-   Geben Sie beim Erstellen der Funktion die WITH SCHEMABINDING-Klausel an. Hiermit wird sichergestellt, dass die Objekte, auf die in der Funktionsdefinition verwiesen wird, nicht geändert werden können, es sei denn, die Funktion wird auch geändert.  
  
## <a name="interoperability"></a>Interoperabilität  
 Die folgenden Anweisungen sind in einer Funktion zulässig:  
  
-   Zuweisungsanweisungen  
  
-   Anweisungen zur Ablaufsteuerung, mit Ausnahme von TRY...CATCH-Anweisungen  
  
-   DECLARE-Anweisungen zum Definieren lokaler Datenbankvariablen.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Mit benutzerdefinierten Funktionen können keine Aktionen ausgeführt werden, die den Status einer Datenbank ändern.  
  
 Benutzerdefinierte Funktionen können geschachtelt werden. Dies bedeutet, dass eine benutzerdefinierte Funktion eine andere aufrufen kann. Die Schachtelungsebene wird um eins erhöht, wenn die aufgerufene Funktion mit der Ausführung beginnt, und wird wieder um eins erniedrigt, wenn die aufgerufene Funktion die Ausführung beendet. Benutzerdefinierte Funktionen unterstützen bis zu 32 geschachtelte Ebenen. Ein Überschreiten der maximalen Schachtelungsebenen verursacht das Fehlschlagen der gesamten Funktionsaufrufskette.   
  
## <a name="metadata"></a>Metadaten  
 In diesem Abschnitt werden die Systemkatalogsichten aufgelistet, die Sie verwenden können, um Metadaten zu benutzerdefinierten Funktionen zurückzugeben.  
  
 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md): Zeigt die Definition von [!INCLUDE[tsql](../../includes/tsql-md.md)] benutzerdefinierten Funktionen an. Zum Beispiel:  
  
```  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o   
    ON m.object_id = o.object_id   
    AND type = ('FN');  
GO  
  
```  
  
 [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md): Zeigt Informationen zu den Parametern an, die in benutzerdefinierten Funktionen definiert sind.  
  
 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md): Zeigt die zugrunde liegenden Objekte an, auf die eine Funktion verweist.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE FUNCTION-Berechtigung in der Datenbank und die ALTER-Berechtigung für das Schema, in dem die Funktion erstellt wird.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="a-using-a-scalar-valued-user-defined-function-to-change-a-data-type"></a>A. Verwenden einer benutzerdefinierten Skalarwertfunktion zum Ändern eines Datentyps  
 Diese einfache Funktion verwendet einen **int**-Datentyp als Eingabe und gibt einen **decimal(10,2)**-Datentyp als Ausgabe zurück.  
  
```  
CREATE FUNCTION dbo.ConvertInput (@MyValueIn int)  
RETURNS decimal(10,2)  
AS  
BEGIN  
    DECLARE @MyValueOut int;  
    SET @MyValueOut= CAST( @MyValueIn AS decimal(10,2));  
    RETURN(@MyValueOut);  
END;  
GO  
  
SELECT dbo.ConvertInput(15) AS 'ConvertedValue';  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER FUNCTION (SQL Server PDW)](http://msdn.microsoft.com/en-us/25ff3798-eb54-4516-9973-d8f707a13f6c)   
 [DROP FUNCTION (SQL Server PDW)](http://msdn.microsoft.com/en-us/1792a90d-0d06-4852-9dec-6de1b9cd229e)  
  
  


