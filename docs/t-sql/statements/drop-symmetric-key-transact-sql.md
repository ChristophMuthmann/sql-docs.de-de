---
title: DROP SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SYMMETRIC KEY
- DROP_SYMMETRIC_KEY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], removing
- deleting symmetric keys
- encryption [SQL Server], symmetric keys
- removing symmetric keys
- dropping symmetric keys
- cryptography [SQL Server], symmetric keys
- DROP SYMMETRIC KEY statement
ms.assetid: 6150bc67-08cb-402e-9c24-b04c9654b434
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf77b14c281f4e0db0990cda321bbdf92b65f6f8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="drop-symmetric-key-transact-sql"></a>DROP SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Entfernt einen symmetrischen Schlüssel aus der aktuellen Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP SYMMETRIC KEY symmetric_key_name [REMOVE PROVIDER KEY]  
```  
  
## <a name="arguments"></a>Argumente  
 *symmetric_key_name*  
 Der Name des symmetrischen Schlüssels, der gelöscht werden soll.  
  
 REMOVE PROVIDER KEY  
 Entfernt einen Schlüssel für erweiterte Schlüsselverwaltung (Extensible Key Management, EKM) von einem EKM-Gerät. Weitere Informationen zur erweiterbaren Schlüsselverwaltung finden Sie unter [erweiterbare Schlüsselverwaltung &#40; Erweiterbare Schlüsselverwaltung &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Hinweise  
 Die Anweisung erzeugt einen Fehler, wenn der Schlüssel in der aktuellen Sitzung geöffnet ist.  
  
 Wenn der asymmetrische Schlüssel einem Schlüssel für erweiterte Schlüsselverwaltung auf einem EKM-Gerät zugeordnet und die Option **REMOVE PROVIDER KEY** nicht angegeben ist, wird der Schlüssel aus der Datenbank, nicht aber vom Gerät gelöscht, und es wird eine Warnung ausgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für den symmetrischen Schlüssel.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der symmetrische Schlüssel `GailSammamishKey6` aus der aktuellen Datenbank entfernt.  
  
```  
CLOSE SYMMETRIC KEY GailSammamishKey6;  
DROP SYMMETRIC KEY GailSammamishKey6;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CLOSE SYMMETRIC KEY &#40; Transact-SQL &#41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
