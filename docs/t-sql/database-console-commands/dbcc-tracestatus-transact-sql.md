---
title: DBCC TRACESTATUS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DBCC_TRACESTATUS_TSQL
- DBCC TRACESTATUS
- TRACESTATUS_TSQL
- TRACESTATUS
dev_langs:
- TSQL
helpviewer_keywords:
- global trace flags [SQL Server]
- status information [SQL Server], trace flags
- trace flags [SQL Server], status information
- DBCC TRACESTATUS statement
- session trace flags [SQL Server]
- displaying trace flag status
ms.assetid: 9be51199-78b4-4b87-ae6e-557246b7e29a
caps.latest.revision: 36
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c85cf36412afdda2e050df6159e52c59e96287bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-tracestatus-transact-sql"></a>DBCC TRACESTATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Zeigt den Status der Ablaufverfolgungsflags an.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC TRACESTATUS ( [ [ trace# [ ,...n ] ] [ , ] [ -1 ] ] )   
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
*trace#*  
Die Nummer des Ablaufverfolgungsflags, für das der Status angezeigt wird. Wenn *trace#* und -1 nicht angegeben werden, werden alle für die Sitzung aktivierten Ablaufverfolgungsflags angezeigt.
  
*n*  
Ein Platzhalter, der anzeigt, dass mehrere Ablaufverfolgungsflags angegeben werden können.
  
-1  
Zeigt den Status von global aktivierten Ablaufverfolgungsflags an. Wenn -1 ohne *trace#* angegeben wird, werden alle aktivierten Ablaufverfolgungsflags des Typs global angezeigt.
  
WITH NO_INFOMSGS  
Unterdrückt alle Informationsmeldungen mit einem Schweregrad von 0 bis 10.
  
## <a name="result-sets"></a>Resultsets  
In der folgenden Tabelle finden Sie eine Beschreibung der Informationen des Resultsets:
  
|Spaltenname|Description|  
|---|---|
|**TraceFlag**|Name des Ablaufverfolgungsflags|  
|**Status**|Zeigt an, ob das Ablaufverfolgungsflag entweder global oder für die Sitzung auf ON oder OFF festgelegt wurde.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|**Global**|Zeigt an, ob das Ablaufverfolgungsflag global festgelegt ist.<br /><br /> 1 = True<br /><br /> 0 = False|  
|**Session**|Zeigt an, ob das Ablaufverfolgungsflag für die Sitzung festgelegt ist.<br /><br /> 1 = True<br /><br /> 0 = False|  
  
DBCC TRACESTATUS gibt eine Spalte für die Nummer des Ablaufverfolgungsflags und eine Spalte für den Status zurück. Zeigt an, ob das Ablaufverfolgungsflag auf ON (1) oder OFF (0) festgelegt ist. Die Spaltenüberschrift für die Nummer des Ablaufverfolgungsflags lautet entweder **Global Trace Flag** oder **Session Trace Flag**, je nachdem, ob Sie den Status eines Ablaufverfolgungsflags vom Typ „Global“ oder „Session“ überprüfen.
  
## <a name="remarks"></a>Remarks  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt es zwei Typen von Ablaufverfolgungsflags: Sitzung und global. Ablaufverfolgungsflags des Typs Session werden für eine Verbindung aktiviert und sind nur für diese Verbindung sichtbar. Globale Ablaufverfolgungsflags werden auf Serverebene festgelegt und sind für jede Verbindung auf dem Server sichtbar.
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der **public** -Rolle.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird der Status aller Ablaufverfolgungsflags gezeigt, die zurzeit global aktiviert sind.
  
```sql  
DBCC TRACESTATUS(-1);  
GO  
```  
  
Im folgenden Beispiel wird der Status von Ablaufverfolgungsflags `2528` und `3205` gezeigt.
  
```sql  
DBCC TRACESTATUS (2528, 3205);  
GO  
```  
  
Im folgenden Beispiel wird gezeigt, ob Ablaufverfolgungsflag `3205` global aktiviert ist.
  
```sql  
DBCC TRACESTATUS (3205, -1);  
GO  
```  
  
Im folgenden Beispiel werden alle Ablaufverfolgungsflags gezeigt, die für die aktuelle Sitzung aktiviert sind.
  
```sql  
DBCC TRACESTATUS();  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
