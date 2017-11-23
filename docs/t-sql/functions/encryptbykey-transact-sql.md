---
title: ENCRYPTBYKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- ENCRYPTBYKEY_TSQL
- ENCRYPTBYKEY
dev_langs: TSQL
helpviewer_keywords:
- authenticators [SQL Server]
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYKEY function
- ENCRYPTBYKEY function
ms.assetid: 0e11f8c5-f79d-46c1-ab11-b68ef05d6787
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fe0267020c4100794593731c0f0651b35ea30395
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="encryptbykey-transact-sql"></a>ENCRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verschlüsselt Daten mithilfe eines symmetrischen Schlüssels.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EncryptByKey ( key_GUID , { 'cleartext' | @cleartext }  
    [, { add_authenticator | @add_authenticator }  
     , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *key_GUID*  
 Ist die GUID des Schlüssels zum Verschlüsseln zu verwendende der *Klartext*. **"uniqueidentifier"**.  
  
 "*Klartext*"  
 Bezeichnet die mithilfe des Schlüssels zu verschlüsselnden Daten.  
  
 @cleartext  
 Eine Variable vom Typ **Nvarchar**, **Char**, **Varchar**, **binäre**, **Varbinary**, oder **Nchar** , die Daten enthält, die mit dem Schlüssel verschlüsselt werden soll.  
  
 *add_authenticator*  
 Gibt an, ob ein Authentifikator zusammen mit verschlüsselt werden, die *Klartext*. Muss beim Verwenden eines Authentifikators 1 sein. **int**.  
  
 @add_authenticator  
 Gibt an, ob ein Authentifikator zusammen mit verschlüsselt werden, die *Klartext*. Muss beim Verwenden eines Authentifikators 1 sein. **int**.  
  
 *Authenticator*  
 Bezeichnet die Daten, aus denen ein Authentifikator abgeleitet wird. **sysname**.  
  
 @authenticator  
 Eine Variable, die Daten enthält, von denen ein Authentifikator abgeleitet werden soll.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varbinary** mit einer maximalen Größe von 8.000 Bytes.  
  
 Gibt NULL zurück, wenn der Schlüssel nicht geöffnet, nicht vorhanden oder ein veralteter RC4-Schlüssel ist und die Datenbank nicht mindestens den Kompatibilitätsgrad 110 aufweist.  
  
## <a name="remarks"></a>Hinweise  
 EncryptByKey verwendet einen symmetrischen Schlüssel. Dieser Schlüssel muss geöffnet sein. Wenn der symmetrische Schlüssel in der aktuellen Sitzung bereits geöffnet ist, ist es nicht notwendig, ihn im Kontext der Abfrage erneut zu öffnen.  
  
 Mit dem Authentifikator kann verhindert werden, dass ganze Werte in verschlüsselten Feldern ersetzt werden. Betrachten Sie dazu beispielsweise die folgende Tabelle mit Daten zu Gehältern.  
  
|Employee_ID|Standard_Title|Base_Pay|  
|------------------|---------------------|---------------|  
|345|Kopierraumhilfe|Fskj%7^edhn00|  
|697|Leiter der Finanzabteilung|M0x8900f56543|  
|694|EDV-Leiter|Cvc97824%^34f|  
  
 Ohne die Verschlüsselung aufzubrechen, kann ein böswilliger Benutzer wichtige Informationen aus dem Kontext folgern, in dem der verschlüsselte Text gespeichert wird. Da ein Leiter der Finanzabteilung besser als eine Kopierraumhilfe verdient, folgt daraus, dass der als M0x8900f56543 verschlüsselte Wert größer als der als Fskj%7^edhn00 verschlüsselte Wert sein muss. Wenn dies der Fall ist, kann jeder beliebige Benutzer mit der ALTER-Berechtigung für die Tabelle der Kopierraumhilfe eine Gehaltserhöhung verschaffen, indem die Daten in seinem Base_Pay-Feld durch eine Kopie der im Base_Pay-Feld gespeicherten Daten des Leiters der Finanzabteilung ersetzt werden. Dieser ganzwertige Ersetzungsangriff umgeht die Verschlüsselung insgesamt.  
  
 Ganzwertige Ersetzungsangriffe können durch Hinzufügen von Kontextinformationen zum Klartext vereitelt werden, bevor dieser verschlüsselt wird. Diese Kontextinformationen werden zum Überprüfen verwendet, ob die Klartextdaten verschoben wurden.  
  
 Wenn ein authenticator-Parameter beim Verschlüsseln der Daten angegeben wird, wird der gleiche Authentifikator zum Entschlüsseln der Daten mithilfe von DecryptByKey benötigt. Zur Verschlüsselungszeit wird ein Hash des Authentifikators zusammen mit dem Klartext verschlüsselt. Zur Entschlüsselungszeit muss der gleiche Authentifikator an DecryptByKey übergeben werden. Stimmen beide nicht überein, schlägt die Entschlüsselung fehl. Dies zeigt an, dass der Wert seit seiner Verschlüsselung verschoben wurde. Es empfiehlt sich, eine Spalte zu verwenden, die einen eindeutigen und unveränderlichen Wert als Authentifikator enthält. Wenn sich der Authentifikatorwert ändert, verlieren Sie möglicherweise den Zugriff auf die Daten.  
  
 Die symmetrische Ver- und Entschlüsselung erfolgt relativ schnell und kann auch bei großen Datenmengen verwendet werden.  
  
> [!IMPORTANT]  
>  Das Verwenden der Veschlüsselungsfunktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zusammen mit der ANSI_PADDING OFF-Einstellung kann aufgrund implizierter Konvertierungen zu Datenverlust führen. Weitere Informationen zu ANSI_PADDING finden Sie unter [SET ANSI_PADDING &#40; Transact-SQL &#41; ](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen veranschaulichte Funktionalität beruht auf Schlüsseln und Zertifikaten, [Vorgehensweise: Verschlüsseln einer Datenspalte](../../relational-databases/security/encryption/encrypt-a-column-of-data.md).  
  
### <a name="a-encrypting-a-string-with-a-symmetric-key"></a>A. Verschlüsseln einer Zeichenfolge mithilfe eines symmetrischen Schlüssels  
 Im folgenden Beispiel wird der `Employee`-Tabelle eine Spalte hinzugefügt und dann der Wert der Sozialversicherungsnummer in der `NationalIDNumber`-Spalte verschlüsselt.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
  
-- Encrypt the value in column NationalIDNumber with symmetric key  
-- SSN_Key_01. Save the result in column EncryptedNationalIDNumber.  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
```  
  
### <a name="b-encrypting-a-record-together-with-an-authentication-value"></a>B. Verschlüsseln eines Datensatzes zusammen mit einem Authentifizierungswert  
  
```  
USE AdventureWorks2012;  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard.   
    ADD CardNumber_Encrypted varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY CreditCards_Key11  
    DECRYPTION BY CERTIFICATE Sales09;  
  
-- Encrypt the value in column CardNumber with symmetric   
-- key CreditCards_Key11.  
-- Save the result in column CardNumber_Encrypted.    
UPDATE Sales.CreditCard  
SET CardNumber_Encrypted = EncryptByKey(Key_GUID('CreditCards_Key11'),   
    CardNumber, 1, CONVERT( varbinary, CreditCardID) );  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DECRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [HASHBYTES &#40; Transact-SQL &#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
  
  
