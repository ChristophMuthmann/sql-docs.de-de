---
title: DROP-Regel (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_RULE_TSQL
- DROP RULE
dev_langs:
- TSQL
helpviewer_keywords:
- rules [SQL Server], removing
- deleting roles
- DROP RULE statement
- removing roles
- dropping roles
ms.assetid: 8370b730-7fd5-43fe-a7f6-8300b3caa16d
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ba898b1c9f94f4e38102da929709b4a05f889b7e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-rule-transact-sql"></a>DROP RULE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt eine oder mehrere benutzerdefinierte Regeln aus der aktuellen Datenbank.  
  
> [!IMPORTANT]  
>  DROP RULE werden in der nächsten Version von entfernt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verwenden Sie DROP RULE nicht bei neuen Entwicklungsarbeiten, und planen Sie die Änderung von Anwendungen, die DROP RULE derzeit verwenden. Verwenden Sie stattdessen CHECK-Einschränkungen, die Sie erstellen können, mit dem CHECK-Schlüsselwort von [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) oder [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md). Weitere Informationen finden Sie unter [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DROP RULE [ IF EXISTS ] { [ schema_name . ] rule_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *IF VORHANDEN IST*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Bedingt löscht die Regel nur, wenn sie bereits vorhanden ist.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Regel gehört.  
  
 *Regel*  
 Die zu entfernende Regel. Regelnamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md). Das Angeben des Regelschemanamens ist optional.  
  
## <a name="remarks"></a>Hinweise  
 Um eine Regel zu löschen, müssen Sie zuerst eine möglicherweise vorhandene Bindung an eine Spalte oder einen Aliasdatentyp aufheben. Verwenden Sie zum Aufheben der Bindung der Regelnamens, **Sp_unbindrule**. Wenn beim Löschen einer Regel noch eine Bindung besteht, wird eine Fehlermeldung angezeigt, und die DROP RULE-Anweisung wird abgebrochen.  
  
 Nach dem Löschen einer Regel werden auf neue Daten, die Sie in die betreffenden Spalten eingeben, die früheren Einschränkungen der gelöschten Regel nicht mehr angewendet. Dies wirkt sich nicht auf bereits vorhandene Daten aus.  
  
 Die DROP RULE-Anweisung gilt nicht für CHECK-Einschränkungen. Weitere Informationen zum Löschen von CHECK-Einschränkungen finden Sie unter [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen von DROP RULE benötigt der Benutzer mindestens die ALTER-Berechtigung für das Schema, zu dem die Regel gehört.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Bindung der `VendorID_rule`-Regel aufgehoben und diese Regel dann gelöscht. 
  
```  
sp_unbindrule 'Production.ProductVendor.VendorID'  
DROP RULE VendorID_rule  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [Sp_bindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [Sp_unbindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  


