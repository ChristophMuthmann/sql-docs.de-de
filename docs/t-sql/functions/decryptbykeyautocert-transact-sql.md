---
title: DECRYPTBYKEYAUTOCERT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 98c1a841c9b160001c3927c0f6b44ea8cf2fc22b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="decryptbykeyautocert-transact-sql"></a>DECRYPTBYKEYAUTOCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt mithilfe eines symmetrischen Schlüssels, der mit einem Zertifikat automatisch entschlüsselt wird, eine Entschlüsselung durch.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *CERT_ID*  
 Die ID des Zertifikats, das zum Schützen des symmetrischen Schlüssels verwendet wird. *Cert_ID* ist vom Datentyp **int**.  
  
 *cert_password*  
 Das Kennwort, mit dem der private Schlüssel des Zertifikats geschützt ist. Kann NULL sein, wenn der private Schlüssel durch den Hauptschlüssel für die Datenbank geschützt ist. *cert_password* ist vom Datentyp **nvarchar**.  
  
 '*ciphertext*'  
 Die mit dem Schlüssel verschlüsselten Daten. *ciphertext* ist vom Datentyp **varbinary**.  
  
 @ciphertext  
 Eine Variable vom Datentyp **varbinary** , in der die mit dem Schlüssel verschlüsselten Daten enthalten sind.  
  
 *add_authenticator*  
 Gibt an, ob zusammen mit dem Nur-Text auch ein Authentifikator verschlüsselt wurde. Dies muss derselbe Wert sein, der beim Verschlüsseln der Daten an EncryptByKey übergeben wurde. Hat den Wert **1**, wenn ein Authentifikator verwendet wurde. *add_authenticator* ist vom Datentyp **int**.  
  
 @add_authenticator  
 Gibt an, ob zusammen mit dem Nur-Text auch ein Authentifikator verschlüsselt wurde. Dies muss derselbe Wert sein, der beim Verschlüsseln der Daten an EncryptByKey übergeben wurde.  
  
 *authenticator*  
 Bezeichnet die Daten, aus denen ein Authentifikator generiert wird. Dies muss derselbe Wert sein, der an EncryptByKey übergeben wurde. *authenticator* ist vom Datentyp **sysname**.  
  
 @authenticator  
 Eine Variable, die Daten enthält, aus denen ein Authentifikator generiert werden soll. Dies muss derselbe Wert sein, der an EncryptByKey übergeben wurde.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varbinary** mit einer maximalen Größe von 8.000 Bytes.  
  
## <a name="remarks"></a>Remarks  
 In DecryptByKeyAutoCert ist die Funktionalität von OPEN SYMMETRIC KEY und von DecryptByKey kombiniert. In einem einzelnen Vorgang wird ein symmetrischer Schlüssel entschlüsselt und mit diesem Schlüssel der verschlüsselte Text entschlüsselt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DEFINITION-Berechtigung für den symmetrischen Schlüssel und die CONTROL-Berechtigung für das Zertifikat.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird gezeigt, wie Code, mit dem eine Entschlüsselung ausgeführt wird, mit `DecryptByKeyAutoCert` vereinfacht werden kann. Dieser Code sollte für eine [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank ausgeführt werden, die nicht bereits über einen Datenbank-Hauptschlüssel verfügt.  
  
```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE CERTIFICATE HumanResources037   
   WITH SUBJECT = 'Sammamish HR',   
   EXPIRY_DATE = '10/31/2009';  
CREATE SYMMETRIC KEY SSN_Key_01 WITH ALGORITHM = DES  
    ENCRYPTION BY CERTIFICATE HumanResources037;  
GO  
----Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037 ;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
--  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key  
--2. Decrypt the data  
--3. Close the symmetric key  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
SELECT NationalIDNumber, EncryptedNationalIDNumber    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--OPTION TWO, using DecryptByKeyAutoCert()  
SELECT NationalIDNumber, EncryptedNationalIDNumber   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoCert ( cert_ID('HumanResources037') , NULL ,EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
