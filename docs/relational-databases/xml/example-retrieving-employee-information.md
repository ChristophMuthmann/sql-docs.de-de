---
title: 'Beispiel: Abrufen von Informationen zu Mitarbeitern | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EXPLICIT mode
ms.assetid: 63cd6569-2600-485b-92b4-1f6ba09db219
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c3c7b4150738ac5dbf878014004c3bda20092e33
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="example-retrieving-employee-information"></a>Beispiel: Abrufen von Informationen zu Mitarbeitern
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
In diesem Beispiel werden die ID und der Name jedes Mitarbeiters abgerufen. In der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank kann employeeID aus der BusinessEntityID-Spalte in der Employee-Tabelle abgerufen werden. Die Namen der Mitarbeiter werden aus der Person-Tabelle abgerufen. Die BusinessEntityID-Spalte kann zum Join der Tabellen verwendet werden.  
  
 Angenommen, Sie möchten mithilfe einer FOR XML EXPLICIT-Transformation ein XML-Dokument generieren, wie im Folgenden gezeigt:  
  
```  
<Employee EmpID="1" >  
  <Name FName="Ken" LName="Sánchez" />  
</Employee>  
...  
```  
  
 Nachdem die Hierarchie zwei Ebenen aufweist, schreiben Sie zwei `SELECT`-Abfragen und wenden UNION ALL an. Im Folgenden wird die erste Abfrage gezeigt, die die Werte für das <`Employee`>-Element sowie dessen Attribute abruft. In der Abfrage wird dem <`Employee`>-Element der `1`-Wert `Tag` und der `Parent`-Wert NULL zugewiesen, da es sich um das Element auf oberster Ebene handelt.  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID AS [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 Im Folgenden wird die zweite Abfrage gezeigt. Sie ruft die Werte für das <`Name`>-Element ab. In der Abfrage wird dem <`2`>-Element der `Tag`-Wert `Name` und der `1`-Tagwert  `Parent` zugewiesen, wodurch <`Employee`> als übergeordnetes Element identifiziert wird.  
  
```  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 Kombinieren Sie diese Abfragen nun mit `UNION AL`L, wenden Sie `FOR XML EXPLICIT` an, und geben Sie die erforderliche `ORDER BY`-Klausel an. Sie müssen das Rowset zuerst nach `BusinessEntityID` und dann nach Namen sortieren, sodass die NULL-Werte in den Namen an erster Stelle aufgeführt werden. Führen Sie die folgende Abfrage ohne FOR XML-Klausel aus, um die generierte Universaltabelle anzuzeigen.  
  
 So sieht die endgültige Abfrage aus:  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID as [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
ORDER BY [Employee!1!EmpID],[Name!2!FName]  
FOR XML EXPLICIT;  
```  
  
 Dies ist das Teilergebnis:  
  
 `<Employee EmpID="1">`  
  
 `<Name FName="Ken" LName="Sánchez" />`  
  
 `</Employee>`  
  
 `<Employee EmpID="2">`  
  
 `<Name FName="Terri" LName="Duffy" />`  
  
 `</Employee>`  
  
 `...`  
  
 Die erste `SELECT` -Anweisung gibt die Spaltennamen des Rowsets des Ergebnisses an. Diese Namen bilden zwei Spaltengruppen. Die Gruppe mit dem `Tag`-Wert `1` im Spaltennamen identifiziert `Employee` als Element und `EmpID` als Attribut. Die andere Spaltengruppe besitzt den `Tag`-Wert `2` im Spaltennamen und identifiziert <`Name`> als Element und `FName` und `LName` als Attribute.  
  
 In der folgenden Tabelle wird das von der Abfrage generierte partielle Rowset gezeigt:  
  
 `Tag Parent  Employee!1!EmpID Name!2!FName Name!2!LName`  
  
 `--- ------  ---------------- ------------ ------------`  
  
 `1   NULL    1                NULL         NULL`  
  
 `2   1       1                Ken          Sánchez`  
  
 `1   NULL    2                NULL         NULL`  
  
 `2   1       2                Terri        Duffy`  
  
 `1   NULL    3                NULL         NULL`  
  
 `2   1       3                Roberto      Tamburello`  
  
 `...`  
  
 Die Zeilen in der Universaltabelle werden auf folgende Weise verarbeitet, um die resultierende XML-Struktur zu erzeugen:  
  
 Die erste Zeile identifiziert den `Tag` -Wert `1`. Deshalb wird die Spaltengruppe, die über den `Tag` -Wert `1` verfügt, als `Employee!1!EmpID`identifiziert. Diese Spalte identifiziert `Employee` als Elementname. Ein <`Employee`>-Element mit `EmpID`-Attributen wird nun erstellt. Diesen Attributen werden entsprechende Spaltenwerte zugewiesen.  
  
 Die zweite Zeile verfügt über den `Tag` -Wert `2`. Daher wird die Spaltengruppe, die im Spaltennamen über den `Tag` -Wert `2` verfügt, als `Name!2!FName`, `Name!2!LName`identifiziert. Diese Spaltennamen identifizieren `Name` als Elementname. Ein <`Name`>-Element mit `FName`- und `LName`-Attributen wird nun erstellt. Diesen Attributen werden entsprechende Spaltenwerte zugewiesen. Diese Zeile identifiziert `1` als `Parent`-Element. Dieses untergeordnete Element wird dem vorhergehenden <`Employee`>-Element hinzugefügt.  
  
 Dieser Prozess wird für die restlichen Zeilen des Rowsets wiederholt. Beachten Sie, dass die Anordnung der Zeilen in der Universaltabelle wichtig ist, damit FOR XML EXPLICIT das Rowset in der richtigen Reihenfolge verarbeitet und die erwünschte XML-Ausgabe generiert.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwenden des EXPLICIT-Modus mit FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
