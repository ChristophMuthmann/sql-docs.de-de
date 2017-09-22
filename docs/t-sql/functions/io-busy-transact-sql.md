---
title: '@@IO_BUSY (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@IO_BUSY'
- '@@IO_BUSY_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- ticks [SQL Server]
- I/O [SQL Server], time spent performing operations
- '@@IO_BUSY function'
- output operations [SQL Server]
- input operations [SQL Server]
- time [SQL Server], I/O operations
ms.assetid: 3c26770c-41ae-4e34-8c82-7bef920ffbca
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 48e1bcd5a80825715ad6aed8649dad843e92c1ea
ms.contentlocale: de-de
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40iobusy-transact-sql"></a>& #x 40; & #x 40; IO_BUSY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Zeit zurück, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seit dem letzten Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für Eingabe- und Ausgabevorgänge aufgewendet hat. Das Ergebnis wird in CPU-Zeitinkrementen ("Takten") angegeben und ist für alle CPUs kumulativ. Somit kann die tatsächlich verstrichene Zeit überschritten werden. Multiplizieren mit@TIMETICKS in Mikrosekunden konvertiert.  
  
> [!NOTE]  
>  Wenn die Zeit in zurückgegeben,@CPU_BUSY, oder @@IO_BUSY ca. 49 Tage Kumulierte CPU-Zeit überschreitet, erhalten Sie eine arithmetische überlaufwarnung ausgegeben. In diesem Fall wird der Wert des @@CPU_BUSY, @@IO_BUSY und @@IDLE Variablen sind nicht genau.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@IO_BUSY  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **integer**  
  
## <a name="remarks"></a>Hinweise  
 Für die Anzeige eines Berichts, der mehrere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Statistiken enthält, führen Sie sp_monitor aus.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Anzahl von Millisekunden zurückgegeben, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für Eingabe/Ausgabe-Vorgänge zwischen der Startzeit und der aktuellen Zeit angewendet hat. Um arithmetischen Überlauf zu vermeiden, wenn die Werte in Mikrosekunden konvertiert, das Beispiel konvertiert einen der Werte, die **"float"** -Datentyp.  
  
```  
SELECT @@IO_BUSY*@@TIMETICKS AS 'IO microseconds',   
   GETDATE() AS 'as of';  
```  
  
 Es folgt ein Standardresultset:  
  
```  
  
IO microseconds as of                   
--------------- ----------------------  
4552312500      12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. dm_os_sys_info &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [@@CPU_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [Sp_monitor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Statistische Systemfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

