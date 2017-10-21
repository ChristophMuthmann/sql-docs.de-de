---
title: GetLevel (Datenbankmodul) | Microsoft Docs
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
- GetLevel
- GetLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetLevel [Database Engine]
ms.assetid: 81577d7e-8ff6-4e73-b7f4-94c03d4921e7
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aac401d8fbe9546404f44f5fa2455f9e9c5dfe9d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="getlevel-database-engine"></a>GetLevel (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine ganze Zahl, die die Tiefe des Knotens darstellt *dies* in der Struktur.
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Transact-SQL syntax  
node.GetLevel ( )   
```  
  
```sql
-- CLR syntax  
SqlInt16 GetLevel ( )   
```  
  
## <a name="return-types"></a>Rückgabetypen  
**SQL Server-Typ: Smallint zurück**
  
**CLR-Typ: SqlInt16 zurück**
  
## <a name="remarks"></a>Hinweise  
Wird zur Bestimmung der Ebene eines oder mehrerer Knoten oder zur Filterung der Knoten nach Elementen einer bestimmten Ebene verwendet. Der Stamm der Hierarchie ist Ebene 0.
  
GetLevel ist sehr nützlich für breitensuchindex Search-Indizes. Weitere Informationen finden Sie unter [hierarchische Daten &#40; SQLServer &#41; ](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-hierarchy-level-as-a-column"></a>A. Zurückgeben der Hierarchieebene als Spalte  
Das folgende Beispiel gibt eine Textdarstellung der **Hierarchyid**, und klicken Sie dann die Hierarchieebene als die **EmpLevel** Spalte für alle Zeilen in der Tabelle:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo;  
```  
  
### <a name="b-returning-all-members-of-a-hierarchy-level"></a>B. Zurückgeben aller Elemente einer Hierarchieebene  
Im folgenden Beispiel werden alle Zeilen in der Tabelle auf Hierarchieebene 2 zurückgegeben:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 2;  
```  
  
### <a name="c-returning-the-root-of-the-hierarchy"></a>C. Zurückgeben des Stamms der Hierarchie  
Im folgenden Beispiel wird der Stamm der Hierarchieebene zurückgegeben.
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 0;  
```  
  
### <a name="d-clr-example"></a>D. CLR-Beispiel  
Der folgende Codeausschnitt Ruft die getlevel ()-Methode:
  
```sql
this.GetLevel()  
```  
  
## <a name="see-also"></a>Siehe auch
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

