---
title: Sys.sp_xtp_unbind_db_resource_pool (Transact-SQL) | Microsoft Docs
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
- sp_xtp_unbind_db_resource_pool_TSQL
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool_TSQL
- sys.sp_xtp_unbind_db_resource_pool
dev_langs: TSQL
helpviewer_keywords:
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool
ms.assetid: 695a796d-087e-4bc8-99d0-ddc342604c75
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6da5bc97801329871d6b433ecf8f049f4b0eb742
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysspxtpunbinddbresourcepool-transact-sql"></a>sys.sp_xtp_unbind_db_resource_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Diese Prozedur entfernt eine vorhandene Bindung zwischen einer Datenbank und einem Ressourcenpool nachzuverfolgen [!INCLUDE[hek_2](../../includes/hek-2-md.md)] speicherauslastung.  Wenn derzeit kein Pool an die angegebene Datenbank gebunden ist, war die Ausführung erfolgreich. Wenn die Datenbankbindung aufgehoben wird, bleibt der zuvor zugeordnete Arbeitsspeicher für speicheroptimierte Objekte dem vorherigen Ressourcenpool zugeordnet. Sie müssen die Datenbank neu starten, um den zugeordneten Arbeitsspeicher freizugeben. Sobald die Bindung einer Datenbank an den Ressourcenpool aufgehoben wird, fällt sie an den DEFAULT-Ressourcenpool zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
sys.sp_xtp_unbind_db_resource_pool 'database_name'  
```  
  
## <a name="arguments"></a>Argumente  
 database_name  
 Der Name eines vorhandenen [!INCLUDE[hek_2](../../includes/hek-2-md.md)] Datenbank aktiviert ist.  
  
#### <a name="parameters"></a>Parameter  
  
## <a name="messages"></a>Meldungen  
 Wenn die Datenbank an einen benannten Ressourcenpool gebunden wurde, wurde die Prozedur erfolgreich ausgeführt. Sie müssen die Datenbank jedoch neu starten, damit die aufgehobene Bindung wirksam wird.  
 Wenn für die angegebene Datenbank keine Bindung besteht, wird `sp_xtp_unbind_db_resource_pool` zwar erfolgreich ausgeführt, gibt aber folgende Informationsmeldung aus:  
  
```  
Msg 41374, Level 16, State 1, Procedure sp_xtp_unbind_db_resource_pool_internal, Line 140.  
Database 'Hekaton_DB' does not have a binding to a resource pool.  
  
```  
  
## <a name="example"></a>Beispiel  
 Im folgenden Code wird die Bindung der Hekaton_DB-Datenbank an den [!INCLUDE[hek_2](../../includes/hek-2-md.md)]-Ressourcenpool aufgehoben.  Wenn Hekaton_DB derzeit nicht an einen [!INCLUDE[hek_2](../../includes/hek-2-md.md)]-Ressourcenpool gebunden ist, wird eine Meldung ausgegeben. Die Datenbank muss neu gestartet werden, damit die aufgehobene Bindung wirksam wird.  
  
```tsql  
sys.sp_xtp_unbind_db_resource_pool 'Hekaton_DB'  
```  
  
## <a name="requirements"></a>Anforderungen  
  
-   Durch den angegebenen Datenbank `database_name` benötigen Sie eine Bindung an eine [!INCLUDE[hek_2](../../includes/hek-2-md.md)] Ressourcenpool.  
  
-   Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [Binden einer Datenbank mit speicheroptimierten Tabellen an einen Ressourcenpool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [Sys.sp_xtp_bind_db_resource_pool &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)  
  
  
