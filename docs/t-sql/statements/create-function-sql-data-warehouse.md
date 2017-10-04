---
title: CREATE-Funktion (SQL Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cad1b2c-5ea0-4001-9060-2f6832ccd057
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 55f1b7e612a1c7d120e06078b0fdba45d6409d36
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-function-sql-data-warehouse"></a>CREATE-Funktion (SQL Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Erstellt eine benutzerdefinierte Funktion in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Eine benutzerdefinierte Funktion ist ein [!INCLUDE[tsql](../../includes/tsql-md.md)] Routine, die Parameter annehmen, eine Aktion, z. B. eine komplexe Berechnung, und gibt das Ergebnis dieser Aktion als Wert zurück. Der Rückgabewert muss einen skalaren (Einzelwert). Verwenden Sie diese Anweisung zum Erstellen einer wiederverwendbaren Routine, die auf folgende Weise verwendet werden kann:  
  
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
  
 *Funktionsname*  
 Der Name der benutzerdefinierten Funktion. Funktionsnamen müssen den Regeln für Bezeichner entsprechen und innerhalb der Datenbank und für jedes Schema eindeutig sein.  
  
> [!NOTE]  
>  Auf den Funktionsnamen müssen Klammern folgen, selbst wenn kein Parameter angegeben ist.  
  
 @*Parametername*  
 Ein Parameter in der benutzerdefinierten Funktion. Ein oder mehrere Parameter können deklariert werden.  
  
 Eine Funktion kann maximal 2.100 Parameter haben. Der Benutzer muss beim Ausführen einer Funktion den Wert jedes deklarierten Parameters angeben (sofern kein Standardwert für den betreffenden Parameter definiert ist).  
  
 Geben Sie einen Parameternamen an, der mit dem Zeichen (@) beginnt. Der Parametername muss den Regeln für Bezeichner entsprechen. Parameter gelten lokal in der jeweiligen Funktion. Dieselben Parameternamen können in anderen Funktionen verwendet werden. Parameter können nur den Platz von Konstanten einnehmen. Sie können nicht anstelle von Tabellennamen, Spaltennamen oder Namen anderer Datenbankobjekte verwendet werden.  
  
> [!NOTE]  
>  ANSI_WARNINGS wird bei der Übergabe von Parametern in einer gespeicherten Prozedur oder in einer benutzerdefinierten Funktion oder beim Deklarieren und Festlegen von Variablen in einer Batchanweisung nicht berücksichtigt. Angenommen, eine Variable definiert ist, als **char(3)**, und klicken Sie dann auf einen Wert größer als 3 Zeichen festgelegt, die Daten auf die definierte Größe und die Einfügung abgeschnitten oder UPDATE-Anweisung erfolgreich ausgeführt wird.  
  
 *parameter_data_type*  
 Ist der Datentyp des Parameters an. Für [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, die alle skalaren Datentypen, die in unterstützt [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] sind zulässig. Der Datentyp Timestamp (Rowversion) ist kein unterstützter Typ.  
  
 [=*Standard* ]  
 Ein Standardwert für den Parameter. Wenn eine *Standardwert* Wert definiert ist, kann die Funktion ausgeführt werden, ohne einen Wert für diesen Parameter anzugeben.  
  
 Wenn ein Parameter der Funktion über einen Standardwert verfügt, muss beim Aufrufen der Funktion das DEFAULT-Schlüsselwort angegeben werden, um den Standardwert abzurufen. In diesem Punkt gibt es einen Unterschied zum Verwenden von Parametern in einer gespeicherten Prozedur. Fehlt im Aufruf einer gespeicherten Prozedur ein Parameter, der einen Standardwert hat, wird automatisch dieser Standardwert verwendet.  
  
 *return_data_type*  
 Der Rückgabewert einer benutzerdefinierten Skalarfunktion. Für [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, die alle skalaren Datentypen, die in unterstützt [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] sind zulässig. Der Datentyp Timestamp (Rowversion) ist kein unterstützter Typ. Der Cursor und die Tabelle nicht skalaren Typen sind nicht zulässig.  
  
 *function_body*  
 Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen.  Die Function_body keine SELECT-Anweisung enthalten und kann nicht auf Datenbankdaten verweisen.  Die Function_body kann nicht auf Tabellen oder Sichten verweisen. Hauptteil der Funktion kann andere deterministischen Funktionen aufrufen, jedoch nicht deterministische Funktionen aufrufen. 
  
 In Skalarfunktionen *Function_body* ist eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, die einen skalaren Wert ergeben.  
  
 *"scalar_expression"*  
 Gibt den skalaren Wert an, den die Skalarfunktion zurückgibt.  
  
 **\<Function_option >:: =** 
  
 Gibt an, dass die Funktion mindestens über eine der folgenden Optionen verfügen wird.  
  
 SCHEMABINDING  
 Gibt an, dass die Funktion an die Datenbankobjekte gebunden ist, auf die sie verweist. Wenn SCHEMABINDING angegeben ist, können an Basisobjekten keine Änderungen vorgenommen werden, die die Funktionsdefinition betreffen können. Zunächst muss die Funktionsdefinition selbst geändert oder gelöscht werden, um Abhängigkeiten in dem zu ändernden Objekt zu entfernen.  
  
 Die Bindung der Funktion an die Objekte, auf die sie verweist, wird nur bei einer der folgenden Aktionen entfernt:  
  
-   Die Funktion wird gelöscht.  
  
-   Die Funktion wird mithilfe der ALTER-Anweisung geändert, wobei die Option SCHEMABINDING nicht angegeben ist.  
  
 Eine Funktion kann nur dann schemagebunden sein, wenn die folgenden Bedingungen erfüllt sind:  
  
-   Alle benutzerdefinierten Funktionen, die von der Funktion verwiesen werden ebenfalls schemagebunden.  
  
-   Die Funktionen und andere benutzerdefinierte Funktionen, die von der Funktion verwiesen werden mit einem einteiligen oder zweiteiligen Namen verwiesen.  
  
-   Integrierte Funktionen und andere benutzerdefinierte Funktionen in der gleichen Datenbank können nur im Text der benutzerdefinierten Funktionen verwiesen werden.  
  
-   Der Benutzer, der die CREATE FUNCTION-Anweisung ausgeführt hat, besitzt REFERENCES-Berechtigungen für die Datenbankobjekte, auf die die Funktion verweist.  
  
 So entfernen Sie SCHEMABINDING verwenden ALTER  
  
 GIBT NULL ZURÜCK, AUF NULL INPUT | **FÜR NULL-EINGABE AUFGERUFEN**  
 Gibt an, die **OnNULLCall** Attribut des eine Skalarwertfunktion. Wenn das Attribut nicht angegeben ist, wird standardmäßig CALLED ON NULL INPUT verwendet. Dies bedeutet, dass der Hauptteil der Funktion ausgeführt wird, selbst wenn NULL als ein Argument übergeben wird.  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Wenn eine benutzerdefinierte Funktion nicht mit der SCHEMABINDING-Klausel erstellt wurde, können sich die an zugrunde liegenden Objekten vorgenommenen Änderungen auf die Definition der Funktion auswirken und bei Aufruf der Funktion zu unerwarteten Ergebnissen führen. Es wird empfohlen, eine der folgenden Methoden zu implementieren, damit die Funktion aufgrund von Änderungen an den zugrunde liegenden Objekten nicht veraltet ist:  
  
-   Geben Sie beim Erstellen der Funktion die WITH SCHEMABINDING-Klausel an. Hiermit wird sichergestellt, dass die Objekte, auf die in der Funktionsdefinition verwiesen wird, nicht geändert werden können, es sei denn, die Funktion wird auch geändert.  
  
## <a name="interoperability"></a>Interoperabilität  
 Die folgenden Anweisungen sind in einer Funktion zulässig:  
  
-   Zuweisungsanweisungen  
  
-   Anweisungen zur Ablaufsteuerung, mit Ausnahme von TRY...CATCH-Anweisungen  
  
-   Anweisungen zum Definieren lokaler Datenbankvariablen zu deklarieren.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Mit benutzerdefinierten Funktionen können keine Aktionen ausgeführt werden, die den Status einer Datenbank ändern.  
  
 Benutzerdefinierte Funktionen können geschachtelt werden. Dies bedeutet, dass eine benutzerdefinierte Funktion eine andere aufrufen kann. Die Schachtelungsebene wird um eins erhöht, wenn die aufgerufene Funktion mit der Ausführung beginnt, und wird wieder um eins erniedrigt, wenn die aufgerufene Funktion die Ausführung beendet. Benutzerdefinierte Funktionen unterstützen bis zu 32 geschachtelte Ebenen. Ein Überschreiten der maximalen Schachtelungsebenen verursacht das Fehlschlagen der gesamten Funktionsaufrufskette.   
  
## <a name="metadata"></a>Metadaten  
 Dieser Abschnitt enthält die systemkatalogsichten, die Sie verwenden können, um Metadaten zu benutzerdefinierten Funktionen zurückzugeben.  
  
 [Sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) : Zeigt die Definition der [!INCLUDE[tsql](../../includes/tsql-md.md)] von benutzerdefinierten Funktionen. Beispiel:  
  
```  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o   
    ON m.object_id = o.object_id   
    AND type = ('FN');  
GO  
  
```  
  
 [Sys.Parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) : Zeigt Informationen zu den in benutzerdefinierten Funktionen definierten Parametern.  
  
 [Sys. sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) : Zeigt die zugrunde liegenden Objekte, die auf eine Funktion verweist.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE FUNCTION-Berechtigung in der Datenbank und die ALTER-Berechtigung für das Schema, in dem die Funktion erstellt wird.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-a-scalar-valued-user-defined-function-to-change-a-data-type"></a>A. Verwenden eine skalarwertige benutzerdefinierte Funktion zum Ändern des Datentyps  
 Diese einfache Funktion nimmt eine **Int** Datentyp als Eingabe und gibt eine **dann decimal(10,2)** Datentyp als Ausgabe.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [ALTER FUNCTION (SQLServer PDW)](http://msdn.microsoft.com/en-us/25ff3798-eb54-4516-9973-d8f707a13f6c)   
 [DROP-Funktion (SQLServer PDW)](http://msdn.microsoft.com/en-us/1792a90d-0d06-4852-9dec-6de1b9cd229e)  
  
  



