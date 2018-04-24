---
title: IsDescendantOf (Datenbank-Engine) | Microsoft-Dokumentation
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
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b0e35c5df5fb2124ba89fd26d7d93d31fa990d39
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt TRUE zurück, wenn *this* ein Nachfolger von „parent“ ist.
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Transact-SQL syntax  
child. IsDescendantOf ( parent )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId IsDescendantOf (SqlHierarchyId parent )  
```  
  
## <a name="arguments"></a>Argumente  
*parent*  
Der **hierarchyid**-Knoten, für den der IsDescendantOf-Test ausgeführt werden sollte.
  
## <a name="return-types"></a>Rückgabetypen  
**SQL Server-Rückgabetyp: bit**
  
**CLR-Rückgabetyp: SqlBoolean**
  
## <a name="remarks"></a>Remarks  
Gibt true für alle Knoten in der Teilstruktur zurück, die die übergeordnete Struktur als Stamm aufweisen, und false für alle anderen Knoten.
  
Das übergeordnete Element wird als sein eigener Nachfolger behandelt.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-isdescendantof-in-a-where-clause"></a>A. Verwenden von IsDescendantOf in einer WHERE-Klausel  
Im folgenden Beispiel werden ein Manager sowie die Mitarbeiter angezeigt, die diesem direkt unterstellt sind.
  
```sql
DECLARE @Manager hierarchyid  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\dylan0'  
  
SELECT * FROM HumanResources.EmployeeDemo  
WHERE OrgNode.IsDescendantOf(@Manager) = 1  
```  
  
### <a name="b-using-isdescendantof-to-evaluate-a-relationship"></a>B. Verwenden von IsDescendantOf zur Evaluierung einer Beziehung  
Im folgenden Code werden drei Variablen deklariert und aufgefüllt. Dann wird die hierarchische Beziehung evaluiert und eines von zwei Ergebnissen auf Grundlage des Vergleiches zurückgegeben:
  
```sql
DECLARE @Manager hierarchyid, @Employee hierarchyid, @LoginID nvarchar(256)  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\terri0' ;  
  
SELECT @Employee = OrgNode, @LoginID = LoginID FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\rob0'  
  
IF @Employee.IsDescendantOf(@Manager) = 1  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is a subordinate of the selected Manager.'  
   END  
ELSE  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is not a subordinate of the selected Manager.' ;  
   END  
```  
  
### <a name="c-calling-a-common-language-runtime-method"></a>C. Aufrufen einer Common Language Runtime-Methode  
Im folgenden Codeausschnitt wird die `IsDescendantOf()`-Methode aufgerufen.
  
```sql
this.IsDescendantOf(Parent)  
```  
  
## <a name="see-also"></a>Siehe auch
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
