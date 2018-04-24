---
title: '@@IDLE (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@IDLE_TSQL'
- '@@IDLE'
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], idle
- ticks [SQL Server]
- '@@IDLE function'
- status information [SQL Server], idle time
- idle time [SQL Server]
ms.assetid: 8f49c62a-8da5-4afd-a5eb-4df8ef8be755
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49606c3f1e144712452bd4d8df66b19598b3ac74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="x40x40idle-transact-sql"></a>&#x40;&#x40;IDLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Zeit zurück, während der sich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seit dem letzten Start im Leerlauf befunden hat. Das Ergebnis wird in CPU-Zeiteinheiten oder "Takten" angegeben. Es ist für alle CPUs kumulativ und kann also höher sein als die tatsächlich abgelaufende Zeit. Führen Sie eine Multiplikation mit @@TIMETICKS durch, um einen Wert in Mikrosekunden zu konvertieren.  
  
> [!NOTE]  
>  Wenn die Zeit, die in @@CPU_BUSY oder @@IO_BUSY zurückgegeben wird, die kumulierte CPU-Zeit um etwa 49 Tage überschreitet, wird eine Warnung zu einem arithmetischen Überlauf ausgegeben. In diesem Fall sind die Werte der Variablen @@CPU_BUSY, @@IO_BUSY und @@IDLE nicht zutreffend.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@IDLE  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 Zur Anzeige eines Berichts, der mehrere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Statistiken enthält, führen Sie **sp_monitor** aus.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie die Millisekunden zurückgegeben werden, während derer sich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zwischen der Startzeit und der aktuellen Zeit im Leerlauf befand. Damit das Konvertieren des Wertes in Mikrosekunden keinen arithmetischen Überlauf zur Folge hat, wird in dem Beispiel einer der Werte in den Datentyp `float` konvertiert.  
  
```  
SELECT @@IDLE * CAST(@@TIMETICKS AS float) AS 'Idle microseconds',  
   GETDATE() AS 'as of';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
I  
Idle microseconds  as of                   
----------------- ----------------------  
8199934           12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [@@CPU_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)   
 [System Statistical Functions &#40;Transact-SQL&#41; (Statistische Systemfunktionen (Transact-SQL))](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
