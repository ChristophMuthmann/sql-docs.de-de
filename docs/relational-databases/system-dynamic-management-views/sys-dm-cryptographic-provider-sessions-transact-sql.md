---
title: dm_cryptographic_provider_sessions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_cryptographic_provider_sessions
- dm_cryptographic_provider_sessions_TSQL
- sys.dm_cryptographic_provider_sessions_TSQL
- dm_cryptographic_provider_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_sessions dynamic management function
ms.assetid: 9a4de02b-1a07-4850-979a-0861fddb7f9d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b60590005ab185f4f03256a0e3845d9a4a61bee
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmcryptographicprovidersessions-transact-sql"></a>sys.dm_cryptographic_provider_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen über geöffnete Sitzungen für einen Kryptografieanbieter zurück.  
 
## <a name="syntax"></a>Syntax  
  
```  
  
sys.dm_cryptographic_provider_sessions(session_identifier)  
```  
  
## <a name="arguments"></a>Argumente  
 *session_identifier*  
 Eine Ganzzahl, die die zurückzugebende Sitzung angibt.  
  
 0 = Nur aktuelle Verbindung  
  
 1 = Alle kryptografischen Verbindungen  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|ID des Kryptografieanbieters.|  
|**session_handle**|**varbytes(8)**|Kryptografisches Sitzungshandle.|  
|**identity**|**nvarchar(128)**|ID, die zur Authentifizierung mit dem Kryptgrafieanbieter verwendet wird.|  
|**spid**|**short**|SPID der Sitzungs-ID für die Verbindung. Weitere Informationen finden Sie unter [@@SPID &#40; Transact-SQL &#41; ](../../t-sql/functions/spid-transact-sql.md).|  
  
## <a name="remarks"></a>Hinweise  
 Die **dm_cryptographic_provider_sessions** Ansicht ist für die aktuelle Verbindung öffentlich sichtbar. Um alle kryptografischen Verbindungen anzuzeigen, benötigen Sie die **Steuerelement** Serverberechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
