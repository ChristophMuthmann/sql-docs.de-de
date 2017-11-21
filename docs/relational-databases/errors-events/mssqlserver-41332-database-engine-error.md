---
title: MSSQLSERVER_41332 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: be21e36f47e2bae00387e1f5aed087c94688f930
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver41332"></a>MSSQLSERVER_41332
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|41332|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQL_SNAPSHOT_NOT_SUPPORTED|  
|Meldungstext|Wenn der TRANSACTION ISOLATION LEVEL der Sitzung auf SNAPSHOT festgelegt ist, kann nicht auf speicheroptimierte Tabellen und systemintern kompilierte gespeicherte Prozeduren zugegriffen werden, und diese können nicht erstellt werden.|  
  
## <a name="explanation"></a>Erklärung  
Die Transaktion wurde auf der Momentaufnahmeisolationsstufe gestartet, und anschließend wurde versucht, eine nicht kompatible Funktion zu verwenden.  
  
## <a name="user-action"></a>Benutzeraktion  
Starten Sie die Transaktion mit einer anderen Isolationsstufe. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Siehe auch  
[In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

