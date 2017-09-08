---
title: DROP-Signatur (Transact-SQL) | Microsoft Docs
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
- DROP SIGNATURE
- DROP_SIGNATURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting signatures
- dropping signatures
- DROP SIGNATURE statement
- removing signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 8a1fd8c5-0e75-4b2f-9d3c-c296bed56cc7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 81823a549f608bdcddb631084904fb303a1ddc9f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-signature-transact-sql"></a>DROP SIGNATURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Löscht eine digitale Signatur aus einer gespeicherten Prozedur, Funktion, Assembly oder einem Trigger.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP [ COUNTER ] SIGNATURE FROM module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | ASYMMETRIC KEY Asym_key_name  
```  
  
## <a name="arguments"></a>Argumente  
 *Modulname*  
 Der Name einer gespeicherten Prozedur, einer Funktion, einer Assembly oder eines Triggers.  
  
 Zertifikat *Cert_name*  
 Der Name eines Zertifikats, mit dem die gespeicherte Prozedur, die Funktion, die Assembly oder der Trigger signiert wird.  
  
 ASYMMETRISCHE Schlüssel *Asym_key_name*  
 Der Name eines asymmetrischen Schlüssels, mit dem die gespeicherte Prozedur, die Funktion, die Assembly oder der Trigger signiert wird.  
  
## <a name="remarks"></a>Hinweise  
 Informationen zu Signaturen werden in der sys.crypt_properties-Katalogsicht angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für das Objekt und die CONTROL-Berechtigung für das Zertifikat oder den asymmetrischen Schlüssel. Falls ein zugeordneter privater Schlüssel mit einem Kennwort geschützt ist, muss der Benutzer zudem das Kennwort kennen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Signatur des Zertifikats `HumanResourcesDP` aus der gespeicherten Prozedur `HumanResources.uspUpdateEmployeeLogin` entfernt.  
  
```  
USE AdventureWorks2012;  
DROP SIGNATURE FROM HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. crypt_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [Signatur hinzufügen &#40; Transact-SQL &#41;](../../t-sql/statements/add-signature-transact-sql.md)  
  
  
