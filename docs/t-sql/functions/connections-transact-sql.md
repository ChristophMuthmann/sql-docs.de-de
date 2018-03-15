---
title: '@@CONNECTIONS (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CONNECTIONS'
- '@@CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CONNECTIONS function'
- connections [SQL Server], number of
- connections [SQL Server], attempted
- number of connection attempts
- attempted connections
ms.assetid: c59836a8-443c-4b9a-8b96-8863ada97ac7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8422da0d4e550c99fac6c9659f771ab98196cb4a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Gibt die Anzahl der erfolgreichen oder nicht erfolgreichen versuchten Verbindungen zurück, die seit dem letzten Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgetreten sind.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>Rückgabetypen
**integer**
  
## <a name="remarks"></a>Remarks  
Verbindungen sind nicht von Benutzern abhängig. Anwendungen können z. B. mehrere Verbindungen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] öffnen, ohne dass der Benutzer diese Verbindungen wahrnimmt.
  
Sie können einen Bericht mit mehreren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Statistiken anzeigen, einschließlich der Verbindungsversuche, indem Sie **sp_monitor** ausführen.
  
@@MAX_CONNECTIONS gibt die maximale Anzahl von Verbindungen mit dem Server an, die gleichzeitig zulässig sind. @@CONNECTIONS wird bei jedem Anmeldeversuch inkrementiert, daher kann @@CONNECTIONS größer sein als @@MAX_CONNECTIONS.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird die Anzahl der Anmeldeversuche bis zum aktuellen Datum und der aktuellen Uhrzeit angezeigt.
  
```sql
SELECT GETDATE() AS 'Today''s Date and Time',   
@@CONNECTIONS AS 'Login Attempts';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
Today's Date and Time  Login Attempts  
---------------------- --------------  
12/5/2006 10:32:45 AM  211023         
```  
  
## <a name="see-also"></a>Siehe auch
[System Statistical Functions &#40;Transact-SQL&#41; (Statistische Systemfunktionen (Transact-SQL))](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)
  
  
