---
title: DROP ASYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP ASYMMETRIC KEY
- DROP_ASYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], removing
- removing asymmetric keys
- encryption [SQL Server], asymmetric keys
- DROP ASYMMETRIC KEY statement
- dropping asymmetric keys
- deleting asymmetric keys
- cryptography [SQL Server], asymmetric keys
ms.assetid: bf94ac07-9b62-4318-b55b-1eed8f3a1ac6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f22fd889c24b0c2422cf7ccf3f21d48be82e4005
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="drop-asymmetric-key-transact-sql"></a>DROP ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Entfernt einen asymmetrischen Schlüssel aus der Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP ASYMMETRIC KEY key_name [ REMOVE PROVIDER KEY ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Key_name*  
 Der Name des asymmetrischen Schlüssels, der aus der Datenbank gelöscht werden soll.  
  
 REMOVE PROVIDER KEY  
 Entfernt einen Schlüssel für erweiterte Schlüsselverwaltung (Extensible Key Management, EKM) von einem EKM-Gerät. Weitere Informationen zur erweiterbaren Schlüsselverwaltung finden Sie unter [erweiterbare Schlüsselverwaltung &#40; Erweiterbare Schlüsselverwaltung &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Hinweise  
 Ein asymmetrischer Schlüssel, mit dem ein symmetrischer Schlüssel in der Datenbank verschlüsselt wurde oder dem ein Benutzer oder Anmeldename zugeordnet wurde, kann nicht gelöscht werden. Bevor Sie einen solchen Schlüssel löschen, müssen Sie jeden Benutzer oder Anmeldenamen löschen, der dem Schlüssel zugeordnet ist. Außerdem müssen Sie jeden symmetrischen Schlüssel löschen oder ändern, der mit dem asymmetrischen Schlüssel verschlüsselt ist. Sie können die Option DROP ENCRYPTION von [ALTER SYMMETRIC KEY](../../t-sql/statements/alter-symmetric-key-transact-sql.md) um die Verschlüsselung mit einem asymmetrischen Schlüssel zu entfernen.  
  
 Metadaten von asymmetrischen Schlüsseln kann zugegriffen werden, indem die [asymmetric_keys](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md) -Katalogsicht angezeigt. Die Schlüssel selbst können nicht direkt in der Datenbank angezeigt werden.  
  
 Wenn der asymmetrische Schlüssel einem Schlüssel für erweiterte Schlüsselverwaltung auf einem EKM-Gerät zugeordnet und die Option REMOVE PROVIDER KEY nicht angegeben ist, wird der Schlüssel aus der Datenbank, nicht aber vom Gerät gelöscht. Eine Warnung wird ausgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für den asymmetrischen Schlüssel.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel entfernt den asymmetrischen Schlüssel `MirandaXAsymKey6` aus der `AdventureWorks2012` -Datenbank.  
  
```  
USE AdventureWorks2012;  
DROP ASYMMETRIC KEY MirandaXAsymKey6;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER SYMMETRIC KEY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)  
  
  
