---
title: "Verwenden der Tabellen „inserted“ und „deleted“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inserted tables
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- INSTEAD OF triggers
- deleted tables
- INSERT statement [SQL Server], DML triggers
- DML triggers, deleted or inserted tables
ms.assetid: ed84567f-7b91-4b44-b5b2-c400bda4590d
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f7b04d0977ceaa1bde5eddf5246be56822517e84
ms.lasthandoff: 04/11/2017

---
# <a name="use-the-inserted-and-deleted-tables"></a>Verwenden der Tabellen inserted und deleted
  DML-Triggeranweisungen verwenden zwei besondere Tabellen: die inserted-Tabelle und die deleted-Tabelle. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt und verwendet diese Tabellen automatisch. Sie können diese temporären, speicherresidenten Tabellen verwenden, um die Auswirkungen bestimmter Datenänderungen zu testen und Bedingungen für DML-Triggeraktionen festzulegen. Das direkte Ändern der Daten in den Tabellen bzw. das Ausführen von Data Definition Language-(DDL-)Vorgängen für die Tabellen, beispielsweise CREATE INDEX, ist nicht möglich.  
  
 In DML-Triggern werden die Tabellen inserted und deleted hauptsächlich für folgende Vorgänge verwendet:  
  
-   Erweitern der referenziellen Integrität zwischen Tabellen.  
  
-   Einfügen oder Aktualisieren von Daten in Basistabellen, die einer Sicht zugrunde liegen.  
  
-   Testen im Hinblick auf Fehler und Ausführen der entsprechenden Vorgänge.  
  
-   Ermitteln des Unterschieds zwischen dem Tabellenstatus vor und nach einer Datenänderung und Ausführen von Aktionen, die auf diesem Unterschied basieren  
  
 In der deleted-Tabelle werden Kopien der von DELETE- und UPDATE-Anweisungen betroffenen Zeilen gespeichert. Während der Ausführung einer DELETE- oder UPDATE-Anweisung werden Zeilen aus der Triggertabelle gelöscht und in die deleted-Tabelle übertragen. Die deleted-Tabelle und die Triggertabelle enthalten normalerweise nicht die gleichen Zeilen.  
  
 In der inserted-Tabelle werden Kopien der durch INSERT- und UPDATE-Anweisungen betroffenen Zeilen gespeichert. Während einer Einfügungs- oder Updatetransaktion werden neue Zeilen sowohl der inserted-Tabelle als auch der Triggertabelle hinzugefügt. Die Zeilen in der inserted-Tabelle sind Kopien der neuen Zeilen in der Triggertabelle.  
  
 Eine Updatetransaktion entspricht einem Löschvorgang mit anschließender Einfügung; die alten Zeilen werden zunächst in die deleted-Tabelle kopiert, und anschließend werden die neuen Zeilen in die Triggertabelle und die inserted-Tabelle kopiert.  
  
 Wenn Sie Triggerbedingungen festlegen, sollten Sie die inserted- und die deleted-Tabelle entsprechend der Aktion verwenden, die den Trigger ausgelöst hat. Es wird zwar kein Fehler ausgegeben, wenn Sie beim Testen einer INSERT-Anweisung auf die deleted-Tabelle oder beim Testen einer DELETE-Anweisung auf die inserted-Tabelle verweisen, diese Triggertesttabellen enthalten jedoch in diesen Fällen keine Zeilen.  
  
> [!NOTE]  
>  Wenn Triggeraktionen von der Anzahl der Zeilen abhängen, die von einer Datenänderung betroffen sind, sollten Sie Tests verwenden (z.B. die Untersuchung von @@ROWCOUNT), die mehrzeilige Datenänderungen (eine INSERT-, DELETE- oder UPDATE-Anweisung, die auf einer SELECT-Anweisung basiert) überprüfen und die entsprechenden Vorgänge ausführen.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] lässt keine Spaltenverweise vom Typ **text**, **ntext**oder **image** in der inserted- und deleted-Tabelle für AFTER-Trigger zu. Diese Datentypen sind jedoch nur aus Gründen der Abwärtskompatibilität eingeschlossen. Speichern Sie umfangreiche Daten bevorzugt mit den Datentypen **varchar(max)**, **nvarchar(max)**und **varbinary(max)** . Sowohl AFTER- als auch INSTEAD OF-Trigger unterstützen **varchar(max)**-, **nvarchar(max)**- und **varbinary(max)**-Daten in der inserted- und deleted-Tabelle. Weitere Informationen finden Sie unter [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 **Beispiel für die Verwendung der inserted-Tabelle in einem Trigger zum Erzwingen einer Geschäftsregel**  
  
 Da sich CHECK-Einschränkungen nur auf Spalten beziehen können, für die die Einschränkung auf Spalten- oder Tabellenebene definiert wurde, müssen tabellenübergreifende Einschränkungen (in diesem Fall Geschäftsregeln) als Trigger definiert werden.  
  
 Im folgenden Beispiel wird ein DML-Trigger erstellt. Der Trigger überprüft die Bonität eines Herstellers, wenn versucht wird, eine neue Bestellung in die `PurchaseOrderHeader` -Tabelle einzufügen. Zum Ermitteln der Bonität des Herstellers im Zusammenhang mit der gerade eingefügten Bestellung muss auf die `Vendor` -Tabelle verwiesen und diese mit der inserted-Tabelle verknüpft werden. Ist die Bonität zu niedrig, wird eine Meldung angezeigt, und die Bestellung wird nicht eingefügt. Bitte beachten Sie, dass in diesem Beispiel multirow-Datenänderungen nicht berücksichtigt werden. Weitere Informationen finden Sie unter [Create DML Triggers to Handle Multiple Rows of Data](../../relational-databases/triggers/create-dml-triggers-to-handle-multiple-rows-of-data.md).  
  
 [!code-sql[TriggerDDL#CreateTrigger3](../../relational-databases/triggers/codesnippet/tsql/use-the-inserted-and-del_1.sql)]  
  
## <a name="using-the-inserted-and-deleted-tables-in-instead-of-triggers"></a>Verwenden der inserted- und deleted-Tabellen in INSTEAD OF-Triggern  
 Für die inserted- und deleted-Tabellen, die an für Tabellen definierte INSTEAD OF-Trigger übergeben werden, gelten dieselben Regeln wie für die inserted- und deleted-Tabellen, die an AFTER-Trigger übergeben werden. Das Format der inserted- und deleted-Tabellen ist mit dem Format der Tabelle identisch, für die der INSTEAD OF-Trigger definiert wurde. Jede Spalte in den inserted- und deleted-Tabellen ist direkt einer Spalte in der Basistabelle zugeordnet.  
  
 Für die Frage, wann eine INSERT- oder UPDATE-Anweisung, die auf eine Tabelle mit einem INSTEAD OF-Trigger verweist, Werte für Spalten angeben muss, gelten dieselben Regeln, wie wenn in der Tabelle kein INSTEAD OF-Trigger vorhanden wäre:  
  
-   Für berechnete Spalten oder Spalten mit einem **timestamp** -Datentyp können keine Werte angegeben werden.  
  
-   Für Spalten mit einer IDENTITY-Eigenschaft können nur Werte angegeben werden, wenn IDENTITY_INSERT für diese Tabelle auf ON festgelegt ist. Wenn IDENTITY_INSERT auf ON festgelegt ist, müssen INSERT-Anweisungen einen Wert angeben.  
  
-   INSERT-Anweisungen müssen Werte für alle NOT NULL-Spalten angeben, die keine DEFAULT-Einschränkungen aufweisen.  
  
-   Außer in berechneten Spalten, Identitätsspalten oder **timestamp** -Spalten sind Werte für alle Spalten, die NULL-Werte zulassen, oder für alle NOT NULL-Spalten optional, die eine DEFAULT-Definition aufweisen.  
  
 Wenn eine INSERT-, UPDATE- oder DELETE-Anweisung auf eine Sicht verweist, die einen INSTEAD OF-Trigger aufweist, ruft [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Trigger auf, anstatt direkte Aktionen für Tabellen auszuführen. Der Trigger muss anhand der in den inserted- und deleted-Tabellen dargestellten Informationen Anweisungen erstellen, die zum Implementieren der angeforderten Aktion in den Basistabellen erforderlich sind, selbst wenn das Format der für die Sicht erstellten Informationen in den inserted- und deleted-Tabellen nicht mit dem Format der Daten in den Basistabellen identisch ist.  
  
 Das Format der inserted- und deleted-Tabellen, das an einen in einer Sicht definierten INSTEAD OF-Trigger übergeben wird, stimmt mit der Auswahlliste der SELECT-Anweisung überein, die für die Sicht definiert wurde. Beispiel:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.EmployeeNames (BusinessEntityID, LName, FName)  
AS  
SELECT e.BusinessEntityID, p.LastName, p.FirstName  
FROM HumanResources.Employee AS e   
JOIN Person.Person AS p  
ON e.BusinessEntityID = p.BusinessEntityID;  
```  
  
 Das Resultset für diese Sicht weist drei Spalten auf: eine **int** -Spalte und zwei **nvarchar** -Spalten. Die inserted-Tabelle und die deleted-Tabelle, die an einen für die Sicht definierten INSTEAD OF-Trigger übergeben werden, enthalten ebenfalls eine **int** -Spalte mit der Bezeichnung `BusinessEntityID`, eine **nvarchar** -Spalte mit der Bezeichnung `LName`und eine **nvarchar** -Spalte mit der Bezeichnung `FName`.  
  
 Die Auswahlliste einer Sicht kann auch Ausdrücke aufweisen, die nicht direkt einer einzigen Basistabellenspalte zugeordnet sind. Einige Sichtausdrücke, z. B. Konstanten- oder Funktionsaufrufe, verweisen möglicherweise nicht auf Spalten und können deshalb ignoriert werden. Komplexe Ausdrücke können auf mehrere Spalten verweisen, aber die inserted- und deleted-Tabellen enthalten für jede eingefügte Zeile nur einen einzigen Wert. Dasselbe gilt für einfache Ausdrücke in einer Sicht, wenn sie auf eine berechnete Spalte mit einem komplexen Ausdruck verweisen. Ein INSTEAD OF-Trigger in der Sicht muss diese Ausdruckstypen verarbeiten.  
  
  
