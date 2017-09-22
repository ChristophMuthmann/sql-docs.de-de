---
title: 'Schritt 3: Machbarkeitsnachweis Herstellen einer Verbindung mit SQL mit Node.js | Microsoft Docs'
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5d5b41b6-129a-40b1-af8b-7e8fbd4a84bb
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 783e6bc2e9dd928aaef2b5ecfb71efe47588a9b6
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-nodejs"></a>Schritt 3: Machbarkeitsnachweis Herstellen einer Verbindung mit SQL mit Node.js

![Download-nach-unten-Eingekreister](../../ssdt/media/download.png)[zum Herunterladen der Node.js SQL-Treiber](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

In diesem Beispiel soll ein Proof of Concept nur berücksichtigt werden.  Der Beispielcode ist aus Gründen der Übersichtlichkeit vereinfacht und von Microsoft empfohlene bewährte Methoden stellt nicht notwendigerweise dar. Andere Beispiele, die die gleiche entscheidenden Funktion verwenden, sind auf Github verfügbar:

- [https://github.com/tediousjs/tedious/BLOB/Master/Examples/](https://github.com/tediousjs/tedious/blob/master/examples/)
  
## <a name="step-1-connect"></a>Schritt 1: Verbinden  
  
Die **neue Verbindung** Funktion dient zum Herstellen einer SQL-Datenbank.  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        userName: 'yourusername',  
        password: 'yourpassword',  
        server: 'yourserver.database.windows.net',  
        // If you are on Microsoft Azure, you need this:  
        options: {encrypt: true, database: 'AdventureWorks'}  
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
    // If no error, then good to proceed.  
        console.log("Connected");  
    });  
```  
  
## <a name="step-2--execute-a-query"></a>Schritt 2: Ausführen einer Abfrage  
  
  
Alle SQL-Anweisungen werden ausgeführt, mit der **neue Request()** Funktion. Wenn die Anweisung Zeilen, z. B. eine select-Anweisung zurückgegeben werden können Sie abrufen, diese mithilfe der **request.on()** Funktion. Wenn keine Zeilen vorhanden sind, gibt die Funktion request.on() leere Listen zurück.  
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        userName: 'yourusername',  
        password: 'yourpassword',  
        server: 'yourserver.database.windows.net',  
        // When you connect to Azure SQL Database, you need these next options.  
        options: {encrypt: true, database: 'AdventureWorks'}  
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement();  
    });  
  
    var Request = require('tedious').Request;  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement() {  
        request = new Request("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;", function(err) {  
        if (err) {  
            console.log(err);}  
        });  
        var result = "";  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                result+= column.value + " ";  
              }  
            });  
            console.log(result);  
            result ="";  
        });  
  
        request.on('done', function(rowCount, more) {  
        console.log(rowCount + ' rows returned');  
        });  
        connection.execSql(request);  
    }  
```  
  
## <a name="step-3-insert-a-row"></a>Schritt 3: Einfügen einer Zeile  
  
In diesem Beispiel wird gezeigt, wie zum Ausführen einer [einfügen](/sql-docs/docs/t-sql/statements/insert-transact-sql) Anweisung sicher, übergeben von Parametern die schützen Ihre Anwendung von [SQL Injection](/sql-docs/docs/relational-databases/tables/primary-and-foreign-key-constraints) Wert.    
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        userName: 'yourusername',  
        password: 'yourpassword',  
        server: 'yourserver.database.windows.net',  
        // If you are on Azure SQL Database, you need these next options.  
        options: {encrypt: true, database: 'AdventureWorks'}  
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement1();  
    });  
  
    var Request = require('tedious').Request  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement1() {  
        request = new Request("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES (@Name, @Number, @Cost, @Price, CURRENT_TIMESTAMP);", function(err) {  
         if (err) {  
            console.log(err);}  
        });  
        request.addParameter('Name', TYPES.NVarChar,'SQL Server Express 2014');  
        request.addParameter('Number', TYPES.NVarChar , 'SQLEXPRESS2014');  
        request.addParameter('Cost', TYPES.Int, 11);  
        request.addParameter('Price', TYPES.Int,11);  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                console.log("Product id of inserted item is " + column.value);  
              }  
            });  
        });       
        connection.execSql(request);  
    }  
```  

