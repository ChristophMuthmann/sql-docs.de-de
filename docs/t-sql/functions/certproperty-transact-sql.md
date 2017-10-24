---
title: CERTPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTPROPERTY
- CERTPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], schema names
- schemas [SQL Server], names
- CERTPROPERTY function
ms.assetid: 966c09aa-bc4e-45b0-ba53-c8381871f638
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b43b587688b574c6d6395b72c5b368b82e617fd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="certproperty-transact-sql"></a>CERTPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt den Wert einer angegebenen Zertifikateigenschaft zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CertProperty ( Cert_ID , '<PropertyName>' )  
  
<PropertyName> ::=  
   Expiry_Date | Start_Date | Issuer_Name   
   | Cert_Serial_Number | Subject | SID | String_SID   
```  
  
## <a name="arguments"></a>Argumente  
*Cert_ID*  
Die ID des Zertifikats. *Cert_ID* ist vom Datentyp int.
  
*Expiry_Date*  
Das Ablaufdatum des Zertifikats.
  
*' Startdatum '.*  
Das Datum, an dem das Zertifikat gültig wird.
  
*Issuer_Name*  
Der Name des Zertifikatausstellers.
  
*Cert_Serial_Number*  
Die Seriennummer des Zertifikats.
  
*Betreff*  
Der Zertifikatsantragsteller.
  
 *SID*  
Die SID des Zertifikats. Dies ist auch die SID eines diesem Zertifikat zugeordneten Anmeldenamens oder Benutzers.
  
*String_SID*  
Die SID des Zertifikats als Zeichenfolge. Dies ist auch die SID eines diesem Zertifikat zugeordneten Anmeldenamens oder Benutzers.
  
## <a name="return-types"></a>Rückgabetypen
Die Angabe der Eigenschaft muss in einfache Anführungszeichen eingeschlossen werden.
  
Der Rückgabetyp hängt von der im Funktionsaufruf angegebenen Eigenschaft ab. Alle Rückgabewerte werden in den Rückgabetyp **sql_variant**eingebunden.
-   *Expiry_Date* und *Start_Date* geben **datetime**zurück.  
-   *Cert_Serial_Number*, *Issuer_Name*, *Subject*und *String_SID* geben **nvarchar**zurück.  
-   *SID* gibt **varbinary**zurück.  
  
## <a name="remarks"></a>Hinweise  
Informationen zu Zertifikaten werden in der [sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) -Katalogsicht angezeigt.
  
## <a name="permissions"></a>Berechtigungen  
Erfordert bestimmte Berechtigungen für das Zertifikat, und dem Aufrufer darf die VIEW DEFINITION-Berechtigung für das Zertifikat nicht verweigert worden sein.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird der Zertifikatsantragsteller zurückgegeben.
  
```sql
-- First create a certificate.  
CREATE CERTIFICATE Marketing19 WITH   
    START_DATE = '04/04/2004' ,  
    EXPIRY_DATE = '07/07/2007' ,  
    SUBJECT = 'Marketing Print Division';  
GO  
  
-- Now use CertProperty to examine certificate  
-- Marketing19's properties.  
DECLARE @CertSubject sql_variant;  
set @CertSubject = CertProperty( Cert_ID('Marketing19'), 'Subject');  
PRINT CONVERT(nvarchar, @CertSubject);  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[ALTER CERTIFICATE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)  
[CERT_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/cert-id-transact-sql.md) 
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)
[sys.certificates &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 
 [Sicherheitskatalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  

