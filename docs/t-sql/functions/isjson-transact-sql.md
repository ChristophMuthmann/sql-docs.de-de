---
title: ISJSON (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0ecbcc4ced2b9503ec9161f7aa93a1a5266960ef
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="isjson-transact-sql"></a>ISJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Testet, ob eine Zeichenfolge gültiges JSON enthält.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
ISJSON ( expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Die zu testende Zeichenfolge.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt 1, wenn die Zeichenfolge eine gültige JSON; enthält Andernfalls wird 0 zurückgegeben. Gibt null zurück, wenn *Ausdruck* ist null.  
  
 Gibt keinen Fehler zurück.  
  
## <a name="remarks"></a>Hinweise  
 **ISJSON** überprüft nicht die Eindeutigkeit der Schlüssel auf derselben Ebene.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="example-1"></a>Beispiel 1  
Im folgende Beispiel führt einen Anweisungsblock bedingt, wenn der Wert des Parameters `@param` gültige JSON enthält.  
  
```sql  
DECLARE @param <data type>
SET @param = <value>

IF (ISJSON(@param) > 0)  
BEGIN  
     -- Do something with the valid JSON value of @param.  
END
 
```  
  
### <a name="example-2"></a>Beispiel 2  
Im folgenden Beispiel werden die Spalten zurückgegeben, falls die Spalte `json_col` ein gültiges JSON enthält.  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  
  
## <a name="see-also"></a>Siehe auch  
 [JSON-Daten &#40; SQLServer &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
