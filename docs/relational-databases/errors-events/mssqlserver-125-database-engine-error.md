---
title: MSSQLSERVER_125 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: "125"
helpviewer_keywords: 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 490c1814d82718080864427ceca229494390607e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver125"></a>MSSQLSERVER_125
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|125|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name||  
|Meldungstext|CASE-Ausdrücke können nur bis zu %d Ebenen geschachtelt werden.|  
  
## <a name="explanation"></a>Erklärung  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist für CASE-Ausdrücke nur eine Schachtelung von 10 Ebenen zulässig.  
  
## <a name="user-action"></a>Benutzeraktion  
Reduzieren Sie die Anzahl der Ebenen von CASE-Anweisungen auf 10 oder weniger.  
  
## <a name="see-also"></a>Siehe auch  
[CASE &#40;Transact-SQL&#41;](~/t-sql/language-elements/case-transact-sql.md)  
  
