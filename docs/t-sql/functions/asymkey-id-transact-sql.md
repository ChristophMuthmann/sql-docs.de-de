---
title: ASYMKEY_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AsymKey_ID
- ASYMKEY_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], AsymKey_ID
- ASYMKEY_ID function
- encryption [SQL Server], asymmetric keys
- identification numbers [SQL Server], asymmetric keys
- IDs [SQL Server], asymmetric keys
- cryptography [SQL Server], asymmetric keys
ms.assetid: d697daf8-2106-4ebb-b09a-ca0be465d747
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf4f12b058c3a4df46679d1d4d5bf9bd56958deb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="asymkeyid-transact-sql"></a>ASYMKEY_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die ID eines asymmetrischen Schlüssels zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
ASYMKEY_ID ( 'Asym_Key_Name' )  
```  
  
## <a name="arguments"></a>Argumente  
*Asym_Key_Name*  
Der Name eines asymmetrischen Schlüssels in der Datenbank.
  
## <a name="return-types"></a>Rückgabetypen
 **int**  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert bestimmte Berechtigungen für den asymmetrischen Schlüssel, und dem Aufrufer darf die VIEW-Berechtigung für den asymmetrischen Schlüssel nicht verweigert worden sein.
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel gibt die ID des asymmetrischen Schlüssels `ABerglundKey11`zurück.
  
```sql
SELECT ASYMKEY_ID('ABerglundKey11');  
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
[ASYMKEYPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/asymkeyproperty-transact-sql.md)  
[KEY_ID &#40; Transact-SQL &#41;](../../t-sql/functions/key-id-transact-sql.md)
  
  
