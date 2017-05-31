---
title: Always Encrypted-Kryptografie | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 02/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Always Encrypted, cryptography system
ms.assetid: ae8226ff-0853-4716-be7b-673ce77dd370
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ee5419dc374c545daa1249f2e6f76d8d13ac4695
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="always-encrypted-cryptography"></a>Always Encrypted-Kryptografie
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Dieses Dokument beschreibt Verschlüsselungsalgorithmen und -mechanismen zum Ableiten von kryptografischem Material, das in der Funktion [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)]verwendet wird.  
  
## <a name="keys-key-stores-and-key-encryption-algorithms"></a>Schlüssel, Schlüsselspeicher und Algorithmen für die Schlüsselverschlüsselung  
 Always Encrypted verwendet zwei Schlüsseltypen: Spaltenhauptschlüssel und Spaltenverschlüsselungsschlüssel.  
  
 Ein Spaltenhauptschlüssel (column master key; CMK) ist ein Schlüsselverschlüsselungsschlüssel (d.h. ein Schlüssel zum Verschlüsseln anderer Schlüssel), der immer vom Client gesteuert wird und in einem externen Schlüsselspeicher gespeichert ist. Ein Clienttreiber, der für Always Encrypted aktiviert ist, interagiert mit dem Schlüsselspeicher über einen CMK-Speicheranbieter, der entweder Teil der Treiberbibliothek (ein [!INCLUDE[msCoName](../../../includes/msconame-md.md)]-/Systemanbieter) oder Teil der Clientanwendung (ein benutzerdefinierter Anbieter) ist. Clienttreiberbibliotheken umfassen derzeit [!INCLUDE[msCoName](../../../includes/msconame-md.md)]-Schlüsselspeicheranbieter für [Windows-Zertifikatspeicher](https://msdn.microsoft.com/library/windows/desktop/aa388160) und Hardwaresicherheitsmodule (HSMs).  Eine aktuelle Liste der Anbieter finden Sie unter [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md). Ein Anwendungsentwickler kann einen benutzerdefinierten Anbieter für einen beliebigen Speicher angeben.  
  
 Ein Spaltenverschlüsselungsschlüssel (column encryption key; CEK) ist ein Inhaltsverschlüsselungsschlüssel (d.h. ein Schlüssel zum Schützen von Daten), der durch einen CMK geschützt ist.  
  
 Alle [!INCLUDE[msCoName](../../../includes/msconame-md.md)] -CMK-Speicheranbieter verschlüsseln CEKs, indem sie RSA-OAEP (RSA mit optimalem asymmetrischen Verschlüsselungs-Padding) mit den durch RFC 3447 in Abschnitt A.2.1 angegebenen Standardparametern verwenden. Diese Standardparameter verwenden eine Hash-Funktion von SHA-1 und eine Maskengenerierungsfunktion von MGF1 mit SHA-1.  
  
## <a name="data-encryption-algorithm"></a>Datenverschlüsselungsalgorithmus  
 Always Encrypted verwendet den Algorithmus **AEAD_AES_256_CBC_HMAC_SHA_256** zum Verschlüsseln von Daten in der Datenbank.  
  
 **AEAD_AES_256_CBC_HMAC_SHA_256** ist abgeleitet vom Spezifikationsentwurf unter [http://tools.ietf.org/html/draft-mcgrew-aead-aes-cbc-hmac-sha2-05](http://tools.ietf.org/html/draft-mcgrew-aead-aes-cbc-hmac-sha2-05). Er verwendet ein authentifiziertes Verschlüsselungsschema mit zugeordneten Daten nach einem Encrypt-then-MAC-Ansatz. D.h. zunächst wird der Klartext verschlüsselt, und anschließend wird der MAC basierend auf dem resultierenden Chiffretext erstellt.  
  
 Um Muster zu verbergen, verwendet **AEAD_AES_256_CBC_HMAC_SHA_256** den Betriebsmodus der Blockchiffreverkettung (Cipher Block Chaining, CBC), in dem ein Anfangswert in das System eingegeben wird, der als Initialisierungsvektor (IV) bezeichnet wird. Die vollständige Beschreibung des CBC-Modus finden Sie unter [http://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf](http://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf).  
  
 **AEAD_AES_256_CBC_HMAC_SHA_256** berechnet einen Chiffretextwert für einen angegebenen Klartextwert mithilfe der folgenden Schritte.  
  
### <a name="step-1-generating-the-initialization-vector-iv"></a>Schritt 1: Generieren des Initialisierungsvektors (IV)  
 Always Encrypted unterstützt zwei Variationen von **AEAD_AES_256_CBC_HMAC_SHA_256**:  
  
-   Zufällig  
  
-   Deterministisch  
  
 Für die zufällige Verschlüsselung wird der IV zufällig generiert. Daher wird jedes Mal, wenn der gleiche Klartext verschlüsselt wird, ein anderer Chiffretext generiert, was jegliche Offenlegung von Informationen verhindert.  
  
```  
When using randomized encryption: IV = Generate cryptographicaly random 128bits  
```  
  
 Bei der deterministischen Verschlüsselung wird der IV nicht zufällig generiert, sondern mithilfe des folgenden Algorithmus vom Klartext abgeleitet:  
  
```  
When using deterministic encryption: IV = HMAC-SHA-256( iv_key, cell_data ) truncated to 128 bits.  
```  
  
 Wobei iv_key vom CEK folgendermaßen abgeleitet wird:  
  
```  
iv_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell IV key" + algorithm + CEK_length)  
```  
  
 Das Abschneiden des HMAC-Werts wird ausgeführt, um einen Block von Daten wie für den IV benötigt anzupassen.    
Daher erzeugt die deterministische Verschlüsselung immer den gleichen Chiffretext für einen angegebenen Klartextwert. Dadurch kann aus einem Vergleich der entsprechenden Chiffretextwerte abgeleitet werden, ob zwei Klartexte identisch sind. Diese eingeschränkte Offenlegung von Informationen ermöglicht dem Datenbanksystem das Unterstützen der Gleichheitsüberprüfung von verschlüsselten Datenwerten.  
  
 Die deterministische Verschlüsselung ist im Vergleich zu Alternativen, wie der Verwendung von vordefinierten IV-Werten, effektiver im Verdecken von Mustern.  
  
### <a name="step-2-computing-aes256cbc-ciphertext"></a>Schritt 2: Berechnen des Chiffretexts „AES_256_CBC“  
 Nach dem Berechnen des IV-Werts wird der Chiffretext **AES_256_CBC** generiert:  
  
```  
aes_256_cbc_ciphertext = AES-CBC-256(enc_key, IV, cell_data) with PKCS7 padding.  
```  
  
 Wobei der Verschlüsselungsschlüssel (enc_key) vom CEK folgendermaßen abgeleitet wird.  
  
```  
enc_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell encryption key" + algorithm + CEK_length )  
```  
  
### <a name="step-3-computing-mac"></a>Schritt 3: Berechnen des MAC  
 Anschließend wird der MAC mithilfe des folgenden Algorithmus berechnet:  
  
```  
MAC = HMAC-SHA-256(mac_key, versionbyte + IV + Ciphertext + versionbyte_length)  
```  
  
 Erläuterungen:  
  
```  
versionbyte = 0x01 and versionbyte_length = 1   
mac_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell MAC key" + algorithm + CEK_length)  
```  
  
### <a name="step-4-concatenation"></a>Schritt 4: Verkettung  
 Schließlich wird der verschlüsselte Wert erzeugt, indem einfach das Algorithmusversionsbyte, der MAC, der IV und der Chiffretext „AES_256_CBC“ verkettet werden:  
  
```  
aead_aes_256_cbc_hmac_sha_256 = versionbyte + MAC + IV + aes_256_cbc_ciphertext  
```  
  
## <a name="ciphertext-length"></a>Chiffretextlänge  
 Die Längen (in Bytes) bestimmter Komponenten des Chiffretexts **AEAD_AES_256_CBC_HMAC_SHA_256** lauten wie folgt:  
  
-   Versionsbyte: 1  
  
-   MAC: 32  
  
-   IV: 16  
  
-   aes_256_cbc_ciphertext: `(FLOOR (DATALENGTH(cell_data)/ block_size) + 1)* block_size`, wobei:  
  
    -   block_size 16 Byte beträgt  
  
    -   cell_data ein Klartextwert ist  
  
     Daher ist die minimale Größe des aes_256_cbc_ciphertext 1 Block, der 16 Byte groß ist.  
  
 Daher kann die Länge des Chiffretexts, die sich aus der Verschlüsselung bestimmter Klartextwerte (cell_data) ergibt, mithilfe der folgenden Formel berechnet werden:  
  
```  
1 + 32 + 16 + (FLOOR(DATALENGTH(cell_data)/16) + 1) * 16  
```  
  
 Beispiel:  
  
-   Ein 4 Bytes langer **int** -Klartextwert wird nach der Verschlüsselung zu einem 65 Bytes langen Binärwert.  
  
-   Ein 2000 Bytes langer **nchar(1000)** -Klartextwert wird nach der Verschlüsselung zu einem 2065 Bytes langen Binärwert.  
  
 Die folgende Tabelle enthält eine vollständige Liste der Datentypen und Längen der Chiffretexte für jeden Typ.  
  
|Datentyp|Chiffretextlänge [Bytes]|  
|---------------|---------------------------------|  
|**bigint**|65|  
|**binary**|Unterschiedlich. Verwenden Sie die oben stehende Formel.|  
|**bit**|65|  
|**char**|Unterschiedlich. Verwenden Sie die oben stehende Formel.|  
|**Datum**|65|  
|**datetime**|65|  
|**datetime2**|65|  
|**datetimeoffset**|65|  
|**decimal**|81|  
|**float**|65|  
|**geography**|N/V (nicht unterstützt)|  
|**Geometrie**|N/V (nicht unterstützt)|  
|**hierarchyid**|N/V (nicht unterstützt)|  
|**image**|N/V (nicht unterstützt)|  
|**int**|65|  
|**money**|65|  
|**nchar**|Unterschiedlich. Verwenden Sie die oben stehende Formel.|  
|**ntext**|N/V (nicht unterstützt)|  
|**numeric**|81|  
|**nvarchar**|Unterschiedlich. Verwenden Sie die oben stehende Formel.|  
|**real**|65|  
|**smalldatetime**|65|  
|**smallint**|65|  
|**smallmoney**|65|  
|**sql_variant**|N/V (nicht unterstützt)|  
|**sysname**|N/V (nicht unterstützt)|  
|**text**|N/V (nicht unterstützt)|  
|**Uhrzeit**|65|  
|**timestamp**<br /><br /> (**rowversion**)|N/V (nicht unterstützt)|  
|**tinyint**|65|  
|**uniqueidentifier**|81|  
|**varbinary**|Unterschiedlich. Verwenden Sie die oben stehende Formel.|  
|**varchar**|Unterschiedlich. Verwenden Sie die oben stehende Formel.|  
|**xml**|N/V (nicht unterstützt)|  
  
## <a name="net-reference"></a>.NET-Referenz  
 Weitere Informationen zu den in diesem Dokument beschriebenen Algorithmen finden Sie in den Dateien **SqlAeadAes256CbcHmac256Algorithm.cs** und **SqlColumnEncryptionCertificateStoreProvider.cs** in der [.NET-Referenz](http://referencesource.microsoft.com/).  
  
## <a name="see-also"></a>Siehe auch  
 [Always Encrypted &#40;Datenbankmodul&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted &#40;Cliententwicklung&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  

