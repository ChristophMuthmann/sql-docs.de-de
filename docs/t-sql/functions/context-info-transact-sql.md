---
title: CONTEXT_INFO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd261b2f7f1cc4234792bec66c3662d6d9b8dcd8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die **Context_info** für die aktuelle Sitzung oder einen Batch mit festgelegter Wert der [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) Anweisung.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>Rückgabewert
Der Wert der **Context_info**.
  
Wenn **Context_info** wurde nicht festgelegt:
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt NULL zurück.  
-   In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] gibt einen eindeutigen sitzungsspezifischen GUID zurück.  
  
## <a name="remarks"></a>Hinweise  
MARS (Multiple Active Result Set) ermöglicht Anwendungen die Ausführung mehrerer Batches oder Anforderungen zur gleichen Zeit über dieselbe Verbindung. Führt einer der Batches in einer MARS-Sitzung SET CONTEXT_INFO aus, wird der neue Kontextwert von der CONTEXT_INFO-Funktion zurückgegeben, wenn sie im gleichen Batch wie die SET-Anweisung ausgeführt wird. Der neue Wert wird von der in einer oder mehreren der anderen Batches der Sitzung ausgeführten CONTEXT_INFO-Funktion nur dann zurückgegeben, wenn diese nach dem Beenden des Batches, der die SET-Anweisung ausführte, gestartet wurden.
  
## <a name="permissions"></a>Berechtigungen  
Benötigt keine besonderen Berechtigungen. Die Kontextinformationen befindet sich auch in der **Sys. dm_exec_requests**, **Sys. dm_exec_sessions**, und **sys.sysprocesses** Systemsichten, jedoch direkte Abfrage der Sichten benötigt SELECT- und VIEW SERVER STATE-Berechtigungen.
  
## <a name="examples"></a>Beispiele  
Im folgenden einfachen Beispiel wird die **Context_info** Wert `0x1256698456`, und verwendet dann die `CONTEXT_INFO` Funktion zum Abrufen des Werts.
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[SET CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  

