---
title: Sp_validname (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_validname
- sp_validname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validname
ms.assetid: d51c53c2-1332-407f-b725-4983f2e710eb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00dc003905fb90ae819bc49eba68aeee2f1cdbb1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
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
 [  **@name=** ] **"***Namen***"**  
 Der Name des der [Bezeichner](../../relational-databases/databases/database-identifiers.md) für deren Gültigkeit überprüft. *Namen* ist **Sysname**, hat keinen Standardwert. *Namen* darf nicht NULL sein, darf keine leere Zeichenfolge sein und darf keine kein binär-Nullzeichen enthalten.  
  
 [  **@raise_error=** ] *Raise_error*  
 Gibt an, ob ein Fehler ausgelöst wird. *Raise_error* ist **Bit**, hat den Standardwert 1. Dies bedeutet, dass Fehler auftreten. 0 bewirkt, dass keine Fehlermeldungen angezeigt werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [NCHAR &#40; Transact-SQL &#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [Nchar und Nvarchar &#40; Transact-SQL &#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)   
 [Ntext, Text und Bild &#40; Transact-SQL &#41;](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
