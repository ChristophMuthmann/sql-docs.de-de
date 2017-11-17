---
title: OPENJSON (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENJSON
- OPENJSON_TSQL
helpviewer_keywords:
- OPENJSON rowset function
- JSON, importing
- JSON, converting from
ms.assetid: 233d0877-046b-4dcc-b5da-adeb22f78531
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 27eeb54d6493bb200e56caada1238d6fafb5b339
ms.contentlocale: de-de
ms.lasthandoff: 10/11/2017

---
# <a name="openjson-transact-sql"></a>OPENJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**OPENJSON** ist eine Tabellenwertfunktion, die JSON-Text analysiert, und gibt Objekte und Eigenschaften aus der JSON-Eingabe als Zeilen und Spalten zurück. Das heißt, **OPENJSON** stellt eine Rowsetsicht eines JSON-Dokuments bereit. Sie können die Spalten explizit in das Rowset und die JSON-eigenschaftspfade zum Auffüllen der Spalten angeben. Da **OPENJSON** einen Satz von Zeilen zurückgibt, können Sie **OPENJSON** in der `FROM` -Klausel eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung ebenso wie Sie jede Tabelle, Sicht oder Funktion mit Tabellenrückgabe verwenden können.  
  
Verwendung **OPENJSON** zum Importieren von JSON-Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], oder zum Konvertieren von JSON-Daten in ein relationales Format für eine app oder dem Dienst nicht nutzen, JSON direkt.  
  
> [!NOTE]  
>  Die **OPENJSON** -Funktion ist verfügbar nur für Kompatibilitätsgrad 130 oder höher. Wenn der Kompatibilitätsgrad Ihrer Datenbank kleiner als 130 ist, kann SQL Server die **OPENJSON**-Funktion nicht finden und ausführen. Andere JSON-Funktionen sind für alle Kompatibilitätsgrade verfügbar.
> 
> Sie können den Kompatibilitätsgrad in der `sys.databases`-Ansicht oder in den Datenbankeigenschaften überprüfen. Sie können den Kompatibilitätsgrad einer Datenbank mithilfe des folgenden Befehls ändern:  
> 
> `ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130`
>   
> Kompatibilitätsgrad 120 kann die Standardeinstellung auch in eine neue Azure SQL-Datenbank sein.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol")[Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
OPENJSON( jsonExpression [ , path ] )  [ <with_clause> ]

<with_clause> ::= WITH ( { colName type [ column_path ] [ AS JSON ] } [ ,...n ] )
```  

Die **OPENJSON** Tabellenwert-Funktion analysiert die *JsonExpression* bereitgestellt, die als erstes Argument und gibt eine oder mehrere Zeilen mit Daten aus der JSON-Objekten im Ausdruck zurück. *JsonExpression* geschachtelte untergeordnete Objekte enthalten kann. Wenn Sie innerhalb ein untergeordneten Objekts analysieren möchten *JsonExpression*, können Sie angeben, eine **Pfad** -Parameter für das JSON-Unterobjekt.

### <a name="openjson"></a>openjson

![Syntax für OPENJSON TVF](../../relational-databases/json/media/openjson-syntax.png "OPENJSON-Syntax")  

Wird standardmäßig die **OPENJSON** Funktion mit Tabellenrückgabe gibt drei Spalten, die den Schlüsselnamen, den Wert enthalten, und der Typ jedes Paars {Key: Value} finden Sie in *JsonExpression*. Als Alternative können Sie explizit festlegbaren Schemaset des Ergebnisses, das **OPENJSON** gibt zurück, durch die Bereitstellung *With_clause*.
  
### <a name="withclause"></a>with_clause
  
![Syntax für WITH-Klausel in der OPENJSON TVF](../../relational-databases/json/media/openjson-shema-syntax.png "OPENJSON WITH-Syntax")

*With_clause* enthält eine Liste von Spalten, bei deren Typen für **OPENJSON** zurückgegeben. Standardmäßig **OPENJSON** entspricht der Schlüssel im *JsonExpression* mit den Spaltennamen in *With_clause* (in diesem Fall Übereinstimmungen Schlüssel setzt voraus, dass sie die Groß-/Kleinschreibung beachtet wird). Wenn ein Spaltenname ein Schlüsselname nicht übereinstimmt, können Sie eine optionale bereitstellen *Column_path*, also eine [JSON Path-Ausdruck](../../relational-databases/json/json-path-expressions-sql-server.md) , die auf einer Taste innerhalb der *JsonExpression*. 

## <a name="arguments"></a>Argumente  
### <a name="jsonexpression"></a>*jsonExpression*  
Ein Unicode-Zeichen-Ausdruck, der JSON-Text enthält.  
  
OPENJSON führt eine Iteration durch die Elemente eines Arrays oder die Eigenschaften des Objekts in der JSON-Ausdruck und gibt eine Zeile für jedes Element oder eine Eigenschaft. Das folgende Beispiel gibt jede Eigenschaft des Objekts als *JsonExpression*:  
  
```sql  
DECLARE @json NVARCHAR(4000) = N'{  
   "StringValue":"John",  
   "IntValue":45,  
   "TrueValue":true,  
   "FalseValue":false,  
   "NullValue":null,  
   "ArrayValue":["a","r","r","a","y"],  
   "ObjectValue":{"obj":"ect"}  
}'

SELECT *
FROM OPENJSON(@json)
```  
  
**Ergebnisse**  
  
|Schlüssel|value|Typ|  
|---------|-----------|----------|  
|StringValue|John|1|  
|IntValue|45|2|  
|trueValue|true|3|  
|falseValue|false|3|  
|nullValue|NULL|0|  
|ArrayValue-Objekts|["a", "R", "R", "a","y"]|4|  
|ObjectValue|{"Obj": "ect"}|5|  

### <a name="path"></a>*Pfad*  
Ist ein optionaler JSON-Pfad-Ausdruck, der verweist auf ein Objekt oder ein Array in *JsonExpression*. **OPENJSON** sucht in der JSON-Text an der angegebenen Position und nur die referenzierte Fragment analysiert. Weitere Informationen finden Sie unter [JSON-Pfadausdrücke &#40; SQLServer &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).

In [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], Sie können eine Variable bereitstellen, als Wert des *Pfad*.
  
Das folgende Beispiel gibt ein geschachteltes Objekt durch Angabe der *Pfad*:  

```sql  
DECLARE @json NVARCHAR(4000) = N'{  
      "path": {  
            "to":{  
                 "sub-object":["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]  
                 }  
              }  
 }';

SELECT [key], value
FROM OPENJSON(@json,'$.path.to."sub-object"')
```  
  
 **Ergebnisse**  
  
|Key|Wert|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
 
Wenn **OPENJSON** analysiert eine JSON-Array, die Funktion gibt die Indizes der Elemente im JSON-Text als Schlüssel.

Entsprechend pfadschritte mit den Eigenschaften des JSON-Ausdrucks verwendete beim Vergleich wird die Groß-/Kleinschreibung und Sortierung nicht bewusst (d. h. eine BIN2-Vergleich). 

### <a name="withclause"></a>*with_clause*
Explizit definiert das Ausgabeschema für die **OPENJSON** -Funktion zurückgibt. Das optionale *With_clause* kann die folgenden Elemente enthalten:

*ColName* ist der Name für die Ausgabespalte.  
  
Standardmäßig **OPENJSON** verwendet, den Namen der Spalte um eine Eigenschaft im JSON-Text entsprechen. Wenn Sie die Spalte angeben, z. B. *Namen* im Schema OPENJSON versucht, diese Spalte mit der Eigenschaft "Name" im JSON-Text zu füllen. Sie können diese standardzuordnung überschreiben, indem die *Column_path* Argument.  
  
*type*  
Ist der Datentyp für die Ausgabespalte.  

> [!NOTE]
> Wenn Sie auch verwenden, die **AS JSON** option, die Spalte *Typ* muss `NVARCHAR(MAX)`.
  
*column_path*  
Ist der JSON-Pfad, der angibt, die Eigenschaft in der angegebenen Spalte zurückgeben. Weitere Informationen finden Sie unter der Beschreibung der *Pfad* Parameter weiter oben in diesem Thema.  
  
Verwendung *Column_path* Zuordnungsregeln an Standardeinstellung zu überschreiben, wenn der Name einer Ausgabespalte nicht mit den Namen der Eigenschaft übereinstimmt.  
  
Entsprechend pfadschritte mit den Eigenschaften des JSON-Ausdrucks verwendete beim Vergleich wird die Groß-/Kleinschreibung und Sortierung nicht bewusst (d. h. eine BIN2-Vergleich).  
  
Weitere Informationen zu Pfaden finden Sie unter [JSON-Pfadausdrücke &#40; SQLServer &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
*ALS JSON*  
Verwenden der **AS JSON** Option in einer Spaltendefinition, um anzugeben, dass die referenzierte Eigenschaft eine innere JSON-Objekt oder Array enthält. Bei Angabe der **AS JSON** Option, den Typ der Spalte muss NVARCHAR(MAX) sein.

-   Wenn Sie keinen **AS JSON** für eine Spalte, die Funktion gibt einen Skalarwert zurück (z. B. Int, String, "true", "false") aus der angegebenen JSON-Eigenschaft für den angegebenen Pfad. Wenn Sie den Pfad darstellt, ein Objekt oder ein Array, und die Eigenschaft kann nicht unter dem angegebenen Pfad nicht gefunden werden, wird die Funktion gibt null im lax Modus oder im strict-Modus einen Fehler zurück. Dieses Verhalten ist vergleichbar mit dem Verhalten von der **JSON_VALUE** Funktion.  
  
-   Bei Angabe von **AS JSON** für eine Spalte, gibt die Funktion ein JSON-Fragment aus der angegebenen JSON-Eigenschaft für den angegebenen Pfad. Wenn der Pfad einen skalaren Wert stellt und die Eigenschaft kann nicht unter dem angegebenen Pfad nicht gefunden werden, wird die Funktion gibt null im lax-Modus oder im strict-Modus einen Fehler zurück. Dieses Verhalten ist vergleichbar mit dem Verhalten von der **JSON_QUERY** Funktion.  
  
> [!NOTE]  
> Wenn es sich bei einer geschachtelten JSON-Fragment aus einer JSON-Eigenschaft zurückgegeben werden sollen, müssen Sie angeben der **AS JSON** Flag. Ohne diese Option, wenn die Eigenschaft nicht gefunden werden kann, OPENJSON gibt einen NULL-Wert nicht in der JSON-Objekt verwiesen wird oder ein Array zurück, oder sie gibt einen Laufzeitfehler im strict-Modus.  
  
Beispielsweise wird die folgende Abfrage gibt und die Elemente eines Arrays formatiert:  
  
```sql  
DECLARE @json NVARCHAR(MAX) = N'[  
  {  
    "Order": {  
      "Number":"SO43659",  
      "Date":"2011-05-31T00:00:00"  
    },  
    "AccountNumber":"AW29825",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":1  
    }  
  },  
  {  
    "Order": {  
      "Number":"SO43661",  
      "Date":"2011-06-01T00:00:00"  
    },  
    "AccountNumber":"AW73565",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":3  
    }  
  }
]'  
   
SELECT *
FROM OPENJSON ( @json )  
WITH (   
              Number   varchar(200)   '$.Order.Number',  
              Date     datetime       '$.Order.Date',  
              Customer varchar(200)   '$.AccountNumber',  
              Quantity int            '$.Item.Quantity',  
              [Order]  nvarchar(MAX)  AS JSON  
 )
```  
  
**Ergebnisse**  
  
|Number|Datum|Customer|Quantity|Order|  
|------------|----------|--------------|--------------|-----------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|{"Number": "SO43659", "Date": "2011-05-31T00:00:00"}|  
|SO43661|2011-06-01T00:00:00|AW73565|3|{"Number": "SO43661", "Date": "2011-06-01T00:00:00"}|  
  

## <a name="return-value"></a>Rückgabewert  
Die Spalten, die OPENJSON-Funktion zurückgibt, hängen von der WITH-Option ab.  
  
1. Beim Aufruf von OPENJSON mit Standardschema - bei einem expliziten Schema nicht in der WITH-Klausel - Angabe zurückgegeben, also die Funktion eine Tabelle mit den folgenden Spalten:  
    1.  **Schlüssel**. Ein nvarchar(4000)-Wert, der den Namen der angegebenen Eigenschaft oder der Index des Elements im angegebenen Array enthält. Die Schlüsselspalte verfügt über eine BIN2-Sortierung.  
    2.  **Wert**. Ein nvarchar(max)-Wert, der den Wert der Eigenschaft enthält. Die Wertspalte erbt seine Sortierung aus *JsonExpression*.
    3.  **Typ**. Int-Wert, der den Typ des Werts enthält. Die **Typ** Spalte wird nur zurückgegeben, wenn Sie mithilfe von OPENJSON mit dem Standardschema. Die Type-Spalte verfügt über einen der folgenden Werte:  
  
        |Wert der Type-Spalte|JSON-Datentyp|  
        |------------------------------|--------------------|  
        |0|NULL|  
        |1|Zeichenfolge|  
        |2|int|  
        |3|"true" / "false"|  
        |4|array|  
        |5|Objekt (object)|  
  
     Nur werden die Eigenschaften der ersten Ebene zurückgegeben. Die Anweisung schlägt fehl, wenn der JSON-Text nicht ordnungsgemäß formatiert ist.  

2. Wenn Sie die OPENJSON aufrufen, und einem expliziten Schema in der WITH-Klausel angeben, gibt die Funktion eine Tabelle mit dem Schema, das Sie in der WITH-Klausel definiert.  

## <a name="remarks"></a>Hinweise  

*Json_path* in das zweite Argument der verwendeten **OPENJSON** oder im *With_clause* können beginnen Sie mit der **lax** oder **strenge** Schlüsselwort.

-   In **lax** Modus **OPENJSON** nicht, wird ein Fehler ausgelöst, wenn das Objekt oder der Wert für den angegebenen Pfad nicht gefunden werden kann. Wenn der Pfad nicht gefunden werden kann, **OPENJSON** gibt ein leeres Resultset oder ein NULL-Wert zurück.
-   In **strenge**, Modus **OPENJSON** gibt einen Fehler zurück, wenn der Pfad nicht gefunden werden kann.

Einige der Beispiele auf dieser Seite Geben Sie explizit des Path-Modus weniger strenge oder strict. Der Path-Modus ist optional. Wenn Sie einen Path-Modus nicht explizit angeben, ist der lax Modus die Standardeinstellung. Weitere Informationen zur Path-Modus und Path-Ausdrücken finden Sie unter [JSON-Pfadausdrücke &#40; SQLServer &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).    

Spaltennamen *With_clause* mit Schlüssel im JSON-Text verglichen. Wenn Sie den Spaltennamen angeben `[Address.Country]`, er wird mit dem Schlüssel verglichen `Address.Country`. Wenn Sie einen geschachtelten Schlüssel verweisen möchten `Country` innerhalb des Objekts `Address`, müssen Sie den Pfad angeben `$.Address.Country` in Spalte Pfad.

*Json_path* Schlüssel mit alphanumerischen Zeichen enthalten kann. Die Schlüsselnamen in Escapezeichen *Json_path* in doppelte Anführungszeichen, wenn Sie Sonderzeichen in den Schlüssel verfügen. Beispielsweise `$."my key $1".regularKey."key with . dot"` Übereinstimmungen Wert 1 in den folgenden JSON-Text:

```json
{
  "my key $1": {
    "regularKey":{
      "key with . dot": 1
    }
  }
}
```  

## <a name="examples"></a>Beispiele  
  
### <a name="example-1---convert-a-json-array-to-a-temporary-table"></a>Beispiel 1: Konvertieren einer JSON-Array in eine temporäre Tabelle  
Das folgende Beispiel enthält eine Liste von Bezeichnern als JSON-Array der Zahlen. Die Abfrage konvertiert JSON-Array in eine Tabelle von Bezeichnern und alle Produkte mit den angegebenen Ids filtert.  
  
```sql  
DECLARE @pSearchOptions NVARCHAR(4000) = N'[1,2,3,4]'

SELECT *
FROM products
INNER JOIN OPENJSON(@pSearchOptions) AS productTypes
 ON product.productTypeID = productTypes.value
```  
  
Diese Abfrage ist im folgenden Beispiel entspricht. Im folgenden Beispiel müssen Sie jedoch, Einbetten von Zahlen in der Abfrage, anstatt sie als Parameter übergeben werden.  
  
```sql  
SELECT *
FROM products
WHERE product.productTypeID IN (1,2,3,4)
```  
  
### <a name="example-2---merge-properties-from-two-json-objects"></a>Beispiel 2: Merge-Eigenschaften von zwei JSON-Objekten  
Das folgende Beispiel wählt eine Vereinigung aller Eigenschaften von zwei JSON-Objekten. Die beiden Objekte verfügen, ein Duplikat *Namen* Eigenschaft. Im Beispiel wird der Schlüssel-Wert verwendet, um die doppelte Zeile aus den Ergebnissen auszuschließen.  
  
```sql  
DECLARE @json1 NVARCHAR(MAX),@json2 NVARCHAR(MAX)

SET @json1=N'{"name": "John", "surname":"Doe"}'

SET @json2=N'{"name": "John", "age":45}'

SELECT *
FROM OPENJSON(@json1)
UNION ALL
SELECT *
FROM OPENJSON(@json2)
WHERE [key] NOT IN (SELECT [key] FROM OPENJSON(@json1))
```  
  
### <a name="example-3---join-rows-with-json-data-stored-in-table-cells-using-cross-apply"></a>Beispiel 3: Join Zeilen mit JSON-Daten gespeichert werden, in Tabellenzellen, die mithilfe des CROSS APPLY  
Im folgenden Beispiel die `SalesOrderHeader` Tabelle besitzt eine `SalesReason` Textspalte, ein Array von enthält `SalesOrderReasons` im JSON-Format. Die `SalesOrderReasons` Objekte enthalten Eigenschaften, z. B. *Qualität* und *Hersteller*. Das Beispiel erstellt einen Bericht, der jede Zeile der Bestellung und die zugehörigen Verkaufsgründe verknüpft. Die OPENJSON-Operator wird das JSON-Array von Verkaufsgründe erweitert, als wären die Gründe in einer separaten untergeordneten Tabelle gespeichert wurden. CROSS APPLY-Operator verknüpft jede Zeile der Bestellung dann an die von der OPENJSON-Tabellenwertfunktion zurückgegebenen Zeilen.  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
> [!TIP] 
> Wenn Sie keine erweitern in der Regel JSON-Arrays in den einzelnen Feldern gespeichert, und verknüpfen Sie sie mit ihren übergeordneten Zeilen, die [!INCLUDE[tsql](../../includes/tsql-md.md)] CROSS APPLY-Operator. Weitere Informationen über den CROSS APPLY, finden Sie unter [FROM &#40; Transact-SQL &#41; ](../../t-sql/queries/from-transact-sql.md).  
  
Dieselbe Abfrage kann umgeschrieben werden, mithilfe von `OPENJSON` mit einem explizit definierten Schema der zurückzugebenden Zeilen:  
  
```sql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
     CROSS APPLY OPENJSON (SalesReasons) WITH (value nvarchar(100) '$')
```  
  
In diesem Beispiel wird die `$` Pfad verweist auf jedes Element im Array. Wenn den zurückgegebenen Wert explizit umgewandelt werden sollen, können Sie diese Art der Abfrage verwenden.  
  
### <a name="example-4---combine-relational-rows-and-json-elements-with-cross-apply"></a>Beispiel 4: kombinieren relationale Zeilen und JSON-Elemente mit CROSS APPLY  
Die folgende Abfrage kombiniert relationalen Zeilen und JSON-Elemente, zu der in der folgenden Tabelle dargestellten Ergebnisse.  
  
```sql  
SELECT store.title, location.street, location.lat, location.long  
FROM store  
CROSS APPLY OPENJSON(store.jsonCol, 'lax $.location')   
     WITH (street varchar(500) ,  postcode  varchar(500) '$.postcode' ,  
     lon int '$.geo.longitude', lat int '$.geo.latitude')  
     AS location
```  
  
**Ergebnisse**  
  
|title|street|Postleitzahl|LON|LAT|  
|-----------|------------|--------------|---------|---------|  
|Gesamte Nahrungsmittel Märkte|17991 Redmond-Methode|WA 98052, USA|47.666124|-122.10155|  
|Sears|148th Ave NE|WA 98052, USA|47.63024|-122.141246,17|  
  
### <a name="example-5---import-json-data-into-sql-server"></a>Beispiel 5 – Importieren von JSON-Daten in SQL Server  
Im folgenden Beispiel wird ein komplettes JSON-Objekt in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle geladen.  
  
```sql  
DECLARE @json NVARCHAR(max)  = N'{  
  "id" : 2,  
  "firstName": "John",  
  "lastName": "Smith",  
  "isAlive": true,  
  "age": 25,  
  "dateOfBirth": "2015-03-25T12:00:00",  
  "spouse": null  
  }';  
   
  INSERT INTO Person  
  SELECT *   
  FROM OPENJSON(@json)  
  WITH (id int,  
        firstName nvarchar(50), lastName nvarchar(50),   
        isAlive bit, age int,  
        dateOfBirth datetime2, spouse nvarchar(50)
```  
  
## <a name="see-also"></a>Siehe auch  
 [JSON-Pfadausdrücke &#40; SQLServer &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON &#40; SQLServer &#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)   
 [Verwenden von OPENJSON mit Standardschema &#40; SQLServer &#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)   
 [Verwenden von OPENJSON mit einem expliziten Schema &#40; SQLServer &#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)  
  
  

