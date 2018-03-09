---
title: Sys. user_token (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.user_token
- user_token
- sys.user_token_TSQL
- user_token_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], security tokens
- sys.user_token catalog view
- user tokens [SQL Server]
- tokens [SQL Server]
- user_token catalog view
ms.assetid: be018103-5e57-43a4-9160-9bf420892aa7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6c552b797a78fe27b0a6b4253ad44aee37b8f67
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysusertoken-transact-sql"></a>sys.user_token (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jeden Datenbankprinzipal zurück, der Teil des Benutzertokens in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|ID des Prinzipals. Der Wert ist innerhalb der Datenbank eindeutig.|  
|**SID**|**varbinary (85)**|Sicherheitsbezeichner des Prinzipals, wenn der Prinzipal datenbankextern definiert ist. Dieser Wert kann z. B. ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename, ein Windows-Anmeldename, ein Anmeldename einer Windows-Gruppe oder ein einem Zertifikat zugeordneter Anmeldename sein. Andernfalls ist dieser Wert NULL.|  
|**name**|**Nvarchar (128)**|Name des Prinzipals. Der Wert ist innerhalb der Datenbank eindeutig.|  
|**Typ**|**Nvarchar (128)**|Beschreibung des Prinzipaltyps. Alle Typen zugeordnet werden **Sid**. Die folgenden Werte sind möglich:<br /><br /> SQL USER<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> ROLE<br /><br /> APPLICATION ROLE<br /><br /> DATABASE ROLE<br /><br /> USER MAPPED TO CERTIFICATE<br /><br /> USER MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**Verwendung**|**Nvarchar (128)**|Zeigt an, dass der Prinzipal an der Auswertung von GRANT- oder DENY-Berechtigungen teilnimmt oder als Authentifikator dient.<br /><br /> Die folgenden Werte sind möglich:<br /><br /> GRANT OR DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. login_token &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
