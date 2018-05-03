---
title: DECRYPTBYKEY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DecryptByKey_TSQL
- DECRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], DecryptByKey function
- decryption [SQL Server], keys
- decryption [SQL Server], symmetric keys
- DECRYPTBYKEY function
ms.assetid: 6edf121f-ac62-4dae-90e6-6938f32603c9
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3d3064da25a280e7fe0d2534e7b2b2040094fbc3
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="decryptbykey-transact-sql"></a>DECRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Entschlüsselt Daten mit einem symmetrischen Schlüssel.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DecryptByKey ( { 'ciphertext' | @ciphertext }   
    [ , add_authenticator, { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *ciphertext*  
 Mit dem Schlüssel verschlüsselte Daten. *ciphertext* ist vom Datentyp **varbinary**.  
  
 **@ciphertext**  
 Eine Variable vom Datentyp **varbinary** , in der die mit dem Schlüssel verschlüsselten Daten enthalten sind.  
  
 *add_authenticator*  
 Gibt an, ob zusammen mit dem Nur-Text auch ein Authentifikator verschlüsselt wurde. Dies muss derselbe Wert sein, der beim Verschlüsseln der Daten an EncryptByKey übergeben wurde. *add_authenticator* ist vom Datentyp **int**.  
  
 *authenticator*  
 Die Daten, aus denen ein Authentifikator generiert werden soll. Dies muss derselbe Wert sein, der an EncryptByKey übergeben wurde. *authenticator* ist vom Datentyp **sysname**.  
  
 **@authenticator**  
 Eine Variable, die Daten enthält, aus denen ein Authentifikator generiert werden soll. Dies muss derselbe Wert sein, der an EncryptByKey übergeben wurde.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varbinary** mit einer maximalen Größe von 8.000 Bytes.
 
Gibt NULL zurück, wenn der symmetrische Schlüssel, der für das Verschlüsseln der Daten verwendet wurde, nicht geöffnet ist oder *ciphertext* den Wert NULL aufweist.
  
## <a name="remarks"></a>Remarks  
 DecryptByKey verwendet einen symmetrischen Schlüssel. Dieser symmetrische Schlüssel muss bereits in der Datenbank geöffnet sein. Es können mehrere Schlüssel gleichzeitig geöffnet sein. Der Schlüssel muss nicht unmittelbar vor dem Entschlüsseln von verschlüsseltem Text geöffnet werden.  
  
 Die symmetrische Ver- und Entschlüsselung erfolgt relativ schnell und kann auch bei großen Datenmengen verwendet werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert, dass der symmetrische Schlüssel in der aktuellen Sitzung geöffnet wurde. Weitere Informationen finden Sie unter [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-decrypting-by-using-a-symmetric-key"></a>A. Entschlüsseln mit einem symmetrischen Schlüssel  
 Im folgenden Beispiel wird verschlüsselter Text mit einem symmetrischen Schlüssel entschlüsselt.  
  
```  
-- First, open the symmetric key with which to decrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
GO  
  
-- Now list the original ID, the encrypted ID, and the   
-- decrypted ciphertext. If the decryption worked, the original  
-- and the decrypted ID will match.  
SELECT NationalIDNumber, EncryptedNationalID   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalID))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-decrypting-by-using-a-symmetric-key-and-an-authenticating-hash"></a>B. Entschlüsseln mit einem symmetrischen Schlüssel und einem Authentifizierungshash  
 Im folgenden Beispiel werden Daten entschlüsselt, die zusammen mit einem Authentifikator verschlüsselt wurden.  
  
```  
-- First, open the symmetric key with which to decrypt the data  
OPEN SYMMETRIC KEY CreditCards_Key11  
   DECRYPTION BY CERTIFICATE Sales09;  
GO  
  
-- Now list the original card number, the encrypted card number,  
-- and the decrypted ciphertext. If the decryption worked,   
-- the original number will match the decrypted number.  
SELECT CardNumber, CardNumber_Encrypted   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByKey(CardNumber_Encrypted, 1 ,   
    HashBytes('SHA1', CONVERT(varbinary, CreditCardID))))   
    AS 'Decrypted card number' FROM Sales.CreditCard;  
GO  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Auswählen eines Verschlüsselungsalgorithmus](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
