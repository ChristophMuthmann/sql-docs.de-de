---
title: GetAncestor (Datenbank-Engine) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e07aa5444fa2805e66517b452a13a1ad675deb4b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="getancestor-database-engine"></a>GetAncestor (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **hierarchyid** zurück, die den *n*-ten Vorgänger von *this* darstellt.
  
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
Ein **int**-Wert, der die Anzahl der Hierarchieebenen nach oben darstellt.
  
## <a name="return-types"></a>Rückgabetypen
**SQL Server-Rückgabetyp: hierarchyid**
  
**CLR-Rückgabetyp: SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
Hiermit wird getestet, ob jeder Knoten in der Ausgabe den aktuellen Knoten als Vorgänger auf der angegebenen Ebene aufweist.
  
Wenn eine Zahl größer als [GetLevel ()](../../t-sql/data-types/getlevel-database-engine.md) übergeben wird, wird NULL zurückgegeben.
  
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
Um den aktuellen Knoten mit `GetAncestor(0)` zurückzugeben, führen Sie den folgenden Code aus.
  
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
[IsDescendantOf &#40;Database Engine&#41; (IsDescendantOf (Datenbank-Engine))](../../t-sql/data-types/isdescendantof-database-engine.md)  
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
