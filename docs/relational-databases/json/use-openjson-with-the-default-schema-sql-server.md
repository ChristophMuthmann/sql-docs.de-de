---
title: "Verwenden von OPENJSON mit dem Standardschema (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OPENJSON mit Standardschema"
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Verwenden von OPENJSON mit dem Standardschema (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Verwenden Sie **OPENJSON** mit dem Standardschema, um eine Tabelle mit einer Zeile für jede Eigenschaft des Objekts oder für jedes Element im Array zurückzugeben.  
  
 Hier ein paar Beispiele, in denen **OPENJSON** mit dem Standardschema verwendet wird. Weitere Informationen und Beispiele finden Sie unter [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## Beispiel: Rückgabe jeder Eigenschaft eines Objekts  
 **Abfrage**  
  
```tsql  
SELECT * FROM OPENJSON('{"name":"John","surname":"Doe","age":45}')  
```  
  
 **Ergebnisse**  
  
|Key|Wert|  
|---------|-----------|  
|name|John|  
|surname|Doe|  
|age|45|  
  
## Beispiel: Rückgabe jedes Element eines Arrays  
 **Abfrage**  
  
```tsql  
SELECT [key], value FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]')  
```  
  
 **Ergebnisse**  
  
|Key|Wert|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
  
## Beispiel: Konvertieren von JSON in eine temporäre Tabelle  
 Die folgende Abfrage gibt alle Eigenschaften des **info**-Objekts zurück.  
  
```tsql  
SET @json = N'{  
    "info":{    
      "type":1,  
      "address":{    
        "town":"Bristol",  
        "county":"Avon",  
        "country":"England"  
      },  
      "tags":["Sport", "Water polo"]  
   },  
   "type":"Basic"  
}'  
  
SELECT * FROM OPENJSON(@json, N'lax $.info')  
```  
  
 **Ergebnisse**  
  
|Key|Wert|Typ|  
|---------|-----------|----------|  
|Typ|1|0|  
|address|{ "town":"Bristol", "county":"Avon", "country":"England" }|5|  
|Transponder|[ "Sport", "Water polo" ]|4|  
  
## Beispiel: Kombinieren relationale Daten und JSON-Daten  
 Im folgenden Beispiel hat die SalesOrderHeader-Tabelle eine SalesReason-Textspalte, die ein Array von SalesOrderReasons im JSON-Format enthält. Die SalesOrderReasons-Objekte enthalten Eigenschaften, z. B. "Manufacturer" und "Quality". Das Beispiel erstellt einen Bericht, der jede Zeile der Bestellung und die zugehörigen Verkaufsgründe verknüpft, indem das JSON-Array von Verkaufsgründe erweitert wird, als wären die Gründe in einer separaten untergeordneten Tabelle gespeichert.  
  
```tsql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
    CROSS APPLY OPENJSON (SalesReasons)  
  
```  
  
 In diesem Beispiel gibt OPENJSON eine Tabelle mit Verkaufsgründen zurück, in denen die Gründe als Wertspalte angezeigt werden. Der CROSS APPLY-Operator verknüpft jede Verkaufszeile der Bestellung mit den von der OPENJSON-Tabellenwertfunktion zurückgegebenen Zeilen.  
  
## Siehe auch  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  