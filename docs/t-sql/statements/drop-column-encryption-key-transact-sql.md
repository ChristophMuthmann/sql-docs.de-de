---
title: DROP COLUMN ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP COLUMN ENCRYPTION
- DROP COLUMN ENCRYPTION KEY
- DROP_COLUMN_ENCRYPTION_TSQL
- DROP_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP COLUMN ENCRYPTION KEY statement
- column encryption key, drop
ms.assetid: 86415302-1383-4d36-9fc7-f780831a2d37
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47208c011acad2d06fdf91cb3762474ca848e23e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-column-encryption-key-transact-sql"></a>DROP COLUMN ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Löscht einen Verschlüsselungsschlüssel für die Spalte aus einer Datenbank an.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP COLUMN ENCRYPTION KEY key_name [;]  
```  
  
## <a name="arguments"></a>Argumente  
 *Key_name*  
 Ist der Name, mit dem die spaltenverschlüsselung-Taste, um aus der Datenbank gelöscht werden.  
  
## <a name="remarks"></a>Hinweise  
 Ein spaltenverschlüsselungsschlüssel kann nicht gelöscht werden, wenn es verwendet wird, um eine Spalte in der Datenbank zu verschlüsseln. Alle Spalten, die mithilfe des Verschlüsselungsschlüssels für die Spalte müssen zuerst gelöscht werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **ALTER ANY COLUMN ENCRYPTION KEY** Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-dropping-a-column-encryption-key"></a>A. Löschen eines spaltenverschlüsselungsschlüssels  
 Das folgende Beispiel löscht einen spaltenverschlüsselungsschlüssel namens `MyCEK`.  
  
```  
DROP COLUMN ENCRYPTION KEY MyCEK;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Always Encrypted &#40;Datenbankmodul&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)  
  
  

