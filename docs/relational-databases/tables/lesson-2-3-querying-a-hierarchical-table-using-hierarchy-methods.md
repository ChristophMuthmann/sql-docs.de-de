---
title: Abfragen einer hierarchischen Tabelle mit hierarchischen Methoden | Microsoft-Dokumentation
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
ms.assetid: 3b4f7dae-65b5-4d8d-8641-87aba9aa692d
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: af8bdce0dd68fbf33d364757cbb07d60054b1100
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-2-3---querying-a-hierarchical-table-using-hierarchy-methods"></a>Lektion 2.3: Abfragen einer hierarchischen Tabelle mit hierarchischen Methoden
Nachdem die Tabelle HumanResources.EmployeeOrg nun vollständig gefüllt ist, zeigt Ihnen diese Aufgabe, wie Sie die Hierarchie mithilfe einiger der hierarchischen Methoden abfragen können.  
  
### <a name="to-find-subordinate-nodes"></a>So suchen Sie untergeordnete Knoten  
  
1.  Sariya ist ein Mitarbeiter unterstellt. Um den unterstellten Mitarbeiter abzufragen, führen Sie die folgende Abfrage aus, die die [IsDescendantOf](../../t-sql/data-types/isdescendantof-database-engine.md) -Methode verwendet:  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.IsDescendantOf(@CurrentEmployee ) = 1 ;  
    ```  
  
    Das Ergebnis listet sowohl Sariya als auch Wanida auf. Sariya wird aufgelistet, weil sie Nachfolger auf Ebene 0 ist. Wanida ist Nachfolger auf Ebene 1.  
  
2.  Sie können diese Informationen auch mit der [GetAncestor](../../t-sql/data-types/getancestor-database-engine.md) -Methode abfragen. `GetAncestor` übernimmt ein Argument für die Ebene, die zurückgegeben werden soll. Da Wanida eine Ebene unter Sariya angesiedelt ist, können Sie `GetAncestor(1)` verwenden, wie der folgende Code veranschaulicht:  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @CurrentEmployee  
    ```  
  
    Dieses Mal listet das Ergebnis nur Wanida auf.  
  
3.  Ändern Sie jetzt `@CurrentEmployee` in David (EmployeeID 6) und die Ebene in 2. Führen Sie folgenden Code aus, um auch Wanida zurückzugeben:  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
    Dieses Mal erhalten Sie auch Mary, die, zwei Ebenen darunter, ebenfalls David unterstellt ist.  
  
### <a name="to-use-getroot-and-getlevel"></a>So verwenden Sie 'GetRoot' und 'GetLevel'  
  
1.  Mit dem Anwachsen der Hierarchie wird es schwieriger zu ermitteln, wo innerhalb der Hierarchie sich die Elemente befinden. Verwenden Sie die [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) -Methode, um zu ermitteln, auf welcher Ebene der Hierarchie sich eine Zeile befindet. Führen Sie den folgenden Code aus, um die Ebenen aller Zeilen anzuzeigen:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  Verwenden Sie die [GetRoot](../../t-sql/data-types/getroot-database-engine.md) -Methode, um den Stammknoten in der Hierarchie zu ermitteln. Im folgenden Code wird die einzelne Zeile, die der Stamm ist, zurückgegeben:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
  
In der nächsten Aufgabe wird die Hierarchie neu organisiert.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Neuanordnen von Daten in einer hierarchischen Tabelle mit hierarchischen Methoden](../../relational-databases/tables/lesson-2-4-reordering-data-in-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
  

