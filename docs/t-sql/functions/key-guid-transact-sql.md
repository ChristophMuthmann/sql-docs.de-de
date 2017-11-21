---
title: KEY_GUID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Key_GUID_TSQL
- Key_GUID
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], GUIDs
- KEY_GUID function
- GUIDs [SQL Server]
ms.assetid: 9246c7b2-7098-42c4-a222-cbf30267c46a
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e167366e86cf10403abc6cafa894ad964c60733
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="keyguid-transact-sql"></a>KEY_GUID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die GUID eines symmetrischen Schlüssels in der Datenbank zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Key_GUID( 'Key_Name' )  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Key_Name* **"**  
 Der Name eines symmetrischen Schlüssels in der Datenbank.  
  
## <a name="return-types"></a>Rückgabetypen  
 **uniqueidentifier**  
  
## <a name="remarks"></a>Hinweise  
 Wenn beim Erstellen des Schlüssels ein Identitätswert angegeben wurde, ist dessen GUID ein MD5-Hash dieses Identitätswerts. Wurde kein Identitätswert angegeben, dann wurde die GUID vom Server generiert.  
  
 Falls es sich bei dem Schlüssel um einen temporären Schlüssel handelt, muss der Schlüsselname mit einem Nummernzeichen (#) beginnen.  
  
## <a name="permissions"></a>Berechtigungen  
 Da temporäre Schlüssel nur während der Sitzung verfügbar sind, in der sie erstellt werden, sind für den Zugriff auf die Schlüssel keine Berechtigungen erforderlich. Um auf einen Schlüssel zugreifen zu können, der nicht temporär ist, benötigt der Aufrufer bestimmte Berechtigungen für den Schlüssel. Die VIEW-Berechtigung für den Schlüssel darf ihm nicht entzogen worden sein.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt die GUID eines symmetrischen Schlüssels namens `ABerglundKey1` zurück.  
  
```  
SELECT Key_GUID('ABerglundKey1');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Sys. symmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [Sys. key_encryptions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)  
  
  

