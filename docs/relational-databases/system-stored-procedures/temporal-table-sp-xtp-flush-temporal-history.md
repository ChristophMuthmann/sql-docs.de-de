---
title: Sp_xtp_flush_temporal_history | Microsoft Docs
ms.custom: 
ms.date: 02/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016 CTP3)
f1_keywords:
- sp_xtp_flush_temporal_history
- sp_xtp_flush_temporal_history_TSQL
- sys.sp_xtp_flush_temporal_history
- sys.sp_xtp_flush_temporal_history_TSQL
helpviewer_keywords:
- sp_xtp_flush_temporal_history
ms.assetid: 322e3170-93f8-468a-a123-104ce7bd7fad
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f68bb1a07ba3edb33c99339b53b0f85e343576ad
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="temporal-table---spxtpflushtemporalhistory"></a>Temporale Tabelle - sp_xtp_flush_temporal_history
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Ruft die datenleerungsaufgabe, um alle durchgeführten Zeilen aus dem staging in-Memory-Tabelle in die datenträgerbasierte Verlaufstabelle zu verschieben.  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_xtp_flush_temporal_history @schema_name, @object_name  
  
```  
  
## <a name="arguments"></a>Argumente  
 *@schema_name*  
 Der Schemaname für die aktuelle oder temporale Tabelle  
  
 *@object_name*  
 Der Name des die aktuelle oder temporale Tabelle  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder >0 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert Db_owner-Berechtigungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Überlegungen zur Systemleistung bei Verwendung von speicheroptimierten temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)  
  
  
