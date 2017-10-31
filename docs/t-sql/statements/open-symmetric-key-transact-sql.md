---
title: OPEN SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
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
- OPEN SYMMETRIC KEY
- OPEN_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], opening
- OPEN SYMMETRIC KEY statement
ms.assetid: ff019a7c-c373-46c7-ac43-ffb7e2ee60b3
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd8302417e09eeef6e8052db6ced58c47cd25158
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="open-symmetric-key-transact-sql"></a>OPEN SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entschlüsselt einen symmetrischen Schlüssel und stellt ihn zur Verwendung zur Verfügung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
OPEN SYMMETRIC KEY Key_name DECRYPTION BY <decryption_mechanism>  
  
<decryption_mechanism> ::=  
    CERTIFICATE certificate_name [ WITH PASSWORD = 'password' ]  
    |  
    ASYMMETRIC KEY asym_key_name [ WITH PASSWORD = 'password' ]  
    |  
    SYMMETRIC KEY decrypting_Key_name  
    |  
    PASSWORD = 'decryption_password'  
```  
  
## <a name="arguments"></a>Argumente  
 *Key_name*  
 Der Name des zu öffnenden symmetrischen Schlüssels.  
  
 Zertifikat *Name*  
 Der Name eines Zertifikats, mit dessen privatem Schlüssel der symmetrische Schlüssel entschlüsselt wird.  
  
 ASYMMETRISCHE Schlüssel *Asym_key_name*  
 Der Name eines asymmetrischen Schlüssels, mit dessen privatem Schlüssel der symmetrische Schlüssel entschlüsselt wird.  
  
 MIT dem Kennwort = "*Kennwort*"  
 Das Kennwort, mit dem der private Schlüssel des Zertifikats oder des asymmetrischen Schlüssels verschlüsselt wurde.  
  
 SYMMETRISCHE Schlüssel *Decrypting_key_name*  
 Der Name eines symmetrischen Schlüssels, mit dem der symmetrische Schlüssel, der geöffnet wird, entschlüsselt wird.  
  
 Kennwort = "*Kennwort*"  
 Das Kennwort, mit dem der symmetrische Schlüssel geschützt wurde.  
  
## <a name="remarks"></a>Hinweise  
 Geöffnete symmetrische Schlüssel werden an die Sitzung gebunden und nicht an den Sicherheitskontext. Ein geöffneter Schlüssel ist weiterhin verfügbar, bis er entweder explizit geschlossen oder die Sitzung beendet wird. Wenn Sie einen symmetrischen Schlüssel öffnen und dann den Kontext wechseln, bleibt der Schlüssel geöffnet und in dem durch Identitätswechsel übernommenen Kontext verfügbar. Informationen zu offenen symmetrischen Schlüsseln werden in der [sys.openkeys & #40; Transact-SQL & #41; ](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md) -Katalogsicht angezeigt.  
  
 Falls der symmetrische Schlüssel mit einem anderen Schlüssel verschlüsselt wurde, muss zuerst dieser Schlüssel geöffnet werden.  
  
 Wenn der symmetrische Schlüssel bereits geöffnet ist, wird die Abfrage eine **NO_OP**.  
  
 Falls das falsche Kennwort, das falsche Zertifikat oder der falsche Schlüssel zum Entschlüsseln des symmetrischen Schlüssels bereitgestellt wurde, erzeugt die Abfrage einen Fehler.  
  
 Symmetrische Schlüssel, die von Kryptografieanbietern erstellt wurden, können nicht geöffnet werden. Verschlüsselung und Entschlüsselung-Vorgänge, die mit dieser Art von symmetrischem Schlüssel erfolgreich ausgeführt werden, ohne die **öffnen** Anweisung, da die Verschlüsselungsanbieter öffnen und schließen den Schlüssel ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Aufrufer benötigt bestimmte Berechtigungen für den Schlüssel, und die VIEW DEFINITION-Berechtigung für den Schlüssel darf ihm nicht verweigert worden sein. Zusätzliche Anforderungen hängen vom Entschlüsselungsmechanismus ab:  
  
-   DECRYPTION BY CERTIFICATE: CONTROL-Berechtigung für das Zertifikat und Kenntnis des Kennworts, mit dem der private Schlüssel verschlüsselt wird.  
  
-   DECRYPTION BY ASYMMETRIC KEY: CONTROL-Berechtigung für den asymmetrischen Schlüssel und Kenntnis des Kennworts, mit dem der private Schlüssel verschlüsselt wird.  
  
-   DECRYPTION BY PASSWORD: Kenntnis eines der Kennwörter, mit denen der symmetrische Schlüssel verschlüsselt wird.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-opening-a-symmetric-key-by-using-a-certificate"></a>A. Öffnen eines symmetrischen Schlüssels mithilfe eines Zertifikats  
 Im folgenden Beispiel wird der symmetrische Schlüssel `SymKeyMarketing3` geöffnet und mit dem privaten Schlüssel des `MarketingCert9`-Zertifikats entschlüsselt.  
  
```  
USE AdventureWorks2012;  
OPEN SYMMETRIC KEY SymKeyMarketing3   
    DECRYPTION BY CERTIFICATE MarketingCert9;  
GO  
```  
  
### <a name="b-opening-a-symmetric-key-by-using-another-symmetric-key"></a>B. Öffnen eines symmetrischen Schlüssels mithilfe eines anderen symmetrischen Schlüssels  
 Im folgenden Beispiel wird der symmetrische Schlüssel `MarketingKey11` geöffnet und mit dem symmetrischen Schlüssel `HarnpadoungsatayaSE3` entschlüsselt.  
  
```  
USE AdventureWorks2012;  
-- First open the symmetric key that you want for decryption.  
OPEN SYMMETRIC KEY HarnpadoungsatayaSE3   
    DECRYPTION BY CERTIFICATE sariyaCert01;  
-- Use the key that is already open to decrypt MarketingKey11.  
OPEN SYMMETRIC KEY MarketingKey11   
    DECRYPTION BY SYMMETRIC KEY HarnpadoungsatayaSE3;  
GO   
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [CLOSE SYMMETRIC KEY & #40; Transact-SQL & #41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  

