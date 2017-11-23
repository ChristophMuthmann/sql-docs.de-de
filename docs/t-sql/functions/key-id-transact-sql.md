---
title: KEY_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- Key_ID
- Key_ID_TSQL
dev_langs: TSQL
helpviewer_keywords:
- identification numbers [SQL Server], symmetric keys
- KEY_ID function
- symmetric keys [SQL Server], IDs
- IDs [SQL Server], symmetric keys
ms.assetid: d7309542-dbbe-41dc-b42e-5d9a1c8b4838
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb01508366558f7d5f755db50efb4a5a5b0d937d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="keyid-transact-sql"></a>KEY_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die ID eines symmetrischen Schlüssels in der aktuellen Datenbank zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Key_ID ( 'Key_Name' )  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Key_Name* **"**  
 Der Name eines symmetrischen Schlüssels in der Datenbank.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 Der Name eines temporären Schlüssels muss mit einem Nummernzeichen (#) beginnen.  
  
## <a name="permissions"></a>Berechtigungen  
 Da temporäre Schlüssel nur während der Sitzung verfügbar sind, in der sie erstellt werden, sind für den Zugriff auf die Schlüssel keine Berechtigungen erforderlich. Um auf einen Schlüssel zuzugreifen, der nicht temporär ist, benötigt der Aufrufer eine Berechtigung für den Schlüssel und muss die VIEW-Berechtigung für den Schlüssel erhalten haben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-id-of-a-symmetric-key"></a>A. Zurückgeben der ID eines symmetrischen Schlüssels  
 Das folgende Beispiel gibt die ID eines Schlüssels mit dem Namen `ABerglundKey1` zurück.  
  
```  
SELECT KEY_ID('ABerglundKey1');  
```  
  
### <a name="b-returning-the-id-of-a-temporary-symmetric-key"></a>B. Zurückgeben der ID eines temporären symmetrischen Schlüssels  
 Das folgende Beispiel gibt die ID eines temporären symmetrischen Schlüssels zurück. `#` wird dem Schlüsselnamen vorangestellt.  
  
```  
SELECT KEY_ID('#ABerglundKey2');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [KEY_GUID &#40; Transact-SQL &#41;](../../t-sql/functions/key-guid-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Sys. symmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
