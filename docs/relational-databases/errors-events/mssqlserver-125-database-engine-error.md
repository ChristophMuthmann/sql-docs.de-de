---
title: MSSQLSERVER_125 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c311a94b0af4c36fbcdfc4abefdc175752d5addf
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

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
  

