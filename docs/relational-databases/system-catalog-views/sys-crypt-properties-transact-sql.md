---
title: Sys. crypt_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- crypt_properties
- crypt_properties_TSQL
- sys.crypt_properties_TSQL
- sys.crypt_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.crypt_properties catalog view
ms.assetid: d5684f5a-30b1-418e-ae4d-ab040db9257e
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d84246fab37c535c0c3665c5aa0c904825ac06b1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syscryptproperties-transact-sql"></a>sys.crypt_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Kryptografieeigenschaft zurück, die einem sicherungsfähigen Element zugeordnet ist.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|Identifiziert die Klasse des Objekts, für das die Eigenschaft vorhanden ist.<br /><br /> 1 = Objekt oder Spalte|  
|**class_desc**|**nvarchar(60)**|Beschreibung der Klasse des Objekts, für das die Eigenschaft vorhanden ist.<br /><br /> OBJECT_OR_COLUMN|  
|**major_id**|**int**|ID des Objekts, für das die Eigenschaft vorhanden ist, interpretiert nach der Klasse.|  
|**Fingerabdruck**|**varbinary(32)**|SHA-1-Hash des verwendeten Zertifikats oder des verwendeten asymmetrischen Schlüssels.|  
|**crypt_type**|**char(4)**|Verschlüsselungstyp.<br /><br /> SPVC = Verschlüsselt mit privatem Zertifikatschlüssel<br /><br /> SPVA = Verschlüsselt mit asymmetrischem privatem Schlüssel<br /><br /> CPVC = Gegensignatur mit privatem Zertifikatschlüssel<br /><br /> CPVA = Gegensignatur mit asymmetrischem Schlüssel|  
|**crypt_type_desc**|**nvarchar(60)**|Beschreibung des Verschlüsselungstyps.<br /><br /> SIGNATURE BY CERTIFICATE<br /><br /> SIGNATURE BY ASYMMETRIC KEY<br /><br /> COUNTER SIGNATURE BY CERTIFICATE<br /><br /> COUNTER SIGNATURE BY ASYMMETRIC KEY|  
|**crypt_property**|**varbinary(max)**|Signierte oder verschlüsselte Bits.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
