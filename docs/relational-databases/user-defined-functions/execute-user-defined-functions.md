---
title: "Ausführen von benutzerdefinierten Funktionen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 08287922d15adabd1128da2edbb1caa65bc3f85f
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="execute-user-defined-functions"></a>Ausführen von benutzerdefinierten Funktionen
  Ausführen einer benutzerdefinierten Funktion mit Transact-SQL
  

> **Hinweis:** Weitere Informationen zu benutzerdefinierten Funktionen finden Sie unter  [Benutzerdefinierte Funktion](https://msdn.microsoft.com/library/ms191007.aspx) und [CREATE FUNCTION (Transact SQL)](https://msdn.microsoft.com/library/ms186755.aspx) . 
  
 
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 In Transact-SQL können Parameter entweder mit *value* oder mit dem Wert*parameter_name*=*value.*angegeben werden. angegeben werden. Ein Parameter ist nicht Teil einer Transaktion. Deshalb wird der Wert eines Parameters, der in einer Transaktion geändert wird, nicht wieder auf seinen ursprünglichen Wert zurückgesetzt, wenn für diese Transaktion später ein Rollback ausgeführt wird. Der Wert, der an den Aufrufer zurückgegeben wird, ist immer der Wert zu dem Zeitpunkt, zu dem das Modul beendet wird.  
  
###  <a name="Security"></a> Sicherheit  
  
 Zum Ausführen der [EXECUTE](https://msdn.microsoft.com/library/ms188332.aspx) -Anweisung sind keine Berechtigungen erforderlich. Es sind jedoch Berechtigungen für die sicherungsfähigen Elemente in der EXECUTE-Zeichenfolge **erforderlich** . Wenn z.B. die Zeichenfolge eine [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) -Anweisung enthält, benötigt der Aufrufer der EXECUTE-Anweisung die INSERT-Berechtigung für die Zieltabelle. Berechtigungen werden überprüft, wenn die EXECUTE-Anweisung erreicht wird, selbst wenn die EXECUTE-Anweisung innerhalb eines Moduls enthalten ist. Weitere Informationen finden Sie unter [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
### <a name="example"></a>Beispiel 
  
Dieses Beispiel verwendet die Skalarwertfunktion `ufnGetSalesOrderStatusText` , die in den meisten Editionen von `AdventureWorks`verfügbar ist.  Der Zweck der Funktion ist einen Textwert für den Verkaufsstatus von einer ganzen Zahl zurückzugeben.  Verändern Sie das Beispiel, indem Sie ganze Zahlen von 1 bis 7 an den **\@Status** -Parameter übergeben.
  
~~~tsql
USE [AdventureWorks2016CTP3]
GO  

-- Declare a variable to return the results of the function. 
DECLARE @ret nvarchar(15);   

-- Execute the function while passing a value to the @status parameter
EXEC @ret = dbo.ufnGetSalesOrderStatusText 
    @Status = 5; 

-- View the returned value.  The Execute and Select statements must be executed at the same time.  
SELECT N'Order Status: ' + @ret; 

-- Result:
-- Order Status: Shipped
~~~
  
  
  

