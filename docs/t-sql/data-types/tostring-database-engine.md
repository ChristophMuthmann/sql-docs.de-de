---
title: ToString (Datenbankmodul) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
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
- ToString
- ToString_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ToString [Database Engine]
ms.assetid: 5fc11ca5-c26d-4518-9512-67aa0270f110
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1544b27215083f8628696cebaaf14c53c628a9ba
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="tostring-database-engine"></a>ToString (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine Zeichenfolge mit der logischen Darstellung von *dies*. ToString wird implizit aufgerufen, wenn eine Konvertierung von **Hierarchyid** -Typ in einen Zeichenfolgentyp stattfindet. Dient als Gegenstück des [Parse &#40; Datenbankmodul &#41;](../../t-sql/data-types/parse-database-engine.md).
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Transact-SQL syntax  
node.ToString  ( )   
-- This is functionally equivalent to the following syntax  
-- which implicitly calls ToString():  
CAST(node AS nvarchar(4000))  
```  
  
```sql
-- CLR syntax  
string ToString  ( )   
```  
  
## <a name="return-types"></a>Rückgabetypen
**SQL Server return type:nvarchar(4000)**
  
**Return CLR-Typ: Zeichenfolge**
  
## <a name="remarks"></a>Hinweise  
Gibt die logische Position in der Hierarchie zurück. Beispielsweise `/2/1/` stellt die vierte Zeile ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) in der folgenden hierarchischen Struktur eines Dateisystems:
  
```sql
/        C:\  
/1/      C:\Database Files  
/2/      C:\Program Files  
/2/1/    C:\Program Files\Microsoft SQL Server  
/2/2/    C:\Program Files\Microsoft Visual Studio  
/3/      C:\Windows  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-transact-sql-example-in-a-table"></a>A. Transact-SQL-Beispiel in einer Tabelle  
Das folgende Beispiel gibt sowohl die `OrgNode` -Spalte als auch die **Hierarchyid** -Datentyp und den besser lesbaren Format:
  
```sql
SELECT OrgNode,  
OrgNode.ToString() AS Node  
FROM HumanResources.EmployeeDemo  
ORDER BY OrgNode ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
OrgNode   Node  
0x        /  
0x58      /1/  
0x5AC0    /1/1/  
0x5B40    /1/2/  
0x5BC0    /1/3/  
0x5C20    /1/4/  
...  
```  
  
### <a name="b-converting-transact-sql-values-without-a-table"></a>B. Konvertieren von Transact-SQL-Werten ohne Tabelle  
Im folgenden Codebeispiel wird mit `ToString` Konvertieren einer **Hierarchyid** Wert in eine Zeichenfolge und `Parse` zum Umwandeln eines Zeichenfolgenwertes in einen **Hierarchyid**.
  
```sql
DECLARE @StringValue AS nvarchar(4000), @hierarchyidValue AS hierarchyid  
SET @StringValue = '/1/1/3/'  
SET @hierarchyidValue = 0x5ADE  
  
SELECT hierarchyid::Parse(@StringValue) AS hierarchyidRepresentation,  
@hierarchyidValue.ToString() AS StringRepresentation ;
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
hierarchyidRepresentation    StringRepresentation
-------------------------    -----------------------
0x5ADE                       /1/1/3/
```
  
### <a name="c-clr-example"></a>C. CLR-Beispiel  
Im folgenden Codeausschnitt wird die Methode ToString() aufgerufen:
  
```sql
this.ToString()  
```  
  
## <a name="see-also"></a>Siehe auch
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

