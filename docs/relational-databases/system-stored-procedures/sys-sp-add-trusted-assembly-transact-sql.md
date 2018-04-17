---
title: Sys.sp_add_trusted_assembly (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_trusted_assembly_TSQL
- sp_add_trusted_assembly
- sys.sp_add_trusted_assembly_TSQL
- sys.sp_add_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_add_trusted_assembly
ms.assetid: ''
caps.latest.revision: ''
author: tmullaney
ms.author: thmullan
manager: craigg
ms.workload: Inactive
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d71afb0e41469e3b73f65bcb9232733861645476
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysspaddtrustedassembly-transact-sql"></a>Sys.sp_add_trusted_assembly (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Fügt eine Assembly zur Liste der vertrauenswürdigen Assemblys für den Server an.

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>Syntax
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>Hinweise  

Diese Prozedur fügt eine Assembly [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md).

## <a name="arguments"></a>Argumente

[ @hash =] '*Wert*"  
Der Hashwert des SHA2_512 der Assembly in der Liste der vertrauenswürdigen Assemblys für den Server hinzuzufügen. Vertrauenswürdige Assemblys können beim Laden [strikte Sicherheit der CLR](../../database-engine/configure-windows/clr-strict-security.md) aktiviert ist, auch wenn die Assembly nicht signiert ist oder die Datenbank ist nicht als vertrauenswürdig gekennzeichnet.

[ @description =] '*Beschreibung*"  
Optionale benutzerdefinierte Beschreibung der Assembly. Microsoft empfiehlt die Verwendung des kanonischen Namens, der den einfachen Namen, Versionsnummer, Kultur, öffentlicher Schlüssel und Architektur der Assembly, vertrauen codiert. Dieser Wert eindeutig kennzeichnet die Assembly, auf der Seite der common Language Runtime (CLR) und entspricht der Wert Clr_name in sys.assemblies. 

## <a name="permissions"></a>Berechtigungen

Erfordert die Mitgliedschaft in der `sysadmin` feste Serverrolle oder `CONTROL SERVER` Berechtigung.

## <a name="examples"></a>Beispiele  

Im folgenden Beispiel wird eine Assembly mit dem Namen `pointudt` zur Liste der vertrauenswürdigen Assemblys für den Server. Diese Werte stehen über [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md).     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>Siehe auch  
  [sys.sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [Strikte Sicherheit der CLR](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

