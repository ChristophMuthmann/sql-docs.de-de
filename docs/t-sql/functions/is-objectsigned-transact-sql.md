---
title: IS_OBJECTSIGNED (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_OBJECTSIGNED
- IS_OBJECTSIGNED_TSQL
dev_langs: TSQL
helpviewer_keywords: IS_OBJECTSIGNED function
ms.assetid: afbc4f7f-8266-4ee6-9802-14a2dbe69ef6
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e3cdcdfec27373a437af6895cbd68a1ceb609c7c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="isobjectsigned-transact-sql"></a>IS_OBJECTSIGNED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt an, ob ein Objekt von einem angegebenen Zertifikat oder asymmetrischen Schlüssel signiert wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IS_OBJECTSIGNED (   
'OBJECT', @object_id, @class, @thumbprint  
  )   
```  
  
## <a name="arguments"></a>Argumente  
 **"OBJECT"**  
 Der Typ der sicherbaren Klasse.  
  
 *@object_id*  
 Die object_id des Objekts, das getestet wird. *@object_id*Typ **Int**.  
  
 *@class*  
 Klasse des Objekts:  
  
-   ‚Zertifikat’  
  
-   ‚asymmetrischer Schlüssel’  
  
 *@class*ist **Sysname**.  
  
 *@thumbprint*  
 Der SHA-Fingerabdruck des Objekts. *@thumbprint*Typ **varbinary(32)**.  
  
## <a name="returned-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 IS_OBJECTSIGNED gibt folgende Werte zurück.  
  
|Rückgabewert|Description|  
|------------------|-----------------|  
|NULL|Das Objekt ist nicht signiert, oder das Objekt ist ungültig.|  
|0|Das Objekt ist signiert, aber die Signatur ist ungültig.|  
|1|Das Objekt ist signiert.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DEFINITION-Berechtigung für das Zertifikat oder den asymmetrischen Schlüssel.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-displaying-extended-properties-on-a-database"></a>A. Anzeigen erweiterter Eigenschaften für eine Datenbank  
 Das folgende Beispiel testet, wenn die Tabelle Spt_fallback_db in der **master** Datenbank durch das schemasignaturzertifikat signiert ist.  
  
```  
USE master;  
-- Declare a variable to hold a thumbprint and an object name  
DECLARE @thumbprint varbinary(20), @objectname sysname;  
  
-- Populate the thumbprint variable with the thumbprint of   
-- the master database schema signing certificate  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%';  
  
-- Populate the object name variable with a table name in master  
SELECT @objectname = 'spt_fallback_db';  
  
-- Query to see if the table is signed by the thumbprint  
SELECT @objectname AS [object name],  
IS_OBJECTSIGNED(  
'OBJECT', OBJECT_ID(@objectname), 'certificate', @thumbprint  
) AS [Is the object signed?] ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. fn_check_object_signatures &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-check-object-signatures-transact-sql.md)  
  
  
