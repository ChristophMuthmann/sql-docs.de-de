---
title: CERTENCODED (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
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
- CERTENCODED
- CERTENCODED_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTENCODED
ms.assetid: 677a0719-7b9a-4f0b-bc61-41634563f924
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6068562cf6694acc99c1e303dbd4ff10ff583ce
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="certencoded-transact-sql"></a>CERTENCODED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Diese Funktion gibt den öffentlichen Teil eines Zertifikats im Binärformat zurück. Diese Funktion akzeptiert eine Zertifikat-ID als Argument und gibt das codierte Zertifikat zurück. Das binäre Ergebnis kann an **CREATE CERTIFICATE … WITH BINARY** übergeben werden, um ein neues Zertifikat zu erstellen.
  
## <a name="syntax"></a>Syntax  
  
```sql
CERTENCODED ( cert_id )  
```  
  
## <a name="arguments"></a>Argumente  
*CERT_ID*  
Die **certificate_id** des Zertifikats. Diesen Wert finden Sie in „sys.certificates“. Er wird auch von der Funktion [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md) zurückgegeben. *cert-id* weist den Datentyp **int** auf.
  
## <a name="return-types"></a>Rückgabetypen
**varbinary**
  
## <a name="remarks"></a>Remarks  
**CERTENCODED** und **CERTPRIVATEKEY** werden zusammen verwendet, um andere Teile eines Zertifikats in binärer Form zurückzugeben.
  
## <a name="permissions"></a>Berechtigungen  
**CERTENCODED** ist öffentlich verfügbar.
  
## <a name="examples"></a>Beispiele  
  
### <a name="simple-example"></a>Einfaches Beispiel  
In diesem Beispiel wird ein Zertifikat mit dem Namen `Shipping04` erstellt. Dann wird die Funktion **CERTENCODED** verwendet, um die binäre Codierung des Zertifikats zurückzugeben. In diesem Beispiel wird festgelegt, dass das Zertifikat bis zum 31. Oktober 2040 gültig ist.
  
```sql
CREATE DATABASE TEST1;
GO
USE TEST1
CREATE CERTIFICATE Shipping04
ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'
WITH SUBJECT = 'Sammamish Shipping Records',
EXPIRY_DATE = '20401031';
GO
SELECT CERTENCODED(CERT_ID('Shipping04'));
  
```  
  
### <a name="b-copying-a-certificate-to-another-database"></a>B. Kopieren eines Zertifikats in eine andere Datenbank  
Im etwas komplexeren Beispiel werden zwei Datenbanken, `SOURCE_DB` und `TARGET_DB`, erstellt. Erstellen Sie anschließend ein Zertifikat in der `SOURCE_DB`, und kopieren Sie dann das Zertifikat in die `TARGET_DB`. Prüfen Sie zum Schluss, ob die in der `SOURCE_DB` verschlüsselten Daten in der `TARGET_DB` mit der Kopie des Zertifikats entschlüsselt werden können.
  
Erstellen Sie die Datenbanken `SOURCE_DB` und `TARGET_DB` und einen Hauptschlüssel in jeder Datenbank, um die Beispielumgebung zu erzeugen. Erstellen Sie dann in `SOURCE_DB` ein Zertifikat.
  
```sql
USE master;  
GO  
CREATE DATABASE SOURCE_DB;  
GO  
USE SOURCE_DB;  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0URCE_DB KEY Pa$$W0rd';  
GO  
CREATE DATABASE TARGET_DB;  
GO  
USE TARGET_DB  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Pa$$W0rd in TARGET_DB';  
GO  
  
-- Create a certificate in SOURCE_DB  
USE SOURCE_DB;  
GO  
CREATE CERTIFICATE SOURCE_CERT WITH SUBJECT = 'SOURCE_CERTIFICATE';  
GO  
```  
  
Extrahieren Sie anschließend die binäre Beschreibung des Zertifikats.
  
```sql
DECLARE @CERTENC VARBINARY(MAX);  
DECLARE @CERTPVK VARBINARY(MAX);  
SELECT @CERTENC = CERTENCODED(CERT_ID('SOURCE_CERT'));  
SELECT @CERTPVK = CERTPRIVATEKEY(CERT_ID('SOURCE_CERT'),  
       'CertEncryptionPa$$word');  
SELECT @CERTENC AS BinaryCertificate;  
SELECT @CERTPVK AS EncryptedBinaryCertificate;  
GO  
```  
  
Erstellen Sie dann das Zertifikatduplikat in der Datenbank `TARGET_DB`. Ändern Sie den folgenden Code, indem Sie die beiden im vorherigen Schritt zurückgegebenen Binärwerte @CERTENC und @CERTPVK einfügen. Nur dann funktionieren die vorherigen Schritte. Schließen Sie diese Werte nicht in Anführungszeichen ein.
  
```sql
-- Create the duplicate certificate in the TARGET_DB database  
USE TARGET_DB  
GO  
CREATE CERTIFICATE TARGET_CERT  
FROM BINARY = <insert the binary value of the @CERTENC variable>  
WITH PRIVATE KEY (  
BINARY = <insert the binary value of the @CERTPVK variable>  
, DECRYPTION BY PASSWORD = 'CertEncryptionPa$$word');  
-- Compare the certificates in the two databases  
-- The two certificates should be the same   
-- except for name and (possibly) the certificate_id  
SELECT * FROM SOURCE_DB.sys.certificates  
UNION  
SELECT * FROM TARGET_DB.sys.certificates;  
```  
  
Mit dem folgenden Code, der wie ein einzelner Stapel ausgeführt wird, wird veranschaulicht, dass in `SOURCE_DB` verschlüsselte Daten in `TARGET_DB` entschlüsselt werden können.
  
```sql
USE SOURCE_DB;  
  
DECLARE @CLEARTEXT nvarchar(100);  
DECLARE @CIPHERTEXT varbinary(8000);  
DECLARE @UNCIPHEREDTEXT_Source nvarchar(100);  
SET @CLEARTEXT = N'Hello World';  
SET @CIPHERTEXT = ENCRYPTBYCERT(CERT_ID('SOURCE_CERT'), @CLEARTEXT);  
SET @UNCIPHEREDTEXT_Source =   
    DECRYPTBYCERT(CERT_ID('SOURCE_CERT'), @CIPHERTEXT)  
-- Encryption and decryption result in SOURCE_DB  
SELECT @CLEARTEXT AS SourceClearText, @CIPHERTEXT AS SourceCipherText,   
       @UNCIPHEREDTEXT_Source AS SourceDecryptedText;  
  
-- SWITCH DATABASE  
USE TARGET_DB;  
  
DECLARE @UNCIPHEREDTEXT_Target nvarchar(100);  
SET @UNCIPHEREDTEXT_Target = DECRYPTBYCERT(CERT_ID('TARGET_CERT'), @CIPHERTEXT);  
-- Encryption and decryption result in TARGET_DB  
SELECT @CLEARTEXT AS ClearTextInTarget, @CIPHERTEXT AS CipherTextInTarget, @UNCIPHEREDTEXT_Target AS DecriptedTextInTarget;   
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
