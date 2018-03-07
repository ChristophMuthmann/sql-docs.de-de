---
title: '@@TOTAL_READ (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/17/2017
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
- '@@TOTAL_READ_TSQL'
- '@@TOTAL_READ'
dev_langs:
- TSQL
helpviewer_keywords:
- number of disk reads
- disks [SQL Server], number of disk reads
- '@@TOTAL_READ function'
- total read [SQL Server]
- read activity since last started
ms.assetid: b505fbe9-9569-4f3d-80b9-b64b5109ac98
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a062d6e9fab425ead0db82542baeca2c54861aae
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40totalread-transact-sql"></a>&#x40;&#x40;TOTAL_READ (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Anzahl der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seit dem letzten Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführten Lesezugriffe auf den Datenträger, nicht auf den Cache, zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
@@TOTAL_READ  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **integer**  
  
## <a name="remarks"></a>Hinweise  
 Zum Anzeigen eines Berichts mit mehreren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Statistiken, einschließlich Lese- und Schreibvorgänge ausführen **Sp_monitor**.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Rückgabe der Gesamtzahl der Lese- und Schreibzugriffen auf das aktuelle Datum und die Uhrzeit.  
  
```  
SELECT @@TOTAL_READ AS 'Reads', @@TOTAL_WRITE AS 'Writes', GETDATE() AS 'As of';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Reads       Writes      As of                   
----------- ----------- ----------------------  
7760        97263       12/5/2006 10:23:00 PM   
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Statistische Systemfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)   
 [@@TOTAL_WRITE &#40;Transact-SQL&#41;](../../t-sql/functions/total-write-transact-sql.md)  
  
  
