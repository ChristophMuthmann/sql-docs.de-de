---
title: Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON (SQL Server) | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 07/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 6e4a7b49bb01bd4254fad855daedd3981b2fa6a8
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="convert-json-data-to-rows-and-columns-with-openjson-sql-server"></a>Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Die Rowsetfunktion **OPENJSON** konvertiert JSON-Text in eine Reihe von Zeilen und Spalten. Nach der Transformation einer JSON-Sammlung in ein Rowset mithilfe von **OPENJSON** können Sie jede beliebige SQL-Abfrage auf zurückgegebene Daten ausführen oder diese in eine Tabelle von SQL Server einfügen. 
  
Die **OPENJSON**-Funktion greift ein einzelnes JSON-Objekt oder eine Sammlung von JSON-Objekten auf und transformiert sie in eine oder mehrere Zeilen. Die **OPENJSON**-Funktion gibt standardmäßig die folgenden Daten zurück:
-   Aus einem JSON-Objekt gibt die Funktion alle Schlüsselwertpaare zurück, die auf der ersten Ebene gefunden werden.
-   Aus einem JSON-Array gibt die Funktion alle Elemente des Arrays mit ihren Indizes zurück.  

Sie können eine optionale **WITH**-Klausel hinzufügen, um ein Schema bereitzustellen, das die Struktur der Ausgabe definiert.  
  
## <a name="option-1---openjson-with-the-default-output"></a>Option 1: OPENJSON mit der Standardausgabe
Bei Verwendung der **OPENJSON**-Funktion ohne ein explizites Schema für die Ergebnisse, d.h. ohne eine **WITH**-Klausel nach **OPENJSON**, gibt die Funktion eine Tabelle mit den folgenden drei Spalten zurück:
1.  Der **Name** der Eigenschaft im Eingabeobjekt (oder Index des Elements im Eingabe-Array)
2.  Der **Wert** der Eigenschaft oder des Array-Elements
3.  Der **Typ** (z.B. Zeichenfolge, Zahl, boolescher Wert, Array oder Objekt)

**OPENJSON** gibt jede Eigenschaft des JSON-Objekts oder jedes Element des Arrays als separate Zeile zurück  

Nachstehend finden Sie ein kurzes Beispiel, das **OPENJSON** mit dem Standardschema – also ohne die optionale **WITH**-Klausel – verwendet und eine Zeile für jede Eigenschaft des JSON-Objekts zurückgibt.  
 
**Beispiel**
```sql  
DECLARE @json NVARCHAR(MAX)

SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';

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

### <a name="more-info-about-openjson-with-the-default-schema"></a>Weitere Informationen zum Verwenden von OPENJSON mit dem Standardschema

Weitere Informationen und Beispiele finden Sie unter [Use OPENJSON with the Default Schema &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md) (Verwenden von OPENJSON mit dem Standardschema &#40;SQL Server&#41;).

Weitere Informationen zu Syntax und Verwendung finden Sie unter [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)zur Verfügung. 

    
## <a name="option-2---openjson-output-with-an-explicit-structure"></a>Option 2: OPENJSON-Ausgabe mit einer expliziten Struktur
Wenn Sie mithilfe der **WITH**-Klausel der **OPENJSON**-Funktion ein Schema für die Ergebnisse angeben, gibt die Funktion eine Tabelle zurück, die nur die von Ihnen in der **WITH**-Klausel definierten Spalten enthält. In der optionalen **WITH**-Klausel können Sie einen Satz von Ausgabespalten, deren Typen und die Pfade der JSON-Quelleigenschaften für jeden Ausgabewert angeben. **OPENJSON** durchläuft das Array von JSON-Objekten, liest Werte auf dem angegebenen Pfad für jede Spalte und konvertiert sie in einen angegebenen Typ.  

Hier finden Sie ein kurzes Beispiel, in dem **OPENJSON** mit einem explizit in der **WITH**-Klausel angegebenen Schema für die Ausgabe verwendet wird.  
  
**Beispiel**
  
```sql  
DECLARE @json NVARCHAR(MAX)
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
  
-   Für jedes Element im JSON-Array generiert **OPENJSON** eine neue Zeile in der Ausgabetabelle. Die zwei Elemente im JSON-Array werden in zwei Zeilen in der zurückgegebenen Tabelle konvertiert.  
  
-   Für jede Spalte, die mithilfe der Syntax `colName type json_path` angegeben wurde, konvertiert die **OPENJSON** den Wert, der in jedem Array-Element im angegebenen Pfad gefunden wurde, in den angegebenen Typ. In diesem Beispiel werden Werte aus der `Date`-Spalte aus jedem Element im Pfad `$.Order.Date` genommen und in datetime-Werte konvertiert.  
  
### <a name="more-info-about-openjson-with-an-explicit-schema"></a>Weitere Informationen zum Verwenden von OPENJSON mit einem expliziten Schema
Weitere Informationen und Beispiele finden Sie unter [Use OPENJSON with an Explicit Schema &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md) (Verwenden von OPENJSON mit einem expliziten Schema &#40;SQL Server&#41;).

Weitere Informationen zu Syntax und Verwendung finden Sie unter [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)zur Verfügung.

## <a name="openjson-requires-compatibility-level-130"></a>OPENJSON erfordert Kompatibilitätsgrad 130
Die **OPENJSON** -Funktion steht nur für den **Kompatibilitätsgrad 130**zur Verfügung. Wenn der Kompatibilitätsgrad Ihrer Datenbank kleiner als 130 ist, kann SQL Server die **OPENJSON**-Funktion nicht finden und ausführen. Andere integrierte JSON-Funktionen sind für alle Kompatibilitätsgrade verfügbar.

Sie können den Kompatibilitätsgrad in der `sys.databases`-Ansicht oder in den Datenbankeigenschaften überprüfen.

Sie können den Kompatibilitätsgrad einer Datenbank mithilfe des folgenden Befehls ändern:   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Viele spezifische Lösungen, Anwendungsfälle und Empfehlungen finden Sie im [Blogbeitrag über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL-Server und in Azure SQL-Datenbank von Jovan Popovic, Program Manager bei Microsoft.
  
## <a name="see-also"></a>Siehe auch  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  

