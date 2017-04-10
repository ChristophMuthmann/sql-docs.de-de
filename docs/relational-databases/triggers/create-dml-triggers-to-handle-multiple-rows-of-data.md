---
title: "Erstellen von DML-Triggern f&#252;r die Verarbeitung mehrerer Datenzeilen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-dml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Mehrzeilige DML-Trigger"
  - "UPDATE-Anweisung [SQL Server], DML-Trigger"
  - "DELETE-Anweisung [SQL Server], DML-Trigger"
  - "Mehrzeilige DML-Trigger [SQL Server]"
  - "INSERT-Anweisung [SQL Server], DML-Trigger"
  - "DML-Trigger, mehrzeilig"
ms.assetid: d476c124-596b-4b27-a883-812b6b50a735
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Erstellen von DML-Triggern f&#252;r die Verarbeitung mehrerer Datenzeilen
  Wenn Sie den Code für einen DML-Trigger schreiben, sollten Sie berücksichtigen, dass es sich bei der Anweisung, die zum Auslösen des Triggers führt, um eine einzelne Anweisung handeln kann, die sich jedoch nicht nur auf eine einzelne Zeile, sondern auf mehrere Datenzeilen auswirkt. Dieses Verhalten trifft häufig auf UPDATE- und DELETE-Trigger zu, da sich diese Anweisungen oft auf mehrere Zeilen auswirken. Eher ungewöhnlich ist dieses Verhalten für INSERT-Trigger, da durch die einfache INSERT-Anweisung nur eine einzelne Zeile hinzugefügt wird. Da ein INSERT-Trigger jedoch durch eine INSERT INTO (*table_name*) SELECT-Anweisung ausgelöst werden kann, kann die Einfügung mehrerer Zeilen zum Aufruf eines einzelnen Triggers führen.  
  
 Die Berücksichtigung mehrzeiliger Operationen ist insbesondere dann wichtig, wenn ein Trigger dazu dient, zusammenfassende Werte für eine Tabelle automatisch neu zu berechnen und die Ergebnisse in einer anderen Tabelle zu speichern, um weitere Berechnungen durchführen zu können.  
  
> [!NOTE]  
>  Die Verwendung von Cursorn in Triggern wird nicht empfohlen, weil dies möglicherweise die Leistung beeinträchtigen kann. Verwenden Sie statt Cursorn rowsetbasierte Logik, um einen Trigger zu erstellen, der sich auf mehrere Zeilen auswirkt.  
  
## Beispiele  
 Die DML-Trigger in den folgenden Beispielen dienen dazu, die laufende Summe einer Spalte in einer anderen Tabelle der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank zu speichern.  
  
### A. Speichern einer laufenden Summe für die Einfügung einer einzelnen Zeile  
 Die erste Version des Triggers funktioniert für die Einfügung einer einzelnen Zeile ordnungsgemäß, wenn eine Datenzeile in die `PurchaseOrderDetail`-Tabelle geladen wird. Der DML-Trigger wird durch eine INSERT-Anweisung ausgelöst, und die neue Zeile wird für die Dauer der Triggerausführung in die **inserted** -Tabelle geladen. Die `UPDATE` -Anweisung liest den Wert der `LineTotal` -Spalte für diese Zeile und addiert ihn zu dem vorhandenen Wert in der `SubTotal` -Spalte in der `PurchaseOrderHeader` -Tabelle. Durch die `WHERE` -Klausel wird sichergestellt, dass die aktualisierte Zeile in der `PurchaseOrderDetail` -Tabelle mit der `PurchaseOrderID` der Zeile in der **inserted** -Tabelle übereinstimmt.  
  
```  
-- Trigger is valid for single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID ;  
```  
  
### B. Speichern einer laufenden Summe für die Einfügung mehrerer Zeilen oder einer einzelnen Zeile  
 Falls mehrere Zeilen eingefügt werden, funktioniert der DML-Trigger in Beispiel A möglicherweise nicht ordnungsgemäß; der Ausdruck auf der rechten Seite eines Zuweisungsausdrucks in einer UPDATE-Anweisung (`SubTotal` + `LineTotal`) kann nur einem einzelnen Wert und nicht einer Liste von Werten entsprechen. Die Auswirkung des Triggers kann somit folgendermaßen beschrieben werden: Er ruft einen Wert aus einer einzelnen Zeile in der **inserted** -Tabelle ab und fügt diesen Wert dem vorhandenen Wert von `SubTotal` in der `PurchaseOrderHeader` -Tabelle für einen bestimmten `PurchaseOrderID` -Wert hinzu. Dieses Verfahren führt möglicherweise nicht zum beabsichtigten Ergebnis, wenn ein einzelner `PurchaseOrderID` -Wert mehrmals in der **inserted** -Tabelle enthalten ist.  
  
 Damit die `PurchaseOrderHeader` -Tabelle ordnungsgemäß aktualisiert wird, muss der Trigger die Möglichkeit mehrerer Zeilen in der **inserted** -Tabelle berücksichtigen. Sie können zu diesem Zweck die `SUM` -Funktion verwenden, die die Gesamtsumme für `LineTotal` für eine Gruppe von Zeilen in der **inserted** -Tabelle für jede `PurchaseOrderID`berechnet. Die `SUM`-Funktion ist in einer korrelierten Unterabfrage (der `SELECT`-Anweisung in Klammern) enthalten. Die Unterabfrage gibt einen einzelnen Wert für jede `PurchaseOrderID` in der **inserted** -Tabelle zurück, die einer `PurchaseOrderID` in der `PurchaseOrderHeader` -Tabelle entspricht oder mit dieser korreliert.  
  
```  
-- Trigger is valid for multirow and single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail2  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted);  
```  
  
 Dieser Trigger kann auch für die Einfügung einer einzelnen Zeile ordnungsgemäß funktionieren, da in diesem Fall die Summe der `LineTotal`-Wertspalte der Summe einer einzelnen Zeile entspricht. Mit diesem Trigger ist jedoch für die korrelierte Unterabfrage und den `IN`-Operator, die in der `WHERE`-Klausel verwendet werden, weitere Verarbeitung durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erforderlich. Dies ist für das Einfügen einer einzelnen Zeile überflüssig.  
  
### C. Speichern einer laufenden Summe in Abhängigkeit von der Einfügungsart  
 Sie können den Trigger so ändern, dass er die Methode verwendet, die für die jeweilige Zeilenanzahl am besten geeignet ist. So kann z. B. mithilfe der `@@ROWCOUNT`-Funktion in der Triggerlogik zwischen der Einfügung einer einzelnen Zeile und der Einfügung mehrerer Zeilen unterschieden werden.  
  
```  
-- Trigger valid for multirow and single row inserts  
-- and optimal for single row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail3  
ON Purchasing.PurchaseOrderDetail  
FOR INSERT AS  
IF @@ROWCOUNT = 1  
BEGIN  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
END  
ELSE  
BEGIN  
      UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted)  
END;  
```  
  
## Siehe auch  
 [DML-Trigger](../../relational-databases/triggers/dml-triggers.md)  
  
  