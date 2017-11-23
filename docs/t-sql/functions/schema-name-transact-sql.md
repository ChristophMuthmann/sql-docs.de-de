---
title: SCHEMA_NAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCHEMA_NAME
- SCHEMA_NAME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- SCHEMA_NAME function
- schemas [SQL Server], names
ms.assetid: 20071b77-2b6e-4ce7-a8e3-fa71480baf73
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 41dd04ebbbc5b07512d243e5d4ac77761ba9ca1e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="schemaname-transact-sql"></a>SCHEMA_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den einer Schema-ID zugeordneten Schemanamen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SCHEMA_NAME ( [ schema_id ] )  
```  
  
## <a name="arguments"></a>Argumente  
  
|Begriff|Definition|  
|----------|----------------|  
|*schema_id*|Die ID des Schemas. *Schema_id* ist ein **Int**. Wenn *Schema_id* ist nicht definiert ist, gibt SCHEMA_NAME den Namen des Standardschemas des Aufrufers zurück.|  
  
## <a name="return-types"></a>Rückgabetypen  
 **sysname**  
  
 Gibt NULL zurück, wenn *Schema_id* ist keine gültige Kennung.  
  
## <a name="remarks"></a>Hinweise  
 SCHEMA_NAME gibt Namen von Systemschemas und benutzerdefinierten Schemas zurück. SCHEMA_NAME kann in einer SELECT-Liste, in einer WHERE-Klausel und überall dort aufgerufen werden, wo ein Ausdruck zulässig ist.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-name-of-the-default-schema-of-the-caller"></a>A. Zurückgeben des Namens des Standardschemas des Aufrufers  
  
```  
SELECT SCHEMA_NAME();  
```  
  
### <a name="b-returning-the-name-of-a-schema-by-using-an-id"></a>B. Zurückgeben des Namens eines Schemas mithilfe einer ID  
  
```  
SELECT SCHEMA_NAME(1);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SCHEMA_ID &#40; Transact-SQL &#41;](../../t-sql/functions/schema-id-transact-sql.md)   
 [Sys.Schemas &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

