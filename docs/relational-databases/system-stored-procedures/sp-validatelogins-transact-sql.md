---
title: Sp_validatelogins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_validatelogins
- sp_validatelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validatelogins
ms.assetid: 6ac52e21-e20d-469b-ad40-5aa091e06b61
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b9f47794888ad9b268971543bbbf0cdee05defbc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spvalidatelogins-transact-sql"></a>sp_validatelogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stellt Informationen zu Windows-Benutzer und Gruppen, die zugeordnet werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Prinzipale, die jedoch nicht mehr in der Windows-Umgebung vorhanden sind.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_validatelogins  
```  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**SID**|**varbinary(85)**|Windows-Sicherheits-ID (SID) des Windows-Benutzers oder der Windows-Gruppe.|  
|**NT-Anmeldung**|**sysname**|Der Name des Windows-Benutzers oder der Windows-Gruppe.|  
  
## <a name="remarks"></a>Hinweise  
 Falls der verwaiste Prinzipal auf Serverebene einen Datenbankbenutzer besitzt, muss der Datenbankbenutzer entfernt werden, bevor der verwaiste Serverprinzipal entfernt werden kann. Verwenden Sie zum Entfernen eines Datenbankbenutzers [DROP USER](../../t-sql/statements/drop-user-transact-sql.md). Falls der Prinzipal auf Serverebene sicherungsfähige Elemente in der Datenbank besitzt, muss der Besitz der sicherungsfähigen Elemente übertragen werden, oder die sicherungsfähigen Elemente müssen gelöscht werden. Um den Besitz von sicherungsfähigen Datenbankelementen zu übertragen, verwenden Sie [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 Verwenden Sie zum Entfernen der Zuordnungen von Windows-Benutzer und Gruppen, die nicht mehr vorhanden [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder **securityadmin** .  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Windows-Benutzer und Gruppen, die nicht mehr vorhanden, jedoch sind weiterhin Zugriff auf eine Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_validatelogins;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Security Stored Procedures &#40;Transact-SQL&#41; (Gespeicherte Sicherheitsprozeduren (Transact-SQL))](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP USER & #40; Transact-SQL & #41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [DROP LOGIN & #40; Transact-SQL & #41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
