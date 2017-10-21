---
title: IsDescendantOf (Datenbankmodul) | Microsoft Docs
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
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f8ff83344e577e5479e21316a3c043d6ef4f702
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt "true" zurück, wenn *dies* ein Nachfolger des übergeordneten Elements.
  
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
*übergeordnete*  
Die **Hierarchyid** Knoten für die die IsDescendantOf-Test ausgeführt werden soll.
  
## <a name="return-types"></a>Rückgabetypen  
**SQL Server-Typ: Bit zurück**
  
**CLR-Typ: SqlBoolean zurück**
  
## <a name="remarks"></a>Hinweise  
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
  
  

