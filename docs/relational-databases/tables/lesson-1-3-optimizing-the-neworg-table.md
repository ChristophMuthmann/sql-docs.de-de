---
title: Optimieren der NewOrg-Tabelle | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
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
- optimizing tables
ms.assetid: 89ff6d37-94c0-4773-8be9-dde943fff023
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f61ee1203067cdc8793f56a1c78d68f24b0b2e9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-1-3---optimizing-the-neworg-table"></a>Lektion 1-3 – Optimieren der NewOrg-Tabelle
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
Die **NewOrd** -Tabelle, die Sie in der Aufgabe [Populating a Table with Existing Hierarchical Data](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) erstellt haben, enthält alle Angestellteninformationen und stellt die hierarchische Struktur mithilfe des **hierarchyid** -Datentyps dar. In dieser Aufgabe werden neue Indizes hinzugefügt, die das Suchen in der **hierarchyid** -Spalte unterstützen.  
  
## <a name="clustered-index"></a>Gruppierter Index  
Die Spalte **hierarchyid** (**OrgNode**) ist der Primärschlüssel für die **NewOrg** -Tabelle. Als die Tabelle erstellt wurde, enthielt sie den gruppierten Index **PK_NewOrg_OrgNode** , der die Eindeutigkeit der **OrgNode** -Spalte erzwingen sollte. Dieser gruppierte Index unterstützt auch eine Tiefensuche in der Tabelle.  
  
## <a name="nonclustered-index"></a>Nicht gruppierter Index  
Dieser Schritt erstellt zwei nicht gruppierte Indizes, um typische Suchoperationen zu unterstützen.  
  
#### <a name="to-index-the-neworg-table-for-efficient-searches"></a>So indizieren Sie die Tabelle 'NewOrg' für effiziente Suchoperationen  
  
1.  Verwenden Sie zur Unterstützung von Abfragen der gleichen Ebene in der Hierarchie die [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) -Methode, um eine berechnete Spalte zu erstellen, welche die Ebene in der Hierarchie enthält. Erstellen Sie dann für diese und die **Hierarchyid**-Spalte einen zusammengesetzten Index. Führen Sie den folgenden Code aus, um die berechnete Spalte und den Breitensuchindex zu erstellen:  
  
    ```  
    ALTER TABLE HumanResources.NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON HumanResources.NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  Erstellen Sie für die Spalte **EmployeeID** einen eindeutigen Index. Dies ist der übliche Singleton-Suchvorgang nach einem einzelnen Mitarbeiter entsprechend der **EmployeeID** -Nummer. Führen Sie den folgenden Code aus, um für **EmployeeID**einen Index zu erstellen:  
  
    ```  
    CREATE UNIQUE INDEX EmpIDs_unq ON HumanResources.NewOrg(EmployeeID) ;  
    GO
    ```  
  
3.  Fügen Sie folgenden Code aus, um die Daten der Tabelle in der Reihenfolge jedes der drei Indizes abzurufen.  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM HumanResources.NewOrg   
    ORDER BY OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY H_Level, OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  Vergleichen Sie die Resultsets, um zu sehen, wie die Reihenfolge in jedem Indextyp gespeichert wird. Im Folgenden werden nur die ersten vier Zeilen jeder Ausgabe gezeigt.  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    Tiefensuchindex: Mitarbeiterdatensätze sind angrenzend an den ihres Managers gespeichert.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    ```

    Sortiert nach **EmployeeID**: Die Zeilen werden in der Reihenfolge der **EmployeeID** gespeichert.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    /1/1/5/1/   0x5AE358    4   12  adventure-works\thierry0
    ```
  
> [!NOTE]  
> Diagramme, die den Unterschied zwischen einem Tiefensuchindex und einem Breitensuchindex zeigen, finden Sie unter [Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).  
  
#### <a name="to-drop-the-unnecessary-columns"></a>So löschen Sie die unnötigen Spalten  
  
1.  Die Spalte **ManagerID** stellt die Mitarbeiter-/Managerbeziehung dar, die jetzt von der Spalte **OrgNode** dargestellt wird. Wenn andere Anwendungen die Spalte **ManagerID** nicht benötigen, könnten Sie diese Spalte löschen, indem Sie die folgende Anweisung verwenden:  
  
    ```  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  Die Spalte **EmployeeID** ist ebenfalls überflüssig. Jeder Mitarbeiter wird bereits durch die Spalte **OrgNode** eindeutig identifiziert. Wenn andere Anwendungen die Spalte **EmployeeID** nicht benötigen, könnten Sie den Index und dann die Spalte löschen, indem Sie folgenden Code verwenden:  
  
    ```  
    DROP INDEX EmpIDs_unq ON HumanResources.NewOrg ;  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
#### <a name="to-replace-the-original-table-with-the-new-table"></a>So ersetzen Sie die ursprüngliche durch die neue Tabelle  
  
1.  Wenn die ursprüngliche Tabelle irgendwelche zusätzlichen Indizes oder Einschränkungen enthält, dann fügen Sie diese der Tabelle **NewOrg** hinzu.  
  
2.  So ersetzen Sie die alte **EmployeeDemo** -Tabelle durch die neue Tabelle. Führen Sie folgenden Code aus, um die alte Tabelle zu löschen und dann die neue Tabelle mit dem Namen der alten Tabelle zu benennen:  
  
    ```  
    DROP TABLE HumanResources.EmployeeDemo ;  
    GO  
    sp_rename 'HumanResources.NewOrg', 'EmployeeDemo' ;  
    GO  
    ```  
  
3.  Führen Sie den folgenden Code aus, um die neue Tabelle zu untersuchen:  
  
    ```  
    SELECT * FROM HumanResources.EmployeeDemo ;  
    ```  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
[Zusammenfassung: Konvertieren einer Tabelle in eine hierarchische Struktur](../../relational-databases/tables/lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
  
  
