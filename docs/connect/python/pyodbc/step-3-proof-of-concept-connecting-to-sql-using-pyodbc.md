---
title: 'Schritt 3: Machbarkeitsnachweis Herstellen einer Verbindung mit SQL Pyodbc mit | Microsoft Docs'
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: python
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: ae1fc34c07fe85e8ecea70f9cc582d2d7908676e
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Schritt 3: Machbarkeitsnachweis Herstellen einer Verbindung mit SQL mit pyodbc

In diesem Beispiel soll ein Proof of Concept nur berücksichtigt werden.  Der Beispielcode ist aus Gründen der Übersichtlichkeit vereinfacht und von Microsoft empfohlene bewährte Methoden stellt nicht notwendigerweise dar.  

**Führen Sie die folgenden Beispielskript** erstellen Sie eine Datei namens test.py, und fügen Sie jeden Codeausschnitt aus, wie Sie fortfahren. 

```
> python test.py
```
  
## <a name="step-1--connect"></a>Schritt 1: Verbinden  
  
```python

import pyodbc 
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 13 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()

```  
  
  
## <a name="step-2--execute-query"></a>Schritt 2: Ausführen der Abfrage  
  
Die cursor.executefunction kann verwendet werden, um ein Resultset aus einer Abfrage an SQL-Datenbank abzurufen. Diese Funktion ist im Wesentlichen akzeptiert jede Abfrage und gibt ein Resultset, das mit der Verwendung von cursor.fetchone() durchlaufen werden können
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>Schritt 3: Einfügen einer Zeile  
  
In diesem Beispiel wird gezeigt, wie zum Ausführen einer [einfügen](../../../t-sql/statements/insert-transact-sql.md) Anweisung sicher, übergeben von Parametern die schützen Ihre Anwendung von [SQL Injection](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) Wert.    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  
  `      
  ## <a name="next-steps"></a>Nächste Schritte  
  
Weitere Informationen finden Sie unter der [Python Developer Center](https://azure.microsoft.com/en-us/develop/python/).

