---
title: Untersuchen der aktuellen Struktur der Mitarbeitertabelle | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- examining the current structure of the employee
ms.assetid: d546a820-105a-417d-ac35-44a6d1d70ac6
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fa6d4693132ec646438ab7cd0f45f85569c4109f
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="lesson-1-1---examining-the-current-structure-of-the-employee-table"></a>Lesson 1-1 – Untersuchen der aktuellen Struktur der Mitarbeitertabelle
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
Die Beispieldatenbank von [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] (oder höher) enthält eine **Employee**-Tabelle im Schema **HumanResources**. Um Änderungen an der ursprünglichen Tabelle zu vermeiden, wird in diesem Schritt eine Kopie der Tabelle **Employee** mit dem Namen **EmployeeDemo**erstellt. Um das Beispiel zu vereinfachen, kopieren Sie nur fünf Spalten aus der ursprünglichen Tabelle. Dann fragen Sie die Tabelle **HumanResources.EmployeeDemo** ab, um zu sehen, wie die Daten in einer Tabelle strukturiert werden, wenn der **hierarchyid** -Datentyp nicht verwendet wird.  
  
### <a name="to-copy-the-employee-table"></a>So kopieren Sie die Mitarbeitertabelle  
  
1.  Führen Sie in einem Abfrage-Editorfenster den folgenden Code aus, um die Tabellenstruktur und die Daten der Tabelle **Employee** in eine neue Tabelle namens **EmployeeDemo**zu kopieren. Da die ursprüngliche Tabelle bereits HierarchyID verwendet, vereinfacht diese Abfrage die Hierarchie, um den Manager des Mitarbeiters abzurufen. Im weiteren Verlauf dieser Lektion rekonstruieren Sie diese Hierarchie.
  
    ```  
    USE AdventureWorks ;  
    GO  
  
    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
      (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
            WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
                (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID
        , emp.JobTitle, emp.HireDate
    INTO HumanResources.EmployeeDemo   
    FROM HumanResources.Employee emp ;
    GO
    ```  
  
### <a name="to-examine-the-structure-and-data-of-the-employeedemo-table"></a>So untersuchen Sie die Struktur und die Daten der Tabelle EmployeeDemo  
  
-   Die neue Tabelle **EmployeeDemo** stellt eine typische Tabelle einer vorhandenen Datenbank dar, die in eine neue Struktur migriert werden soll. Führen Sie in einem Abfrage-Editorfenster den folgenden Code aus, um zu zeigen, wie die Mitarbeiter-Manager-Beziehungen mithilfe eines Selbstjoins dargestellt werden:  
  
    ```  
    SELECT   
        Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
        Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.JobTitle  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  JobTitle  
    NULL    NULL    1   adventure-works\ken0    Chief Executive Officer
    1   adventure-works\ken0    2   adventure-works\terri0  Vice President of Engineering
    1   adventure-works\ken0    16  adventure-works\david0  Marketing Manager
    1   adventure-works\ken0    25  adventure-works\james1  Vice President of Production
    1   adventure-works\ken0    234 adventure-works\laura1  Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0   Information Services Manager
    1   adventure-works\ken0    273 adventure-works\brian3  Vice President of Sales
    2   adventure-works\terri0  3   adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0    Senior Tool Designer
    ...  
    ```  
  
    Die Ausgabe umfasst insgesamt 290 Zeilen.  
  
Beachten Sie, dass die **ORDER BY** -Klausel bewirkt, dass die Mitarbeiter, die einer Managementebene direkt unterstellt sind, jeweils zusammen aufgelistet werden. So werden beispielsweise die sieben Mitarbeiter, die **MgrID** 1 (ken0) direkt unterstellt sind, nebeneinander aufgeführt. Es ist zwar nicht unmöglich, aber sehr viel schwieriger, alle Mitarbeiter zu gruppieren, die **MgrID** 1 auch indirekt unterstellt sind.  
  
In der nächsten Aufgabe erstellen Sie eine neue Tabelle mit dem **hierarchyid** -Datentyp und verschieben die Daten in diese neue Tabelle.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
[Auffüllen einer Tabelle mit vorhandenen hierarchischen Daten](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
  
  
