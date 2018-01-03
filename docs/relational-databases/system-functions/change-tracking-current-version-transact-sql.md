---
title: CHANGE_TRACKING_CURRENT_VERSION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_CURRENT_VERSION_TSQL
- CHANGE_TRACKING_CURRENT_VERSION
dev_langs: TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_CURRENT_VERSION
- CHANGE_TRACKING_CURRENT_VERSION
ms.assetid: 3027c4f7-6b4d-4089-a369-5926e8a8da1c
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a560013a52a801b6b2ddf29050218f2370307717
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="changetrackingcurrentversion-transact-sql"></a>CHANGE_TRACKING_CURRENT_VERSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Version zurück, die mit der letzten Transaktion, für die ein Commit ausgeführt wurde, verknüpft ist. Diese Version kann verwendet werden, wenn Sie Änderungen auflisten, mit [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CHANGE_TRACKING_CURRENT_VERSION ( )  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 **bigint**  
  
## <a name="remarks"></a>Hinweise  
 Gibt NULL zurück, wenn die Änderungsnachverfolgung für die Datenbank nicht aktiviert ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine lokale Variable, `@next_baseline`, zum Speichern der aktuellen Version von Überarbeitungen deklariert, und anschließend die Funktion `CHANGE_TRACKING_CURRENT_VERSION()` zum Abrufen des Werts für die Variable verwendet.  
  
```sql  
DECLARE @next_baseline bigint;  
SET @next_baseline = CHANGE_TRACKING_CURRENT_VERSION();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Änderungsnachverfolgungsfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
