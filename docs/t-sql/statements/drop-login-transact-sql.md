---
title: DROP LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP LOGIN
- DROP_LOGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting login accounts
- logins [SQL Server], removing
- DROP LOGIN statement
- removing login accounts
- dropping login accounts
ms.assetid: acb5c3dc-7aa2-49f6-9330-573227ba9b1a
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c8c13d7800893b860b1bcaf3f631f01f190a2715
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-login-transact-sql"></a>DROP LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldekonto.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DROP LOGIN login_name  
```  
  
## <a name="arguments"></a>Argumente  
 *login_name*  
 Gibt den Namen des zu löschenden Anmeldenamens an.  
  
## <a name="remarks"></a>Hinweise  
 Eine Anmeldung kann nicht gelöscht werden, während sie angemeldet ist. Eine Anmeldung, die der Besitzer eines sicherungsfähigen Elements, eines Objekts auf Serverebene oder eines SQL Server-Agentauftrags ist, kann nicht gelöscht werden.  
  
 Ein Anmeldename, dem Datenbankbenutzer zugeordnet sind, kann gelöscht werden. Dabei werden jedoch verwaiste Benutzer erstellt. Weitere Informationen finden Sie unter [Problembehandlung bei verwaisten Benutzern &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)aus.  
  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)], Anmeldedaten erforderlich, um eine Verbindung zu authentifizieren und Firewallregeln auf Serverebene werden in jeder Datenbank vorübergehend zwischengespeichert. Dieser Cache wird in regelmäßigen Abständen aktualisiert. Führen Sie zum Erzwingen einer Aktualisierung des Authentifizierungscache und stellen Sie sicher, dass eine Datenbank die aktuelle Version der Tabelle Anmeldungen verfügt, [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY LOGIN-Berechtigung auf dem Server.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-dropping-a-login"></a>A. Löschen eine Anmeldung  
 Im folgenden Beispiel wird der Anmeldename `WilliJo` gelöscht.  
  
```  
DROP LOGIN WilliJo;  
GO 
```  
 
  
## <a name="see-also"></a>Siehe auch  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  


