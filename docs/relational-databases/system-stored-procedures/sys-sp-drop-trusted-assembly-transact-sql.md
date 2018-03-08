---
title: Sys.sp_drop_trusted_assembly (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/14/2017
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
- sp_drop_trusted_assembly_TSQL
- sp_drop_trusted_assembly
- sys.sp_drop_trusted_assembly_TSQL
- sys.sp_drop_trusted_assembly
dev_langs: TSQL
helpviewer_keywords: sys.sp_drop_trusted_assembly
ms.assetid: 
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c04f2992d0f715d95eda631de97dd6e8eb3dac72
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysspdroptrustedassembly-transact-sql"></a>Sys.sp_drop_trusted_assembly (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Löscht eine Assembly aus der Liste der vertrauenswürdigen Assemblys auf dem Server.

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>Syntax
```  
sp_drop_trusted_assembly 
    [ @hash = ] 'value'
```  

## <a name="arguments"></a>Argumente

[ @hash =] '*Wert*"  
Der Hashwert des SHA2_512 der Assembly, die aus der Liste der vertrauenswürdigen Assemblys für den Server zu löschen. Vertrauenswürdige Assemblys möglicherweise geladen, wenn Clr strikte Sicherheit aktiviert ist, auch wenn die Assembly nicht signiert ist oder die Datenbank ist nicht als vertrauenswürdig gekennzeichnet.

## <a name="remarks"></a>Hinweise  

Diese Prozedur entfernt eine Assembly aus [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md).

## <a name="permissions"></a>Berechtigungen

Erfordert die Mitgliedschaft in der `sysadmin` feste Serverrolle oder `CONTROL SERVER` Berechtigung.

## <a name="examples"></a>Beispiele  

Das folgende Beispiel löscht einen Assemblyhash aus der Liste der vertrauenswürdigen Assemblys für den Server an.  

```  
EXEC sp_drop_trusted_assembly 
0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC; 
```  

## <a name="see-also"></a>Siehe auch  
  [Sys.sp_add_trusted_assembly](sys-sp-add-trusted-assembly-transact-sql.md) [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) [DROP ASSEMBLY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

