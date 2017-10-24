---
title: DECRYPTBYPASSPHRASE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYPASSPHRASE
- DECRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], DECRYPTBYPASSPHRASE function
- DECRYPTBYPASSPHRASE function
ms.assetid: ca34b5cd-07b3-4dca-b66a-ed8c6a826c95
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0af2f19acced57d722427c8f341db62dbdb34198
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbypassphrase-transact-sql"></a>DECRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Entschlüsselt Daten, die mit einer Passphrase verschlüsselt wurden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DecryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Passphrase*  
 Die Passphrase, die zum Generieren des Schlüssels für die Entschlüsselung verwendet wird.  
  
 @passphrase  
 Eine Variable vom Typ **nvarchar**, **char**, **varchar**oder **nchar** , die die Passphrase enthält, die zum Generieren des Schlüssels für die Entschlüsselung verwendet wird.  
  
 '*ciphertext*'  
 Der zu entschlüsselnde verschlüsselte Text.  
  
 @ciphertext  
 Eine Variable vom Typ **varbinary** , die den verschlüsselten Text enthält. Die maximale Größe beträgt 8.000 Bytes.  
  
 *add_authenticator*  
 Gibt an, ob zusammen mit dem Nur-Text auch ein Authentifikator verschlüsselt wurde. Hat den Wert 1, wenn ein Authentifikator verwendet wurde. **int**.  
  
 @add_authenticator  
 Gibt an, ob zusammen mit dem Nur-Text auch ein Authentifikator verschlüsselt wurde. Hat den Wert 1, wenn ein Authentifikator verwendet wurde. **int**.  
  
 *Authenticator*  
 Die Authentifikatordaten. **sysname**.  
  
 @authenticator  
 Eine Variable, die Daten enthält, von denen ein Authentifikator abgeleitet werden soll.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varbinary** mit einer maximalen Größe von 8.000 Bytes.  
  
## <a name="remarks"></a>Hinweise  
 Zum Ausführen dieser Funktion sind keine Berechtigungen erforderlich.  
  
 Gibt NULL zurück, wenn der falsche Passphrase oder falsche Authentifikatorinformationen verwendet werden.  
  
 Die Passphrase wird zum Generieren eines Entschlüsselungsschlüssels verwendet, der nicht persistent ist.  
  
 Falls beim Verschlüsseln des verschlüsselten Texts ein Authentifikator eingeschlossen wurde, muss der Authentifikator zur Entschlüsselungszeit bereitgestellt werden. Falls der zur Entschlüsselungszeit bereitgestellte Authentifikatorwert nicht mit dem mit den Daten verschlüsselten Authentifikatorwert übereinstimmt, kann die Entschlüsselung nicht ausgeführt werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die im aktualisierte Datensatz entschlüsselt [EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
-- Get the pass phrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
= 'A little learning is a dangerous thing!';  
  
-- Decrypt the encrypted record.  
SELECT CardNumber, CardNumber_EncryptedbyPassphrase   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByPassphrase(@PassphraseEnteredByUser, CardNumber_EncryptedbyPassphrase, 1   
    , CONVERT(varbinary, CreditCardID)))  
    AS 'Decrypted card number' FROM Sales.CreditCard   
    WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Auswählen eines Verschlüsselungsalgorithmus](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
  
  

