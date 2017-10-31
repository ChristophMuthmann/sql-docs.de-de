---
title: '@@TOTAL_WRITE (Transact-SQL) | Microsoft Docs'
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
- '@@TOTAL_WRITE'
- '@@TOTAL_WRITE_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- write activity since last started [SQL Server]
- number of disk writes
- '@@TOTAL_WRITE function'
- disks [SQL Server], numbr of disk writes
- total write [SQL Server]
ms.assetid: cd528126-51ee-4aa4-a21f-f32ce5c80fac
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 1c0d3e0e7fb4029eda62f17fb2abd297ae1284a3
ms.contentlocale: de-de
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40totalwrite-transact-sql"></a>& #x 40; & #x 40; TOTAL_WRITE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Anzahl der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seit dem letzten Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführten Schreibzugriffe auf den Datenträger zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
@@TOTAL_WRITE  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **integer**  
  
## <a name="remarks"></a>Hinweise  
 Zum Anzeigen eines Berichts mit mehreren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Statistiken, einschließlich Lese- und Schreibvorgänge ausführen **Sp_monitor**.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Rückgabe der Gesamtanzahl von Lese- und Schreibzugriffen auf den Datenträger bis zum aktuellen Datum und der aktuellen Uhrzeit angezeigt.  
  
```  
SELECT @@TOTAL_READ AS 'Reads', @@TOTAL_WRITE AS 'Writes', GETDATE() AS 'As of'  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Reads       Writes      As of                   
----------- ----------- ----------------------  
7760        97263       12/5/2006 10:23:00 PM   
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_monitor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Statistische Systemfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)   
 [@@TOTAL_READ &#40;Transact-SQL&#41;](../../t-sql/functions/total-read-transact-sql.md)  
  
  

