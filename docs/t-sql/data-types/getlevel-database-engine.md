---
title: GetLevel (Datenbank-Engine) | Microsoft-Dokumentation
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
- GetLevel
- GetLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetLevel [Database Engine]
ms.assetid: 81577d7e-8ff6-4e73-b7f4-94c03d4921e7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a12afc32b16a6cd6af3cf5a5551b783a450207e1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="getlevel-database-engine"></a>GetLevel (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt einen Integer zurück, der die Tiefe des Knotens *this* in der Struktur darstellt.
  
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
**SQL Server-Rückgabetyp: smallint**
  
**CLR-Rückgabetyp: SqlInt16**
  
## <a name="remarks"></a>Remarks  
Wird zur Bestimmung der Ebene eines oder mehrerer Knoten oder zur Filterung der Knoten nach Elementen einer bestimmten Ebene verwendet. Der Stamm der Hierarchie ist Ebene 0.
  
GetLevel ist sehr nützlich für Breitensuchindizes. Weitere Informationen finden Sie unter [Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-hierarchy-level-as-a-column"></a>A. Zurückgeben der Hierarchieebene als Spalte  
Im folgenden Beispiel wird eine Textdarstellung von **hierarchyid** und anschließend die Hierarchieebene als **EmpLevel**-Spalte für alle Zeilen in der Tabelle zurückgegeben:
  
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
Im folgenden Codeausschnitt wird die GetLevel()-Methode aufgerufen:
  
```sql
this.GetLevel()  
```  
  
## <a name="see-also"></a>Siehe auch
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
