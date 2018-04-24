---
title: VERIFYSIGNEDBYCERT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
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
- VERIFYSIGNEDBYCERT
- VERIFYSIGNEDBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- digitally signed data for changes [SQL Server]
- verifying digitally signed data for changes
- testing digitally signed data for changes
- checking digitally signed data for changes
- VERIFYSIGNEDBYCERT
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 4e041f33-60c4-4190-91c7-220d51dd6c8f
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0e41c82f56f27c37d4bef6d73c641538f1bc6266
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="verifysignedbycert-transact-sql"></a>VERIFYSIGNEDBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Testet, ob digital signierte Daten seit der Signierung geändert wurden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
VerifySignedByCert( Cert_ID , signed_data , signature )  
```  
  
## <a name="arguments"></a>Argumente  
 *Cert_ID*  
 Die ID eines Zertifikats in der Datenbank. *Cert_ID* ist vom Datentyp **int**.  
  
 *signed_data*  
 Eine Variable vom Typ **nvarchar**, **char**, **varchar**oder **nchar** , die mit einem Zertifikat signierte Daten enthält.  
  
 *signature*  
 Die Signatur, die an die signierten Daten angefügt wurde. *signature* ist vom Datentyp **varbinary**.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
 Gibt 1 zurück, wenn die signierten Daten nicht geändert wurden, andernfalls 0.  
  
## <a name="remarks"></a>Remarks  
 **VerifySignedBycert** entschlüsselt die Signatur der Daten mit dem öffentlichen Schlüssel des angegebenen Zertifikats und vergleicht den entschlüsselten Wert mit einem neu berechneten MD5-Hash der Daten. Wenn die Werte zusammenpassen, wird die Signatur als gültig bestätigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DEFINITION-Berechtigung für das Zertifikat.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-verifying-that-signed-data-has-not-been-tampered-with"></a>A. Überprüfen, dass signierte Daten nicht manipuliert wurden  
 Im folgenden Beispiel wird getestet, ob die Informationen in `Signed_Data` seit dem Signieren mithilfe des Zertifikats namens `Shipping04`geändert wurden. Die Signatur wird in `DataSignature`gespeichert. Das Zertifikat, `Shipping04`, wird an die `Cert_ID`-Funktion übergeben, die die ID des Zertifikats in der Datenbank zurückgibt. Gibt `VerifySignedByCert` den Wert 1 zurück, ist die Signatur einwandfrei. Gibt `VerifySignedByCert` den Wert 0 zurück, handelt es sich bei den Daten in `Signed_Data` nicht um die Daten, die zum Generieren von `DataSignature`verwendet wurden. In diesem Fall wurde entweder `Signed_Data` seit dem Signieren geändert, oder `Signed_Data` wurde mithilfe eines anderen Zertifikats signiert.  
  
```  
SELECT Data, VerifySignedByCert( Cert_Id( 'Shipping04' ),  
    Signed_Data, DataSignature ) AS IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
### <a name="b-returning-only-records-that-have-a-valid-signature"></a>B. Zurückgeben von Datensätzen mit einer gültigen Signatur  
 Diese Abfrage gibt nur Datensätze zurück, die nicht geändert wurden, seit sie mithilfe des Zertifikats `Shipping04`signiert wurden.  
  
```  
SELECT Data FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByCert( Cert_Id( 'Shipping04' ), Data,   
    DataSignature ) = 1   
AND Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [SIGNBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/signbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
