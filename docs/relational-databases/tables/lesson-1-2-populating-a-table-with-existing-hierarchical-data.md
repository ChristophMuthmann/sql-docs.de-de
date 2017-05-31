---
title: "Auffüllen einer Tabelle mit vorhandenen hierarchischen Daten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- HierarchyID
ms.assetid: fd943d84-dbe6-4a05-912b-c88164998d80
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4569fb3f5bc56d04624756eb3fccba8da1d4ad2f
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-1-2---populating-a-table-with-existing-hierarchical-data"></a>Lektion 1-2 – Auffüllen einer Tabelle mit vorhandenen hierarchischen Daten
In dieser Aufgabe wird eine neue Tabelle erstellt und mit den Daten aus der Tabelle **EmployeeDemo** aufgefüllt. Diese Aufgabe umfasst die folgenden Schritte:  
  
-   Erstellen Sie eine neue Tabelle, die eine **hierarchyid** -Spalte enthält. Diese Spalte könnte die vorhandenen Spalten **EmployeeID** und **ManagerID** ersetzen. Sie behalten diese Spalten jedoch bei, weil bestehende Anwendungen möglicherweise auf diese Spalten verweisen und weil dann die Daten nach der Übertragung leichter verständlich sind. Gemäß der Tabellendefinition ist **OrgNode** der Primärschlüssel, so dass diese Spalte eindeutige Werte enthalten muss. Der gruppierte Index der Spalte **OrgNode** speichert das Datum in **OrgNode** -Sequenz.  
  
-   Erstellen Sie eine temporäre Tabelle, mit deren Hilfe verfolgt wird, wie viele Mitarbeiter jedem Manager direkt unterstellt sind.  
  
-   Füllen Sie die neue Tabelle mit Daten aus der Tabelle **EmployeeDemo** auf.  
  
### <a name="to-create-a-new-table-named-neworg"></a>So erstellen Sie eine neue Tabelle namens NewOrg  
  
-   Führen Sie in einem Abfrage-Editorfenster den folgenden Code aus, um eine einfache Tabelle namens **HumanResources.NewOrg**zu erstellen.  
  
    ```  
    CREATE TABLE NewOrg  
    (  
      OrgNode hierarchyid,  
      EmployeeID int,  
      LoginID nvarchar(50),  
      ManagerID int  
    CONSTRAINT PK_NewOrg_OrgNode  
      PRIMARY KEY CLUSTERED (OrgNode)  
    );  
    GO  
    ```  
  
### <a name="to-create-a-temporary-table-named-children"></a>So erstellen Sie eine temporäre Tabelle namens #Children  
  
1.  Erstellen Sie eine temporäre Tabelle namens **#Children** mit einer Spalte namens **Num** , in der für jeden Knoten die Anzahl der untergeordneten Elemente verzeichnet wird:  
  
    ```  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  Fügen Sie einen Index hinzu, der die Abfrage, mit der die Tabelle **NewOrg** aufgefüllt wird, erheblich beschleunigt:  
  
    ```  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="to-populate-the-neworg-table"></a>So füllen Sie die Tabelle NewOrg auf  
  
1.  In rekursiven Abfragen sind Unterabfragen mit Aggregaten nicht zulässig. Füllen Sie die Tabelle **#Children** stattdessen mit folgendem Code auf, in dem die [ROW_NUMBER()](../../t-sql/functions/row-number-transact-sql.md) -Methode zum Auffüllen der Spalte **Num** verwendet wird:  
  
    ```  
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM EmployeeDemo  
    GO  
  
    ```  
  
2.  Überprüfen Sie die Tabelle **#Children** . Die Spalte **Num** enthält fortlaufende Nummern für die einzelnen Manager.  
  
    ```  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    `EmployeeID ManagerID Num`  
  
    `---------- --------- ---`  
  
    `1        NULL       1`  
  
    `2         1         1`  
  
    `3         1         2`  
  
    `4         2         1`  
  
    `5         2         2`  
  
    `6         2         3`  
  
    `7         3         1`  
  
    `8         3         2`  
  
    `9         4         1`  
  
    `10        4         2`  
  
3.  Füllen Sie die Tabelle **NewOrg** auf. Verwenden Sie die Methoden GetRoot und ToString, um die Werte der Spalte **Num** zu verketten, so dass sie dem **hierarchyid** -Format entsprechen, und aktualisieren Sie anschließend die Spalte **OrgNode** mit den resultierenden hierarchischen Werten:  
  
    ```  
    WITH paths(path, EmployeeID)   
    AS (  
    -- This section provides the value for the root of the hierarchy  
    SELECT hierarchyid::GetRoot() AS OrgNode, EmployeeID   
    FROM #Children AS C   
    WHERE ManagerID IS NULL   
  
    UNION ALL   
    -- This section provides values for all nodes except the root  
    SELECT   
    CAST(p.path.ToString() + CAST(C.Num AS varchar(30)) + '/' AS hierarchyid),   
    C.EmployeeID  
    FROM #Children AS C   
    JOIN paths AS p   
       ON C.ManagerID = P.EmployeeID   
    )  
    INSERT NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO  
  
    ```  
  
4.  Eine **hierarchyid** -Spalte ist verständlicher, wenn sie in das Zeichenformat konvertiert wird. Überprüfen Sie die Daten der Tabelle **NewOrg** , indem Sie den folgenden Code ausführen, der zwei Darstellungen der Spalte **OrgNode** enthält:  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM NewOrg   
    ORDER BY LogicalNode;  
    GO  
  
    ```  
  
    Die Spalte **LogicalNode** konvertiert die **hierarchyid** -Spalte in ein lesbareres Textformat, das die Hierarchie darstellt. In den restlichen Aufgaben werden Sie die `ToString()` -Methode verwenden, um die **hierarchyid** -Spalten im logischen Format anzuzeigen.  
  
5.  Löschen Sie die temporäre Tabelle, die nicht mehr benötigt wird:  
  
    ```  
    DROP TABLE #Children  
    GO  
    ```  
  
In der nächsten Aufgabe werden Indizes erstellt, um die hierarchische Struktur zu unterstützen.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Optimieren der NewOrg-Tabelle](../../relational-databases/tables/lesson-1-3-optimizing-the-neworg-table.md)  
  
  
  

