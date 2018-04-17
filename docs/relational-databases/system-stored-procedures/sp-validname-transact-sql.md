---
title: Sp_validname (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_validname
- sp_validname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validname
ms.assetid: d51c53c2-1332-407f-b725-4983f2e710eb
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 521c3fc409157de59a3164a145cca96102eb49bb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spvalidname-transact-sql"></a>sp_validname (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Überprüft die Gültigkeit von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichnernamen. Alle nicht binäre und nicht NULL ist Daten, einschließlich Unicode-Daten, die mithilfe von gespeichert werden, können die **Nchar**, **Nvarchar**, oder **Ntext** -Datentypen werden als gültige Zeichen für akzeptiert Bezeichnernamen dürfen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_validname [@name =] 'name'   
     [, [@raise_error =] raise_error]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@name=** ] **'***name***'**  
 Der Name des der [Bezeichner](../../relational-databases/databases/database-identifiers.md) für deren Gültigkeit überprüft. *Namen* ist **Sysname**, hat keinen Standardwert. *Namen* darf nicht NULL sein, darf keine leere Zeichenfolge sein und darf keine kein binär-Nullzeichen enthalten.  
  
 [  **@raise_error=** ] *Raise_error*  
 Gibt an, ob ein Fehler ausgelöst wird. *Raise_error* ist **Bit**, hat den Standardwert 1. Dies bedeutet, dass Fehler auftreten. 0 bewirkt, dass keine Fehlermeldungen angezeigt werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Datenbankmodulprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [Nchar und Nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)   
 [Ntext, Text und Image &#40;Transact-SQL&#41;](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
