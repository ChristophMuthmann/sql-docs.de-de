---
title: DECRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
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
- DECRYPTBYASYMKEY
- DECRYPTBYASYMKEY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], DECRYPTBYASYMKEY function
- DECRYPTBYASYMKEY function
- decryption [SQL Server], asymmetric keys
ms.assetid: d9ebcd30-f01c-4cfe-b95e-ffe6ea13788b
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c85f80e0b8df4f2e61ad0d5f20e9e5ba4d8b582
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Entschlüsselt Daten mit einem asymmetrischen Schlüssel.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Asym_Key_ID*  
 Die ID eines asymmetrischen Schlüssels in der Datenbank. *Asym_Key_ID* ist vom Datentyp **int**.  
  
 *Chiffretext*  
 Eine Zeichenfolge mit Daten, die mit dem asymmetrischen Schlüssel verschlüsselt wurden.  
  
 @ciphertext  
 Eine Variable vom Typ **varbinary** , die Daten enthält, die mit dem asymmetrischen Schlüssel verschlüsselt wurden.  
  
 *Asym_Key_Password*  
 Das Kennwort, mit dem der asymmetrische Schlüssel in der Datenbank verschlüsselt wurde.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varbinary** mit einer maximalen Größe von 8.000 Bytes.  
  
## <a name="remarks"></a>Hinweise  
 Das Verschlüsseln/Entschlüsseln mit einem asymmetrischen Schlüssel ist im Vergleich zum Verschlüsseln/Entschlüsseln mit einem symmetrischen Schlüssel sehr teuer. Von einem asymmetrischen Schlüssel wird abgeraten, wenn Sie große Datasets wie z. B. Benutzerdaten in Tabellen verwenden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für den asymmetrischen Schlüssel.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird verschlüsselter Text entschlüsselt, der mit dem asymmetrischen Schlüssel `JanainaAsymKey02`verschlüsselt wurde, der in `AdventureWorks2012.ProtectedData04`gespeichert war. Die zurückgegebenen Daten werden mit dem asymmetrischen Schlüssel `JanainaAsymKey02`entschlüsselt, der mit dem Kennwort `pGFD4bb925DGvbd2439587y`entschlüsselt wurde. Der Nur-Text wird in den Datentyp **nvarchar**konvertiert.  
  
```  
SELECT CONVERT(nvarchar(max),  
    DecryptByAsymKey( AsymKey_Id('JanainaAsymKey02'),   
    ProtectedData, N'pGFD4bb925DGvbd2439587y' ))   
AS DecryptedData   
FROM [AdventureWorks2012].[Sales].[ProtectedData04]   
WHERE Description = N'encrypted by asym key''JanainaAsymKey02''';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ENCRYPTBYASYMKEY &#40; Transact-SQL &#41;](../../t-sql/functions/encryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Auswählen eines Verschlüsselungsalgorithmus](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
