---
title: Sp_droprole (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_droprole
- sp_droprole_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_droprole
ms.assetid: 889ee074-00f8-40a9-bddb-d7d3ef0cbc19
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2cf1d1d96b04e8508281968acd3f15637dba9a70
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spdroprole-transact-sql"></a>sp_droprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt eine Datenbankrolle aus der aktuellen Datenbank.  
  
> [!IMPORTANT]  
>  In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **Sp_droprole** wurde durch die DROP ROLE-Anweisung ersetzt. **Sp_droprole** ist lediglich aus Gründen der Kompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und möglicherweise in einer zukünftigen Version nicht mehr unterstützt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@rolename =** ] **"***Rolle***"**  
 Der Name der Datenbankrolle, die aus der aktuellen Datenbank entfernt werden soll. *role* ist vom Datentyp **sysname**und hat keinen Standardwert. *role* muss in der aktuellen Datenbank bereits vorhanden sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Mit **sp_droprole**können nur Datenbankrollen entfernt werden.  
  
 Es ist nicht möglich, eine Datenbankrolle mit vorhandenen Mitgliedern zu entfernen. Vor dem Entfernen der Datenbankrolle müssen zunächst alle Mitglieder aus der Datenbankrolle entfernt werden. Entfernen Sie mithilfe von **sp_droprolemember**Benutzer aus einer Rolle. Sollten Benutzer weiterhin Mitglieder der Rolle sein, zeigen Sie diese Mitglieder mit **sp_droprole** an.  
  
 Feste Rollen und die **public** -Rolle können nicht entfernt werden.  
  
 Es ist nicht möglich, eine Rolle zu entfernen, die sicherungsfähige Elemente besitzt. Vor dem Löschen einer Anwendungsrolle, die sicherungsfähige Elemente besitzt, müssen Sie zuerst den Besitz dieser sicherungsfähigen Elemente übertragen oder diese löschen. Verwenden Sie ALTER AUTHORIZATION, um den Besitzer von Objekten zu ändern, die nicht entfernt werden dürfen.  
  
 **sp_droprole** kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für die Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `Sales`-Anwendungsrolle entfernt.  
  
```  
EXEC sp_droprole 'Sales';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [DROP ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Sp_dropapprole &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
