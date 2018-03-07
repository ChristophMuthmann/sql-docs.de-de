---
title: CERTPRIVATEKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTPRIVATEKEY
- CERTPRIVATEKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTPRIVATEKEY
ms.assetid: 33e0f01e-39ac-46da-94ff-fe53b1116df4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: df513e6ce63ff49e31ad05e5a4dca0372de69c83
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="certprivatekey-transact-sql"></a>CERTPRIVATEKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt den privaten Schlüssel eines Zertifikats im Binärformat zurück. Diese Funktion akzeptiert drei Argumente.
-   Eine Zertifikat-ID.  
-   Ein Verschlüsselungskennwort, das verwendet wird, um die von der Funktion zurückgegebenen Bits des privaten Schlüssels zu verschlüsseln, damit die Schlüssel nicht als Klartext für Benutzer angezeigt werden.  
-   Ein optionales Entschlüsselungskennwort. Ist ein Entschlüsselungskennwort angegeben, wird es verwendet, um den privaten Schlüssel des Zertifikats zu entschlüsseln. Andernfalls wird der Datenbankhauptschlüssel verwendet.  
  
Nur Benutzer, die Zugriff auf den privaten Schlüssel des Zertifikats haben, können diese Funktion verwenden. Diese Funktion gibt den privaten Schlüssel im PVK-Format zurück.
  
## <a name="syntax"></a>Syntax  
  
```sql
CERTPRIVATEKEY   
    (  
          cert_ID   
        , ' encryption_password '   
      [ , ' decryption_password ' ]  
    )  
```  
  
## <a name="arguments"></a>Argumente  
*Zertifikat-ID*  
Die **certificate_id** des Zertifikats. Diese Option ist verfügbar, über sys.certificates oder mithilfe der [CERT_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/cert-id-transact-sql.md) Funktion. *cert_id* ist vom Typ **int**
  
*encryption_password*  
Das Kennwort, das verwendet wird, um den zurückgegebenen Binärwert zu verschlüsseln.
  
*decryption_password*  
Das Kennwort, das verwendet wird, um den zurückgegebenen Binärwert zu entschlüsseln.
  
## <a name="return-types"></a>Rückgabetypen
**varbinary**
  
## <a name="remarks"></a>Hinweise  
**CERTENCODED** und **CERTPRIVATEKEY** werden zusammen verwendet, um andere Teile eines Zertifikats in binärer Form zurückzugeben.
  
## <a name="permissions"></a>Berechtigungen  
**CERTPRIVATEKEY** ist Öffentlichkeit zur Verfügung.
  
## <a name="examples"></a>Beispiele  
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Use 5tr0ng P^55Words'  
GO  
CREATE CERTIFICATE Shipping04   
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20141031';  
GO  
SELECT CERTPRIVATEKEY(CERT_ID('Shipping04'), 'jklalkaa/; uia3dd');  
```  
  
Ein komplexeres Beispiel, das verwendet **CERTPRIVATEKEY** und **CERTENCODED** zum Kopieren eines Zertifikats in eine andere Datenbank finden Sie unter Beispiel B im Thema [CERTENCODED &#40; Transact-SQL &#41; ](../../t-sql/functions/certencoded-transact-sql.md).
  
## <a name="see-also"></a>Siehe auch
[Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[Erstellen Sie CERTIFICATE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-certificate-transact-sql.md) 
 [Sicherheitsfunktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/security-functions-transact-sql.md) 
 [sys.certificates &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
