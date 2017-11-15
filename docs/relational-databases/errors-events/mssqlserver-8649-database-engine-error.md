---
title: MSSQLSERVER_8649 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 065e943af721367f648a81b1c4e44c5a2ecc358c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver8649"></a>MSSQLSERVER_8649
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|8649|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|COST_TOO_HIGH|  
|Meldungstext|Die Abfrage wurde abgebrochen, da die geschätzten Kosten der Abfrage (%d) den konfigurierten Schwellenwert %d überschreiten. Wenden Sie sich an den Systemadministrator.|  
  
## <a name="explanation"></a>Erklärung  
Die Abfrage wurde abgebrochen, weil die geschätzten Kosten dieser Abfrage den für QUERY_GOVERNOR_COST_LIMIT festgelegten konfigurierten Schwellenwert überschreiten.  
  
## <a name="user-action"></a>Benutzeraktion  
Setzen Sie die Option QUERY_GOVERNOR_COST_LIMIT auf einen höheren Wert.  
  
## <a name="see-also"></a>Siehe auch  
[SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](~/t-sql/statements/set-query-governor-cost-limit-transact-sql.md)  
  
