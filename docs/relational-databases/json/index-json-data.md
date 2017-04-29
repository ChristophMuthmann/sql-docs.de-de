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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cf3c58c7d71a98bfaa1f27611762bf7fb3fe8725
ms.lasthandoff: 04/11/2017

---
# <a name="index-json-data"></a>Indizieren von JSON-Daten
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Datenbankindizes verbessern die Leistung Ihrer Filter- und Sortierungsvorgänge. Ohne Indizes muss SQL Server bei jeder Datenabfrage einen vollständigen Tabellenscan durchführen.  
  
 JSON ist kein integrierter Datentyp in SQL Server 2016, und SQL Server 2016 verfügt nicht über benutzerdefinierte JSON-Indizes. Sie können jedoch Ihre Abfragen über JSON-Dokumente optimieren, indem Sie Standardindizes verwenden.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Indizieren von JSON-Eigenschaften mithilfe von berechneten Spalten  
 Wenn Sie JSON-Daten in SQL Server speichern, möchten Sie normalerweise die Abfrageergebnisse nach den Eigenschaften der JSON-Dokumente filtern oder sortieren.  
  
 In diesem Beispiel verfügt die AdventureWorks-Tabelle SalesOrderHeader über eine „Info“-Spalte, die verschiedene Informationen zu Verkaufsaufträgen enthält – beispielsweise Informationen zum Kunden, Vertriebsmitarbeiter, zur Versand-/Rechnungsadresse und so weiter. Sie möchten Werte aus der Infospalte verwenden, um Verkaufsaufträge eines Kunden zu filtern. Hier ist die Abfrage, die Sie optimieren möchten, indem Sie einen Index verwenden.  
  
```tsql  
SELECT SalesOrderNumber,OrderDate,JSON_VALUE(Info,'$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info,'$.Customer.Name')=N'Aaron Campbell' 
```  
  
 Falls Sie Ihre Filter oder die ORDER BY-Klausel in Bezug auf eine Eigenschaft in einem JSON-Dokument beschleunigen möchten, können Sie die gleichen Indizes verwenden, wie bei Ihren anderen Spalten. Sie können jedoch in JSON-Dokumenten nicht direkt auf Eigenschaften verweisen. Zunächst müssen Sie eine „virtuelle Spalte“ erstellen, die die Werte zurückgibt, die Sie für die Filterung verwenden möchten. Sie müssen dann einen Index auf dieser virtuellen Spalte erstellen.  
  
 Das folgende Beispiel erstellt eine berechnete Spalte, die für die Indizierung verwendet werden kann, und erstellt dann einen Index für diese Spalte. Dieses Beispiel erstellt eine Spalte, die den Namen des Kunden verfügbar macht, der im Pfad „$.Customer.Name“ in den JSON-Dokumenten gespeichert ist.  
  
```tsql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
  
 Die Spalte wird nicht permanent berechnet. Sie beansprucht keinen zusätzlichen Platz in der Tabelle. Sie wird nur berechnet, wenn der Index erneut erstellt werden muss.  
  
 Es ist wichtig, dass Sie die berechnete Spalte mit dem gleichen Ausdruck erstellen, den Sie in Ihren Abfragen verwenden möchten – in diesem Beispiel `JSON_VALUE(Info, '$.Customer.Name')`.  
  
 Sie müssen Ihre Abfragen nicht neu schreiben. Falls Sie Ausdrücke mit der JSON-VALUE-Funktion verwenden, sieht SQL Server, dass es eine äquivalent berechnete Spalte mit dem gleichen Ausdruck gibt. Er wendet, falls möglich, einen Index darauf an. Hier ist der Ausführungsplan für die Abfrage in diesem Beispiel.  
  
 ![Ausführungsplan](../../relational-databases/json/media/jsonindexblog1.png "Ausführungsplan")  
  
 Statt eines vollständigen Tabellenscans verwendet SQL Server eine Indexsuche im nicht gruppierten Index, und findet so die Zeilen, die die angegebenen Bedingungen erfüllen. Er verwendet dann eine Schlüsselsuche in der Tabelle SalesOrderHeader, um andere Spalten abzurufen, auf die die Abfrage verweist – in diesem Beispiel SalesOrderNumber und OrderDate.  
  
 Diese zusätzliche Suche können Sie umgehen, indem Sie die geforderten Spalten dem JSON-Index hinzufügen. Sie können diese Spalten als standardmäßig enthaltene Spalten hinzufügen, wie im folgenden Beispiel gezeigt.  
  
```tsql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
 In diesem Fall liest SQL Server keine zusätzlichen Daten von der Tabelle SalesOrderHeader, da alle benötigten Informationen im nicht gruppierten JSON-Index enthalten sind. Das ist eine gute Möglichkeit, JSON- und Spaltendaten in Abfragen zu kombinieren, und um optimale Indizes für Ihre Arbeitsauslastung zu erstellen.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON-Indizes sind Indizes mit Sortierungserkennung  
 Eine wichtige Eigenschaft von JSON-Indizes ist, dass sie Sortierungserkennungen haben. Das Ergebnis der Funktion JSON_VALUE ist ein Textwert, der seine Sortierung vom Eingabeausdruck erbt. Die Werte im Index sind daher nach den Sortierungsregeln geordnet, die in den Quellenspalten definiert sind.  
  
 Um dies zu demonstrieren, erstellt das folgende Beispiel eine einfache Sammlungstabelle mit einem Primärschlüssel und JSON-Inhalt.  
  
```tsql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
 Der vorherige Befehl gibt die serbisch-kyrillische Sortierung für die JSON-Spalte an. Das folgende Beispiel füllt die Tabelle auf und erstellt einen Index auf die Namenseigenschaft.  
  
```tsql  
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
  
 Die vorherigen Befehle erstellen einen Standardindex auf die berechnete Spalte „vName“, die den Wert der JSON-Eigenschaft „$.name“ darstellt. In der serbisch-kyrillischen Codepage lautet die Reihenfolge der Buchstaben „A“, „Б“, „В“, „Г“, „Д“, „Ђ“, „Е“, usw. Die Reihenfolge der Elemente im Index entspricht den serbisch-kyrillischen Regeln, da das Ergebnis der JSON_VALUE-Funktion seine Sortierung aus der Quellspalte erbt. Im folgenden Beispiel wird diese Auflistung abgefragt und die Ergebnisse nach Namen sortiert.  
  
```tsql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Wenn Sie sich den tatsächlichen Ausführungsplan ansehen, sehen Sie, dass er die sortierten Werte aus dem nicht gruppierten Index verwendet.  
  
 ![Ausführungsplan](../../relational-databases/json/media/jsonindexblog2.png "Ausführungsplan")  
  
 Obwohl die Abfrage eine ORDER BY-Klausel hat, verwendet der Ausführungsplan keinen Sort-Operator. Der JSON-Index ist bereits nach den Regeln für serbisches Kyrillisch geordnet. Daher kann SQL Server den nicht gruppierten Index verwenden, in dem die Ergebnisse bereits sortiert sind.  
  
 Falls wir jedoch die Reihenfolge der Sortierung nach Ausdruck ändern – falls wir beispielsweise `COLLATE French_100_CI_AS_SC` hinter die JSON_VALUE-Funktion platzieren – erhalten wir einen anderen Ausführungsplan für die Abfrage.  
  
 ![Ausführungsplan](../../relational-databases/json/media/jsonindexblog3.png "Ausführungsplan")  
  
 Da die Anordnung der Werte im Index nicht mit den französischen Sortierungsregeln übereinstimmt, kann SQL Server den Index nicht verwenden, um Ergebnisse zu ordnen. Daher wird ein Sort-Operator hinzugefügt, der Ergebnisse nach den französischen Sortierungsregeln sortiert.  
  
  

