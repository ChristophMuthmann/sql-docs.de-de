---
title: Indizieren von JSON-Daten | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 06/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 3ed7a51b28d2b17b3239f971d0f4f684bec145cd
ms.contentlocale: de-de
ms.lasthandoff: 06/23/2017

---
# <a name="index-json-data"></a>Indizieren von JSON-Daten
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Klicken Sie in SQL Server 2016 JSON ist kein integrierter Datentyp, und SQL Server verfügt nicht über benutzerdefinierte JSON-Indizes. Sie können die Abfragen jedoch über JSON-Dokumente optimieren, indem Sie Standardindizes verwenden. 

Datenbankindizes verbessern die Leistung der Filter-und Sortierungsvorgänge. Ohne Indizes muss SQL Server bei jeder Datenabfrage einen vollständigen Tabellenscan durchführen.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Indizieren von JSON-Eigenschaften mithilfe von berechneten Spalten  
Wenn Sie JSON-Daten in SQL Server speichern, in der Regel möchten Sie Filter- oder Sortierausdruck Abfrageergebnisse nach einer oder mehreren *Eigenschaften* der JSON-Dokumente.  

### <a name="example"></a>Beispiel 
In diesem Beispiel wird angenommen, dass die AdventureWorks `SalesOrderHeader` Tabelle besitzt eine `Info` Spalte, die verschiedene Informationen im JSON-Format zu Verkaufsaufträgen enthält. Er enthält beispielsweise Informationen zu Kunden, Vertriebsmitarbeiter, Liefer-und Rechnungsadresse und So weiter. Sie möchten Werte aus der `Info` Spalte, um Verkaufsaufträge eines Kunden zu filtern.

### <a name="query-to-optimize"></a>Abfrage zur Optimierung
Hier ist ein Beispiel für den Typ der Abfrage, die Sie optimieren, indem Sie einen Index verwenden möchten.  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>Für beispielindex
Wenn Sie die Filter beschleunigen möchten oder `ORDER BY` -Klausel auf eine Eigenschaft in ein JSON-Dokument können Sie die gleichen Indizes, die Sie bereits für andere Spalten verwenden. Sie können jedoch nicht *direkt* verweisen auf Eigenschaften in JSON-Dokumenten.
    
1.  Zunächst müssen Sie eine "virtuelle Spalte" erstellen, die die Werte, die Sie zum Filtern verwenden möchten zurückgibt.
2.  Sie müssen dann einen Index auf dieser virtuellen Spalte erstellen.  
  
Das folgende Beispiel erstellt eine berechnete Spalte, die für die Indizierung verwendet werden kann. Er erstellt dann einen Index für die neue berechnete Spalte. Dieses Beispiel erstellt eine Spalte, die den Namen des Kunden verfügbar macht, die in gespeichert ist die `$.Customer.Name` Pfad in die JSON-Daten. 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>Weitere Informationen über die berechnete Spalte 
Die Spalte wird nicht permanent berechnet. Sie wird nur berechnet, wenn der Index erneut erstellt werden muss. Sie beansprucht keinen zusätzlichen Platz in der Tabelle.   
  
Es ist wichtig, dass Sie erstellen die berechnete Spalte mit dem gleichen Ausdruck, die Sie in Ihren Abfragen – in diesem Beispiel verwenden möchten, ist des Ausdrucks `JSON_VALUE(Info, '$.Customer.Name')`.  
  
Sie müssen Ihre Abfragen nicht neu schreiben. Bei Verwendung von Ausdrücken mit der `JSON_VALUE` -Funktion, wie gezeigt in der Beispielabfrage, die oben genannten SQL Server erkennt, dass eine Äquivalent berechnete Spalte mit dem gleichen Ausdruck und wendet einen Index nach Möglichkeit.

### <a name="execution-plan-for-this-example"></a>Ausführungsplan für dieses Beispiel
Hier ist der Ausführungsplan für die Abfrage in diesem Beispiel wird ein.  
  
![Ausführungsplan](../../relational-databases/json/media/jsonindexblog1.png "Ausführungsplan")  
  
Statt eines vollständigen Tabellenscans verwendet SQL Server eine Indexsuche im nicht gruppierten Index, und findet so die Zeilen, die die angegebenen Bedingungen erfüllen. Anschließend wird eine Schlüsselsuche in der `SalesOrderHeader` Tabelle, die andere Spalten abzurufen, die in der Abfrage – in diesem Beispiel verwiesen werden `SalesOrderNumber` und `OrderDate`.  
 
### <a name="optimize-the-index-further-with-included-columns"></a>Optimieren Sie den Index mit eingeschlossenen Spalten
Sie können diese zusätzliche Suche in der Tabelle vermeiden, wenn Sie die geforderten Spalten im Index hinzufügen. Sie können diese Spalten als standardmäßig enthaltene Spalten hinzufügen, wie im folgenden Beispiel gezeigt, die erweitert die `CREATE INDEX` oben gezeigte Beispiel.  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
In diesem Fall SQL Server keinen zusätzlichen Daten aus der `SalesOrderHeader` Tabelle, da Sie alles, was es muss in der nicht gruppierten JSON-Index enthalten ist. Dies ist eine gute Möglichkeit, JSON- und Spaltendaten in Abfragen zu kombinieren und um optimale Indizes für Ihre arbeitsauslastung zu erstellen.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON-Indizes sind Indizes mit Sortierungserkennung  
Ein wichtiges Feature von Indizes für JSON-Daten ist, dass die Indizes mit sortierungserkennung sind. Das Ergebnis der `JSON_VALUE` Funktion, die Sie verwenden, wenn Sie die berechnete Spalte erstellen, ist ein Textwert, der seine Sortierung vom Eingabeausdruck erbt. Aus diesem Grund werden die Werte im Index sortiert den Sortierungsregeln in den quellenspalten definiert.  
  
Um dies zu demonstrieren, erstellt das folgende Beispiel eine einfache Sammlungstabelle mit einem Primärschlüssel und JSON-Inhalt.  
  
```sql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
Der vorherige Befehl gibt die serbisch-kyrillische Sortierung für die JSON-Spalte an. Das folgende Beispiel füllt die Tabelle auf und erstellt einen Index auf die Namenseigenschaft.  
  
```sql  
INSERT INTO JsonCollection
VALUES
(N'{"name":"Иво","surname":"Андрић"}'),
(N'{"name":"Андрија","surname":"Герић"}'),
(N'{"name":"Владе","surname":"Дивац"}'),
(N'{"name":"Новак","surname":"Ђоковић"}'),
(N'{"name":"Предраг","surname":"Стојаковић"}'),
(N'{"name":"Михајло","surname":"Пупин"}'),
(N'{"name":"Борислав","surname":"Станковић"}'),
(N'{"name":"Владимир","surname":"Грбић"}'),
(N'{"name":"Жарко","surname":"Паспаљ"}'),
(N'{"name":"Дејан","surname":"Бодирога"}'),
(N'{"name":"Ђорђе","surname":"Вајферт"}'),
(N'{"name":"Горан","surname":"Бреговић"}'),
(N'{"name":"Милутин","surname":"Миланковић"}'),
(N'{"name":"Никола","surname":"Тесла"}')
GO
  
ALTER TABLE JsonCollection
ADD vName AS JSON_VALUE(json,'$.name')

CREATE INDEX idx_name
ON JsonCollection(vName)
```  
  
Die vorherigen Befehle erstellen einen Standardindex auf die berechnete Spalte `vName`, der den Wert darstellt, aus dem JSON `$.name` Eigenschaft. In der serbisch-kyrillischen Codepage lautet die Reihenfolge der Buchstaben „A“, „Б“, „В“, „Г“, „Д“, „Ђ“, „Е“, usw. Die Reihenfolge der Elemente im Index ist kompatibel mit den Regeln für Serbisches Kyrillisch da das Ergebnis der `JSON_VALUE` Funktion seine Sortierung aus der Quellspalte erbt. Im folgenden Beispiel wird diese Auflistung abgefragt und die Ergebnisse nach Namen sortiert.  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Wenn Sie sich den tatsächlichen Ausführungsplan ansehen, sehen Sie, dass er die sortierten Werte aus dem nicht gruppierten Index verwendet.  
  
 ![Ausführungsplan](../../relational-databases/json/media/jsonindexblog2.png "Ausführungsplan")  
  
 Obwohl die Abfrage hat einen `ORDER BY` -Klausel, die der Ausführungsplan keinen Sort-Operator verwendet keine. Der JSON-Index ist bereits nach den Regeln für serbisches Kyrillisch geordnet. Daher kann SQL Server den nicht gruppierten Index verwenden, in dem die Ergebnisse bereits sortiert sind.  
  
 Jedoch wenn wir die Sortierung ändern die `ORDER BY` Expression - angenommen, wir uns konzentrieren `COLLATE French_100_CI_AS_SC` nach der `JSON_VALUE` Funktion – erhalten wir einen anderen Abfrageausführungsplan.  
  
 ![Ausführungsplan](../../relational-databases/json/media/jsonindexblog3.png "Ausführungsplan")  
  
 Da die Anordnung der Werte im Index nicht mit den französischen Sortierungsregeln übereinstimmt, kann SQL Server den Index nicht verwenden, um Ergebnisse zu ordnen. Daher wird ein Sort-Operator hinzugefügt, der Ergebnisse nach den französischen Sortierungsregeln sortiert.  
 
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Für viele spezifische Lösungen Fälle und Empfehlungen zu verwenden, finden Sie unter der [Blogeinträge von jovan zur integrierten JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL Server und Azure SQL-Datenbank von Microsoft Program Manager Jovan Popovic.

