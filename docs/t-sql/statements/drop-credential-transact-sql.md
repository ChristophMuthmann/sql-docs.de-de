---
title: DROP CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/19/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP CREDENTIAL
- DROP_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing credentials
- DROP CREDENTIAL statement
- credentials [SQL Server], DROP CREDENTIAL statement
- authentication [SQL Server], credentials
- deleting credentials
- dropping credentials
ms.assetid: df22c826-317d-45a6-b078-186acb65f71e
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 99526bd72839ff483d39f0e78634ea27039388ae
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-credential-transact-sql"></a>DROP CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt Anmeldeinformationen für den Server.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>Argumente  
 *credential_name*  
 Der Name der Anmeldeinformationen, die für den Server entfernt werden sollen.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie zum Löschen des geheime Schlüssel einer Anmeldeinformation zugeordnet werden, ohne die Anmeldeinformationen selbst löschen [ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md).  
  
 Informationen zu Anmeldeinformationen werden in der **sys.credentials** -Katalogsicht angezeigt.  
  
> [!WARNING]  
>  Proxys werden Anmeldeinformationen zugeordnet. Werden Anmeldeinformationen gelöscht, die von einem Proxy verwendet werden, kann der zugehörige Proxy nicht mehr verwendet werden. Wenn Sie von einem Proxy verwendete Anmeldeinformationen löschen, löschen Sie den Proxy (mit [Sp_delete_proxy &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md) und erstellen Sie anhand den zugehörigen Proxy neu [Sp_add_proxy &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY CREDENTIAL-Berechtigung. Zum Löschen von Systemanmeldeinformationen ist die CONTROL SERVER-Berechtigung erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Anmeldeinformationen `Saddles` entfernt.  
  
```  
DROP CREDENTIAL Saddles;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anmeldeinformationen &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP DATABASE ausgelegte CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

