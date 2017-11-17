---
title: Write (Datenbankmodul) | Microsoft Docs
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
- Write_TSQL
- Write
dev_langs:
- TSQL
helpviewer_keywords:
- Write [Database Engine]
ms.assetid: 7c554334-d2d9-4eae-a4ae-097aa4020e1a
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60707b57671c2ad607bd85b0fedececccd478038
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="write-database-engine"></a>Write (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Schreibt eine binäre Darstellung der schreiben **SqlHierarchyId** in den übergebenen **BinaryWriter**. Schreibvorgang kann nicht aufgerufen werden, mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)]. Verwenden Sie stattdessen CAST oder CONVERT.
  
## <a name="syntax"></a>Syntax  
  
```sql
void Write( BinaryWriter w )   
```  
  
## <a name="arguments"></a>Argumente  
*w*  
Ein **BinaryWriter** Objekt, mit dem die binäre Darstellung dieses **Hierarchyid** Knoten geschrieben wird.
  
## <a name="return-types"></a>Rückgabetypen  
**CLR-Typ: Void zurückgeben**
  
## <a name="remarks"></a>Hinweise  
Schreiben wird intern von verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Wenn ist es erforderlich, z. B. beim Laden von Daten aus einer **Hierarchyid** Spalte. Schreiben wird außerdem intern aufgerufen, wenn eine Konvertierung zwischen erfolgt **Hierarchyid** und **Varbinary**.
  
## <a name="examples"></a>Beispiele  
  
```sql
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
  
```  
  
## <a name="see-also"></a>Siehe auch
[Lesen &#40; Datenbankmodul &#41;](../../t-sql/data-types/read-database-engine.md)  
[ToString &#40; Datenbankmodul &#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

