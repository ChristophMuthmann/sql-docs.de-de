---
title: CONTEXT_INFO (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONTEXT_INFO_TSQL
- CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- CONTEXT_INFO function
- Multiple Active Result Sets
- context information [SQL Server]
- MARS [SQL Server]
- session context information [SQL Server]
ms.assetid: 571320f5-7228-4b0e-9d01-ab732d2d1eab
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 98a275622a809b3856b66d825cd48e2698fea51b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt den **context_info**-Wert zurück, der für die aktuelle Sitzung bzw. den aktuellen Batch mithilfe der [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md)-Anweisung festgelegt wurde.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>Rückgabewert
Der Wert von **context_info**.
  
Wenn **context_info** nicht festgelegt wurde:
-   Wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULL zurückgegeben.  
-   Wird in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ein eindeutiger sitzungsspezifischer GUID zurückgegeben.  
  
## <a name="remarks"></a>Remarks  
MARS (Multiple Active Result Set) ermöglicht Anwendungen die Ausführung mehrerer Batches oder Anforderungen zur gleichen Zeit über dieselbe Verbindung. Führt einer der Batches in einer MARS-Sitzung SET CONTEXT_INFO aus, wird der neue Kontextwert von der CONTEXT_INFO-Funktion zurückgegeben, wenn sie im gleichen Batch wie die SET-Anweisung ausgeführt wird. Der neue Wert wird von der in einer oder mehreren der anderen Batches der Sitzung ausgeführten CONTEXT_INFO-Funktion nur dann zurückgegeben, wenn diese nach dem Beenden des Batches, der die SET-Anweisung ausführte, gestartet wurden.
  
## <a name="permissions"></a>Berechtigungen  
Benötigt keine besonderen Berechtigungen. Die Kontextinformationen werden auch in den Systemansichten **sys.dm_exec_requests**, **sys.dm_exec_sessions** und **sys.sysprocesses** gespeichert. Allerdings sind für die direkte Abfrage der Sichten die SELECT- und VIEW SERVER STATE-Berechtigungen erforderlich.
  
## <a name="examples"></a>Beispiele  
Im folgenden einfachen Beispiel wird der **context_info**-Wert auf `0x1256698456` festgelegt und der Wert dann mithilfe der `CONTEXT_INFO`-Funktion abgerufen.
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
