---
title: DECRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYASYMKEY
- DECRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], DECRYPTBYASYMKEY function
- DECRYPTBYASYMKEY function
- decryption [SQL Server], asymmetric keys
ms.assetid: d9ebcd30-f01c-4cfe-b95e-ffe6ea13788b
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7196e7eedf5d1a808853df55259fcee1891c345
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
  
  

