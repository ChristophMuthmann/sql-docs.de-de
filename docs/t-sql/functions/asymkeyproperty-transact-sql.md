---
title: ASYMKEYPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
- ASYMKEYPROPERTY_TSQL
- ASYMKEYPROPERTY
dev_langs: TSQL
helpviewer_keywords: ASYMKEYPROPERTY
ms.assetid: a30581f2-e1b1-4996-93e6-527ff96b7c42
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 808f7c8d840f18d9e09fe9906e366fb7feb76cff
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="asymkeyproperty-transact-sql"></a>ASYMKEYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die Eigenschaften eines asymmetrischen Schlüssels zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
ASYMKEYPROPERTY (Key_ID , 'algorithm_desc' | 'string_sid' | 'sid')  
```  
  
## <a name="arguments"></a>Argumente  
*Key_ID*  
Die Key_ID eines asymmetrischen Schlüssels in der Datenbank. Um die Key_ID zu ermitteln, wenn Sie nur den Schlüsselnamen kennen, verwenden Sie die ASYMKEY_ID. *Key_ID* ist vom Datentyp **int**.
  
**‚**algorithm_desc**’**  
Gibt an, dass die Ausgabe die Algorithmusbeschreibung des asymmetrischen Schlüssels zurückgibt. Nur verfügbar für aus einem EKM-Modul erstellte asymmetrische Schlüssel.
  
**‚**string_sid**’**  
Gibt an, dass die Ausgabe die SID des asymmetrischen Schlüssels im **nvarchar()** -Format zurückgibt.
  
**'**sid**'**  
Gibt an, dass die Ausgabe die SID des asymmetrischen Schlüssels im Binärformat zurückgibt.
  
## <a name="return-types"></a>Rückgabetypen  
**sql_variant**
  
## <a name="permissions"></a>Berechtigungen  
Erfordert bestimmte Berechtigungen für den asymmetrischen Schlüssel, und dem Aufrufer darf die VIEW-Berechtigung für den asymmetrischen Schlüssel nicht verweigert worden sein.
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel gibt die Eigenschaften des asymmetrischen Schlüssels mit der Key_ID 256 zurück.
  
```sql
SELECT   
ASYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm,  
ASYMKEYPROPERTY(256, 'string_sid') AS String_SID,  
ASYMKEYPROPERTY(256, 'sid') AS SID ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[ALTER ASYMMETRIC KEY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
[DROP ASYMMETRIC KEY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)  
[VERIFYSIGNEDBYASYMKEY &#40; Transact-SQL &#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)  
[Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[Sys. asymmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)  
[Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
[ASYMKEY_ID &#40; Transact-SQL &#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
[SYMKEYPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/symkeyproperty-transact-sql.md)
  
  
