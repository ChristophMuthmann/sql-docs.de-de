---
title: GetAncestor (Datenbankmodul) | Microsoft Docs
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
- GetAncestor_TSQL
- GetAncestor
dev_langs:
- TSQL
helpviewer_keywords:
- GetAncestor [Database Engine]
ms.assetid: b96a986f-d5e4-4034-8013-de7974594ee9
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7649b3290175787b293ea1b720bb299ead89971
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="getancestor-database-engine"></a>GetAncestor (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **Hierarchyid** darstellt der  *n* ten Vorgänger von *dies*.
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Transact-SQL syntax  
child.GetAncestor ( n )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetAncestor ( int n )  
```  
  
## <a name="arguments"></a>Argumente  
*n*  
Ein **Int**, welche die Anzahl der Ebenen in der Hierarchie nach oben.
  
## <a name="return-types"></a>Rückgabetypen
**SQL Server-Typ: Hierarchyid zurück**
  
**CLR-Typ: SqlHierarchyId zurück**
  
## <a name="remarks"></a>Hinweise  
Hiermit wird getestet, ob jeder Knoten in der Ausgabe den aktuellen Knoten als Vorgänger auf der angegebenen Ebene aufweist.
  
Wenn eine Zahl größer als [getlevel ()](../../t-sql/data-types/getlevel-database-engine.md) wird übergeben, wird NULL zurückgegeben.
  
Wenn eine negative Zahl übergeben wird, wird eine Ausnahme ausgelöst.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-finding-the-child-nodes-of-a-parent"></a>A. Suchen der untergeordneten Knoten eines übergeordneten Elements  
`GetAncestor(1)` gibt die Mitarbeiter zurück, die `david0` als unmittelbaren Vorgänger (übergeordnetes Element) haben. Im folgenden Beispiel wird `GetAncestor(1)` verwendet.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(1) = @CurrentEmployee ;  
```  
  
### <a name="b-returning-the-grandchildren-of-a-parent"></a>B. Zurückgeben der untergeordneten Elemente zweiter Ordnung eines übergeordneten Elements  
`GetAncestor(2)` gibt die Mitarbeiter zurück, die sich in der aktuellen Hierarchie zwei Ebenen unter dem aktuellen Knoten befinden. Dies sind die untergeordneten Knoten zweiter Ordnung des aktuellen Knotens. Im folgenden Beispiel wird `GetAncestor(2)` verwendet.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\ken0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(2) = @CurrentEmployee ;  
```  
  
### <a name="c-returning-the-current-row"></a>C. Zurückgeben der aktuellen Zeile  
Mit den aktuellen Knoten zurückzugebenden `GetAncestor(0)`, führen Sie den folgenden Code.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(0) = @CurrentEmployee ;  
```  
  
### <a name="d-returning-a-hierarchy-level-if-a-table-is-not-present"></a>D. Zurückgeben einer Hierarchieebene, wenn keine Tabelle vorhanden ist  
`GetAncestor` gibt die ausgewählte Ebene in der Hierarchie zurück, auch wenn keine Tabelle vorhanden ist. Beispiel: Mit dem folgenden Code wird ein aktueller Mitarbeiter festgelegt, und die `hierarchyid` vom Vorgänger des aktuellen Mitarbeiters wird ohne Verweis auf eine Tabelle zurückgegeben.
  
```sql
DECLARE @CurrentEmployee hierarchyid ;  
DECLARE @TargetEmployee hierarchyid ;  
SELECT @CurrentEmployee = '/2/3/1.2/5/3/' ;  
SELECT @TargetEmployee = @CurrentEmployee.GetAncestor(2) ;  
SELECT @TargetEmployee.ToString(), @TargetEmployee ;  
```  
  
### <a name="e-calling-a-common-language-runtime-method"></a>E. Aufrufen einer Common Language Runtime-Methode  
Im folgenden Codeausschnitt wird die `GetAncestor()`-Methode aufgerufen.
  
```sql
this.GetAncestor(1)  
```  
  
## <a name="see-also"></a>Siehe auch
[IsDescendantOf &#40; Datenbankmodul &#41;](../../t-sql/data-types/isdescendantof-database-engine.md)  
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

