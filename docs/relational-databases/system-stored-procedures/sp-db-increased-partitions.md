---
title: Sp_db_increased_partitions | Microsoft Docs
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
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs: TSQL
helpviewer_keywords: sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5266ce8c25465b6fd398111e7fd7e2d6634f5f34
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spdbincreasedpartitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktiviert oder deaktiviert die Unterstützung für bis zu 15.000 Partitionen für die angegebene Datenbank.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2 bis [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 und höhere Versionen). Weitere Informationen finden Sie unter [Unterstützung für 15.000 Partitionen in SQL Server 2008 SP2 und SQL Server 2008 R2 SP1](http://go.microsoft.com/fwlink/p/?LinkId=299658),|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @dbname=] '*Database_name*"  
 Der Name der Datenbank. *Dbname* ist **Sysname** hat den Standardwert NULL. Wenn *Dbname* nicht angegeben wird, wird die aktuelle Datenbank verwendet.  
  
 [ @increased_partitions=] '*Increased_partitions*"  
 Aktiviert oder deaktiviert die Unterstützung für bis zu 15.000 Partitionen in der angegebenen Datenbank. *Increased_partitions* ist **varchar(6)** hat den Standardwert NULL. Zulässige Werte sind 'ON' bzw. 'TRUE', um die Unterstützung zu aktivieren, und 'OFF' bzw. 'FALSE', um die Unterstützung zu deaktivieren. Wenn *Increased_partitions* nicht angegeben ist, wird die Prozedur zurückgibt, 1, um anzugeben, Unterstützung für die angegebene Datenbank aktiviert ist, oder 0, um Unterstützung anzugeben ist deaktiviert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER DATABASE-Berechtigung für die angegebene Datenbank.  
  
  
