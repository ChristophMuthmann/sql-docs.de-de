---
title: GetDescendant (Datenbank-Engine) | Microsoft-Dokumentation
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
- GetDescendant_TSQL
- GetDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- GetDescendant [Database Engine]
ms.assetid: f5f39596-033e-4243-acbc-caa188b45b03
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d79b0bc3d47acf6be5315688398e7047b823d8e7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="getdescendant-database-engine"></a>GetDescendant (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt einen untergeordneten Knoten des übergeordneten Elements zurück.
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Transact-SQL syntax  
parent.GetDescendant ( child1 , child2 )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetDescendant ( SqlHierarchyId child1 , SqlHierarchyId child2 )   
```  
  
## <a name="arguments"></a>Argumente  
*child1*  
NULL oder die **hierarchyid** eines untergeordneten Elements des aktuellen Knotens.
  
*child2*  
NULL oder die **hierarchyid** eines untergeordneten Elements des aktuellen Knotens.
  
## <a name="return-types"></a>Rückgabetypen  
**SQL Server-Rückgabetyp: hierarchyid**
  
**CLR-Rückgabetyp: SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
Gibt einen untergeordneten Knoten zurück, der ein Nachfolger des übergeordneten Elements ist.
-   Ist parent NULL, wird NULL zurückgegeben.  
-   Ist parent nicht NULL und sind sowohl child1 als auch child2 NULL, dann wird ein parent untergeordneter Knoten zurückgegeben.  
-   Sind parent und child1 nicht NULL und ist child2 NULL, dann wird ein parent untergeordneter Knoten zurückgegeben, der größer als child1 ist.  
-   Sind parent und child2 nicht NULL und ist child1 NULL, dann wird ein parent untergeordneter Knoten zurückgegeben, der kleiner als child2 ist.  
-   Sind parent, child1 und child2 nicht NULL, dann wird ein untergeordneter Knoten zurückgegeben, der größer als child1 und kleiner als child2 ist.  
-   Ist child1 nicht NULL und außerdem kein untergeordnetes Element von parent, wird eine Ausnahme ausgelöst.  
-   Ist child2 nicht NULL und außerdem kein untergeordnetes Element von parent, wird eine Ausnahme ausgelöst.  
-   Ist child1 >= child2, wird eine Ausnahme ausgelöst.  
  
GetDescendant ist deterministisch. Deshalb erzeugt GetDescendant immer die gleiche Ausgabe, wenn es mit den gleichen Eingaben aufgerufen wird. Die genaue Identität des erzeugten untergeordneten Elements kann jedoch abhängig von seiner Beziehung zu den anderen Knoten variieren, wie in Beispiel C veranschaulicht wird.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-inserting-a-row-as-the-least-descendant-node"></a>A. Einfügen einer Zeile als unterster Nachfolgerknoten  
Ein neuer Mitarbeiter wird eingestellt und berichtet einem vorhandenen Mitarbeiter auf Knoten `/3/1/`. Führen Sie den folgenden Code aus, um mithilfe der GetDescendant-Methode ohne Argumente eine neue Zeile einzufügen, um den Knoten der neuen Zeile auf `/3/1/1/` festzulegen:
  
```sql
DECLARE @Manager hierarchyid;   
SET @Manager = CAST('/3/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(NULL, NULL),  
'adventure-works\FirstNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="b-inserting-a-row-as-a-greater-descendant-node"></a>B. Einfügen einer Zeile als höherer Nachfolgerknoten  
Ein weiterer neuer Mitarbeiter wird eingestellt, der ebenfalls dem Abteilungsleiter aus Beispiel A berichtet. Führen Sie den folgenden Code aus, um mithilfe der GetDescendant-Methode eine neue Zeile einzufügen, wobei Sie mit dem child1-Argument festlegen, dass der Knoten der neuen Zeile auf den Knoten aus Beispiel A folgen soll und somit `/3/1/2/` lautet:
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, NULL),  
'adventure-works\SecondNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="c-inserting-a-row-between-two-existing-nodes"></a>C. Einfügen einer Zeile zwischen zwei vorhandenen Knoten  
Ein dritter neuer Mitarbeiter wird eingestellt, der ebenfalls dem Abteilungsleiter aus Beispiel A berichtet. In diesem Beispiel wird die neue Zeile mit einem Knoten eingefügt, der größer ist als `FirstNewEmployee` in Beispiel A und kleiner als `SecondNewEmployee` in Beispiel B. Führen Sie den folgenden Code mithilfe der GetDescendant-Methode aus. Verwenden Sie die Argumente child1 und child2, um festzulegen, dass der Knoten der neuen Zeile der Knoten `/3/1/1.1/` sein wird:
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid, @Child2 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
SET @Child2 = CAST('/3/1/2/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, @Child2),  
'adventure-works\ThirdNewEmployee', 'Application Intern', '3/11/07') ;  
  
```  
  
Nach Abschluss der Beispiele A, B und C sind die der Tabelle hinzugefügten Knoten Peers der folgenden **hierarchyid**-Werte:
  
`/3/1/1/`
  
`/3/1/1.1/`
  
`/3/1/2/`
  
Knoten `/3/1/1.1/` ist größer als Knoten `/3/1/1/`, befindet sich aber auf der gleichen Ebene in der Hierarchie.
  
### <a name="d-scalar-examples"></a>D. Skalarbeispiele  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt willkürliche Einfüge- und Löschvorgänge beliebiger **hierarchyid**-Knoten. Mit GetDescendant() ist es immer möglich, einen Knoten zwischen zwei beliebigen **hierarchyid**-Knoten zu generieren. Führen Sie den folgenden Code aus, um mithilfe von `GetDescendant` Beispielknoten zu generieren:
  
```sql
DECLARE @h hierarchyid = hierarchyid::GetRoot();  
DECLARE @c hierarchyid = @h.GetDescendant(NULL, NULL);  
SELECT @c.ToString();  
DECLARE @c2 hierarchyid = @h.GetDescendant(@c, NULL);  
SELECT @c2.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
SET @c = @h.GetDescendant(@c, @c2);  
SELECT @c.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
```  
  
### <a name="e-clr-example"></a>E. CLR-Beispiel  
Im folgenden Codeausschnitt wird die `GetDescendant()`-Methode aufgerufen:
  
```sql
SqlHierarchyId parent, child1, child2;  
parent = SqlHierarchyId.GetRoot();  
child1 = parent.GetDescendant(SqlHierarchyId.Null, SqlHierarchyId.Null);  
child2 = parent.GetDescendant(child1, SqlHierarchyId.Null);  
Console.Write(parent.GetDescendant(child1, child2).ToString());  
```  
  
## <a name="see-also"></a>Siehe auch
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
