---
title: Sys. key_encryptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
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
- sys.key_encryptions
- key_encryptions_TSQL
- sys.key_encryptions_TSQL
- key_encryptions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.key_encryptions catalog view
ms.assetid: c39cecf8-af63-40b9-98e5-f84a5bf3ae54
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a922f80485fafe721124719d3d65566cdad02deb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syskeyencryptions-transact-sql"></a>sys.key_encryptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Verschlüsselung mit einem symmetrischen Schlüssel zurück, die mit der ENCRYPTION BY-Klausel der CREATE SYMMETRIC KEY-Anweisung angegeben ist.  

  
|Spaltennamen|Datentypen|Description|  
|------------------|----------------|-----------------|  
|**key_id**|**int**|ID des verschlüsselten Schlüssels.|  
|**Fingerabdruck**|**varbinary(32)**|SHA-1-Hash des Zertifikats, mit dem der Schlüssel verschlüsselt wird, oder der GUID des symmetrischen Schlüssels, mit dem der Schlüssel verschlüsselt wird.|  
|**crypt_type**|**char(4)**|Verschlüsselungstyp:<br /><br /> ESKS = Verschlüsselt mit symmetrischem Schlüssel<br /><br /> ESKP, ESP2 oder ESP3 = verschlüsselt mit Kennwort<br /><br /> EPUC = Verschlüsselt mit Zertifikat<br /><br /> EPUA = Verschlüsselt mit asymmetrischem Schlüssel<br /><br /> ESKM = Verschlüsselt mit Hauptschlüssel|  
|**crypt_type_desc**|**nvarchar(60)**|Beschreibung des Verschlüsselungstyps:<br /><br /> ENCRYPTION BY SYMMETRIC KEY<br /><br /> ENCRYPTION BY PASSWORD <br />(Beginnend mit [!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)], enthält eine Versionsnummer für die Verwendung von CSS.)<br /><br /> ENCRYPTION BY CERTIFICATE<br /><br /> ENCRYPTION BY ASYMMETRIC KEY<br /><br /> ENCRYPTION BY MASTER KEY<br /><br /> Hinweis: Windows DPAPI wird verwendet, um den Diensthauptschlüssel zu schützen.|  
|**crypt_property**|**varbinary(max)**|Signierte oder verschlüsselte Bits.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
