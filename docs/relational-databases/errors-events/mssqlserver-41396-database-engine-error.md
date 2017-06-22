---
title: MSSQLSERVER_41396 | Microsoft-Dokumentation
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
- 41396 (Database Engine error)
ms.assetid: 4ff04042-8367-46f3-8a16-c94682d6eedb
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1138b36fa3426407b29d928defe7a65179049db0
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver41396"></a>MSSQLSERVER_41396
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|41396|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|MAX_SORT_ROWS_EXCEEDED|  
|Meldungstext|Das Pufferlimit wurde vom Sortiervorgang überschritten. Die Ausführung der gespeicherten Prozedur wurde abgebrochen. Weitere Informationen finden Sie in der SQL Server-Onlinedokumentation.|  
  
## <a name="explanation"></a>Erklärung  
Systemintern kompilierte gespeicherte Prozeduren führen Sortiervorgänge im Arbeitsspeicher aus. Es gibt eine Beschränkung bezüglich der Größe des Sortierungspuffers. Dieser Fehler bewirkt, dass dieser Grenzwert von der Größe des Sortierungspuffers überschritten wird. Der Sortiervorgang und die Ausführung der gespeicherten Prozedur wurden abgebrochen.  
  
Die Größe jeder Zeile bzw. jedes Eintrags im Sortierungspuffer hängt von der Anzahl der sortierten Zeilen, der Anzahl der Joins sowie von der Anzahl und dem Typ der Aggregatfunktionen in der Abfrage ab. Indem Sie die Abfrage vereinfachen, können Sie die Größe jeder Zeile reduzieren, wodurch mehr Zeilen in den Sortierungspuffer passen. Die Größe der Zeilen in den Basistabellen wirkt sich nicht auf die Größe der einzelnen Zeilen oder Einträge im Sortierungspuffer aus.  
  
## <a name="user-action"></a>Benutzeraktion  
Wählen Sie weniger Zeilen aus, oder verringern Sie die Komplexität der Abfrage, indem Sie Joins oder Aggregatfunktionen entfernen.  
  
## <a name="see-also"></a>Siehe auch  
[In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

