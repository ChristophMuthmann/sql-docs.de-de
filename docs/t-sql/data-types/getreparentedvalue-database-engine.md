---
title: GetReparentedValue (Datenbank-Engine) | Microsoft-Dokumentation
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0b054e9651cce9a486d4acf9e997a601114e98a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="getreparentedvalue-database-engine"></a>GetReparentedValue (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt den Knoten zurück, dessen Pfad im Stamm der Pfad zu *newRoot* gefolgt von dem Pfad von *oldRoot* zu *this* ist.
  
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
Ein **hierarchyid**-Wert, der den Knoten der zu ändernden Hierarchieebene angibt.
  
*newRoot*  
Ein **hierarchyid**-Wert, der den Knoten angibt, der den *oldRoot*-Abschnitt des aktuellen Knotens zur Verschiebung des Knotens ersetzt.
  
## <a name="return-types"></a>Rückgabetypen  
**SQL Server-Rückgabetyp: hierarchyid**
  
**CLR-Rückgabetyp: SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
Kann verwendet werden, um die Struktur durch Verschieben von Knoten von *oldRoot* nach *newRoot* zu ändern. Mit GetReparentedValue können Sie einen Knoten einer Hierarchie an eine neue Position in der Hierarchie verschieben. Der **hierarchyid**-Datentyp stellt die hierarchische Struktur dar, setzt sie jedoch nicht durch. Benutzer müssen sicherstellen, dass der hierarchyid-Wert für die neue Position angemessen strukturiert ist. Mit einem eindeutigen Index für den **hierarchyid**-Datentyp können Sie doppelte Einträge vermeiden. Ein Beispiel für die Verschiebung einer vollständigen Teilstruktur finden Sie unter [Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-comparing-two-node-locations"></a>A. Vergleichen von zwei Knotenpositionen  
Im folgenden Beispiel wird der aktuelle hierarchyid-Wert eines Knotens gezeigt. Des Weiteren wird der **hierarchyid**-Wert gezeigt, den der Knoten aufweist, wenn er an die Position des Nachfolgers des **@NewParent**-Knotens verschoben wird. Zur Darstellung der hierarchischen Beziehungen wird die `ToString()`-Methode verwendet.
  
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
Im folgenden Codeausschnitt wird die GetReparentedValue ()-Methode aufgerufen:
  
```sql
this. GetReparentedValue(oldParent, newParent)  
```  
  
## <a name="see-also"></a>Siehe auch
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
