---
title: Sys. fn_check_object_signatures (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_check_object_signatures_TSQL
- fn_check_object_signatures_TSQL
- fn_check_object_signatures
- sys.fn_check_object_signatures
dev_langs: TSQL
helpviewer_keywords: sys.fn_check_object_signatures function
ms.assetid: 47509566-d3d7-46a9-89c1-91b4895d56b9
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b4f237723380c7220086f4b6642609f6e9177315
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysfncheckobjectsignatures-transact-sql"></a>sys.fn_check_object_signatures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Gibt eine Liste mit allen signierbaren Objekten zurück und gibt an, ob ein Objekt von einem angegebenen Zertifikat oder asymmetrischem Schlüssel signiert wird. Wenn das Objekt von dem angegebenen Zertifikat dem asymmetrischen Schlüssel signiert wird, gibt sie außerdem zurück, ob die Signatur des Objekts gültig ist.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn_ check_object_signatures (   
    { '@class' } , { @thumbprint }   
  )   
```  
  
## <a name="arguments"></a>Argumente  
 {' @*Klasse*'}  
 Identifiziert den Typ des Fingerabdrucks, der bereitgestellt wird:  
  
-   ‚Zertifikat’  
  
-   ‚asymmetrischer Schlüssel’  
  
 @*Klasse* ist **Sysname**.  
  
 {@*Fingerabdruck* }  
 SHA-1-Hash des Zertifikats, mit dem der Schlüssel verschlüsselt wird, oder der GUID des asymmetrischen Schlüssels, mit dem der Schlüssel verschlüsselt wird. @*Fingerabdruck* ist **varbinary(20)**.  
  
## <a name="tables-returned"></a>Zurückgegebene Tabellen  
 Die folgende Tabelle enthält die Spalten, die **Fn_check_object_signatures** zurückgibt.  
  
|Column|Typ|Description|  
|------------|----------|-----------------|  
|Typ|**nvarchar(120)**|Gibt die Typbeschreibung oder -assembly zurück.|  
|entity_id|**int**|Gibt die Objekt-ID des Objekts zurück, das ausgewertet wird.|  
|is_signed|**int**|Gibt 0 zurück, wenn das Objekt nicht durch den bereitgestellten Fingerabdruck signiert wird. Gibt 1 zurück, wenn das Objekt durch den bereitgestellten Fingerabdruck signiert wird.|  
|is_signature_valid|**int**|Wenn der is_signed-Wert 1 ist, wird 0 zurückgegeben, wenn die Signatur nicht gültig ist. Gibt den Wert 1 zurück, wenn die Signatur gültig ist.<br /><br /> Wenn der is_signed-Wert 0 ist, wird immer 0 zurückgegeben.|  
  
## <a name="remarks"></a>Hinweise  
 Verwendung **Fn_check_object_signatures** zu bestätigen, dass böswillige Benutzer Objekte nicht manipuliert wurden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DEFINITION-Berechtigung für das Zertifikat oder den asymmetrischen Schlüssel.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das Schemasignaturzertifikat für die `master`-Datenbank gefunden und der `is_signed`-Wert von 1 und der `is_signature_valid`-Wert von 1 für diejenigen Objekte zurückgegeben, die durch das Schemasignaturzertifikat signiert werden und die gültige Signaturen aufweisen.  
  
```  
USE master;  
-- Declare a variable to hold the thumbprint.  
DECLARE @thumbprint varbinary(20) ;  
-- Populate the thumbprint variable with the master database schema signing certificate.  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%' ;  
-- Evaluates the objects signed by the schema signing certificate  
SELECT type, entity_id, OBJECT_NAME(entity_id) AS [object name], is_signed, is_signature_valid  
FROM sys.fn_check_object_signatures ('certificate', @thumbprint) ;  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [IS_OBJECTSIGNED &#40; Transact-SQL &#41;](../../t-sql/functions/is-objectsigned-transact-sql.md)  
  
  
