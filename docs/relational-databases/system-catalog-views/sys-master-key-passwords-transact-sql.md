---
title: Sys. master_key_passwords (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.master_key_passwords_TSQL
- master_key_passwords_TSQL
- sys.master_key_passwords
- master_key_passwords
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_key_passwords catalog view
ms.assetid: b8e18cff-a9e6-4386-98ce-1cd855506e03
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ea8e225af776493f2a191ea83ce591c51ba624c8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysmasterkeypasswords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jedes Kennwort des Datenbank-Hauptschlüssels zurück, das mit der gespeicherten Prozedur **sp_control_dbmasterkey_password** hinzugefügt wurde. Die Kennwörter, mit denen die Hauptschlüssel geschützt werden, werden im Anmeldeinformationspeicher gespeichert. Der Anmeldeinformationsname weist folgendes Format auf: ##DBMKEY_<database_family_guid>_<random_password_guid>##. Das Kennwort wird als Anmeldeinformation-Kennwort gespeichert. Für jedes Kennwort, das mit **sp_control_dbmasterkey_password**hinzugefügt wird, gibt es eine Zeile in **sys.credentials**.  
  
 Jede Zeile in dieser Sicht enthält eine **credential_id** und den **family_guid** einer Datenbank, deren Hauptschlüssel mit dem Kennwort für diese Anmeldeinformationen geschützt ist. Ein Join mit **sys.credentials** mit der **credential_id** gibt sinnvolle Felder zurück, wie z. B. **create_date** und den Anmeldeinformationsnamen.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**credential_id**|**int**|Die ID der Anmeldeinformationen, zu denen das Kennwort gehört. Diese ID ist innerhalb der Serverinstanz eindeutig.|  
|**family_guid**|**uniqueidentifier**|Eindeutige ID der ursprünglichen Datenbank zum Zeitpunkt der Erstellung. Dieser GUID bleibt unverändert, nachdem die Datenbank wiederhergestellt oder angefügt wurde, selbst wenn der Datenbankname geändert wird.<br /><br /> Wenn die automatische Entschlüsselung durch den Diensthauptschlüssel ein Fehler auftritt, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet die **Family_guid** zum Identifizieren von Anmeldeinformationen, die das Kennwort zum Schützen von Datenbank-Hauptschlüssels enthalten können.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
