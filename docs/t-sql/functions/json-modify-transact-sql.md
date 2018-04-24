---
title: JSON_MODIFY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 96bc8255-a037-4907-aec4-1a9c30814651
caps.latest.revision: 16
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1a0e15872ca8e161a75b2506b098ede4dd324cf3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="jsonmodify-transact-sql"></a>JSON_MODIFY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Aktualisiert den Wert einer Eigenschaft in einer JSON-Zeichenfolge und gibt die aktualisierte JSON-Zeichenfolge zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
JSON_MODIFY ( expression , path , newValue )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein Ausdruck. In der Regel der Name einer Variablen oder einer Spalte, die JSON-Text enthält.  
  
 **JSON_MODIFY** gibt einen Fehler zurück, wenn *expression* keinen gültigen JSON-Text enthält.  
  
 *path*  
 Ein JSON-Pfadausdruck, der die zu aktualisierende Eigenschaft angibt.

 *path* verfügt über die folgende Syntax:  
  
 `[append] [ lax | strict ] $.<json path>`  
  
-   *append*  
    Optionaler Modifizierer, der angibt, dass der neue Wert an das Array angefügt werden sollte, auf das der *\<json path>* verweist.  
  
-   *lax*  
    Gibt an, dass die Eigenschaft, auf die der *\<json path>* verweist, nicht existieren muss. Wenn die Eigenschaft nicht vorhanden ist, versucht JSON_MODIFY, den neuen Wert für den angegebenen Pfad einzufügen. Dies kann fehlschlagen, wenn die Eigenschaft nicht in den Pfad eingefügt werden kann. Wenn Sie weder *lax* noch *strict* angeben, ist der Standardmodus *lax*.  
  
-   *strict*  
    Gibt an, dass die Eigenschaft, auf die *\<json path>* verweist, im JSON-Ausdruck enthalten sein muss. Wenn die Eigenschaft nicht vorhanden ist, gibt JSON_MODIFY einen Fehler zurück.  
  
-   *\<json path>*  
    Gibt den Pfad für die zu aktualisierende Eigenschaft an. Weitere Informationen finden Sie unter [JSON-Pfadausdrücke &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
In [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] können Sie eine Variable als Wert von *path* bereitstellen.

**JSON_MODIFY** gibt einen Fehler zurück, wenn das Format von *path* ungültig ist.  
  
 *newValue*  
 Der neue Wert für die von *path* angegebene Eigenschaft.  
  
 Im Lax-Modus löscht JSON_MODIFY den angegebenen Schlüssel, wenn der neue Wert NULL ist.  
  
JSON_MODIFY versieht alle Sonderzeichen im neuen Wert mit Escapezeichen, wenn der Typ des Werts NVARCHAR oder VARCHAR ist. Ein Textwert wird nicht mit Escapezeichen versehen, wenn es ein ordnungsgemäß formatierter JSON ist, der von FOR JSON, JSON_QUERY oder JSON_MODIFY erzeugt wurde.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt den aktualisierten Wert von *expression* als ordnungsgemäß formatierten JSON-Text zurück.  
  
## <a name="remarks"></a>Remarks  
 Mit der JSON_MODIFY-Funktion können Sie den Wert einer vorhandenen Eigenschaft aktualisieren, ein neues Schlüssel-Wert-Paar einfügen oder einen Schlüssel löschen, der auf einer Kombination von Modi und bereitgestellten Werten basiert.  
  
 Die folgende Tabelle vergleicht das Verhalten von **JSON_MODIFY** im Lax-Modus und im Strict-Modus. Weitere Informationen zu den optionalen Path-Modusangaben (Lax oder Strict) finden Sie unter [JSON Path Expressions &#40;SQL Server&#41; (JSON-Pfadausdrücke (SQL Server))](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Vorhandener Wert|Pfad ist vorhanden|Lax-Modus|Strict-Modus|  
|--------------------|-----------------|--------------|-----------------|  
|Nicht NULL|ja|Vorhandenen Wert aktualisieren.|Vorhandenen Wert aktualisieren.|  
|Nicht NULL|nein|Versucht, ein neues Schlüssel-Wert-Paar für den angegebenen Pfad zu erstellen.<br /><br /> Dies kann fehlschlagen. Wenn Sie beispielsweise den Pfad `$.user.setting.theme` angeben, fügt JSON_MODIFY den Schlüssel `theme` nicht ein, wenn die `$.user`- oder `$.user.settings`-Objekte nicht vorhanden sind, oder wenn Einstellungen ein Array oder ein Skalarwert sind.|Fehler – INVALID_PROPERTY|  
|NULL|ja|Löscht die vorhandene Eigenschaft.|Legt den vorhandenen Wert auf NULL fest.|  
|NULL|nein|Keine Aktion. Das erste Argument wird als Ergebnis zurückgegeben.|Fehler – INVALID_PROPERTY|  
  
 Im Lax-Modus versucht JSON_MODIFY, ein neues Schlüssel-Wert-Paar zu erstellen, aber in einigen Fällen schlägt dies möglicherweise fehl.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="example---basic-operations"></a>Beispiel: Grundlegende Vorgänge  
 Das folgende Beispiel zeigt die grundlegenden Vorgänge, die mit JSON-Text ausgeführt werden können.  
  
 **Dataseteigenschaften**  
  
```sql  

DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update name  

SET @info=JSON_MODIFY(@info,'$.name','Mike')

PRINT @info

-- Insert surname  

SET @info=JSON_MODIFY(@info,'$.surname','Smith')

PRINT @info

-- Delete name  

SET @info=JSON_MODIFY(@info,'$.name',NULL)

PRINT @info

-- Add skill  

SET @info=JSON_MODIFY(@info,'append $.skills','Azure')

PRINT @info
```  
  
 **Ergebnisse**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---multiple-updates"></a>Beispiel: Mehrere Updates  
 Mit JSON_MODIFY können Sie nur eine Eigenschaft aktualisieren. Wenn Sie mehrere Updates ausführen müssen, können Sie mehrere Aufrufe von JSON_MODIFY verwenden.  
  
 **Dataseteigenschaften**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Multiple updates  

SET @info=JSON_MODIFY(JSON_MODIFY(JSON_MODIFY(@info,'$.name','Mike'),'$.surname','Smith'),'append $.skills','Azure')

PRINT @info
```  
  
 **Ergebnisse**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---rename-a-key"></a>Beispiel: Einen Schlüssel umbenennen  
 Im folgenden Beispiel wird die Vorgehensweise beim Umbenennen einer Eigenschaft in JSON-Text mit der JSON_MODIFY-Funktion gezeigt. Zunächst können Sie den Wert einer vorhandenen Eigenschaft annehmen. Fügen Sie ihn als neues Schlüssel-Wert-Paar ein. Anschließend können Sie den alten Schlüssel löschen, indem Sie den Wert der alten Eigenschaft auf NULL festlegen.  
  
 **Dataseteigenschaften**  
  
```sql  
DECLARE @product NVARCHAR(100)='{"price":49.99}'

PRINT @product

-- Rename property  

SET @product=
 JSON_MODIFY(
  JSON_MODIFY(@product,'$.Price',CAST(JSON_VALUE(@product,'$.price') AS NUMERIC(4,2))),
  '$.price',
  NULL
 )

PRINT @product
```  
  
 **Ergebnisse**  
  
```json  
{
    "price": 49.99
} {
    "Price": 49.99
}
```  
  
 Wenn der neue Wert nicht in einen numerischen Typ umgewandelt wird, behandelt JSON_MODIFY ihn als Text und umgibt ihn mit doppelten Anführungszeichen.  
  
### <a name="example---increment-a-value"></a>Beispiel: Einen Wert erhöhen  
 Im folgenden Beispiel wird die Vorgehensweise beim Erhöhen eines Eigenschaftswerts in JSON-Text mit der JSON_MODIFY-Funktion gezeigt. Zunächst können Sie den Wert der vorhandenen Eigenschaft annehmen. Fügen Sie ihn als neues Schlüssel-Wert-Paar ein. Anschließend können Sie den alten Schlüssel löschen, indem Sie den Wert der alten Eigenschaft auf NULL festlegen.  
  
 **Dataseteigenschaften**  
  
```sql  
DECLARE @stats NVARCHAR(100)='{"click_count": 173}'

PRINT @stats

-- Increment value  

SET @stats=JSON_MODIFY(@stats,'$.click_count',
 CAST(JSON_VALUE(@stats,'$.click_count') AS INT)+1)

PRINT @stats
```  
  
 **Ergebnisse**  
  
```json  
{
    "click_count": 173
} {
    "click_count": 174
}
```  
  
### <a name="example---modify-a-json-object"></a>Beispiel: Ändern eines JSON-Objekts  
 JSON_MODIFY behandelt das *newValue*-Argument als Nur-Text, auch wenn ordnungsgemäß formatierter JSON-Text enthalten ist. Daher ist die JSON-Ausgabe der Funktion von doppelten Anführungszeichen eingeschlossen. Alle Sonderzeichen werden mit Escapezeichen versehen, wie im folgenden Beispiel gezeigt.  
  
 **Dataseteigenschaften**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array

SET @info=JSON_MODIFY(@info,'$.skills','["C#","T-SQL","Azure"]')

PRINT @info
```  
  
 **Ergebnisse**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": "["C#","T-SQL","Azure"]"
}
```  
  
 Geben Sie zum Vermeiden der automatischen Escapezeichen *newValue* mithilfe der JSON_QUERY-Funktion an. JSON_MODIFY weiß, dass der von JSON_MODIFY zurückgegebene Wert ein ordnungsgemäß formatierter JSON ist, damit der Wert nicht mit einem Escapezeichen versehen wird.  
  
 **Dataseteigenschaften**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array  

SET @info=JSON_MODIFY(@info,'$.skills',JSON_QUERY('["C#","T-SQL","Azure"]'))

PRINT @info
```  
  
 **Ergebnisse**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": ["C#", "T-SQL", "Azure"]
}
```  
  
### <a name="example---update-a-json-column"></a>Beispiel: Aktualisieren einer JSON-Spalte  
 Im folgenden Beispiel wird der Wert einer Eigenschaft in einer Tabellenspalte, die JSON enthält, aktualisiert.  
  
```sql  
UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,"$.info.address.town",'London')
WHERE EmployeeID=17
 
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [JSON-Pfadausdrücke &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON-Daten &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
