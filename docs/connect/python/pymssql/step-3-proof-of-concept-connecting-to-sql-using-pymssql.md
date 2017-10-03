---
title: 'Schritt 3: Machbarkeitsnachweis Herstellen einer Verbindung mit SQL Pymssql mit | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: f230af88796afce17b6858a7e4ac5136a04e9dd3
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>Schritt 3: Machbarkeitsnachweis Herstellen einer Verbindung mit SQL mit pymssql
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

In diesem Beispiel soll ein Proof of Concept nur berücksichtigt werden.  Der Beispielcode ist aus Gründen der Übersichtlichkeit vereinfacht und von Microsoft empfohlene bewährte Methoden stellt nicht notwendigerweise dar.  
  
## <a name="step-1--connect"></a>Schritt 1: Verbinden  
  
Die [pymssql.connect](http://pymssql.org/en/latest/ref/pymssql.html) Funktion dient zum Herstellen einer SQL-Datenbank.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>Schritt 2: Ausführen der Abfrage  
  
Die [cursor.execute](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute) Funktion kann verwendet werden, um ein Resultset aus einer Abfrage an SQL-Datenbank abzurufen. Diese Funktion ist im Wesentlichen akzeptiert jede Abfrage und gibt ein Resultset, das mit der Verwendung von durchlaufen werden kann [cursor.fetchone()](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone).  
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute('SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;')  
    row = cursor.fetchone()  
    while row:  
        print str(row[0]) + " " + str(row[1]) + " " + str(row[2])     
        row = cursor.fetchone()  
```  
  
## <a name="step-3--insert-a-row"></a>Schritt 3: Einfügen einer Zeile  
  
In diesem Beispiel wird gezeigt, wie zum Ausführen einer [einfügen](../../../t-sql/statements/insert-transact-sql.md) Anweisung sicher, übergeben von Parametern die schützen Ihre Anwendung von [SQL Injection](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) Wert.    
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express', 'SQLEXPRESS', 0, 0, CURRENT_TIMESTAMP)")  
    row = cursor.fetchone()  
    while row:  
        print "Inserted Product ID : " +str(row[0])  
        row = cursor.fetchone()  
    conn.commit()
    conn.close()
```  
  
## <a name="step-4--rollback-a-transaction"></a>Schritt 4: Rollback einer Transaktion  
  
Dieses Codebeispiel veranschaulicht die Verwendung von Transaktionen in der Sie:  
  
* Eine Transaktion starten  
* Fügen Sie eine Zeile mit Daten  
* Rollback Ihre Transaktion einfügen rückgängig machen  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("BEGIN TRANSACTION")  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, CURRENT_TIMESTAMP)")  
    conn.rollback()  
    conn.close()
```  
    
  ## <a name="next-steps"></a>Nächste Schritte  
  
Weitere Informationen finden Sie unter der [Python Developer Center](https://azure.microsoft.com/en-us/develop/python/).
