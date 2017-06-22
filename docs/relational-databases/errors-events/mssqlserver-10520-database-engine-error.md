---
title: MSSQLSERVER_10520 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 57ba200cf6381ddc6d100d516bcf5f0168bb7262
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10520"></a>MSSQLSERVER_10520
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10520|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PG_PARAM_NOT_ALLOWED|  
|Meldungstext|Die Planhinweisliste „%.*ls“ kann nicht erstellt werden, weil @type als „%ls“ angegeben und ein Wert ungleich NULL für den „%ls“-Parameter festgelegt wurde. Dieser Typ erfordert einen NULL-Wert für den Parameter. Geben Sie NULL für den Parameter an, oder ändern Sie den Typ in einen Typ, der Werte ungleich NULL für den Parameter zulässt.|  
  
## <a name="explanation"></a>Erklärung  
Der in @type angegebene Typ erfordert einen Wert NULL für den angegebenen Parameter. Es wurde jedoch ein Wert ungleich NULL angegeben.  
  
## <a name="user-action"></a>Benutzeraktion  
Geben Sie NULL für den Parameter an, oder ändern Sie den Typ in einen Typ, der Werte ungleich NULL für den Parameter zulässt.  
  
## <a name="see-also"></a>Siehe auch  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Planhinweislisten](~/relational-databases/performance/plan-guides.md)  
  

