---
title: 'Schritt 3: Machbarkeitsnachweis Herstellen einer Verbindung mit SQL Ruby mit | Microsoft Docs'
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ruby
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 445782c1958ee5344f64b365dd81725c5ac8e6f6
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>Schritt 3: Machbarkeitsnachweis Herstellen einer Verbindung mit SQL mit Ruby

In diesem Beispiel soll ein Proof of Concept nur berücksichtigt werden.  Der Beispielcode ist aus Gründen der Übersichtlichkeit vereinfacht und von Microsoft empfohlene bewährte Methoden stellt nicht notwendigerweise dar.  
  
## <a name="step-1--connect"></a>Schritt 1: Verbinden  
  
Die [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) Funktion dient zum Herstellen einer SQL-Datenbank.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>Schritt 2: Ausführen einer Abfrage  
  
Kopieren Sie den folgenden Code in eine leere Datei. Rufen Sie diese test.rb. Dann führen sie durch Eingabe des folgenden Befehls von der Befehlszeile aus:  
  
    ruby test.rb  
  
Im Codebeispiel ist die [TinyTds::Result](https://github.com/rails-sqlserver/tiny_tds) Funktion dient zum Abrufen eines Resultsets aus einer Abfrage an SQL-Datenbank. Diese Funktion akzeptiert eine Abfrage und gibt ein Resultset zurück. Das Resultset mithilfe der Tabulatortaste durchlaufen [result.each führen | Zeile |](https://github.com/rails-sqlserver/tiny_tds).  
  
``` ruby 
    require 'tiny_tds'    
    print 'test'       
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC")  
    results.each do |row|  
    puts row  
    end  
```  
  
## <a name="step-3--insert-a-row"></a>Schritt 3: Einfügen einer Zeile  
  
In diesem Beispiel wird gezeigt, wie zum Ausführen einer [einfügen](../../t-sql/statements/insert-transact-sql.md) Anweisung sicher, übergeben von Parametern die schützen Ihre Anwendung von [SQL Injection](../../relational-databases/tables/primary-and-foreign-key-constraints.md) Wert.    
  
Um TinyTDS mit Azure verwenden, wird empfohlen, dass Sie mehrere ausführen `SET` Anweisungen zu ändern, wie die aktuelle Sitzung spezifische Informationen behandelt. Empfohlene `SET` Anweisungen werden im Codebeispiel bereitgestellt. Beispielsweise `SET ANSI_NULL_DFLT_ON` können neue Spalten erstellt, um null-Werte zulassen, selbst wenn der zulässigkeitsstatus der NULL-der Spalte nicht explizit angegeben ist.  
  
Zum Ausrichten von mit Microsoft SQL Server ["DateTime"](http://msdn.microsoft.com/library/ms187819.aspx) formatieren, verwenden Sie die [Strftime](http://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) Funktion in die entsprechende "DateTime" umgewandelt.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SET ANSI_NULLS ON")  
    results = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")  
    results = client.execute("SET ANSI_NULL_DFLT_ON ON")  
    results = client.execute("SET IMPLICIT_TRANSACTIONS OFF")  
    results = client.execute("SET ANSI_PADDING ON")  
    results = client.execute("SET QUOTED_IDENTIFIER ON")  
    results = client.execute("SET ANSI_WARNINGS ON")  
    results = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")  
    require 'date'  
    t = Time.now  
    curr_date = t.strftime("%Y-%m-%d %H:%M:%S.%L")  
    results = client.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate)  
    OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, '#{curr_date}' )")  
    results.each do |row|  
    puts row  
    end  
```

