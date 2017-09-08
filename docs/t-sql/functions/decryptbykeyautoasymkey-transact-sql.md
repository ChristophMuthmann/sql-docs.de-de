---
title: DECRYPTBYKEYAUTOASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/09/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOASYMKEY_TSQL
- DECRYPTBYKEYAUTOASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOASYMSKEY function
ms.assetid: 5521d4cf-740c-4ede-98b6-4ba90b84e32d
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 74aa8bad7e6d848296ef2997017758883226ac48
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbykeyautoasymkey-transact-sql"></a>DECRYPTBYKEYAUTOASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entschlüsselt Text mithilfe eines symmetrischen Schlüssels, der automatisch mithilfe eines asymmetrischen Schlüssels entschlüsselt wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DecryptByKeyAutoAsymKey ( akey_ID , akey_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *akey_ID*  
 Die ID des asymmetrischen Schlüssels, der zum Schützen des symmetrischen Schlüssels verwendet wird. *akey_ID* ist **int**  
  
 *akey_password*  
 Das Kennwort, durch das der private Schlüssel des asymmetrischen Schlüssels geschützt wird. Kann NULL sein, wenn der private Schlüssel durch den Hauptschlüssel für die Datenbank geschützt ist. *akey_password* ist **nvarchar**  
  
 '*ciphertext*'  
 Die mit dem Schlüssel verschlüsselten Daten. *ciphertext* ist vom Datentyp **varbinary**.  
  
 @ciphertext  
 Eine Variable vom Datentyp **varbinary** , in der die mit dem Schlüssel verschlüsselten Daten enthalten sind.  
  
 *add_authenticator*  
 Gibt an, ob zusammen mit dem Nur-Text auch ein Authentifikator verschlüsselt wurde. Dies muss derselbe Wert sein, der beim Verschlüsseln der Daten an EncryptByKey übergeben wurde. Hat den Wert 1, wenn ein Authentifikator verwendet wurde. *add_authenticator* ist vom Datentyp **int**.  
  
 @add_authenticator  
 Gibt an, ob zusammen mit dem Nur-Text auch ein Authentifikator verschlüsselt wurde. Dies muss derselbe Wert sein, der beim Verschlüsseln der Daten an EncryptByKey übergeben wurde.  
  
 *Authenticator*  
 Bezeichnet die Daten, aus denen ein Authentifikator generiert wird. Dies muss derselbe Wert sein, der an EncryptByKey übergeben wurde. *authenticator* ist vom Datentyp **sysname**.  
  
 @authenticator  
 Eine Variable, die Daten enthält, aus denen ein Authentifikator generiert werden soll. Dies muss derselbe Wert sein, der an EncryptByKey übergeben wurde.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varbinary** mit einer maximalen Größe von 8.000 Bytes.  
  
## <a name="remarks"></a>Hinweise  
 In DecryptByKeyAutoAsymKey ist die Funktionalität von OPEN SYMMETRIC KEY und von DecryptByKey kombiniert. In einem einzelnen Vorgang wird ein symmetrischer Schlüssel entschlüsselt und mit diesem Schlüssel der verschlüsselte Text entschlüsselt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DEFINITION-Berechtigung für den symmetrischen Schlüssel und die CONTROL-Berechtigung für den asymmetrischen Schlüssel.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird gezeigt, wie Code, mit dem eine Entschlüsselung ausgeführt wird, mit `DecryptByKeyAutoAsymKey` vereinfacht werden kann. Dieser Code sollte ausgeführt werden, auf eine [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank, die nicht bereits einen Datenbank-Hauptschlüssel verfügt.  
  
```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE ASYMMETRIC KEY SSN_AKey   
    WITH ALGORITHM = RSA_2048 ;   
GO  
CREATE SYMMETRIC KEY SSN_Key_02 WITH ALGORITHM = DES  
    ENCRYPTION BY ASYMMETRIC KEY SSN_AKey;  
GO  
--  
--Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber2 varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber2  
    = EncryptByKey(Key_GUID('SSN_Key_02'), NationalIDNumber);  
GO  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key.  
--2. Decrypt the data.  
--3. Close the symmetric key.  
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
SELECT NationalIDNumber, EncryptedNationalIDNumber2    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--OPTION TWO, using DecryptByKeyAutoAsymKey()  
SELECT NationalIDNumber, EncryptedNationalIDNumber2   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoAsymKey ( AsymKey_ID('SSN_AKey') , NULL ,EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

