---
title: "Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OPENJSON"
  - "JSON, Importieren"
  - "Importieren von JSON"
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Die Rowsetfunktion **OPENJSON** ermöglicht es Ihnen, JSON-Text in eine Reihe von Zeilen und Spalten zu konvertieren. Sie können **OPENJSON** verwenden, um SQL-Abfragen auf JSON-Sammlungen auszuführen oder JSON-Text in SQL Server-Tabellen zu importieren.  
  
> [!NOTE] Die **OPENJSON**-Funktion steht nur für den **Kompatibilitätsgrad 130** zur Verfügung. Wenn der Kompatibilitätsgrad Ihrer Datenbank kleiner als 130 ist, kann SQL Server die **OPENJSON**-Funktion nicht finden und ausführen. Andere JSON-Funktionen sind für alle Kompatibilitätsgrade verfügbar. Sie können den Kompatibilitätsgrad in der Sicht „sys.databases“ oder in den Datenbankeigenschaften überprüfen.
> 
>   Sie können den Kompatibilitätsgrad der Datenbank mithilfe des folgenden Befehls ändern:   
>   ALTER DATABASE Datenbankname SET COMPATIBILITY_LEVEL = 130  
  
 Die **OPENJSON**-Funktion greift ein einzelnes JSON-Objekt oder eine Sammlung von JSON-Objekten auf und transformiert sie in eine oder mehrere Zeilen. In der Standardeinstellung gibt die **OPENJSON**-Funktion alle Schlüssel-Wert-Paare zurück, die sich auf der ersten Ebene des JSON-Objekts befinden, oder alle Elemente in JSON-Arrays mit ihren Indizes.  
  
 Sie können ein Zeilenschema angeben, das mithilfe der WITH-Klausel von der **OPENJSON**-Funktion zurückgegeben wird. Dieses explizite Schema definiert die Struktur der Ausgabe.  
  
## Verwenden von OPENJSON ohne Ergebnisschema

Nachstehend finden Sie ein kurzes Beispiel, das **OPENJSON** mit dem Standardschema verwendet und eine Zeile für jede Eigenschaft des JSON-Objekts zurückgibt.  
 
Wenn Sie die **OPENJSON**-Funktion ohne das angegebene Ergebnisschema verwenden (z.B. ohne WITH-Klausel nach OPENJSON), gibt die Funktion eine Tabelle mit drei Spalten zurück: Name der Eigenschaft im Eingabeobjekt (oder Index des Elements im Eingabearray), Wert der Eigenschaft oder des Arrayelements und Typ (z.B. Zeichenfolge, Zahl, boolescher Wert, Feld oder Objekt). Eigenschaften des JSON-Objekts (oder die Elemente des Arrays) werden in separaten Zeilen zurückgegeben.  

-   Weitere Informationen und Beispiele finden Sie unter [Use OPENJSON with the Default Schema &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md) (Verwenden von OPENJSON mit dem Standardschema &#40;SQL Server&#41;).
-   Weitere Informationen zu Syntax und Verwendung finden Sie unter [OPENJSON-Klausel &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md). 

```tsql  
SET @json = '{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';  
  
SELECT *  
FROM OPENJSON(@json);  
```  
  
**Ergebnisse**  
  
|Schlüssel|value|Typ|  
|---------|-----------|----------|  
|name|John|1|  
|surname|Doe|1|  
|age|45|2|  
|skills|["SQL","C#","MVC"]|4|
    
## Verwenden von OPENJSON mit einem expliziten Schema

Hier finden Sie ein kurzes Beispiel, in dem **OPENJSON** mit einem explizit angegebenen Schema verwendet wird.  
  
Wenn Sie in der WITH-Klausel der **OPENJSON**-Funktion ein Schema aus zurückgegebenen Ergebnissen angeben, gibt die Funktion eine Tabelle mit den Spalten zurück, die Sie in der WITH-Klausel definieren. In der WITH-Klausel können Sie einen Satz von Ausgabespalten, deren Typen und die Pfade der JSON-Quelleigenschaften für jeden Ausgabewert angeben. **OPENJSON** wird das Array von JSON-Objekten durchlaufen, Werte auf dem angegebenen Pfad für jede Spalte lesen und in einen angegebenen Typ konvertieren.  

-   Weitere Informationen und Beispiele finden Sie unter [Use OPENJSON with an Explicit Schema &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md) (Verwenden von OPENJSON mit einem expliziten Schema &#40;SQL Server&#41;).
-   Weitere Informationen zu Syntax und Verwendung finden Sie unter [OPENJSON-Klausel &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).
  
```tsql  
SET @json =   
 N'[  
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
  
SELECT * FROM  
OPENJSON ( @json )  
WITH (   
             Number   varchar(200) '$.Order.Number' ,  
             Date     datetime     '$.Order.Date',  
             Customer varchar(200) '$.AccountNumber',  
             Quantity int          '$.Item.Quantity'  
)  
```  
  
**Ergebnisse**  
  
|Number|Datum|Customer|Quantity|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
 Diese Funktion gibt die Elemente eines JSON-Arrays zurück und formatiert diese.  
  
-   Für jedes Element im JSON-Array generiert **OPENJSON** eine neue Zeile in der Ausgabetabelle. Zwei Elemente im JSON-Array werden in zwei Zeilen in der zurückgegebenen Tabelle konvertiert.  
  
-   Für jede Spalte, die mithilfe der Syntax `colName type json_path` angegeben wurde, konvertiert die **OPENJSON**-Funktion den Wert, der im Arrayelement im angegebenen Pfad gefunden wurde, in einen angegebenen Typ und füllt eine Zelle in der Ausgabetabelle auf. In diesem Beispiel werden Werte für die Datumsspalte aus jedem Objekt im Pfad `$.Order.Date` aufgegriffen und in datetime-Werte konvertiert.  
  
Sobald Sie die JSON-Sammlung in ein Rowset transformiert haben, können Sie jede beliebige SQL-Abfrage auf zurückgegebene Daten ausführen oder diese in eine Tabelle einfügen.  
  
## Erfahren Sie mehr über OPENJSON und integrierte JSON-Unterstützung in SQL Server  
 [Blogeinträge von Jovan Popovic, Program Manager bei Microsoft](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## Siehe auch  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  