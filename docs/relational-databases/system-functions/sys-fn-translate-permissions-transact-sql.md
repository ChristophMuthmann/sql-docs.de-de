---
title: Sys. fn_translate_permissions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_translate_permissions
- sys.fn_translate_permissions_TSQL
- fn_translate_permissions
- fn_translate_permissions_TSQL
dev_langs: TSQL
helpviewer_keywords:
- permissions bitmask [SQL Server]
- sys.fn_translate_permissions function
- fn_translate_permissions function
ms.assetid: ac97121f-2bd0-4f71-8e45-42c8584edbc5
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3a9b089f2926ab701d286141101b0c17e2c027e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysfntranslatepermissions-transact-sql"></a>sys.fn_translate_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Übersetzt die von der SQL-Ablaufverfolgung zurückgegebene Bitmaske von Berechtigungen in eine Tabelle von Berechtigungsnamen.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_translate_permissions ( level , perms )  
```  
  
## <a name="arguments"></a>Argumente  
 *Ebene*  
 Die Art eines sicherungsfähigen Elements, für die die Berechtigung übernommen wird. *Ebene* ist **nvarchar(60)**.  
  
 *Perms*  
 Eine Bitmaske, die in der Berechtigungsspalte zurückgegeben wird. *Perms* ist **varbinary(16)**.  
  
## <a name="returns"></a>Rückgabewert  
 **table**  
  
## <a name="remarks"></a>Hinweise  
 Der zurückgegebene Wert in der **Berechtigungen** Spalte von einer SQL-Ablaufverfolgung ist eine Integer-Darstellung einer Bitmaske, die durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] effektive Berechtigungen berechnet. Jede der 25 Arten sicherungsfähiger Elemente verfügt über einen eigenen Satz Berechtigungen mit entsprechenden numerischen Werten. **Sys. fn_translate_permissions** übersetzt diese Bitmaske in eine Tabelle von Berechtigungsnamen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="example"></a>Beispiel  
 Die folgende Abfrage verwendet `sys.fn_builtin_permissions` um die Berechtigungen anzuzeigen, die gelten für Zertifikate und verwendet dann `sys.fn_translate_permissions` zum Zurückgeben der Ergebnisse der Bitmaske von Berechtigungen.  
  
```  
SELECT * FROM sys.fn_builtin_permissions('CERTIFICATE');  
SELECT '0001' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0001);  
SELECT '0010' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0010);  
SELECT '0011' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0011);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  
