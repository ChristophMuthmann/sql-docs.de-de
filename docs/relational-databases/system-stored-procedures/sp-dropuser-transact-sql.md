---
title: Sp_dropuser (Transact-SQL) | Microsoft Docs
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
- sp_dropuser
- sp_dropuser_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_dropuser
ms.assetid: e28f18f9-7ecf-4568-89f4-fe5c520df386
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 242950773bb0eabbd8b4170a05fd228311604bdf
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spdropuser-transact-sql"></a>sp_dropuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt einen Datenbankbenutzer aus der aktuellen Datenbank. **Sp_dropuser** gewährleistet die Kompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [DROP USER](../../t-sql/statements/drop-user-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@name_in_db =**] **"***Benutzer***"**  
 Der Name des Benutzers, der entfernt werden soll. *Benutzer* ist ein **Sysname**, hat keinen Standardwert. *Benutzer* muss in der aktuellen Datenbank vorhanden sein. Wenn Sie einen Windows-Anmeldenamen angeben, verwenden Sie den Namen, mit dem der Anmeldename von der Datenbank identifiziert wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dropuser** führt **Sp_revokedbaccess** beim Entfernen des Benutzers aus der aktuellen Datenbank.  
  
 Verwendung **Sp_helpuser** um eine Liste der Benutzernamen anzuzeigen, die aus der aktuellen Datenbank entfernt werden können.  
  
 Wenn ein Datenbankbenutzer entfernt wird, werden auch alle Aliase für diesen Benutzer entfernt. Wenn der Benutzer ein leeres Schema mit dem gleichen Namen wie der Benutzer besitzt, wird das Schema gelöscht. Wenn der Benutzer andere sicherungsfähige Elemente in der Datenbank besitzt, wird der Benutzer nicht gelöscht. Der Besitz der Objekte muss zuerst auf einen anderen Prinzipal übertragen werden. Weitere Informationen finden Sie unter [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md). Beim Entfernen eines Datenbankbenutzers werden automatisch die Berechtigungen dieses Benutzers entfernt, und der Benutzer wird aus allen Datenbankrollen entfernt, in denen er Mitglied ist.  
  
 **Sp_dropuser** kann nicht verwendet werden, um das Entfernen des Datenbankbesitzers (**Dbo**) **INFORMATION_SCHEMA** Benutzer oder die **Gast** Benutzer aus der  **Master** oder **Tempdb** Datenbanken. In anderen als Systemdatenbanken hebt `EXEC sp_dropuser 'guest'` CONNECT-Berechtigung von Benutzer **Gast**. Der Benutzer selbst wird jedoch nicht gelöscht.  
  
 **Sp_dropuser** kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY USER-Berechtigung in der Datenbank.  
  
## <a name="examples"></a>Beispiele  
 Im folgende Beispiel entfernt den Benutzer `Albert` aus der aktuellen Datenbank.  
  
```  
EXEC sp_dropuser 'Albert';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [DROP USER &#40; Transact-SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
