---
title: MSSQLSERVER_41302 | Microsoft-Dokumentation
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
- 41302 (Database Engine error)
ms.assetid: 01e75618-afec-4232-ba68-93ab7bc31003
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82590136989c70ec171c06ae6a8f1dcc6d919a61
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver41302"></a>MSSQLSERVER_41302
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|41302|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|WRITE_WRITE_CONFLICT|  
|Meldungstext|Für die aktuelle Transaktion wurde versucht, einen Datensatz zu aktualisieren, der aktualisiert wurde, nachdem diese Transaktion gestartet wurde. Die Transaktion wurde abgebrochen.|  
  
## <a name="explanation"></a>Erklärung  
Bei der Transaktion trat ein Schreibkonflikt auf und die Anweisung wurde beendet.  
  
## <a name="user-action"></a>Benutzeraktion  
Wiederholen Sie den Vorgang später in einer anderen Transaktion. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Siehe auch  
[In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

