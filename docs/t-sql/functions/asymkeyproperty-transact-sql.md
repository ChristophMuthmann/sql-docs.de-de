---
title: ASYMKEYPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASYMKEYPROPERTY_TSQL
- ASYMKEYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASYMKEYPROPERTY
ms.assetid: a30581f2-e1b1-4996-93e6-527ff96b7c42
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62ed19d07264d971045582c093a4c5ccdf6d8926
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="asymkeyproperty-transact-sql"></a>ASYMKEYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
  
  

