---
title: Sys. symmetric_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- symmetric_keys
- sys.symmetric_keys
- sys.symmetric_keys_TSQL
- symmetric_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.symmetric_keys catalog view
ms.assetid: d410eae1-3a52-45de-b9a1-52d2bd93a8eb
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7dae3699cb464bf224986f3904d1df9b6d416bd4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="syssymmetrickeys-transact-sql"></a>sys.symmetric_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jeden symmetrischen Schlüssel zurück, der mit der CREATE SYMMETRIC KEY-Anweisung erstellt wird.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Name des Schlüssels. Dieser ist in der c4database eindeutig.|  
|**principal_id**|**int**|ID des Datenbankprinzipals, der der Besitzer des Schlüssels ist.|  
|**symmetric_key_id**|**int**|ID des Schlüssels. Ist innerhalb der Datenbank eindeutig.|  
|**key_length**|**int**|Länge des Schlüssels in Bits.|  
|**key_algorithm**|**char(2)**|Der mit dem Schlüssel verwendete Algorithmus:<br /><br /> R2 = RC2<br /><br /> R4 = RC4<br /><br /> D = DES<br /><br /> D3 = Triple DES<br /><br /> DT = TRIPLE_DES_3KEY<br /><br /> DX = DESX<br /><br /> A1 = AES 128<br /><br /> A2 = AES 192<br /><br /> A3 = AES 256<br /><br /> N.V. = EKM-Schlüssel|  
|**algorithm_desc**|**nvarchar(60)**|Beschreibung des mit dem Schlüssel verwendeten Algorithmus:<br /><br /> RC2<br /><br /> RC4<br /><br /> DES<br /><br /> Triple_DES<br /><br /> TRIPLE_DES_3KEY<br /><br /> DESX<br /><br /> AES_128<br /><br /> AES_192<br /><br /> AES_256<br /><br /> NULL (nur Extensible Key Management-Algorithmen)|  
|**create_date**|**datetime**|Das Datum, an dem der Schlüssel erstellt wurde.|  
|**modify_date**|**datetime**|Das Datum, an dem der Schlüssel geändert wurde.|  
|**key_guid**|**uniqueidentifier**|Global eindeutiger Bezeichner (GUID, Globally Unique Identifier) für den Schlüssel. Dieser Bezeichner wird für persistente Schlüssel automatisch generiert. GUIDs für temporäre Schlüssel werden von dem vom Benutzer angegebenen Passphrase abgeleitet.|  
|**key_thumbprint**|**sql_variant**|SHA-1-Hash des Schlüssels. Der Hash ist global eindeutig. Bei Schlüsseln, die nicht der erweiterbaren Schlüsselverwaltung entsprechen, ist dieser Wert NULL.|  
|**provider_type**|**nvarchar(120)**|Der Typ des Kryptografieanbieters:<br /><br /> CRYPTOGRAPHIC PROVIDER = Extensible Key Management-Schlüssel<br /><br /> NULL = Nicht-Extensible Key Management-Schlüssel|  
|**cryptographic_provider_guid**|**uniqueidentifier**|Der GUID für den Kryptografieanbieter. Bei Schlüsseln, die nicht der erweiterbaren Schlüsselverwaltung entsprechen, ist dieser Wert NULL.|  
|**cryptographic_provider_algid**|**sql_variant**|Die Algorithmus-ID für den Kryptografieanbieter. Bei Schlüsseln, die nicht der erweiterbaren Schlüsselverwaltung entsprechen, ist dieser Wert NULL.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Hinweise  
 Der RC4-Algorithmus ist veraltet. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
> [!NOTE]  
>  Der RC4-Algorithmus wird nur aus Gründen der Abwärtskompatibilität unterstützt. Neues Material kann nur mit RC4 oder RC4_128 verschlüsselt werden, wenn die Datenbank den Kompatibilitätsgrad 90 oder 100 besitzt. (Nicht empfohlen.) Verwenden Sie stattdessen einen neueren Algorithmus, z. B. einen der AES-Algorithmen. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] kann mit RC4 oder RC4_128 verschlüsseltes Material in jedem Kompatibilitätsgrad entschlüsselt werden.  
  
 **Erläuterung der DES-Algorithmen:**  
  
-   DESX wurde falsch benannt. Symmetrische Schlüssel, die mit ALGORITHM = DESX erstellt sind, verwenden eigentlich die TRIPLE DES-Chiffre mit einem 192-Bit-Schlüssel. Der DESX-Algorithmus wird nicht bereitgestellt. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
-   Symmetrische Schlüssel, die mit ALGORITHM = TRIPLE_DES_3KEY erstellt sind, verwenden die TRIPLE DES-Chiffre mit einem 192-Bit-Schlüssel.  
  
-   Symmetrische Schlüssel, die mit ALGORITHM = TRIPLE_DES erstellt sind, verwenden die TRIPLE DES-Chiffre mit einem 128-Bit-Schlüssel.  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
