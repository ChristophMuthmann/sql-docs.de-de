---
title: Indizieren von JSON-Daten | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
caps.latest.revision: "9"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 559847d392fa744b32fc2aa0cdb70eeb9b2c4ebd
ms.sourcegitcommit: 06131936f725a49c1364bfcc2fccac844d20ee4d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2018
---
# <a name="index-json-data"></a>Indizieren von JSON-Daten
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

In SQL Server und SQL-Datenbank ist JSON kein integrierter Datentyp, und SQL Server verfügt nicht über benutzerdefinierte JSON-Indizes. Sie können jedoch Ihre Abfragen über JSON-Dokumente optimieren, indem Sie Standardindizes verwenden. 

Datenbankindizes verbessern die Leistung von Filter- und Sortierungsvorgängen. Ohne Indizes muss SQL Server bei jeder Datenabfrage einen vollständigen Tabellenscan durchführen.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Indizieren von JSON-Eigenschaften mithilfe von berechneten Spalten  
Wenn Sie JSON-Daten in SQL Server speichern, möchten Sie normalerweise die Abfrageergebnisse nach mindestens einer *Eigenschaft* der JSON-Dokumente filtern oder sortieren.  

### <a name="example"></a>Beispiel 
In diesem Beispiel wird angenommen, dass die AdventureWorks-`SalesOrderHeader`-Tabelle über eine `Info`-Spalte verfügt, die verschiedene Informationen im JSON-Format zu Verkaufsaufträgen enthält. Sie enthält beispielsweise Informationen zu Kunde, Vertriebsmitarbeiter, Versand- und Rechnungsadresse usw. Sie möchten Werte aus der `Info`-Spalte verwenden, um Verkaufsaufträge eines Kunden zu filtern.

### <a name="query-to-optimize"></a>Zu optimierende Abfrage
Hier finden Sie ein Beispiel der Art von Abfrage, die Sie optimieren möchten, indem Sie einen Index verwenden.  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>Beispielindex
Falls Sie Ihre Filter oder die `ORDER BY`-Klausel in Bezug auf eine Eigenschaft in einem JSON-Dokument beschleunigen möchten, können Sie die gleichen Indizes verwenden, die Sie bereits bei Ihren anderen Spalten verwenden. Sie können in JSON-Dokumenten jedoch nicht *direkt* auf Eigenschaften verweisen.
    
1.  Zunächst müssen Sie eine „virtuelle Spalte“ erstellen, die die Werte zurückgibt, die Sie für die Filterung verwenden möchten.
2.  Sie müssen dann einen Index auf dieser virtuellen Spalte erstellen.  
  
Im folgenden Beispiel wird eine berechnete Spalte erstellt, die für die Indizierung verwendet werden kann. Anschließend wird ein Index für die neue berechnete Spalte erstellt. In diesem Beispiel wird eine Spalte erstellt, die den Namen des Kunden verfügbar macht, der im Pfad `$.Customer.Name` in den JSON-Daten gespeichert ist. 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>Weitere Informationen über die berechnete Spalte 
Die Spalte wird nicht permanent berechnet. Sie wird nur berechnet, wenn der Index erneut erstellt werden muss. Sie beansprucht keinen zusätzlichen Platz in der Tabelle.   
  
Es ist wichtig, dass Sie die berechnete Spalte mit dem gleichen Ausdruck erstellen, den Sie in Ihren Abfragen verwenden möchten – in diesem Beispiel handelt es sich dabei um den Ausdruck `JSON_VALUE(Info, '$.Customer.Name')`.  
  
Sie müssen Ihre Abfragen nicht neu schreiben. Falls Sie wie in der vorherigen Beispielabfrage dargestellt Ausdrücke mit der `JSON_VALUE`-Funktion verwenden, erkennt SQL Server, dass es eine gleichwertig berechnete Spalte mit dem gleichen Ausdruck gibt und wendet dann, falls möglich, einen Index darauf an.

### <a name="execution-plan-for-this-example"></a>Ausführungsplan für dieses Beispiel
Hier finden Sie den Ausführungsplan für die Abfrage in diesem Beispiel.  
  
![Ausführungsplan](../../relational-databases/json/media/jsonindexblog1.png "Ausführungsplan")  
  
Statt eines vollständigen Tabellenscans verwendet SQL Server eine Indexsuche im nicht gruppierten Index, und findet so die Zeilen, die die angegebenen Bedingungen erfüllen. Er verwendet dann eine Schlüsselsuche in der Tabelle `SalesOrderHeader`, um die anderen Spalten abzurufen, auf die die Abfrage verweist – in diesem Beispiel `SalesOrderNumber` und `OrderDate`.  
 
### <a name="optimize-the-index-further-with-included-columns"></a>Weiteres Optimieren des Index mit enthaltenen Spalten
Diese zusätzliche Suche können Sie umgehen, indem Sie die geforderten Spalten dem Index hinzufügen. Sie können diese Spalten als standardmäßig enthaltene Spalten hinzufügen. Dies wird im folgenden Beispiel dargestellt, das eine Erweiterung des vorherigen `CREATE INDEX`-Beispiels darstellt.  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
In diesem Fall muss SQL Server keine zusätzlichen Daten aus der Tabelle `SalesOrderHeader` lesen, da alle benötigten Informationen im nicht gruppierten JSON-Index enthalten sind. Dieser Index ist eine gute Möglichkeit, um JSON- und Spaltendaten in Abfragen zu kombinieren und optimale Indizes für Ihre Arbeitsauslastung zu erstellen.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON-Indizes sind Indizes mit Sortierungserkennung  
Eine wichtige Funktion von Indizes für JSON-Daten ist, dass die Indizes über eine Sortierungserkennung verfügen. Das Ergebnis der Funktion `JSON_VALUE`, die Sie beim Erstellen der berechneten Spalte verwenden, ist ein Textwert, der seine Sortierung vom Eingabeausdruck erbt. Die Werte im Index sind daher nach den Sortierungsregeln geordnet, die in den Quellspalten definiert sind.  
  
Im folgenden Beispiel wird eine einfache Sammlungstabelle mit einem Primärschlüssel und JSON-Inhalten erstellt, um zu demonstrieren, dass die Indizes über eine Sortierungserkennung verfügen.  
  
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
  
Die vorherigen Befehle erstellen einen Standardindex auf die berechnete Spalte `vName`, die den Wert der JSON-Eigenschaft `$.name` darstellt. In der serbisch-kyrillischen Codepage lautet die Reihenfolge der Buchstaben „A“, „Б“, „В“, „Г“, „Д“, „Ђ“, „Е“, usw. Die Reihenfolge der Elemente im Index entspricht den serbisch-kyrillischen Regeln, da das Ergebnis der `JSON_VALUE`-Funktion seine Sortierung aus der Quellspalte erbt. Im folgenden Beispiel wird diese Auflistung abgefragt und die Ergebnisse nach Namen sortiert.  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Wenn Sie sich den tatsächlichen Ausführungsplan ansehen, sehen Sie, dass er die sortierten Werte aus dem nicht gruppierten Index verwendet.  
  
 ![Ausführungsplan](../../relational-databases/json/media/jsonindexblog2.png "Ausführungsplan")  
  
 Obwohl die Abfrage eine `ORDER BY`-Klausel hat, verwendet der Ausführungsplan keinen Sort-Operator. Der JSON-Index ist bereits nach den Regeln für serbisches Kyrillisch geordnet. Daher kann SQL Server den nicht gruppierten Index verwenden, in dem die Ergebnisse bereits sortiert sind.  
  
 Falls Sie jedoch die Sortierung des `ORDER BY`-Ausdrucks ändern, indem Sie beispielsweise `COLLATE French_100_CI_AS_SC` an die `JSON_VALUE`-Funktion anhängen, erhalten Sie einen anderen Ausführungsplan für die Abfrage.  
  
 ![Ausführungsplan](../../relational-databases/json/media/jsonindexblog3.png "Ausführungsplan")  
  
 Da die Anordnung der Werte im Index nicht mit den französischen Sortierungsregeln übereinstimmt, kann SQL Server den Index nicht verwenden, um Ergebnisse zu ordnen. Daher wird ein Sort-Operator hinzugefügt, der Ergebnisse nach den französischen Sortierungsregeln sortiert.  
 
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Viele spezifische Lösungen, Anwendungsfälle und Empfehlungen finden Sie im [Blogbeitrag über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL-Server und in Azure SQL-Datenbank von Jovan Popovic, Program Manager bei Microsoft.
