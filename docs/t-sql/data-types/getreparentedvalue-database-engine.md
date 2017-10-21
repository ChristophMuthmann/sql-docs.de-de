---
title: GetReparentedValue (Datenbankmodul) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reparent_TSQL
- Reparent
dev_langs:
- TSQL
helpviewer_keywords:
- Reparent [Database Engine]
ms.assetid: f47f8e25-08ef-498b-84f4-a317aca1f358
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57f565258c7fd95347d7d9bd36b2dd2034712efe
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="getreparentedvalue-database-engine"></a>GetReparentedValue (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt einen Knoten zurück, dessen Pfad vom Stamm des Pfads zum *"newroot"*, gefolgt vom Pfad von *OldRoot* auf *dies*.
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Transact-SQL syntax  
node. GetReparentedValue ( oldRoot, newRoot )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetReparentedValue ( SqlHierarchyId oldRoot , SqlHierarchyId newRoot )  
```  
  
## <a name="arguments"></a>Argumente  
*oldRoot*  
Ein **Hierarchyid** also der Knoten, der die Ebene der Hierarchie darstellt, die geändert werden soll.
  
*"newroot"*  
Ein **Hierarchyid** , die den Knoten, der ersetzt darstellt der *OldRoot* Abschnitt des aktuellen Knotens zur Verschiebung des Knotens.
  
## <a name="return-types"></a>Rückgabetypen  
**SQL Server-Typ: Hierarchyid zurück**
  
**CLR-Typ: SqlHierarchyId zurück**
  
## <a name="remarks"></a>Hinweise  
Kann verwendet werden, um die Struktur zu ändern, indem Sie Knoten aus verschieben *OldRoot* auf *"newroot"*. Mit GetReparentedValue können Sie einen Knoten einer Hierarchie an eine neue Position in der Hierarchie verschieben. Die **Hierarchyid** Datentyp darstellt, aber die hierarchische Struktur wird nicht erzwungen. Benutzer müssen sicherstellen, dass der hierarchyid-Wert für die neue Position angemessen strukturiert ist. Ein eindeutiger Index für die **Hierarchyid** -Datentyp kann doppelte Einträge vermeiden. Ein Beispiel für das Verschieben von einer kompletten Teilstruktur, finden Sie unter [hierarchische Daten &#40; SQLServer &#41; ](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-comparing-two-node-locations"></a>A. Vergleichen von zwei Knotenpositionen  
Im folgenden Beispiel wird der aktuelle hierarchyid-Wert eines Knotens gezeigt. Außerdem wird gezeigt, was die **Hierarchyid** des Knotens wäre, wenn der Knoten verschoben des Nachfolgers die  **@NewParent**  Knoten. Zur Darstellung der hierarchischen Beziehungen wird die `ToString()`-Methode verwendet.
  
```sql
DECLARE @SubjectEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
SELECT @SubjectEmployee = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\gail0' ;  
SELECT @OldParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\roberto0' ; -- who is /1/1/  
SELECT @NewParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\wanida0' ; -- who is /2/3/  
  
SELECT OrgNode.ToString() AS Current_OrgNode_AS_Text,   
(@SubjectEmployee. GetReparentedValue(@OldParent, @NewParent) ).ToString() AS Proposed_OrgNode_AS_Text,  
OrgNode AS Current_OrgNode,  
@SubjectEmployee. GetReparentedValue(@OldParent, @NewParent) AS Proposed_OrgNode,  
*  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = @SubjectEmployee ;  
GO  
```  
  
### <a name="b-updating-a-node-to-a-new-location"></a>B. Aktualisieren eines Knotens mit einer neuen Position  
Im folgenden Beispiel wird `GetReparentedValue()` in einer UPDATE-Anweisung verwendet, um einen Knoten in einer Hierarchie von einer alten an eine neue Position zu verschieben:
  
```sql
DECLARE @SubjectEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
SELECT @SubjectEmployee = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\gail0' ; -- Node /1/1/2/  
SELECT @OldParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\roberto0' ; -- Node /1/1/  
SELECT @NewParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\wanida0' ; -- Node /2/3/  
  
UPDATE HumanResources.EmployeeDemo  
SET OrgNode = @SubjectEmployee. GetReparentedValue(@OldParent, @NewParent)   
WHERE OrgNode = @SubjectEmployee ;  
  
SELECT OrgNode.ToString() AS Current_OrgNode_AS_Text,   
*  
FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\gail0' ; -- Now node /2/3/2/  
```  
  
### <a name="c-clr-example"></a>C. CLR-Beispiel  
Der folgende Codeausschnitt Ruft die GetReparentedValue ()-Methode:
  
```sql
this. GetReparentedValue(oldParent, newParent)  
```  
  
## <a name="see-also"></a>Siehe auch
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

