---
title: ENCRYPTBYASYMKEY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff79a5a15cb293646d75d4a411632f58c3efe0de
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verschlüsselt Daten mit einem asymmetrischen Schlüssel.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>Argumente  
 *Asym_Key_ID*  
 Die ID eines asymmetrischen Schlüssels in der Datenbank. **int**.  
  
 *Klartext*  
 Eine Zeichenfolge der Daten, die mit dem asymmetrischen Schlüssel verschlüsselt werden.  
  
 **@plaintext**  
 Eine Variable vom Typ **nvarchar**, **char**, **varchar**, **binary**, **varbinary** oder **nchar** mit Daten, die mit dem asymmetrischen Schlüssel verschlüsselt werden sollen.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varbinary** mit einer maximalen Größe von 8.000 Bytes.  
  
## <a name="remarks"></a>Remarks  
 Das Verschlüsseln und Entschlüsseln mit einem asymmetrischen Schlüssel ist im Vergleich zum Verschlüsseln und Entschlüsseln mit einem symmetrischen Schlüssel sehr teuer. Es ist nicht empfehlenswert, große Datasets, wie z. B. Benutzerdaten in Tabellen, mithilfe eines asymmetrischen Schlüssels zu verschlüsseln. Stattdessen sollten Sie die Daten mithilfe eines starken symmetrischen Schlüssels verschlüsseln und den symmetrischen Schlüssel mithilfe eines asymmetrischen Schlüssels verschlüsseln.  
  
 **EncryptByAsymKey** gibt je nach Algorithmus **NULL** zurück, wenn die Eingabe eine bestimmte Anzahl von Bytes überschreitet. Die Grenzwerte lauten wie folgt: ein 512-Bit-RSA-Schlüssel kann bis zu 53 Bytes verschlüsseln, ein 1024-Bit-Schlüssel kann bis zu 117 Bytes verschlüsseln, und ein 2048-Bit-Schlüssel kann bis zu 245 Bytes verschlüsseln. (Beachten Sie, dass in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beide Zertifikate und asymmetrischen Schlüssel Wrapper für RSA-Schlüssel sind.)  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der in `@cleartext` gespeicherte Text mit dem asymmetrischen Schlüssel `JanainaAsymKey02` verschlüsselt. Die verschlüsselten Daten werden in die `ProtectedData04`-Tabelle eingefügt.  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
