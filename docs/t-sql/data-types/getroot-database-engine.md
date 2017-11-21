---
title: GetRoot (Datenbankmodul) | Microsoft Docs
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
- GetRoot
- GetRoot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetRoot [Database Engine]
ms.assetid: 240b70f1-eeda-44ab-b4bb-9e4af80fa7c0
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4de7e4010400cbf3d192efb3dd6709792d734ba
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="getroot-database-engine"></a>GetRoot (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt den Stamm der Hierarchiestruktur zurück. GetRoot() ist eine statische Methode.
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Transact-SQL syntax  
hierarchyid::GetRoot ( )   
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId GetRoot ( )   
```  
  
## <a name="return-types"></a>Rückgabetypen  
**SQL Server-Typ: Hierarchyid zurück**
  
**CLR-Typ: SqlHierarchyId zurück**
  
## <a name="remarks"></a>Hinweise  
Wird verwendet, um den Stammknoten in einer Hierarchiestruktur zu bestimmen.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-transact-sql-example"></a>A. Beispiel für Transact-SQL  
Im folgenden Beispiel wird der Stamm der Hierarchiestruktur zurückgegeben.
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = hierarchyid::GetRoot()  
```  
  
### <a name="b-clr-example"></a>B. CLR-Beispiel  
Der folgende Codeausschnitt Ruft die GetRoot()-Methode:
  
```sql
SqlHierarchyId.GetRoot()  
```  
  
## <a name="see-also"></a>Siehe auch
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

