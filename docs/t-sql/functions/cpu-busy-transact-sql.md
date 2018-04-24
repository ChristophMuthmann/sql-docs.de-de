---
title: '@@CPU_BUSY (Transact-SQL) | Microsoft-Dokumentation'
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
- '@@CPU_BUSY_TSQL'
- '@@CPU_BUSY'
dev_langs:
- TSQL
helpviewer_keywords:
- CPU [SQL Server]
- status information [SQL Server], CPU
- ticks [SQL Server]
- time [SQL Server], CPU activity
- '@@CPU_BUSY function'
- statistical information [SQL Server], CPU
- CPU [SQL Server], activity
ms.assetid: 81ae0e64-79fa-4a74-9aa5-37045c4cd211
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: da3fd1c4b0e66be485dcf25fdd0b3bdcb0079c6c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="x40x40cpubusy-transact-sql"></a>&#x40;&#x40;CPU_BUSY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Gibt die Zeit zurück, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seit dem letzten Start beansprucht hat. Das Ergebnis wird in CPU-Zeitinkrementen oder "Takten" angegeben. Es ist für alle CPUs kumulativ und kann also höher sein als die tatsächlich abgelaufene Zeit. Führen Sie eine Multiplikation mit @@TIMETICKS durch, um einen Wert in Mikrosekunden zu konvertieren.
  
> [!NOTE]  
>  Wenn die Zeit, die in @@CPU_BUSY oder @@IO_BUSY zurückgegeben wird, ca. 49 Tage der kumulierten CPU-Zeit überschreitet, wird eine Warnung zu einem arithmetischen Überlauf ausgegeben. In diesem Fall sind die Werte der Variablen @@CPU_BUSY, @@IO_BUSY und @@IDLE nicht zutreffend.  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```
@@CPU_BUSY  
```  
  
## <a name="return-types"></a>Rückgabetypen
**integer**
  
## <a name="remarks"></a>Remarks  
Um einen Bericht anzuzeigen, der mehrere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Statistiken enthält, einschließlich der CPU-Aktivität, führen Sie „[sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)“ aus.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel werden die Rückgabewerte der CPU-Aktivität für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum aktuellen Datum und der aktuellen Uhrzeit angezeigt. Damit das Konvertieren des Wertes in Mikrosekunden keinen arithmetischen Überlauf zur Folge hat, wird in dem Beispiel einer der Werte in den Datentyp `float` konvertiert.
  
```sql
SELECT @@CPU_BUSY * CAST(@@TIMETICKS AS float) AS 'CPU microseconds',   
   GETDATE() AS 'As of' ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
CPU microseconds As of
---------------- -----------------------
18406250         2006-12-05 17:00:50.600
```
  
## <a name="see-also"></a>Siehe auch
[sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE &#40;Transact-SQL&#41;](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)  
[Statistische Systemfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  
