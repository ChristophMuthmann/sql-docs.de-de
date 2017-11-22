---
title: JSON_MODIFY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 96bc8255-a037-4907-aec4-1a9c30814651
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0c4f5c0f65e6f7ae8b532cb42d117fa49fc83b00
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
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
 Ein Ausdruck. In der Regel der Name einer Variablen oder eine Spalte, die JSON-Text enthält.  
  
 **JSON_MODIFY** gibt einen Fehler zurück, wenn *Ausdruck* kein gültiges JSON enthält.  
  
 *Pfad*  
 Ein JSON-Path-Ausdruck, der die zu aktualisierende Eigenschaft angibt.

 *Pfad* hat die folgende Syntax:  
  
 `[append] [ lax | strict ] $.<json path>`  
  
-   *Anfügen*  
    Optionaler Modifizierer, der angibt, dass der neue Wert für das Array verweist angefügt werden sollen  *\<Json-Pfad >*.  
  
-   *lax*  
    Gibt an, dass die Eigenschaft verweist  *\<Json-Pfad >* noch nicht existieren. Wenn die Eigenschaft nicht vorhanden ist, versucht JSON_MODIFY ab, den neuen Wert für den angegebenen Pfad einfügen. Einfügung kann fehlschlagen, wenn die Eigenschaft auf den Pfad kann nicht eingefügt werden. Wenn Sie keinen *lax* oder *strenge*, *lax* ist der Standardmodus.  
  
-   *Strict*  
    Gibt an, dass die Eigenschaft verweist  *\<Json-Pfad >* muss in der JSON-Ausdruck sein. Wenn die Eigenschaft nicht vorhanden ist, wird von JSON_MODIFY ein Fehler zurückgegeben.  
  
-   *\<JSON-Pfad >*  
    Gibt den Pfad für die Eigenschaft zu aktualisieren. Weitere Informationen finden Sie unter [JSON-Pfadausdrücke &#40; SQLServer &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
In [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], Sie können eine Variable bereitstellen, als Wert des *Pfad*.

**JSON_MODIFY** gibt einen Fehler zurück, wenn das Format der *Pfad* ist ungültig.  
  
 *newValue*  
 Der neue Wert für die Eigenschaft, die vom angegebenen *Pfad*.  
  
 Im Modus "lax" löscht JSON_MODIFY den angegebenen Schlüssel aus, wenn der neue Wert NULL ist.  
  
JSON_MODIFY schützt alle Sonderzeichen in den neuen Wert an, wenn der Typ des Werts vom Typ NVARCHAR oder VARCHAR ist. Ein Textwert ist nicht mit Escapezeichen versehen wird jedoch ordnungsgemäß formatierte JSON durch FOR JSON, JSON_QUERY oder JSON_MODIFY erzeugt.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt zurück, den aktualisierten Wert des *Ausdruck* als ordnungsgemäß formatierte JSON-Text.  
  
## <a name="remarks"></a>Hinweise  
 Die JSON_MODIFY-Funktion können Sie den Wert einer vorhandenen Eigenschaft aktualisieren, fügen Sie ein neues Schlüssel-Wert-Paar oder Löschen eines Schlüssels basierend auf einer Kombination von Modi und stellen Werte zur Verfügung.  
  
 Die folgende Tabelle vergleicht das Verhalten des **JSON_MODIFY** im lax Modus und im strict-Modus. Weitere Informationen zu den optionalen Modus Pfadangabe ("lax" oder "strict"), finden Sie unter [JSON-Pfadausdrücke &#40; SQLServer &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Vorhandener Wert|Pfad vorhanden ist.|Lax-Modus|Strict-Modus|  
|--------------------|-----------------|--------------|-----------------|  
|NOT NULL|ja|Aktualisieren Sie den vorhandenen Wert.|Aktualisieren Sie den vorhandenen Wert.|  
|NOT NULL|Nein|Versucht, ein neues Schlüssel-Wert-Paar für den angegebenen Pfad erstellen.<br /><br /> Dies kann fehlschlagen. Angenommen, wenn Sie den Pfad angeben `$.user.setting.theme`, JSON_MODIFY nicht den Schlüssel ein `theme` Wenn die `$.user` oder `$.user.settings` Objekte sind nicht vorhanden, oder wenn Einstellungen ist ein Array oder einen skalaren Wert.|Fehler – INVALID_PROPERTY|  
|NULL|ja|Löschen Sie die vorhandene Eigenschaft.|Den vorhandenen Wert auf null festgelegt.|  
|NULL|Nein|Keine Aktion. Das erste Argument als Ergebnis zurückgegeben.|Fehler – INVALID_PROPERTY|  
  
 Im Modus "lax" JSON_MODIFY versucht, ein neues Schlüssel-Wert-Paar zu erstellen, aber in einigen Fällen möglicherweise fehl.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="example---basic-operations"></a>Beispiel: grundlegende Vorgänge  
 Das folgende Beispiel zeigt die grundlegenden Vorgänge, die mit JSON-Text ausgeführt werden können.  
  
 **Abfrage**  
  
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
  
### <a name="example---multiple-updates"></a>Beispiel – mehrere updates  
 Mit JSON_MODIFY können Sie nur eine Eigenschaft aktualisieren. Wenn Sie mehrere Updates ausführen müssen, können Sie mehrere Aufrufe von JSON_MODIFY verwenden.  
  
 **Abfrage**  
  
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
  
### <a name="example---rename-a-key"></a>Beispiel: Umbenennen eines Schlüssels  
 Im folgenden Beispiel wird die Vorgehensweise beim Umbenennen einer Eigenschaft in JSON-Text mit der JSON_MODIFY-Funktion. Zunächst können Sie den Wert einer vorhandenen Eigenschaft annehmen und fügen Sie ihn als neuen Schlüssel-Wert-Paar. Anschließend können Sie den alten Schlüssel löschen, indem der Wert der alten Eigenschaft auf NULL festlegen.  
  
 **Abfrage**  
  
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
  
 Wenn den neuen Wert in einen numerischen Typ nicht umgewandelt wird, wird JSON_MODIFY wird als Text behandelt und in doppelte Anführungszeichen umgeben.  
  
### <a name="example---increment-a-value"></a>Beispiel - Inkrement ein-Wert  
 Im folgende Beispiel zeigt, wie sich den Wert einer Eigenschaft in JSON-Text mit der JSON_MODIFY-Funktion zu erhöhen. Sie können zunächst der Wert der vorhandenen Eigenschaft und fügen Sie ihn als neuen Schlüssel-Wert-Paar. Anschließend können Sie den alten Schlüssel löschen, indem der Wert der alten Eigenschaft auf NULL festlegen.  
  
 **Abfrage**  
  
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
  
### <a name="example---modify-a-json-object"></a>Beispiel: Ändern von JSON-Objekt  
 JSON_MODIFY behandelt die *NewValue* Argument als nur-Text auch wenn darin ordnungsgemäß formatierte JSON-Text. Daher die JSON-Ausgabe der Funktion ist in doppelte Anführungszeichen eingeschlossen, und alle Sonderzeichen werden mit Escapezeichen versehen, wie im folgenden Beispiel gezeigt.  
  
 **Abfrage**  
  
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
  
 Geben Sie zum Vermeiden der automatischen Schutz *NewValue* mithilfe der JSON_QUERY-Funktion. JSON_MODIFY weiß, dass der Wert von JSON_MODIFY zurückgegebenen ordnungsgemäß formatierte JSON, damit es den Wert mit Escapezeichen versehen nicht.  
  
 **Abfrage**  
  
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
 Das folgende Beispiel aktualisiert den Wert einer Eigenschaft in einer Tabellenspalte, die JSON enthält.  
  
```sql  
UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,"$.info.address.town",'London')
WHERE EmployeeID=17
 
```  
  
## <a name="see-also"></a>Siehe auch  
 [JSON-Pfadausdrücke &#40; SQLServer &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON-Daten &#40; SQLServer &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
