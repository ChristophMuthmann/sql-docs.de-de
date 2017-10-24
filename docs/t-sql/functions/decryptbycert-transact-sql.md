---
title: DECRYPTBYCERT (Transact-SQL) | Microsoft Docs
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
- DecryptByCert_TSQL
- DECRYPTBYCERT
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], decryption
- decryption [SQL Server], certificates
- DECRYPTBYCERT function
ms.assetid: 4950d787-40fa-4e26-bce8-2cb2ceca12fb
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ebdc328e49635af823cd64e8539ee5b7cfa95c76
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbycert-transact-sql"></a>DECRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Entschlüsselt Daten mithilfe des privaten Schlüssels eines Zertifikats.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DecryptByCert ( certificate_ID , { 'ciphertext' | @ciphertext }   
    [ , { 'cert_password' | @cert_password } ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Zertifikat-ID*  
 Die ID eines Zertifikats in der Datenbank. *certificate*_ID ist vom Datentyp **int**.  
  
 *Chiffretext*  
 Eine Datenzeichenfolge, die mithilfe des öffentlichen Schlüssels des Zertifikats verschlüsselt wurde.  
  
 @ciphertext  
 Eine Variable vom Datentyp **varbinary** , in der die mit dem Zertifikat verschlüsselten Daten enthalten sind.  
  
 *cert_password*  
 Das Kennwort, das zum Verschlüsseln des privaten Schlüssels des Zertifikats verwendet wurde. Muss Unicode sein.  
  
 @cert_password  
 Eine Variable vom Typ **nchar** oder **nvarchar** , die das Kennwort enthält, mit dem der private Schlüssel des Zertifikats verschlüsselt wurde. Muss Unicode sein.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varbinary** mit einer maximalen Größe von 8.000 Bytes.  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion entschlüsselt Daten mithilfe des privaten Schlüssels eines Zertifikats. Kryptografische Umwandlungen, die asymmetrische Schlüssel verwenden, nehmen umfangreiche Ressourcen in Anspruch. Daher sind EncryptByCert und DecryptByCert für die Routineverschlüsselung von Benutzerdaten nicht geeignet.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für das Zertifikat.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden in `[AdventureWorks2012].[ProtectedData04]` Zeilen ausgewählt, die als `data encrypted by certificate JanainaCert02`markiert sind. Im Beispiel wird der verschlüsselte Text mithilfe des privaten Schlüssels des Zertifikats `JanainaCert02`entschlüsselt, das zuerst mithilfe des Kennworts `pGFD4bb925DGvbd2439587y`des Zertifikats entschlüsselt wird. Die entschlüsselten Daten werden von **varbinary** in **nvarchar**konvertiert.  
  
```  
SELECT convert(nvarchar(max), DecryptByCert(Cert_Id('JanainaCert02'),  
    ProtectedData, N'pGFD4bb925DGvbd2439587y'))  
FROM [AdventureWorks2012].[ProtectedData04]   
WHERE Description   
    = N'data encrypted by certificate '' JanainaCert02''';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ENCRYPTBYCERT &#40; Transact-SQL &#41;](../../t-sql/functions/encryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

