---
title: Sys.Certificates (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- certificates
- certificates_TSQL
- sys.certificates_TSQL
- sys.certificates
dev_langs:
- TSQL
helpviewer_keywords:
- sys.certificates catalog view
ms.assetid: e5046102-a65c-401e-b80d-05636884dec9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 60cb7a204aaa38a3aaaa24b8c04bb676715de783
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syscertificates-transact-sql"></a>sys.certificates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jedes Zertifikat in der Datenbank zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Name des Zertifikats. Ist in der Datenbank eindeutig.|  
|**Zertifikat-ID**|**int**|ID des Zertifikats. Ist in der Datenbank eindeutig.|  
|**principal_id**|**int**|ID des Datenbankprinzipals, der der Besitzer dieses Zertifikats ist.|  
|**pvt_key_encryption_type**|**char(2)**|Die Verschlüsselungsart des privaten Schlüssels.<br /><br /> NA = Kein privater Schlüssel für das Zertifikat<br /><br /> MK = Privater Schlüssel wird mit dem Hauptschlüssel verschlüsselt<br /><br /> PW = Privater Schlüssel wird mit einem benutzerdefinierten Kennwort verschlüsselt<br /><br /> SK = Privater Schlüssel wird mit dem Diensthauptschlüssel verschlüsselt|  
|**pvt_key_encryption_type_desc**|**nvarchar(60)**|Die Beschreibung der Verschlüsselungsart des privaten Schlüssels.<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**is_active_for_begin_dialog**|**bit**|Mit dem Wert 1 werden mit diesem Zertifikat verschlüsselte Dienstdialoge initiiert.|  
|**issuer_name**|**nvarchar(442)**|Name des Zertifikatausstellers.|  
|**cert_serial_number**|**nvarchar(64)**|Seriennummer des Zertifikats.|  
|**SID**|**varbinary (85)**|Anmelde-SID für dieses Zertifikat.|  
|**string_sid**|**vom Datentyp nvarchar(128)**|Zeichenfolgendarstellung der Anmelde-SID für dieses Zertifikat.|  
|**Betreff**|**nvarchar(4000)**|Betreff dieses Zertifikats.|  
|**expiry_date**|**datetime**|Das Ablaufdatum des Zertifikats.|  
|**' Startdatum '.**|**datetime**|Das Datum, ab dem das Zertifikat gültig ist.|  
|**Fingerabdruck**|**varbinary(32)**|SHA-1-Hash des Zertifikats. Der SHA-1-Hash ist global eindeutig.|  
|**attested_by**|**nvarchar(260)**|Nur zur Verwendung durch das System.|  
|pvt_key_last_backup_date|**datetime**|Datum und Uhrzeit des letzten Exports des privaten Zertifikatschlüssels.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
  
