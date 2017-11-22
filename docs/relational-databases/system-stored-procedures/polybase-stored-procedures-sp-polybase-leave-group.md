---
title: "\"sp_polybase_leave_group\" aus (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords: sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f86b26be75bfc5311714c969c9d965152a8acf5f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="polybase-stored-procedures---sppolybaseleavegroup"></a>Gespeicherte PolyBase-Prozeduren - "sp_polybase_leave_group" aus
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Entfernt eine SQL Server-Instanz aus einer PolyBase-Gruppe für horizontale hochskalierungsberechnung an. 
 
 SQL Server-Instanz benötigen den [PolyBase-Leitfaden](../../relational-databases/polybase/polybase-guide.md) Feature installiert.  PolyBase ermöglicht die Integration von nicht - SQL Server-Datenquellen, z. B. Hadoop und Azure Blob-Speicher. Siehe auch [Sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="remarks"></a>Hinweise  
 Sie können nur als Computeknoten aus einer Gruppe entfernen.  
  
 Starten Sie nach dem Ausführen der gespeicherten Prozedur, auf dem Computer das PolyBase-Modul und PolyBase-Datenverschiebungsdienst neu. So überprüfen die folgende DMV auf dem Hauptknoten ausführen: **sys.dm_exec_compute_nodes**.  
  
## <a name="example"></a>Beispiel  
 Im Beispiel wird den aktuellen Computer aus einer PolyBase-Gruppe entfernt.  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
