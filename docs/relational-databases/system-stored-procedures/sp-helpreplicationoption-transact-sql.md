---
title: Sp_helpreplicationoption (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpreplicationoption
- sp_helpreplicationoption_TSQL
helpviewer_keywords: sp_helpreplicationoption
ms.assetid: ef988dbc-dd0b-4132-80ab-81eebec1cffe
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 378a931a86932be4535906f34432d2a4ea2356e9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpreplicationoption-transact-sql"></a>sp_helpreplicationoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt die Replikationsoptionstypen an, die für einen Server aktiviert sind. Diese gespeicherte Prozedur wird auf jedem Server für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpreplicationoption [ [ @optname =] 'option_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@optname =**] **"***Option_name***"**  
 Der Name der Replikationsoption, die abgefragt werden soll. *Option_name* ist **Sysname**, hat den Standardwert NULL.  
  
|Wert|Description|  
|-----------|-----------------|  
|**transaktionale**|Ein Resultset wird zurückgegeben, wenn die Transaktionsreplikation aktiviert ist.|  
|**Merge**|Ein Resultset wird zurückgegeben, wenn die Mergereplikation aktiviert ist.|  
|NULL (Standard)|Es wird kein Resultset zurückgegeben.|  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|Name der Replikationsoption. Die folgenden Werte sind möglich:<br /><br /> **transaktionale**<br /><br /> **Merge**|  
|**Wert**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Hauptversion**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Nebenversion lauten**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Revision**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**install_failures**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpreplicationoption** dient zum Abrufen von Informationen zu Replikationsoptionen, die auf einem bestimmten Server aktiviert. Verwenden Sie zum Abrufen von Informationen zu einer bestimmten Datenbank **Sp_helpreplicationdboption**.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Ausführungsberechtigungen erhält standardmäßig die **public** -Rolle.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
