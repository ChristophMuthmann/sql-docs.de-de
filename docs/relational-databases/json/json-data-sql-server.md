---
title: JSON-Daten (SQL Server) | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- JSON
- JSON, built-in support
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: e2a427682aebeeccc82a1b7f6521399b8a0b6fe8
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="json-data-sql-server"></a>JSON-Daten (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

JSON ist ein beliebtes Textdatenformat zum Austauschen von Daten in modernen Webanwendungen und mobilen Anwendungen. JSON wird auch zum Speichern von unstrukturierten Daten in Protokolldateien oder NoSQL-Datenbanken wie Microsoft Azure DocumentDB verwendet. Viele REST-Webdienste geben Ergebnisse als JSON-Text formatiert zurück oder akzeptieren Daten, die im JSON-Format formatiert sind. Beispielsweise verfügen die meisten Azure-Dienste wie Azure Search, Azure Storage und Azure DocumentDb über REST-Endpunkte, die JSON zurückgeben oder verarbeiten. JSON ist auch das hauptsächliche Format zum Austauschen von Daten zwischen Webseiten und Webservern mithilfe von AJAX-Aufrufen.  
  
 Hier ist ein Beispiel des JSON-Texts:  
  
```json  
[{
    "name": "John",
    "skills": ["SQL", "C#", "Azure"]
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```  
  
 SQL Server bietet integrierte Funktionen und Operatoren, mit denen Sie die folgenden Schritte mit dem JSON-Text ausführen können.  
  
-   Analysieren Sie JSON-Text und lesen oder ändern Sie Werte.  
  
-   Wandeln Sie Arrays von JSON-Objekten in das Tabellenformat um.  
  
-   Wenden Sie eine beliebige Transact-SQL-Abfrage auf die konvertierte JSON-Objekte an.  
  
-   Formatieren Sie die Ergebnisse der Transact-SQL-Abfragen in das JSON-Format.  
  
 ![Übersicht über die integrierte Unterstützung für JSON](../../relational-databases/json/media/jsonslides1overview.png "Overview of built-in JSON support")  
  
## <a name="key-json-capabilities-of-sql-server"></a>Wichtige JSON-Funktionen von SQL Server 
Hier werden weitere Informationen über die wichtigsten Funktionen von SQL Server durch die integrierte Unterstützung für JSON bereitgestellt.

### <a name="extract-values-from-json-text-and-use-them-in-queries"></a>Extrahieren von Werten aus JSON-Text und Verwenden dieser Werte in Abfragen
Wenn Sie JSON-Text verwenden, der in Datenbanktabellen gespeichert wird, können Sie integrierte Funktionen verwenden, um Werte im JSON-Text zu lesen oder zu ändern.  
  
-   Verwenden Sie die **JSON_VALUE**-Funktion, um einen skalaren Wert aus einer JSON-Zeichenfolge zu extrahieren.
  
-   Verwenden Sie **JSON_QUERY**, um ein Objekt oder ein Array aus einer JSON-Zeichenfolge zu extrahieren.
  
-   Verwenden Sie die **ISJSON** -Funktion zum Testen, ob eine Zeichenfolge ein gültiges JSON-Format enthält.

-   Verwenden Sie die **JSON_MODIFY**-Funktion zum Ändern eines Werts in einer JSON-Zeichenfolge.

**Beispiel**
  
 Im folgenden Beispiel verwendet die Abfrage sowohl relationale als auch JSON-Daten (gespeichert in einer Spalte mit dem Namen `jsonCol`) aus einer Tabelle:  
  
```sql  
SELECT Name,Surname,
 JSON_VALUE(jsonCol,'$.info.address.PostCode') AS PostCode,
 JSON_VALUE(jsonCol,'$.info.address."Address Line 1"')+' '
  +JSON_VALUE(jsonCol,'$.info.address."Address Line 2"') AS Address,
 JSON_QUERY(jsonCol,'$.info.skills') AS Skills
FROM People
WHERE ISJSON(jsonCol)>0
 AND JSON_VALUE(jsonCol,'$.info.address.Town')='Belgrade'
 AND Status='Active'
ORDER BY JSON_VALUE(jsonCol,'$.info.address.PostCode')
```  
  
 Anwendungen und Tools erkennen keinen Unterschied zwischen den Werten aus skalaren Tabellenspalten und denen aus JSON-Spalten. Sie können Werte aus dem JSON-Text in jedem Teil der Transact-SQL-Abfrage verwenden (z.B. WHERE-, ORDER BY-, GROUP BY-Klauseln, Fenster-Aggregate usw.). JSON-Funktionen verwenden eine JavaScript-ähnliche Syntax zum Verweisen auf Werte in JSON-Text.

Weitere Informationen finden Sie unter [Validate, Query, and Change JSON Data with Built-in Functions &#40;SQL Server&#41; (Überprüfen, Abfragen und Ändern von JSON-Daten mit integrierten Funktionen [SQL Server])](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)(Überprüfen, Abfragen und Ändern von JSON-Daten mit integrierten Funktionen [SQL Server]), [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)und [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
### <a name="change-json-values"></a>Ändern der JSON-Werte
Wenn Sie Teile des JSON-Texts ändern müssen, können Sie die **JSON_MODIFY**-Funktion verwenden, um den Wert einer Eigenschaft in einer JSON-Zeichenfolge zu aktualisieren und die aktualisierte JSON-Zeichenfolge zurückzugeben. Im folgenden Beispiel wird der Wert einer Eigenschaft in einer Variable aktualisiert, die JSON enthält.  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=JSON_MODIFY(@jsonInfo,'$.info.address[0].town','London') 
```  
  
### <a name="convert-json-collections-to-a-rowset"></a>Konvertieren der JSON-Sammlungen in ein Rowset
Eine benutzerdefinierte Abfragesprache ist zur Abfrage von JSON-Daten in SQL Server nicht erforderlich. Zum Abfragen von JSON-Daten können Sie Standard-T-SQL verwenden. Wenn Sie eine Abfrage erstellen oder JSON-Daten protokollieren müssen, können Sie die JSON-Daten einfach durch Aufrufen der **OPENJSON**-Rowsetfunktion in Zeilen und Spalten konvertieren. Weitere Informationen finden Sie unter [Convert JSON Data to Rows and Columns with OPENJSON &#40;SQL Server&#41; (Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON [SQL Server])](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).  
  
 Im folgenden Beispiel wird **OPENJSON** aufgerufen, um ein Array von Objekten, das in einer `@json`-Variablen gespeichert ist, in ein Rowset zu transformieren, das mithilfe der SQL **SELECT**-Standardanweisung abgefragt werden kann:  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json =  
N'[  
       { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },  
       { "id" : 5,"info": { "name": "Jane", "surname": "Smith" }, "dob": "2005-11-04T12:00:00" }  
 ]'  
   
SELECT *  
FROM OPENJSON(@json)  
  WITH (id int 'strict $.id',  
        firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',  
        age int, dateOfBirth datetime2 '$.dob')  
```  
  
 **Ergebnisse**  
  
|id|firstName|lastName|age|dateOfBirth|  
|--------|---------------|--------------|---------|-----------------|  
|2|John|Smith|25||  
|5|Jane|Smith||2005-11-04T12:00:00|  
  
 **OPENJSON** transformiert das Array von JSON-Objekten in eine Tabelle, wobei jedes Objekt als eine Zeile dargestellt wird. Die Schlüssel/Wert-Paare werden als Zellen zurückgegeben. Die Ausgabe verwendet die folgenden Regeln.
-   **OPENJSON** konvertiert JSON-Werte in die in der **WITH**-Klausel angegebenen Typen.
-   **OPENJSON** kann sowohl einfache Schlüssel/Wert-Paare als auch geschachtelte, hierarchisch angeordnete Objekte verarbeiten.
-   Sie müssen nicht alle im JSON-Text enthaltenen Felder zurückgeben.
-   **OPENJSON** gibt NULL-Werte zurück, wenn JSON-Werte nicht vorhanden sind.
-   Sie können optional einen Pfad zu der Typspezifikation angeben, um auf eine geschachtelte Eigenschaft, oder um mit einem anderen Namen auf eine Eigenschaft zu verweisen.
-   Das optionale **strenge** im Pfad gibt an, dass die Werte für die angegebenen Eigenschaften im JSON-Text vorhanden sein müssen.

Weitere Informationen finden Sie unter [Convert JSON Data to Rows and Columns with OPENJSON &#40;SQL Server&#41; (Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON [SQL Server])](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) (Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON [SQL Server]) und [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
### <a name="convert-sql-server-data-to-json-or-export-json"></a>Konvertieren von SQL Server-Daten in JSON oder Exportieren von JSON
Formatieren Sie Daten aus SQL Server oder die Ergebnisse von SQL-Abfragen im JSON-Format, indem Sie die **FOR JSON** -Klausel einer **SELECT** -Anweisung hinzufügen. Verwenden Sie FOR JSON, um die Formatierung der JSON-Ausgabe von den Clientanwendungen an SQL Server zu delegieren. Weitere Informationen finden Sie unter [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Formatieren von Abfrageergebnissen als JSON mit FOR JSON [SQL Server])](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 Im folgenden Beispiel wird der PATH-Modus mit der FOR JSON-Klausel verwendet.  
  
```sql  
SELECT id, firstName AS "info.name", lastName AS "info.surname", age, dateOfBirth as dob  
FROM People  
FOR JSON PATH  
```  
  
Am **FOR JSON** -Klausel formatiert SQL-Ergebnisse als JSON-Text, der für alle Apps bereitgestellt werden kann, die JSON verstehen. Die Option PATH verwendet in der SELECT-Klausel durch Punkte getrennte Aliase, um Objekte in den Abfrageergebnissen zu schachteln.  
  
 **Ergebnisse**  
  
```json  
[{
    "id": 2,
    "info": {
        "name": "John",
        "surname": "Smith"
    },
    "age": 25
}, {
    "id": 5,
    "info": {
        "name": "Jane",
        "surname": "Smith"
    },
    "dob": "2005-11-04T12:00:00"
}] 
```  
  
 Weitere Informationen finden Sie unter [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) (Formatieren von Abfrageergebnissen als JSON mit FOR JSON [SQL Server]) und [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  
  
## <a name="combine-relational-and-json-data"></a>Kombinieren von relationalen und JSON-Daten
 SQL Server bietet ein Hybridmodell zum Speichern und Verarbeiten von relationalen Daten und JSON-Daten mithilfe der Transact-SQL-Standardsprache. Sie können Sammlungen Ihrer JSON-Dokumente nach Tabellen anordnen, Beziehungen zwischen ihnen herstellen, in Tabellen gespeicherte, stark typisierte Skalarspalten mit flexiblen Schlüssel-Wert/Paaren kombinieren, die in JSON-Spalten gespeichert werden, und sowohl Skalarwerte als auch JSON-Werte in einer oder mehreren Tabellen mithilfe von vollständigem Transact-SQL abfragen.
 
JSON-Text wird in der Regel in „varchar“- oder „nvarchar“-Spalten gespeichert und als Nur-Text indiziert. Jede SQL Server-Funktion oder -Komponente, die Text unterstützt, unterstützt auch JSON, daher gibt es fast keine Einschränkungen hinsichtlich der Interaktion zwischen JSON und anderen SQL Server-Funktionen. Sie können JSON im Arbeitsspeicher oder in temporalen Tabellen speichern, Sicherheitsprädikate auf Zeilenebene auf JSON-Text anwenden usw.

Wenn bei Ihnen reine JSON-Arbeitsauslastungen vorliegen, für die Sie eine Abfragesprache verwenden möchten, die der Verarbeitung von JSON-Dokumenten angepasst ist, sollten Sie Microsoft Azure [DocumentDB](https://azure.microsoft.com/services/documentdb/)in Erwägung ziehen.  
  
 Hier folgen einige Anwendungsfälle, die veranschaulichen, wie Sie die integrierte JSON-Unterstützung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwenden können.  
  
## <a name="return-data-from-a-sql-server-table-formatted-as-json"></a>Rückgabe von Daten aus einer SQL Server-Tabelle im JSON-Format  
 Wenn Sie einen Webdienst verwenden, der Daten von der Datenbankebene übernimmt und sie im JSON-Format oder in JavaScript-Frameworks oder -Bibliotheken (die Daten im JSON-Format akzeptieren) zurückgibt, können Sie die Ergebnisse direkt in einer SQL-Abfrage formatieren. Anstatt Code zu schreiben oder eine Bibliothek einzuschließen, um tabellarische Abfrageergebnisse zu konvertieren und dann Objekte in das JSON-Format zu serialisieren, können Sie auch FOR JSON verwenden, um die JSON-Formatierung an SQL Server zu delegieren.  
  
 Sie können z.B. eine JSON-Ausgabe generieren, die der OData-Spezifikation entspricht. Der Webdienst erwartet eine Anforderung und Antwort im folgenden Format.  
  
-   Anforderung: `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  
  
-   Antwort: `{"@odata.context":"http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity","ProductID":1,"ProductName":"Chai"}`  
  
 Diese OData-URL stellt eine Anforderung für die Spalten „ProductID“ und „ProductName“ für das Produkt mit der ID „1“. Sie können **FOR JSON** verwenden, um die Ausgabe erwartungsgemäß in SQL Server zu formatieren.  
  
```sql  
SELECT 'http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity'
 AS '@odata.context',   
 ProductID, Name as ProductName   
FROM Production.Product  
WHERE ProductID = 1  
FOR JSON AUTO  
```  
  
Das Ergebnis dieser Abfrage ist ein vollständig mit der OData-Spezifikation konformer JSON-Text. Formatierung und Escapevorgang werden von SQL Server übernommen. SQL Server kann Abfrageergebnisse in einem beliebigen Format wie OData JSON oder GeoJSON formatieren. Weitere Informationen finden Sie unter [Returning spatial data in GeoJSON format (Zurückgeben von räumlichen Daten im GeoJSON-Format)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/returning-spatial-data-in-geojson-format-part-1).  
  
## <a name="analyze-json-data-with-sql-queries"></a>Analysieren von JSON-Daten mit SQL-Abfragen  
 Wenn Sie JSON-Daten für Berichtszwecke filtern oder aggregieren müssen, können Sie JSON mithilfe von **OPENJSON** in ein relationales Format transformieren. Verwenden Sie dann Standard- [!INCLUDE[tsql](../../includes/tsql-md.md)] und integrierte Funktionen, um die Berichte vorzubereiten.  
  
```sql  
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date  
FROM   SalesOrderRecord AS Tab  
          CROSS APPLY  
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')  
           WITH (  
              Number   varchar(200) N'$.Order.Number',   
              Date     datetime     N'$.Order.Date',  
              Customer varchar(200) N'$.AccountNumber',   
              Quantity int          N'$.Item.Quantity'  
           )  
  AS SalesOrderJsonData  
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'  
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified  
```  
  
 Sowohl Standardtabellenspalten und -werte aus JSON-Text können in derselben Abfrage verwendet werden. Sie können Indizes zum `JSON_VALUE(Tab.json, '$.Status')`-Ausdruck hinzufügen, um die Leistung der Abfrage zu verbessern. Weitere Informationen finden Sie unter [Indizieren von JSON-Daten](../../relational-databases/json/index-json-data.md).
  
## <a name="import-json-data-into-sql-server-tables"></a>Importieren von JSON-Daten in SQL Server-Tabellen  
 Wenn Sie JSON-Daten aus einem externen Dienst in SQL Server laden müssen, können Sie die Daten mit **OPENJSON** in SQL Server importieren, anstatt die Daten in der Anwendungsschicht zu analysieren.  
  
```sql  
DECLARE @jsonVariable NVARCHAR(MAX)

SET @jsonVariable = N'[  
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
  
INSERT INTO SalesReport  
SELECT SalesOrderJsonData.*  
FROM OPENJSON (@jsonVariable, N'$.Orders.OrdersArray')  
           WITH (  
              Number   varchar(200) N'$.Order.Number',   
              Date     datetime     N'$.Order.Date',  
              Customer varchar(200) N'$.AccountNumber',   
              Quantity int          N'$.Item.Quantity'  
           )  
  AS SalesOrderJsonData;  
```  
  
 Der Inhalt der JSON-Variable kann von einem externen REST-Dienst bereitgestellt, als Parameter von einem clientseitigen JavaScript-Framework gesendet oder aus externen Dateien geladen werden. Sie können Ergebnisse aus JSON-Text ganz einfach in eine SQL-Tabelle einfügen, dort aktualisieren oder zusammenführen. Weitere Informationen zu diesem Szenario finden Sie unter den folgenden Blogbeiträgen.
-   [OPENJSON – The easiest way to import JSON text into table](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/09/22/openjson-the-easiest-way-to-import-json-text-into-table/)
-   [Upsert JSON documents in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/03/upsert-json-documents-in-sql-server-2016)
-   [Loading GeoJSON data into SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/).  
  
## <a name="load-json-files-into-sql-server"></a>Laden von JSON-Dateien in SQL Server  
 In Dateien gespeicherte Informationen können als Standard-JSON oder als JSON-Text formatiert werden, in dem Zeilenumbrüche als Trennzeichen verwendet werden. SQL Server kann die Inhalte aus JSON-Dateien importieren, sie mit **OPENJSON**- oder **JSON_VALUE**-Funktionen analysieren und in Tabellen laden.  
  
-   Wenn Ihre JSON-Dokumente in lokalen Dateien gespeichert, auf freigegebenen Netzlaufwerken oder einem Azure File Storage-Speicherort gespeichert werden, auf die SQL Server zugreifen kann, können Sie einen Massenimport durchführen, um die JSON-Daten in SQL Server zu laden. Weitere Informationen zu diesem Szenario finden Sie unter [Importing JSON files into SQL Server using OPENROWSET (BULK)](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2015/10/07/importing-json-files-into-sql-server-using-openrowset-bulk.aspx)(Importieren von JSON-Dateien in SQL Server mithilfe von OPENROWSET [BULK]).  
  
-   Wenn Ihre JSON-Dateien, die Zeilenumbrüche als Trennzeichen verwenden, in Azure-Blobspeicher oder im Hadoop-Dateisystem gespeichert werden, können Sie den JSON-Text mithilfe von Polybase laden, in Transact-SQL-Code analysieren und in Tabellen laden.  
  
## <a name="test-drive-built-in-json-support"></a>Testen der integrierten JSON-Unterstützung  
 **Testen Sie die integrierte JSON-Unterstützung mithilfe der AdventureWorks-Beispieldatenbank.** Laden Sie zum Abrufen der AdventureWorks-Beispieldatenbank zumindest die Datenbankdatei und die Beispiel- und Skriptdatei [here](https://www.microsoft.com/en-us/download/details.aspx?id=49502). Nach der Wiederherstellung der Beispieldatenbank auf einer Instanz von SQL Server 2016, entpacken Sie die Beispieldateien, und öffnen Sie die Datei „JSON Sample Queries procedures views and indexes.sql“ im JSON-Ordner. Führen Sie die Skripts in dieser Datei aus, um einige der vorhandenen Daten als JSON-Daten neu zu formatieren, führen Sie Beispielabfragen und -berichte für die JSON-Daten aus, indizieren Sie die JSON-Daten, und importieren und exportieren Sie JSON.  
  
 Mit den in der Datei enthaltenen Skripts haben Sie die folgenden Möglichkeiten.  
  
1.  Denormalisieren Sie die vorhandenen Schemas, um Spalten mit JSON-Daten zu erstellen.  
  
    1.  Speichern Sie Informationen aus den Tabellen „SalesReasons“, „SalesOrderDetails“, „SalesPerson“, „Customer“ sowie aus anderen Tabellen, die auftragsbezogene Daten enthalten, in der Tabelle „SalesOrder_json“ in JSON-Spalten.  
  
    2.  Speichern Sie Informationen aus den Tabellen „EmailAddresses“ bzw. „PersonPhone“ als Arrays von JSON-Objekten in der Tabelle „Person_json“.  
  
2.  Erstellen Sie Prozeduren und Sichten, die JSON-Daten abfragen.  
  
3.  Indizieren Sie JSON-Daten: Erstellen Sie Indizes zu JSON-Eigenschaften und Volltextindizes.  
  
4.  Importieren und exportieren Sie JSON: Erstellen Sie Prozeduren und führen Sie diese aus, die den Inhalt der Tabellen „Person“ und „SalesOrder“ als JSON-Ergebnisse exportieren und importieren sowie die Tabellen „Person“ und „SalesOrder“ mithilfe von JSON-Eingaben aktualisieren.  
  
5.  Führen Sie Abfragebeispiele aus: Führen Sie einige Abfragen aus, die die in den Schritten 2 und 4 erstellten gespeicherten Prozeduren und Sichten aufrufen.  
  
6.  Bereinigen Sie Skripts: Führen Sie diesen Teil nicht aus, wenn Sie die in den Schritten 2 und 4 erstellten gespeicherten Prozeduren und Sichten beibehalten möchten.  
  
## <a name="learn-more-about-built-in-json-support"></a>Weitere Informationen zur integrierten JSON-Unterstützung  
  
### <a name="topics-in-this-section"></a>Themen in diesem Abschnitt  
 [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Formatieren von Abfrageergebnissen als JSON mit FOR JSON [SQL Server])](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
 Verwenden Sie die FOR JSON-Klausel, um die Formatierung der JSON-Ausgabe von Ihren Clientanwendungen an SQL Server zu delegieren.  
  
 [Convert JSON Data to Rows and Columns with OPENJSON &#40;SQL Server&#41; (Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON [SQL Server])](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)  
 Verwenden Sie OPENJSON, um JSON-Daten in SQL Server zu importieren oder JSON-Daten für eine App oder einen Dienst in das relationale Format zu konvertieren, die JSON derzeit nicht direkt verarbeiten können, z. B. SQL Server Integration Services.  
  
 [Validate, Query, and Change JSON Data with Built-in Functions &#40;SQL Server&#41; (Überprüfen, Abfragen und Ändern von JSON-Daten mit integrierten Funktionen [SQL Server])](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)  
 Verwenden Sie diese integrierten Funktionen, um JSON-Text zu überprüfen und einen Skalarwert, ein Objekt oder ein Array zu extrahieren.  
  
 [JSON Path Expressions &#40;SQL Server&#41; (JSON-Pfadausdrücke [SQL Server])](../../relational-databases/json/json-path-expressions-sql-server.md)  
 Verwenden Sie einen Pfadausdruck, um den zu verwendenden JSON-Text anzugeben.  
  
 [Indizieren von JSON-Daten](../../relational-databases/json/index-json-data.md)  
 Verwenden Sie berechnete Spalten, um für Eigenschaften in JSON-Dokumenten Indizes mit Sortierungserkennung zu erstellen.  
  
[Lösen häufiger Probleme mit JSON in SQL Server](../../relational-databases/json/solve-common-issues-with-json-in-sql-server.md)  
 Hier finden Sie Antworten auf einige häufig gestellte Fragen zu der integrierten JSON-Unterstützung in SQL Server.  
  
### <a name="microsoft-blog-posts"></a>Microsoft-Blogbeiträge  
  
-   Für viele spezifische Lösungen Fälle und Empfehlungen zu verwenden, finden Sie unter der [Blogeinträge von jovan zur integrierten JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL Server und Azure SQL-Datenbank von Microsoft Program Manager Jovan Popovic.  
  
### <a name="reference-topics"></a>Referenzthemen  
  
-   [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md) (FOR JSON)  
  
-   [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
-   [JSON Functions &#40;Transact-SQL&#41; (JSON-Funktionen [Transact-SQL])](../../t-sql/functions/json-functions-transact-sql.md)  
  
    -   [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)  
  
    -   [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)  
  
    -   [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
    -   [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)  
  
  

