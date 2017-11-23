---
title: Parse (Datenbankmodul) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Parse
- Parse_TSQL
dev_langs: TSQL
helpviewer_keywords: Parse [Database Engine]
ms.assetid: b37e28b6-6e2e-470a-945b-ce5252da743a
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e80c29d1a13e0b77792ec6d3533d4d80cf355b40
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="parse-database-engine"></a>Parse (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Parse konvertiert die kanonische Zeichenfolgendarstellung einer **Hierarchyid** zu einem **Hierarchyid** Wert. Analyse wird implizit aufgerufen, wenn eine Konvertierung von einem Zeichenfolgentyp in **Hierarchyid** auftritt. Dient als Gegenstück des [ToString](../../t-sql/data-types/tostring-database-engine.md). Parse() ist eine statische Methode.
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Transact-SQL syntax  
hierarchyid::Parse ( input )  
-- This is functionally equivalent to the following syntax   
-- which implicitly calls Parse():  
CAST ( input AS hierarchyid )  
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId Parse ( SqlString input )   
```  
  
## <a name="arguments"></a>Argumente  
*Eingabe*  
[!INCLUDE[tsql](../../includes/tsql-md.md)]: Der Wert des Zeichendatentyps, der konvertiert wird.
  
CLR: Der Zeichenfolgenwert, der ausgewertet wird.
  
## <a name="return-types"></a>Rückgabetypen  
**SQL Server-Typ: Hierarchyid zurück**
  
**CLR-Typ: SqlHierarchyId zurück**
  
## <a name="remarks"></a>Hinweise  
Wenn die Analyse einen Wert empfängt, die nicht auf eine gültige Darstellung der Zeichenfolge ist ein **Hierarchyid**, wird eine Ausnahme ausgelöst. Z. B. wenn **Char** -Datentypen nachfolgende Leerzeichen enthalten, wird eine Ausnahme ausgelöst.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>A. Konvertieren von Transact-SQL-Werten ohne Tabelle  
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
  
### <a name="b-clr-example"></a>B. CLR-Beispiel  
Der folgende Codeausschnitt Ruft die Parse()-Methode:
  
```sql
string input = “/1/2/”;  
SqlHierarchyId.Parse(input);  
```  
  
## <a name="see-also"></a>Siehe auch
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Hierarchische Daten &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
