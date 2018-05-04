---
title: Sp_addrole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_addrole
- sp_addrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrole
ms.assetid: e8a21642-8440-419a-8585-93d3d9d44f00
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: da6b1a1138863977521750c7770dc42bf918b18c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddrole-transact-sql"></a>sp_addrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine neue Datenbankrolle in der aktuellen Datenbank.  
  
> [!IMPORTANT]  
>  **Sp_addrole** wird aus Gründen der Kompatibilität mit früheren Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und möglicherweise in einer zukünftigen Version nicht mehr unterstützt. Verwendung [CREATE ROLE](../../t-sql/statements/create-role-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addrole [ @rolename = ] 'role' [ , [ @ownername = ] 'owner' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@rolename =** ] **"***Rolle***"**  
 Der Name der neuen Datenbankrolle. *role* ist vom Datentyp **sysname**und hat keinen Standardwert. *Rolle* muss ein gültiger Bezeichner (ID) sein und muss nicht in der aktuellen Datenbank bereits vorhanden.  
  
 [  **@ownername =**] **"***Besitzer***"**  
 Der Besitzer der neuen Datenbankrolle. *Besitzer* ist ein **Sysname**, Standardwert ist der aktuelle Benutzer. *Besitzer* ein Datenbankbenutzer oder eine Datenbankrolle in der aktuellen Datenbank sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Die Namen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankrollen können zwischen 1 und 128 Zeichen (Buchstaben, Sonderzeichen und Ziffern) enthalten. Die Namen von Datenbankrollen können nicht: einen umgekehrten Schrägstrich enthalten (\\), NULL, oder eine leere Zeichenfolge (**''**).  
  
 Nachdem Sie eine Datenbankrolle hinzugefügt haben, verwenden Sie [Sp_addrolemember &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) zu der Rolle Prinzipale hinzuzufügen. Wenn mit den Anweisungen GRANT, DENY oder REVOKE Berechtigungen auf die Datenbankrolle angewendet werden, erben die Mitglieder der Datenbankrolle die Berechtigungen, als würden die Berechtigungen direkt auf die Konten dieser Mitglieder angewendet.  
  
> [!NOTE]  
>  Neue Serverrollen können nicht erstellt werden. Rollen können nur auf der Datenbankebene erstellt werden.  
  
 **Sp_addrole** kann nicht innerhalb einer benutzerdefinierten Transaktion verwendet werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE ROLE-Berechtigung für die Datenbank. Wenn Sie ein Schema erstellen, ist CREATE SCHEMA für die Datenbank erforderlich. Wenn *Besitzer* als ein Benutzer oder eine Gruppe angegeben wird, ist IMPERSONATE für diesen Benutzer oder Gruppe erforderlich. Wenn *Besitzer* als eine Rolle angegeben wird, erfordert die ALTER-Berechtigung für diese Rolle oder ein Mitglied dieser Rolle. Wenn der Besitzer als Anwendungsrolle angegeben wird, ist die ALTER-Berechtigung für diese Anwendungsrolle erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der aktuellen Datenbank die neue Rolle `Managers` hinzugefügt.  
  
```  
EXEC sp_addrole 'Managers';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Security Stored Procedures &#40;Transact-SQL&#41; (Gespeicherte Sicherheitsprozeduren (Transact-SQL))](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)  
  
  
