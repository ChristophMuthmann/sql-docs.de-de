---
title: dm_cryptographic_provider_keys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys
- sys.dm_cryptographic_provider_keys
dev_langs: TSQL
helpviewer_keywords: sys.dm_cryptographic_provider_keys dynamic management function
ms.assetid: 5a8c1421-c56b-44b5-96e5-4f01782a0c7c
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b16cf946a2e963ac0421fe91ac11df6e9021ed1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmcryptographicproviderkeys-transact-sql"></a>sys.dm_cryptographic_provider_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen die von einem Anbieter für erweiterte Schlüsselverwaltung (Extensible Key Management, EKM) bereitgestellten Schlüssel zurück.  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
dm_cryptographic_provider_keys ( provider_id )  
```  
  
## <a name="arguments"></a>Argumente  
 *provider_id*  
 Die ID des EKM-Anbieters, ohne Standardwert.  
  
## <a name="tables-returned"></a>Zurückgegebene Tabellen  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**key_ID**|**int**|ID des Schlüssels beim Anbieter.|  
|**Key_name**|**nvarchar(512)**|Name des Schlüssels beim Anbieter.|  
|**key_thumbprint**|**varbinary(32)**|Fingerabdruck des Anbieters des Schlüssels.|  
|**algorithm_id**|**int**|ID des Algorithmus beim Anbieter.|  
|**algorithm_tag**|**int**|Tag des Algorithmus beim Provider.|  
|**KEY_TYPE**|**NCHAR(256)**|Typ des Schlüssels beim Anbieter.|  
|**Schlüssellänge**|**int**|Länge des Schlüssels beim Anbieter.|  
  
## <a name="permissions"></a>Berechtigungen  
 Bei Abfrage dieser Ansicht wird der Benutzerkontext mit dem Anbieter authentifiziert, und es werden alle für den Benutzer sichtbaren Schlüssel aufgezählt.  
  
 Wenn der Benutzer nicht mit dem EKM-Anbieter authentifiziert werden kann, werden keine Schlüsselinformationen zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Schlüsseleigenschaften für einen Anbieter mit der ID `1234567`veranschaulicht.  
  
```  
SELECT * FROM sys.dm_cryptographic_provider_keys(1234567);  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
